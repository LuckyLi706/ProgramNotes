<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [抓包](#%E6%8A%93%E5%8C%85)
  - [Flidder](#flidder)
  - [Charles](#charles)
  - [Proxyman](#proxyman)
  - [whistle](#whistle)
  - [Wireshark](#wireshark)
  - [Packet Capture](#packet-capture)
  - [tcpdump](#tcpdump)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 抓包

## Flidder

+ [使用教程](https://www.oschina.net/p/fiddler?hmsr=aladdin1e1)

+ [修改请求和回复数据](https://www.cnblogs.com/kristin/p/8445055.html)

+ [Fiddler抓包和修改WebSocket数据，支持wss](https://blog.csdn.net/weixin_30947043/article/details/97329308)

+ 安卓7.0以上抓取https（7.0以上默认不信任用户的证书）

  - 在res/xml中新建文件 network_security_config.xml
  
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
    //创建完后，在androidManifest.xml中的application里面写：
    android:networkSecurityConfig="@xml/network_security_config"
    ```
  
  - 移动代理证书到系统目录下（需要root权限）
  
    将证书移动到/system/etc/security/cacerts/目录下

## Charles

个人感觉比较好看，支持Windows、Mac，但是要收费

+ [入门篇](https://www.52pojie.cn/thread-1468565-1-1.html)

## Proxyman
只支持Mac系统下安装,可以抓Android和IOS
+ [下载地址](https://proxyman.io/)

## whistle

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

## Wireshark

+ [Https详解+wireshark抓包演示](https://www.jianshu.com/p/a3a25c6627ee)
+ [Wireshark解密HTTPS流量的两种方法，最新版ssl改成tls](https://www.cnblogs.com/yurang/p/11505741.html)
+ [wireshark 实用过滤表达式（针对ip、协议、端口、长度和内容）](https://www.cnblogs.com/softidea/p/10446388.html)

+ https://apkpure.com/cn/packet-capture/app.greyshirts.sslcapture)

## tcpdump

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

