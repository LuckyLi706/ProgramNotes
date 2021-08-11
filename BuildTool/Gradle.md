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
}
```



```groovy
android {
    compileSdkVersion 29
    buildToolsVersion '29.0.2'
    defaultConfig {
        applicationId "com.lucky.app"
        minSdkVersion 17
        targetSdkVersion 29
        versionCode 5
        versionName "1.5.0"
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
        flavorDimensions "versionCode"
        renderscriptTargetApi 19
        renderscriptSupportModeEnabled true
        multiDexEnabled true

        ndk {
            abiFilters "armeabi-v7a", "arm64-v8a"
        }
    }
    signingConfigs {
        release {
            keyAlias ''
            keyPassword ''
            storeFile file('')
            storePassword ''
        }
    }

    buildTypes {
        release {
            signingConfig signingConfigs.release
            //混淆
            //minifyEnabled true
            // Zipalign优化
            //zipAlignEnabled true
            // 移除无用的resource文件
            //shrinkResources true
            // 前一部分代表系统默认的android程序的混淆文件，该文件已经包含了基本的混淆声明，后一个文件是自己的定义混淆文件
            //proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'

            /**
            配置BuildConfig变量
            **/
            buildConfigField("String", "PACK_TIME", "\"" + getTime() + "\"")
            buildConfigField("String", "BASE_URL", '"https://yzp.ssl.ysten.com/ysp-tv-api/"')
            buildConfigField("String", "MQTT_URL", '"tcp://36.155.71.242:8099"')
            buildConfigField("boolean", "IS_TEST", "false")
        }
        debug {

            //测试环境
            signingConfig signingConfigs.release
            buildConfigField("String", "PACK_TIME", "\"" + getTime() + "\"")
            buildConfigField("String", "BASE_URL", '"https://yzpdev.ssl.ysten.com/ysp-tv-api/"')
            buildConfigField("String", "MQTT_URL", '"tcp://39.99.189.185:1883"')
            buildConfigField("boolean", "IS_TEST", "true")
        }
    }

    lintOptions {
        checkReleaseBuilds false
        abortOnError false
    }
    sourceSets.main {
        jniLibs.srcDirs = ['src/main/libs'];
    }

    /**
     针对不同的渠道来生成不同参数
     xml配置：
     <meta-data
            android:name="LAUNCHER"
            android:value="${IS_LAUNCHER}" />
     java配置：       
     */
    productFlavors {
        cmcc {
            manifestPlaceholders = [CATEGORY_VALUE: "android.intent.category.DEFAULT", IS_LAUNCHER: false, CHANNEL_VALUE: "cmcc", IS_NEED_UPDATE: false]
        }
        launcher {
            manifestPlaceholders = [CATEGORY_VALUE: "android.intent.category.HOME", IS_LAUNCHER: true, CHANNEL_VALUE: "launcher", IS_NEED_UPDATE: true]
        }
        normal {
            manifestPlaceholders = [CATEGORY_VALUE: "android.intent.category.DEFAULT", IS_LAUNCHER: false, CHANNEL_VALUE: "normal", IS_NEED_UPDATE: true]
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    //输出release包
    applicationVariants.all { variant ->
        if (variant.buildType.name.equals('release')) {//防止AS无法安装debug包(apk)
            if (!isPack()) {
                return;
            }
            variant.outputs.all { output ->
                outputFileName = 'yst.cs' + "_" + "${variant.productFlavors[0].name}" + "_" + variant.versionName + "_" + variant.versionCode + '.apk'
                //outputFileName2  = "app-release.apk"
                //打包路径
                variant.packageApplication.outputDirectory = new File(project.rootDir.absolutePath + "/apk")
            }
        }
    }
}
```

