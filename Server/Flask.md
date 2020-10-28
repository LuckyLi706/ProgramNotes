# Flask

## 请求

+ https://www.jianshu.com/p/f644330c596a
+ https://www.jianshu.com/p/54057b4f0437

## MySQL

+ [操作mysql数据库](https://www.cnblogs.com/ccorz/p/5711955.html)
+ http://www.bjhee.com/flask-ext4.html

## MongoDB

### 连接mongo数据库
```python
  import pymongo   #导入mongo库
  mongo = pymongo.MongoClient('127.0.0.1', 27017)  #连接mongo对象实例
  db_name = mongo.test  # 获取数据库
  db_collection = db_name.dfp  # 获取集合对象
  brand1 = [{"$match": {"platform": "AND"}}, {"$group": {"_id": "$brand", "total": {"$sum": 1}}}]   #内联查询语句
  result = db_collection.aggregate(brand1, allowDiskUse=True) （result为对象）
```