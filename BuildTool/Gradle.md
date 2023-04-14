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

+ [Gadle中文文档](https://doc.yonyoucloud.com/doc/wiki/project/GradleUserGuide-Wiki/about_this_user_guide.html)

+ [Gradle入门很好的文章](https://juejin.cn/post/7155109977579847710)

+ 特点

  1. Gradle是一个基于JVM运行的构建工具，使用java编写；

  2. 脚本语言(DSL)使用[Groovy](../Groovy.md)(.gradle)、[Kotlin](../Kotlin.md)(.gradle.kts)编写，都是高级语言，都是面向对象编程；

  3. Gradle中的核心对象是`Task`，Task是Gradle中最小的构建单元，Action是最小的执行单元；

  4. Gradle中的`Project`对应一个工程，是树形结构，可以向下或向上遍历，还用来关联Task；

  5. Gradle提供了很好的扩展能力，可以根据需求自定义插件及配置；

  6. Gradle在各个`生命周期`阶段提供了丰富的回调，对于切面处理的扩展很有帮助；

## Gradle初级

### 配置

#### gradle-wrapper

+ [Gradle下载地址](https://services.gradle.org/distributions/)

  下载的Gradle类型分为all、bin、doc

  - `doc`：顾名思义，用户文档；
  - `bin`：即binary，可运行并不包含多余的东西；
  - `all`：包含所有，除了bin之外还有用户文档、sample等；

+ [Gradle、Android Gradle Plugin、Android Studio三者的版本映射关系](https://developer.android.google.cn/studio/releases/gradle-plugin?hl=zh-cn#updating-gradle)

`wrapper`是对Gradle的一层封装，封装的意义在于可以使Gradle的版本跟着项目走，这样这个项目就可以很方便的在不同的设备上运行，比如开源项目一般都不会把gradle文件夹设置到`gitignore`文件里，就是为了保证你clone下来是可以运行的。

- `gradle-wrapper.jar`：主要是Gradle的运行逻辑，包含下载Gradle；

- `gradle-wrapper.properties`：gradle-wrapper的配置文件，核心是定义了Gradle版本；


```ini
#Sun Oct 16 15:59:36 CST 2022
# 下载的Gradle的压缩包解压后的主目录；
distributionBase=GRADLE_USER_HOME
# Gradle版本的下载地址；
distributionUrl=https://services.gradle.org/distributions/gradle-7.4-bin.zip
# 相对于distributionBase的解压后的Gradle的路径，为wrapper/dists；
distributionPath=wrapper/dists
# 同distributionPath，不过是存放zip压缩包的；
zipStorePath=wrapper/dists
# 同distributionBase，不过是存放zip压缩包的主目录；
zipStoreBase=GRADLE_USER_HOME
```

### 常用命令及构建参数

### 生命周期

#### 三个阶段

任何构建任务都会执行这三个阶段

1. Initialization (初始化)

   在 Initialization (初始化) 阶段，Gradle会决定构建中包含哪些项目，并会为每个项目创建Project实例。为了决定构建中会包含哪些项目，Gradle首先会寻找settings.gradle来决定此次为单项目构建还是多项目构建，单项目就是module，多项目即project+app+module(1+n)

2. Configuration (配置)

   在 Configuration (配置) 阶段，Gradle会评估构建项目中包含的所有构建脚本，随后应用插件、使用DSL配置构建，并在最后注册Task，同时惰性注册它们的输入，因为并不一定会执行。

3. Execution (执行)

   最后，在 Execution (执行) 阶段，Gradle会执行构建所需的Task集合。

## Gradle中级

### 依赖管理

### buildSrc

### 打包配置

### Task

### Project

## Gradle高级

### 插件开发

### 编译提速

### Android打包流程

## Android（AGP）

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

+ [从AGP构建过程到APK打包过程](https://juejin.cn/post/6963527524609425415)

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

### 配置相关

#### setting.gradle

##### 7.0之前

大多数setting.gradle的作用是为了配置子工程，在Gradle多工程是通过工程树表示的

```groovy
include ':demo1app', ':demo2app'    //指定Module的名字

project(':demo1app').projectDir = new File("Demo1\\demo1app") //可以手动指定Module的路径（非必须）
project(':demo2app').projectDir = new File("Demo2\\demo2app")
```

##### 7.0之后

```groovy
//插件管理，指定插件下载的仓库，及版本。
pluginManagement {
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
    }
}

//依赖管理，指定依赖库的仓库地址，及版本。即7.0之前的allprojects。顺序决定了先从哪个仓库去找依赖库并下载，一般为了编译稳定，会把阿里的镜像地址（或自建私有仓库）放在Google()仓库之前。
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}
rootProject.name = "GradleX"   //项目名称
include ':app'   //用于指定构建应用时应将哪些模块包含在内，即参与构建的模块.
```

#### build.gradle（Project）

+ [AGP版本与Gradle版本对应关系](https://developer.android.com/studio/releases/gradle-plugin?hl=zh-cn)

##### 7.0之前

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {//这里是gradle脚本执行所需依赖，分别是对应的maven库和插件
    
    repositories {
        google()//从Android Studio3.0后新增了google()配置，可以引用google上的开源项目
        jcenter()//是一个类似于github的代码托管仓库，声明了jcenter()配置，可以轻松引用 jcenter上的开源项目
    }
    dependencies {
        //安卓的gradle插件（AGP）
        classpath 'com.android.tools.build:gradle:4.1.0'
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


//安卓Gradle插件7.0以上，该文件变成以下内容
plugins {
    id 'com.android.application' version '7.4.1' apply false
    id 'com.android.library' version '7.4.1' apply false
    id 'org.jetbrains.kotlin.android' version '1.5.31' apply false
}
```

##### 7.0之后

Gradle7.0之后，project下的`build.gradle`文件变动很大，默认只有plugin的引用了，其他原有的配置挪到`settings.gradle`文件中了。

```groovy
//7.0以上版本如果无法确认id，可以添加如下方式确认插件
buildscript {
    ...
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.6.20"
    }
}

//plugin格式  id «plugin id» version «plugin version» [apply «false»] 
//apply false表示不将该plugin应用于当前项目，比如在多项目构建中，我只想在某个子项目依赖该plugin就好了
plugins {
    id 'com.android.application' version '7.3.0' apply false
    id 'com.android.library' version '7.3.0' apply false
    id 'org.jetbrains.kotlin.android' version '1.7.10' apply false
}

//我只想在某个子项目依赖该plugin
if (subproject.name == "subProject") {
        apply plugin: 'org.jetbrains.kotlin.android'
   }
}
```

#### build.gradle（Module）

+ [flavorDimensions多维度理解](https://blog.csdn.net/chen_xi_hao/article/details/80526049)
+ apply plugin和apply from的区别
  + apply plugin：'yechaoa'：叫做二进制插件，二进制插件一般都是被打包在一个jar里独立发布的，比如我们自定义的插件，再发布的时候我们也可以为其指定plugin id，这个plugin id最好是一个全限定名称，就像你的包名一样；
  + apply from：'yechaoa.gradle'：叫做应用脚本插件，应用脚本插件，其实就是把这个脚本加载进来，和二进制插件不同的是它使用的是`from`关键字，后面紧跟一个脚本文件，可以是本地的，也可以是网络存在的，如果是网络上的话要使用`HTTP URL`。
    - 虽然它不是一个真正的插件，但是不能忽视它的作用，它是脚本文件模块化的基础，我们可以把庞大的脚本文件进行分块、分段整理拆分成一个个共用、职责分明的文件，然后使用apply from来引用它们，比如我们可以把常用的函数放在一个utils.gradle脚本里，供其他脚本文件引用。

```groovy
/**
plugins 闭包，定义当前的项目类型
com.android.application //表示当前为app项目
com.android.library   //表示当前为库文件

7.0之前这样写
apply plugin: 'com.android.application'
apply plugin: 'com.android.library'

7.0之后这样写
plugins {
    id 'com.android.application'
}
**/
plugins {
    id 'com.android.application'
}

/**
android{} 闭包
是Android插件提供的一个扩展类型，可以让我们自定义Gradle Android工程，是Gradle Android工程配置的唯一入口。
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
            multiDexEnabled：      //是否拆成多个Dex
            multiDexKeepFile：     //指定文本文件编译进主Dex文件中
            multiDexKeepProguard： //指定混淆文件编译进主Dex文件中
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
  
    //开启或关闭构建功能，常见的有viewBinding、dataBinding、compose。
    buildFeatures {
        viewBinding = true
        // dataBinding = true
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

/**
implementation：该依赖方式所依赖的库不会传递，只会在当前module中生效。
api：该依赖方式会传递所依赖的库，当其他module依赖了该module时，可以使用该module下使用api依赖的库。
provided：只在编译时有效，不会参与打包。
testImplementation：只在单元测试代码的编译以及最终打包测试apk时有效
debugImplementation：只在debug模式的编译和最终的debug apk打包时有效
releaseImplementation：仅仅针对Release 模式的编译和最终的Release apk打包。
**/
dependencies {
    //依赖libs目录下的所有jar文件
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.8.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
}
```

#### gradle.properties

位于项目的根目录下，用于指定 Gradle 构建工具包本身的设置，也可用于项目版本管理。

```ini
# Project-wide Gradle settings.
# IDE (e.g. Android Studio) users:
# Gradle settings configured through the IDE *will override*
# any settings specified in this file.
# For more details on how to configure your build environment visit
# http://www.gradle.org/docs/current/userguide/build_environment.html
# Specifies the JVM arguments used for the daemon process.
# The setting is particularly useful for tweaking memory settings.
org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m
# When configured, Gradle will run in incubating parallel mode.
# This option should only be used with decoupled projects. More details, visit
# http://www.gradle.org/docs/current/userguide/multi_project_builds.html#sec:decoupled_projects
# org.gradle.parallel=true
# AndroidX package structure to make it clearer which packages are bundled with the
# Android operating system, and which are packaged with your app"s APK
# https://developer.android.com/topic/libraries/support-library/androidx-rn
android.useAndroidX=true
# Automatically convert third-party libraries to use AndroidX
android.enableJetifier=true
# Kotlin code style for this project: "official" or "obsolete":
kotlin.code.style=official

# ---------- 编译相关 start ----------

#并行编译
org.gradle.parallel=true

#构建缓存
org.gradle.caching=true

# ---------- 编译相关 end ----------

# ---------- 版本相关 start ----------

yechaoaPluginVersion="1.0.0"
# 以下是gradle的引用方式
# pluginManagement {
#  plugins {
#        id 'com.yechaoa.gradlex' version "${yechaoaPluginVersion}"
#    }
# }
# ---------- 版本相关 end ----------
```

#### local.properties

```ini
## This file must *NOT* be checked into Version Control Systems,
# as it contains information specific to your local configuration.
#
# Location of the SDK. This is only used by Gradle.
# For customization when using a Version Control System, please read the
# header note.
#Mon Feb 08 19:07:41 CST 2021
sdk.dir=/Users/yechao/Library/Android/sdk

# ndk的这种引入方式已废弃，直接在gradle下的android{}下设置
ndk.dir=/Users/yechao/Library/Android/ndk   
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

