# 命令

## adb

pc端和Android端交互的命令工具，[详细命令地址](https://github.com/mzlogin/awesome-adb)

## aapt

对apk中使用的资源进行打包，aapt2在AS3.0出现的，在build-tools目录下

### 作用

+ 编译res目录xml文件
+ 编译AndroidManifest.xml
+ 生成R.java
+ 生成Resources.arsc

### 查看编译后的xml文件信息

- aapt d badging x.apk          //查看APK的相关描述(如包名、版本、label等)
- aapt d permissions x.apk    //查看APK的权限
- aapt d resources x.apk       //查看APK的Resources.arsc
- aapt d xmltree x.apk x.xml //查看编译后的XML文件(如AndroidManifest.xml)

### 编译xml文件

- aapt package [-d][-f][-m][-u][-v][-x][-z][-M AndroidManifest.xml]              
- -S    res目录         
- -M    AndroidManifest.xml路径    
- -A    assert目录    
- -I    android.jar路径    
- -J    R.java输出目录    
- -F    APK输出目录

### 生成R.java

+ aapt package -J R.java输出目录 -S res路径 -I android.jar路径 -M AndroidManifest.xml路径

## apksigner 

对APK进行v2签名。[v1和v2签名区别](https://blog.csdn.net/lxlmycsdnfree/article/details/80801719)

### v1签名（使用jdk）

```java
//jdk1.6
jarsigner -verbose -keystore android.keystore(签名证书文件) -signedjar enhanced_signed.apk(签名后的apk) enhanced.apk(签名前的apk) android.keystore(keystore别名)

//jdk1.7
jarsigner -digestalg SHA1 -sigalg MD5withRSA -keystore android.keystore -storepass(keystore密码) android -signedjar enhanced_sign.apk enhanced.apk android.keystore
```

### #v2签名（使用apksigner）

```java
apksigner sign --ks aoaoyi.jks --ks-key-alias aoaoyi --ks-pass pass:aoaoyi.com --key-pass pass:aoaoyi.com –out output.apk input.apk

apksigner sign                 //执行签名操作
--ks 你的jks路径               //jks签名证书路径
--ks-key-alias 你的alias    //生成jks时指定的alias
--ks-pass pass:你的密码           //KeyStore密码
--key-pass pass:你的密码          //签署者的密码，即生成jks时指定alias对应的密码
--out output.apk               //输出路径
input.apk                   //需要签名的APK
```

### 检查apk是否签名

```java
apksigner verify -v --print-certs xxx.apk

参数:
 -v, --verbose  //显示详情(显示是否使用V1和V2签名)
--print-certs   //显示签名证书信息
```

## dexdump

查看dex文件的指令代码，在build-tools目录下

```java
dexdump: [-c] [-d] [-f] [-h] [-i] [-l layout] [-m] [-t tempfile] dexfile(apk,zip ,jar格式)
-c : verify checksum and exit       //dex的adler32校验
-d : disassemble code sections    //展示所有字节码
-f : display summary information from file header 
-h : display file header details    //输出dex的Header结构
-i : ignore checksum failures 
-l : output layout, either ‘plain’ or ‘xml’ 
-m : dump register maps (and nothing else) 
-t : temp file name (defaults to /sdcard/dex-temp-*)
```

## sqlite3

```java
//介绍
sqlite3 为android所使用的轻量级数据库，管理各种db文件，

//进入sqlite数据库命令行
sqlite3 test.db

//显示数据库信息
.database

//查看表信息
.table

//查看表结构
.schema tableName 

//查看表数据
select * from tableName; 

//向表中添加新记录
insert  into  <table_name>  values (value1, value2,…);

//更新表中记录
update  <table_name>  set  <f1=value1>, <f2=value2>…   where  <expression>;  

//删除表
drop  table  <table_name>

#列出命令的提示信息
```

