# IOS

## 开发

+ 基础（预备知识OC或者Swift）
+ 进阶
+ 开源库
+ [Cocoapods](IOSCocoapods.md)

## 逆向

+ [工具篇]()
+ [调试](IOSDebug.md)

## 其他

### 刷机和越狱

+ ROM相关知识

  ```
  1.下载的固件代号意义：
  如：iPhone_4.7_10.3.3_14G60_Restore
  4.7：代表4.7寸的屏幕
  10.3.3：表示系统大版本号
  14G60：大版本号的一个小版本号
  
  2.硬件内部代号
  iPhone         Internal Name: iPhone11
  iPhone 3G   Internal Name: iPhone12
  iPhone 3GS Internal Name: iPhone21
  iPhone 4      Internal Name: iPhone31 iPhone32 iPhone33
  iPhone 4S    Internal Name: iPhone41
  iPhone 5      Internal Name: iPhone51 iPhone52
  iPhone 5s     Internal Name: iPhone61 iPhone62
  iPhone 6       Internal Name: iPhone72
  iPhone 6 Plus  Internal Name: iPhone71
  iPhone 6s         Internal Name: iPhone81
  iPhone 6s Plus Internal Name: iPhone82
  iPhone 7	 Internal Name: iPhone9,1 iPhone9,3
  iPhone 7 Plus   Internal Name: iPhone9,2 iPhone9,4
  iPhone 8	Internal Name: iPhone10,1 iPhone10,4
  iPhone 8 Plus   Internal Name: iPhone10,2 iPhone10,5
  iPhone X	Internal Name: iPhone10,3 iPhone10,6
  ```

+ 刷机

  PP助手和爱思助手上面去下载（IOS一般不可降低版本，除非官网开放了降级通道）

+ 越狱

  - [unc0ver下载](https://github.com/pwn20wndstuff/Undecimus/releases)
  - [Cydia出现 host unreachable](https://bbs.feng.com/read-htm-tid-11777306.html)

  ```
  //高版本越狱
  下载unc0ver，需要自签名
  ```

+ Cydia插件
  
  + openssh（局域网内连接手机查看文件，如xshell）
  + [frida（使用js来hook ipa）](http://build.frida.re/)
  + Filza（手机上查看文件）

### libimobiledevice和ideviceinstaller

```
libimobiledevice又称libiphone，是一个开源包，可以让Linux支持连接iPhone/iPod Touch等iOS设备，跨平台意义。
（类似于安卓的adb）
官方github地址：https://github.com/libimobiledevice/libimobiledevice
安装：（/usr/local/Cellar）
brew install --HEAD libimobiledevice。   //安装最新版本的
brew install usbmuxd --HEAD    //安装最新版本的usb连接
brew install ideviceinstaller        //安装ideviceinstaller，ideviceinstaller命令在其bin目录下。
在/usr/local/Cellar/libimobiledevice/
一直出现错误Could not connect to lockdownd. Exiting.，使用第三种方法解决了（https://www.cnblogs.com/lily-20141202/p/10404377.html）

一.  ideviceinstaller命令
      1. ideviceinstaller -u [udid] -i [xxx.ipa]    //给指定连接的设备安装应用
      2. ideviceinstaller -u [udid] -U [bundleId]  //给指定连接的设备卸载应用
      3. ideviceinstaller [-u udid] -l                   // 指定设备，查看安装的第三方应用
      4. ideviceinstaller [-u udid] -l -o list_user      //指定设备，查看安装的第三方应用
      5. ideviceinstaller [-u udid] -l -o list_system    //指定设备，查看安装的系统应用
      6. ideviceinstaller  [-u udid] -l -o list_all       //指定设备，查看安装的系统应用和第三方应用

二.  其他命令
      1. idevicescreenshot /Users/lijie/Downloads/1.png   //截屏保存到该目录的1.png
      2. ideviceinfo     //获取手机的所有信息
      3. idevicedate   //获取手机时间
      4. idevicediagnostics restart    //重启手机
      5. idevicesyslog     //获取手机上所有日志
```

