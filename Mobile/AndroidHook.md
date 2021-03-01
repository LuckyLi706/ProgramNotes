# Hook

## [Xposed](https://github.com/rovo89)

+ [XposedInstaller](https://github.com/rovo89/XposedInstaller)

   主要作为模块的一个容器，直接拉代码安装apk文件

+ [XposedBridge.jar]( https://github.com/rovo89/XposedBridge)

  + [各版本地址]( https://jcenter.bintray.com/de/robv/android/xposed/api/)

  用于编写模块的jar

### 编写Xposed模块

#### 配置

1. 关闭Android Studio的 Instant Run

   ```
    File -> Settings -> Build, Execution, Deployment -> Instant Run
   ```

2. 下载XposedBridge.jar

3.  gradle配置

   ```groovy
   dependencies {
       provided  fileTree(include: ['*.jar'], dir: 'libs')   //需要修改成provided,目前推荐compileOnly
       implementation 'com.android.support:appcompat-v7:28.0.0'
       implementation 'com.android.support.constraint:constraint-layout:1.1.3'
       testImplementation 'junit:junit:4.12'
       androidTestImplementation 'com.android.support.test:runner:1.0.2'
       androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
       provided  files('libs/XposedBridgeApi-54.jar')      //需要修改成provided,目前推荐compileOnly
   }
   ```

4. 新建assets资源文件夹，新建名为xposed_init文件，内容填写完整的执行Hook的类名（包含包名）

5. AndroidManifest.xml配置（写在applicaton标签内即可）

   ```xml
   <application
       android:allowBackup="true"
       android:icon="@mipmap/ic_launcher"
       android:label="@string/app_name"
       android:roundIcon="@mipmap/ic_launcher_round"
       android:supportsRtl="true"
       android:theme="@style/AppTheme">
       <!--true表示作为一个Xposed模块-->
       <meta-data
           android:name="xposedmodule"    
           android:value="true" />
       <!--展示在Xposed内的模块描述-->
       <meta-data
           android:name="xposeddescription"
           android:value="入门教程" />
       <!--支持的最低版本-->
       <meta-data
           android:name="xposedminversion"
           android:value="54" />
       <activity android:name=".MainActivity">
           <intent-filter>
               <action android:name="android.intent.action.MAIN" />
               <category android:name="android.intent.category.LAUNCHER" />
           </intent-filter>
       </activity>
   </application>
   ```

6. 编写Hook类

   ```java
   public class XMoudle implements IXposedHookLoadPackage {
       @Override
       public void handleLoadPackage(XC_LoadPackage.LoadPackageParam loadPackageParam) throws Throwable {
           if(loadPackageParam.packageName.equals("com.jacky.hook")){   //过滤包名表示只hook本应用
        XposedBridge.log("XLZH " + loadPackageParam.packageName);  //打印日志,在Xposed中可以观察日志
        XposedHelpers.findAndHookMethod(TelephonyManager.class, "getDeviceId", new XC_MethodReplacement() {
                   @Override
                   protected Object replaceHookedMethod(MethodHookParam methodHookParam) throws Throwable {
                       return "this is imei";
                   }
               });
               XposedHelpers.findAndHookMethod(TelephonyManager.class, "getSubscriberId", new XC_MethodReplacement() {
                   @Override
                   protected Object replaceHookedMethod(MethodHookParam methodHookParam) throws Throwable {
                       return "this is imsi";
                   }
               });
           }
       }
   }
   ```

#### Xposed修改参数代码

```java
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getDeviceId", GetCatValue("imei"));
HTool.XHookMethod("com.android.internal.telephony.PhoneSubInfo",mLpp.classLoader, "getDeviceId", GetCatValue("imei"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSubscriberId", GetCatValue("imsi"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getLine1Number", GetCatValue("number"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSimSerialNumber", GetCatValue("simserial"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSimCountryIso", GetCatValue("simcountryiso"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSimOperator", GetCatValue("simoperator"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSimOperatorName", GetCatValue("simoperatorname"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getNetworkCountryIso", GetCatValue("networkcountryiso"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getNetworkOperator", GetCatValue("networkoperator"));
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getNetworkOperatorName", GetCatValue("networkoperatorname"));
 
//WIFI信息
HTool.XHookMethod(android.net.wifi.WifiInfo.class.getName(),mLpp.classLoader, "getMacAddress", GetCatValue("wifimac"));
HTool.XHookMethod(android.net.wifi.WifiInfo.class.getName(),mLpp.classLoader, "getBSSID", GetCatValue("bssid"));
HTool.XHookMethod(android.net.wifi.WifiInfo.class.getName(),mLpp.classLoader, "getSSID", "\""+GetCatValue("ssid")+"\"");
XposedHelpers.findAndHookMethod(java.net.NetworkInterface.class.getName(),mLpp.classLoader, "getHardwareAddress", new Object[] {
        new XC_MethodHook()
        {
            protected void afterHookedMethod(MethodHookParam param) throws Throwable
            {
                //每个安卓系统中 至少存在5个以上的MAC地址 
                //但大多数软件只修改了MAC和BSSID 
                //真正的MAC修改是在此处理函数中监听每次访问.
            }
        }});
         
//蓝牙信息
HTool.XHookMethod(BluetoothAdapter.class.getName(),mLpp.classLoader,"getAddress", GetCatValue("bluemac"));
HTool.XHookMethod(BluetoothAdapter.class.getName(),mLpp.classLoader, "getName", GetCatValue("bluename"));
 
//设置手机信息 无论手机是否插入了sim卡 都会模拟出SIM卡的信息 APP获得SIM卡消息时返回该手机已有SIM卡
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getPhoneType", TelephonyManager.PHONE_TYPE_GSM);
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getNetworkType", TelephonyManager.NETWORK_TYPE_HSPAP);
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "getSimState", TelephonyManager.SIM_STATE_READY);
HTool.XHookMethod(android.telephony.TelephonyManager.class.getName(),mLpp.classLoader, "hasIccCard", true);
 
     
//修改手机系统信息 此处是手机的基本信息 包括厂商 信号 ROM版本 安卓版本 主板 设备名 指纹名称等信息
XposedHelpers.setStaticObjectField(android.os.Build.class, "MODEL", GetCatValue("model"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "MANUFACTURER", GetCatValue("manufacturer"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "BRAND", GetCatValue("brand"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "HARDWARE", GetCatValue("hardware"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "BOARD", GetCatValue("board"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "SERIAL", GetCatValue("serial"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "DEVICE", GetCatValue("device"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "ID", GetCatValue("id"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "PRODUCT", GetCatValue("product"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "DISPLAY", GetCatValue("display"));
XposedHelpers.setStaticObjectField(android.os.Build.class, "FINGERPRINT", GetCatValue("fingerprint"));
 
XposedHelpers.findAndHookMethod("android.os.SystemProperties",mLpp.classLoader, "native_get", new Object[] {String.class,String.class,
        new XC_MethodHook()
        {
            //为了防止某些APP跳过Build类 而直接使用SystemProperties.native_get获得参数
        }});
//修改系统版本 我看到世面上的软件基本上都是不能修改系统版本的 从而造成了刷量后 很多渠道最终会显示你的APP用户全部使用的某一系统版本
//这样的话数据就太假了.
XposedHelpers.setStaticObjectField(android.os.Build.VERSION.class, "RELEASE", GetCatValue("version"));
XposedHelpers.setStaticObjectField(android.os.Build.VERSION.class, "SDK", GetCatValue("apilevel"));
 
HTool.XHookMethod(android.os.Build.class.getName(),mLpp.classLoader, "getRadioVersion", GetCatValue("radioversion"));
 
//修改为指定的运营商mnc mcc信息
XposedHelpers.findAndHookMethod(android.content.res.Resources.class.getName(),mLpp.classLoader, "getConfiguration", new Object[] {
        new XC_MethodHook()
        {
            ...........................
            //此处的mnc和mcc必须和系统中其他关于运营商的数据对应!
        }});
 
//修改ANDROID_ID
XposedHelpers.findAndHookMethod(android.provider.Settings.Secure.class.getName(),mLpp.classLoader, "getString",
new Object[] {ContentResolver.class,String.class,
        new XC_MethodHook()
        {
            ...............................
            //此处会根据传入的String参数 判断返回值 其中包括比较关键的数据就是android_id
        }});
 
//防止APP使用Runtime.exec方式获取一些特定的系统属性
XposedHelpers.findAndHookMethod(Runtime.class.getName(),mLpp.classLoader, "exec",new Object[] {String.class,String[].class, File.class,
        new XC_MethodHook()
        {
            //一些APP从JAVA层获得到了数据 还会从shell(native)层获得一些更底层的数据 来判断用户的合法性
            //经常用到的有 cat、getprop、ifconfig等等命令，当exec执行这些命令后 往往会返回一些手机的真实信息
            //因为框架和处理方式不同，...部分此处根据自己需求，编写重定向返回值的过程...
        }});
 
//修改位置信息
XposedHelpers.findAndHookMethod(LocationManager.class.getName(),mLpp.classLoader, "getLastKnownLocation",
    new Object[] {String.class,
            new XC_MethodHook()
            {
                ..........................
                //返回预先设置好的经纬度信息以伪装地理位置
            }});
 
HTool.XHookMethod(Location.class.getName(),mLpp.classLoader, "getLatitude", latitude);
HTool.XHookMethod(Location.class.getName(),mLpp.classLoader, "getLongitude", longitude);
 
 
//修改GSM制式手机的基站信息
HTool.XHookMethod(android.telephony.gsm.GsmCellLocation.class.getName(),mLpp.classLoader, "getLac", GsmLac);
HTool.XHookMethod(android.telephony.gsm.GsmCellLocation.class.getName(),mLpp.classLoader, "getCid", GsmCid);
 
 
//修改CDMA制式手机的基站信息
HTool.XHookMethod(android.telephony.cdma.CdmaCellLocation.class.getName(),mLpp.classLoader, "getBaseStationLatitude", CdmaLatitude);
HTool.XHookMethod(android.telephony.cdma.CdmaCellLocation.class.getName(),mLpp.classLoader, "getBaseStationLongitude", CdmaLongitude);
HTool.XHookMethod(android.telephony.cdma.CdmaCellLocation.class.getName(),mLpp.classLoader, "getBaseStationId", CdmaBid);
HTool.XHookMethod(android.telephony.cdma.CdmaCellLocation.class.getName(),mLpp.classLoader, "getSystemId", CdmaSid);
HTool.XHookMethod(android.telephony.cdma.CdmaCellLocation.class.getName(),mLpp.classLoader, "getNetworkId", CdmaNid);
 
 
//模拟手机的APP列表
XposedHelpers.findAndHookMethod("android.app.ApplicationPackageManager",mLpp.classLoader, "getInstalledPackages",new Object[] {int.class,
        new XC_MethodHook()
        {
            //此处模拟正常用户的APP列表 其中随机的增加和删除一些常用APP 以达到每个手机的APP有很大的随意性和合理性
        }});
 
XposedHelpers.findAndHookMethod("android.app.ApplicationPackageManager",mLpp.classLoader, "getInstalledApplications",new Object[] {int.class,
        new XC_MethodHook()
        {
            //此处模拟正常用户的APP列表 其中随机的增加和删除一些常用APP 以达到每个手机的APP有很大的随意性和合理性
        }});
         
//防止APP的VPN SOCK5 HTTP代理检测
XposedHelpers.findAndHookMethod(java.net.NetworkInterface.class.getName(),mLpp.classLoader, "getNetworkInterfacesList",new Object[] {
        new XC_MethodHook()
        {
            ........................................
            //此处对于一些连接信息 对JAVA做了隐藏处理 但对于系统和Native层依然是可见的 所以APP不会检测到代理 但代理却可以正常的运行...
        }});
```

#### 错误集锦

```
1.Caused by: java.lang.NoClassDefFoundError: Class not found using the boot class loader; no stack trace available
       解决：File -> Settings -> Build, Execution, Deployment -> Instant Run关闭Android Studio的 Instant Run

2.The Xposed API classes are compiled into the module's APK
        解决：
   .provided  fileTree(include: ['*.jar'], dir: 'libs')   //需要修改成provided,目前推荐compileOnly
    provided  files('libs/XposedBridgeApi-54.jar')      //需要修改成provided,目前推荐compileOnly
    （如果使用compile，api库的classes将会被打包到apk中，会导致bug，特别是在Android 4.x设备上。使用provided只是让module可以通过编译，在apk中只有对api的引用）
```

### Xposed插件

+ [Xposed钉钉打卡](https://github.com/wuxiaosu/XposedRimetHelper)
+ [跳过https校验](xposed_apk/JustTrustMe.apk)
+ [进行webview强行调试](xposed_apk/WebViewDebugHook.apk)
+ [微信修改](https://github.com/wuxiaosu/XposedWechatHelper)

### Magisk

+ [高版本root和使用xposed的神器](https://github.com/topjohnwu/Magisk)
+ [Magisk刷机包下载地址](https://github.com/topjohnwu/Magisk/releases)
+ [Magisk版Xposed地址](https://forum.xda-developers.com/xposed/unofficial-systemless-xposed-t3388268)

### VisualXposed

+ [在非ROOT环境下运行Xposed模块的实现](https://github.com/android-hacker/VirtualXposed/blob/vxp/CHINESE.md)
+ [太极](https://github.com/taichi-framework/TaiChi/wiki/FAQ)

## [Cydia Substrate](http://www.cydiasubstrate.com/)

Cydia Substrate（非开源，Hook native层代码较好）

+ [例子](http://www.cydiasubstrate.com/id/38be592b-bda7-4dd2-b049-cec44ef7a73b/)

## [Firda](https://github.com/frida)

Frida是一款基于python + javascript 的hook框架，通杀android\ios\linux\win\osx等各平台，基于脚本的交互

+ [例子](https://www.jianshu.com/p/ca8381d3e094)