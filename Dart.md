# Dart

## 入门

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

### 内建类型

#### Number

```dart
//int和double

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

