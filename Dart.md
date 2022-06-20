# Dart

## 入门

+ [官方文档](https://dart.cn/guides/language/language-tour)

```dart
//入口函数
void main() {
  print(12);
}
```

## 变量

未初始化的变量默认值是 `null`。即使变量是数字 类型默认值也是 null，因为在 Dart 中一切都是对象，数字类型 也不例外。

```dart
var name = 'Bob';   //自动推断类型
dynamic name = 'Bob'; //动态类型
String name = 'Bob';  //显示指定类型

//Dart中的const 和 final 都可以用来定义一个不可变的常量，但又有一些不一样的区别。使用const 定义的常量是需要在编译阶段即可确定的值，而这个值一旦确定就不能再变化，否则会报错。
const a=10; 等同于 const int a=10;  //必须在编译期确定值
final timeStamp = new DateTime.now(); //只有运行时可以获取到值，可以使用final
```

### 空安全

#### ?可空表示符

我们可以通过将`?`跟在类型的后面来表示它后面的变量或参数可接受Null

```dart
class CommonModel {
  String? firstName; //可空的成员变量
  int getNameLen(String? lastName /*可空的参数*/) {
    int firstLen = firstName?.length ?? 0;    //如果firstName为null就取0
    int lastLen = lastName?.length ?? 0;
    return firstLen + lastLen;
  }
}

//当程序启用空安全后，类的成员变量默认是不可空的，所以对于一个非空的成员变量需要指定其初始化方式
class CommonModel {
  List names=[];//定义时初始化
  final List colors;//在构造方法中初始化
  late List urls;//延时初始化
  CommonModel(this.colors);
  ...
```

#### late（延迟初始化）

```dart
late List urls;//延时初始化
  setUrls(List urls){
    this.urls=urls;
  }
  int getUrlLen(){
    return urls.length;
  }
```

### 内建类型

#### Number

```dart
//int和double，int 和 double 都是 num 的子类
//可以直接使用num类型
num x = 1; 
x += 2.5;   

//类型转换
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

#### String

```dart
//Dart 字符串是一组 UTF-16 单元序列。 字符串通过单引号或者双引号创建。
//1、内嵌表达式 ${expression}
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');

//2、使用 r 前缀，可以创建 “原始 raw” 字符串
var s = r"In a raw string, even \n isn't special.";
```

#### Boolean

```dart
//Dart 使用 bool 类型表示布尔值。 Dart 只有字面量 true and false 是布尔类型， 这两个对象都是编译时常量。
```

#### List

```dart
//Dart 推断 list 的类型为 List<int> 。 如果尝试将非整数对象添加到此 List 中， 则分析器或运行时会引发错误
var list = [1, 2, 3];
list[2] = 10; //替换某个值
int c = list[2]; //获取
list.removeAt(2); //删除某个
print(list.toString());
```

#### Set

```dart
//在 Dart 中 Set 是一个元素唯一且无需的集合
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};

//要创建一个空集，使用前面带有类型参数的 {} ，或者将 {} 赋值给 Set 类型的变量
var names = <String>{};
// Set<String> names = {}; // 这样也是可以的。
// var names = {}; // 这样会创建一个 Map ，而不是 Set 。
```

#### Map

```dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// Map 对象也可以使用 Map 构造函数创建：
var gifts = Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

## 函数

### 函数声明

```dart
//1、常规声明
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}

//2、省略类型声明
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}

//3、箭头表达式（=> expr 语法是 { return expr; } 的简写）
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

### 可选参数

```dart
//1、命名可选参数
//定义函数是，使用 {param1, param2, …} 来指定命名参数
void enableFlags({bool bold, bool hidden}) {...}
//函数调用
enableFlags(bold: true, hidden: false);


//2、位置可选参数
//将参数放到 [] 中来标记参数是可选的：
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
//函数调用
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');

//3、默认参数值
//可以使用 = 来定义可选参数的默认值。 默认值只能是编译时常量。 如果没有提供默认值，则默认值为 null
/// 设置 [bold] 和 [hidden] 标志 ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold 值为 true; hidden 值为 false.
enableFlags(bold: true);
```

## 类和对象

### final和const关键字

```dart
//final
final 用来修饰变量，只能被赋值一次，运行时赋值。也就是当程序运行到这里才会被赋值。

