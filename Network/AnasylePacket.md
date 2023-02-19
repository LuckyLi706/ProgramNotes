# 抓包

## 客户端配置

### Android

#### Charles

1. 安装Charles软件
2. 如果只想抓取手机端的包，在Charles中去掉勾选Proxy -> Windows Proxy（Mac是macOS Proxy），默认都是开启的。
3. 选择Proxy -> Proxy Settings，HTTP Proxy下面两个都勾选。查看当前监听的端口号。
4. 选择Proxy -> SSL Proxy Setting，添加Location，在Host输入自己要抓包的域名；如果想看所有抓包情况，Host中输入\*，Port中输入\*；或者只过滤https的，可以在Host中输入\*，Port中输入443
5. 最后手机设置代理，长按当前Wifi名；高级选项 -> 代理 ->  手动 ，然后输入ip和监听的端口号。然后在手机浏览器中输入http://chls.pro/ssl去下载安装证书。

#### 问题点总结

+ 安卓7.0以上部分模拟器无法代理抓包的问题（在高级选项中的代理设置无效 ，比如雷电4.0）

  + 方案一：安装ProxyDroid app，然后打开app去配置全局代理

  + 方案二：使用adb 命令设置全局代理

    ```
    adb shell settings get global http_proxy   //获取当前手机的代理信息
    adb shell settings put global http_proxy 172.20.10.4:8888   //设置当前手机的代理为172.20.10.4:8888
    adb shell settings delete global http_proxy   //删除当前手机的所有代理信息
    ```

