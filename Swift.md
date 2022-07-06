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

### Dictionary（字典）