//const
const 只可以修饰变量，常量构造函数。修饰的变量只可以被赋值一次。const修饰的变量在整个App的生命周期内都是不可变的常量，在内存中也只会创建一次，之后的每次调用都会复用第一次创建的对象。

//const 和final的区别
取值的时机不同，const在编译时候就已经确定下来，而final修饰的变量在运行时才会确定下来。
应用范畴不同，final用来修饰变量，const不仅修饰变量，还可以修饰常量构造函数。
相同内容对象创建不同，const的list1，list2内容一样，会指向同一个对象。final修饰的list1和list2内容一样，但是会指向不同的变量。
const修饰的list不能修改内容，而final修饰的list可以修改内容。
final 不能修饰类和方法，和java的不同。
```

### identical、is和as关键字

```dart
//identical 用来比较两个对象是否一样

//is用来表示A对象是否是A的实例

//as用于类型强转
```

### runtimeType方法

```dart
//用来获取某个对象的类型
class Test{
    
}

Test test=Test();
print(test.runtimeType())
//输出Test    
```

### 构造函数

#### 默认构造函数

```dart
// 默认构造函数与 Java 类似，可以是无参构造函数和有参构造函数；但与 Java 不同的是，Dart 构造函数不允许重载，即不允许有相同名称的构造函数；
//如果不声明构造函数，则会提供默认无参构造函数；
class People {
  People() {
    print('Dart --> People()');
  }
}

//有参构造函数（可以使用语法糖）
class People {
  String name;
  int age, sex;

  /// 不可与无参构造函数同时出现
  People(name, age, {sex}) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    print('Dart --> People($name, $age, {$sex})');
  }
  
  /// 简易语法糖
  People(this.name, this.age, {this.sex});
}

//当子类继承父类时，初始化子类构造函数会优先初始化父类构造函数；继承时需要使用 super() 父类构造函数，若父类为无参构造函数时可以省略
class Student extends People {
  Student(name, age, {sex}) : super() {
    this.name = name;
    this.age = age;
    this.sex = sex;
    print('Dart --> Student($name, $age, {$sex}) extends People()');
  }
}
People people = People();
print('<---------------->');
Student student = Student('阿策小和尚', 100, sex: 0);
```

#### 命名构造函数

```dart
//使用命名构造函数可以为实现多个构造函数或提供更清晰的构造函数；同时子类需要实现 super() 构造函数类型完全取决于父类构造函数类型；其中命名构造函数是不允许被继承的，若子类需要实现与父类同名的命名构造函数，则需要调用父类的同名的命名构造函数；
People.fromMap(map) {
  this.name = map['name'];
  this.age = map['age'];
  this.sex = map['sex'];
  print('Dart --> People.fromMap($map) --> $name, $age, $sex');
}

Student.fromMap(map) : super.fromMap(map) {
  this.name = map['name'];
  this.age = map['age'];
  this.sex = map['sex'];
  print('Dart --> Student.fromMap($map) extends People() --> $name,$age,$sex');
}

Map map = {'name': '阿策小和尚', 'age': 100, 'sex': 0};
People people = People.fromMap(map);
print('<---------------->');
Student student = Student.fromMap(map);
```

#### 常量构造函数

```dart
/**
1.其中所有实例变量都是 final 类型的，类中不允许有普通变量类型，因此其变量在构造函数完成之后不允许变更；
2.变量中不允许有初始值；
3.常量构造函数必须用 const 关键词修饰；
4.常量构造函数不允许有函数体；
5.实例化时需要加 const 否则实例化的对象仍然可以修改变量值；
**/
class People {
  final String name ;
  final int age ;
  final int sex;
  const People(this.name, this.age, {this.sex});
}

class Student extends People {
  Student(name, age, {sex}) : super(name, age, sex: sex){
    print('Dart --> Student($name, $age, {$sex}) extends People() --> $name, $age, $sex');
  }
}

const People people = People('阿策小和尚', 100, sex: 0);
print('People.name=${people.name}, age=${people.age}, sex=${people.sex}');
print('<---------------->');
Student student = Student('阿策小和尚', 100, sex: 0);
print('Student.name=${student.name}, age=${student.age}, sex=${student.sex}');
```

#### 工厂构造函数

```dart
/**
工厂构造函数不需要每次构建新的实例，且不会自动生成实例,而是通过代码来决定返回的实例对象；工厂构造函数类似于 static 静态成员，无法访问 this 指针；一般需要依赖其他类型构造函数；工厂构造函数还可以实现单例；
**/

