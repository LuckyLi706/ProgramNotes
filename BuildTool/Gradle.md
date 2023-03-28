<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Gradle](#gradle)
  - [Groovy语法](#groovy%E8%AF%AD%E6%B3%95)
    - [初探](#%E5%88%9D%E6%8E%A2)
    - [入门](#%E5%85%A5%E9%97%A8)
    - [变量类型](#%E5%8F%98%E9%87%8F%E7%B1%BB%E5%9E%8B)
    - [逻辑控制](#%E9%80%BB%E8%BE%91%E6%8E%A7%E5%88%B6)
    - [闭包](#%E9%97%AD%E5%8C%85)
      - [基础](#%E5%9F%BA%E7%A1%80)
      - [使用](#%E4%BD%BF%E7%94%A8)
      - [详解](#%E8%AF%A6%E8%A7%A3)
    - [复杂类型](#%E5%A4%8D%E6%9D%82%E7%B1%BB%E5%9E%8B)
      - [列表](#%E5%88%97%E8%A1%A8)
      - [映射](#%E6%98%A0%E5%B0%84)
      - [范围](#%E8%8C%83%E5%9B%B4)
    - [面向对象](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)
      - [定义](#%E5%AE%9A%E4%B9%89)
      - [方法](#%E6%96%B9%E6%B3%95)
  - [Android](#android)
    - [源码相关](#%E6%BA%90%E7%A0%81%E7%9B%B8%E5%85%B3)
      - [AndroidStudio关联Gradle源码](#androidstudio%E5%85%B3%E8%81%94gradle%E6%BA%90%E7%A0%81)
    - [setting.gradle](#settinggradle)
    - [build.gradle（外）](#buildgradle%E5%A4%96)
    - [build.gradle（内）](#buildgradle%E5%86%85)
    - [ndk配置](#ndk%E9%85%8D%E7%BD%AE)
    - [jar脚本](#jar%E8%84%9A%E6%9C%AC)
    - [aar脚本](#aar%E8%84%9A%E6%9C%AC)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Gradle

+ [gradle中文文档](https://doc.yonyoucloud.com/doc/wiki/project/GradleUserGuide-Wiki/about_this_user_guide.html)

+ gradle的组成
  - groovy核心语法
  - build script block
  - gradle api
+ 优势
  - 灵活性上
  - 粒度性上
  - 扩展性上
  - 兼容性上

## Groovy语法

### 初探

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

### 入门

- 可以不需要main方法，像脚本语言一样直接运行
- 不需要使用分号结尾
- 打印可以使用println或者println()

### 变量类型

+ 基本类型和对象类型和java一样，唯一不同的是基本类型都是包装类型

  ```groovy
  例子:
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

+ 定义方式

   1. 强类型定义（和java一样，需要强制声明变量的类型）

   2. 弱类型定义（使用**def关键字**来定义，不需要指定类型，可以重新赋值给其他类型的值）

      ```groovy
      int a_1=12  //强类型定义
      def b_1=12  //弱类型定义
      b_1="12"    //重新赋值
      ```

+ 字符串

  ```groovy
  /**
  单引号和三引号区别（类型为String）
  1、单引号（和双引号一样）
  2、三引号（可以有格式，和python一样）
  使用扩展表达式定义${变量}（带有扩展表达式的类型为GString，可以和String无缝对接）
  **/
  def name = '123'
  def doublename = "123"   //和上面单引号一样
  //有格式
  def tuplename = '''      
  123
  123
  123'''
  println(tuplename)
  def one = "123"
  //使用${变量}
  def two = "sayHello${one}"
  println(two)
  println(two.class)
  def sum = "two add three equal${2 + 3}"   //扩展表达式
  println(sum)
  
  //输出结果
  123
  123
  123
  sayHello123
  class org.codehaus.groovy.runtime.GStringImpl
  two add three equal5
  ```

### 逻辑控制

- 顺序逻辑
- 条件逻辑

       1. if/else
          2. switch/case

- 循环逻辑

    1. while循环
       2. for循环

### 闭包

#### 基础

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

#### 使用

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

#### 详解

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

### 复杂类型

#### 列表

```groovy
//列表数据结构
def list=[1,2,3,4]
println list.class
println list.size()
//定义数组
//第一种方式,使用as关键字
def array=[1,2,3,4] as int[]
//第二种方式，使用强类型定义
int[] array2=[1,2,34]
println array.class

//输出
class java.util.ArrayList
4
class [I
```

#### 映射

```groovy
//映射数据结构（相当于Java的Map）
//可以添加任意元素
//key默认为单引号不可变字符串

def colors=[rea:"123",ble:"222"]
//获取值第一种方式
println colors["rea"]
//获取值第二种方式
println colors.rea
//添加元素
colors.yello="111"
//添加多个元素
colors.complex=[a:1,b:2]
println colors
println colors.getClass()

//结果
123
123
[rea:123, ble:222, yello:111, complex:[a:1, b:2]]
class java.util.LinkedHashMap
```

#### 范围

```java
//范围数据结构(对象是Range，是List的子类)
def range=1..10  //定义1-10范围的数据
println range[0]
println range.contains(10)
println range.from
println range.to
//遍历
range.each {
    print it
}
println range.class

//输出
1
true
1
10
12345678910
class groovy.lang.IntRange
```

### 面向对象

#### 定义

```groovy
//类、抽象类（使用trait关键字）、接口（使用interface关键字）定义

//1、groovy中默认都是public的
class Person implements Action,DefaultAction{
    //定义属性
    int age
    String name
    //定义方法
    def increaseAge(Integer years){
        this.age=years
    }

    @Override
    def drink() {
        return null
    }

    @Override
    def eat() {
        return null
    }
}

//抽象类DefaultAction
//抽象类
trait DefaultAction {
    abstract eat()

    def learn(){
        println "我在学习"
    }
}

//接口Action
//接口
interface Action {
    def drink()
}

//调用
//无论你是直接使用点或者get/set,最终都会调用get/set方法
//只要声明了属性，会自动生成get/set方法
def person=new Person(name:"lucky",age:10)   //初始化可以直接给属性初始化值
println "the name is ${person.name},the age is ${person.age}"
person.increaseAge(19)
println "the name is ${person.getName()},the age is ${person.getAge()}"

//输出
the name is lucky,the age is 10
the name is 19,the age is 10
```

#### 方法

```groovy
class Person {
    //定义属性
    int age
    String name
    /**
     * 一个方法找不到时，用它来代替
     * @param name
     * @param args
     * @return
     */
    @Override
    def invokeMethod(String name, Object args) {
        return "mehod"
    }

    def methodMissing(String name, Object args) {
        return "${name}+${args}"+"mehod"
    }
}

//调用
def person=new Person(name:"lucky",age:10)

//不存在该方法时，优先去metaClass找，然后是否存在methodMissing，最后是否存在invokeMethod，都没有抛出异常
println person.cry()
//为类动态添加一个属性
person.metaClass.sex="male"
println person.sex
//为类动态注入一个方法,需要使用闭包
person.metaClass.sexUpperCase={ ->sex.toUpperCase()}
println person.sexUpperCase()
//为类添加动态的静态方法
Person.metaClass.static.AddStaticMethod={ -> println "static method"}
Person.AddStaticMethod()

//输出
cry+[]mehod
male
MALE
static method
```

## Android

### 源码相关

+ [Gradle插件和Gradle版本对应关系](https://developer.android.com/studio/releases/gradle-plugin)

+ [Gradle API](https://developer.android.com/reference/tools/gradle-api)

+ 几个重要的类

  - [CommonExtension](https://developer.android.com/reference/tools/gradle-api/4.2/com/android/build/api/dsl/CommonExtension#buildtypes_1)
  - [LibraryExtension](https://developer.android.com/reference/tools/gradle-api/4.2/com/android/build/api/dsl/LibraryExtension)
  - [ApplicationExtension](https://developer.android.com/reference/tools/gradle-api/4.2/com/android/build/api/dsl/ApplicationExtension)

  ```
  CommonExtension  里面定义了大量的闭包
  LibraryExtension 对应Library
  ApplicationExtension 对应了Application
  ```

#### AndroidStudio关联Gradle源码

```groovy
dependencies {

    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'com.google.android.material:material:1.2.1'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    testImplementation 'junit:junit:4.+'
    androidTestImplementation 'androidx.test.ext:junit:1.1.2'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.3.0'

    compileOnly("com.android.tools.build:gradle:4.1.1"){   //在moudle这边添加这个依赖,4.1.1表示当前使用的Gradle插件版本
        //移除这两个依赖，会有冲突，然后Ctrl+右击就可以进入相关源码了
        exclude module: 'common'    
        exclude module: 'bundletool'
    }
}
```

### setting.gradle

大多数setting.gradle的作用是为了配置子工程，再Gradle多工程是通过工程树表示的

```groovy
include ':demo1app', ':demo2app'    //指定Module的名字

project(':demo1app').projectDir = new File("Demo1\\demo1app") //可以手动指定Module的路径（非必须）
project(':demo2app').projectDir = new File("Demo2\\demo2app")
```

### build.gradle（外）

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {//这里是gradle脚本执行所需依赖，分别是对应的maven库和插件
    
    repositories {
        google()//从Android Studio3.0后新增了google()配置，可以引用google上的开源项目
        jcenter()//是一个类似于github的代码托管仓库，声明了jcenter()配置，可以轻松引用 jcenter上的开源项目
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:4.1.0'此处是android的插件gradle，gradle是一个强大的项目构建工具
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {//这里是项目本身需要的依赖，比如项目所需的maven库
    repositories {
        google()
        jcenter()
    }
}

// 运行gradle clean时，执行此处定义的task任务。
// 该任务继承自Delete，删除根目录中的build目录。
// 相当于执行Delete.delete(rootProject.buildDir)。
// gradle使用groovy语言，调用method时可以不用加（）。
task clean(type: Delete) {
    delete rootProject.buildDir
}
```

### build.gradle（内）

+ [flavorDimensions多维度理解](https://blog.csdn.net/chen_xi_hao/article/details/80526049)

```groovy
/**
plugins 闭包，定义当前的项目类型
com.android.application //表示当前为app项目
com.android.library   //表示当前为库文件

之前可以这样写
apply plugin: 'com.android.application'
apply plugin: 'com.android.library'

**/
plugins {
    id 'com.android.application'
}

/**
android{} 闭包
主要为了配置项目构建的各种属性
**/
android{
    compileSdkVersion 27//设置编译时用的Android版本
    //defaultConfig{}闭包
    defaultConfig {
        applicationId "com.billy.myapplication"//项目的包名
        minSdkVersion 16//项目最低兼容的版本
        targetSdkVersion 27//项目的目标版本
        versionCode 1//版本号
        versionName "1.0"//版本名称
        flavorDimensions "company"   //风味维度（针对多渠道打包的，必须填写）
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"//表明要使用AndroidJUnitRunner进行单元测试
        multiDexEnabled true   //支持多dex
    }
    
    /**
    signingConfigs闭包，闭包下面的标签名字可以随意起
    签名文件的配置，自动化打包
    需要放在buildTypes上面,不然找不到签名
    **/
    signingConfigs {// 自动化打包配置
        release {// 线上环境
            keyAlias 'test'    //签名别名
            keyPassword '123456' //签名密码
            storeFile file('test.keystore')  //签名文件
            storePassword '123456'   //签名文件的密码
            storeType 'jks'  //签名类型。当我们不填时，默认为 jks 类型
            v1SigningEnabled true //是否使用 v1 类型的签名方案。默认为true，即开启状态。如果我们将其置为false，则会导致在 7.0 以下版本，无法正常安装。
            v2SigningEnabled true //是否使用 v2 类型的签名方案。默认为true，即开启状态。v2在 7.0 版本之后才支持
        }
        debug {// 开发环境
            keyAlias 'test'
            keyPassword '123456'
            storeFile file('test.keystore')
            storePassword '123456'
        }
    }
    
    
    //buildTypes闭包
    buildTypes{ // 生产/测试环境配置
        //生成安装文件的主要配置
        release {// 生产环境
            /**
            生成的字段将保存到BuildConfig文件中
            这个方法接收三个非空的参数，第一个：确定值的类型，第二个：指定key的名字，第三个：传值
            带有方法的格式的值："\"" + getTime() + "\""
            带有字符串的格式的值：'"tcp://36.155.71.242:8099"'或者"\"https://release.cn/\""
            使用BuildConfig.LOG_DEBUG获取值。
            **/
            buildConfigField("boolean", "LOG_DEBUG", "false")//配置Log日志
            buildConfigField("String", "URL_PERFIX", "\"https://release.cn/\"")// 配置URL前缀
            minifyEnabled true//是否对代码进行混淆
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'//指定混淆的规则文件
            signingConfig signingConfigs.release//设置签名信息，使用signingConfigs闭包下的release标签
            pseudoLocalesEnabled true//是否在APK中生成伪语言环境，帮助国际化的东西，一般使用的不多
            shrinkResources true //是否清理无用资源,依赖于minifyEnabled
            zipAlignEnabled true//是否对APK包执行ZIP对齐优化，减小zip体积，增加运行效率
            applicationIdSuffix 'test'//在applicationId 中添加了一个后缀，一般使用的不多
            versionNameSuffix 'test'//在applicationId 中添加了一个后缀，一般使用的不多
        }
        debug {// 测试环境
            buildConfigField("boolean", "LOG_DEBUG", "true")//配置Log日志
            buildConfigField("String", "URL_PERFIX", "\"https://test.com/\"")// 配置URL前缀
            minifyEnabled false//是否对代码进行混淆
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'//指定混淆的规则文件
            signingConfig signingConfigs.debug//设置签名信息,使用signingConfigs闭包下的debug标签
            debuggable false//是否支持断点调试
            jniDebuggable false//是否可以调试NDK代码
            renderscriptDebuggable false//是否开启渲染脚本就是一些c写的渲染方法
            shrinkResources false //是否清理无用资源,依赖于minifyEnabled
            zipAlignEnabled true//是否对APK包执行ZIP对齐优化，减小zip体积，增加运行效率
            pseudoLocalesEnabled false//是否在APK中生成伪语言环境，帮助国际化的东西，一般使用的不多
            applicationIdSuffix 'test'//在applicationId 中添加了一个后缀，一般使用的不多
            versionNameSuffix 'test'//在applicationId 中添加了一个后缀，一般使用的不多
        }
    }
    
    /**
    productFlavors{}闭包
    多渠道配置
    下面有三个产品test1、test2、test3
    也可以为每个产品单独配置applicationId、versionName等
    **/
    productFlavors {
        test1 {
            /**
            使用BuildConfig
            使用方法：BuildConfig.displayFamilyName
            **/
            buildConfigField 'boolean', 'displayFamilyName', 'true'  
            /**
            配合AndroidManifest.xml使用
            
            xml配置
            <meta-data
            android:name="APP_KEY"
            android:value="${APP_KEY}"/>
            
            java代码：
            ApplicationInfo appInfo = getPackageManager()
                    .getApplicationInfo(getPackageName(),
                            PackageManager.GET_META_DATA);

            String app_key = appInfo.metaData.getString("APP_KEY");
           
            **/
            manifestPlaceholders = ["APP_KEY": "test1"]    //可以使用逗号隔开在[]中添加多个
            /**
            在资源文件中使用
            string.xml:
            <resources>
               <string name="app_name">@string/appName</string>
            </resources>
            **/
            resValue "string", "appName", '"111"'  
            
            
        }
        test2 {
            buildConfigField 'boolean', 'displayFamilyName', 'false'  //列表Item前面是显示姓还是名
            manifestPlaceholders = ["APP_KEY": '"test12"']
            resValue "string", "appName", '"222"'
        }
        test3 {
            buildConfigField 'boolean', 'displayFamilyName', 'true'  //列表Item前面是显示姓还是名
            manifestPlaceholders = ["APP_KEY": "123456789333"]
            resValue "string", "appName", '"333"'
        }
    }
    
    
    /**
    自定义包的名字和文件输出路径
    **/
    applicationVariants.all { variant ->
        if (variant.buildType.name.equals('release')) { 
            variant.outputs.all { output ->
                outputFileName = 'company' + "_" + "${variant.productFlavors[0].name}" + "_" + variant.versionName + "_" + variant.versionCode + '.apk'
                //outputFileName2  = "app-release.apk"
                //打包路径
                variant.packageApplication.outputDirectory = new File(project.rootDir.absolutePath + "/apk")
            }
        }
    }
    
    /**
    packagingOptions{}闭包：打包时的相关配置
    **/
    packagingOptions{
        //pickFirsts做用是 当有重复文件时 打包会报错 这样配置会使用第一个匹配的文件打包进入apk
        // 表示当apk中有重复的META-INF目录下有重复的LICENSE文件时  只用第一个 这样打包就不会报错
        pickFirsts = ['META-INF/LICENSE']

        //merges何必 当出现重复文件时 合并重复的文件 然后打包入apk
        //这个是有默认值得 merges = [] 这样会把默默认值去掉  所以我们用下面这种方式 在默认值后添加
        merge 'META-INF/LICENSE'

        //这个是在同时使用butterknife、dagger2做的一个处理。同理，遇到类似的问题，只要根据gradle的提示，做类似处理即可。
        exclude 'META-INF/services/javax.annotation.processing.Processor'
    }
    
    /**
    lintOptions{}闭包：代码扫描分析
    程序在编译的时候会检查lint，有任何错误提示会停止build，我们可以关闭这个开关
    **/
    lintOptions {
        abortOnError false //即使报错也不会停止打包
        checkReleaseBuilds false  //打包release版本的时候进行检测
    }
    
    
}
```

### 多渠道打包脚本

```groovy
static def buildTime() {
    return new Date().format("yyyy_MM_dd_HH_mm")
}

android {
    compileSdkVersion 30
    buildToolsVersion '30.0.3'

    defaultConfig {
        applicationId "com.imi.gamestore"
        minSdkVersion 19
        targetSdkVersion 31
        versionCode 5
        versionName "2.0"
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"

        flavorDimensions "imi"   //风味维度（针对多渠道打包的，必须填写）

        multiDexEnabled true

        ndk {
            // 设置支持的SO库架构
            abiFilters 'x86', 'armeabi-v7a', 'x86_64', 'arm64-v8a'
        }
    }

    ....

    /**
     productFlavors{}闭包
     多渠道配置
     下面有三个产品test1、test2、test3
     也可以为每个产品单独配置applicationId、versionName等
     **/
    productFlavors {
        XiaoPai {}
    }

    //定义一个装apk文件路径的数组
    def fileArray = []

    /**
     自定义包的名字和文件输出路径
     **/
    applicationVariants.all { variant ->    //批量修改Apk名字
        variant.outputs.all { output ->
            if (!variant.buildType.isDebuggable()) {
                //获取签名的名字 variant.signingConfig.name
                //要被替换的源字符串
                def sourceFile = "app-${variant.flavorName}-${variant.buildType.name}"
                //替换的字符串
                def replaceFile = "ImiLand_${variant.flavorName}_${variant.versionName}_${buildTime()}"
                outputFileName = output.outputFile.name.replace(sourceFile, replaceFile)
                fileArray.add(outputFile.parentFile.absolutePath + File.separator + replaceFile + ".apk")
            }
        }
    }

    build {
        doLast() {
            println "任务1编译打包完成后需要复制apk的数量:" + fileArray.size()
            forEachFile(fileArray)
        }
    }
}


def forEachFile(fileArray) {
    fileArray.forEach { file ->
        //遍历进行文件操作
        println "任务3遍历apk文件"
        move_apk(file)
    }
}

def move_apk(originalFile) {
    def intoFile = project.rootDir.absolutePath + File.separator + "apk"
    copy {
        from originalFile
        into intoFile
    }
}
```

### [ndk配置](https://developer.android.com/studio/projects/gradle-external-native-builds)

```groovy
//cmake相关属性
ANDROID_TOOLCHAIN	clang (default)
gcc (deprecated)	
指定 Cmake 编译所使用的工具链。
使用示例：arguments "-DANDROID_TOOLCHAIN=clang"

ANDROID_PLATFORM	API版本	
指定 NDK 所用的安卓平台的版本是多少。
使用示例：arguments "-DANDROID_PLATFORM=android-21"

ANDROID_STL	
gnustl_static（default）
详细见附表（C++ 库支持）
指定 Cmake 编译所使用的标准模版库。
使用示例：arguments "-DANDROID_STL=gnustl_static"

ANDROID_PIE	ON （android-16 以上默认为 ON）
OFF （android-15 以下默认为 OFF）	
使得编译的 elf 文件可以加载到内存中的任意位置就叫 pie（position independent executables）。
出于安全保护，在 Android 4.4 之后可执行文件必须是采用PIE编译的。
使用示例：arguments "-DANDROID_PIE=ON"

ANDROID_CPP_FEATURES	空（default）
rtti（支持 RTTI）
exceptions（支持 C++ 异常）	
指定是否需要支持 RTTI（RunTime Type Information）和 C++ 的异常，默认为空。
使用示例：arguments "-DANDROID_CPP_FEATURES=rtti exceptions"

ANDROID_ALLOW_UNDEFINED_SYMBOLS	TRUE
FALSE（default）	
指定在编译时，如果遇到未定义的引用时是否抛出错误。如果要允许这些类型的错误，请将该变量设置为 TRUE。
使用示例：arguments "-DANDROID_ALLOW_UNDEFINED_SYMBOLS=TRUE"

ANDROID_ARM_MODE	arm
thumb (default)	
如果是 thumb 模式，每条指令的宽度是 16 位，如果是 arm 模式，每条指令的宽度是 32 位。
使用示例：arguments "-DANDROID_ARM_MODE=arm"

ANDROID_ARM_NEON	TRUE
FALSE（default）	
指定在编译时，是否使用 NEON 对代码进行优化。NEON 只适用于 armeabi-v7a 和 x86 ABI，且并非所有基于 ARMv7 的 Android 设备都支持 NEON，但支持的设备可能会因其支持标量/矢量指令而明显受益。
更多参考：https://developer.android.com/ndk/guides/cpu-arm-neon#rd
使用示例：arguments "-DANDROID_ARM_NEON=TRUE"

ANDROID_DISABLE_NO_EXECUTE	TRUE
FALSE（default）	
指定在编译时是否启动 NX（No eXecute）。NX 是一种应用于 CPU 的技术，帮助防止大多数恶意程序的攻击。如果要禁用 NX，请将该变量设置为 TRUE。
使用示例：arguments "-DANDROID_DISABLE_NO_EXECUTE=TRUE"

ANDROID_DISABLE_RELRO	TRUE
FALSE（default）	
RELocation Read-Only (RELRO) 重定位只读，它能够保护库函数的调用不受攻击者重定向的影响。如果要禁用 RELRO，请将该变量设置为 TRUE。
使用示例：arguments "-DANDROID_DISABLE_RELRO=FALSE"

ANDROID_DISABLE_FORMAT_STRING_CHECKS	TRUE
FALSE（default）	
在类似 printf 的方法中使用非常量格式字符串时是否抛出错误。如果为 TRUE，即不检查字符串格式。
使用示例：arguments "-DANDROID_DISABLE_FORMAT_STRING_CHECKS=FALSE"

附表（C++ 库支持）
libstdc++	 默认最小系统 C++ 运行时库	 不适用
gabi++_static	 GAbi++ 运行时（静态）。	 C++ 异常和 RTTI
gabi++_shared	 GAbi++ 运行时（共享）。	 C++ 异常和 RTTI
stlport_static	 STLport 运行时（静态）。	 C++ 异常和 RTTI；标准库
stlport_shared	 STLport 运行时（共享）。	 C++ 异常和 RTTI；标准库
gnustl_static	 GNU STL（静态）。	 C++ 异常和 RTTI；标准库
gnustl_shared	 GNU STL（共享）。	 C++ 异常和 RTTI；标准库
c++_static	 LLVM libc++ 运行时（静态）。	 C++ 异常和 RTTI；标准库
c++_shared	 LLVM libc++ 运行时（共享）。	 C++ 异常和 RTTI；标准库

android {
  ...
  defaultConfig {
    ...
    //配置cmake的属性    
    externalNativeBuild {
      cmake {
        // 指定一些编译选项
        cppFlags "-std=c++11 -frtti -fexceptions"
        // 也可以使用下面这种语法向变量传递参数：
        // arguments "-D变量名=参数".
        arguments "-DANDROID_ARM_NEON=TRUE",
        // 使用下面这种语法向变量传递多个参数（参数之间使用空格隔开）：
        // arguments "-D变量名=参数1 参数2"
                  "-DANDROID_CPP_FEATURES=rtti exceptions"
 
        // 指定ABI
        abiFilters "armeabi-v7a" , "arm64-v8a"
      }
    }
    //或者这样来指定ABI
    ndk {
      // Specifies the ABI configurations of your native
      // libraries Gradle should build and package with your app.
      abiFilters 'x86', 'x86_64', 'armeabi', 'armeabi-v7a',
                   'arm64-v8a'
    }
  }
  buildTypes {...}
  
  externalNativeBuild {
    cmake {
        path "CMakeLists.txt"  //指定CMakeLists文件
    }
  }
  
  //指定ndk版本,路径在sdk/ndk/版本
  android {
     ndkVersion "25.2.9519653"
  }
}
```

### jar脚本

```groovy
/**
高版本archiveName和destinationDir参数会提示过时
可以使用下面两个替换
destinationDir is replaced by destinationDirectory
archiveName is replaced by archiveFileName
**/
task generateJar(type: Jar, dependsOn: ['build']) {   //当前的脚本依赖于build脚本
    archiveName = "yyyyy.jar" //打包后的jar包名
    //打包的资源路径
    from('build/intermediates/javac/debug/classes')
    destinationDir = file('release') //打包后jar文件的存放路径
    //添加一些忽略文件
    exclude('android')   //忽略android目录下的所有文件
    //忽略掉全部BuiuldConfig文件
    exclude('**/BuildConfig.class')
    exclude('**/BuildConfig\$*.class')
    //忽略掉全部R文件
    exclude('**/R.class')
    exclude('**/R\$*.class')
}

//删除已存在的 Jar 包
task deleteOldJar(type: Delete) {
  delete 'build/libs/analytics.jar'
}
```

### aar脚本

```groovy
android.libraryVariants.all { variant ->
        if(variant.name.equalsIgnoreCase("release")) {
            variant.outputs.all { output ->
                def f = output.outputFileName
                if (f != null && f.endsWith('.aar')) {  
                    def fileName = "zidingyi-v${defaultConfig.versionName}.aar"   //自定义aar名字
                    output.outputFileName = fileName
                }
            }
        }
    }
```

