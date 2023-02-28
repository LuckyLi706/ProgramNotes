# MySQL

+ [MySQL下载地址](https://downloads.mysql.com/archives/community/)

+ [mac数据库操作（忘记密码）](https://blog.csdn.net/w893932747/article/details/89337631)
+ [Mac上修改MySQL默认字符集为utf8](https://www.cnblogs.com/jie-fang/p/10214207.html)
+ [mysql命令行修改字符编码](https://www.cnblogs.com/chcong/p/6197238.html)

## 安装和启动

### mac

1. 下载MySQL，[下载地址](https://downloads.mysql.com/archives/community/)

   brew install mysql       //默认安装8.0版本

2. 配置文件

   默认配置文件位置：/usr/local/etc/my.cnf

3. 启动

   ````
   //使用服务
   brew services start mysql
   //不使用服务，只是启动
   mysql.server start
   ````

4. 进入数据库

   ```
   //进入mysql工作台
   mysql -u root -p   //mac默认没有密码
   
   //windows,根据初始化密码进入数据库,然后插入修改密码
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
   
   //mac mysql8.0修改验证方式
   1、找到mysql配置文件并加入default_authentication_plugin=mysql_native_password
   2、ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';
   ```

### windows

1. 下载MySQL，[下载地址](https://downloads.mysql.com/archives/community/)
2. 在解压后的文件目录下新建一个my.ini文件（以下是配置内容）

```ini
[mysqld]
# 设置端口
port=3306
# 安装目录
basedir=C:\\ProgramFiles\\mysql-8.0.17-winx64   # 我把和w键那行的反斜线记忆为windows的，另一个为linux版的斜线
# 设置数据库数据存放目录
datadir=C:\\ProgramFiles\\mysql-8.0.17-winx64\\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 字符集默认为UTF8
character-set-server=utf8
# 创建新表时默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置客户端默认字符集
default-character-set=utf8
[client]
# 客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```

2. 初始化数据
   mysqld --initialize --console
   在这边拿到初始化密码
   [Server] A temporary password is generated for root@localhost:初始密码

3. mysqld --install
   成功后会提示安装成功

4. 启动

   ```
   net start mysql  //启动数据库
   net stop mysql  //关闭数据库
   ```

5. 进入数据库

   ```
   //进入mysql工作台
   mysql -u root -p   //mac默认没有密码
   
   //windows,根据初始化密码进入数据库,然后插入修改密码
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
   
   //mac mysql8.0修改验证方式
   1、找到mysql配置文件并加入default_authentication_plugin=mysql_native_password
   2、ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';
   ```

### linux

1. 查看是否有MySQL

   ```
   rpm -qa | grep mysql  //查看是否安装了MySQL
   rpm -e xxx   //删除
   ```

2. 下载MySQL，[下载地址](https://downloads.mysql.com/archives/community/)

   wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz

3. 解压下载的mysql

   tar xzvf mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz

4. 移动mysql到/usr/local目录下

   mv mysql-5.7.24-linux-glibc2.12-x86_64 /usr/local/
   cd /usr/local/
   mv mysql-5.7.24-linux-glibc2.12-x86_64 mysql

5. 改变mysql权限

   chown -R mysql:mysql /usr/local/mysql
   chmod -R 755 /usr/local/mysql

6. 编辑配置文件my.cnf，添加配置如下（文件在/etc/my.cnf，没有就新建）

   ```mysql
   [mysqld]
   bind-address=0.0.0.0
   port=3306
   user=mysql
   basedir=/usr/local/mysql
   datadir=/usr/local/mysql/data/
   socket=/tmp/mysql.sock
   log-error=/usr/local/mysql/data/mysql.err
   pid-file=/usr/local/mysql/data/mysql.pid
   #character config
   character_set_server=utf8mb4
   symbolic-links=0
   explicit_defaults_for_timestamp=true
   ```

7. 初始化（临时密码在/usr/local/mysql/data/mysql.err里面）

   ```
   cd /usr/local/mysql/bin/
   ./mysqld --defaults-file=/etc/my.cnf --basedir=/usr/local/mysql/ --datadir=/usr/local/mysql/data/ --user=root --initialize
   ```

8. 启动MySQL

   ```
   cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
   service mysql start   //启动数据库
   service mysql stop   //停止数据库
   service mysql restart   //重启数据库
   ```

9. 进入数据库

   ```
   mysql -u root -p   //输入密码
   ```

#### 问题点

+ 执行第5步的时候，出现error while loading shared libraries: libnuma.so.1: cannot open shared object file: No such file or directory

  ```shell
  yum -y install numactl
  ```

+ Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)

  ```shell
  //建立软链接
  ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock
  ln -s /tmp/mysql.sock /var/lib/mysql/mysql.sock
  ```

+ You must reset your password using ALTER USER statement before executing this statement.

  ```
  //MySQL版本5.7.6版本以前用户可以使用如下命令：
  mysql> SET PASSWORD = PASSWORD('Admin2022!');
  
  MySQL版本5.7.6版本开始的用户可以使用如下命令：
  mysql> ALTER USER USER() IDENTIFIED BY 'Admin2022!';
  ```

  

## 增删改查

### 基础命令

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
7.describe Student;  //展示学生表的内容
```

### 增

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

### 删

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

### 改

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

### 查

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