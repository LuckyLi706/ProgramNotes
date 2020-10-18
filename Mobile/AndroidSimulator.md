# 模拟器

## 连接模拟器

```
1、逍遥模拟器
      连接：adb connect 127.0.0.1:21503

2、网易MuMu模拟器（官网：http://mumu.163.com/index.html）
      连接：adb connect 127.0.0.1:7555

3、蓝叠模拟器
      连接：adb connect 127.0.0.1:5555

4、手机模拟大师模拟器（官网：http://g.ludashi.com/）
      连接：adb connect 127.0.0.1:9974
      （手机1端口是9974，手机2在手机1 的基础上加10，手机3在手机2的基础上加10）

5、天天模拟器
      连接：adb connect 127.0.0.1:6555

6、51模拟器（官网：https://www.51mnq.com/）
      连接：adb connect 127.0.0.1:5555
      （多开的模拟器都有一个端口，第一个是5555，第二个是10001，第三个10006，第四个10011）

7、雷电模拟器
      连接：adb connect 127.0.0.1:5555

8、genymontion模拟器（ARM包 https://blog.csdn.net/GHY2016/article/details/83422620）
       选择自己的安卓SDK目录（通过模拟器上面的可以看到ip，通过ip进行连接）

       直接adb shell

9、夜神(Nox)模拟器
      连接：adb connect 127.0.0.1:62001

10、海马玩模拟器
      连接：adb connect 127.0.0.1:26944
      Windows 版，0.8.5 及以前的版本，默认端口号：53001
      Windows 版，0.8.6 及以后的版本，默认端口号：26944

11、iTools模拟器
       连接：adb connect 127.0.0.1:62001
```

## [模拟器、仿真器、虚拟设备和虚拟机的区别](https://github.com/imknown/IMKDevelopmentDaily/blob/master/2016/08/25_%E6%A8%A1%E6%8B%9F%E5%99%A8%E3%80%81%E4%BB%BF%E7%9C%9F%E5%99%A8%E3%80%81%E8%99%9A%E6%8B%9F%E8%AE%BE%E5%A4%87%E5%92%8C%E8%99%9A%E6%8B%9F%E6%9C%BA%E7%9A%84%E5%8C%BA%E5%88%AB.md)

## [模拟器介绍](https://github.com/imknown/IMKDevelopmentDaily/blob/master/2016/06/10_Android%20Emulator%20on%20Windows.md)

## 检测模拟器

[针对QEMU, KVM, QEMU-KVM 和 Goldfish的理解](https://blog.csdn.net/span76/article/details/19165345)

```
夜神（NOX）基于vbox
最新夜神手机检测不到/system/bin/nox-prop文件以及data/data下的文件名，猜测对这些文件做了权限限制。读取不到。
文件目录对部分有权限的获取（比如sd卡目录的部分特有文件）
检测目录：/storage/emulated/legacy/BigNoxHD, /lib/libnoxd.so,/lib/libnoxspeedup.so,
            /data/property/persist.nox.androidid, system/app/Helper/NoxHelp_zh.apk", /data/dalvik-cache/profiles/com.bignox.app.store.hd
检测包名：com.bignox.google.installer, com.bignox.app.store.hd

51（51模拟器）基于BlueStacks内核（检测基于BlueStacks做进一步检测）
检测目录：/.51services,/51共享文件夹,/storage/sdcard/windows/..

逍遥模拟器（官网 http://www.xyaz.cn/）
检测目录：/data/data/com.microvirt.launcher,/data/data/com.microvirt.tools, /data/data/com.microvirt.installer
检测包名：com.microvirt.market, com.microvirt.launcher, com.microvirt.installer

蓝叠模拟器（官网https://www.bluestacks.cn/ 两个安卓系统版本一个安卓4.4.2，一个安卓7.1）
和夜神一样，猜测对某些文件做了权限限制，一些配置文件。读取不到。(data/data目录以及system目录读取不到)
4.4.2和7.1版本
测录：/sdcard/Android/data/com.bluestacks.home,/sdcard/Android/data/com.bluestacks.settings, /sdcard/windows/BstSharedFolder
检测包名：com.bluestacks.appmart, com.bluestacks.settings

网易MuMu模拟器（官网http://mumu.163.com/ win版本和mac版本）
检测目录：/data/data/com.mumu.launcher, /data/data/com.mumu.store,/data/data/com.netease.mumu.cloner
检测包名：com.mumu.store, com.mumu.launcher, com.mumu.audio
sensor有Nemu特征

天天模拟器（官网http://www.ttmnq.com/）基于vbox
检测目录：/data/data/com.tiantian.ime,/system/priv-app/TianTianLauncher/TianTianLauncher.apk,/init.ttVM_x86.rc
未对相关系统文件做限制，所以判断依据较多。慢慢整理。
检测包名：com.tiantian.ime
sensor有TiantianVM特征

雷电模拟器（官网http://www.ldmnq.com/）基于vbox
检测目录：/sdcard/ldAppStore, /system/app/ldAppStore/ldAppStore.apk

Genymotion模拟器（官网https://www.genymotion.com/） 基于vbox
检测目录：/data/data/com.google.android.launcher.layouts.genymotion,/system/app/GenymotionLayout/GenymotionLayout.apk, /dev/socket/baseband_genyd
检测包名：com.genymotion.superuser
sensor有Genymotion特征

Xamarin.Android（VS的一款安卓模拟器）基于vbox

鲁大师模拟器（基于vbox）
检测目录：/ldsboxshare, /init.ludashi.rc",/init.ludashi.sh

原生模拟器
检测目录：/sys/module/goldfish_audio,/sys/module/goldfish_sync,

//其他模拟器（）
桌面安卓模拟器：
凤凰 os（http://www.phoenixos.com/）
remix os（https://www.resurrectionremix.com/）

Appetize
在线测试h5的Android和IOS模拟器

IOS模拟器
1、黑雷
2、果仁
```

