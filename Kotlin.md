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

### 控制流

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



## 集合

![](images/kotlin_collections.png)

### List

```kotlin
/**
Kotlin中的List默认实现时Java的ArrayList
可重复
List<T> 不可写,只能读
创建方式：listOf()

MutableList<T> 可读可写
创建方式：mutableListOf()
**/
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

