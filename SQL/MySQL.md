# 基础

## 安装

### mac

```
brew install mysql
```



## 启动

### mac

```
//使用服务
brew services start mysql
//不使用服务，只是启动
mysql.service start
```

### linux

```
service mysqld start  //启动数据库
service mysqld stop  //关闭数据库
```

## 运行

```sql
//进入mysql工作台
mysql -u root -p   //mac默认没有密码
```

# 增删改查

## 基础命令

```sql
1.show databases;   //显示所有数据库
2.create(drop) database lijie; //创建和删除lijie数据库
3.use lijie;  //使用lijie数据库
4.show tables; //展示当前数据库下的所有表
5.create table <表名> (<字段名1> <类型1> [,..<字段名n> <类型n>]);   //创建表

例子: 
create table Student(id int(4) not null primary key auto_increment,name char(20) not null,sex int(4) not null default '0',degree double(16,2));
//创建一个学生成绩表
6.drop table Student   //删除学生成绩表
```

## 增

+ 插入语句
```sql
INSERT INTO 表名[(字段名1,字段名2,..)'] VALUES(值1,值2,..);
例1:
INSERT INTO student[(id,name,grade)] VALUES(1,'zhangshan',98);
//向学生表中插入一条所有字段数据,字段名可省略
例2:
INSERT INTO student[(id,name)] VALUES(3,'wangwu');
//向学生表中插入指定字段数据
```
+ 其他写法
```sql
INSERT INTO 表名 SET 字段名1=值1[,字段名2=值2，…]
例:
INSERT INTO student SET id=4，name='zhaoliu',grade=72;
//向学生表中插入一条数据
```
+ 同时插入多条数据
```sql
INSERT INTO 表名[(字段名1,字段名2,…)] VALUES(值1,值2,…),(值1,值2,…),…(值1,值2,…)
例:
INSERT INTO student VALUES(5,'lilei',99),(6,'hanmeimei',87),(8,'poly',76);
//同时向学生表插入三条数据
```

## 删

+ 删除部分数据
```sql
DELETE FROM 表名 [WHERE 条件表达式]
例:
DELETE  FROM student WHERE id=7;   //删除学生表中的id值为7的记录
```
+ 删除全部数据
```sql
DELETE FROM 表名
例:
DELETE FROM student;    //删除学生表的所有数据
```

## 改

+ 更新数据
```sql
UPDATE 表名 SET 字段名1=值1,[,字段名2=值2,…] [WHERE 条件表达式]
例1:
UPDATE student SET name='caocao',grade=50 WHERE id=1;
//更新学生表id为1的记录

例2:
UPDATE student SET grade=80;
//更新学生表中全部记录,将grade字段更新为80
```

## 查

```sql
SELECT 字段名1,字段名2,… FROM 表名
例:
SELECT id,name,grade FROM student;
//查询学生表中的id,name,grade字段(查询所有字段可替换为*)
```
+ 条件查询
```sql
SELECT 字段名1,字段名2,…FROM 表名WHERE 条件表达式
例:
SELECT id,name FROM student  WHERE id=4;
//查询学生表中id为4的id和name字段
```
+ 带IN关键字的查询
```sql
SELECT * | 字段名1,字段名2,…FROM 表名 WHERE 字段名 [NOT] IN (元素1,元素2,…)
例:
SELECT * FROM student WHERE  id IN (1,2,3);
//查询student表中id值为1,2,3的记录
```
+ 带BETWEEN AND关键字的查询
```sql
SELECT * | { 字段名1，字段名2，… } FROM 表名 WHERE 字段名 [ NOT ] BETWEEN 值1 AND 值2;
例:
SELECT id,name FROM student WHERE id BETWEEN 2 AND 5;
//查询student表中id值在2~5之间的人的id和name
```
+ 带DISTINCT关键字的查询
```sql
SELECT DISTINCT 字段名 FROM 表名;
例:
SELECT DISTINCT gender FROM student;
//查询学生表中gender字段的值，结果中不允许出行重复的值。
```
+ 带LIKE关键字的查询
```sql
SELECT * | 字段名1,字段名2,… FROM 表名 WHERE 字段名 [NOT] LIKE '匹配字符串';
例:
SELECT id,name FROM student WHERE name LIKE "S%"
//查询student表中name字段以字符"s"开头的人的id,name
```