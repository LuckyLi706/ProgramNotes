# Flask

## 入门

+ [Python](../Python.md)
+ [Flask v2.2.x 英文文档 ](https://flask.palletsprojects.com/en/2.2.x/)
+ [Flask v2.1.x 中文文档 ](https://dormousehole.readthedocs.io/en/latest/)

### 注意点

```python
# 使用python运行
python app.py (此时会走main函数)

# 使用flask运行
flask run -p 8080 -h 0.0.0.0 （指定主机和端口，此时不会走main函数）
```

## 请求和响应

#### GET和POST

```python
import json

from flask import Flask
from flask import request

@app.route('/')
def hello_world():  # put application's code here
    return 'Hello World!'


# 参数可以携带请求发送
@app.route('/user/<username>')
def profile(username):
    return f'{username}\'s profile'


# GET和POST普通请求
@app.route('/login', methods=['GET', 'POST'])
def get_post_request():
    if request.method == 'GET':
        # 通过这种方式获取GET请求的值，
        # 如果当前请求不存在这个键，会引发一个 KeyError
        user_name_get = request.args.get('user', '')
        pass_word_get = request.args.get('pass', '')
        # 格式化字符串
        return "user：%s，pass：%s" % (user_name_get, pass_word_get)
    else:
        if request.method == 'POST':
            # 通过这种方式获取POST提交的表单
            if len(request.form) != 0:
                user_name_get = request.form['user']
                pass_word_get = request.form['pass']
                return "user：%s，pass：%s" % (user_name_get, pass_word_get)
            else:
                # 通过这种方式获取POST提交的json数据
                json_data = request.get_data()
                # 将拿到的数据转为json
                json_data_value = json.loads(json_data)
                return "user：%s，pass：%s" % (json_data_value['user'], json_data_value['pass'])
        else:
            return 'NOT SUPPORT METHOD'


if __name__ == '__main__':
    app.run()
```

#### 文件上传

```python
import json
import os

from flask import Flask
from flask import request

# 获取当前目录
basedir = os.path.abspath(os.path.dirname(__file__))
app = Flask(__name__)


# 上传单个文件
@app.route('/upload', methods=['POST'])
def upload_file():
    if request.method == "POST":
        f = request.files['file']
        save_file(f)
        return 'upload_file_success'


# 上传多个文件和json混合上传
@app.route('/upload_files', methods=['POST'])
def upload_files():
    if request.method == "POST":
        data = request.form.get('data')
        print(data)
        file_list = request.files.getlist('file')
        for file in file_list:
            save_file(file)
        return 'upload_files_success'


# 保存文件到本地
def save_file(file):
    # 生成随机数
    # random_num = random.randint(0, 100)
    # f.filename.rsplit('.', 1)[1] 获取文件的后缀
    # filename = datetime.now().strftime("%Y%m%d%H%M%S") + "_" + str(random_num) + "." + file.filename.rsplit('.', 1)[1]
    file_path = basedir + '/' + file.filename  # basedir 代表获取当前位置的绝对路径
    file.save(file_path)  # 把图片保存到static 中的file 文件名


if __name__ == '__main__':
    app.run()

```

#### 定时任务

```python
from flask import Flask
from flask_apscheduler import APScheduler

# 需要下载Flask_APScheduler库
app = Flask(__name__)

scheduler = APScheduler()
scheduler.init_app(app)
scheduler.start()


# 黑名单功能，一小时的定时任务
@scheduler.task('interval', id='1', seconds=1 * 60 * 60, misfire_grace_time=900)
def print_hello():
    print('Hello,World')


if __name__ == '__main__':
    app.run()

```

## WebSocket和SocketIo

+ [Websocket和Socket.io的区别及应用](https://www.jianshu.com/p/970dcfd174dc)

#### WebSocket

+ [websockets库](https://websockets.readthedocs.io/en/stable/)

```python
import asyncio
import websockets

# 需要下载websockets

# websocket 接受和发送数据
async def handler(websocket):
    while True:
        message = await websocket.recv()
        await websocket.send('消息收到啦,%s' % message)


# websocket监听
async def main():
    async with websockets.serve(handler, "0.0.0.0", 8080):
        await asyncio.Future()  # run forever

# 访问地址ws://127.0.0.1:8080
if __name__ == "__main__":
    asyncio.run(main())
```

#### SocketIo

+ [官方文档](https://socket.io/zh-CN/get-started/chat)

```python
from flask import Flask, request
from flask_socketio import SocketIO, emit, join_room, leave_room, send

app = Flask(__name__)
socketio = SocketIO(app)

# 需要下载 flask-socketio

# 自定义事件
@socketio.on("information")
def handle_event(*message):
    user_id = message[0]
    room = message[1]
    message_info = message[2]
    # 向房间号所有的用户发消息，不包括自己
    print(f'{user_id} to room:{room} send {message_info}')
    emit("information", message_info, to=room, include_self=False)


# 房间的概念，加入房间
@socketio.on('join')
def join(*data):
    user_id = data[0]
    room = data[1]
    join_room(room)
    # send为内置普通事件，客户端必须使用event='message'去接收消息
    # 向房间号所有的用户发消息，不包括自己
    print(f'{user_id} user has entered the room')
    send(f'{user_id} user has entered the room', to=room, include_self=False)


# 房间的概念，离开房间
@socketio.on('leave')
def leave(*data):
    user_id = data[0]
    room = data[1]
    leave_room(room)
    # send为内置普通事件，客户端必须使用event='message'去接收消息
    # 向房间号所有的用户发消息，不包括自己
    print(f'{user_id} user has left the room')
    send(f'{user_id} user has left the room', to=room)


if __name__ == "__main__":
    socketio.run(app, host="0.0.0.0", port=5000)

```

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