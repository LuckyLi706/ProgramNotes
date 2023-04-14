# Groovy

## 基础

### 简介

- 介绍

   1. 是一种基于JVM的敏捷开发语言
   2. 结合了Python、Ruby、Smalltalk的许多强大的特性
   3. 可以与Java完美结合，而且可以使用Java所有的库

- 特性

    1. 语法上支持动态类型，闭包等新一代特性
    2. 无缝基础所有已经存在的java类库
    3. 既支持面向对象又面向过程编程

- 优势

    1. 一种更加敏捷的编程语言
    2. 入门很容易，功能很强大
    3. 既可以作为编程语言，也可以作为脚本语言

- 可以不需要main方法，像脚本语言一样直接运行
- 不需要使用分号结尾
- 打印可以使用println或者println()

```groovy
//以下两种方式都可以，可以省略括号
println "Hello,World"
println("Hello,World")
```

### 安装环境

需要配置Java环境

+ [Groovy下载地址](http://www.groovy-lang.org/download.html)

+ groovyConsole

  groovyConsole是一个用Groovy写的图形化的GUI，非常简洁好用。


```
//mac可以使用brew安装
brew install groovy
```

### 数据类型

#### 变量定义方式

1. 强类型定义（和java一样，需要强制声明变量的类型）
2. 弱类型定义（使用**def关键字**来定义，不需要指定类型，可以重新赋值给其他类型的值）

```groovy
int a_1=12  //强类型定义
def b_1=12  //弱类型定义
b_1="12"    //重新赋值
```

#### 基本数据类型

+ 基本类型和对象类型和java一样，唯一不同的是基本类型都是包装类型

```groovy
/**
以下是基本数据类型
byte -这是用来表示字节值。例如2。
short -这是用来表示一个短整型。例如10。
int -这是用来表示整数。例如1234。
long -这是用来表示一个长整型。例如10000090。
float -这是用来表示32位浮点数。例如12.34。
double -这是用来表示64位浮点数，这些数字是有时可能需要的更长的十进制数表示。例如12.3456565。
char -这定义了单个字符文字。例如“A”。
Boolean -这表示一个布尔值，可以是true或false。
**/

//例子:
int a=12
println(a.class)
double b=12
println(b.class)

/*
输出结果
class java.lang.Integer
class java.lang.Double
* */
```

#### 字符串（String和GString）

```groovy
//groovy 有两种字符串 String和GString
//只有双引号或者三个双引号的字符串才能成为GString，可以使用插值表达式。

//1.单引号字符串
def x = "123"
def str = 'abc' //不可变字符串,不支持占位插值符$
def str1 = 'abc${x}' //无法解析${x} 结果为abc${x}

//2.双引号字符串
def x = "123"
def str = "abc${x}" //可变字符串，支持占位插值符$ 结果为abc123，{}可以省略

//3.三个单引号字符串
def x = "123"
def str = '''abc${x}''' //可以多行输入,不支持占位插值符$,结果为abc${x}
def str1 = '''
hello
world
'''
//结果为
hello
world

//4.三个双引号字符串
def x = "123"
def str = """abc $x""" //可以多行输入,支持占位插值符$,结果为abc 123

//基本用法
def a = "Hello"
def b = "World"
def c = a + b  //通过加号将两个字符串相加
println c      //输出HelloWorld
println c[4]   //输出字符串的第四个字符，输出o
println c[2, 5] //输出字符串的第二个和第五个字符，输出lW
println c[2..6] //输出字符串从第二个到第六个字符串，输出lloWo
println c * 2   //使用*运算符来实现字符串的重复，输出HelloWorldHelloWorld
println c.length() //输出字符串的长度，输出10

//其他方法
/**
center()
返回一个新的长度为numberOfChars的字符串，该字符串由左侧和右侧用空格字符填充的收件人组成。
compareToIgnoreCase()
按字母顺序比较两个字符串，忽略大小写差异。
concat()
将指定的String连接到此String的结尾。
eachMatch()
处理每个正则表达式组（参见下一节）匹配的给定String的子字符串。
endsWith()
测试此字符串是否以指定的后缀结尾。
equalsIgnoreCase()
将此字符串与另一个字符串进行比较，忽略大小写注意事项。
getAt()
它在索引位置返回字符串值
indexOf()
返回此字符串中指定子字符串第一次出现的索引。
matches()
它输出字符串是否匹配给定的正则表达式。
minus()
删除字符串的值部分。
next()
此方法由++运算符为String类调用。它增加给定字符串中的最后一个字符。
padLeft（）
填充字符串，并在左边附加空格。
padRight()
填充字符串，并在右边附加空格。
plus()
追加字符串
previous()
此方法由CharSequence的 - 运算符调用。
replaceAll（）
通过对该文本的关闭结果替换捕获的组的所有出现。
reverse()
创建一个与此String相反的新字符串。
split()
将此String拆分为给定正则表达式的匹配项。
subString()
返回一个新的String，它是此String的子字符串。
toUpperCase()
将此字符串中的所有字符转换为大写。
toLowerCase()
将此字符串中的所有字符转换为小写。
**/
```

#### 列表（List）

```groovy
//列表数据结构
def list=[1,2,3,4]
println list.class     //输出class java.util.ArrayList
println list.size()    //输出4

//定义数组
//第一种方式,使用as关键字
def array=[1,2,3,4] as int[]
//第二种方式，使用强类型定义
int[] array2=[1,2,34]
println array.class   //输出class [I
```

#### 范围（Range）

```groovy
//范围数据结构(对象是Range，是List的子类)
def range=1..10  //定义1-10范围的数据
println range[0]  //输出1
println range.contains(10) //输出true
println range.from  //输出1
println range.to   //输出10
//遍历
range.each {
    print it   //输出12345678910
}
println range.class   //输出groovy.lang.IntRange
```

#### 映射（Map）

```groovy
//映射数据结构（相当于Java的Map）
//可以添加任意元素
//key默认为单引号不可变字符串

def colors=[rea:"123",ble:"222"]
//获取值第一种方式
println colors["rea"]   //输出123
//获取值第二种方式
println colors.rea    //输出123
//添加元素
colors.yello="111"
//添加多个元素
colors.complex=[a:1,b:2]
println colors   //输出[rea:123, ble:222, yello:111, complex:[a:1, b:2]]
println colors.getClass()   //输出class java.util.LinkedHashMap
```

### 运算符、条件语句和循环

#### 循环

##### for循环

```groovy
def x = ['2', '3']
//for in
for (y in x) {  //可以不显示声明类型
    println y
}
/**
输出
2
3
**/


//for : 
for (String y : x) { //需要显示声明类型
    println y
}
/**
输出
2
3
**/
```

##### each循环

```groovy
def x = ['2', '3']

x.each {  //集合都支持each语法，默认参数为it
    println it
}

/**
输出
2
3
**/
```

##### **整型方法循环**

 ```groovy
 //upto()函数表示升序循环
 1.upto(3) {
     println it 
 }
 /**
 输出
 1
 2
 3
 **/
 
 //downto()函数表示降序循环
 3.downto(1) {
     println it  
 }
 /**
 输出
 3
 2
 1
 **/
 
 //n.times()方法，从0到n-1的循环
 3.times {
     println it
 }
 /**
 输出
 0
 1
 2
 **/
 
 //a.step(b,c)方法，从a到b-1,步距为c
 1.step(7, 2) {
     println it
 }
 /**
 输出
 1
 3
 5
 **/
 ```

### 方法

#### 定义

```groovy
//方法和变量一样，返回值类型可以使用弱类型def定义，也可以指定强类型
def hello(){
    return "Hello,World"
}

String world(){
    return "Hello,World"
}

println hello()   //输出Hello,World
println world()   //输出Hello,World
```

#### 参数

```groovy
//带参数的函数
def sum(int a,int b){
    return a+b
}

//带默认参数的函数
def plus(int a,int b=2){
    return a-b
}

//可变参数的函数
def log(msg, String[] details) {  //使用数组的方式
    println "$msg - ${details}"
}
def log2(msg, String... details) {  //使用...的方式
    println "$msg - ${details}"
}

//调用有参数的方法可以不带括号
def add(int x, int y) {
    return x + y
}

println sum(1,2)  //输出3
println plus(2)    //输出0
println plus(10,4)  //输出6
log('test', '1', '2')    //输出test - [1, 2]
log2('test', '1', '2')   //输出test - [1, 2]
print(add 2, 3)   //输出5，可以不带括号
```

### 其他

#### 空安全（?）

```groovy
def upperCase(str) {
    str?.toUpperCase()
}

println upperCase("hello world!") // HELLO WORLD!
println upperCase(null) // null
```

## 闭包

### 基础

+ 闭包定义

  ```groovy
  //定义闭包
  def clouser={ println("Hello groovy")}
  //调用闭包
  clouser.call()
  //或者
  clouser()
  
  //输出
  Hello groovy
  Hello groovy
  ```

+ 闭包参数

  ```groovy
  //定义携带参数的闭包
  //->左边是参数，右边是闭包体
  def clouser1={ String name->println("Hello,${name}")}
  //多个参数使用逗号隔开
  def clouser2={ String name,int age->println("Hello,${name},${age}")}
  //每个闭包都有一个默认的隐式参数it
  def clouser3={ println("Hello,${it}")}
  clouser1.call("groovy")
  clouser2.call("groovy",2)
  clouser3.call("groovy")
  
  //输出
  Hello,groovy
  Hello,groovy,2
  Hello,groovy
  Hello groovy
  ```

+ 闭包返回值

  ```groovy
  //返回值
  //闭包是一定有返回值的
  def clouser4={ println("Hello groovy")}
  println clouser4.call()
  //使用return作为返回值
  def clouser5={ return ("Hello groovy")}
  println clouser5.call()
  
  //输出
  null
  Hello groovy
  ```

### 使用

+ 与基础类型使用

  ```groovy
  int x = fab(5)
  int y = fab2(5)
  int z=cal(101)
  println(x)
  println(y)
  println(z)
  //计算阶乘的方法1
  int fab(int number) {
      int result = 1
      //upto实现递增循环
      1.upto(number, { num -> result *= num })
      return result
  }
  //计算阶乘的方法2
  int fab2(int number) {
      int result = 1
      //upto实现递减循环
      //闭包作为方法参数的最后一个可以直接使用{}
      number.downto(1) {
          num -> result *= num
      }
      return result
  }
  //求和运算
  int cal(int number) {
      int result = 0
      //从0开始做循环
      number.times {
          num->result += num
      }
      return result
  }
  
  //输出
  120
  120
  5050
  ```

+ 与String集合使用

  ```groovy
  //与字符串结合使用
  String str = "the 2 and 3 is 5"
  //each的遍历
  str.each {}
  //find来查找符合条件的第一个
  println str.find {
          //查找是否为Number类型
      String value -> value.isNumber()
  }
  //findAll查找所有符合条件的
  def list = str.findAll {
      String value -> value.isNumber()
  }
  println list.toListString()
  //any只要满足一个条件，返回true
  def result = str.any {
      String value -> value.isNumber()
  }
  println(result)
  //every只要不满足一个条件，就返回false
  println str.every {
      String value -> value.isNumber()
  }
  
  //输出
  2
  [2, 3, 5]
  true
  false
  ```

+ 与数据结构结合使用

+ 与文件结合使用

### 详解

+ 关键变量（关键字this、owner、delegate）

  ```groovy
  println("***********************闭包的详细讲解****************************")
  //三个重要变量this、owner、delegate
  def scriptClouser = {
      println "this:" + this   //代表闭包定义处的类
      println "owner:" + owner //代表闭包定义处的类或者对象
      println "delegate" + delegate  //代表任意对象，默认与owner一样
  }
  scriptClouser.call()
  //内部类中定义闭包
  println "****************内部类中定义闭包************************"
  class Person{
      def classClouser={
          println "classClouser this:" + this
          println "classClouser owner:" + owner
          println "classClouser delegate" + delegate
      }
      //方法中的闭包
      def say(){
          def classClouser={
              println "classMethodClouser this:" + this
              println "classMethodClouser owner:" + owner
              println "classMethodClouser delegate" + delegate
          }
          classClouser.call()
      }
  }
  Person p=new Person()
  p.classClouser.call()
  p.say()
  //闭包中定义闭包
  println "**************闭包中定义闭包***********************"
  def nestClouser={
      def innerClouser={
          println "innerClouser this:" + this
          println "innerClouser owner:" + owner      //输出nestClouser实例对象
          println "innerClouser delegate" + delegate  //输出nestClouser实例对象
      }
      innerClouser.delegate=p   //修改默认的delegate对象
      innerClouser.call()
  }
  nestClouser.call()
  
  //输出
  ***********************闭包的详细讲解****************************
  this:variable.ClousrerStudy@71075444
  owner:variable.ClousrerStudy@71075444
  delegatevariable.ClousrerStudy@71075444
  ****************内部类中定义闭包************************
  classClouser this:variable.Person@6cb107fd
  classClouser owner:variable.Person@6cb107fd
  classClouser delegatevariable.Person@6cb107fd
  classMethodClouser this:variable.Person@6cb107fd
  classMethodClouser owner:variable.Person@6cb107fd
  classMethodClouser delegatevariable.Person@6cb107fd
  **************闭包中定义闭包***********************
  innerClouser this:variable.ClousrerStudy@71075444
  innerClouser owner:variable.ClousrerStudy$_run_closure13@239a307b
  innerClouser delegatevariable.Person@6cb107fd
  ```

+ 委托策略

  ```groovy
  println "********************委托策略*********************"
  class Student{
      String name
      def pretty={ println "My name is ${name}"}
  
      @Override
      String toString() {
          return pretty.call()
      }
  }
  
  class Teacher{
      String name
  }
  Student stu=new Student(name:"jack")
  Teacher tea=new Teacher(name:"lucky")
  stu.pretty.delegate=tea
  //闭包默认会从自己的类中找name，设置以下就会从delegate对象中优先查找，找不到再去自己的类中查找
  stu.pretty.resolveStrategy=Closure.DELEGATE_FIRST //闭包的委托策略设置
  stu.toString()
  
  //输出
  ********************委托策略*********************
  My name is lucky
  ```

## 面向对象

### 属性

```groovy
//Groovy中声明了一个属性，系统会自动生成get和set方法。
class Cat {
    def speed = 10
}

def cat = new Cat()
println cat.getSpeed()  //输出10，也可以直接使用cat.speed
cat.setSpeed(20)

//set方法重定义
class Car {
    def speed = 10

    def setSpeed(sp) {
        speed = sp * 2
    }
}
Car car = new Car()
println car.speed // 10
car.speed = 100
println car.speed //200

//get方法重定义
class Car {
    def getSpeed() {
        100
    }
}
Car car = new Car()
println car.speed // 100
```

### 方法

Groovy方法属于动态类型，只有在调用时才会检查。可以调用`respondsTo()`方法来检查是否存在该方法。

#### 构造方法

```groovy
//在没有主动声明的构造函数时
class Cat {
    def speed = 10
}

def cat = new Cat(speed: 100)  //属性可以作为构造函数的入参
println cat.speed   //输出100

//显示声明了构造函数
class Cat {
    def speed = 10

    Cat(String name){
    }
}

def cat = new Cat('大黄')  //调用构造函数
println cat.speed  //输出10
```

#### respondsTo()方法

```groovy
class Rectangle {
    void draw() {
        println "Rectangel draw"
    }
}
class Circle {
    void draw() {
        println "Circle draw"
    }
    def getRadius() {
        return 10
    }
}
class Oval {
    void draw() {
        println "Oval draw"
    }
}
void draw(shape) {
    shape.draw()

    if (shape.metaClass.respondsTo(shape, "getRadius")) {   //检查是否存在getRadius方法
        println "radius = ${shape.getRadius()}"
    }
}
draw(new Rectangle())
draw(new Circle())
draw(new Oval())
```

## 文件

### 读取文件

```groovy
//按行读取
new File("E:/Example.txt").eachLine {  
         line -> println "line : $line"; 
      }

//读取所有内容
File file = new File("E:/Example.txt") 
println file.text 
```

### 写入文件

```groovy
new File('E:/','Example.txt').withWriter('utf-8') { 
         writer -> writer.writeLine 'Hello World' 
      }  
```

### 删除文件

```groovy
def file = new File('E:/Example.txt')
file.delete()
```

### 其他

```groovy
//1.获取文件大小
File file = new File("E:/Example.txt")
println "The file ${file.absolutePath} has ${file.length()} bytes"

//2.测试文件是否为目录
def file = new File('E:/') 
println "File? ${file.isFile()}" 
println "Directory? ${file.isDirectory()}"

//3.创建目录
def file = new File('E:/Directory')
file.mkdir()

//4.复制文件
def src = new File("E:/Example.txt")
def dst = new File("E:/Example1.txt")
dst << src.text

//5.输出目录下的所有文件（不包含子文件夹下的文件）
new File("E:/Temp").eachFile() {  
         file->println file.getAbsolutePath()
}

//6.输出输出目录下的所有文件（包含子文件夹下的文件）
new File("E:/temp").eachFileRecurse() {
         file -> println file.getAbsolutePath()
}
```