class People {
  String name;
  int age, sex;
  static People _cache;

  People() {
    print('Dart --> People()');
  }

  People.fromMap(map) {
    this.name = map['name'];
    this.age = map['age'];
    this.sex = map['sex'];
    print('Dart --> People.fromMap($map) --> $name, $age, $sex');
  }

  factory People.map(map) {
    if (People._cache == null) {
      People._cache = new People.fromMap(map);
      print('Dart --> People.map($map) --> ${map['name']}, ${map['age']}, ${map['sex']} --> People._cache == null');
    }
    print('Dart --> People.map($map) --> ${map['name']}, ${map['age']}, ${map['sex']}');
    return People._cache;
  }

  factory People.fromJson(json) => People();
}

Map map = {'name': '阿策小和尚', 'age': 100, 'sex': 0};
People people = People.map(map);
print('People.name=${people.name}, age=${people.age}, sex=${people.sex}, hashCode=${people.hashCode}');
print('<---------------->');
People people2 = People.map(map);
print('People2.name=${people2.name}, age=${people2.age}, sex=${people2.sex}, hashCode=${people2.hashCode}');
print('<---------------->');
People people3 = People.fromMap(map);
print('People3.name=${people3.name}, age=${people3.age}, sex=${people3.sex}, hashCode=${people3.hashCode}');
print('<---------------->');
People people4 = People.fromJson(map);
print('People4.name=${people4.name}, age=${people4.age}, sex=${people4.sex}, hashCode=${people4.hashCode}');
```

#### 传递性和单例

```dart
//若在声明构造函数时，多个函数之间有类似的逻辑关联，为了减少代码冗余，可以通过函数传递来精简代码；小菜创建了一个 People.fromAdd() 构造函数，对于相同地方的 People 可以通过 People.fromBJ() 来传递到 People.fromAdd() 来实现；
People.fromAdd(this.name, this.address);
People.fromBJ(name) : this.fromAdd(name, '北京');

People people6 = People.fromAdd('阿策小和尚', '北京');
print('People6.name=${people6.name}, address=${people6.address}, hashCode=${people6.hashCode}');
People people7 = People.fromBJ('阿策小和尚');
print('People7.name=${people7.name}, address=${people7.address}, hashCode=${people7.hashCode}');

//使用工厂模式实现单例
class Singleton {
  static final Singleton _singleton = Singleton._internal();

  factory Singleton() => _singleton;

  Singleton._internal();    //创建私有构造函数，外部不可访问。
}

//不使用工厂模式实现单例
class Singleton {
  static final Singleton _singleton = Singleton._();

  //factory Singleton() => _singleton;
  static Singleton getInstance(){
    return _singleton;
  }

  Singleton._();
}
```

### 抽象类（extends）

### 接口（implements）

### 扩展方法（extension）

### 混入类（mixin ）

## 泛型



## 异步 

### Future

```dart
//1. Future.then
//使用 Future.delayed 模拟一个耗时操作，2秒后返回字符串“Hello Dart”，然后在then中接收到异步返回值，并打印出来：
Future.delayed(new Duration(seconds: 2), () {
      return "Hello Dart";
    }).then((value) => print(value));  //打印Hello Dart

//2. Future.catchError
//如果异步任务发生错误，我们可以在catchError中捕获错误：
Future.delayed(new Duration(seconds: 2), () {
      throw AssertionError('Error');
    }).then((value) {
      print('success');
    }).catchError((e) {
      print(e);
    });
//或者直接使用then方法的可选参数onError来捕获
Future.delayed(new Duration(seconds: 2), () {
//      return "Hello Dart";
      throw AssertionError('Error');
    }).then((value) {
      print('success');
    },onError: (e){
      print(e);
    });

//3. Future.whenComplete
//当请求结束后处理一些操作（无论请求成功还是失败，比如取消loading等操作），那么使用whenComplete回调：
Future.delayed(new Duration(seconds: 2), () {
//      return "Hello Dart";
      throw AssertionError('Error');
    }).then((value) {
      //success
      print('success');
    }).catchError((e) {
      //error
      print(e);
    }).whenComplete(() {
      print('whenComplete');  //一定会执行
    });

