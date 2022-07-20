<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Kotlin](#kotlin)
  - [基础](#%E5%9F%BA%E7%A1%80)
    - [入门](#%E5%85%A5%E9%97%A8)
    - [?和?.和!!.](#%E5%92%8C%E5%92%8C)
    - [访问控制](#%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6)
    - [typealias（类型别名）](#typealias%E7%B1%BB%E5%9E%8B%E5%88%AB%E5%90%8D)
  - [数据类型](#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [整型](#%E6%95%B4%E5%9E%8B)
    - [浮点型](#%E6%B5%AE%E7%82%B9%E5%9E%8B)
    - [字符类型](#%E5%AD%97%E7%AC%A6%E7%B1%BB%E5%9E%8B)
    - [布尔类型](#%E5%B8%83%E5%B0%94%E7%B1%BB%E5%9E%8B)
    - [字符串类型](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%B1%BB%E5%9E%8B)
    - [数组（Array）](#%E6%95%B0%E7%BB%84array)
    - [类型转换](#%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2)
  - [控制流](#%E6%8E%A7%E5%88%B6%E6%B5%81)
    - [If](#if)
    - [when](#when)
    - [for和while](#for%E5%92%8Cwhile)
  - [运算符](#%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [位运算符](#%E4%BD%8D%E8%BF%90%E7%AE%97%E7%AC%A6)
  - [函数](#%E5%87%BD%E6%95%B0)
    - [函数介绍和使用](#%E5%87%BD%E6%95%B0%E4%BB%8B%E7%BB%8D%E5%92%8C%E4%BD%BF%E7%94%A8)
    - [高阶函数与 lambda 表达式](#%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0%E4%B8%8E-lambda-%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [内联函数](#%E5%86%85%E8%81%94%E5%87%BD%E6%95%B0)
  - [类与对象](#%E7%B1%BB%E4%B8%8E%E5%AF%B9%E8%B1%A1)
    - [类](#%E7%B1%BB)
    - [继承](#%E7%BB%A7%E6%89%BF)
    - [抽象类](#%E6%8A%BD%E8%B1%A1%E7%B1%BB)
    - [属性和字段](#%E5%B1%9E%E6%80%A7%E5%92%8C%E5%AD%97%E6%AE%B5)
    - [接口](#%E6%8E%A5%E5%8F%A3)
    - [扩展](#%E6%89%A9%E5%B1%95)
    - [数据类](#%E6%95%B0%E6%8D%AE%E7%B1%BB)
    - [内部类和嵌套类](#%E5%86%85%E9%83%A8%E7%B1%BB%E5%92%8C%E5%B5%8C%E5%A5%97%E7%B1%BB)
  - [集合](#%E9%9B%86%E5%90%88)
    - [List](#list)
    - [Set](#set)
    - [Map](#map)
  - [协程](#%E5%8D%8F%E7%A8%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Kotlin

+ [官方中文文档](https://www.kotlincn.net/docs/reference/basic-syntax.html)

## 基础

### 入门

```kotlin
//main方法的写法（Kotlin的main函数有两种写法）
//方法1（java的改造版）
class First {
    //java的改造版
    companion object {   //相当于java的static关键字
        @JvmStatic
        fun main(arrays: Array<String>) {
            print("Hello,World")
        }
    }
}
//方法2（kotlin的写法，脱离类的包裹）
fun main() {
    print("Hello,World")
}

//基础语法
fun main(){
    //定义变量使用var和val（可以进行上下文推断出该变量类型）
    var a = 1  // 使用var来定义可变的变量
    val b = 2  // 使用val定义一个常量
    
    var c:Int = 3 //显示申明该变量类型
    
    print(c)   //打印输出
}
```

### ?和?.和!!.

```kotlin
/**
?和?.和!!.区别
**/
var str: String? = null         //?表示声明的str变量可以为null
str?.substring(2)     //?.表示如果str为null就不执行这行
str!!.substring(2)    //!!.表示如果str为null就抛出空指针异常
```

### 访问控制

```kotlin
/**
类、对象、接口、构造函数、方法、属性和它们的 setter 都可以有 可见性修饰符。 （getter 总是与属性有着相同的可见性。） 
在 Kotlin 中有这四个可见性修饰符：private、 protected、 internal 和 public。 如果没有显式指定修饰符的话，默认可见性是 public。
**/

/**
包（函数、属性和类、对象和接口可以在顶层声明，即直接在包内：）
1. 如果你不指定任何可见性修饰符，默认为 public，这意味着你的声明将随处可见；
2. 如果你声明为 private，它只会在声明它的文件内可见；
3. 如果你声明为 internal，它会在相同模块内随处可见；
4. protected 不适用于顶层声明。
**/
// 文件名：example.kt
package foo

private fun foo() { …… } // 在 example.kt 内可见
public var bar: Int = 5 // 该属性随处可见
    private set         // setter 只在 example.kt 内可见   
internal val baz = 6    // 相同模块内可见

/**
类和接口
对于类内部声明的成员：
1. private 意味着只在这个类内部（包含其所有成员）可见；
2. protected—— 和 private一样 + 在子类中可见。
3. internal —— 能见到类声明的 本模块内 的任何客户端都可见其 internal 成员；
4. public —— 能见到类声明的任何客户端都可见其 public 成员。
Kotlin 中，外部类不能访问内部类的 private 成员。
如果你覆盖一个 protected 成员并且没有显式指定其可见性，该成员还会是 protected 可见性。

构造函数：
要指定一个类的的主构造函数的可见性，使用以下语法（注意你需要添加一个显式 constructor 关键字）：
**/
open class Outer {
    private val a = 1
    protected open val b = 2
    internal val c = 3
    val d = 4  // 默认 public
    
    protected class Nested {
        public val e: Int = 5
    }
}

class Subclass : Outer() {
    // a 不可见
    // b、c、d 可见
    // Nested 和 e 可见

    override val b = 5   // “b”为 protected
}

class Unrelated(o: Outer) {
    // o.a、o.b 不可见
    // o.c 和 o.d 可见（相同模块）
    // Outer.Nested 不可见，Nested::e 也不可见
}

class C private constructor(a: Int) { …… }   //这里private声明了主构造函数不可见
```

### typealias（类型别名）

```kotlin
//类型别名为现有类型提供替代名称。 如果类型名称太长，你可以另外引入较短的名称，并使用新的名称替代原类型名。

//例如，通常缩减集合类型是很有吸引力的
typealias NodeSet = Set<Network.Node>
typealias FileTable<K> = MutableMap<K, MutableList<File>>

//为函数起一个别名
typealias MyHandler = (Int, String, Any) -> Unit
typealias Predicate<T> = (T) -> Boolean

//为内部类起个别名
class A {
    inner class Inner
}
class B {
    inner class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner
```

## 数据类型

### 整型

```kotlin
/**
四种类型：
类型  大小（比特）  最小    最大
Byte	8	-128	127
Short	16	-32768	32767
Int	   32	-2,147,483,648 (-231)	2,147,483,647 (231 - 1)
Long	64	-9,223,372,036,854,775,808 (-263)	9,223,372,036,854,775,807 (263 - 1)

无符号整型
kotlin.UByte: 无符号 8 比特整数，范围是 0 到 255
kotlin.UShort: 无符号 16 比特整数，范围是 0 到 65535
kotlin.UInt: 无符号 32 比特整数，范围是 0 到 2^32 - 1
kotlin.ULong: 无符号 64 比特整数，范围是 0 到 2^64 - 1
**/

//所有以未超出 Int 最大值的整型值初始化的变量都会推断为 Int 类型。如果初始值超过了其最大值，那么推断为 Long 类型。 如需显式指定 Long 型值，请在该值后追加 L 后缀
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1

//Kotlin不支持八进制
val decimalInteger = 17    //十进制，Long 类型用大写 L 标记: 17L
//前缀0b表示二进制
val binaryInteger = 0b10001       // 二进制的17
//前缀0x表示十六进制
val hexadecimalInteger = 0x11     // 十六进制的17

//字面值（增加可读性）
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010


//无符号整型定义
val b: UByte = 1u  // UByte，已提供预期类型
val s: UShort = 1u // UShort，已提供预期类型
val l: ULong = 1u  // ULong，已提供预期类型

val a1 = 42u // UInt：未提供预期类型，常量适于 UInt
val a2 = 0xFFFF_FFFF_FFFFu // ULong：未提供预期类型，常量不适于 UInt
val a = 1UL // ULong，即使未提供预期类型并且常量适于 UInt
```

### 浮点型

```kotlin
/**
类型	大小（比特数）	有效数字比特数	指数比特数	十进制位数
Float	32	24	8	6-7
Double	64	53	11	15-16
**/

val pi = 3.14 // Double
val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // Float，实际值为 2.7182817，指定Float类型要加f
```

### 字符类型

```kotlin
/**
字符用 Char 类型表示。它们不能直接当作数字
字符字面值用单引号括起来: '1'。 特殊字符可以用反斜杠转义。 支持这几个转义序列：\t、 \b、\n、\r、\'、\"、\\ 与 \$。 编码其他字符要用 Unicode 转义序列语法：'\uFF00'
**/

//显示转换
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // 显式转换为数字
}
```

### 布尔类型

```kotlin
/**
布尔用 Boolean 类型表示，它有两个值：true 与 false。
若需要可空引用布尔会被装箱。
内置的布尔运算有：
|| – 短路逻辑或
&& – 短路逻辑与
! - 逻辑非
**/
```

### 字符串类型

```kotlin
//字符串用 String 类型表示。字符串是不可变的。 字符串的元素——字符可以使用索引运算符访问: s[i]。 可以用 for 循环迭代字符串:
for (c in str) {
    println(c)
}

//拼接字符串
val s = "abc" + 1
println(s + "def")

//去除每行最前面的前导空格
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin("|")      //去除每行前面的|以及前面的空格

//字符串模板
val s = "abc"
println("$s.length is ${s.length}") // 输出“abc.length is 3”
```

### 数组（Array）

```kotlin
/**
1、使用arrayOf
arrayOf(1, 2, 3) 创建了 array [1, 2, 3]。 或者，库函数 arrayOfNulls() 可以用于创建一个指定大小的、所有元素都为空的数组
2、数组大小以及一个函数参数的 Array 构造函数
**/
val text = arrayOf("1", "2", 3)   //使用arrOf可以添加不同的数据
    text.forEach {
        print(it is Int)
    }

// 创建一个 Array<String> 初始化为 ["0", "1", "4", "9", "16"]
val asc = Array(5) { i -> (i * i).toString() }
asc.forEach { println(it) }

/**
Kotlin 也有无装箱开销的专门的类来表示原生类型数组: ByteArray、 ShortArray、IntArray 等等（没有StringArray）。这些类与 Array 并没有继承关系，但是它们有同样的方法属性集。它们也都有相应的工厂方法:
kotlin.UByteArray: 无符号字节数组
kotlin.UShortArray: 无符号短整型数组
kotlin.UIntArray: 无符号整型数组
kotlin.ULongArray: 无符号长整型数组
**/
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]

// 大小为 5、值为 [0, 0, 0, 0, 0] 的整型数组
val arr = IntArray(5)

// 例如：用常量初始化数组中的值
// 大小为 5、值为 [42, 42, 42, 42, 42] 的整型数组
val arr = IntArray(5) { 42 }

// 例如：使用 lambda 表达式初始化数组中的值
// 大小为 5、值为 [0, 1, 2, 3, 4] 的整型数组（值初始化为其索引值）
var arr = IntArray(5) { it * 1 }
```



### 类型转换

```kotlin
/**
1. 数字类型的转换（每个数字类型支持如下的转换）
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
**/
```

## 控制流

### If

```kotlin
/**
Kotlin中的if除了有java的功能,还有很多其他好处
**/
// 1、作为表达式
val max = if (a > b) a else b
// 2、if 的分支可以是代码块，最后的表达式作为该块的值
val max = if (a > b) {
    print("Choose a")
    a
} else {
    print("Choose b")
    b
}
```

### when

```kotlin
/**
Kotlin中的when关键字相当于Java的switch...case..
**/
//1、基本用法
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // 注意这个块
        print("x is neither 1 nor 2")
    }
}
//2、任意表达式（而不只是常量）作为分支条件
when (x) {
    parseInt(s) -> print("s encodes x")
    else -> print("s does not encode x")
}
//3、可以检测一个值在（in）或者不在（!in）一个区间或者集合中
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
//4、另一种可能性是检测一个值是（is）或者不是（!is）一个特定类型的值
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")   //智能转换后,可以直接访问该属性
    else -> false
}
//5、when 也可以用来取代 if-else if链。 如果不提供参数，所有的分支条件都是简单的布尔表达式，而当一个分支的条件为真时则执行该分支：
when {
    x.isOdd() -> print("x is odd")
    y.isEven() -> print("y is even")
    else -> print("x+y is odd.")
}
```

### for和while

```kotlin
/**
for循环
**/
//1、for 循环可以对任何提供迭代器（iterator）的对象进行遍历
for (item in collection) print(item)
//2、区间表达式
for (i in 1..3) {
    println(i)
}
for (i in 6 downTo 0 step 2) {
    println(i)
}

/**
while循环类似Java
**/

/**
Break 与 Continue 标签跳转到指定位置
在 Kotlin 中任何表达式都可以用标签（label）来标记。 标签的格式为标识符后跟 @ 符号，例如：abc@、fooBar@都是有效的标签
标签限制的 break 跳转到刚好位于该标签指定的循环后面的执行点。 continue 继续标签指定的循环的下一次迭代。
**/
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (j==5) break@loop   //当j==5时跳出整个循环
    }
}
```

## 运算符

### 位运算符

```kotlin
/**
shl(bits) – 有符号左移
shr(bits) – 有符号右移
ushr(bits) – 无符号右移
and(bits) – 位与
or(bits) – 位或
xor(bits) – 位异或
inv() – 位非
**/

val x = (1 shl 2) and 0x000FF000
```

## 函数

### 函数介绍和使用

```kotlin
//定义（fun关键字）
fun double(x: Int): Int {   
    return 2 * x
}

//用法
val result = double(2)

//默认参数
fun read(
    b: Array<Byte>, 
    off: Int = 0,    //off参数默认为0
    len: Int = b.size) {}

//如果一个默认参数在一个无默认值的参数之前，那么该默认值只能通过使用具名参数调用该函数来使用
fun foo(
    bar: Int = 0, 
    baz: Int,
) { /*……*/ }

foo(baz = 1) // 使用默认值 bar = 0

//当函数返回单个表达式时，可以省略花括号并且在 = 符号之后指定代码体即可
fun double(x: Int): Int = x * 2
fun double(x: Int) = x * 2

//可变数量的参数（Varargs）
fun <T> asList(vararg ts: T): List<T> {
    val result = ArrayList<T>()
    for (t in ts) // ts is an Array
        result.add(t)
    return result
}
val a = arrayOf(1, 2, 3)
val list = asList(-1, 0, *a, 4)   //如果我们已经有一个数组并希望将其内容传给该函数，我们使用伸展（spread）操作符（在数组前面加 *）

//函数作用域
//1. 局部函数
fun dfs(graph: Graph) {
    fun dfs(current: Vertex, visited: MutableSet<Vertex>) {
        if (!visited.add(current)) return
        for (v in current.neighbors)
            dfs(v, visited)
    }
    dfs(graph.vertices[0], HashSet())
}
//局部函数可以访问外部函数（即闭包）的局部变量，所以在上例中，visited 可以是局部变量：
fun dfs(graph: Graph) {
    val visited = HashSet<Vertex>()
    fun dfs(current: Vertex) {
        if (!visited.add(current)) return
        for (v in current.neighbors)
            dfs(v)
    }

    dfs(graph.vertices[0])
}
//2. 成员函数
class Sample {
    fun foo() { print("Foo") }
}
Sample().foo() // 创建类 Sample 实例并调用 foo
//3. 泛型函数
//函数可以有泛型参数，通过在函数名前使用尖括号指定：
fun <T> singletonList(item: T): List<T> { /*……*/ }
```

### 高阶函数与 lambda 表达式

```kotlin
//简单的例子
fun test(t: (Int, Int) -> Int): Int {   //定义一个高阶函数
    return t(4, 5)
}
//调用方式1（注意格式）
print(test { a, b ->
        a + b
    })
//调用方式2，使用lambda表达式
print(test(t = { a: Int, b: Int -> a + b }))

//另外一种实现
fun test(t: (Int, Int) -> Int): Int {
    return t(4, 5)
}
val test_high: (Int, Int) -> Int = ::add  //用这种方式来引用函数
fun add(num1: Int, num2: Int): Int = num1 + num2
//调用（只能使用这种方式）
println(test(t = test_high))

//高阶函数是将函数用作参数或返回值的函数。一个不错的示例是集合的函数式风格的 fold
fun <T, R> Collection<T>.fold(
    initial: R, 
    combine: (acc: R, nextElement: T) -> R
): R {
    var accumulator: R = initial
    for (element: T in this) {
        accumulator = combine(accumulator, element)
    }
    return accumulator
}
/**
参数 combine 具有函数类型 (R, T) -> R，因此 fold 接受一个函数作为参数， 该函数接受类型分别为 R 与 T 的两个参数并返回一个 R 类型的值。 在 for-循环内部调用该函数，然后将其返回值赋值给 accumulator。
**/

/**
函数类型
Kotlin 使用类似 (Int) -> String 的一系列函数类型来处理函数的声明： val onClick: () -> Unit = ……。

这些类型具有与函数签名相对应的特殊表示法，即它们的参数和返回值：
1. 所有函数类型都有一个圆括号括起来的参数类型列表以及一个返回类型：(A, B) -> C 表示接受类型分别为 A 与 B 两个参数并返回一个 C 类型值的函数类型。 参数类型列表可以为空，如 () -> A。Unit 返回类型不可省略。
2. 函数类型可以有一个额外的接收者类型，它在表示法中的点之前指定： 类型 A.(B) -> C 表示可以在 A 的接收者对象上以一个 B 类型参数来调用并返回一个 C 类型值的函数。 带有接收者的函数字面值通常与这些类型一起使用。
挂起函数属于特殊种类的函数类型，它的表示法中有一个 suspend 修饰符 ，例如 suspend () -> Unit 或者 suspend A.(B) -> C。
3. 函数类型表示法可以选择性地包含函数的参数名：(x: Int, y: Int) -> Point。 这些名称可用于表明参数的含义

如需将函数类型指定为可空，请使用圆括号：((Int, Int) -> Int)?。
函数类型可以使用圆括号进行接合：(Int) -> ((Int) -> Unit)
箭头表示法是右结合的，(Int) -> (Int) -> Unit 与前述示例等价，但不等于 ((Int) -> (Int)) -> Unit。
**/

/**
lambda 表达式定义
（直白的说，Lambda就是一小段可以作为参数传递的代码。）
一般向某个函数传参都只能是变量，而Lambda可以传一段代码。
kotlin的集合中也有很多类似的函数式API ，如map() filter() maxByOrNull()等
**/

//使用（集合中找长度最长的单词）
val list = listOf("Hello", "world", "I", "am", "kotlin")
val lambda = { word: String -> word.length }
val maxLengthWord = list.maxByOrNull(lambda)    //maxByOrNull传入一小段代码
println("max length word is $maxLengthWord")

//简化写法
val list = listOf("Hello", "world", "I", "am", "kotlin")
val maxLengthWord = list.maxByOrNull { it.length }	// maxByOrNull传入的就是一个简化的Lambda表达式
println("max length word is $maxLengthWord")

//简化规则
//规则1（可以不需要专门定义lambda，可以将其直接传入，如下：）
val maxLengthWord = list.maxByOrNull({ word: String -> word.length })
//规则2（kotlin中，当Lambda参数是函数的最后一个参数时，可以将Lambda表达式移到函数括号()的后面）
val maxLengthWord = list.maxByOrNull() { word: String -> word.length }
//规则3（kotlin中，如果Lambda参数是函数的唯一参数的话，可以将函数括号( )省略，如下：）
val maxLengthWord = list.maxByOrNull { word: String -> word.length }
//规则4（kotlin拥有出色的类型推导机制，因此可以省略参数类型声明，如下：）
val maxLengthWord = list.maxByOrNull { word -> word.length }
//规则5（当Lambda表达式的参数列表中只有一个参数时，可以省略声明参数名，直接用 it 关键字代替，就得到了上面的最终简化版本，如下：）
val maxLengthWord = list.maxByOrNull { it.length }
//规则6（kotlin中，需要实现某个抽象类的时候，若该抽象类只有一个抽象方法需要重写，则可以用Lambda直接传入该方法的实现代码，java 1.8以后也支持如此，如下：）
widgetBtnF2nmczuc.setOnClickListener({ p0 -> Log.d(TAG, p0.toString()) })
widgetBtnF2nmczuc.setOnClickListener { Log.d(TAG, it.toString()) }  //根据1、2、3、4、5规则再简化
```

### 内联函数

## 类与对象

### 类

```kotlin
//类（使用class关键字）
class Invoice { /*……*/ }

//构造函数
//1、主构造函数
class Person constructor(firstName: String) { /*……*/ }
//如果主构造函数没有任何注解或者可见性修饰符，可以省略这个 constructor 关键字。
class Person(firstName: String) { /*……*/ }
//主构造函数不能包含任何的代码。初始化的代码可以放到以 init 关键字作为前缀的初始化块（initializer blocks）中。
class InitOrderDemo(name: String) {
    val firstProperty = "First property: $name".also(::println)    
    init {
        println("First initializer block that prints ${name}")
    }    
    val secondProperty = "Second property: ${name.length}".also(::println)    
    init {
        println("Second initializer block that prints ${name.length}")
    }
}
//声明属性以及从主构造函数初始化属性，Kotlin 有简洁的语法（初始化过的参数可以直接使用）
class Person(val firstName: String, val lastName: String, var age: Int) { /*……*/ }
//如果构造函数有注解或可见性修饰符，这个 constructor 关键字是必需的，并且这些修饰符在它前面：
class Customer public @Inject constructor(name: String) { /*……*/ }
//2、次构造函数（类也可以声明前缀有 constructor的次构造函数：）
class Person {
    var children: MutableList<Person> = mutableListOf()
    constructor(parent: Person) {
        parent.children.add(this)
    }
}
//如果类有一个主构造函数，每个次构造函数需要委托给主构造函数， 可以直接委托或者通过别的次构造函数间接委托。委托到同一个类的另一个构造函数用 this 关键字即可：
class Person(val name: String) {
    var children: MutableList<Person> = mutableListOf()
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
//请注意，初始化块中的代码实际上会成为主构造函数的一部分。委托给主构造函数会作为次构造函数的第一条语句，因此所有初始化块与属性初始化器中的代码都会在次构造函数体之前执行。即使该类没有主构造函数，这种委托仍会隐式发生，并且仍会执行初始化块
class Constructors {
    init {
        println("Init block")
    }

    constructor(i: Int) {
        println("Constructor")
    }
}
//如果一个非抽象类没有声明任何（主或次）构造函数，它会有一个生成的不带参数的主构造函数。构造函数的可见性是 public。如果你不希望你的类有一个公有构造函数，你需要声明一个带有非默认可见性的空的主构造函数：
class DontCreateMe private constructor () { /*……*/ }

//创建类的实例（不需要new关键字）
val invoice = Invoice()
val customer = Customer("Joe Smith")
```

### 继承

```kotlin
/**
继承：
1. 在 Kotlin 中所有类都有一个共同的超类 Any，这对于没有超类型声明的类是默认超类：
2. Any 有三个方法：equals()、 hashCode() 与 toString()。因此，为所有 Kotlin 类都定义了这些方法。
3. 默认情况下，Kotlin 类是最终（final）的：它们不能被继承。 要使一个类可继承，请用 open 关键字标记它。

*/

//如果派生类有一个主构造函数，其基类可以（并且必须） 用派生类主构造函数的参数就地初始化。
open class Customer(name: String) {

}
class People(val name: String) : Customer(name) {
}
//如果派生类没有主构造函数，那么每个次构造函数必须使用 super 关键字初始化其基类型，或委托给另一个构造函数做到这一点。 注意，在这种情况下，不同的次构造函数可以调用基类型的不同的构造函数：
class MyView : View {
    constructor(ctx: Context) : super(ctx)
    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
}

//方法覆盖（override）
open class Shape {
    open fun draw() { /*……*/ }   //必须显示声明为open，允许覆盖
    fun fill() { /*……*/ }
}

class Circle() : Shape() {
    override fun draw() { /*……*/ }
}

//属性覆盖（override）
open class Shape {
    open val vertexCount: Int = 0
}

class Rectangle : Shape() {
    override val vertexCount = 4
}
//你可以在主构造函数中使用 override 关键字作为属性声明的一部分
interface Shape {
    val vertexCount: Int
}

class Rectangle(override val vertexCount: Int = 4) : Shape // 总是有 4 个顶点

class Polygon : Shape {
    override var vertexCount: Int = 0  // 以后可以设置为任何数
}

//派生类初始化顺序
//在构造派生类的新实例的过程中，第一步完成其基类的初始化（在之前只有对基类构造函数参数的求值），因此发生在派生类的初始化逻辑运行之前
open class Base(val name: String) {

    init { println("Initializing Base") }

    open val size: Int = 
        name.length.also { println("Initializing size in Base: $it") }
}

class Derived(
    name: String,
    val lastName: String,
) : Base(name.capitalize().also { println("Argument for Base: $it") }) {

    init { println("Initializing Derived") }

    override val size: Int =
        (super.size + lastName.length).also { println("Initializing size in Derived: $it") }
}

//调用超类实现（super）
open class Rectangle {
    open fun draw() { println("Drawing a rectangle") }
    val borderColor: String get() = "black"
}

class FilledRectangle : Rectangle() {
    override fun draw() {
        super.draw()
        println("Filling the rectangle")
    }

    val fillColor: String get() = super.borderColor
}
//在一个内部类中访问外部类的超类，可以通过由外部类名限定的 super 关键字来实现：super@Outer：
class FilledRectangle: Rectangle() {
    override fun draw() { 
        val filler = Filler()
        filler.drawAndFill()
    }

    inner class Filler {
        fun fill() { println("Filling") }
        fun drawAndFill() {
            super@FilledRectangle.draw() // 调用 Rectangle 的 draw() 实现
            fill()
            println("Drawn a filled rectangle with color ${super@FilledRectangle.borderColor}") // 使用 Rectangle 所实现的 borderColor 的 get()
        }
    }
}

//覆盖规则（ 为了表示采用从哪个超类型继承的实现，我们使用由尖括号中超类型名限定的 super，如 super<Base>）
open class Rectangle {
    open fun draw() { /* …… */ }
}

interface Polygon {
    fun draw() { /* …… */ } // 接口成员默认就是“open”的
}

class Square() : Rectangle(), Polygon {
    // 编译器要求覆盖 draw()：
    override fun draw() {
        super<Rectangle>.draw() // 调用 Rectangle.draw()
        super<Polygon>.draw() // 调用 Polygon.draw()
    }
}
```

### 抽象类

```kotlin
/**
类以及其中的某些成员可以声明为 abstract。 抽象成员在本类中可以不用实现。 需要注意的是，我们并不需要用 open 标注一个抽象类或者函数——因为这不言而喻。
我们可以用一个抽象成员覆盖一个非抽象的开放成员
**/
open class Polygon {
    open fun draw() {}
}

abstract class Rectangle : Polygon() {
    abstract override fun draw()
}
```

### 属性和字段

```kotlin
//1、Getters 与 Setters
//语法
var <propertyName>[: <PropertyType>] [= <property_initializer>]
    [<getter>]
    [<setter>]
//例子
var stringRepresentation: String
    get() = this.toString()
    set(value) {
        setDataFromString(value) // 解析字符串并赋值给其他属性
    }

//2、幕后字段（在类中肯定是有一个字段用于存储属性的值 , 这个字段就是幕后字段 , 每个属性都有一个默认的幕后字段）
var counter = 0 // 注意：这个初始器直接为幕后字段赋值
    set(value) {
        if (value >= 0) field = value    //这边的field就是幕后字段，就是value本身
    }

//3、编译器常量（位于顶层或者是 object 声明 或 companion object 的一个成员）
const val SUBSYSTEM_DEPRECATED: String = "This subsystem is deprecated"    //使用const定义

//4、延迟初始化属性与变量
public class MyTest {
    lateinit var subject: TestSubject    //使用lateinit关键字,延迟初始化

    @SetUp fun setup() {
        subject = TestSubject()
    }

    @Test fun test() {
        subject.method()  // 直接解引用
    }
}
```

### 接口

```kotlin
/**
Kotlin 的接口可以既包含抽象方法的声明也包含实现。与抽象类不同的是，接口无法保存状态。它可以有属性但必须声明为抽象或提供访问器实现。
**/

//1、定义
interface MyInterface {
    fun bar()
    fun foo() {
      // 可选的方法体
    }
}

//2、实现接口
class Child : MyInterface {
    override fun bar() {
        // 方法体
    }
}

/**
3、接口中的属性
你可以在接口中定义属性。在接口中声明的属性要么是抽象的，要么提供访问器的实现。在接口中声明的属性不能有幕后字段（backing field），因此接口中声明的访问器不能引用它们
**/
interface MyInterface {
    val prop: Int // 抽象的

    val propertyWithImplementation: String
        get() = "foo"

    fun foo() {
        print(prop)
    }
}

class Child : MyInterface {
    override val prop: Int = 29
}

/**
4、接口继承
一个接口可以从其他接口派生，从而既提供基类型成员的实现也声明新的函数与属性。很自然地，实现这样接口的类只需定义所缺少的实现
**/
interface Named {
    val name: String
}

interface Person : Named {
    val firstName: String
    val lastName: String
    
    override val name: String get() = "$firstName $lastName"
}

data class Employee(
    // 不必实现“name”
    override val firstName: String,
    override val lastName: String,
    val position: Position
) : Person


//5、实现多个接口处理覆盖冲突
interface A {
    fun foo() { print("A") }
    fun bar()
}

interface B {
    fun foo() { print("B") }
    fun bar() { print("bar") }
}

class C : A {
    override fun bar() { print("bar") }
}

class D : A, B {
    override fun foo() {
        super<A>.foo()
        super<B>.foo()
    }

    override fun bar() {
        super<B>.bar()
    }
}

//6、入参接口
interface Model {
    fun onSuccess()
    fun onFail()
}
val model = object : Model{     //使用这个语法来获取model接口的实例
        override fun onSuccess() {
            
        }
        override fun onFail() {
            
        }
    }

//6、函数式（SAM）接口（函数式接口可以有多个非抽象成员，但只能有一个抽象成员。）
fun interface IntPredicate {   //声明为函数接口
   fun accept(i: Int): Boolean
}

val isEven = IntPredicate { it % 2 == 0 }   //可以使用这个方式来调用

fun main() {
   println("Is 7 even? - ${isEven.accept(7)}")
}
```

### 扩展

```kotlin
//扩展函数
//声明一个扩展函数，我们需要用一个 接收者类型 也就是被扩展的类型来作为他的前缀。 下面代码为 MutableList<Int> 添加一个swap 函数
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] // “this”对应该列表
    this[index1] = this[index2]
    this[index2] = tmp
}
val list = mutableListOf(1, 2, 3)
list.swap(0, 2) // “swap()”内部的“this”会保存“list”的值

//扩展作用域
//要使用所定义包之外的一个扩展，我们需要在调用方导入它
package org.example.usage
import org.example.declarations.getLongestString

fun main() {
    val list = listOf("red", "green", "blue")
    list.getLongestString()
}
```

### 数据类

```kotlin
//定义
data class User(val name: String, val age: Int)

//无参构造函数，必须指定默认值
data class User(val name: String = "", val age: Int = 0)

//类体中声明属性（对于那些自动生成的函数，编译器只使用在主构造函数内部定义的属性。如需在生成的实现中排除一个属性，请将其声明在类体中）
data class Person(val name: String) {
    var age: Int = 0
}

//复制
val jack = User(name = "Jack", age = 1)
val olderJack = jack.copy(age = 2)

//数据类和解构声明
val jane = User("Jane", 35)
val (name, age) = jane
println("$name, $age years of age") // 输出 "Jane, 35 years of age"
```

### 内部类和嵌套类

```kotlin
//嵌套类
class Outer {
    private val bar: Int = 1
    class Nested {
        fun foo() = 2
    }
}

val demo = Outer.Nested().foo() // == 2

//内部类（inner）
class Outer {
    private val bar: Int = 1
    inner class Inner {   // 使用inner关键字，来表示内部类
        fun foo() = bar
    }
}

val demo = Outer().Inner().foo() // == 1

//匿名内部类
window.addMouseListener(object : MouseAdapter() {
    override fun mouseClicked(e: MouseEvent) { …… }
    override fun mouseEntered(e: MouseEvent) { …… }
})
val listener = ActionListener { println("clicked") }
```

## 集合

![](images/kotlin_collections.png)

### List

```kotlin
//Kotlin中的List默认实现时Java的ArrayList
//List<T>   不可写,只能读
//创建方式：listOf()

//MutableList<T> 可读可写
//创建方式：mutableListOf()

//空集合
val empty = emptyList<String>()

//list 的初始化函数
val doubled = List(3, { it * 2 })  // 如果你想操作这个集合，应使用 MutableList
println(doubled)

//具体类型构造函数（例如 ArrayList 或 LinkedList，可以使用这些类型的构造函数。 类似的构造函数对于 Set 与 Map 的各实现中均有提供）
val linkedList = LinkedList<String>(listOf("one", "two", "three"))

//复制（在特定时刻通过集合复制函数，例如toList()、toMutableList()、toSet() 等等。创建了集合的快照。 结果是创建了一个具有相同元素的新集合 如果在源集合中添加或删除元素，则不会影响副本。副本也可以独立于源集合进行更改。）
val sourceList = mutableListOf(1, 2, 3)
val copyList = sourceList.toMutableList()
val readOnlyCopyList = sourceList.toList()   //将mutableList转换为List
sourceList.add(4)
println("Copy size: ${copyList.size}")   
//readOnlyCopyList.add(4)             // 编译异常
println("Read-only copy size: ${readOnlyCopyList.size}")

//迭代器
//方式1
val numbers = listOf("one", "two", "three", "four")
val numbersIterator = numbers.iterator()
while (numbersIterator.hasNext()) {
    println(numbersIterator.next())
}
//方式2
val numbers = listOf("one", "two", "three", "four")
for (item in numbers) {
    println(item)
}
//方式3
val numbers = listOf("one", "two", "three", "four")
numbers.forEach {
    println(it)
}

/**
List迭代器
对于列表，有一个特殊的迭代器实现： ListIterator 它支持列表双向迭代：正向与反向。 反向迭代由 hasPrevious() 和 previous() 函数实现。 此外， ListIterator 通过 nextIndex() 与 previousIndex() 函数提供有关元素索引的信息
**/
val numbers = listOf("one", "two", "three", "four")
val listIterator = numbers.listIterator()
while (listIterator.hasNext()) listIterator.next()
println("Iterating backwards:")
while (listIterator.hasPrevious()) {
    print("Index: ${listIterator.previousIndex()}")
    println(", value: ${listIterator.previous()}")
}

/**
可变迭代器
为了迭代可变集合，于是有了 MutableIterator 来扩展 Iterator 使其具有元素删除函数 remove() 。因此，可以在迭代时从集合中删除元素。
**/
val numbers = mutableListOf("one", "two", "three", "four")
val mutableIterator = numbers.iterator()
while (mutableIterator.hasNext()) {
    val next: String = mutableIterator.next()
    if (next == "four") {
       mutableIterator.remove()
  }
}
println("After removal: $numbers")
```

### Set

```kotlin
/**
Kotlin中的Set默认实现是Java的LinkedHashSet
不可重复,元素顺序是插入顺序
Set<T> 不可写,只能读
创建方式：setOf()

MutableSet<T> 可读可写
创建方式：mutableSetOf()

另一种HashSet<T>,没有顺序,内存占用少
**/
```

### Map

```kotlin

```

## 协程

### 入门

```kotlin
fun main() {
    GlobalScope.launch { // 在后台启动一个新的协程并继续
        delay(1000L)   //延迟一秒
        println("World!")
    }
    println("Hello,") // 主线程中的代码会立即执行
    runBlocking {     // runBlocking表示阻塞了当前线程
        delay(2000L)  // ……我们延迟 2 秒来保证 JVM 的存活
        println("runBlocking end")
    }
}
//输出：
//Hello,
//World!
//runBlocking end


//等待任务完成
suspend fun main() {
    val job = GlobalScope.launch { // 启动一个新协程并保持对这个作业的引用
        delay(1000L)
        println("World!")
    }
    println("Hello,")
    job.join() // 等待直到子协程执行结束
}


//提取函数重构（suspend）
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch { doWorld() }
    println("Hello,")
}
// 这是你的第一个挂起函数
suspend fun doWorld() {
    delay(1000L)
    println("World!")
}

//重复任务（repeat）
import kotlinx.coroutines.*

fun main() = runBlocking {
    repeat(100_000) { // 启动大量的协程
        launch {
            delay(5000L)
            print(".")
        }
    }
}
```

### 创建协程的方式
```kotlin

/**
创建一个协程的方式有很多种，可以通过 runBlocking，launch (CoroutineScope.lauch / GlobalScope.lauch)，withContext ，async 等这些方法来都能创建协程，这些都是我们可能会在协程里用到的常见方法
**/

//1、可在全局创建协程的： launch 与 runBlocking
// launch 与 runBlocking都能在全局开启一个协程，但 lauch 是非阻塞的 而 runBlocking 是阻塞的

/**
launch:
从下面运行结果可以看出，通过CoroutineScope.launch开启一个协程，协程体里的任务时就会先挂起（suspend），让CoroutineScope.launch后面的代码继续执行，直到协程体内的方法执行完成再自动切回来所在的上下文回调结果。

CoroutineScope.launch 中我们可以看到接收了一个参数Dispatchers.Main，这是一个表示协程上下文的参数，用于指定该协程体里的代码运行在哪个线程。当指定为Dispatchers.Main时，协程体里的代码也是运行在主线程。 当指定为Dispatchers.IO，则当前协程运行在一个子线程里。

还有刚提到了挂起 suspend ， 它是Kotlin 中的一个关键字，它一般标识在一个函数的开头，用于表示该函数是个耗时操作，如上面的delay(timeMillis: Long)就是被声明为 suspend 函数。这个关键字主要作用就是为了作一个提醒，并不会因为添加了这个关键字就会该函数立即跑到一个子线程上。suspend 函数是只能在协程体内生效，在Kotlin 协程中，当遇到 suspend 函数的时候 ，该协程会自动逃离当前所在的线程执行任务，此时原来协程所在的线程就继续干自己的事，等到协程的suspend 函数执行完成后又自动切回来原来线程继续往下走。一句话说，suspend就是让协程该走就走，该回来就回来。但如果协程所在的线程已经运行结束了，协程还没执行完成就不会继续执行了 。为了避免这样的情况就需要结合 runBlocking 来暂时阻塞当前线程，保证代码的执行顺序
**/
btn.setOnClickListener {
    CoroutineScope(Dispatchers.Main).launch{
        delay(500)     //延时500ms
        Log.e("TAG","1.执行CoroutineScope.... [当前线程为：${Thread.currentThread().name}]")
    }
    Log.e("TAG","2.BtnClick.... [当前线程为：${Thread.currentThread().name}]")
/**
运行结果：
2020-03-30 10:51:32.094 :  2.BtnClick.... [当前线程为：main]
2020-03-30 10:51:32.600 :  1.执行CoroutineScope.... [当前线程为：main]
**/

/**
运行结果刚好和上面launch启动的协程例子相反，这里的Log先输出1...再输出2...， 程序会等待执行完成runBlocking内的协程体代码，再执行它后面的代码。  runBlocking里的任务如果是非常耗时的操作时，会一直阻塞当前线程，在实际开发中很少会用到runBlocking。 由于runBlocking 接收的 lambda 代表着一个 CoroutineScope，所以 runBlocking 协程体内可继续通过launch来继续创建一个协程，避免了lauch所在的线程已经运行结束而切不回来的情况。
**/
btn.setOnClickListener {
    runBlocking{
        delay(500)    //延时500ms
        Log.e("TAG","1.runBlocking.... [当前线程为：${Thread.currentThread().name}]")
    }
    Log.e("TAG","2.BtnClick.... [当前线程为：${Thread.currentThread().name}]")
}
/**
运行结果：
2020-03-30 11:23:41.516 :  1.runBlocking.... [当前线程为：main]
2020-03-30 11:23:41.517 :  2.BtnClick.... [当前线程为：main]
**/

//2、可返回结果的协程：withContext 与 async
//withContext 与 async 都可以返回耗时任务的执行结果。 一般来说，多个 withContext 任务是串行的， 且withContext 可直接返回耗时任务的结果。 多个 async 任务是并行的，async 返回的是一个Deferred<T>，需要调用其await()方法获取结果。


/**
withContext:
下面例子使用 withContext 获取耗时任务结果：定义2个耗时任务，一个2000ms后返回结果，另一个1000ms后返回结果。
从下面结果可以看出，多个withConext是串行执行，如上代码执行顺序为先执行task1再执行task2，共耗时两个任务的所需时间的总和。这是因为withConext是个 suspend 函数，当运行到 withConext 时所在的协程就会挂起，直到withConext执行完成后再执行下面的方法。所以withConext可以用在一个请求结果依赖另一个请求结果的这种情况。
**/
btn.setOnClickListener {
    CoroutineScope(Dispatchers.Main).launch {
        val time1 = System.currentTimeMillis()
 
        val task1 = withContext(Dispatchers.IO) {
            delay(2000)
            Log.e("TAG", "1.执行task1.... [当前线程为：${Thread.currentThread().name}]")
            "one"  //返回结果赋值给task1
        }
                
        val task2 = withContext(Dispatchers.IO) {
            delay(1000)
            Log.e("TAG", "2.执行task2.... [当前线程为：${Thread.currentThread().name}]")
            "two"  //返回结果赋值给task2
        }
 
        Log.e("TAG", "task1 = $task1  , task2 = $task2 , 耗时 ${System.currentTimeMillis()-time1} ms  [当前线程为：${Thread.currentThread().name}]")
    }
}
/**
运行结果：
2020-03-30 15:31:46.279 : 1.执行task1.... [当前线程为：DefaultDispatcher-worker-1]
2020-03-30 15:31:47.283 : 2.执行task2.... [当前线程为：DefaultDispatcher-worker-1]
2020-03-30 15:31:47.284 : task1 = one  , task2 = two , 耗时 3009 ms  [当前线程为：main]
**/

/**
async ... await():
如果同时处理多个耗时任务，且这几个任务都无相互依赖时，可以使用 async ...  await() 来处理，将上面的例子改为 async 来实现如下

改为用async后，运行结果耗时明显比使用withContext更短，且看到与withContext不同的是，task2比task1优先执行完成 。所以说 async 的任务都是并行执行的。但事实上有一种情况例外，我们把await()方法的调用提前到 async 的后面：
**/
btn.setOnClickListener {
    CoroutineScope(Dispatchers.Main).launch {
        val time1 = System.currentTimeMillis()
 
        val task1 = async(Dispatchers.IO) {
            delay(2000)
            Log.e("TAG", "1.执行task1.... [当前线程为：${Thread.currentThread().name}]")
            "one"  //返回结果赋值给task1
        }
 
        val task2 = async(Dispatchers.IO) {
            delay(1000)
            Log.e("TAG", "2.执行task2.... [当前线程为：${Thread.currentThread().name}]")
            "two"  //返回结果赋值给task2
        }
 
        Log.e("TAG", "task1 = ${task1.await()}  , task2 = ${task2.await()} , 耗时 ${System.currentTimeMillis() - time1} ms  [当前线程为：${Thread.currentThread().name}]")
}
/**
运行结果：
2020-03-30 16:00:20.709 : 2.执行task2.... [当前线程为：DefaultDispatcher-worker-3]
2020-03-30 16:00:21.709 : 1.执行task1.... [当前线程为：DefaultDispatcher-worker-3]
2020-03-30 16:00:21.711 : task1 = one  , task2 = two , 耗时 2037 ms  [当前线程为：main]
**/

/**
刚只是把await()的位置改了，就出现这样的结果，所以原因应该就是在await()方法身上，点进 await() 源码看一下，终于明白了是怎么一回事，原来await() 仅仅被定义为 suspend 函数，因此直接在async 后面使用 await() 就和 withContext 一样，程序运行到这里就会被挂起直到该函数执行完成才会继续执行下一个 async 。但事实上await()也不一定导致协程会被挂起，await() 只有在 async 未执行完成返回结果时，才会挂起协程。若 async 已经有结果了，await() 则直接获取其结果并赋值给变量，此时不会挂起协程。
**/
btn.setOnClickListener {
    CoroutineScope(Dispatchers.Main).launch {
        val time1 = System.currentTimeMillis()
 
        val task1 = async(Dispatchers.IO) {
            delay(2000)
            Log.e("TAG", "1.执行task1.... [当前线程为：${Thread.currentThread().name}]")
            "one"  //返回结果赋值给task1
        }.await()
 
        val task2 = async(Dispatchers.IO) {
            delay(1000)
            Log.e("TAG", "2.执行task2.... [当前线程为：${Thread.currentThread().name}]")
            "two"  //返回结果赋值给task2
        }.await()
 
        Log.e("TAG", "task1 = $task1  , task2 = $task2 , 耗时 ${System.currentTimeMillis() - time1} ms  [当前线程为：${Thread.currentThread().name}]")
    }
}
/**
运行结果：
2020-03-30 16:17:03.370 : 1.执行task1.... [当前线程为：DefaultDispatcher-worker-1]
2020-03-30 16:17:04.373 : 2.执行task2.... [当前线程为：DefaultDispatcher-worker-1]
2020-03-30 16:17:04.374 : task1 = one  , task2 = two , 耗时 3016 ms  [当前线程为：main]
**/

/**
3、anko里的一个扩展函数  doAsync
doAsync 拿出来单独解释，是因为它容易联想到协程中的 async，实际上又与 async 关系不大，因为 doAsync并没有用到协程库中的东西。粗略看了下 doAsync 的源码它的实现都是基于Java的 Future  类进行异步处理和通过Handler进行线程切换 ，从而封装的一个扩展函数方便线程切换
**/
btn.setOnClickListener {
    doAsync {
        Log.e("TAG", " doAsync...   [当前线程为：${Thread.currentThread().name}]")
        uiThread {
            Log.e("TAG", " uiThread....   [当前线程为：${Thread.currentThread().name}]")
        }
    }
}
/**
运行结果：
2020-03-30 16:58:42.268 :  doAsync...   [当前线程为：pool-1-thread-1]
2020-03-30 16:58:42.270 :  uiThread....   [当前线程为：main]
**/
```
