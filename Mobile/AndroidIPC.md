# 多进程启动方式和注意点

## 启动方式

+ 给四大组件在AndroidManifest中指定android:process属性.
+ 通过JNI在native层去fork一个进程

## 命名方式
+ 进程名以:开头的进程属于当前应用的私有进程,其他应用的组件不可以和他跑在同一个进程
+ 进程名不以:开头的进程属于全局进程,其他应用通过ShareUID方式可以和他跑在同一个进程
Android系统为每一个应用分配一个唯一的UID,具体相同UID的应用才能共享数据,两个应用通过ShareUID跑在同一个进程是要有要求的,需要这两个应用有相同的ShareUID并且签名一样。这样才能访问对方的私有数据。

## 注意点
+ 静态成员和单例模式完全失效
+ 线程同步机制完全失效
+ SharePreferences的可靠性下降
+ Application会多次创建

# 跨进程通信方式

## 使用Intent跨进程通信

- Activity，Service，Receiver 都支持在 Intent 中传递 Bundle 数据，而 Bundle 实现了 Parcelable 接口，可以在不同的进程间进行传输。
- 在一个进程中启动了另一个进程的 Activity，Service 和 Receiver ，可以在 Bundle 中附加要传递的数据通过 Intent 发送出去

## 使用文件共享跨进程通信

- Windows 上，一个文件如果被加了排斥锁会导致其他线程无法对其进行访问，包括读和写；而 Android 系统基于 Linux ，使得其并发读取文件没有限制地进行，甚至允许两个线程同时对一个文件进行读写操作，尽管这样可能会出问题。
- 可以在一个进程中序列化一个对象到文件系统中，在另一个进程中反序列化恢复这个对象（注意：并不是同一个对象，只是内容相同。）。
- SharedPreferences 是个特例，系统对它的读 / 写有一定的缓存策略，即内存中会有一份 ShardPreferences 文件的缓存，系统对他的读 / 写就变得不可靠，当面对高并发的读写访问，SharedPreferences 有很多大的几率丢失数据。因此，IPC 不建议采用 SharedPreferences

## 使用Messenger跨进程通信

- Messenger 是一种轻量级的 IPC 方案，它的底层实现是 AIDL ，可以在不同进程中传递 Message 对象，它一次只处理一个请求，在服务端不需要考虑线程同步的问题，服务端不存在并发执行的情形
- 实现步骤
  1. 服务端进程
```java
//作为服务端,用来接收客户端的消息,并且也可以回复消息
    private static class MessengerHandler extends Handler {

        @Override
        public void handleMessage(@NonNull Message msg) {
            if (msg.what == 0x1) {
                Logutil.d(msg.getData().getString("key"));


                //获取客户端传来的Messenger对象,并向其回复消息
                Messenger clientMessenger = msg.replyTo;
                Message message = new Message();
                Bundle bundle = new Bundle();
                bundle.putString("key", "服务端收到消息,稍后再回复你");
                message.what = 0x2;
                message.setData(bundle);
                try {
                    clientMessenger.send(message);
                } catch (RemoteException e) {
                    e.printStackTrace();
                }
            }

        }
    }

    private static Messenger messenger = new Messenger(new MessengerHandler());

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return messenger.getBinder();
    }
```
  2. 客户端进程
```java
Intent intent = new Intent(MainActivity.this, ipcService.class);
bindService(intent, connection, BIND_AUTO_CREATE);

//作为客户端,向服务端发送消息
    private ServiceConnection connection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            //向服务端发送消息
            messenger = new Messenger(iBinder);
            Bundle bundle = new Bundle();
            bundle.putString("key", "客户端给你发消息了");
            Message message = new Message();
            message.what = 0x1;
            message.setData(bundle);

            //将接收服务端回复的Messager传递给服务端
            message.replyTo = mGetRelpyMessager;
            try {
                messenger.send(message);
            } catch (RemoteException e) {
                e.printStackTrace();
            }
        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {

        }
    };

    //接收服务端回复的消息
    private static class MessengerHandler extends Handler {

        @Override
        public void handleMessage(@NonNull Message msg) {
            if (msg.what == 0x2) {
                Logutil.d(msg.getData().getString("key"));
            }

        }
    }

    private Messenger messenger;

    private Messenger mGetRelpyMessager = new Messenger(new MessengerHandler());
```