//4. Future.wait
//使用Future.wait 是一个界面同时发起多个请求时，需要这几个请求都获取数据成功再处理页面UI展示时使用。比如两个网络请求，这俩请求都返回成功后才执行 then，只要有一个返回失败，就会走error回调。
Future.wait([
      //2s后返回
      Future.delayed(new Duration(seconds: 2), () {
        return 'Hello';
      }),

      //4s后返回
      Future.delayed(new Duration(seconds: 4), () {
        return 'Dart';
      })
    ]).then((value) {
      //success
      print(value[0] + value[1]);
    }).catchError((e) {
      //error
      print(e);
    });
```

### await和async

```dart
//1. 没有耗时操作的Future方法
void main() async{
  print(DateTime.now().millisecondsSinceEpoch);
  await b();
  print(DateTime.now().millisecondsSinceEpoch);
}

Future b() async{
  Future.delayed(Duration(seconds: 5));
  print('bbb');
  return null;
}
/**
执行结果：
1624498836677
bbb
1624498836687
**/

//2. 含有耗时操作的Future方法
void main() async{
  print(DateTime.now().millisecondsSinceEpoch);
  await b();
  print(DateTime.now().millisecondsSinceEpoch);
}

Future b() async{
  await Future.delayed(Duration(seconds: 5));
  print('bbb');
  return null;
}
/**
执行结果：
1624498896578
bbb
1624498901599
等待b方法执行完5s后再打印。
**/

//3. 含有耗时操作不等待
void main() async{
  print(DateTime.now().millisecondsSinceEpoch);
  b();
  print(DateTime.now().millisecondsSinceEpoch);
}

Future b() async{
  await Future.delayed(Duration(seconds: 5));
  print('bbb');
  return null;
}
/**
1624498979805
1624498979810
bbb
方法b中有耗时操作，但是main方法中没有等待b执行完成。
**/
```

## 网络

### Http

```dart
//使用HttpClient来发起请求，正常为接下来的五步

//1、创建HttpClient
HttpClient httpClient = HttpClient();
/**
2、打开Http连接，设置请求头

这一步可以使用任意Http Method，如httpClient.post(...)、httpClient.delete(...)等。如果包含Query参数，可以在构建uri时添加，如：
Uri uri = Uri(scheme: "https", host: "flutterchina.club", queryParameters: {
    "xx":"xx",
    "yy":"dd"
  });

通过HttpClientRequest可以设置请求header，如：
request.headers.add("user-agent", "test");

如果是post或put等可以携带请求体方法，可以通过HttpClientRequest对象发送request body，如：
String payload="...";
request.add(utf8.encode(payload)); 
//request.addStream(_inputStream); //可以直接添加输入流
**/
HttpClientRequest request = await httpClient.getUrl(uri);

//3、等待连接服务器（这一步完成后，请求信息就已经发送给服务器了，返回一个HttpClientResponse对象，它包含响应头（header）和响应流(响应体的Stream)，接下来就可以通过读取响应流来获取响应内容）
HttpClientResponse response = await request.close();

//4、读取响应内容（我们通过读取响应流来获取服务器返回的数据，在读取时我们可以设置编码格式，这里是utf8。）
String responseBody = await response.transform(utf8.decoder).join();

//5、请求结束，关闭HttpClient
httpClient.close();
```

#### HttpClient配置

```dart
/**
常用配置
有些属性只是为了更方便的设置请求头，对于这些属性，你完全可以通过HttpClientRequest直接设置header，不同的是通过HttpClient设置的对整个httpClient都生效，而通过HttpClientRequest设置的只对当前请求生效。
**/
idleTimeout	   //对应请求头中的keep-alive字段值，为了避免频繁建立连接，httpClient在请求结束后会保持连接一段时间，超过这个阈值后才会关闭连接。
connectionTimeout	//和服务器建立连接的超时，如果超过这个值则会抛出SocketException异常。
maxConnectionsPerHost	//同一个host，同时允许建立连接的最大数量。
autoUncompress	//对应请求头中的Content-Encoding，如果设置为true，则请求头中Content-Encoding的值为当前HttpClient支持的压缩算法列表，目前只有"gzip"
userAgent	//对应请求头中的User-Agent字段。
```

#### HTTP请求认证

#### 代理

#### 证书认证

### WebSocket

```dart
/**
WebSocket分为4个步骤
1.连接到WebSocket服务器。
2.监听来自服务器的消息。
3.将数据发送到服务器。
4.关闭WebSocket连接。
**/

