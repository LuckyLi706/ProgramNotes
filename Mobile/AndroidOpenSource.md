<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [UI](#ui)
- [数据库](#%E6%95%B0%E6%8D%AE%E5%BA%93)
  - [Room](#room)
    - [创建实例](#%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B)
      - [Java](#java)
      - [Kotlin](#kotlin)
    - [创建实体](#%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BD%93)
      - [Java](#java-1)
      - [Kotlin](#kotlin-1)
    - [增删改查](#%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5)
      - [Java](#java-2)
      - [Kotlin](#kotlin-2)
    - [调用](#%E8%B0%83%E7%94%A8)
    - [表关联](#%E8%A1%A8%E5%85%B3%E8%81%94)
      - [嵌套对象](#%E5%B5%8C%E5%A5%97%E5%AF%B9%E8%B1%A1)
      - [一对一](#%E4%B8%80%E5%AF%B9%E4%B8%80)
      - [一对多](#%E4%B8%80%E5%AF%B9%E5%A4%9A)
    - [存储复杂数据（Lst、Map）](#%E5%AD%98%E5%82%A8%E5%A4%8D%E6%9D%82%E6%95%B0%E6%8D%AElstmap)
      - [Java](#java-3)
    - [数据库升级](#%E6%95%B0%E6%8D%AE%E5%BA%93%E5%8D%87%E7%BA%A7)
    - [其他问题](#%E5%85%B6%E4%BB%96%E9%97%AE%E9%A2%98)
- [网络请求](#%E7%BD%91%E7%BB%9C%E8%AF%B7%E6%B1%82)
  - [Volley](#volley)
    - [使用](#%E4%BD%BF%E7%94%A8)
    - [源码](#%E6%BA%90%E7%A0%81)
  - [OkHttp](#okhttp)
    - [使用](#%E4%BD%BF%E7%94%A8-1)
    - [日志拦截器](#%E6%97%A5%E5%BF%97%E6%8B%A6%E6%88%AA%E5%99%A8)
    - [WebSocket](#websocket)
      - [Java](#java-4)
      - [Kotlin](#kotlin-3)
  - [Retrofit](#retrofit)
    - [使用](#%E4%BD%BF%E7%94%A8-2)
    - [Retrofit单例](#retrofit%E5%8D%95%E4%BE%8B)
      - [Java](#java-5)
      - [Kotlin](#kotlin-4)
    - [请求注解](#%E8%AF%B7%E6%B1%82%E6%B3%A8%E8%A7%A3)
    - [配合LiveData](#%E9%85%8D%E5%90%88livedata)
    - [断点下载大文件](#%E6%96%AD%E7%82%B9%E4%B8%8B%E8%BD%BD%E5%A4%A7%E6%96%87%E4%BB%B6)
- [图片加载](#%E5%9B%BE%E7%89%87%E5%8A%A0%E8%BD%BD)
  - [Glide](#glide)
    - [使用](#%E4%BD%BF%E7%94%A8-3)
    - [任意布局加载图片](#%E4%BB%BB%E6%84%8F%E5%B8%83%E5%B1%80%E5%8A%A0%E8%BD%BD%E5%9B%BE%E7%89%87)
    - [修改存储位置和大小](#%E4%BF%AE%E6%94%B9%E5%AD%98%E5%82%A8%E4%BD%8D%E7%BD%AE%E5%92%8C%E5%A4%A7%E5%B0%8F)
- [日志](#%E6%97%A5%E5%BF%97)
    - [Xlog](#xlog)
- [地图](#%E5%9C%B0%E5%9B%BE)
    - [百度](#%E7%99%BE%E5%BA%A6)
      - [获取经纬度](#%E8%8E%B7%E5%8F%96%E7%BB%8F%E7%BA%AC%E5%BA%A6)
- [工具库](#%E5%B7%A5%E5%85%B7%E5%BA%93)
    - [经纬度转换](#%E7%BB%8F%E7%BA%AC%E5%BA%A6%E8%BD%AC%E6%8D%A2)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# UI

+ [悬浮窗](https://github.com/yhaolpz/FloatWindow)
+ [SuperTextView](https://github.com/chenBingX/SuperTextView)
  ```xml
  //设置圆角，可以单独设置圆角
  <com.coorchice.library.SuperTextView
        android:id="@+id/stv_app_name"
        style="@style/StrokeStyle"
        android:layout_width="match_parent"
        android:layout_height="20dp"
        app:stv_solid="#80000000"
        app:stv_corner="6dp"         
        app:stv_left_bottom_corner="true"
        app:stv_right_bottom_corner="true"
        android:gravity="left|center_vertical"
        android:textSize="11sp"
        android:paddingStart="5dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintBottom_toBottomOf="parent" />

  //设置描边
  <style name="StrokeStyle">
        <item name="stv_text_fill_color">@color/white</item>
        <item name="stv_text_stroke">true</item>
        <item name="stv_text_stroke_color">@color/dialog_text_view_stroke</item>
        <item name="stv_text_stroke_width">1dp</item>
        <item name="fontFamily">@font/medium</item>
  </style>      
  ```
+ [权限申请](https://github.com/getActivity/XXPermissions)


# 数据库
## Room
+ [官网](https://developer.android.google.cn/training/data-storage/room)

+ ```groovy
  //Java
  def room_version = "2.3.0"

      implementation "androidx.room:room-runtime:$room_version"
      annotationProcessor "androidx.room:room-compiler:$room_version"

      // optional - RxJava2 support for Room
      implementation "androidx.room:room-rxjava2:$room_version"

      // optional - RxJava3 support for Room
      implementation "androidx.room:room-rxjava3:$room_version"

      // optional - Guava support for Room, including Optional and ListenableFuture
      implementation "androidx.room:room-guava:$room_version"

      // optional - Test helpers
      testImplementation "androidx.room:room-testing:$room_version"

      // optional - Paging 3 Integration
      implementation "androidx.room:room-paging:2.4.0-rc01"

  //Kotlin
  dependencies {
      val roomVersion = "2.3.0"

      implementation("androidx.room:room-runtime:$roomVersion")
      annotationProcessor("androidx.room:room-compiler:$roomVersion")

      // To use Kotlin annotation processing tool (kapt)
      kapt("androidx.room:room-compiler:$roomVersion")
      // To use Kotlin Symbolic Processing (KSP)
      ksp("androidx.room:room-compiler:$roomVersion")

      // optional - Kotlin Extensions and Coroutines support for Room
      implementation("androidx.room:room-ktx:$roomVersion")

      // optional - RxJava2 support for Room
      implementation("androidx.room:room-rxjava2:$roomVersion")

      // optional - RxJava3 support for Room
      implementation("androidx.room:room-rxjava3:$roomVersion")

      // optional - Guava support for Room, including Optional and ListenableFuture
      implementation("androidx.room:room-guava:$roomVersion")

      // optional - Test helpers
      testImplementation("androidx.room:room-testing:$roomVersion")

      // optional - Paging 3 Integration
      implementation("androidx.room:room-paging:2.4.0-rc01")
  }
  ```

### 创建实例

#### Java

```java
//@Database包含数据库持有者，并作为与 App 持久关联数据的底层连接的主要访问点。
@Database(entities = {User.class}, version = 1, exportSchema = false)
public abstract class AppDataBase extends RoomDatabase {

    private static String DB_PATH = FileUtil.getStoragePath("db") + "/" + Constants.DB_NAME;  //自定义数据库路径

    public abstract UserDao getUserDao();

    private static AppDataBase instance;

    public static AppDataBase getInstance() {
        synchronized (AppDataBase.class) {
            if (instance == null) {
                instance = Room.databaseBuilder(GDSApplication.getContext(), AppDataBase.class, DB_PATH).allowMainThreadQueries().addMigrations(MIGRATION_1_2).build();    //初始化数据库,allow表示允许主线程查询,不建议主线程操作
            }
            return instance;
        }
    }
}
```

#### Kotlin

```Kotlin
@Database(entities = [User::class, AppState::class], version = 1, exportSchema = false)
abstract class AppDataBase : RoomDatabase() {

    companion object {
        @Volatile
        private var instance: AppDataBase? = null

        fun getInstance(): AppDataBase {
            return instance ?: synchronized(this) {
                instance ?: buildDatabase().also { instance = it }
            }
        }

        private fun buildDatabase(): AppDataBase {
            return Room.databaseBuilder(
                GameStoreApplication.context,
                AppDataBase::class.java,
                "store.db"   //数据库名字
            ).build()
        }
    }

    abstract fun getUserDao(): UserDao

    abstract fun getApkState(): AppStateDao

}
```

### 创建实体

#### Java

```java
//@Entity注解表示声明实体
//默认数据库表名和实体名一样,实体tableName可以修改数据库名,
//可以使用primaryKeys设置多个主键
@Entity(tableName = "users",primaryKeys = {"firstName", "lastName"})  
public class User {
    @PrimaryKey    //第二种方式设置主键
    public int id;

    @ColumnInfo(name = "first_name")    //设置别名
    public String firstName;
    public String lastName;

    @Ignore   //该注解表示当前字段不入库
    Bitmap picture;
}
```

#### Kotlin

```kotlin
@Entity
class AppState {
    @PrimaryKey(autoGenerate = true)
    var id: Int = 0
    var apkDownLoadState: Int = 0  //当前的下载状态
    var apkCachePath = ""   //apk的缓存地址
    var apkPackageName = "" //apk包名
    var apkUrl: String = "" //apk地址
    var apkMd5: String = "" //apk的md5码
    var apkVersion: String = ""  //包体版本
    var startClass: String = ""  //启动类

    override fun toString(): String {
        return "AppState(id=$id, apkDownLoadState=$apkDownLoadState, apkCachePath='$apkCachePath', apkPackageName='$apkPackageName', apkUrl='$apkUrl', apkMd5='$apkMd5', apkVersion='$apkVersion')"
    }
}
```

### 增删改查

#### Java

```Java
//@Dao注解表示操作数据库的方法
@Dao
public interface UserDao {

    @Insert   //插入注解
    void insertOne(User user);

    @Query("SELECT * FROM User WHERE username = 'admin'")  //查询注解（从User表中查询username为admin的数据）
    List<User> getAdmin();

    //以下是配合RxJava使用的
    @Query("SELECT * FROM User WHERE username = (:name)")
    Maybe<List<User>> getUser(String name);     //配合RxJava使用

    @Update    //更新注解
    Maybe<Integer> updateOneUser(User user);   //更新一条任务数据

    @Insert
    Completable insertOneUser(User user);    //添加一条新的任务

    @Query("Delete FROM User WHERE username = (:name)")
    Single<Integer> deleteOneUser(String name);   //删除一条数据

    @Query("SELECT * FROM User")
    Maybe<List<User>> getAllUser();

    //原始SQL查询,比如数据分页就需要使用原始SQL才可以
    /**
     * 根据条件来查询数据
     * 参考 https://blog.csdn.net/m0_37168878/article/details/83375849
     *
     * @param supportSQLiteQuery 原始SQL
     *  SimpleSQLiteQuery query = new SimpleSQLiteQuery(SQL, new String[]{mSpnTaskName.getText().toString()});  //后面的一个参数为未知参数,参数代表下面的taskName参数,没有就写空数组
     SQL += " AND taskName=?";
            SQL += " order by id desc " + " limit " + MAX_PAGE_COUNT + " offset " + mOffestCount;
            SimpleSQLiteQuery query = new SimpleSQLiteQuery(SQL, new String[]{mSpnTaskName.getText().toString()});
            mPresenter.queryConditionTest(query);
     * @return
     */
    @RawQuery()
    Maybe<List<User>> queryConditionTest(SimpleSQLiteQuery supportSQLiteQuery);
}
```

#### Kotlin

```Kotlin
@Dao
abstract class AppStateDao {
    @Insert
    abstract fun insertApkState(appState: AppState): Long  //插入apk状态

    @Update
    abstract fun updateApkState(appState: AppState): Int //更新apk状态

    @Query("SELECT * FROM appstate WHERE apkPackageName=(:apkPackageName)")
    abstract fun queryApkState(apkPackageName: String): LiveData<AppState>    //配合LiveData使用

    //可以查询子集（新创建一个对象对应数据表的字段）
    data class NameTuple(   //创建一个对象，只包含数据里面的first_name和last_name字段
        @ColumnInfo(name = "first_name") val firstName: String?,
        @ColumnInfo(name = "last_name") val lastName: String?
    )
    @Query("SELECT first_name, last_name FROM user")
    fun loadFullName(): List<NameTuple>   //查询字集
}
```

### 调用

```java
AppDataBase.getInstance().getUserDao().getAdmin();   //（从User表中查询username为admin的数据）

ppDataBase.getInstance().getApkState().queryApkState(apkPackageName) //从ApkState表中查询apkPackageName为apkPackageName的数据
```

### 表关联

#### 嵌套对象

```kotlin
data class Address(
        val street: String?,
        val state: String?,
        val city: String?,
        @ColumnInfo(name = "post_code") val postCode: Int
    )

@Entity
data class User(
        @PrimaryKey val id: Int,
        val firstName: String?,
        @Embedded val address: Address?   //@Embedded 注解表示嵌套Address对象
)

//表示 User 对象的表将包含具有以下名称的列：id、firstName、street、state、city 和 post_code
```

#### 一对一

```kotlin
@Entity
data class User(
   @PrimaryKey val userId: Long,
   val name: String,
   val age: Int
)

@Entity
data class Library(
   @PrimaryKey val libraryId: Long,
   val userOwnerId: Long
)

data class UserAndLibrary(
  @Embedded val user: User,
  @Relation(        //使用@Relation注解来关联两个主键
      parentColumn = "userId",      //表示父实体主键列
      entityColumn = "userOwnerId"  //表示引用父实体主键的子实体列的名称
        )
  val library: Library
)

@Transaction     //需要进行两部操作，确保整个过程原子方式操作
@Query("SELECT * FROM User")
fun getUsersAndLibraries(): List<UserAndLibrary>
```

#### 一对多

```kotlin
@Entity
    data class User(
        @PrimaryKey val userId: Long,
        val name: String,
        val age: Int
    )

    @Entity
    data class Playlist(
        @PrimaryKey val playlistId: Long,
        val userCreatorId: Long,
        val playlistName: String
    )

data class UserWithPlaylists(
        @Embedded val user: User,
        @Relation(
              parentColumn = "userId",
              entityColumn = "userCreatorId"
        )
        val playlists: List<Playlist>
    )

@Transaction
    @Query("SELECT * FROM User")
    fun getUsersWithPlaylists(): List<UserWithPlaylists>
```

### 存储复杂数据（Lst、Map）

Room默认不支持存储复杂数据，可以使用转换器

#### Java

```Java
//
public class SensorInfoConverter {

    @TypeConverter   //将存储的类型转换为我们需要使用的类型
    public static List<SensorInfo> revert(String gasType) {
        // 使用Gson方法把json格式的string转成List
        String[] sensorInfos = gasType.split(":");
        List<SensorInfo> gasTypeInfoList = new ArrayList<>();
        for (String info : sensorInfos) {
            if (!info.equals("")) {
                try {
                    String[] infos = info.split("\\+");
                    SensorInfo sensorInfo = new SensorInfo();
                    sensorInfo.setSpem_port(Integer.parseInt(infos[0]));
                    sensorInfo.setSensor_type(infos[1]);
                    sensorInfo.setBaud_rate(Integer.parseInt(infos[2]));
                    sensorInfo.setMeasure_unit(infos[3]);
                    sensorInfo.setFetch_circle(Long.parseLong(infos[4]));
                    sensorInfo.setTime_out(Long.parseLong(infos[5]));
                    sensorInfo.setPoint(Integer.parseInt(infos[6]));
                    gasTypeInfoList.add(sensorInfo);
                } catch (Exception e) {
                    LogUtil.e(e.getMessage());
                }
            }
        }
        return gasTypeInfoList;
    }

    @TypeConverter   //转换为存储的String类型
    public static String converter(List<SensorInfo> sensorInfoList) {
        // 使用Gson方法把List转成json格式的string，便于我们用的解析
        String value = "";
        if (sensorInfoList == null) {
            return value;
        }
        for (SensorInfo sensorInfo : sensorInfoList) {
            value += sensorInfo.toString();
        }
        return value;
    }
}
```

### 数据库升级

```java
public Migration(int startVersion, int endVersion)  //使用该方法来升级

//Migration有两个参数，startVersion和endVersion。startVersion表示当前版本（手机上安装的版本），endVersion表示将要升级到的版本。如果你的手机中的应用程序数据库的版本为1，那么下方Migration会将你的数据库版本从1升级到2。
static final Migration MIGRATION_1_2 = new Migration(1, 2)
{
    @Override
    public void migrate(@NonNull SupportSQLiteDatabase database)
    {
        //执行升级相关操作
    }
};

//以此类推，如果你的数据库需要从2升级到3，则需要写这样一个Migration。
private static Migration MIGRATION_2_3 = new Migration(2, 3)
{
    @Override
    public void migrate(@NonNull SupportSQLiteDatabase database)
    {
        //执行升级相关操作
    }
};

//如果用户手机上安装的应用程序数据库版本为1，而当前要安装的应用程序数据库版本为3，这种情况该怎么办呢？这种情况下，Room会先判断当前有没有从1->3的Migration升级方案，如果有，就直接执行从1->3的升级方案，如果没有，那么Room会按照顺序先后执行Migration(1, 2)->Migration(2, 3)以完成升级。

//写好Migration之后，我们还需要通过addMigrations()方法，将升级方案添加到Room。
Room.databaseBuilder(context.getApplicationContext(), MyDatabase.class, DATABASE_NAME)
    .addMigrations(MIGRATION_1_2, MIGRATION_2_3, MIGRATION_1_3)
    .build();

//修改数据库的版本（在实例里面）
@Database(entities = {Student.class}, version = 1)

//Schema文件（查看数据库表结构的变化）
//Schema文件是默认导出的，你只需要指定它导出的位置即可。（exportSchema默认为true）
@Database(entities = {Student.class}, exportSchema = true, version = 1)
//设置导出位置
android {
    defaultConfig {
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = ["room.schemaLocation": "$projectDir/schemas".toString()]//指定数据库schema导出的位置
            }
        }
    }
}

//销毁与重建策略（在Sqlite中修改表结构会比较麻烦。比如我们希望将Student表中的age字段类型从INTEGER改为TEXT。）
/**
1.创建一张符合我们要求的临时表temp_Student
2.将数据从旧表Student拷贝至临时表temp_Student
3.删除旧表Student
4.将临时表temp_Student重命名为Student
**/
static final Migration MIGRATION_3_4 = new Migration(3, 4)
    {
        @Override
        public void migrate(SupportSQLiteDatabase database)
        {
            database.execSQL("CREATE TABLE temp_Student (" +
                    "id INTEGER PRIMARY KEY NOT NULL," +
                    "name TEXT," +
                    "age TEXT)");
            database.execSQL("INSERT INTO temp_Student (id, name, age) " +
                    "SELECT id, name, age FROM Student");
            database.execSQL("DROP TABLE Student");
            database.execSQL("ALTER TABLE temp_Student RENAME TO Student");
        }
    };

//添加字段（如果没有提供足够的迁移来从当前版本移动到最新版本，Room 将清除数据库并重新创建。对于 #1，因为仅仅更新了版本号升级，所以Room会把本地的数据库清除并创建，即本地数据库的数据将会丢失，这并不是推荐的操作）
//保留数据库
// 如果数据库有改动，则需要更新数据库版本来同步更新数据库，以下为示例方法：
        private val MIGRATION_1_2 = object : Migration(1, 2) {
            override fun migrate(database: SupportSQLiteDatabase) {
                database.execSQL("ALTER TABLE Bean ADD COLUMN `deletedDate` INTEGER")
                //添加非空字段时，默认值不能为空，即我们添加上默认值即可。如下：DEFAULT
                database.execSQL("ALTER TABLE Bean ADD COLUMN `isDeleted` INTEGER NOT NULL DEFAULT 0")
            }
        }
//重新创建数据库（对之前数据不需要）
private val MIGRATION_1_2 = object : Migration(1, 2) {
            override fun migrate(database: SupportSQLiteDatabase) {
                database.execSQL("DROP TABLE IF EXISTS Bean")
                database.execSQL("CREATE TABLE IF NOT EXISTS `Bean` (`id` INTEGER NOT NULL, `checksum` TEXT NOT NULL, `deletedDate` INTEGER, `isDeleted` INTEGER NOT NULL, PRIMARY KEY(`id`))")
            }
        }
```

### 其他问题

+ Row too big to fit into CursorWindow

  ```java
  /**
       * 修复Row too big to fit into CursorWindow（上限为2M）
       * <p>
       * https://www.it-swarm.dev/zh/android/sqlite-android%E6%95%B0%E6%8D%AE%E5%BA%93%E6%B8%B8%E6%A0%87%E7%AA%97%E5%8F%A3%E5%88%86%E9%85%8D2048-kb%E5%A4%B1%E8%B4%A5/1068546317/
       */
      private static void fix() {
          try {
              Field field = CursorWindow.class.getDeclaredField("sCursorWindowSize");
              field.setAccessible(true);
              field.set(null, 102400 * 1024); //the 102400 is the new size added
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  ```

# 网络请求

## Volley

### 使用

```java
package com.lucky.newsandroid.network;

import android.content.Context;
import android.graphics.Bitmap;
import android.util.LruCache;
import android.widget.ImageView;

import com.android.volley.AuthFailureError;
import com.android.volley.DefaultRetryPolicy;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.ImageLoader;
import com.android.volley.toolbox.ImageRequest;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;
import com.lucky.newsandroid.R;

import org.json.JSONObject;

import java.util.Map;

/**
 * 作者：jacky on 2019/9/24 12:23
 * 邮箱：jackyli706@gmail.com
 */
public class VolleyManager {

    private static VolleyManager volleyManager;
    private int timeout = 2000;
    private int maxretry = 0;
    private float backoff = 0f;
    private Map<String, String> map;
    private boolean isCahce;

    private RequestQueue queue;

    private VolleyManager() {
    }

    public static VolleyManager getInstance() {
        if (volleyManager == null) {
            synchronized (VolleyManager.class) {
                if (volleyManager == null) {
                    volleyManager = new VolleyManager();
                }
            }
        }
        return volleyManager;
    }

    //初始化Volley
    public void initVolley(Context context) {
        queue = Volley.newRequestQueue(context.getApplicationContext());
    }

    //设置超时策略
    public void setRetry(int timeout, int maxretry, float backoff) {
        this.timeout = timeout;
        this.maxretry = maxretry;
        this.backoff = backoff;
    }

    //设置请求头
    public void setHeader(Map<String, String> map) {
        this.map = map;
    }

    //设置缓存
    public void setShouldCache(boolean isCache) {
        this.isCahce = isCache;
    }

    //请求字符串数据
    public void getString(int method, String url, Result<String> result) {
        StringRequest stringRequest = new StringRequest(method, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                result.onSuccess(response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        stringRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        stringRequest.setShouldCache(isCahce);
        queue.add(stringRequest);
    }

    //请求Json数据
    public void getJson(int method, String url, String requestBody, Result<JSONObject> result) {

        JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(method, url, requestBody, new Response.Listener<JSONObject>() {
            @Override
            public void onResponse(JSONObject response) {
                result.onSuccess(response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        jsonObjectRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        jsonObjectRequest.setShouldCache(isCahce);
        queue.add(jsonObjectRequest);
    }

    //请求图片数据
    public void getImage(String url, Result<Bitmap> result) {

        ImageRequest imageRequest = new ImageRequest(url, new Response.Listener<Bitmap>() {
            @Override
            public void onResponse(Bitmap response) {
                result.onSuccess(response);
            }
        }, 0, 0, Bitmap.Config.RGB_565, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        imageRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        imageRequest.setShouldCache(isCahce);
        queue.add(imageRequest);
    }

    /**
     * ImageLoader的内部使用ImageRequest来实现，
     * 它的构造器可以传入一个ImageCache缓存形参，
     * 实现了图片缓存的功能，同时还可以过滤重复链接，
     * 避免重复发送请求
     *
     * @param url
     */
    public void useImageLoader(String url, ImageView imageView) {
        ImageLoader imageLoader = new ImageLoader(queue, new BitmapCache());
        ImageLoader.ImageListener listener = ImageLoader.getImageListener(imageView, R.mipmap.ic_launcher, R.mipmap.ic_launcher);
        imageLoader.get(url, listener);
    }

    /**
     * NetworkImageView是一个自定义控件，继承自ImageView，封装了请求网络加载图片的功能。
     * 先在布局中引用：
     * <com.android.volley.toolbox.NetworkImageView
     * android:id="@+id/nv_image"
     * android:layout_width="200dp"
     * android:layout_height="200dp"
     * android:layout_centerHorizontal="true"
     * android:layout_below="@id/iv_image"
     * android:layout_marginTop="20dp"
     * ></com.android.volley.toolbox.NetworkImageView>
     * 代码中使用:
     * iv_image = (ImageView) this.findViewById(R.id.iv_image);
     * RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
     * ImageLoader imageLoader = new ImageLoader(mQueue, new BitmapCache());
     * nv_image.setDefaultImageResId(R.drawable.ico_default);
     * nv_image.setErrorImageResId(R.drawable.ico_default);
     * nv_image.setImageUrl("http://img.my.csdn.net/uploads/201603/26/1458988468_5804.jpg",
     * imageLoader);
     * NetworkImageView并没有提供设置最大宽度和高度的方法，根据我们设置控件的宽和高结合网络图片的宽和高内部会自动去实现压缩，
     * 如果我们不想要压缩可以设置NetworkImageView控件的宽和高都为wrap_content。
     */

    private class BitmapCache implements ImageLoader.ImageCache {

        LruCache<String, Bitmap> cache;
        int max = 10 * 1024 * 1024;

        BitmapCache() {
            cache = new LruCache<String, Bitmap>(max) {
                @Override
                protected int sizeOf(String key, Bitmap value) {
                    return value.getRowBytes() * value.getHeight();
                }
            };
        }

        @Override
        public Bitmap getBitmap(String url) {
            return cache.get(url);
        }

        @Override
        public void putBitmap(String url, Bitmap bitmap) {
            cache.put(url, bitmap);
        }
    }

    public void cancelAllRequest() {
        queue.cancelAll(this);
    }

    public interface Result<T> {

        void onSuccess(T response);

        void onError(Exception e);
    }
}
```

### 源码

![image](https://s2.ax1x.com/2019/05/29/VuBtde.png)

```java
//从上图可以看到Volley分为三个线程，分别是主线程、缓存调度线程、和网络调度线程，首先请求会加入缓存队列，如果发现可以找到相应的缓存结果就直接读取缓存并解析，然后回调给主线程；如果在缓存中没有找到结果，则将这条请求加入到网络队列中，然后发送HTTP请求，解析响应并写入缓存，并回调给主线程。

//1、从RequestQueue入手
//我们都知道使用Volley之前首先要创建RequestQueue：
RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
//这也是volley运作的入口，看看newRequestQueue：
public static RequestQueue newRequestQueue(Context context) {
        return newRequestQueue(context, (HttpStack)null);
    }

public static RequestQueue newRequestQueue(Context context, HttpStack stack) {
        return newRequestQueue(context, stack, -1);
    }
//连续调用了两个重载函数，最终调用的是：
public static RequestQueue newRequestQueue(Context context, HttpStack stack, int maxDiskCacheBytes) {
        File cacheDir = new File(context.getCacheDir(), "volley");
        String userAgent = "volley/0";

        try {
            String network = context.getPackageName();
            PackageInfo queue = context.getPackageManager().getPackageInfo(network, 0);
            userAgent = network + "/" + queue.versionCode;
        } catch (NameNotFoundException var7) {
            ;
        }

        if(stack == null) {
            if(VERSION.SDK_INT >= 9) {
                stack = new HurlStack();
            } else {
                stack = new HttpClientStack(AndroidHttpClient.newInstance(userAgent));
            }
        }

        BasicNetwork network1 = new BasicNetwork((HttpStack)stack);
        RequestQueue queue1;
        if(maxDiskCacheBytes <= -1) {
            queue1 = new RequestQueue(new DiskBasedCache(cacheDir), network1);
        } else {
            queue1 = new RequestQueue(new DiskBasedCache(cacheDir, maxDiskCacheBytes), network1);
        }

        queue1.start();
        return queue1;
    }
//可以看到如果android版本大于等于2.3则调用基于HttpURLConnection的HurlStack，否则就调用基于HttpClient的HttpClientStack。并创建了RequestQueue，调用了start()方法：
public void start() {
      this.stop();
      this.mCacheDispatcher = new CacheDispatcher(this.mCacheQueue, this.mNetworkQueue, this.mCache, this.mDelivery);
      this.mCacheDispatcher.start();

      for(int i = 0; i < this.mDispatchers.length; ++i) {
          NetworkDispatcher networkDispatcher = new NetworkDispatcher(this.mNetworkQueue, this.mNetwork, this.mCache, this.mDelivery);
          this.mDispatchers[i] = networkDispatcher;
          networkDispatcher.start();
      }

  }
//CacheDispatcher是缓存调度线程，并调用了start()方法，在循环中调用了NetworkDispatcher的start()方法，NetworkDispatcher是网络调度线程，默认情况下mDispatchers.length为4，默认开启了4个网络调度线程，也就是说有5个线程在后台运行并等待请求的到来。接下来我们创建各种的Request，并调用RequestQueue的add()方法：
public <T> Request<T> add(Request<T> request) {
       request.setRequestQueue(this);
       Set var2 = this.mCurrentRequests;
       synchronized(this.mCurrentRequests) {
           this.mCurrentRequests.add(request);
       }

       request.setSequence(this.getSequenceNumber());
       request.addMarker("add-to-queue");
       //如果不能缓存，则将请求添加到网络请求队列中
       if(!request.shouldCache()) {
           this.mNetworkQueue.add(request);
           return request;
       } else {
           Map var8 = this.mWaitingRequests;
           synchronized(this.mWaitingRequests) {
               String cacheKey = request.getCacheKey();

      //之前是否有执行相同的请求且还没有返回结果的，如果有的话将此请求加入mWaitingRequests队列，不再重复请求
               if(this.mWaitingRequests.containsKey(cacheKey)) {
                   Object stagedRequests = (Queue)this.mWaitingRequests.get(cacheKey);
                   if(stagedRequests == null) {
                       stagedRequests = new LinkedList();
                   }

                   ((Queue)stagedRequests).add(request);
                   this.mWaitingRequests.put(cacheKey, stagedRequests);
                   if(VolleyLog.DEBUG) {
                       VolleyLog.v("Request for cacheKey=%s is in flight, putting on hold.", new Object[]{cacheKey});
                   }
               } else {
  //没有的话就将请求加入缓存队列mCacheQueue，同时加入mWaitingRequests中用来做下次同样请求来时的重复判断依据
                   this.mWaitingRequests.put(cacheKey, (Object)null);
                   this.mCacheQueue.add(request);
               }

               return request;
           }
       }
   }
//通过判断request.shouldCache()，来判断是否可以缓存，默认是可以缓存的，如果不能缓存，则将请求添加到网络请求队列中，如果能缓存就判断之前是否有执行相同的请求且还没有返回结果的，如果有的话将此请求加入mWaitingRequests队列，不再重复请求；没有的话就将请求加入缓存队列mCacheQueue，同时加入mWaitingRequests中用来做下次同样请求来时的重复判断依据。
//从上面可以看出RequestQueue的add()方法并没有做什么请求网络或者对缓存进行操作。当将请求添加到网络请求队列或者缓存队列时，这时在后台的网络调度线程和缓存调度线程轮询各自的请求队列发现有请求任务则开始执行，我们先看看缓存调度线程。

//2、CacheDispatcher缓存调度线程
//CacheDispatcher的run()方法：
public void run() {
    if(DEBUG) {
        VolleyLog.v("start new dispatcher", new Object[0]);
    }
    //线程优先级设置为最高级别
    Process.setThreadPriority(10);
    this.mCache.initialize();

    while(true) {
        while(true) {
            while(true) {
                while(true) {
                    try {
                    //获取缓存队列中的一个请求
                        final Request e = (Request)this.mCacheQueue.take();
                        e.addMarker("cache-queue-take");
                        //如果请求取消了则将请求停止掉
                        if(e.isCanceled()) {
                            e.finish("cache-discard-canceled");
                        } else {
                        //查看是否有缓存的响应
                            Entry entry = this.mCache.get(e.getCacheKey());
                            //如果缓存响应为空，则将请求加入网络请求队列
                            if(entry == null) {
                                e.addMarker("cache-miss");
                                this.mNetworkQueue.put(e);
                            //判断缓存响应是否过期    
                            } else if(!entry.isExpired()) {
                                e.addMarker("cache-hit");
                                //对数据进行解析并回调给主线程
                                Response response = e.parseNetworkResponse(new NetworkResponse(entry.data, entry.responseHeaders));
                                e.addMarker("cache-hit-parsed");
                                if(!entry.refreshNeeded()) {
                                    this.mDelivery.postResponse(e, response);
                                } else {
                                    e.addMarker("cache-hit-refresh-needed");
                                    e.setCacheEntry(entry);
                                    response.intermediate = true;
                                    this.mDelivery.postResponse(e, response, new Runnable() {
                                        public void run() {
                                            try {
                                                CacheDispatcher.this.mNetworkQueue.put(e);
                                            } catch (InterruptedException var2) {
                                                ;
                                            }

                                        }
                                    });
                                }
                            } else {
                                e.addMarker("cache-hit-expired");
                                e.setCacheEntry(entry);
                                this.mNetworkQueue.put(e);
                            }
                        }
                    } catch (InterruptedException var4) {
                        if(this.mQuit) {
                            return;
                        }
                    }
                }
            }
        }
    }
}

static {
    DEBUG = VolleyLog.DEBUG;
}
//看到四个while循环有些晕吧，让我们挑重点的说，首先从缓存队列取出请求，判断是否请求是否被取消了，如果没有则判断该请求是否有缓存的响应，如果有并且没有过期则对缓存响应进行解析并回调给主线程。接下来看看网络调度线程。

//3、NetworkDispatcher网络调度线程
//NetworkDispatcher的run()方法：
public void run() {
       Process.setThreadPriority(10);

       while(true) {
           long startTimeMs;
           Request request;
           while(true) {
               startTimeMs = SystemClock.elapsedRealtime();

               try {
               //从队列中取出请求
                   request = (Request)this.mQueue.take();
                   break;
               } catch (InterruptedException var6) {
                   if(this.mQuit) {
                       return;
                   }
               }
           }

           try {
               request.addMarker("network-queue-take");
               if(request.isCanceled()) {
                   request.finish("network-discard-cancelled");
               } else {
                   this.addTrafficStatsTag(request);
                   //请求网络
                   NetworkResponse e = this.mNetwork.performRequest(request);
                   request.addMarker("network-http-complete");
                   if(e.notModified && request.hasHadResponseDelivered()) {
                       request.finish("not-modified");
                   } else {
                       Response volleyError1 = request.parseNetworkResponse(e);
                       request.addMarker("network-parse-complete");
                       if(request.shouldCache() && volleyError1.cacheEntry != null) {                         
                           //将响应结果存入缓存
                           this.mCache.put(request.getCacheKey(), volleyError1.cacheEntry);
                           request.addMarker("network-cache-written");
                       }

                       request.markDelivered();
                       this.mDelivery.postResponse(request, volleyError1);
                   }
               }
           } catch (VolleyError var7) {
               var7.setNetworkTimeMs(SystemClock.elapsedRealtime() - startTimeMs);
               this.parseAndDeliverNetworkError(request, var7);
           } catch (Exception var8) {
               VolleyLog.e(var8, "Unhandled exception %s", new Object[]{var8.toString()});
               VolleyError volleyError = new VolleyError(var8);
               volleyError.setNetworkTimeMs(SystemClock.elapsedRealtime() - startTimeMs);
               this.mDelivery.postError(request, volleyError);
           }
       }
   }
//网络调度线程也是从队列中取出请求并且判断是否被取消了，如果没取消就去请求网络得到响应并回调给主线程。请求网络时调用this.mNetwork.performRequest(request)，这个mNetwork是一个接口，实现它的类是BasicNetwork，我们来看看BasicNetwork的performRequest()方法：
public NetworkResponse performRequest(Request<?> request) throws VolleyError {
        long requestStart = SystemClock.elapsedRealtime();

        while(true) {
            HttpResponse httpResponse = null;
            Object responseContents = null;
            Map responseHeaders = Collections.emptyMap();

            try {
                HashMap e = new HashMap();
                this.addCacheHeaders(e, request.getCacheEntry());
                httpResponse = this.mHttpStack.performRequest(request, e);
                StatusLine statusCode1 = httpResponse.getStatusLine();
                int networkResponse1 = statusCode1.getStatusCode();
                responseHeaders = convertHeaders(httpResponse.getAllHeaders());
                if(networkResponse1 == 304) {
                    Entry requestLifetime2 = request.getCacheEntry();
                    if(requestLifetime2 == null) {
                        return new NetworkResponse(304, (byte[])null, responseHeaders, true, SystemClock.elapsedRealtime() - requestStart);
                    }

                    requestLifetime2.responseHeaders.putAll(responseHeaders);
                    return new NetworkResponse(304, requestLifetime2.data, requestLifetime2.responseHeaders, true, SystemClock.elapsedRealtime() - requestStart);
                }
...省略
//从上面可以看到在12行调用的是HttpStack的performRequest()方法请求网络，接下来根据不同的响应状态码来返回不同的NetworkResponse。另外HttpStack也是一个接口，实现它的两个类我们在前面已经提到了就是HurlStack和HttpClientStack。让我们再回到NetworkDispatcher，请求网络后，会将响应结果存在缓存中，如果响应结果成功则调用this.mDelivery.postResponse(request, volleyError1)来回调给主线程。来看看Delivery的postResponse()方法：
public void postResponse(Request<?> request, Response<?> response, Runnable runnable) {
       request.markDelivered();
       request.addMarker("post-response");
       this.mResponsePoster.execute(new ExecutorDelivery.ResponseDeliveryRunnable(request, response, runnable));
   }
//来看看ResponseDeliveryRunnable里面做了什么：
private class ResponseDeliveryRunnable implements Runnable {
       private final Request mRequest;
       private final Response mResponse;
       private final Runnable mRunnable;

       public ResponseDeliveryRunnable(Request request, Response response, Runnable runnable) {
           this.mRequest = request;
           this.mResponse = response;
           this.mRunnable = runnable;
       }

       public void run() {
           if(this.mRequest.isCanceled()) {
               this.mRequest.finish("canceled-at-delivery");
           } else {
               if(this.mResponse.isSuccess()) {
                   this.mRequest.deliverResponse(this.mResponse.result);
               } else {
                   this.mRequest.deliverError(this.mResponse.error);
               }

               if(this.mResponse.intermediate) {
                   this.mRequest.addMarker("intermediate-response");
               } else {
                   this.mRequest.finish("done");
               }

               if(this.mRunnable != null) {
                   this.mRunnable.run();
               }

           }
       }
   }
//第17行调用了this.mRequest.deliverResponse(this.mResponse.result)，这个就是实现Request抽象类必须要实现的方法，我们来看看StringRequest的源码：
public class StringRequest extends Request<String> {
    private final Listener<String> mListener;

    public StringRequest(int method, String url, Listener<String> listener, ErrorListener errorListener) {
        super(method, url, errorListener);
        this.mListener = listener;
    }

    public StringRequest(String url, Listener<String> listener, ErrorListener errorListener) {
        this(0, url, listener, errorListener);
    }

    protected void deliverResponse(String response) {
        this.mListener.onResponse(response);
    }

 ...省略
}
//在deliverResponse方法中调用了this.mListener.onResponse(response)，最终将response回调给了Response.Listener的onResponse()方法。我们用StringRequest请求网络的写法是这样的：
RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
        StringRequest mStringRequest = new StringRequest(Request.Method.GET, "http://www.baidu.com",
                new Response.Listener<String>() {
                    @Override
                    public void onResponse(String response) {
                        Log.i("wangshu", response);
                    }
                }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Log.e("wangshu", error.getMessage(), error);
            }
        });
        //将请求添加在请求队列中
        mQueue.add(mStringRequest);
```

## OkHttp

- [github地址](https://github.com/square/okhttp)

- [官方文档](hhttps://square.github.io/okhttp/)

- ```groovy
  implementation 'com.squareup.okhttp3:okhttp:3.10.0'
  ```

### 使用

```java
//1、创建OkHttpClient实例
/**
三种方法
1. 创建一个默认配置OkHttpClient，可以使用默认的构造函数。
2. 通过new OkHttpClient.Builder()方法来一步一步配置一个OkHttpClient实例。
3. 如果要求使用现有的实例，可以通过newBuilder()方法来进行构造
**/
//配置说明
Dispatcher dispatcher;          // 分发
Proxy proxy;                    // 代理
List<Protocol> protocols;
List<ConnectionSpec> connectionSpecs;
final List<Interceptor> interceptors = new ArrayList<>(); // 拦截器
final List<Interceptor> networkInterceptors = new ArrayList<>(); // 网络拦截器
ProxySelector proxySelector;
CookieJar cookieJar;
Cache cache;    // 缓存
InternalCache internalCache;
SocketFactory socketFactory;
SSLSocketFactory sslSocketFactory;
HostnameVerifier hostnameVerifier;
CertificatePinner certificatePinner;
Authenticator proxyAuthenticator;   // 代理证书
Authenticator authenticator;        // 证书
ConnectionPool connectionPool;
Dns dns;        // DNS
boolean followSslRedirects;
boolean followRedirects;
boolean retryOnConnectionFailure;
int connectTimeout;  //连接超时时间
int readTimeout;     //读取超时时间
int writeTimeout;    //写入超时时间

//2、创建Request请求(默认为GET请求)
//最简单的构造Request实例
Request request = new Request.Builder()
      .url(url)
      .build();
// 其他配置
url(String url);  //url地址
addHeader(String name, String value);  //添加请求头
removeHeader(String name) //移除某个请求头
headers(Headers headers)  //添加请求头,通过Headers来构造
post(RequestBody body)   //使用post来请求,通过RequestBody来构造入参
...
//创建RequestBody
//传递json
MediaType JSON =MediaType.parse("application/json;charset=utf-8");
RequestBody requestBody=RequestBody.create(JSON,jsonString);

//3、发送请求
//添加请求
Call call=okHttpClient.newCall(request);
//获取结果
1、异步(结果都在子线程种)
call.enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {

            }

            @Override
            public void onResponse(Call call, Response response) throws IOException {
                response.body().string();  //获取返回的结果
            }
        });

2、同步(运行在当前线程,需要开启子线程)
try {
            Response response = call.execute();
            String string = response.body().string();  //返回结果
        } catch (IOException e) {
            e.printStackTrace();
}
```

### 日志拦截器

```kotlin
package com.imi.gamestore.manager.net.interceptor

import com.imi.gamestore.utils.JsonUtil
import com.imi.gamestore.utils.LogUtil
import okhttp3.*
import okio.Buffer


/**
 * 自定义的http拦截器
 *
 * 拦截请求信息和回复信息
 */
class HttpLogInterceptor : Interceptor {
    //private val format = SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS")

    private val post = "POST"

    override fun intercept(chain: Interceptor.Chain): Response {
        val request = chain.request()
        LogUtil.d(
            JsonUtil.objectToJson(
                RequestLog(
                    "请求数据",
                    request.url().toString(),
                    request.method()
                )
            )
        )
        if (post == request.method()) {
            val copy = request.newBuilder().build()
            val buffer = Buffer()
            copy.body()?.writeTo(buffer)
            LogUtil.json(buffer.readUtf8())
        }

        val response = chain.proceed(chain.request())

        return if (response.body() != null && response.body()!!.contentType() != null) {
            val mediaType: MediaType? = response.body()!!.contentType()
            val string = response.body()!!.string()
            //LogUtil.d("mediaType =  :  " + mediaType.toString())
            LogUtil.d(
                JsonUtil.objectToJson(
                    ResponseLog(
                        "响应数据",
                        request.url().toString(),
                        response.code(),
                        response.protocol(),
                        mediaType.toString()
                    )
                )
            )
            LogUtil.json(string)
            val responseBody = ResponseBody.create(mediaType, string)
            response.newBuilder().body(responseBody).build()
        } else {
            response
        }
    }
}

data class ResponseLog(
    val state: String,
    val url: String,
    val code: Int,
    //val message: String,
    val protocol: Protocol,
    val mediaType: String,
)

data class RequestLog(
    val state: String,
    val url: String,
    val method: String,
)
```

### WebSocket

#### Java

```java
package com.shoukong.umpsky.manager.net.websocket;

import com.shoukong.umpsky.Constants;
import com.shoukong.umpsky.listener.WebSocketEventListener;
import com.shoukong.umpsky.utils.LogUtil;

import java.util.Objects;
import java.util.concurrent.TimeUnit;

import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import okhttp3.WebSocket;
import okhttp3.WebSocketListener;
import okhttp3.logging.HttpLoggingInterceptor;
import okio.ByteString;

//参考 https://github.com/fomin-zhu/websocket
public class WebSocketManager {

    private static final WebSocketManager webSocketManager = new WebSocketManager();

    private WebSocketManager() {

    }

    private HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor(message -> LogUtil.e("WebSocket请求日志:" + message)).setLevel(HttpLoggingInterceptor.Level.BODY);

    public static WebSocketManager getInstance() {
        return webSocketManager;
    }

    private OkHttpClient client;
    private Request request;
    private WebSocketEventListener webSocketEventListener;
    private WebSocket mWebSocket;

    private boolean isConnect = false;

    public void init(WebSocketEventListener message) {
        loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
        client = Objects.requireNonNull(new OkHttpClient.Builder()
                .writeTimeout(30, TimeUnit.SECONDS))
                .readTimeout(30, TimeUnit.SECONDS)
                .connectTimeout(30, TimeUnit.SECONDS)
                .addInterceptor(loggingInterceptor)
                .build();
        request = new Request.Builder().url(Constants.WEBSOCKET_URL).build();
        webSocketEventListener = message;
        connect();
    }

    /**
     * 连接
     */
    public void connect() {
        if (isConnect()) {
            LogUtil.e("web socket connected");
            return;
        }
        client.newWebSocket(request, createListener());
    }

    /**
     * 是否连接
     */
    public boolean isConnect() {
        return mWebSocket != null && isConnect;
    }

    /**
     * 发送消息
     *
     * @param text 字符串
     * @return boolean
     */
    public boolean sendMessage(String text) {
        if (!isConnect()) return false;
        return mWebSocket.send(text);
    }

    /**
     * 发送消息
     *
     * @param byteString 字符集
     * @return boolean
     */
    public boolean sendMessage(ByteString byteString) {
        if (!isConnect()) return false;
        return mWebSocket.send(byteString);
    }

    /**
     * 关闭连接
     */
    public void close() {
        if (isConnect()) {
            mWebSocket.cancel();
            mWebSocket.close(1001, "客户端主动关闭连接");
        }
    }

    private WebSocketListener createListener() {
        return new WebSocketListener() {
            @Override
            public void onOpen(WebSocket webSocket, Response response) {
                super.onOpen(webSocket, response);
                LogUtil.e("open:" + response.toString());
                mWebSocket = webSocket;
                isConnect = response.code() == 101;
                if (!isConnect) {
                    //reconnect();
                } else {
                    LogUtil.e("connect success.");
                    if (webSocketEventListener != null) {
                        webSocketEventListener.onConnectSuccess();
                    }
                }
            }

            @Override
            public void onMessage(WebSocket webSocket, String text) {
                super.onMessage(webSocket, text);
                if (webSocketEventListener != null) {
                    webSocketEventListener.onMessage(text);
                }
            }

            @Override
            public void onMessage(WebSocket webSocket, ByteString bytes) {
                super.onMessage(webSocket, bytes);
                if (webSocketEventListener != null) {
                    webSocketEventListener.onMessage(bytes.base64());
                }
            }

            @Override
            public void onClosing(WebSocket webSocket, int code, String reason) {
                super.onClosing(webSocket, code, reason);
                mWebSocket = null;
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onClose();
                }
            }

            @Override
            public void onClosed(WebSocket webSocket, int code, String reason) {
                super.onClosed(webSocket, code, reason);
                mWebSocket = null;
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onClose();
                }
            }

            @Override
            public void onFailure(WebSocket webSocket, Throwable t, Response response) {
                super.onFailure(webSocket, t, response);
                if (response != null) {
                    LogUtil.e("connect failed：" + response.message());
                }
                LogUtil.e("connect failed throwable：" + t.getMessage());
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onConnectFailed();
                }
            }
        };
    }
}
```

#### Kotlin

```kotlin
package com.imi.gamestore.manager.net

import com.imi.gamestore.Constants
import com.imi.gamestore.utils.LogUtil
import okhttp3.*
import okhttp3.logging.HttpLoggingInterceptor
import okio.ByteString
import java.util.concurrent.TimeUnit


/**
 * Websocket
 * 还可以使用ping帧来保活
 * 还可以进行鉴权
 */
class WebSocketManager private constructor() {

    private lateinit var webSocket: WebSocket
    private lateinit var request: Request
    private lateinit var client: OkHttpClient
    private var isConnect: Boolean = false
    private lateinit var webSocketState: WebSocketState

    private val loggingInterceptor =
        HttpLoggingInterceptor { message: String -> LogUtil.d("WebSocket请求日志:$message") }.setLevel(
            HttpLoggingInterceptor.Level.BODY
        )

    //懒汉
    companion object {
        val instance: WebSocketManager by lazy(mode = LazyThreadSafetyMode.SYNCHRONIZED) {
            WebSocketManager()
        }
    }

    fun initWebSocket(webSocketState: WebSocketState) {
        client = OkHttpClient.Builder()
            .readTimeout(3, TimeUnit.SECONDS) //设置读取超时时间
            .writeTimeout(3, TimeUnit.SECONDS) //设置写的超时时间
            .connectTimeout(3, TimeUnit.SECONDS) //设置连接超时时间
            .addInterceptor(loggingInterceptor)
            .build()

        this.webSocketState = webSocketState
        //构建一个连接请求对象
        request = Request.Builder().get().url(Constants.WEBSOCKET_URL).build()
        //进行连接
        connect()
    }

    //连接
    private fun connect() {
        if (isConnect) {
            return
        }
        webSocket = client.newWebSocket(request, createListener())
    }

    //重新连接
    private fun reconnect() {
        Thread.sleep(3000)   //暂停3秒
        connect()
    }

    //关闭连接
    private fun close() {
        if (isConnect) {
            webSocket.cancel()
            webSocket.close(1001, "客户端主动关闭连接")
        }
    }

    fun sendMessage(message: String) {
        if (isConnect) {
            webSocket.send(message)
        }
    }

    private fun createListener(): WebSocketListener {
        return object : WebSocketListener() {
            override fun onOpen(webSocket: WebSocket, response: Response) {
                super.onOpen(webSocket, response)
                isConnect = response.code() == 101
                if (!isConnect) {
                    reconnect()
                } else {
                    webSocketState.connectSuccess()
                    startScheduleThread()
                    LogUtil.d("连接成功")
                }
            }

            override fun onMessage(webSocket: WebSocket, text: String) {
                super.onMessage(webSocket, text)
                webSocketState.message(text)
            }

            override fun onMessage(webSocket: WebSocket, bytes: ByteString) {
                super.onMessage(webSocket, bytes)
            }

            override fun onClosing(webSocket: WebSocket, code: Int, reason: String) {
                super.onClosing(webSocket, code, reason)
                LogUtil.d("onClosing")
                isConnect = false
            }

            override fun onClosed(webSocket: WebSocket, code: Int, reason: String) {
                super.onClosed(webSocket, code, reason)
                LogUtil.d("onClosed")
                isConnect = false
            }

            override fun onFailure(webSocket: WebSocket, t: Throwable, response: Response?) {
                super.onFailure(webSocket, t, response)
                LogUtil.d("onFailure")
                isConnect = false
                reconnect()
            }
        }
    }

    //心跳（每40秒执行一次）
    fun startScheduleThread() {
        Thread(Runnable {
            while (isConnect) {
                sendMessage("HEART_BEAT")
                Thread.sleep(40000)
            }
        }).start()

    }
}

interface WebSocketState {
    fun connectSuccess()
    fun connectFail()
    fun message(message: String)
}
```

## Retrofit

- [github地址](https://github.com/square/retrofit)

- [官方文档](https://square.github.io/retrofit/)

- ```groovy
  //Retrofit网络请求
      implementation 'com.squareup.retrofit2:retrofit:2.4.0'   
      implementation 'com.squareup.retrofit2:converter-gson:2.4.0'  //gson转换器
      implementation 'com.google.code.gson:gson:2.8.6'   //gson
      implementation 'io.reactivex.rxjava2:rxandroid:2.1.0'
      implementation 'com.squareup.okhttp3:logging-interceptor:3.11.0'  //log拦截器
      implementation 'com.squareup.retrofit2:adapter-rxjava2:2.4.0'  //支持rxjava
  ```

### 使用

```java
//1、建立接口
public interface RetService {
    @GET("/")
    Call<ResponseBody> getBaiduDu();
}

//2、构建Retrofit对象
Retrofit retrofit=new Retrofit.Builder().baseUrl("https://www.baidu.com").build();

//3、获取代理对象
RetService service = retrofit.create(RetService.class);

//4、发起请求
Call<ResponseBody> baiduDu = service.getBaiduDu();

//5、获取结果
// 1、异步
baiduDu.enqueue(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
                try {
                    Log.d("ddd",response.body().string());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {

            }
        });

// 2、同步
Response<ResponseBody> execute = baiduDu.execute();
execute.body().string()
```

### Retrofit单例

#### Java

```java
package com.shoukong.umpsky.manager.net.http;

import com.shoukong.umpsky.Constants;
import com.shoukong.umpsky.utils.LogUtil;

import java.io.IOException;
import java.util.concurrent.TimeUnit;

import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import okhttp3.logging.HttpLoggingInterceptor;
import retrofit2.Retrofit;
import retrofit2.adapter.rxjava2.RxJava2CallAdapterFactory;
import retrofit2.converter.gson.GsonConverterFactory;

/**
 * author : lijie
 * date : 2019/12/5 10:24
 * e-mail : jackyli706@gmail.com
 * description :
 * <p>
 * 针对大图片或者大文件，使用拦截器拦截日志的话只保留header日志
 * 不然会导致OutOfMemory异常
 * 参考解决方案  https://blog.csdn.net/jklwan/article/details/101002449
 * <p>
 * 参考：https://www.jianshu.com/p/2e8b400909b7
 */
public class RetrofitManager {

    private static Retrofit retrofit;

    //Log日志
    private HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor(new HttpLoggingInterceptor.Logger() {
        @Override
        public void log(String message) {
            LogUtil.e("HTTP请求日志:" + message);
        }
    }).setLevel(HttpLoggingInterceptor.Level.BODY);

    //Ok的拦截器
    private OkHttpClient okHttpClient() {
        loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);

        return new OkHttpClient.Builder()
                .writeTimeout(3, TimeUnit.SECONDS)
                .connectTimeout(3, TimeUnit.SECONDS)
                .readTimeout(3, TimeUnit.SECONDS)
                .retryOnConnectionFailure(false)
                .addInterceptor(loggingInterceptor)
                //自定义连接池最大空闲连接数和等待时间大小，否则默认最大5个空闲连接
                // .connectionPool(new ConnectionPool(32, 5, TimeUnit.MINUTES))
//                .addInterceptor(new Interceptor() {
//                    @Override
//                    public Response intercept(Chain chain) throws IOException {
//                        Request request = chain.request()
//                                .newBuilder()
//                                // .addHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8")
//                                // .addHeader("Accept-Encoding", "gzip, deflate")
//                                .addHeader("Connection", "close")
//                                // .addHeader("Accept", "*/*")
//                                // .addHeader("Cookie", "add cookies here")
//                                .build();
//                        return chain.proceed(request);
//                    }
//                })
                .build();

        //Retrofit的使用
    }

    private RetrofitManager() {
        retrofit = new Retrofit.Builder()
                .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
                .addConverterFactory(GsonConverterFactory.create())
                .baseUrl(Constants.HTTP_URL + "/")
                .client(okHttpClient())
                .build();
    }

    public static Retrofit get() {
        if (retrofit == null) {
            new RetrofitManager();
        }
        return retrofit;
    }

    public <T> T create(Class<T> clazz) {
        return retrofit.create(clazz);
    }

}
```

#### Kotlin

```kotlin
package com.imi.gamestore.manager.net

import com.imi.gamestore.Constants
import com.imi.gamestore.api.ApiService
import com.imi.gamestore.manager.net.adapter.LiveDataCallAdapterFactory
import com.imi.gamestore.manager.net.interceptor.HttpLogInterceptor
import okhttp3.OkHttpClient
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory
import java.util.concurrent.ConcurrentHashMap
import java.util.concurrent.Executors
import java.util.concurrent.TimeUnit

class RetrofitManager private constructor() {

    companion object {

        private var retrofitManager: RetrofitManager? = null

        fun getInstance(): RetrofitManager {
            if (retrofitManager == null) {
                retrofitManager = RetrofitManager()
            }
            return retrofitManager!!
        }
    }

    //用于URL基地址和Retrofit对象的映射
    private var retrofitMap: ConcurrentHashMap<String, Retrofit> = ConcurrentHashMap()

    fun createApiService(): ApiService {
        return getRetrofit()!!.create(ApiService::class.java)
    }


    private fun getRetrofit(): Retrofit? {
        return getRetrofit(Constants.BASE_URL)
    }

    //为以后可能出现不同url的处理保留
    private fun getRetrofit(baseUrl: String): Retrofit? {

        if (retrofitMap.size == 0 || !retrofitMap.contains(baseUrl) || retrofitMap[baseUrl] == null) {
            val okHttpClient = OkHttpClient.Builder()
                //自定义拦截器用于日志输出
                .addInterceptor(HttpLogInterceptor())
                .connectTimeout(5000, TimeUnit.SECONDS)
                .readTimeout(5000, TimeUnit.SECONDS)
                .writeTimeout(5000, TimeUnit.SECONDS)
                .build()

            val retrofit = Retrofit.Builder().baseUrl(baseUrl)
                .callbackExecutor(Executors.newSingleThreadExecutor())  //默认结果返回在主线程，将结果放到子线程处理
                //格式转换
                .addConverterFactory(GsonConverterFactory.create())
                //正常的retrofit返回的是call，此方法用于将call转化成Rxjava的Observable或其他类型
                .addCallAdapterFactory(LiveDataCallAdapterFactory())
                .client(okHttpClient)
                .build()

            retrofitMap[baseUrl] = retrofit
        }
        return retrofitMap[baseUrl];
    }

}
```

### 请求注解

```java
/**
 * author : lijie
 * date : 2019/12/5 10:29
 * e-mail : jackyli706@gmail.com
 * description :
 */
public interface ApiService {

    **
     *   断点下载（Kotlin方法）   
     *   Range的使用形式
     *   bytes=0-499	表示头500个字节
     *   bytes=500-999	表示第二个500字节
     *   bytes=-500	表示最后500个字节
     *   bytes=500-	表示500字节以后的范围
     *   bytes=0-0,-1	第一个和最后一个字节
     */
    @Streaming
    @GET
    fun downloadApk(@Header("Range") range: String, @Url apkUrl: String): Call<ResponseBody>

    //Get方法传参（Kotlin）    
    @GET("api/wechat/getQRCode")
    fun getWeChatQrCode(@Query("sn") sn: String): LiveData<BaseResponse<String>>

    /**
    普通POST请求（请求json的数据）
    请求数据：UMSIdentifyMsg为对象映射为json
    回复数据：json映射为ResponseMsg对象
    **/
    @POST("ums/UMSIdentify")
    @Headers("Content-Type:application/json; charset=utf-8")
    Call<ResponseMsg> umsIdentify(@Body UMSIdentifyMsg UMSIdentifyMsg);

    /**
    以下是RxJava+Retrofit
    **/
    //Get请求
    @GET("gds/GDSHeart")
    Observable<ResponseMsg> connectSaas();

    /**
     *  多张图片上传
       RequestBody requestBody[] = new RequestBody[picPath.length];
       for (int i = 0; i < picPath.length; i++) {
            requestBody[i] = RequestBody.create(MediaType.parse("multipart/form-data"), picPath[i]);
        }
        MultipartBody.Part[] part = new MultipartBody.Part[requestBody.length];
        for (int i = 0; i < requestBody.length; i++) {
            part[i] = MultipartBody.Part.createFormData("picture", picPath[i].getName(), requestBody[i]);
        }
        return RetrofitManager.get().create(ApiService.class).uploadPic(part);
     */
    @Multipart
    @POST("gds/GDSTaskPic")
        //防止乱码
    Observable<ResponseMsg> uploadPic(@Part MultipartBody.Part[] file);

    //在子线程网络请求主线程更新UI
    mainModel.connectSaas().subscribeOn(Schedulers.io())
                    .observeOn(AndroidSchedulers.mainThread())
                    .subscribe(responseMsg -> {
                        if (mView == null) {
                            LogUtil.d("connectSaas----Success" + ":" + "mView is NULL");
                            return;
                        }
                        mView.hideLoading();
                        mView.connectSaasSuccess(responseMsg);
                    }, throwable -> {
                        if (mView == null) {
                            LogUtil.d("connectSaas----Fail" + ":" + "mView is NULL");
                            return;
                        }
                        mView.hideLoading();
                        if (throwable == null) {
                            mView.connectSaasFail("展示数据失败");
                        } else {
                            mView.connectSaasFail(throwable.getMessage());
                        }
                    });
}
```

### 配合LiveData

```Kotlin
//LiveDataCallAdapter.kt
package com.imi.gamestore.manager.net.adapter

import androidx.lifecycle.LiveData
import com.imi.gamestore.base.BaseResponse
import retrofit2.Call
import retrofit2.CallAdapter
import retrofit2.Callback
import retrofit2.Response
import java.lang.reflect.Type
import java.util.concurrent.atomic.AtomicBoolean

class LiveDataCallAdapter<T>(private val responseType: Type) :
    CallAdapter<T, LiveData<T>> {

    override fun responseType(): Type {
        return responseType
    }

    override fun adapt(call: Call<T>): LiveData<T> {
        return object : LiveData<T>() {
            var started = AtomicBoolean(false)

            override fun onActive() {
                super.onActive()
                if (started.compareAndSet(false, true)) {
                    call.enqueue(object : Callback<T> {
                        override fun onResponse(call: Call<T>, response: Response<T>) {
                            if (response.code() >= 400) {
                                val value =
                                    BaseResponse<T>(response.code(), response.errorBody().toString(), null) as T
                                postValue(value)
                            } else {
                                postValue(response.body())
                            }
                        }

                        override fun onFailure(call: Call<T>, throwable: Throwable) {
                            val value =
                                BaseResponse<T>(-1, throwable.message!!, null) as T
                            postValue(value)
                        }
                    })
                }
            }
        }
    }
}

//LiveDataCallAdapterFactory.kt
package com.imi.gamestore.manager.net.adapter

import androidx.lifecycle.LiveData
import com.imi.gamestore.base.BaseResponse
import retrofit2.CallAdapter
import retrofit2.Retrofit
import java.lang.reflect.ParameterizedType
import java.lang.reflect.Type

/**
 * 这个也还可以
 * https://github.com/AlfredoBejarano/Retrofit-LiveData-Adapter
 * 暂时没有使用
 */
class LiveDataCallAdapterFactory : CallAdapter.Factory() {
    override fun get(
        returnType: Type,
        annotations: Array<Annotation>,
        retrofit: Retrofit
    ): CallAdapter<*, *>? {
        if (getRawType(returnType) != LiveData::class.java) return null
        //获取第一个泛型类型
        val observableType = getParameterUpperBound(0, returnType as ParameterizedType)
        val rawType = getRawType(observableType)
        if (rawType != BaseResponse::class.java) {
            throw IllegalArgumentException("type must be BaseResponse")
        }
        if (observableType !is ParameterizedType) {
            throw IllegalArgumentException("resource must be parameterized")
        }
        return LiveDataCallAdapter<Any>(observableType)
    }
}

//ApiResponse.kt
package com.imi.gamestore.manager.net.adapter
data class ApiResponse<T>(
    var data: T?,
    var errorCode: Int,
    var errorMsg: String
)

//添加适配器，处理返回的数据
.addCallAdapterFactory(LiveDataCallAdapterFactory())
```

### 断点下载大文件

```kotlin
   /**   定义请求
     *   Range的使用形式
     *   bytes=0-499	表示头500个字节
     *   bytes=500-999	表示第二个500字节
     *   bytes=-500	表示最后500个字节
     *   bytes=500-	表示500字节以后的范围
     *   bytes=0-0,-1	第一个和最后一个字节
     */
    @Streaming
    @GET
    fun downloadApk(@Header("Range") range: String, @Url apkUrl: String): Call<ResponseBody>

//下载帮助类
class DownloadHelper {

    companion object {
        var allCall: HashMap<String, Call<ResponseBody>> = HashMap()   //保存所有请求的call

        var mCall: Call<ResponseBody>? = null

        /**
         * @startPoint 开始的字节
         * @handler 推送到主线程
         * @apkUrl apk地址
         */
        fun startDownload(
            startPoint: Long,
            handler: Handler?,
            apkUrl: String,
            apkCachePath: String
        ) {
            LogUtil.d("startPoint:$startPoint")
            mCall = RetrofitManager.getInstance().createApiService()
                .downloadApk(
                    "bytes=$startPoint-",
                    apkUrl
                )
            mCall!!.enqueue(DownloadCallback(startPoint, handler, apkCachePath))
            allCall[apkUrl] = mCall!!
        }

        //取消了移除call
        fun cancelDownload(apkUrl: String) {
            allCall[apkUrl]?.cancel()
            allCall.remove(apkUrl)
        }
    }
}

//真正的下载
class DownloadCallback(
    private var startPoint: Long,
    private var mHandler: Handler?,
    private var apkCachePath: String
) :
    Callback<ResponseBody> {

    override fun onResponse(call: Call<ResponseBody>, response: Response<ResponseBody>) {
        if (response.code() != HttpURLConnection.HTTP_PARTIAL && response.code() != HttpURLConnection.HTTP_OK) {
            //返回code非206 ，不支持断点续传
            mHandler?.sendEmptyMessage(400);
            return;
        }
        downloadApk(response.body()!!)
    }

    override fun onFailure(call: Call<ResponseBody>, t: Throwable) {
        mHandler?.sendEmptyMessage(100);
    }

    private fun downloadApk(body: ResponseBody) {
        val startPoint = this.startPoint
        val apkCachePath = this.apkCachePath

        var inputStream: InputStream? = null
        var outputStream: OutputStream? = null
        try {
            val fileReader = ByteArray(8 * 1024 * 1024)
            val fileSize: Long = body.contentLength()
            LogUtil.d("总大小:$fileSize")
            var fileSizeDownloaded: Long = startPoint
            inputStream = body.byteStream()
            outputStream =
                FileOutputStream(apkCachePath, true)
            while (true) {
                val read: Int = inputStream.read(fileReader)
                if (read == -1) {
                    break
                }
                outputStream.write(fileReader, 0, read)
                fileSizeDownloaded += read
                val msg: Message = Message.obtain()
                msg.arg1 =
                    ((fileSizeDownloaded.toFloat() / (fileSize + startPoint)) * 100).toInt()
                msg.what = 300;
                mHandler?.sendMessage(msg)
                SystemClock.sleep(50);
            }
            outputStream.flush();
        } catch (e: Exception) {
            LogUtil.d(e.toString())
        } finally {
            inputStream?.close()
            outputStream?.close()
        }
    }
}
```



# 图片加载

## Glide

+ [官网](https://github.com/bumptech/glide)

+ [中文文档](https://muyangmin.github.io/glide-docs-cn/)

+ ```groovy
  implementation "com.github.bumptech.glide:glide:4.11.0"
  kapt 'com.github.bumptech.glide:compiler:4.11.0'    //kotlin的话需要kapt开头，java使用annotationProcessor开头
  ```

### 使用

```java
//1、加载图片到imageView
Glide.with(Context context).load(Strint url).into(ImageView imageView);

//2、各种形式的图片加载到ImageView
// 加载本地图片
File file = new File(getExternalCacheDir() + "/image.jpg");
Glide.with(this).load(file).into(imageView);

// 加载应用资源
int resource = R.drawable.image;
Glide.with(this).load(resource).into(imageView);

// 加载二进制流
byte[] image = getImageBytes();
Glide.with(this).load(image).into(imageView);

// 加载Uri对象
Uri imageUri = getImageUri();
Glide.with(this).load(imageUri).into(imageView);

//3、加载带有占位图（占位图目的为在目的图片还未加载出来的时候，提前展示给用户的一张图片）
Glide.with(this).load(url).placeholder(R.drawable.loading).into(imageView);

//4、加载失败 放置占位符
Glide.with(this).load(url).placeholder(R.drawable.loading).error(R.drawable.error)
     .diskCacheStrategy(DiskCacheStrategy.NONE)//关闭Glide的硬盘缓存机制
     .into(imageView);
//DiskCacheStrategy.NONE： 表示不缓存任何内容。
//DiskCacheStrategy.SOURCE： 表示只缓存原始图片。
//DiskCacheStrategy.RESULT： 表示只缓存转换过后的图片（默认选项）。
//DiskCacheStrategy.ALL ： 表示既缓存原始图片，也缓存转换过后的图片。

//5、加载指定格式的图片--指定为静止图片
Glide.with(this)
     .load(url)
     .asBitmap()//只加载静态图片，如果是git图片则只加载第一帧。
     .placeholder(R.drawable.loading)
     .error(R.drawable.error)
     .diskCacheStrategy(DiskCacheStrategy.NONE)
     .into(imageView);

//6、加载动态图片
Glide.with(this)
     .load(url)
     .asGif()//加载动态图片，若现有图片为非gif图片，则直接加载错误占位图。
     .placeholder(R.drawable.loading)
     .error(R.drawable.error)
     .diskCacheStrategy(DiskCacheStrategy.NONE)
     .into(imageView);

//7、加载指定大小的图片
Glide.with(this)
     .load(url)
     .placeholder(R.drawable.loading)
     .error(R.drawable.error)
     .diskCacheStrategy(DiskCacheStrategy.NONE)
     .override(100, 100)//指定图片大小
     .into(imageView);

//8、关闭框架的内存机制
Glide.with(this)
     .load(url)
     .skipMemoryCache(true)  //传入参数为false时，则关闭内存缓存。
     .into(imageView);

//9、关闭框架的硬盘存储
Glide.with(this)
     .load(url)
     .diskCacheStrategy(DiskCacheStrategy.NONE)     //关闭硬盘缓存操作
     .into(imageView);
//其他参数表示：
//DiskCacheStrategy.NONE： 表示不缓存任何内容。
//DiskCacheStrategy.SOURCE： 表示只缓存原始图片。
//DiskCacheStrategy.RESULT： 表示只缓存转换过后的图片（默认选项）。
//DiskCacheStrategy.ALL ： 表示既缓存原始图片，也缓存转换过后的图片。
```

### 任意布局加载图片

```kotlin
//给ConstraintLayout添加背景
Glide.with(this).load(url).into(object :
            CustomViewTarget<ConstraintLayout, Drawable>(binding.bgGameDetail) {
            override fun onLoadFailed(errorDrawable: Drawable?) {

            }

            override fun onResourceReady(resource: Drawable, transition: Transition<in Drawable>?) {
                binding.bgGameDetail.background = resource;
            }

            override fun onResourceCleared(placeholder: Drawable?) {
            }

        });
```

### 修改存储位置和大小

```kotlin
package com.imi.gamestore

import android.content.Context
import com.bumptech.glide.GlideBuilder
import com.bumptech.glide.annotation.GlideModule
import com.bumptech.glide.load.engine.cache.DiskLruCacheFactory
import com.bumptech.glide.module.AppGlideModule
import com.imi.gamestore.utils.FileUtil


/**
 * 设置Glide缓存的大小和位置
 *
 * @size 1G
 * @location /sdcard/Android/data/包名/files/image
 */

@GlideModule
class CacheGlideModule : AppGlideModule() {

    private var diskCacheSizeBytes = 1024 * 1024 * 3000L // 3000 MB
    private var imagePath = FileUtil.getImagePath()

    override fun applyOptions(context: Context, builder: GlideBuilder) {
        builder.setDiskCache(DiskLruCacheFactory(imagePath, diskCacheSizeBytes))
    }

    override fun isManifestParsingEnabled(): Boolean {
        return false
    }

}
```

# 日志

### Xlog

+ [github地址](https://github.com/elvishew/XLog)

```kotlin
private fun initLog() {
        val config: LogConfiguration = LogConfiguration.Builder()
            .logLevel(LogLevel.DEBUG)           // 指定日志级别，低于该级别的日志将不会被打印，默认为 LogLevel.ALL
            .tag("FFF")                                         // 指定 TAG，默认为 "X-LOG"
            .enableThreadInfo()                                    // 允许打印线程信息，默认禁止
            .enableStackTrace(2)                                   // 允许打印深度为 2 的调用栈信息，默认禁止
            .enableBorder()                                        // 允许打印日志边框，默认禁止
            //.jsonFormatter( MyJsonFormatter())                  // 指定 JSON 格式化器，默认为 DefaultJsonFormatter
            //.xmlFormatter( MyXmlFormatter())                    // 指定 XML 格式化器，默认为 DefaultXmlFormatter
            //.throwableFormatter( MyThrowableFormatter())        // 指定可抛出异常格式化器，默认为 DefaultThrowableFormatter
            //.threadFormatter( MyThreadFormatter())              // 指定线程信息格式化器，默认为 DefaultThreadFormatter
            //.stackTraceFormatter( MyStackTraceFormatter())      // 指定调用栈信息格式化器，默认为 DefaultStackTraceFormatter
            //.borderFormatter( MyBoardFormatter())               // 指定边框格式化器，默认为 DefaultBorderFormatter
            //.addObjectFormatter(AnyClass.class,                    // 为指定类型添加对象格式化器
            //       new AnyClassObjectFormatter())                     // 默认使用 Object.toString()
            //.addInterceptor(new BlacklistTagsFilterInterceptor(    // 添加黑名单 TAG 过滤器
            //       "blacklist1", "blacklist2", "blacklist3"))
            //.addInterceptor(new MyInterceptor())                   // 添加一个日志拦截器
            .build()

        val androidPrinter = AndroidPrinter(true);         // 通过 android.util.Log 打印日志的打印器
        val consolePrinter = ConsolePrinter()             // 通过 System.out 打印日志到控制台的打印器
        val filePrinter = FilePrinter                   // 打印日志到文件的打印器
            .Builder(filesDir.absolutePath)                             // 指定保存日志文件的路径
            // .fileNameGenerator(new DateFileNameGenerator ())        // 指定日志文件名生成器，默认为 ChangelessFileNameGenerator("log")
            // .backupStrategy(new NeverBackupStrategy ())             // 指定日志文件备份策略，默认为 FileSizeBackupStrategy(1024 * 1024)
            // .cleanStrategy(new FileLastModifiedCleanStrategy (MAX_TIME))     // 指定日志文件清除策略，默认为 NeverCleanStrategy()
            // .flattener(new MyFlattener ())                          // 指定日志平铺器，默认为 DefaultFlattener
            .build();

        XLog.init(                                                 // 初始化 XLog
            config,                                                // 指定日志配置，如果不指定，会默认使用 new LogConfiguration.Builder().build()
            androidPrinter,                                        // 添加任意多的打印器。如果没有添加任何打印器，会默认使用 AndroidPrinter(Android)/ConsolePrinter(java)
            //consolePrinter,
            filePrinter
        )
    }
```



# 地图

### 百度

#### 获取经纬度

```java
public class BaiduLocationManager {
    private static final BaiduLocationManager ourInstance = new BaiduLocationManager();

    public static BaiduLocationManager getInstance() {
        return ourInstance;
    }

    private BaiduLocationManager() {
    }

    private GpsReceiver gpsReceiver;

    public void registerReceiver(Context context) {
        IntentFilter filter = new IntentFilter();
        filter.addAction(GPS_ACTION);
        gpsReceiver = new GpsReceiver(mIvGps);
        context.registerReceiver(gpsReceiver, filter);
    }

    public void unregisterReceiver(Context context) {
        context.unregisterReceiver(gpsReceiver);
    }

    public LocationClient mLocationClient = null;
    private MyLocationListener myListener = new MyLocationListener();

    public void initLocation() {
        mLocationClient = new LocationClient(GDSApplication.getContext());
        //声明LocationClient类
        mLocationClient.registerLocationListener(myListener);
        //注册监听函数
        LocationClientOption option = new LocationClientOption();
        option.setLocationMode(LocationClientOption.LocationMode.Hight_Accuracy);
        //可选，设置定位模式，默认高精度
        //LocationMode.Hight_Accuracy：高精度；
        //LocationMode. Battery_Saving：低功耗；
        //LocationMode. Device_Sensors：仅使用设备；

        /**
         *   bd09ll  表示百度经纬度坐标，
         *   gcj02   表示经过国测局加密的坐标，
         *   wgs84   表示gps获取的坐标。
         */
        option.setCoorType("bd09ll");
        //可选，设置返回经纬度坐标类型，默认GCJ02
        //GCJ02：国测局坐标；
        //BD09ll：百度经纬度坐标；
        //BD09：百度墨卡托坐标；
        //海外地区定位，无需设置坐标类型，统一返回WGS84类型坐标
        option.setScanSpan(1000);
        //可选，设置发起定位请求的间隔，int类型，单位ms
        //如果设置为0，则代表单次定位，即仅定位一次，默认为0
        //如果设置非0，需设置1000ms以上才有效
        option.setOpenGps(true);
        //可选，设置是否使用gps，默认false
        //使用高精度和仅用设备两种定位模式的，参数必须设置为true
        option.setLocationNotify(true);
        //可选，设置是否当GPS有效时按照1S/1次频率输出GPS结果，默认false
        option.setIgnoreKillProcess(false);
        //可选，定位SDK内部是一个service，并放到了独立进程。
        //设置是否在stop的时候杀死这个进程，默认（建议）不杀死，即setIgnoreKillProcess(true)
        option.SetIgnoreCacheException(false);
        //可选，设置是否收集Crash信息，默认收集，即参数为false
        option.setWifiCacheTimeOut(0);
        //可选，V7.2版本新增能力
        //如果设置了该接口，首次启动定位时，会先判断当前Wi-Fi是否超出有效期，若超出有效期，会先重新扫描Wi-Fi，然后定位
        option.setEnableSimulateGps(false);
        //可选，设置是否需要过滤GPS仿真结果，默认需要，即参数为false
        option.setOpenGps(true);  //是否开启gps定位
        mLocationClient.setLocOption(option);
        //mLocationClient为第二步初始化过的LocationClient对象
        //需将配置好的LocationClientOption对象，通过setLocOption方法传递给LocationClient对象使用
        //更多LocationClientOption的配置，请参照类参考中LocationClientOption类的详细说明
    }

    private LocationInfo locationInfo;

    public void setListener(LocationInfo listener) {

        locationInfo = listener;
    }

    public interface LocationInfo {
        void onSuccess(BDLocation bdLocation);

        void onFail(String error);
    }


    public class MyLocationListener extends BDAbstractLocationListener {
        @Override
        public void onReceiveLocation(BDLocation location) {
            //此处的BDLocation为定位结果信息类，通过它的各种get方法可获取定位相关的全部结果
            //以下只列举部分获取经纬度相关（常用）的结果信息
            //更多结果信息获取说明，请参照类参考中BDLocation类中的说明

            int tag = 1;
            StringBuffer sb = new StringBuffer(256);
            sb.append("time : ");
            /**
             * 时间也可以使用systemClock.elapsedRealtime()方法 获取的是自从开机以来，每次回调的时间；
             * location.getTime() 是指服务端出本次结果的时间，如果位置不发生变化，则时间不变
             */
            sb.append(location.getTime());
            sb.append("\nlocType : ");// 定位类型
            sb.append(location.getLocType());
            sb.append("\nlocType description : ");// *****对应的定位类型说明*****
            sb.append(location.getLocTypeDescription());
            sb.append("\nlatitude : ");// 纬度
            sb.append(location.getLatitude());
            sb.append("\nlongtitude : ");// 经度
            sb.append(location.getLongitude());
            sb.append("\nradius : ");// 半径
            sb.append(location.getRadius());
            sb.append("\nCountryCode : ");// 国家码
            sb.append(location.getCountryCode());
            sb.append("\nProvince : ");// 获取省份
            sb.append(location.getProvince());
            sb.append("\nCountry : ");// 国家名称
            sb.append(location.getCountry());
            sb.append("\ncitycode : ");// 城市编码
            sb.append(location.getCityCode());
            sb.append("\ncity : ");// 城市
            sb.append(location.getCity());
            sb.append("\nDistrict : ");// 区
            sb.append(location.getDistrict());
            sb.append("\nTown : ");// 获取镇信息
            sb.append(location.getTown());
            sb.append("\nStreet : ");// 街道
            sb.append(location.getStreet());
            sb.append("\naddr : ");// 地址信息
            sb.append(location.getAddrStr());
            sb.append("\nStreetNumber : ");// 获取街道号码
            sb.append(location.getStreetNumber());
            sb.append("\nUserIndoorState: ");// *****返回用户室内外判断结果*****
            sb.append(location.getUserIndoorState());
            sb.append("\nDirection(not all devices have value): ");
            sb.append(location.getDirection());// 方向
            sb.append("\nlocationdescribe: ");
            sb.append(location.getLocationDescribe());// 位置语义化信息
            sb.append("\nPoi: ");// POI信息
            if (location.getPoiList() != null && !location.getPoiList().isEmpty()) {
                for (int i = 0; i < location.getPoiList().size(); i++) {
                    Poi poi = (Poi) location.getPoiList().get(i);
                    sb.append("poiName:");
                    sb.append(poi.getName() + ", ");
                    sb.append("poiTag:");
                    sb.append(poi.getTags() + "\n");
                }
            }
            if (location.getPoiRegion() != null) {
                sb.append("PoiRegion: ");// 返回定位位置相对poi的位置关系，仅在开发者设置需要POI信息时才会返回，在网络不通或无法获取时有可能返回null
                PoiRegion poiRegion = location.getPoiRegion();
                sb.append("DerectionDesc:"); // 获取POIREGION的位置关系，ex:"内"
                sb.append(poiRegion.getDerectionDesc() + "; ");
                sb.append("Name:"); // 获取POIREGION的名字字符串
                sb.append(poiRegion.getName() + "; ");
                sb.append("Tags:"); // 获取POIREGION的类型
                sb.append(poiRegion.getTags() + "; ");
                sb.append("\nSDK版本: ");
            }
            if (location.getLocType() == BDLocation.TypeGpsLocation) {// GPS定位结果
                sb.append("\nspeed : ");
                sb.append(location.getSpeed());// 速度 单位：km/h
                sb.append("\nsatellite : ");
                sb.append(location.getSatelliteNumber());// 卫星数目
                sb.append("\nheight : ");
                sb.append(location.getAltitude());// 海拔高度 单位：米
                sb.append("\ngps status : ");
                sb.append(location.getGpsAccuracyStatus());// *****gps质量判断*****
                sb.append("\ndescribe : ");
                sb.append("gps定位成功");
                locationInfo.onSuccess(location);
            } else if (location.getLocType() == BDLocation.TypeNetWorkLocation) {// 网络定位结果
                // 运营商信息
                if (location.hasAltitude()) {// *****如果有海拔高度*****
                    sb.append("\nheight : ");
                    sb.append(location.getAltitude());// 单位：米
                }
                sb.append("\noperationers : ");// 运营商信息
                sb.append(location.getOperators());
                sb.append("\ndescribe : ");
                sb.append("网络定位成功");
                locationInfo.onSuccess(location);
            } else if (location.getLocType() == BDLocation.TypeOffLineLocation) {// 离线定位结果
                sb.append("\ndescribe : ");
                sb.append("离线定位成功，离线定位结果也是有效的");
                locationInfo.onSuccess(location);
            } else if (location.getLocType() == BDLocation.TypeServerError) {
                sb.append("\ndescribe : ");
                sb.append("服务端网络定位失败，可以反馈IMEI号和大体定位时间到loc-bugs@baidu.com，会有人追查原因");
                locationInfo.onFail(sb.toString());
            } else if (location.getLocType() == BDLocation.TypeNetWorkException) {
                sb.append("\ndescribe : ");
                sb.append("网络不同导致定位失败，请检查网络是否通畅");
                locationInfo.onFail(sb.toString());
            } else if (location.getLocType() == BDLocation.TypeCriteriaException) {
                sb.append("\ndescribe : ");
                sb.append("无法获取有效定位依据导致定位失败，一般是由于手机的原因，处于飞行模式下一般会造成这种结果，可以试着重启手机");
                locationInfo.onFail(sb.toString());
            }
            LogUtil.d(sb.toString());
        }


        @Override
        public void onLocDiagnosticMessage(int locType, int diagnosticType, String diagnosticMessage) {
            super.onLocDiagnosticMessage(locType, diagnosticType, diagnosticMessage);
            int tag = 2;
            StringBuffer sb = new StringBuffer(256);
            sb.append("诊断结果: ");
            if (locType == BDLocation.TypeOffLineLocationFail) {
                if (diagnosticType == 3) {
                    sb.append("定位失败，请您检查您的网络状态");
                    sb.append("\n" + diagnosticMessage);
                }
            } else if (locType == BDLocation.TypeCriteriaException) {
                if (diagnosticType == 4) {
                    sb.append("定位失败，无法获取任何有效定位依据");
                    sb.append("\n" + diagnosticMessage);
                } else if (diagnosticType == 5) {
                    sb.append("定位失败，无法获取有效定位依据，请检查运营商网络或者Wi-Fi网络是否正常开启，尝试重新请求定位");
                    sb.append(diagnosticMessage);
                } else if (diagnosticType == 6) {
                    sb.append("定位失败，无法获取有效定位依据，请尝试插入一张sim卡或打开Wi-Fi重试");
                    sb.append("\n" + diagnosticMessage);
                } else if (diagnosticType == 7) {
                    sb.append("定位失败，飞行模式下无法获取有效定位依据，请关闭飞行模式重试");
                    sb.append("\n" + diagnosticMessage);
                } else if (diagnosticType == 9) {
                    sb.append("定位失败，无法获取任何有效定位依据");
                    sb.append("\n" + diagnosticMessage);
                }
            } else if (locType == BDLocation.TypeServerError) {
                if (diagnosticType == 8) {
                    sb.append("定位失败，请确认您定位的开关打开状态，是否赋予APP定位权限");
                    sb.append("\n" + diagnosticMessage);
                }
            }
        }
    }

    public void startLocation() {
        if (mLocationClient != null) {
            //mLocationClient为第二步初始化过的LocationClient对象
            //调用LocationClient的start()方法，便可发起定位请求
            mLocationClient.start();
        }
    }

    public void stopLocation() {
        if (mLocationClient != null) {
            mLocationClient.stop();
        }
    }
```



# 工具库

+ [非常好用的工具库](https://github.com/Blankj/AndroidUtilCode)

### 经纬度转换

```java
/**
 * 将百度坐标转换成GPS坐标工具类
 * <p>
 * 参考
 * https://www.cnblogs.com/fuyinshan/p/6733459.html
 * https://blog.csdn.net/yingtian648/article/details/79000331
 * https://github.com/taoweiji/JZLocationConverter-for-Android
 * <p>
 * 高德和谷歌国内使用火星坐标，国外使用wgs84
 * 百度国内使用BD-09坐标,国外使用wgs84
 */
public class LocationUtil {
    public final static double a = 6378245.0;
    private final static double ee = 0.00669342162296594323;

    private static double LAT_OFFSET_0(double x, double y) {
        return -100.0 + 2.0 * x + 3.0 * y + 0.2 * y * y + 0.1 * x * y + 0.2 * Math.sqrt(Math.abs(x));
    }

    private static double LAT_OFFSET_1(double x, double y) {
        return (20.0 * Math.sin(6.0 * x * Math.PI) + 20.0 * Math.sin(2.0 * x * Math.PI)) * 2.0 / 3.0;
    }

    private static double LAT_OFFSET_2(double x, double y) {
        return (20.0 * Math.sin(y * Math.PI) + 40.0 * Math.sin(y / 3.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static double LAT_OFFSET_3(double x, double y) {
        return (160.0 * Math.sin(y / 12.0 * Math.PI) + 320 * Math.sin(y * Math.PI / 30.0)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_0(double x, double y) {
        return 300.0 + x + 2.0 * y + 0.1 * x * x + 0.1 * x * y + 0.1 * Math.sqrt(Math.abs(x));
    }

    private static double LON_OFFSET_1(double x, double y) {
        return (20.0 * Math.sin(6.0 * x * Math.PI) + 20.0 * Math.sin(2.0 * x * Math.PI)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_2(double x, double y) {
        return (20.0 * Math.sin(x * Math.PI) + 40.0 * Math.sin(x / 3.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_3(double x, double y) {
        return (150.0 * Math.sin(x / 12.0 * Math.PI) + 300.0 * Math.sin(x / 30.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static final double RANGE_LON_MAX = 137.8347;
    private static final double RANGE_LON_MIN = 72.004;
    private static final double RANGE_LAT_MAX = 55.8271;
    private static final double RANGE_LAT_MIN = 0.8293;

    private static final double jzA = 6378245.0;
    private static final double jzEE = 0.00669342162296594323;

    private static double transformLat(double x, double y) {
        double ret = LAT_OFFSET_0(x, y);
        ret += LAT_OFFSET_1(x, y);
        ret += LAT_OFFSET_2(x, y);
        ret += LAT_OFFSET_3(x, y);
        return ret;
    }

    private static double transformLon(double x, double y) {
        double ret = LON_OFFSET_0(x, y);
        ret += LON_OFFSET_1(x, y);
        ret += LON_OFFSET_2(x, y);
        ret += LON_OFFSET_3(x, y);
        return ret;
    }

    public static boolean outOfChina(double lat, double lon) {
        if (lon < RANGE_LON_MIN || lon > RANGE_LON_MAX)
            return true;
        if (lat < RANGE_LAT_MIN || lat > RANGE_LAT_MAX)
            return true;
        return false;
    }

    private static LatLng gcj02Encrypt(double ggLat, double ggLon) {
        LatLng resPoint = new LatLng();
        double mgLat;
        double mgLon;
        if (outOfChina(ggLat, ggLon)) {
            resPoint.latitude = ggLat;
            resPoint.longitude = ggLon;
            return resPoint;
        }
        double dLat = transformLat(ggLon - 105.0, ggLat - 35.0);
        double dLon = transformLon(ggLon - 105.0, ggLat - 35.0);
        double radLat = ggLat / 180.0 * Math.PI;
        double magic = Math.sin(radLat);
        magic = 1 - jzEE * magic * magic;
        double sqrtMagic = Math.sqrt(magic);
        dLat = (dLat * 180.0) / ((jzA * (1 - jzEE)) / (magic * sqrtMagic) * Math.PI);
        dLon = (dLon * 180.0) / (jzA / sqrtMagic * Math.cos(radLat) * Math.PI);
        mgLat = ggLat + dLat;
        mgLon = ggLon + dLon;

        resPoint.latitude = mgLat;
        resPoint.longitude = mgLon;
        return resPoint;
    }

    private static LatLng gcj02Decrypt(double gjLat, double gjLon) {
        LatLng gPt = gcj02Encrypt(gjLat, gjLon);
        double dLon = gPt.longitude - gjLon;
        double dLat = gPt.latitude - gjLat;
        LatLng pt = new LatLng();
        pt.latitude = gjLat - dLat;
        pt.longitude = gjLon - dLon;
        return pt;
    }

    private static LatLng bd09Decrypt(double bdLat, double bdLon) {
        LatLng gcjPt = new LatLng();
        double x = bdLon - 0.0065, y = bdLat - 0.006;
        double z = Math.sqrt(x * x + y * y) - 0.00002 * Math.sin(y * Math.PI);
        double theta = Math.atan2(y, x) - 0.000003 * Math.cos(x * Math.PI);
        gcjPt.longitude = z * Math.cos(theta);
        gcjPt.latitude = z * Math.sin(theta);
        return gcjPt;
    }

    private static LatLng bd09Encrypt(double ggLat, double ggLon) {
        LatLng bdPt = new LatLng();
        double x = ggLon, y = ggLat;
        double z = Math.sqrt(x * x + y * y) + 0.00002 * Math.sin(y * Math.PI);
        double theta = Math.atan2(y, x) + 0.000003 * Math.cos(x * Math.PI);
        bdPt.longitude = z * Math.cos(theta) + 0.0065;
        bdPt.latitude = z * Math.sin(theta) + 0.006;
        return bdPt;
    }

    /**
     * @param location 世界标准地理坐标(WGS-84)
     * @return 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @brief 世界标准地理坐标(WGS - 84) 转换成 中国国测局地理坐标（GCJ-02）<火星坐标>
     * <p>
     * ####只在中国大陆的范围的坐标有效，以外直接返回世界标准坐标
     */
    public static LatLng wgs84ToGcj02(LatLng location) {
        return gcj02Encrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 中国国测局地理坐标（GCJ-02）
     * @return 世界标准地理坐标（WGS-84）
     * @brief 中国国测局地理坐标（GCJ-02） 转换成 世界标准地理坐标（WGS-84）
     * <p>
     * ####此接口有1－2米左右的误差，需要精确定位情景慎用
     */
    public static LatLng gcj02ToWgs84(LatLng location) {
        return gcj02Decrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 世界标准地理坐标(WGS-84)
     * @return 百度地理坐标（BD-09)
     * @brief 世界标准地理坐标(WGS - 84) 转换成 百度地理坐标（BD-09)
     */
    public static LatLng wgs84ToBd09(LatLng location) {
        LatLng gcj02Pt = gcj02Encrypt(location.latitude, location.longitude);
        return bd09Encrypt(gcj02Pt.latitude, gcj02Pt.longitude);
    }

    /**
     * @param location 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @return 百度地理坐标（BD-09)
     * @brief 中国国测局地理坐标（GCJ-02）<火星坐标> 转换成 百度地理坐标（BD-09)
     */
    public static LatLng gcj02ToBd09(LatLng location) {
        return bd09Encrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 百度地理坐标（BD-09)
     * @return 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @brief 百度地理坐标（BD-09) 转换成 中国国测局地理坐标（GCJ-02）<火星坐标>
     */
    public static LatLng bd09ToGcj02(LatLng location) {
        return bd09Decrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 百度地理坐标（BD-09)
     * @return 世界标准地理坐标（WGS-84）
     * @brief 百度地理坐标（BD-09) 转换成 世界标准地理坐标（WGS-84）
     * <p>
     * ####此接口有1－2米左右的误差，需要精确定位情景慎用
     */
    public static LatLng bd09ToWgs84(LatLng location) {
        LatLng gcj02 = bd09ToGcj02(location);
        return gcj02Decrypt(gcj02.latitude, gcj02.longitude);
    }

    public static class LatLng {
        public double latitude;
        public double longitude;

        public LatLng(double latitude, double longitude) {
            this.latitude = latitude;
            this.longitude = longitude;
        }

        public LatLng() {
        }

        public double getLatitude() {
            return latitude;
        }

        public void setLatitude(double latitude) {
            this.latitude = latitude;
        }

        public double getLongitude() {
            return longitude;
        }

        public void setLongitude(double longitude) {
            this.longitude = longitude;
        }
    }

    /*
     * 大地坐标系资料WGS-84 长半径a=6378137 短半径b=6356752.3142 扁率f=1/298.2572236
     *
     *  根据一点的经纬度和距离来计算另一个点的经纬度
     */
    /**
     * 扁率f=1/298.2572236
     */
    private static double f = 1 / 298.2572236;

    /**
     * 计算另一点经纬度
     *
     * @param lon  wgs84经度
     * @param lat  wgs84维度
     * @param brng 方位角
     * @param dist 距离（米）
     */
    public static LatLng computerThatLonLat(double lon, double lat, double brng, double dist) {

        double alpha1 = rad(brng);
        double sinAlpha1 = Math.sin(alpha1);
        double cosAlpha1 = Math.cos(alpha1);

        double tanU1 = (1 - f) * Math.tan(rad(lat));
        double cosU1 = 1 / Math.sqrt((1 + tanU1 * tanU1));
        double sinU1 = tanU1 * cosU1;
        double sigma1 = Math.atan2(tanU1, cosAlpha1);
        double sinAlpha = cosU1 * sinAlpha1;
        double cosSqAlpha = 1 - sinAlpha * sinAlpha;
        /**
         * 长半径a=6378137
         */
        double longRadius = 6378137;
        /**
         * 短半径b=6356752.3142
         */
        double shortRadius = 6356752.3142;
        double uSq = cosSqAlpha * (longRadius * longRadius - shortRadius * shortRadius) / (shortRadius * shortRadius);
        double A = 1 + uSq / 16384 * (4096 + uSq * (-768 + uSq * (320 - 175 * uSq)));
        double B = uSq / 1024 * (256 + uSq * (-128 + uSq * (74 - 47 * uSq)));

        double cos2SigmaM = 0;
        double sinSigma = 0;
        double cosSigma = 0;
        double sigma = dist / (shortRadius * A), sigmaP = 2 * Math.PI;
        while (Math.abs(sigma - sigmaP) > 1e-12) {
            cos2SigmaM = Math.cos(2 * sigma1 + sigma);
            sinSigma = Math.sin(sigma);
            cosSigma = Math.cos(sigma);
            double deltaSigma = B * sinSigma * (cos2SigmaM + B / 4 * (cosSigma * (-1 + 2 * cos2SigmaM * cos2SigmaM)
                    - B / 6 * cos2SigmaM * (-3 + 4 * sinSigma * sinSigma) * (-3 + 4 * cos2SigmaM * cos2SigmaM)));
            sigmaP = sigma;
            sigma = dist / (shortRadius * A) + deltaSigma;
        }

        double tmp = sinU1 * sinSigma - cosU1 * cosSigma * cosAlpha1;
        double lat2 = Math.atan2(sinU1 * cosSigma + cosU1 * sinSigma * cosAlpha1,
                (1 - f) * Math.sqrt(sinAlpha * sinAlpha + tmp * tmp));
        double lambda = Math.atan2(sinSigma * sinAlpha1, cosU1 * cosSigma - sinU1 * sinSigma * cosAlpha1);
        double C = f / 16 * cosSqAlpha * (4 + f * (4 - 3 * cosSqAlpha));
        double L = lambda - (1 - C) * f * sinAlpha
                * (sigma + C * sinSigma * (cos2SigmaM + C * cosSigma * (-1 + 2 * cos2SigmaM * cos2SigmaM)));

        double revAz = Math.atan2(sinAlpha, -tmp); // final bearing

        System.out.println(revAz);
        System.out.println(lon + deg(L) + "," + deg(lat2));
        LatLng latLng = new LatLng(deg(lat2), lon + deg(L));
        return latLng;
    }

    /**
     * 度换成弧度
     *
     * @param d 度
     * @return 弧度
     */
    private static double rad(double d) {
        return d * Math.PI / 180.0;
    }

    /**
     * 弧度换成度
     *
     * @param x 弧度
     * @return 度
     */
    private static double deg(double x) {
        return x * 180 / Math.PI;
    }
}
```

+
