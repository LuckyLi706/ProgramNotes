# Kotlin

## 基础语法

### main函数

```kotlin
//Kotlin的main函数有两种写法
class First {
    //java的改造版
    companion object {   //相当于java的static关键字
        @JvmStatic
        fun main(arrays: Array<String>) {
            print("Hello,World")
        }
    }
}

//kotlin的写法，脱离类的包裹
fun main() {
    print("Hello,World")
}
```

### 变量

```kotlin
/**
Kotlin定义变量使用val和var关键字
val表示只读变量
var表示可重新赋值变量

存在Byte、Short、Long、Int、Float、Double、Char
数组采用ByteArray、 ShortArray、IntArray等等表示
字符串采用String
**/
val a: Int = 1  // 立即赋值，显示的表示变量a为int类型
val b = 2   // 自动推断出 `Int` 类型

var x = 5 // 自动推断出 `Int` 类型
x += 1

/**
字符串模板
格式${填写变量名或者调用方法都可以}
**/
var a = 1
// 模板中的简单名称：
val s1 = "a is $a" 

a = 2
// 模板中的任意表达式：
val s2 = "${s1.replace("is", "was")}, but now is $a"

/**
?和?.和!!.区别
**/
var str: String? = null         //?表示声明的str变量可以为null
str?.substring(2)     //?.表示如果str为null就不执行这行
str!!.substring(2)    //!!.表示如果str为null就抛出空指针异常
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

## 类与对象

### 类

```kotlin
/**
 *  Kotlin中默认所有类都是final
 *  open关键字写在类前面表示该类可以被继承，写在方法前面表示该方法可以被重写
 *
 *  主构造函数写在类名后面,使用constructor关键字,如果没有修饰符号或者注解可以省略constructor,(public constructor或者@inject constructor不可省略)
 *  主构造函数的参数可以直接用val或者var表示,直接作为构造变量来使用
 *  init{}可以作为主构造函数的初始化
 *
 *  如果类有一个主构造函数，每个次构造函数需要委托给主构造函数， 可以直接委托或者通过别的次构造函数间接委托。委托到同一个类的另一个构造函数用 this 关键字即可
 *
 *  Kotlin中的继承使用：
 *  重新方法使用在方法前面加上override关键字
 *  调用父类的方法使用super
 *
 *  实例化对象，无new关键字
 *  val people=People()
 */
open class People constructor(name: String) {

    var name: String? = name

    init {
        this.name = name
    }

    //次构造函数
    constructor(c: String, b: String) : this(c) {
        print("$c,$b")
    }

    open fun test() {
        print(name)
    }
}

//继承使用:
class Student(name: String) : People(name) {

    override fun test() {
        super.test()
        println(name)
    }

    constructor(a: String, b: String) : this(a) {

    }
}

class Worker : People {

    constructor(name: String) : super(name)
    constructor(c: String, b: String) : super(c, b)
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