## 使用AIDL跨进程通信

### Messenger缺点:
+ Messenger 是以串行的方式处理客户端发来的消息，如果大量消息同时发送到服务端，服务端只能一个一个处理
+ 大量并发请求就不适合用 Messenger 
+ Messenger 只适合传递消息，不能跨进程调用服务端的方法。

### AIDL优点
+ AIDL 可以解决并发和跨进程调用方法的问题，要知道 Messenger 本质上也是 AIDL ，只不过系统做了封装方便上层的调用而已。

### AIDL 文件支持的数据类型
+ 基本数据类型
+ String和CharSequence
+ List(只支持ArrayList,里面每个元素都能必须被AIDL支持)
+ Map(只支持HashMap,里面每个元素都能必须被AIDL支持,包括key和value)
+ Parcelable(所有实现了Parcelable接口的对象)
+ AIDL(所有的AIDL接口本身也可以再AIDL文件中使用)

### 注意点
+ import相关的aidl类或者Parcelable类
+ 对于Parcelable作为函数参数的情况，需要添加 in, out或者inout参数修饰
关于in, out和inout三者之间的区别，请参考
https://blog.csdn.net/luoyanglizi/article/details/51958091
+ aidl接口中只支持方法，不支持声明静态变量。这一点不同于传统的接口

### 操作步骤（双向通信）

