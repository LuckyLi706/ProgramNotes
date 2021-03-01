# Android

## 开发

### 入门

1. [Java](../Java.md)
2. [Kotlin](../Kotlin.md)
3. [Java官方学习](https://www.oracle.com/technetwork/cn/java/newtojava-100451-zhs.html)
4. [Kotlin官方学习](https://www.kotlincn.net/docs/reference/)

### 进阶

+ [UI](AndroidUI.md)
+ [JNI（native层）](AndroidJNI.md)
+ [IPC（跨进程）](AndroidIPC.md)
+ [开源库](AndroidOpenSource.md)

### 学习资料

+ [Android 开发中的日常积累](https://github.com/lizhangqu/CoreLink)
+ [Android 学习资料收集](https://github.com/Freelander/Android_Data)
+ [收集利用 Kotlin 进行 Android 开发的开源库，扩展，工具，开源项目，资料等高质量资源的集合](https://github.com/adisonhuang/awesome-kotlin-android)
+ [Android面试总结](https://github.com/ddnosh/BestReview)

### 安卓源码

  - [在线镜像](http://androidxref.com/9.0.0_r3/xref/)
  - [官网](https://github.com/aosp-mirror)

+ 开发系统应用

  - 添加系统标志

    ```xml
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="com.shoukong.umpsky"
        android:sharedUserId="android.uid.system">    //加入这一句xml
    ```

  - 去安卓源码下的build/target/product/security获取platform.x509.pem和platform.pk8文件

  - 用工具把系统签名文件导入自己的签名文件，[keytool-importkeypair](https://github.com/getfatday/keytool-importkeypair)

    ```sh
    //导入命令,然后就可以使用新的jks进行系统签名了
    ./keytool-importkeypair -k myJks.jks -p 123456 -pk8 platform.pk8 -cert platform.x509.pem -alias MySign
    ```

  - 查看是否转换成功

    ```
    查看jks : keytool -list -v -keystore [~/keystore文件夹/keystore.jks] -storepass 123456
    查看pem：keytool -printcert -file [pem绝对路径] 
    ```

  - [申请app为系统应用，使用WebView报错解决方案](https://blog.csdn.net/wxj280306451/article/details/106522384)

  - 参考文章
  
    1. [Android 生成系统签名文件的可行性分析](https://www.jianshu.com/p/12f27d292ffd)
    2. [Android Studio自动生成带系统签名的apk](https://blog.csdn.net/cxq234843654/article/details/51557025)
  
### 其他开发

  + [大疆无人机](大疆SDK（安卓版）.md)

## 逆向

+ [Smail语法（Dalvik指令）](AndroidSmail.md)
+ [工具](AndroidDecompileTool.md)
+ [调试](AndroidDebug.md)
+ Hook
+ ELF文件
  1. [C++](../C++.md)
  2. [ARM汇编](AndroidARM.md)
+ 脱壳

## 其他

+ [命令（SDK的命令工具）](AndroidCommand.md)
+ [刷机和Root](AndroidBrushRoot.md)
+ [多开](AndroidMultiboxing.md)
+ [模拟器](AndroidSimulator.md)
+ [上传自己的库到jcenter](https://blog.csdn.net/linglongxin24/article/details/53415932)

  ```groovy
  /** 以下开始是将Android Library上传到jcenter的相关配置**/
  
  apply plugin: 'com.github.dcendents.android-maven'
  apply plugin: 'com.jfrog.bintray'
  
  //项目主页
  def siteUrl = 'https://github.com/LuckyLi706/AndroidPlugin'    // project homepage
  //项目的版本控制地址
  def gitUrl = 'https://github.com/LuckyLi706/AndroidPlugin.git' // project git
  
  //发布到组织名称名字，必须填写
  group = "com.lucky.commplugin"
  //发布到JCenter上的项目名字，必须填写
  def libName = "CommPlugin"
  // 版本号，下次更新是只需要更改版本号即可
  version = "1.0.0"
  /**  上面配置后上传至jcenter后的编译路径是这样的： compile 'cn.bluemobi.dylan:sqlitelibrary:1.0'  **/
  
  //生成源文件
  task sourcesJar(type: Jar) {
      from android.sourceSets.main.java.srcDirs
      classifier = 'sources'
  }
  //生成文档
  task javadoc(type: Javadoc) {
      source = android.sourceSets.main.java.srcDirs
      classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
      options.encoding "UTF-8"
      options.charSet 'UTF-8'
      options.author true
      options.version true
      failOnError false
  }
  
  //文档打包成jar
  task javadocJar(type: Jar, dependsOn: javadoc) {
      classifier = 'javadoc'
      from javadoc.destinationDir
  }
  //拷贝javadoc文件
  task copyDoc(type: Copy) {
      from "${buildDir}/docs/"
      into "docs"
  }
  
  //上传到jcenter所需要的源码文件
  artifacts {
      archives javadocJar
      archives sourcesJar
  }
  
  // 配置maven库，生成POM.xml文件
  install {
      repositories.mavenInstaller {
          // This generates POM.xml with proper parameters
          pom {
              project {
                  packaging 'aar'
                  name '硬件通信库'
                  url siteUrl
                  licenses {
                      license {
                          name '硬件通信库'
                          url 'https://github.com/LuckyLi706/AndroidPlugin'
                      }
                  }
                  developers {
                      developer {
                          id 'jackyli706'
                          name 'lijie'
                          email 'jackyli706@gmail.com'
                      }
                  }
                  scm {
                      connection gitUrl
                      developerConnection gitUrl
                      url siteUrl
                  }
              }
          }
      }
  }
  
  //上传到jcenter
  bintray {
      user = rootProject.ext.user    //读取config.gradle文件里面的 bintray.user
      key = rootProject.ext.key  //读取config.gradle文件里面的 bintray.apikey
      configurations = ['archives']
      pkg {
          repo = "FirstMaven"
          name = libName    //发布到JCenter上的项目名字，必须填写
          desc = '硬件通信'    //项目描述
          websiteUrl = siteUrl
          vcsUrl = gitUrl
          licenses = ["Apache-2.0"]
          publish = true
      }
  }
  ```

  
