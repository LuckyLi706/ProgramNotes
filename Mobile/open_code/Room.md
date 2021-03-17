# Room

+ [官网](https://developer.android.google.cn/training/data-storage/room)

## 入门

### 集成

```groovy
dependencies {
  def room_version = "2.2.5"

  implementation "androidx.room:room-runtime:$room_version"
  annotationProcessor "androidx.room:room-compiler:$room_version"

  // optional - RxJava support for Room
  implementation "androidx.room:room-rxjava2:$room_version"

  // optional - Guava support for Room, including Optional and ListenableFuture
  implementation "androidx.room:room-guava:$room_version"

  // optional - Test helpers
  testImplementation "androidx.room:room-testing:$room_version"
}
```

### 第一个例子

```java
//实体
    @Entity
    public class User {
        @PrimaryKey
        public int uid;

        @ColumnInfo(name = "first_name")
        public String firstName;

        @ColumnInfo(name = "last_name")
        public String lastName;
    }

//Dao层（可配合RxJava来返回）
    @Dao
    public interface UserDao {
        @Query("SELECT * FROM user")
        List<User> getAll();

        @Query("SELECT * FROM user WHERE uid IN (:userIds)")
        List<User> loadAllByIds(int[] userIds);

        @Query("SELECT * FROM user WHERE first_name LIKE :first AND " +
               "last_name LIKE :last LIMIT 1")
        User findByName(String first, String last);

        @Insert
        void insertAll(User... users);

        @Delete
        void delete(User user);
    }

//数据库实例
@Database(entities = {User.class}, version = 1, exportSchema = false)
public abstract class AppDataBase extends RoomDatabase {

    private static String DB_PATH = FileUtil.getStoragePath("db") + "/" + Constants.DB_NAME;

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

//调用
AppDataBase.getInstance().getUserDao().getAll();   //获取User表的所有数据
```

## 实体

### 字段不入库

```java
@Entity
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String lastName;

    @Ignore   //该注解表示当前字段不入库
    Bitmap picture;
}
```

### 主键

```java
@Entity(primaryKeys = {"firstName", "lastName"})  //多个主键
public class User {
    public String firstName;
    public String lastName;

    @Ignore
    Bitmap picture;
}
```

### 字段别名

```java
@Entity(tableName = "users")  //默认数据库名和实体名一样,实体tableName可以修改数据库名
public class User {
    @PrimaryKey
    public int id;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")  //默认字段名和变量名一样,可以使用name来修改字段名
    public String lastName;

    @Ignore
    Bitmap picture;
}
```

## 表关联

### 一对一

### 一对多

### 一对多

## 存储复杂数据

### 自定义转换器

```java
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

## 增删改查

```java
@Dao
public interface UserDao {

    @Insert
    void insertOne(User user);

    @Query("SELECT * FROM User WHERE username = 'admin'")
    List<User> getAdmin();
    
    //以下是配合RxJava使用的
    @Query("SELECT * FROM User WHERE username = (:name)")
    Maybe<List<User>> getUser(String name);

    @Update
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

## 数据库升级

## 相关问题

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

