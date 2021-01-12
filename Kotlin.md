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