+ [android之AIDL跨进程通信详解 (四)AIDL中RemoteCallbackList的使用及权限验证方式](https://blog.csdn.net/q610098308/article/details/80939393)
+ [AIDL实现进程间通信](https://blog.csdn.net/ding3106/article/details/83506819)

#### 操作AIDL

右击工程main/java目录下的包名，New -> AIDL -> AIDL File，根据弹出的窗口，命名 Parcelable 数据封装类的类名，以 "Book" 为例，生成 Book.aidl 文件。生成的aidl文件默认保存在main/java的同级aidl目录（新生成）下。默认生成的Book.aidl中Book是Interface类型，修改为parcelable关键字，注意首字母是小写

1. Book.aidl

```java
// Book.aidl
package com.lucky.learn;

// Declare any non-default types here with import statements

parcelable Book; //表示这是个序列号对象
```

2. IBookManager.aidl

```java
// IBookManager.aidl
package com.lucky.learn;
import com.lucky.learn.Book;
import com.lucky.learn.AddBookListener;
interface IBookManager {
    //basicTypes 方法是示例，意思是支持的基本数据类型，可以直接删除
    void basicTypes(int anInt, long aLong, boolean aBoolean, float aFloat,
            double aDouble, String aString);

    List<Book> getBookList();  //获取所有的书

    void addBook(in Book book); //添加书

    //我想每添加一本书都能通知客户端
    void registerListener(AddBookListener listener);  //注册回调接口
    void unregisterListener(AddBookListener listener); //解除回调接口
}
```
3. AddBookListener.aidl

```java
// AddBookListener.aidl
package com.lucky.learn;
import com.lucky.learn.Book;
// Declare any non-default types here with import statements

interface AddBookListener {
    void onAddBookListener(in Book book);
}
```

+ Book.java（再次右击工程 main/java 目录下的包名（此包要和aidl中的包名保持一致），New -> Java Class，在弹出的窗口中输入和步骤一中同名的类名，并实现Parcelable 接口。）
```java
package com.lucky.learn;

import android.os.Parcel;
import android.os.Parcelable;

public class Book implements Parcelable {

    private int bookId;
    private String bookName;

    public Book(int bookId, String bookName) {
        this.bookId = bookId;
        this.bookName = bookName;
    }

    protected Book(Parcel in) {
        bookId = in.readInt();
        bookName = in.readString();
    }

    public static final Creator<Book> CREATOR = new Creator<Book>() {
        @Override
        public Book createFromParcel(Parcel in) {
            return new Book(in);
        }

        @Override
        public Book[] newArray(int size) {
            return new Book[size];
        }
    };

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel parcel, int i) {
        parcel.writeInt(bookId);
        parcel.writeString(bookName);
    }

    @Override
    public String toString() {
        return "Book{" +
                "bookId=" + bookId +
                ", bookName='" + bookName + '\'' +
                '}';
    }
}
```
#### 操作客户端和服务端
+ 服务端（ServerService.java）
```java
package com.lucky.learn.service;

import android.app.Service;
import android.content.Intent;
import android.os.Binder;
import android.os.IBinder;
import android.os.RemoteCallbackList;
import android.os.RemoteException;
import android.util.Log;

import com.lucky.learn.AddBookListener;
import com.lucky.learn.Book;
import com.lucky.learn.IBookManager;

import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class ServerService extends Service {

    private CopyOnWriteArrayList<Book> books = new CopyOnWriteArrayList<>();
    //通过系统提供的类来注册和解除回调
    private RemoteCallbackList<AddBookListener> addBookListenerRemoteCallbackList = new RemoteCallbackList<>();

    public ServerService() {
    }

    private final Binder binder = new IBookManager.Stub() {
        @Override
        public void basicTypes(int anInt, long aLong, boolean aBoolean, float aFloat, double aDouble, String aString) throws RemoteException {

        }

        @Override
        public List<Book> getBookList() throws RemoteException {
            return books;
        }

        @Override
        public void addBook(Book book) throws RemoteException {
            books.add(book);
            int pid = android.os.Process.myPid();
            Log.d("FFF", "收到客户端消息：" + book.toString() + "," + pid);
            callBackBook(book);  //收到消息,回调给客户端
        }

        @Override
        public void registerListener(AddBookListener listener) throws RemoteException {
            if (listener != null) {
                addBookListenerRemoteCallbackList.register(listener);
            }
        }

        @Override
        public void unregisterListener(AddBookListener listener) throws RemoteException {
            if (listener != null) {
                addBookListenerRemoteCallbackList.unregister(listener);
            }
        }
    };

    private void callBackBook(Book book) {
        final int N = addBookListenerRemoteCallbackList.beginBroadcast(); //可能有多个客户端存在
        for (int i = 0; i < N; i++) {
            try {
                addBookListenerRemoteCallbackList.getBroadcastItem(i).onAddBookListener(book);
            } catch (RemoteException e) {
                e.printStackTrace();
            }
        }
        addBookListenerRemoteCallbackList.finishBroadcast();

    }

    @Override
    public IBinder onBind(Intent intent) {
        return binder;
    }

    @Override
    public void onCreate() {
        super.onCreate();
    }
}
```
+ 客户端（MainActivity.java）
```java
Intent intent = new Intent(MainActivity.this, aidlService.class);
bindService(intent, aidiConn, BIND_AUTO_CREATE);

public class MainActivity extends AppCompatActivity {

    private IBookManager iBookManager;

    private final AddBookListener addBookListener = new AddBookListener.Stub() {
        @Override
        public void onAddBookListener(Book book) throws RemoteException {
            int pid = android.os.Process.myPid();
            Log.d("FFF", "收到服务端消息：" + book.toString() + "," + pid);
        }
    };

    private final ServiceConnection serviceConnection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            iBookManager = IBookManager.Stub.asInterface(iBinder);
            try {
                iBookManager.registerListener(addBookListener);
            } catch (RemoteException e) {
                Log.d("FFF", e.getMessage());
            }
        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {

        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bindService(new Intent(this, ServerService.class), serviceConnection, BIND_AUTO_CREATE);

        //添加book
        if (iBookManager != null) {
                    try {
                        iBookManager.addBook(new Book(3, "10"));

                        //List<Book> bookList = iBookManager.getBookList();
                        //Log.d("FFF", bookList.toString());
                    } catch (RemoteException e) {
                        Log.d("FFF", e.getMessage());
                    }
                }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();

        //解绑
        if (iBookManager != null && iBookManager.asBinder().isBinderAlive()) {
            try {
                iBookManager.unregisterListener(addBookListener);
            } catch (RemoteException e) {
                e.printStackTrace();
            }
        }
        unbindService(serviceConnection);
    }
```

#### 不同App调用(另一个App要将包以及包下的所有文件都复制过去)
+ 客户端调用
```java
Intent intent = new Intent();
//通过隐式启动来连接第二个App
//保证连接的App的配置文件android:exported="true"
intent.setComponent(new ComponentName("com.lucky.newsandroid", "com.lucky.newsandroid.ui.service.aidlService"));
bindService(intent, aidiConn, BIND_AUTO_CREATE);

private ServiceConnection aidiConn = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            IBookManager iBookManager = IBookManager.Stub.asInterface(iBinder);
            try {
                List<Book> bookList = iBookManager.getBookList();
                Log.d("FFF", bookList.toString());
            } catch (RemoteException e) {
                e.printStackTrace();
            }
        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {

        }
    };

```

#### 权限控制(通过权限来限制其他客户端的访问)

## 使用ContentProvider跨进程

+ 用于不同应用间数据共享和 Messenger 底层实现同样是 Binder 和 AIDL，系统做了封装，使用简单。 
+ 系统预置了许多 ContentProvider ，如通讯录、日程表，需要跨进程访问。 
+ 使用方法：继承 ContentProvider 类实现 6 个抽象方法，这六个方法均运行在 ContentProvider 进程中，除 onCreate 运行在主线程里，其他五个方法均由外界回调运行在 Binder 线程池中。
+ ContentProvider 的底层数据，可以是 SQLite 数据库，可以是文件，也可以是内存中的数据。

### 操作步骤
+ 自定义ContentProvider
```
package com.lucky.newsandroid.ui.provider;

import android.content.ContentProvider;
import android.content.ContentValues;
import android.content.Context;
import android.content.UriMatcher;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.net.Uri;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;

import com.lucky.newsandroid.db.DBOpenHelper;
import com.lucky.newsandroid.utils.Logutil;

/**
 * 作者：jacky on 2019/9/26 17:07
 * 邮箱：jackyli706@gmail.com
 */
public class BookProvider extends ContentProvider {

    private static final String AUTHORITY = "com.lucky.newsandroid.book.provider";
    public static final Uri BOOK_CONTENT_URI = Uri.parse("content://" + AUTHORITY + "/book");
    public static final Uri USER_CONTENT_URI = Uri.parse("content://" + AUTHORITY + "/user");

    public static final int BOOK_URI_CODE = 0;
    public static final int USER_URI_CODE = 1;

    private static final UriMatcher sUriMatcher = new UriMatcher(UriMatcher.NO_MATCH);

    static {
        //分别为book和user指定Uri
        sUriMatcher.addURI(AUTHORITY, "book", BOOK_URI_CODE);
        sUriMatcher.addURI(AUTHORITY, "user", USER_URI_CODE);
    }

    private Context context;
    private SQLiteDatabase mDb;

    //运行在主线程中,不要做耗时操作
    @Override
    public boolean onCreate() {
        Logutil.d("onCreate,当前线程:" + Thread.currentThread().getName());
        context = getContext();

        //演示所用,不推荐在UI线程进行耗时操作
        initProviderData();
        return false;
    }

    //初始化数据库数据
    private void initProviderData() {
        mDb = new DBOpenHelper(context).getWritableDatabase();
        //删除两张表的数据
        mDb.execSQL("delete from " + DBOpenHelper.BOOK_TABLE_NAME);
        mDb.execSQL("delete from " + DBOpenHelper.USER_TABLE_NAME);
        //添加数据
        mDb.execSQL("insert into book values(1,'Android')");
        mDb.execSQL("insert into book values(2,'IOS')");
        mDb.execSQL("insert into book values(3,'WEB')");
        mDb.execSQL("insert into user values(1,'jack',10)");
        mDb.execSQL("insert into user values(2,'lison',20)");

    }

    @Nullable
    @Override
    public Cursor query(@NonNull Uri uri, @Nullable String[] strings, @Nullable String s, @Nullable String[] strings1, @Nullable String s1) {
        Logutil.d("query,当前线程:" + Thread.currentThread().getName());
        String table = getTableName(uri);
        return mDb.query(table, strings, s, strings1, null, null, s1, null);
    }

    @Nullable
    @Override
    public String getType(@NonNull Uri uri) {
        return null;
    }

    @Nullable
    @Override
    public Uri insert(@NonNull Uri uri, @Nullable ContentValues contentValues) {
        String table = getTableName(uri);
        mDb.insert(table, null, contentValues);
        context.getContentResolver().notifyChange(uri, null);
        return uri;
    }

    @Override
    public int delete(@NonNull Uri uri, @Nullable String s, @Nullable String[] strings) {
        String table = getTableName(uri);
        int count = mDb.delete(table, s, strings);
        if (count > 0) {
            context.getContentResolver().notifyChange(uri, null);
        }
        return count;
    }

    @Override
    public int update(@NonNull Uri uri, @Nullable ContentValues contentValues, @Nullable String s, @Nullable String[] strings) {
        String table = getTableName(uri);
        int row = mDb.update(table, contentValues, s, strings);
        if (row > 0) {
            context.getContentResolver().notifyChange(uri, null);
        }
        return row;
    }

    //获取数据库表
    private String getTableName(Uri uri) {
        String tableName = null;
        switch (sUriMatcher.match(uri)) {
            case BOOK_URI_CODE:
                tableName = DBOpenHelper.BOOK_TABLE_NAME;
                break;
            case USER_URI_CODE:
                tableName = DBOpenHelper.USER_TABLE_NAME;
                break;
        }
        return tableName;
    }
}

```
```
<provider

            android:authorities="com.lucky.newsandroid.book.provider"
            android:name=".ui.provider.BookProvider"
            android:permission="com.lucky.PROVIDER"
            android:process=":provider"/>
```

+ 自定义数据库管理
```
package com.lucky.newsandroid.db;

import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

/**
 * 作者：jacky on 2019/9/26 17:24
 * 邮箱：jackyli706@gmail.com
 *
 * 进行数据的创建升级和降级
 */
public class DBOpenHelper extends SQLiteOpenHelper {

    private static final String DB_NAME = "book_provider.db";
    public static final String BOOK_TABLE_NAME = "book";
    public static final String USER_TABLE_NAME = "user";
    private static final int DB_VERSION = 1;


    public DBOpenHelper(@Nullable Context context) {
        super(context, DB_NAME, null, DB_VERSION);
    }


    @Override
    public void onCreate(SQLiteDatabase db) {
        //图书和用户信息表
        String CREATE_BOOK_TABLE = "CREATE TABLE IF NOT EXISTS " + BOOK_TABLE_NAME + "(_id INTEGER PRIMARY KEY," + "name TEXT)";
        db.execSQL(CREATE_BOOK_TABLE);
        String CREATE_USER_TABLE = "CREATE TABLE IF NOT EXISTS " + USER_TABLE_NAME + "(_id INTEGER PRIMARY KEY," + "name TEXT," + "sex TEXT)";
        db.execSQL(CREATE_USER_TABLE);
    }

    @Override
    public void onUpgrade(SQLiteDatabase sqLiteDatabase, int i, int i1) {

    }
}

```
+ 跨进程调用
```
private void startProvide() {
        Uri bookUri = BookProvider.BOOK_CONTENT_URI;
        //插入数据
        ContentValues values = new ContentValues();
        values.put("_id", 6);
        values.put("name", "Spring");
        getContentResolver().insert(bookUri, values);

        //查询数据
        Cursor bookCursor = getContentResolver().query(bookUri, new String[]{"_id", "name"}, null, null, null);
        while (bookCursor.moveToNext()) {
            Logutil.d("bookId:" + bookCursor.getInt(0) + ",bookName:" + bookCursor.getString(1));
        }
        bookCursor.close();

        Uri userUri = BookProvider.USER_CONTENT_URI;
        //插入数据
        values.put("_id", 3);
        values.put("name", "lijie");
        values.put("sex", "1");
        getContentResolver().insert(userUri, values);

        //查询数据
        Cursor userCursor = getContentResolver().query(userUri, new String[]{"_id", "name", "sex"}, null, null, null);
        while (userCursor.moveToNext()) {
            Logutil.d("userId:" + userCursor.getInt(0) + ",userName:" + userCursor.getString(1) + ",userSex:" + userCursor.getInt(2));
        }
        userCursor.close();
    }
```