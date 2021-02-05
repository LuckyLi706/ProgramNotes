# Android

## 开发

+ 入门
  1. [Java](../Java.md)
  2. [Kotlin](../Kotlin.md)
  3. [Java官方学习](https://www.oracle.com/technetwork/cn/java/newtojava-100451-zhs.html)
  4. [Kotlin官方学习](https://www.kotlincn.net/docs/reference/)

+ 进阶

  - [UI](AndroidUI.md)

  + [JNI（native层）](AndroidJNI.md)
  + [IPC（跨进程）](AndroidIPC.md)

+ [开源库](AndroidOpenSource.md)

+ 安卓源码
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
  
+ 其他开发

  + [大疆无人机](大疆SDK（安卓版）.md)

## 逆向

+ [Smail语法（Dalvik指令）](AndroidSmail.md)
+ [工具](AndroidDecompileTool.md)
+ [调试](AndroidDebug.md)
+ Hook
+ ELF文件
  1. [C++](../C++.md)
  2. ARM汇编
+ 脱壳

## 其他

+ [命令（SDK的命令工具）](AndroidCommand.md)
+ [刷机和Root](AndroidBrushRoot.md)
+ [多开](AndroidMultiboxing.md)
+ [模拟器](AndroidSimulator.md)