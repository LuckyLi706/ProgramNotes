<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Swift](#swift)
  - [基础](#%E5%9F%BA%E7%A1%80)
    - [typealias（类型别名）](#typealias%E7%B1%BB%E5%9E%8B%E5%88%AB%E5%90%8D)
    - [?、！、nil](#nil)
    - [异常](#%E5%BC%82%E5%B8%B8)
    - [访问控制](#%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6)
  - [数据类型](#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [整型](#%E6%95%B4%E5%9E%8B)
    - [浮点型](#%E6%B5%AE%E7%82%B9%E5%9E%8B)
    - [字符型（字符串）](#%E5%AD%97%E7%AC%A6%E5%9E%8B%E5%AD%97%E7%AC%A6%E4%B8%B2)
    - [类型转换](#%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2)
      - [is和as](#is%E5%92%8Cas)
      - [Any和AnyObject](#any%E5%92%8Canyobject)
    - [布尔类型](#%E5%B8%83%E5%B0%94%E7%B1%BB%E5%9E%8B)
    - [元祖](#%E5%85%83%E7%A5%96)
    - [断言](#%E6%96%AD%E8%A8%80)
  - [运算符](#%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [三元运算符](#%E4%B8%89%E5%85%83%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [空运算符（??）](#%E7%A9%BA%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [区间运算符](#%E5%8C%BA%E9%97%B4%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [恒等运算符（===）](#%E6%81%92%E7%AD%89%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [位运算符](#%E4%BD%8D%E8%BF%90%E7%AE%97%E7%AC%A6)
  - [集合](#%E9%9B%86%E5%90%88)
    - [Array（数组）](#array%E6%95%B0%E7%BB%84)
    - [Set（集合）](#set%E9%9B%86%E5%90%88)
    - [Dictionary（字典）](#dictionary%E5%AD%97%E5%85%B8)
  - [控制流](#%E6%8E%A7%E5%88%B6%E6%B5%81)
    - [For..in..循环](#forin%E5%BE%AA%E7%8E%AF)
    - [While循环](#while%E5%BE%AA%E7%8E%AF)
    - [If](#if)
    - [Switch](#switch)
    - [Countinue和Break](#countinue%E5%92%8Cbreak)
    - [带标签的跳转](#%E5%B8%A6%E6%A0%87%E7%AD%BE%E7%9A%84%E8%B7%B3%E8%BD%AC)
    - [guard（提前退出）](#guard%E6%8F%90%E5%89%8D%E9%80%80%E5%87%BA)
  - [函数](#%E5%87%BD%E6%95%B0)
    - [定义和使用](#%E5%AE%9A%E4%B9%89%E5%92%8C%E4%BD%BF%E7%94%A8)
    - [参数和返回值](#%E5%8F%82%E6%95%B0%E5%92%8C%E8%BF%94%E5%9B%9E%E5%80%BC)
    - [参数标签和参数名称](#%E5%8F%82%E6%95%B0%E6%A0%87%E7%AD%BE%E5%92%8C%E5%8F%82%E6%95%B0%E5%90%8D%E7%A7%B0)
    - [函数类型](#%E5%87%BD%E6%95%B0%E7%B1%BB%E5%9E%8B)
  - [闭包](#%E9%97%AD%E5%8C%85)
  - [枚举](#%E6%9E%9A%E4%B8%BE)
  - [类](#%E7%B1%BB)
    - [类和结构体](#%E7%B1%BB%E5%92%8C%E7%BB%93%E6%9E%84%E4%BD%93)
      - [构造函数](#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
      - [析构函数](#%E6%9E%90%E6%9E%84%E5%87%BD%E6%95%B0)
    - [属性](#%E5%B1%9E%E6%80%A7)
      - [存储属性](#%E5%AD%98%E5%82%A8%E5%B1%9E%E6%80%A7)
      - [计算属性](#%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7)
      - [属性观察器](#%E5%B1%9E%E6%80%A7%E8%A7%82%E5%AF%9F%E5%99%A8)
      - [属性包装器](#%E5%B1%9E%E6%80%A7%E5%8C%85%E8%A3%85%E5%99%A8)
    - [方法](#%E6%96%B9%E6%B3%95)
    - [下标](#%E4%B8%8B%E6%A0%87)
    - [继承](#%E7%BB%A7%E6%89%BF)
    - [扩展](#%E6%89%A9%E5%B1%95)
    - [协议](#%E5%8D%8F%E8%AE%AE)
  - [并发](#%E5%B9%B6%E5%8F%91)
    - [任务和任务组](#%E4%BB%BB%E5%8A%A1%E5%92%8C%E4%BB%BB%E5%8A%A1%E7%BB%84)
    - [Actors](#actors)
  - [泛型](#%E6%B3%9B%E5%9E%8B)
  - [自动引用计数](#%E8%87%AA%E5%8A%A8%E5%BC%95%E7%94%A8%E8%AE%A1%E6%95%B0)
    - [强引用](#%E5%BC%BA%E5%BC%95%E7%94%A8)
    - [弱引用](#%E5%BC%B1%E5%BC%95%E7%94%A8)
    - [无主引用](#%E6%97%A0%E4%B8%BB%E5%BC%95%E7%94%A8)
    - [无主可选引用](#%E6%97%A0%E4%B8%BB%E5%8F%AF%E9%80%89%E5%BC%95%E7%94%A8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Swift

感觉语法和Kotlin和相似

+ [官方文档](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html)
+ [中文文档](https://swiftgg.gitbook.io/swift/swift-jiao-cheng/01_the_basics)

## 基础

所有语句都不需要加分号

```swift
//使用var和let（可以进行上下文推断出该变量类型）
var a=10  //使用var来定义一个变量
let b=100 //使用let定义一个常量

var c:String="Hello,World"  //显示申名改变量为String类型

//输出
print(c)   //使用print方法来输出常量和变量
```

### typealias（类型别名） 

```swift
//类型别名,对UInt16起个别名AudioSample
typealias AudioSample = UInt16

var maxAmplitudeFound = AudioSample.min  // maxAmplitudeFound 现在是 0
```

### ?、！、nil

```swift
/**
? 表示当前变量可以赋值nil
! 强制解析变量，忽视nil
nil 类似于null，
**/

// serverResponseCode 包含一个可选的 Int 值 404
var serverResponseCode: Int? = 404
// serverResponseCode 现在不包含值
serverResponseCode = nil

let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // 需要感叹号来获取值

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString  // 不需要感叹号
```

### 异常

```swift
//如果在调用系统某一个方法时，该方法最后有一个throws.说明该方法会抛出异常，如果一个方法会抛出异常，那么需要对该异常进行处理

//JSONSerialization.jsonObject(with: <data数据>, options: .mutableContainers)是系统层会抛出异常的方法
//方式1 try方式 手动处理
do {
 try JSONSerialization.jsonObject(with: <data数据>, options: .mutableContainers)
} catch {
   // error异常的对象（系统临时创建的）
   print(error)
}

//方式2 try?方式 系统帮助我们处理异常，如果该方法出现了异常，则该方法返回nil，如果没有异常，则返回对应的对象(最常用)
guard let anyObject = try? JSONSerialization.jsonObject(with: <data数据>, options: .mutableContainers) else{
     return
}

//方式3 try! 方式 直接告诉系统，该方法没有异常。注意：如果该方法出现了异常，那么程序会报错（崩溃）
let anyObject = try! JSONSerialization.jsonObject(with: <data数据>, options: .mutableContainers)
```

### 访问控制

```swift
/**
1. open 和 public 级别可以让实体被同一模块源文件中的所有实体访问，在模块外也可以通过导入该模块来访问源文件里的所有实体。通常情况下，你会使用 open 或 public 级别来指定框架的外部接口。open 和 public 的区别在后面会提到。
2. internal 级别让实体被同一模块源文件中的任何实体访问，但是不能被模块外的实体访问。通常情况下，如果某个接口只在应用程序或框架内部使用，就可以将其设置为 internal 级别。
3. fileprivate 限制实体只能在其定义的文件内部访问。如果功能的部分实现细节只需要在文件内使用时，可以使用 fileprivate 来将其隐藏。
4. private 限制实体只能在其定义的作用域，以及同一文件内的 extension 访问。如果功能的部分细节只需要在当前作用域内使用时，可以使用 private 来将其隐藏
**/
```

## 数据类型

### 整型

```swift
//8位无符号整型 UInt8
//32位有符号整型 Int32

/**
8位无符号整型 UInt8
32位有符号整型 Int32

无需特殊指定整数的长度
(有符号)Swift提供了⼀个特殊的整数类型Int，长度与当前平台的原⽣字长相同：
在32位平台上，Int和Int32长度相同。
在64位平台上，Int和Int64长度相同。

(无符号)Swift提供了⼀个特殊的整数类型UInt，长度与当前平台的原⽣字长相同：
在32位平台上，UInt和UInt32长度相同。
在64位平台上，UInt和UInt64长度相同。

**/

let minValue = UInt8.min // minValue为0，是UInt8类型的最⼩值
let maxValue = UInt8.max // maxValue为255，是UInt8类型的最⼤值

//尽量不要使用 UInt，除非你真的需要存储一个和当前平台原生字长相同的无符号整数。除了这种情况，最好使用 Int，即使你要存储的值已知是非负的。统一使用 Int 可以提高代码的可复用性
var number:Int=100

let decimalInteger = 17
//前缀0b表示二进制
let binaryInteger = 0b10001       // 二进制的17
//前缀0o表示八进制
let octalInteger = 0o21           // 八进制的17
//前缀0x表示十六进制
let hexadecimalInteger = 0x11     // 十六进制的17

//为了增强可读性,也可以使用下划线的方式定义
let oneMillion = 1_000_000
```

### 浮点型

```swift
/**
浮点数是有⼩数部分的数字，⽐如3.14159，0.1和-273.15。
Double表⽰64位浮点数。当你需要存储很⼤或者很⾼精度的浮点数时请使⽤此类型
Float表⽰32位浮点数。精度要求不⾼的话可以使⽤此类型

Double 精确度很高，至少有 15 位小数，而 Float 只有 6 位小数。选择哪个类型取决于你的代码需要处理的值的范围，在两种类型都匹配的情况下，将优先选择 Double
**/

//为了增强可读性,也可以使用下划线的方式定义
let justOverOneMillion = 1_000_000.000_000_1
```

### 字符型（字符串）

```swift
//1.初始化字符串
// 两个字符串均为空并等价
var emptyString = ""               // 空字符串字面量
var anotherEmptyString = String()  // 初始化方法
//检查是否为空
if emptyString.isEmpty {
    print("Nothing to see here")
}

//2.拼接字符串和字符
let string1 = "hello"
let string2 = " there"
// welcome 现在等于 "hello there"
var welcome = string1 + string2

var instruction = "look over"
instruction += string2
// instruction 现在等于 "look over there"

//3.字符串插值
let multiplier = 3
// message 是 "3 times 2.5 is 7.5"
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"

//4.访问和修改字符串
let greeting = "Guten Tag!"
greeting[greeting.startIndex]  // G（获取第一个字符）
greeting[greeting.index(before: greeting.endIndex)]  // !（endIndex实际获取的是字符串长度），这边before相当于获取字符串获取最后一个字符
greeting[greeting.index(after: greeting.startIndex)]  // u after相当于获取第一个字符的后面一个字符
let index = greeting.index(greeting.startIndex, offsetBy: 7)  
greeting[index]   // a

//5.遍历字符串
// 打印输出“G u t e n   T a g ! ”
for index in greeting.indices {
   print("\(greeting[index]) ", terminator: "")
}

//6.插入和删除
var welcome = "hello"
// welcome 变量现在等于 "hello!"
welcome.insert("!", at: welcome.endIndex)
// welcome 变量现在等于 "hello there!"
welcome.insert(contentsOf:" there", at: welcome.index(before: welcome.endIndex))
// welcome 现在等于 "hello there"
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome 现在等于 "hello"
let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)

//7.子字符串
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
// beginning 的值为 "Hello"
let beginning = greeting[..<index]
// 把结果转化为 String 以便长期存储。
let newString = String(beginning)

//8.字符串比较
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    // 打印输出“These two strings are considered equal”
    print("These two strings are considered equal")
}
```

### 类型转换

```swift
//整数之间的相互转换
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)    //输出2001

//整型和浮点型相互转换
var a = 10
var b = Double(a)  //转换为Double类型
var c = Int(b)     //转换为Int类型

/**
整型、浮点型和字符串相互转换
Double(a)  //a为数字字符串则为Optional(10.0),表示包装类型。如果不是数字字符串，返回nil
**/
var a = "10"
var c = 100.10
var d = Double(c) + Double(a)!   //加个!表示强制转换,如果String不是数字,跑出异常
```

#### is和as

```swift
//用类型检查操作符（is）来检查一个实例是否属于特定子类型。若实例属于那个子类型，类型检查操作符返回 true，否则返回 false。


//某类型的一个常量或变量可能在幕后实际上属于一个子类。当确定是这种情况时，你可以尝试用类型转换操作符（as? 或 as!）向下转到它的子类型
```

#### Any和AnyObject

```swift
/**
Any 可以表示任何类型，包括函数类型。
AnyObject 可以表示任何类类型的实例。
**/
```

### 布尔类型

```swift
//Swift有⼀个基本的布尔(Boolean)类型，叫做Bool
//Swift有两个布尔常量，true和false
```

### 元祖

*元组（tuples）*把多个值组合成一个复合值。元组内的值可以是任意类型，并不要求是相同类型

```swift
//定义方式1  http404Error 的类型是 (Int, String)，值是 (404, "Not Found")
let http404Error = (404, "Not Found")

//定义方式2
let http200Status = (statusCode: 200, description: "OK")

//取值方式1（你可以将一个元组的内容分解（decompose）成单独的常量和变量）
let (statusCode, statusMessage) = http404Error
// 输出“The status code is 404”
print("The status code is \(statusCode)")
// 输出“The status message is Not Found”
print("The status message is \(statusMessage)")

///取值方式2
// 输出“The status code is 404”
print("The status code is \(http404Error.0)")
// 输出“The status message is Not Found”
print("The status message is \(http404Error.1)")

//取值方式3（对应定义方式2）
// 输出“The status code is 200”
print("The status code is \(http200Status.statusCode)")
// 输出“The status message is OK”
print("The status message is \(http200Status.description)")
```

### 断言

```dart
//可以使用断言来进行调试
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")  // 因为 age < 0，所以断言会触发
```

## 运算符

### 三元运算符

```swift
//使用 ? :
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
```

### 空运算符（??）

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   //默认值为 nil

// userDefinedColorName 的值为空，所以 colorNameToUse 的值为 "red"
var colorNameToUse = userDefinedColorName ?? defaultColorName
```

### 区间运算符

```swift
//闭区间运算符（闭区间运算符在迭代一个区间的所有值时是非常有用的，如在 for-in 循环中：）
for index in 1...5 {
    print("\(index) * 5 = \(index * 5)")
}

//半开区间运算符（半开区间的实用性在于当你使用一个从 0 开始的列表（如数组）时，非常方便地从0数到列表的长度。）
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("第 \(i + 1) 个人叫 \(names[i])")
}

//单侧区间运算符
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian

for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```

### 恒等运算符（===）

```swift
/**
请注意，“相同”（用三个等号表示，===）与“等于”（用两个等号表示，==）的不同。“相同”表示两个类类型（class type）的常量或者变量引用同一个类实例。“等于”表示两个实例的值“相等”或“等价”，判定时要遵照设计者定义的评判标准
**/

// 打印 "tenEighty and alsoTenEighty refer to the same VideoMode instance."
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
```

### 位运算符

```swift
//1. 取反运算符（~）
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits // 等于 0b11110000

//2. 按位与运算符（&）
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits // 等于 00111100

//3. 按位或运算符（|）
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits // 等于 11111110

//4. 按位异或运算符（^）
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits // 等于 00010001

//5. 左移运算符（<<）和右移运算符（>>）
let shiftBits: UInt8 = 4 // 即二进制的 00000100
shiftBits << 1           // 00001000
shiftBits << 2           // 00010000
shiftBits << 5           // 10000000
shiftBits << 6           // 00000000
shiftBits >> 2           // 00000001
```

## 集合

### Array（数组）

```swift
//创建数组
//1、创建空数组
var someInts: [Int] = []
// 打印“someInts is of type [Int] with 0 items.”
print("someInts is of type [Int] with \(someInts.count) items.")
//2、带有默认值
var threeDoubles = Array(repeating: 0.0, count: 3)  //数量为3，都是0.0
//3、两个数组相加
var anotherThreeDoubles = Array(repeating: 2.5, count: 3) // anotherThreeDoubles 被推断为 [Double]，等价于 [2.5, 2.5, 2.5]
var sixDoubles = threeDoubles + anotherThreeDoubles    // sixDoubles 被推断为 [Double]，等价于 [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]

//访问和修改数组
shoppingList.count    //通过count来获取数组长度
shoppingList.append("Flour")   //添加数据
shoppingList += ["Baking Powder"]  // shoppingList 现在有四项了
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]  // shoppingList 现在有七项了
var firstItem = shoppingList[0]    //访问数组,第一项是“Eggs”
shoppingList.insert("Maple Syrup", at: 0)   //插入数据，指定位置
let mapleSyrup = shoppingList.remove(at: 0)  //删除数据，指定位置
let apples = shoppingList.removeLast()  //删除最后一项数据

//遍历数组
//方式一
for item in shoppingList {
    print(item)
}
//方式二
for (index, value) in shoppingList.enumerated() {
    print("Item \(String(index + 1)): \(value)")
}
```

### Set（集合）

*集合*用来存储相同类型并且没有确定顺序的值。当集合元素顺序不重要时或者希望确保每个元素只出现一次时可以使用集合而不是数组。

```swift
//创建集合
//1、创建集合
var letters = Set<Character>()
// 打印“letters is of type Set<Character> with 0 items.”
print("letters is of type Set<Character> with \(letters.count) items.")
//2、利用字面量创建集合
// favoriteGenres 被构造成含有三个初始值的集合
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]    //简化写法

//访问和修改集合
// 打印“I have 3 favorite music genres.”
print("I have \(favoriteGenres.count) favorite music genres.")
favoriteGenres.insert("Jazz")  //插入数据
favoriteGenres.remove("Rock")  //删除数据，不存在该数据会返回nil（removeAll()删除所有元素）
favoriteGenres.contains("Funk")  //是否包含某个元素

//遍历集合
//方式一
for genre in favoriteGenres {
    print("\(genre)")
}
//方式二
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}

/**
其他操作
使用 intersection(_:) 方法根据两个集合的交集创建一个新的集合。
使用 symmetricDifference(_:) 方法根据两个集合不相交的值创建一个新的集合。
使用 union(_:) 方法根据两个集合的所有值创建一个新的集合。
使用 subtracting(_:) 方法根据不在另一个集合中的值创建一个新的集合
**/
```

### Dictionary（字典）

Swift 的字典使用 `Dictionary<Key, Value>` 定义，其中 `Key` 是一种可以在字典中被用作键的类型，`Value` 是字典中对应于这些键所存储值的数据类型

```swift
//创建字典
//1、创建一个空字典
var namesOfIntegers: [Int: String] = [:]
//2、用字典字面量创建字典
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

//访问和修改字典
// 打印“The dictionary of airports contains 2 items.”（这个字典有两个数据项）
print("The dictionary of airports contains \(airports.count) items.")
airports["LHR"] = "London"    //修改或者添加数据 airports 字典现在有三个数据项
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {  //updateValue用来更新值，不存在返回nil，存在返回旧的值
    print("The old value for DUB was \(oldValue).")   
}
airports["APL"] = nil   //删除数据，赋值为 nil 来从字典里移除一个键值对
if let removedValue = airports.removeValue(forKey: "DUB") {   //removeValue用于删除值，不存在返回nil
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}

//遍历字典
//方式一
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
//方式二
// Airport code: YYZ
// Airport code: LHR
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
for airportName in airports.values {
    print("Airport name: \(airportName)")
}
//方式三
let airportCodes = [String](airports.keys)
// airportCodes 是 ["YYZ", "LHR"]

let airportNames = [String](airports.values)
// airportNames 是 ["Toronto Pearson", "London Heathrow"]
```

## 控制流

### For..in..循环

```swift
//1、遍历数组
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}

//2、遍历字典
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}

//3、使用数组范围遍历
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}

//4、如果你不需要区间序列内每一项的值，你可以使用下划线（_）替代变量名来忽略这个值：
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}

//5、使用半开区间运算符（..<）来表示一个左闭右开的区间
let minutes = 60
for tickMark in 0..<minutes {
    // 每一分钟都渲染一个刻度线（60次）
}

//6、使用stride(from:to:by:) 函数跳过不需要的标记
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // 每5分钟渲染一个刻度线（0, 5, 10, 15 ... 45, 50, 55）
}

//7、可以在闭区间使用 stride(from:through:by:) 起到上面同样作用
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // 每3小时渲染一个刻度线（3, 6, 9, 12）
}
```

### While循环

```swift
//语法
while condition {
	statements
}

//repeat...while... 类似于其他语言的do...while...
repeat {
	statements
} while condition
```

### If

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
```

### Switch

```swift
/**
Swift switch 语句中，默认语法是必须要添加 default 语句。
Swift Switch 语句中， break 是可以省略不写的，默认执行完当前 case 下的内容后，直接返回了，即使后续还有可满足的条件，可以使用Fallthrough
**/

//switch+fallthrough组合
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)   // 输出“The number 5 is a prime number, and also an integer.”


//1、基础用法
let someChar: Character = "z"
switch someChar {
case "a":
    print("this is a ")
case "b":
    print("this is b")
case "z":
    print("this is z")
default:
    print("this is else ")
}

//2、复合匹配
let someChar: Character = "Z"
switch someChar {
case "a":
    print("this is a ")
case "z","Z":
    print("this is z")   //输出this is z
default:
    print("this is else ")
}

//3、区间匹配
let count = 20
var resultValue = ""
switch count {
case 0:
    resultValue = "none"
case 1..<12:
    resultValue = "a few"
case 12..<100:
    resultValue = "dozens of"
case 100..<1000:
    resultValue = "hundreds of"
default:
    resultValue = "many"
}
print(resultValue)      //输出dozens of

//4、元组匹配
let somePoint = (1,1)

switch somePoint {
case (0, 0):
    print("point at origin")
case (_, 0):    //下划线表示可以是任意值，这里的条件是只需要满足第二个值0
    print("point at x-axis")
case (0, _):    // 下划线表示可以是任意值，这里的条件是只需要满足第一个是0
    print("point at y-axis")
case (-2...2, -2...2):      //输出point is box
    print("point is box")
default:
    print("point at other place")
}

//5、值绑定
let somePoint = (1,0)

switch somePoint {
case (0, 0):
    print("point at origin")
case (let x, 0):    // 当前条件只需要满足第二个值是0， 并且可以引用 x 来获取第一位的值，
    print("point at x-axis , distance is \(x)")  //输出point at x-axis , distance is 1
case (0, let y):     // 当前条件只需要满足第一个值是0， 并且可以引用 x 来获取第二位的值，
    print("point at y-axis, distance is \(y)")
case (-2...2, -2...2):
    print("point is box")
default:
    print("point at other place")
}

//6、where语句
let point = (1,2)
switch point {
case (0, 0):
    print("---- 0, 0")
case (let x, let y) where y == 2:
    print("second value = 2")   //second value = 2
default:
    print("other value")
}
```

### Countinue和Break

```swift
//continue
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
for character in puzzleInput {
    switch character {
    case "a", "e", "i", "o", "u", " ":
        continue
    default:
        puzzleOutput.append(character)
    }
}
print(puzzleOutput)
    // 输出“grtmndsthnklk”

//break
let numberSymbol: Character = "三"  // 简体中文里的数字 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    print("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    print("An integer value could not be found for \(numberSymbol).")
}
// 输出“The integer value of 三 is 3.”
```

### 带标签的跳转

```swift
//语法
label name: while condition {
     statements
 }

//例子
gameLoop: while square != finalSquare {
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // 骰子数刚好使玩家移动到最终的方格里，游戏结束。
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // 骰子数将会使玩家的移动超出最后的方格，那么这种移动是不合法的，玩家需要重新掷骰子
        continue gameLoop
    default:
        // 合法移动，做正常的处理
        square += diceRoll
        square += board[square]
    }
}
print("Game over!")
```

### guard（提前退出）

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

// 输出“Hello John!”
// 输出“I hope the weather is nice near you.”
greet(person: ["name": "John"])
// 输出“Hello Jane!”
// 输出“I hope the weather is nice in Cupertino.”
greet(person: ["name": "Jane", "location": "Cupertino"])
```

## 函数

### 定义和使用

```swift
//定义函数
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}

//调用
print(greet(person: "Anna"))   // 输出“Hello, Anna!”
print(greet(person: "Brian"))  // 输出“Hello, Brian!”
```

### 参数和返回值

```swift
//无参数函数
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())  // 打印“hello, world”

//多参数函数
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))   // 打印“Hello again, Tim!”

//无返回值函数
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")   // 打印“Hello, Dave!”

//多重返回值
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")   // 打印“min is -6 and max is 109”

//可选元组返回值
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")  // 打印“min is -6 and max is 109”
}

//隐式返回的函数
//下面两个函数的效果一样
func greeting(for person: String) -> String {
    "Hello, " + person + "!"
}
print(greeting(for: "Dave"))
// 打印 "Hello, Dave!"

func anotherGreeting(for person: String) -> String {
    return "Hello, " + person + "!"
}
print(anotherGreeting(for: "Dave"))
// 打印 "Hello, Dave!"
```

### 参数标签和参数名称

```swift
/**
每个函数参数都有一个参数标签（argument label）以及一个参数名称（parameter name）。
参数标签在调用函数的时候使用；调用的时候需要将函数的参数标签写在对应的参数前面。
参数名称在函数的实现中使用。默认情况下，函数参数使用参数名称来作为它们的参数标签
**/

//指定参数标签
//下面这个函数第一个使用了参数名称作为参数标签，第二个参数使用了from作为参数标签
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))    // 打印“Hello Bill!  Glad you could visit from Cupertino.”

//忽略参数标签
//使用_来声明不需要参数标签，调用的时候就不需要显示的来使用参数标签了
func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
     // 在函数体内，firstParameterName 和 secondParameterName 代表参数中的第一个和第二个参数值
}
someFunction(1, secondParameterName: 2)

//默认参数值
func someFunction(parameterWithoutDefault: Int, parameterWithDefault: Int = 12) {
    // 如果你在调用时候不传第二个参数，parameterWithDefault 会值为 12 传入到函数体中。
}
someFunction(parameterWithoutDefault: 3, parameterWithDefault: 6) // parameterWithDefault = 6
someFunction(parameterWithoutDefault: 4) // parameterWithDefault = 12

//可变参数
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)   // 返回 3.0, 是这 5 个数的平均数。
arithmeticMean(3, 8.25, 18.75)  // 返回 10.0, 是这 3 个数的平均数

//输入输出参数（使用inout）
//输入输出参数不能有默认值，而且可变参数不能用 inout 标记
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)  //变量前缀使用&符号
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")   // 打印“someInt is now 107, and anotherInt is now 3”
```

### 函数类型

```swift
//Void类型（这个函数的类型是：() -> Void，或者叫“没有参数，并返回 Void 类型的函数”。）
func printHelloWorld() {
    print("hello, world")
}

//函数作为参数类型
func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)    //addTwoInts是一个函数 打印“Result: 8”

//函数作为返回值
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}

func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}

var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)  // moveNearerToZero 现在指向 stepBackward() 函数。输出2
```

## 闭包

+ [参考代码](https://blog.csdn.net/same_life/article/details/123349858)

Swift 中的闭包与 C 和 Objective-C 中的代码块（blocks）以及其他一些编程语言中的匿名函数（Lambdas）比较相似

```swift
/**
1> 语法形式为
{
(参数列表) -> 返回值类型 in 函数体代码
}
2> 相关书写规则

1. 参数可以有多个，多个参数用,隔开
2. 参数列表的小括号可以省略
3. 返回值类型也可以省略
4. 当没有参数时in可以省略
5. in可以看作是一个分隔符，将函数体和前面的参数、返回值分隔开来
6. 单表达式闭包隐式返回可以省略 return 关键字
**/

//1、有参有返回值
//右边是严格按照了闭包表达式来写的，有参数，有括号，有返回值。
let testOne:(String, String) -> String = { (s1: String, s2: String) -> String in
    return s1 + s2
}
print(testOne("test", "one"))
//下面再看下闭包表达式的简写
//这个跟上一个是等价的，闭包表达式省去了参数的括号,返回箭头以及返回值类型.因为swift编译器能自动根据 = 去做类型判断,从而推断出相关类型
let testOne2:(String, String) -> String = { s1, s2 in
    return s1 + s2
}
print(testOne2("test", "one"))

//2、无参数无返回值
let testOne:() -> Void = {
    print("testOne")
}
print(testOne())

//3、删除 return 关键字
let testOne:(String, String) -> String = {s1, s2 in s1 + s2}
print(testOne("test", " one"))

//4、通过 $0 , $1 , $2 等名字来引用闭包的实际参数值
let testOne:(String, String) -> String = { $0 + $1 }
print(testOne("test", " one"))

//5、运算符函数
let names = ["zhangsan", "lisi", "wangwu", "zhaoliu"]
var reversedNames = names.sorted(by: > )
print(reversedNames)

/**
6、尾随闭包
1. 当函数的最后一个参数是闭包时，在函数调用时可以把闭包表达式写在()外面
2. 尾随闭包是一个书写在函数括号之后的闭包表达式
3. 如果将一个很长的闭包表达式作为函数的最后一个实参，使用尾随闭包可以增强函数的可读性
**/
//函数类型作为形式参数类型
func exec(_ mathFunction: (Int, Int) -> Int, a: Int, b: Int) {
    mathFunction(a, b)
}
//调用 exec 函数
exec({ num1, num2 in     //给定一个符合函数类型的闭包,可以看作是第一个参数的函数实现
    return num1 + num2
}, a: 3, b: 5)
//这样的函数调用形式看起来很不友好，如果闭包表达式有很多行的话，会更加不友好，不利于代码的阅读。swift提供了一个尾随闭包的概念
//尾随闭包
func exec(a: Int, b: Int, mathFunction: (Int, Int) -> Int) {
    mathFunction(a, b)
}
把闭包表达式写在了函数括号之后，增强了代码的可读性，这就是尾随闭包
//exec(a: 3, b: 5) { (num1, num2) -> Int in
//    return num1 + num2
//}
//尾随闭包可以使用简化参数名，如$0, $1(从0开始，表示第i个参数...)
exec(a: 3, b: 5) { return $0 + $1 }

//如果闭包表达式是函数的唯一实参，而且使用了尾随闭包的语法，可以将函数名后边的圆括号省略
func exec2(mathFunction:(Int, Int) -> Int) {
    print(mathFunction(1, 2))
}
//调用, 将函数名后边的圆括号省略
exec2 { (num1, num2) -> Int in
    return num1 + num2
}

/**
7、逃逸闭包
1. 如果一个闭包被作为一个函数的参数，并且在函数执行完之后才被执行，那么这种情况下的闭包就被称为逃逸闭包
2. 在参数名的:后面用@escaping来修饰说明逃逸闭包
3. 一般在涉及到异步操作时，闭包放在异步线程里，在这种情况下就会出现逃逸闭包，特别是在网络请求时会出现这种情况
**/
//逃逸闭包
func exec(fn: @escaping () -> ()) {
    //延迟 5 秒
    DispatchQueue.main.asyncAfter(deadline: DispatchTime.now() + 5) {
        //5 秒后调用闭包
        fn()
    }
    print("函数执行完毕")
}
//调用函数
exec {
    print("闭包执行完毕")
}
//这段代码会先打印"函数执行完毕"，5秒后再执行闭包打印"闭包执行完毕"


/**
8、自动闭包
1. 自动闭包是一种自动创建的用来把作为实际参数传递给函数的表达式打包的闭包
2. 这种闭包不接受任何参数（@autoclosure只支持() -> T格式的参数），当它被调用的时候，会返回被包装在其中的表达式的值
3. 这种便利语法让你能够省略闭包的花括号，用一个普通的表达式来代替显式的闭包
4. 自动闭包允许你延迟处理，因此闭包内部的代码直到你调用它的时候才会运行
**/
//添加 @autoclosure 关键字, 当闭包被调用的时候，会返回被包装在其中的表达式的值
public func assert(_ condition: @autoclosure () -> Bool, _ message: @autoclosure () -> String = String(), file: StaticString = #file, line: UInt = #line) {
    if !condition() {
        print(message())
    }
}
let number = 3
assert(number > 3, "number 不大于3")  //输出: number 不大于3

//自动闭包允许延迟处理
var person = ["zhangsan", "lisi", "wangwu", "zhailiu"]
print(person.count)    // 输出: 4
let deletePerson = { person.remove(at: 0) }
print(person.count)   //此时输出还是 4,因为没有调用闭包没有被调用,闭包里的代码没有被执行

//此时调用闭包
print(deletePerson())  //输出 "zhangsan"
print(person.count)    //输出: 3

//闭包作为实际参数传递给函数时,能获得同样的延时求值行为
//闭包作为实参, 可以显示的使用闭包
var person = ["zhangsan", "lisi", "wangwu", "zhailiu"]
func serve(customer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}
//函数接受一个返回顾客名字的显式的闭包
serve(customer: { person.remove(at: 0) })  //打印: Now serving zhangsan!

//自动闭包作为实际参数
var person = ["zhangsan", "lisi", "wangwu", "zhailiu"]
//customerProvider 参数将自动转化为一个闭包，因为该参数被标记了 @autoclosure 特性
func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: person.remove(at: 0))  //打印: Now serving zhangsan!
```

## 枚举

```swift
/**
和结构体一样，swift中的枚举也是值类型。除了定义一个或多个case成员
1. 可以定义方法，计算属性，下标
2. 可以通过mutating定义可变方法
3. 可以扩展，遵守协议，支持范型

和结构体的唯一区别就是枚举不能定义存储属性
**/

//定义（Swift 的枚举成员在被创建时不会被赋予一个默认的整型值。在下面的 CompassPoint 例子中，north，south，east 和 west 不会被隐式地赋值为 0，1，2 和 3）
enum CompassPoint {
    case north
    case south
    case east
    case west
}

//调用
var directionToHead = CompassPoint.west 

//使用switch..case..
directionToHead = .south
switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}
```

## 类

### 类和结构体

```swift
/**
类和结构体的相同点：
1. Swift 中结构体和类有很多共同点。两者都可以：
2. 定义属性用于存储值
3. 定义方法用于提供功能
4. 定义下标操作用于通过下标语法访问它们的值
5. 定义构造器用于设置初始值
6. 通过扩展以增加默认实现之外的功能
7. 遵循协议以提供某种标准功能

类的多余功能：
1. 继承允许一个类继承另一个类的特征
2. 类型转换允许在运行时检查和解释一个类实例的类型
4. 析构器允许一个类实例释放任何其所被分配的资源
5. 引用计数允许对一个类的多次引用
**/

//定义
struct Resolution {   //结构体使用struct关键字
    var width = 0
    var height = 0
}

class VideoMode {    //类使用class关键字
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}

//获取实例
let someResolution = Resolution()
let someVideoMode = VideoMode()

//属性访问
// 打印 "The width of someResolution is 0"
print("The width of someResolution is \(someResolution.width)")

//你也可以访问子属性，如 VideoMode 中 resolution 属性的 width 属性：
// 打印 "The width of someVideoMode is 0"
print("The width of someVideoMode is \(someVideoMode.resolution.width)")

//你也可以使用点语法为可变属性赋值：
someVideoMode.resolution.width = 1280
// 打印 "The width of someVideoMode is now 1280"
print("The width of someVideoMode is now \(someVideoMode.resolution.width)")

//结构体的构造器（所有结构体都有一个自动生成的成员逐一构造器，用于初始化新结构体实例中成员的属性。新实例中各个属性的初始值可以通过属性的名称传递到成员逐一构造器之中）
let vga = Resolution(width: 640, height: 480)
//类没有
```

#### 构造函数

```swift
//语法。没有显示自定义构造函数时，都会有个默认的构造函数。
init() {
    // 在此处执行构造过程
}

//例子
struct Fahrenheit {
    var temperature: Double
    init() {   //构造函数
        temperature = 32.0
    }
}
var f = Fahrenheit()
// 打印“The default temperature is 32.0° Fahrenheit”
print("The default temperature is \(f.temperature)° Fahrenheit")

//构造方法的定义和普通函数的入参形式差不多，也要定义参数标签，以及可以使用下划线来不命名参数标签
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
// boilingPointOfWater.temperatureInCelsius 是 100.0
let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// freezingPointOfWater.temperatureInCelsius 是 0.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)


//结构体的逐一构造器
struct Size {
    var width = 0.0, height = 0.0
}
//以下三种构造函数都可以使用
let twoByTwo = Size(width: 2.0, height: 2.0)  //可以直接使用
let zeroByTwo = Size(height: 2.0)
print(zeroByTwo.width, zeroByTwo.height)  // 打印 "0.0 2.0"
let zeroByZero = Size()
print(zeroByZero.width, zeroByZero.height)   // 打印 "0.0 0.0"
```

#### 析构函数

```swift
//语法
deinit {
    // 执行析构过程
}

class Player {
    var coinsInPurse: Int
    init(coins: Int) {   //构造函数
        coinsInPurse = Bank.distribute(coins: coins)
    }
    func win(coins: Int) {
        coinsInPurse += Bank.distribute(coins: coins)
    }
    deinit {    //析构函数
        Bank.receive(coins: coinsInPurse)
    }
}

var playerOne=Player()
playerOne = nil   //析构函数调用
```

### 属性

#### 存储属性

```swift
/**
存储属性:属性放在该对象内部,占用该对象内存,所以只有struct和class才有存储属性,枚举就不可以有存储属性,因为关联值和原始值都放在枚举类里面,而不是枚举实例化对象
**/

//例子（下面的例子定义了一个名为 FixedLengthRange 的结构体，该结构体用于描述整数的区间，且这个范围值在被创建后不能被修改）
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
// 该区间表示整数 0，1，2
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// 该区间现在表示整数 6，7，8
rangeOfThreeItems.firstValue = 6

//1、常量结构体实例的存储属性
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)  // 该区间表示整数 0，1，2，3
// 尽管 firstValue 是个可变属性，但这里还是会报错
rangeOfFourItems.firstValue = 6

/**
2、延时加载存储属性
延时加载存储属性是指当第一次被调用的时候才会计算其初始值的属性。在属性声明前使用 lazy 来标示一个延时加载存储属性。
必须将延时加载属性声明成变量（使用 var 关键字），因为属性的初始值可能在实例构造完成之后才会得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延时加载。
**/
class DataImporter {
    /*
    DataImporter 是一个负责将外部文件中的数据导入的类。
    这个类的初始化会消耗不少时间。
    */
    var fileName = "data.txt"
    // 这里会提供数据导入功能
}

class DataManager {
    lazy var importer = DataImporter()
    var data: [String] = []
    // 这里会提供数据管理功能
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// DataImporter 实例的 importer 属性还没有被创建  
print(manager.importer.fileName) // DataImporter 实例的 importer 属性现在被创建了
// 输出“data.txt”
```

#### 计算属性

```swift
/**
计算属性： 只用作计算,没有真正存储到实例化对象的内存中
**/
//计算属性：就是set和get方法的组合
 /*语法格式
 [修饰符] var 计算属性名：属性类型{
     get{
     }
     set(形参名){
     }
 }
 */
 
 class User  {
     var first:String = ""
     var last:String = ""
     //定义计算属性
     var fullName:String{
         //定义计算属性的getter方法，该方法的返回值由first、last两个存储属性决定
         get{
             return first + "_" + last
         }
         //定义计算属性的setter方法
         set(newValue){
             var names = newValue.componentsSeparatedByString("_")
             self.first = names[0]
             self.last = names[1]
         }
     }
     init(first:String,last:String){
         self.first = first
         self.last = last
     }
 }
 //创建一个实例
 let s = User(first: "heyang", last: "hello")
 println(s.fullName)
 s.fullName = "何杨_你好"
 println(s.fullName)
 //只读属性，则无需set部分，可以省略get和花括号
```

#### 属性观察器

```swift
/**
属性观察器：属性观察器监控和响应属性值的变化，每次属性被设置值的时候都会调用属性观察器，即使新值和当前值相同的时候也不例外。
willSet 在新的值被设置之前调用
didSet 在新的值被设置之后调用
**/

/**
1. StepCounter 类定义了一个叫 totalSteps 的 Int 类型的属性。它是一个存储属性，包含 willSet 和 didSet 观察器。
2. 当 totalSteps 被设置新值的时候，它的 willSet 和 didSet 观察器都会被调用，即使新值和当前值完全相同时也会被调用。
3. 例子中的 willSet 观察器将表示新值的参数自定义为 newTotalSteps，这个观察器只是简单的将新的值输出。didSet 观察器在 totalSteps 的值改变后被调用，它把新值和旧值进行对比，如果总步数增加了，就输出一个消息表示增加了多少步。didSet 没有为旧值提供自定义名称，所以默认值 oldValue 表示旧值的参数名。
**/
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("将 totalSteps 的值设置为 \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("增加了 \(totalSteps - oldValue) 步")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// 将 totalSteps 的值设置为 200
// 增加了 200 步
stepCounter.totalSteps = 360
// 将 totalSteps 的值设置为 360
// 增加了 160 步
stepCounter.totalSteps = 896
// 将 totalSteps 的值设置为 896
// 增加了 536 步
```

#### 属性包装器

```swift
/**
属性包装器在管理属性如何存储和定义属性的代码之间添加了一个分隔层。举例来说，如果你的属性需要线程安全性检查或者需要在数据库中存储它们的基本数据，那么必须给每个属性添加同样的逻辑代码。当使用属性包装器时，你只需在定义属性包装器时编写一次管理代码，然后应用到多个属性上来进行复用
**/

/**
定义一个属性包装器，你需要创建一个定义 wrappedValue 属性的结构体、枚举或者类。
在下面的代码中，TwelveOrLess 结构体确保它包装的值始终是小于等于 12 的数字。如果要求它存储一个更大的数字，它则会存储 12 这个数字。
**/
@propertyWrapper
struct TwelveOrLess {
    private var number = 0
    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, 12) }
    }
}

struct SmallRectangle {
    @TwelveOrLess var height: Int
    @TwelveOrLess var width: Int
}

var rectangle = SmallRectangle()
print(rectangle.height)
// 打印 "0"

rectangle.height = 10
print(rectangle.height)
// 打印 "10"

rectangle.height = 24
print(rectangle.height)
// 打印 "12"
```

### 方法

```swift
//1. 实例方法
class Counter {
    var count = 0
    func increment() {
        count += 1
    }
    func increment(by amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}

let counter = Counter()
// 初始计数值是0
counter.increment()
// 计数值现在是1
counter.increment(by: 5)
// 计数值现在是6
counter.reset()
// 计数值现在是0

//2. self属性（self相当于自身，相当于Java的this）
func increment() {
    self.count += 1
}

//3. 实例方法中修改值类型。结构体和枚举是值类型。默认情况下，值类型的属性不能在它的实例方法中被修改。可以添加mutating关键字
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// 打印“The point is now at (3.0, 4.0)”

//4. 在可变方法中给 self 赋值
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}

/**
static和class的区别
相同点
1. 可以修饰方法，static 修饰的方法叫做静态方法，class 修饰的叫做类方法。
2. 都可以修饰计算属性。
不同点
1. class 不能修饰存储属性。
2. class 修饰的计算属性可以被重写，static 修饰的不能被重写。
3. static 可以修饰存储属性，static 修饰的存储属性称为静态变量(常量)。
4. static 修饰的静态方法不能被重写，class 修饰的类方法可以被重写。
5. class 修饰的类方法被重写时，可以使用static 让方法变为静态方法。
6. class 修饰的计算属性被重写时，可以使用static 让其变为静态属性，但它的子类就不能被重写了。
7.class 只能在类中使用，但是static 可以在类，结构体，或者枚举中使用。
有一个比较特殊的是protocol。在Swift中class、struct和enum都是可以实现protocol的。那么如果我们想在protocol里定义一个类型域上的方法或者计算属性的话，应该用哪个关键字呢？答案是使用class进行定义，但是在实现时还是按照规则：在class里使用class关键字，而在struct或enum中仍然使用static，虽然在protocol中定义时使用的是class。

**/

//5. 类型方法（在方法的 func 关键字之前加上关键字 static，来指定类型方法。类还可以用关键字 class 来指定，从而允许子类重写父类该方法的实现）
class MathFormula {
//声明类型方法
    class func abs(number:Int) -> Int {
        if number < 0
        {
            return (-number)
            
        }else {
            return number
        }
    }
}

struct absTurn
{
//用static关键字声明结构体的类型方法
    static func abs(number: Int) -> Int
    {
        if number < 0
        {
            return (-number)
        } else{
            return number
        }
    }
}

let no = MathFormula.abs(number: -35)
let num = absTurn.abs(number: -5)
print("获取绝对值结果no：\(no)")           //获取绝对值结果no：86
print("获取反绝对值结果num：\(num)")       //获取反绝对值结果num：3
```

### 下标

```swift
/定义下标使用关键字subscript,可以使用[]语法
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// 打印“six times three is 18”
```

### 继承

```swift
//定义父类
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // 什么也不做——因为车辆不一定会有噪音
    }
}

//定义子类，使用冒号
class Bicycle: Vehicle {
    var hasBasket = false
    
    /**
    重写：
    在方法 makeNoise() 的重写实现中，可以通过 super.someMethod() 来调用超类版本的 makeNoise() 方法。使用override关键字。
    在属性 currentSpeed 的 getter 或 setter 的重写实现中，可以通过 super.currentSpeed 来访问超类版本的 currentSpeed 属性。
    在下标的重写实现中，可以通过 super[someIndex] 来访问超类版本中的相同下标
    **/
    override func makeNoise() {
        print("Choo Choo")
    }
}

/**
防止被重写：
1. 你可以通过把方法，属性或下标标记为 final 来防止它们被重写，只需要在声明关键字前加上 final 修饰符即可（例如：final var、final func、final class func 以及 final subscript）。
2. 任何试图对带有 final 标记的方法、属性或下标进行重写的代码，都会在编译时会报错。在类扩展中的方法，属性或下标也可以在扩展的定义里标记为 final。
3. 可以通过在关键字 class 前添加 final 修饰符（final class）来将整个类标记为 final 。这样的类是不可被继承的，试图继承这样的类会导致编译报错
**/
```

### 扩展

```swift
/**
扩展可以给一个现有的类，结构体，枚举，还有协议添加新的功能。它还拥有不需要访问被扩展类型源代码就能完成扩展的能力（即逆向建模）。
扩展和 Objective-C 的分类很相似。（与 Objective-C 分类不同的是，Swift 扩展是没有名字的。）
Swift 中的扩展可以：
1. 添加计算型实例属性和计算型类属性
2. 定义实例方法和类方法
3. 提供新的构造器
4. 定义下标
5. 定义和使用新的嵌套类型
6. 使已经存在的类型遵循（conform）一个协议
**/

//语法
extension SomeType {
  // 在这里给 SomeType 添加新的功能
}

//1. 属性扩展
//例子（对Swift 内建的 Double 类型扩展属性）
extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}
let oneInch = 25.4.mm
// 打印“One inch is 0.0254 meters”
print("One inch is \(oneInch) meters")
// 打印“Three feet is 0.914399970739201 meters”
let threeFeet = 3.ft
print("Three feet is \(threeFeet) meters")


//2. 构造器扩展
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
}
let defaultRect = Rect()
let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0),
   size: Size(width: 5.0, height: 5.0))
extension Rect {    //扩展Rect
    init(center: Point, size: Size) {   //添加构造器
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}

//3. 扩展方法
//给 Int 类型添加了一个新的实例方法叫做 repetitions
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}
3.repetitions {
    //输出Hello!Hello!Hello!
    print("Hello!")
}
//扩展可变实例方法
extension Int {
    mutating func square() {
        self = self * self
    }
}
var someInt = 3
someInt.square()  // someInt 现在是 9

//扩展下标
//对 Swift 的 Int 类型添加了一个整数类型的下标
extension Int {
    subscript(digitIndex: Int) -> Int {
        var decimalBase = 1
        for _ in 0..<digitIndex {
            decimalBase *= 10
        }
        return (self / decimalBase) % 10
    }
}
746381295[0]
// 返回 5
746381295[1]
// 返回 9
746381295[2]
// 返回 2
746381295[8]
// 返回 7
```

### 协议

```swift
//语法
protocol SomeProtocol {
	// 这里是协议的定义部分
}
//结构体实现多个协议
struct SomeStructure: FirstProtocol, AnotherProtocol {
	// 这里是结构体的定义部分
}
//子类继承父类并实现多个协议
class SomeClass: SomeSuperClass, FirstProtocol, AnotherProtocol {
	// 这里是类的定义部分
}

//1. 属性要求
protocol SomeProtocol {
	var mustBeSettable: Int { get set }  //表示可读可写
	var doesNotNeedToBeSettable: Int { get }  //表示只可读
}
//在协议中定义类型属性时，总是使用 static 关键字作为前缀。当类类型遵循协议时，除了 static 关键字，还可以使用 class 关键字来声明类型属性
protocol AnotherProtocol {
	static var someTypeProperty: Int { get set }
}

//2. 方法要求
protocol SomeProtocol {
    //在协议中定义类方法的时候，总是使用 static 关键字作为前缀。即使在类实现时，类方法要求使用 class 或 static 作为关键字前缀
	static func someTypeMethod()
}
//只有一个方法的协议
protocol RandomNumberGenerator {
    func random() -> Double
}

//3. 构造器要求
protocol SomeProtocol {
    init(someParameter: Int)
}
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {   //必须要加required关键字
        // 这里是构造器的实现部分
    }
}

protocol SomeProtocol {
    init()
}
class SomeSuperClass {
    init() {
        // 这里是构造器的实现部分
    }
}
class SomeSubClass: SomeSuperClass, SomeProtocol {
    // 因为遵循协议，需要加上 required
    // 因为继承自父类，需要加上 override
    required override init() {
        // 这里是构造器的实现部分
    }
}
```

## 并发

```swift
//定义异步函数（使用async关键字，对于那些既是异步又是 throwing 的函数，需要把 async 写在throws 关键字前边。）
func listPhotos(inGallery name: String) async -> [String] {
    let result = // 省略一些异步网络请求代码
    return result
}

/**
代码中被 await 标记的悬点表明当前这段代码可能会暂停等待异步方法或函数的返回。这也被称为让出线程（yielding the thread），因为在幕后 Swift 会挂起你这段代码在当前线程的执行，转而让其他代码在当前线程执行。因为有 await 标记的代码可以被挂起，所以在程序中只有特定的地方才能调用异步方法或函数：
1. 异步函数，方法或变量内部的代码
2. 静态函数 main() 中被打上 @main 标记的结构体、类或者枚举中的代码
3. 游离的子任务中的代码，之后会在非结构化并行中说明
**/
let photoNames = await listPhotos(inGallery: "Summer Vacation")
let sortedNames = photoNames.sorted()
let name = sortedNames[0]
let photo = await downloadPhoto(named: name)
show(photo)

//Task.sleep()方法表示暂停
func listPhotos(inGallery name: String) async -> [String] {
    await Task.sleep(2 * 1_000_000_000)  // 两秒
    return ["IMG001", "IMG99", "IMG0404"]
}

//异步序列（每次收到一个元素后对其进行处理）
import Foundation

let handle = FileHandle.standardInput
for try await line in handle.bytes.lines {
    print(line)
}

//并行
async let firstPhoto = downloadPhoto(named: photoNames[0])
async let secondPhoto = downloadPhoto(named: photoNames[1])
async let thirdPhoto = downloadPhoto(named: photoNames[2])

let photos = await [firstPhoto, secondPhoto, thirdPhoto]   //前面三个都是并行的，直到遇到当前的await才会等待
show(photos)
```

### 任务和任务组

### Actors

## 泛型

## 自动引用计数

### 强引用

### 弱引用

### 无主引用

### 无主可选引用
