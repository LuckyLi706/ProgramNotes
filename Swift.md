# Swift

感觉语法和Kotlin和相似

## 基础

所有语句都不需要加分号

### 定义变量和常量

```swift
//使用var和let（可以进行上下文推断出该变量类型）

var a=10  //定义一个变量

let b=100 //定义一个常量

var c:String="Hello,World"  //显示申名改变量为String类型
```

### 整型

```swift
//8位无符号整型 UInt8
//32位有符号整型 Int32

let minValue = UInt8.min // minValue为0，是UInt8类型的最⼩值
let maxValue = UInt8.max // maxValue为255，是UInt8类型的最⼤值

/**
无需特殊指定整数的长度
(有符号)Swift提供了⼀个特殊的整数类型Int，长度与当前平台的原⽣字长相同：
在32位平台上，Int和Int32长度相同。
在64位平台上，Int和Int64长度相同。

(无符号)Swift提供了⼀个特殊的整数类型UInt，长度与当前平台的原⽣字长相同：
在32位平台上，UInt和UInt32长度相同。
在64位平台上，UInt和UInt64长度相同。
**/
```

### 浮点型

```swift
//浮点数是有⼩数部分的数字，⽐如3.14159，0.1和-273.15。

//Double表⽰64位浮点数。当你需要存储很⼤或者很⾼精度的浮点数时请使⽤此类型。
//Float表⽰32位浮点数。精度要求不⾼的话可以使⽤此类型。
```

### 类型转换

```swift
//Int <=> Double
var a=10
var b=Double(a)  //转换为Double类型
var c=Int(b)     //转换为Int类型

/**
String <=> Int或者Double

Double(a)  //a为数字字符串则为Optional(10.0),表示包装类型。如果不是数字字符串，返回nil

**/
var a="10"
var c=100.10
var d=Double(c)+Double(a)!   //加个!表示强制转换,如何String不是数字,跑出异常
```

### typealias关键字（类型别名）

### 布尔类型

```swift
//Swift有⼀个基本的布尔(Boolean)类型，叫做Bool
//Swift有两个布尔常量，true和false
```

### 元祖

### 断言

