# 基础

## 安装

+ [MongoDB官网](https://www.mongodb.com/)

+ [MongoDB中文社区](http://www.mongoing.com/)

+ [MongoDB下载地址](https://www.mongodb.com/download-center/community)

### mac

```
brew install mysql
```

### windows

```
// Linux类似操作
1.解压MongoDB压缩包
2.在文件夹下创建data文件夹以及logs文件,创建配置文件mongod.conf文件,修改path(log文件存储位置)、dbPath(数据存储位置)、pidFilePath(pid文件存储地址)

mongod.conf配置文件
#日志文件位置 （必须）
logpath=D:\DataBase\mongodb-4.0.4\logs\mongo.log
# 以追加方式写入日志
logappend=true
# 是否以守护进程方式运行
fork = true
# 默认27017
#port = 27017
# 数据库文件位置（必须）
dbpath=D:\DataBase\mongodb-4.0.4\data 
# 启用定期记录CPU利用率和 I/O 等待
#cpu = true
# 是否以安全认证方式运行，默认是不认证的非安全方式

//集群搭建
1.按照以上方式启动多个MongoDB节点.
2.使用mongo命令进入任一节点,输入
config = { _id:"repset", members:[ {_id:0,host:"10.100.1.154:27018",priority:1},{_id:1,host:"10.100.1.154:27019",arbiterOnly:true},{_id:2,host:"10.100.1.153:27018",priority:2}] }
//1为从节点,2为主节点,arbiterOnly:true为仲裁
#初始化副本集配置
rs.initiate(config)
注：mongodb默认是从主节点读写数据的，副本节点上不允许读，需要设置副节点可读
db.getMongo().setSlaveOk()
```

## 启动

### mac

```

```

### linux

```

```

### windows

```
mongod -f mongdb.conf     //启动MongDB
```



## 进入console

```sql
直接进入bin目录 输入mongo 
```

# 增删改查

## 基础命令

```sql
#数据库(db)
1.一个数据库可以有多个集合，应该将一个应用的所有数据存在一个数据库上。
2.一个mongoDB的实例可以运行多个database，database之间是完全独立的，每个database有自己的权限，每个database存储于磁盘的不同文件。
3.三个保留数据库名：admin、local、config
4.show dbs 展示所有数据库名

#集合(collection)
1.相当于关系数据库的表，不过没有数据结构的定义。它有多个document组成。因为是无结构定义的，所以你可以把任何document存入一个collection里
2.show collections  展示当前数据库下的所有集合名

#文档(document)
1.document中的键值对是有序的
2.document中的值(value)可以由很多类型，字符串，数字，一个另外的文档……
3.每一个document都有自己的_id，它在document所处的collection是唯一的。

#其他
1.use dfp  切换数据库到dfp
2.db.fingerprint  当前数据库下的fingerprint集合
3.rs和sh相关命令
```

## 增

```sql

```
## 删

```sql
#删除库  
db.dropDatabase()  //固定格式,删除当前库(不用跟参数,区分大小写)

#删除集合
db.dfp.drop()   //删除当前数据库下的dfp集合

#删除数据
db.dfp.remove({条件})  //删除该集合中满足条件的所有数据
```
## 改

+ 更新数据
```sql

```

## 查

```sql
#查询全部数据：
db.persons.find()

#查询指定的键对应的信息：
db.persons.find({ 条件 },{ 要查询的键 })

如：db.persons.find({},{_id:0,price:1}) 
{}表示从全部数据中查询,_id写0是不展示_id,其他字段不展示可以不写,1表示展示price

#按条件查询
1、对应的条件语句：$lt(小于)、$lte(小于等于)、
$gt(大于)、$gte(大于等于)、$ne(不等于)
如：db.persons.find({price:{$gte:20,$lte:30}},{_id:0,price:1})
第一个范围中找第二个参数的信息
2.

#管道聚合（关键字aggregate aggregate管道聚合的返回数据不能超过16M，超过16M就会报异常错误。解决方法就是设置allowDiskUse:true，即允许使用磁盘缓存。）[效率高]
http://www.runoob.com/mongodb/mongodb-aggregate.html

#模糊查询
db.persons.find({"personName":/名字的部分字符/})
```