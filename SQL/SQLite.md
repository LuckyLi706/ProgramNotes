# SQLite

+ [命令行工具](https://www.sqlite.org/download.html)
+ [可视化工具](http://www.sqliteexpert.com/download.html)

## 增删改查

### 基本数据类型

```
存储类型：integer(整型)、real(浮点型)、text(文本字符串)、blob(二进制数据)
    字段解释：not null：字段的值不能为空。
            unique：字段的值必需唯一。
            default：指定字段的默认值。
            primary key：主键，用来唯一的标识某条记录，相当于记录的身份证。主键可以是一个或多个字段，应由计算机自动生成和管理。主键字段默认包含了not null和unique两个约束。
            autoincrement：当主键是integer类型时，应该增加autoincrement约束，能实现主键值的自动增长
```

### 基础命令

```
//创建数据库（如果存在就打开数据库）
sqlite3 DatabaseName.db

//查看数据库所有表
.tables

//创建表
CREATE TABLE COMPANY(
   ID INT PRIMARY KEY     NOT NULL,
   NAME           TEXT    NOT NULL,
   AGE            INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL
);

//删除表
DROP TABLE COMPANY;
DROP TABLE IF EXISTS 表名;

//查看表结构
.schema 表名

//推出操作界面
.quit
```

### 增

```
INSERT INTO TABLE_NAME [(column1, column2, column3,...columnN)]  VALUES (value1, value2, value3,...valueN);

例子：（以下插入方式都可以）
1、INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) VALUES (1, 'Paul', 32, 'California', 20000.00 );
2、INSERT INTO COMPANY VALUES (7, 'James', 24, 'Houston', 10000.00 );  
```

### 删

```
//将表内的一个记录删除
delete from table_name where condition;

//其中删除记录需要在where后输入附加条件，如果有多个条件，则可以使用AND/OR连接条件。例如：
//表示从表student中删除number等于10102的记录。
delete from student where number = 10102;

//表示从表student中删除score小于60并且sex为nan的记录。
delete from student where score < 60 AND sex = 'nan';

//如果想删除某表内所有记录，则可以输入命令
delete from table_name;
```

### 改

```
//如果想修改表内某个记录的某个或某几个列的值，则可以输入命令
//其中修改记录需要在where后输入附加条件，如果有多个条件，则可以使用AND/OR连接条件。
update table_name set column1 = value1, column2 = value2…… where condition;
```

### 查

```
//使用select语句可以输出一个表内指定的列信息，然后使用where子句确定筛选条件。
select column1,column2…… from table_name where condition;

//如果想输出表内所有列，则可以将column指定为
select * from table_name;//输出表内所有列的信息
```