/**
1.连接到WebSocket服务器。
**/
final channel = IOWebSocketChannel.connect('ws://echo.websocket.org');

/**
2.监听来自服务器的消息。
WebSocketChannel提供了一个来自服务器的消息Stream 。该Stream类是dart:async包中的一个基础类。它提供了一种方法来监听来自数据源的异步事件。与Future返回单个异步响应不同，Stream类可以随着时间推移传递很多事件。该StreamBuilder (opens new window)组件将连接到一个Stream， 并在每次收到消息时通知Flutter重新构建界面。
当服务器传输的数据是指定为二进制时，StreamBuilder的snapshot.data的类型就是List<int>，是文本时，则为String
**/
StreamBuilder(
              stream: channel.stream,
              builder: (context, snapshot) {
                //网络不通会走到这
                if (snapshot.hasError) {
                  _text = "网络不通...";
                } else if (snapshot.hasData) {
                  _text = "echo: "+snapshot.data;
                }
                return Padding(
                  padding: const EdgeInsets.symmetric(vertical: 24.0),
                  child: Text(_text),
                );
              },
            )
    
/**
3.将数据发送到服务器。
为了将数据发送到服务器，我们会add消息给WebSocketChannel提供的sink。
WebSocketChannel提供了一个StreamSink (opens new window)，它将消息发给服务器。
StreamSink类提供了给数据源同步或异步添加事件的一般方法。
**/
channel.sink.add('Hello!');

/**
4.关闭WebSocket连接。
在我们使用WebSocket后，要关闭连接：
**/
channel.sink.close();

//完整例子
import 'package:flutter/material.dart';
import 'package:web_socket_channel/io.dart';

class WebSocketRoute extends StatefulWidget {
  @override
  _WebSocketRouteState createState() => _WebSocketRouteState();
}

class _WebSocketRouteState extends State<WebSocketRoute> {
  TextEditingController _controller = TextEditingController();
  IOWebSocketChannel channel;
  String _text = "";


  @override
  void initState() {
    //创建websocket连接
    channel = IOWebSocketChannel.connect('ws://echo.websocket.org');
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("WebSocket(内容回显)"),
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            Form(
              child: TextFormField(
                controller: _controller,
                decoration: InputDecoration(labelText: 'Send a message'),
              ),
            ),
            StreamBuilder(
              stream: channel.stream,
              builder: (context, snapshot) {
                //网络不通会走到这
                if (snapshot.hasError) {
                  _text = "网络不通...";
                } else if (snapshot.hasData) {
                  _text = "echo: "+snapshot.data;
                }
                return Padding(
                  padding: const EdgeInsets.symmetric(vertical: 24.0),
                  child: Text(_text),
                );
              },
            )
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _sendMessage,
        tooltip: 'Send message',
        child: Icon(Icons.send),
      ),
    );
  }

  void _sendMessage() {
    if (_controller.text.isNotEmpty) {
      channel.sink.add(_controller.text);
    }
  }

  @override
  void dispose() {
    channel.sink.close();
    super.dispose();
  }
}
```

### Socket

```dart
//使用Socket来模拟器http请求
class SocketRoute extends StatelessWidget {
  const SocketRoute({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: _request(),
      builder: (context, snapShot) {
        return Text(snapShot.data.toString());
      },
    );
  }

  _request() async {
    //建立连接
    var socket = await Socket.connect("baidu.com", 80);
    //根据http协议，发起 Get请求头
    socket.writeln("GET / HTTP/1.1");
    socket.writeln("Host:baidu.com");
    socket.writeln("Connection:close");
    socket.writeln();
    await socket.flush(); //发送
    //读取返回内容，按照utf8解码为字符串
    String _response = await utf8.decoder.bind(socket).join();
    await socket.close();
    return _response;
  }
}
```