+ 关于https证书的安装（7.0以上默认不信任用户的证书，必须要把代理证书移动到系统目录下）

  - 方案一（需要root）：

    1. 先安装证书

       ```
       Charles：
       在手机浏览器中输入http://chls.pro/ssl，然后下载证书，直接在手机上面安装。
       
       小黄鸟（HttpCanary App）：
       打开App，然后设置 -> SSL证书设置 -> 安装HttpCanary根证书
       ```

    2. 进入/data/misc/user/0/cacerts-added目录，这就是用户证书的目录，然后找到你刚才安装的证书（可能有多个.0后缀的证书，可以根据时间来找，或者全部删除重新安装一次），然后将其移动到/system/etc/security/cacerts/目录下。

       ```
       //出现 Read-only file system的问题解决:
       adb root
       adb remount rw /system   //重新挂载让系统目录有读写权限
       ```

  - 方案二（需要root）

    1. 从抓包软件中导出证书

       ```
       Charles：
       Help -> SSL Proxying -> Save Charles Root Certificate 导出pem文件到电脑上
       
       小黄鸟（HttpCanary App）：
       打开App，然后设置 -> SSL证书设置 -> 安装HttpCanary根证书，类型System Trusted (.0) 导出位置在/sdcard/HttpCanary/cert文件夹下面
       ```

    2. 使用[OpenSSL](https://so.csdn.net/so/search?q=OpenSSL&spm=1001.2101.3001.7020)工具来修改证书文件名（Mac/Linux自带这个工具，Windows需要下载）

       ```
       //根据导出的证书类型来执行
       
       1、cer证书转pem
       openssl x509 -inform der -in FiddlerRoot.cer -out file.pem
       
       2、获取pem证书hash（执行完会生成一个hash值）
       openssl x509 -subject_hash_old -in file.pem
       
       3、将file.pem重新命名为hash.0文件
       ```

    3. 将hash.0文件导入到/system/etc/security/cacerts/目录下。

  - 方案三（不要root）

    待完善

    1. 在手机中开启一个虚拟机，可以开启root和使用Xposed插件（如VMOS PRO，[VirtualXposed](https://github.com/android-hacker/VirtualXposed)，[太极](https://github.com/android-hacker/exposed)）
    2. xp插件关闭SSL验证：[ustTrustMe](https://github.com/Fuzion24/JustTrustMe)、JustMePlush、 [TrustMeAlready](https://github.com/ViRb3/TrustMeAlready)

+ Android Studio自带模拟器开启代理抓包

  ```shell
  # 使用如下命令启动模拟器
  # -writable-system 参数表示让系统可以写入，不然挂载不了
  # -http-proxy 参数表示设置当前模拟器的代理
  emulator -avd 模拟器名字 -writable-system -http-proxy http://127.0.0.1:8888 
  ```

+ 安卓7.0以上添加配置文件抓取https（针对自己开发调试的app，当然也可以反编译别人的app加入以下配置）

  1. 在res/xml中新建文件 network_security_config.xml

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <network-security-config>
         <!-- 支持 Android 9.0 以上使用部分域名时使用 http -->
         <domain-config cleartextTrafficPermitted="true">
             <domain includeSubdomains="true">sample.domain</domain>
         </domain-config>
         <!-- 支持 Android 7.0 以上调试时，信任 Charles 和 Fiddler 等用户信任的证书 -->
         <base-config cleartextTrafficPermitted="true">
             <trust-anchors>
                 <certificates src="system" />
                 <certificates src="user" />
             </trust-anchors>
         </base-config>
     </network-security-config>
     ```

  2. 在AndroidManifest.xml中的application里面添加如下配置

     ```xml
     android:networkSecurityConfig="@xml/network_security_config"
     ```

### IOS

#### Charles

1. 安装Charles软件
2. 如果只想抓取手机端的包，在Charles中去掉勾选Proxy -> Windows Proxy（Mac是macOS Proxy），默认都是开启的。IOS模拟器如果关闭了这个选项，需要手动去设置代理，不然证书下载不了（见Mac手动设置代理）。
3. 选择Proxy -> Proxy Settings，HTTP Proxy下面两个都勾选。查看当前监听的端口号。
4. 选择Proxy -> SSL Proxy Setting，添加Location，在Host输入自己要抓包的域名；如果想看所有抓包情况，Host中输入\*，Port中输入\*；或者只过滤https的，可以在Host中输入\*，Port中输入443
5. 
   + IOS 模拟器
     + 注意点：Help -> SSL Proxying -> Install Charles Root Certificate in IOS Simulators 这个选项没效果，依然抓不到https的包
     + 直接在浏览器中输入http://chls.pro/ssl去下载安装证书。然后在Settings -> General -> About -> Profile 里面去安装证书
     + 最后在Settings -> General -> About -> Certificate Trust Settings中勾选证书。
   + IOS 真机
     + 手机设置代理，点击连接网络的详细信息；配置代理 ->  手动 ，然后输入ip和监听的端口号。然后在手机浏览器中输入http://chls.pro/ssl去下载安装证书。
     + 然后在设置-> 通用-> 关于-> 描述文件  里面去安装证书
     + 需要到iPhone设置 -> 关于本机 -> 证书信任设置中启用根证书 

#### Stream（App）

1. 打开Stream App，选择HTTPS抓包，然后点击安装CA证书
2. 弹出添加VPN配置，选择允许，输入密码，在设置 -> 通用 -> VPN与设备管理 -> VPN -> 选择Stream，状态选择连接
3. 再次打开Stream App，选择HTTPS抓包，点击安装CA证书，需要去下一个配置描述文件
4. 在设置 -> 通用 -> VPN与设备管理 中多个一个已下载的描述文件，点进去安装。
5. 最后在设置 -> 通用 -> 关于本机 -> 证书信任设置 把Stream开头的选项打开。然后就可以抓到https的包了。

### Mac

#### Charles

1. 配置Charles证书；选择Help -> SSL Proxying -> install Charles Root Certificate
2. 会自动导入 Charles Proxy CA 证书并打开 Keychain Access，双击新导入的证书弹出证书信息页面，将 Secure Sockets Layer(SSL) 设置为 Always Trust，关闭页面后弹出密码提示，输入密码更新系统信任设置。
3. 然后在Charles中勾选Proxy -> macOS Proxy（这个默认打开了）
4. 最后选择Proxy -> SSL Proxy Setting，添加Location，在Host输入自己要抓包的域名；如果想看所有抓包情况，Host中输入\*，Port中输入\*；或者只过滤https的，可以在Host中输入\*，Port中输入443

#### 问题点总结

+ 如果浏览器还是不能抓https的包，试试下面的方案
  1. 直接在浏览器访问chls.pro/ssl ，去下载证书，
  2. 导入浏览器证书，这里以Chrome浏览器为例，打开设置—高级—管理证书，然后导入
  3. 和工具端一样，将证书存储到“受信任的根证书颁发机构”下，后面直接下一步即可
+ 如果不能抓Chrome的包，可以下载安装Chrome插件[switch sharp](https://www.crx4chrome.com/crx/543/)，手动设置代理
+ 手动设置代理，系统设置 -> 网络 -> 代理 -> Web Proxy和Secure Proxy都设置代理

### Windows

#### Charles

1. 配置Charles证书；选择Help -> SSL Proxying -> install Charles Root Certificate
2. 会出现证书安装的信息，选择安装证书
3. 证书导入，选择本地计算机
4. 将证书安装在“受信任的根证书颁发机构”
5. 然后在Charles中勾选Proxy -> Windows Proxy（这个默认打开了）
6. 最后选择Proxy -> SSL Proxy Setting，添加Location，在Host输入自己要抓包的域名；如果想看所有抓包情况，Host中输入\*，Port中输入\*；或者只过滤https的，可以在Host中输入\*，Port中输入443

#### 问题点总结

+ 如果浏览器还是不能抓https的包，试试下面的方案
  1. 直接在浏览器访问chls.pro/ssl ，去下载证书，
  2. 导入浏览器证书，这里以Chrome浏览器为例，打开设置—高级—管理证书，然后导入
  3. 和工具端一样，将证书存储到“受信任的根证书颁发机构”下，后面直接下一步即可
+ 如果不能抓Chrome的包，可以下载安装Chrome插件[switch sharp](https://www.crx4chrome.com/crx/543/)，手动设置代理
+ 手动设置代理，设置 -> 网络和Internet -> 使用代理服务器

## 抓包工具

### Flidder（支持全平台）

+ [使用教程](https://www.oschina.net/p/fiddler?hmsr=aladdin1e1)
+ [修改请求和回复数据](https://www.cnblogs.com/kristin/p/8445055.html)
+ [Fiddler抓包和修改WebSocket数据，支持wss](https://blog.csdn.net/weixin_30947043/article/details/97329308)

### Charles（支持全平台）

+ 注册码

  注册用户名: https://zhile.io
  注册码    : 48891cf209c6d32bf4

+ [入门篇](https://www.52pojie.cn/thread-1468565-1-1.html)

### HttpCanary（小黄鸟，只支持安卓）

### Stream（只支持IOS）

### whistle

whistle 是一款用 Node 实现的跨平台的 Web 调试代理工具

+ [github地址](https://github.com/avwo/whistle)
+ [官方文档](http://wproxy.org/whistle/)

```
//1、安装
npm install -g whistle

//2、启动和停止
w2 start/w2 stop

//3、打开
使用浏览器打开http://127.0.0.1:8899/界面
```

### Wireshark

+ [Https详解+wireshark抓包演示](https://www.jianshu.com/p/a3a25c6627ee)
+ [Wireshark解密HTTPS流量的两种方法，最新版ssl改成tls](https://www.cnblogs.com/yurang/p/11505741.html)
+ [wireshark 实用过滤表达式（针对ip、协议、端口、长度和内容）](https://www.cnblogs.com/softidea/p/10446388.html)

+ https://apkpure.com/cn/packet-capture/app.greyshirts.sslcapture)

### tcpdump

tcpdump是Linux系统中普遍使用的一款开源网络协议分析工具

+ [安卓的tcpdump下载地址](https://www.androidtcpdump.com/android-tcpdump/downloads)

```
//linux
-a 　　　将网络地址和广播地址转变成名字；
-d 　　　将匹配信息包的代码以人们能够理解的汇编格式给出；
-dd 　　　将匹配信息包的代码以c语言程序段的格式给出；
-ddd 　　　将匹配信息包的代码以十进制的形式给出；
-e 　　　在输出行打印出数据链路层的头部信息，包括源mac和目的mac，以及网络层的协议；
-f 　　　将外部的Internet地址以数字的形式打印出来；
-l 　　　使标准输出变为缓冲行形式；
-n 　　　指定将每个监听到数据包中的域名转换成IP地址后显示，不把网络地址转换成名字；
-nn：    指定将每个监听到的数据包中的域名转换成IP、端口从应用名称转换成端口号后显示
-t 　　　在输出的每一行不打印时间戳；
-v 　　　输出一个稍微详细的信息，例如在ip包中可以包括ttl和服务类型的信息；
-vv 　　　输出详细的报文信息；
-c 　　　在收到指定的包的数目后，tcpdump就会停止；
-F 　　　从指定的文件中读取表达式,忽略其它的表达式；
-i 　　　指定监听的网络接口；
-p    将网卡设置为非混杂模式，不能与host或broadcast一起使用
-r 　　　从指定的文件中读取包(这些包一般通过-w选项产生)；
-w 　　　直接将包写入文件中，并不分析和打印出来；
-s snaplen         snaplen表示从一个包中截取的字节数。0表示包不截断，抓完整的数据包。默认的话 tcpdump 只显示部分数据包,默认68字节。
-T 　　　将监听到的包直接解释为指定的类型的报文，常见的类型有rpc （远程过程调用）和snmp（简单网络管理协议；）
-X            告诉tcpdump命令，需要把协议头和包内容都原原本本的显示出来（tcpdump会以16进制和ASCII的形式显示），这在进行协议分析时是绝对的利器

//android（必须root）
1、push到手机的/data/local/tmp
2、chmod 6755 /data/local/tcpdump
3、/data/local/tcpdump -p -vv -s 0 -w /sdcard/capture.pcap  //生成分析文件
4、使用wireshark打开分析
```

