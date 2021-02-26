# IDA Pro

## 简介

+ [7.0各平台版本下载地址](https://www.52pojie.cn/thread-675251-1-1.html)

+ [各种动态调试server含义（dbgsrv目录下）](解释地址：https://www.hex-rays.com/products/ida/support/idadoc/1463.shtml)

  | File name          | Target system                       | Debugged programs   |
  | ------------------ | ----------------------------------- | ------------------- |
  | android_server     | RM Android                          | 32-bit ELF files    |
  | android_server64   | AArch64 Android    64-bit ELF files | 64-bit ELF files    |
  | android_x64_server | 86 Android 32-bit 32-bit ELF files  | 32-bit ELF files    |
  | android_x86_server | x86 Android 64-bit                  | 64-bit ELF files    |
  | armlinux_server    | ARM Linux                           | 32-bit ELF files    |
  | linux_server       | Linux 32-bit                        | 32-bit ELF files    |
  | linux_server64     | Linux 64-bit                        | 64-bit ELF files    |
  | mac_server         | Mac OS X                            | 32-bit Mach-O files |
  | mac_server64       | Mac OS X                            | 64-bit Mach-O files |
  | win32_remote.exe   | MS Windows 32-bit                   | 32-bit PE files     |
  | win64_remote64.exe | MS Windows 64-bit                   | 64-bit PE files     |

## 快捷键

```
#搜索函数
crtl+f

#将汇编代码转为c代码
F5（32位可以，64位不可以）

#跳转到目标地址
g

#调试将DCB转换为汇编代码
p

#Thumb16位和ARM32位切换
alt+g

#跳转到segment(段)
ctrl+s
```

## 安卓调试

### 启动式调试

```
1.push  
IDA 目录的android_server到手机的/data/local/tmp（调试arm使用真机最好）

2.启动服务端
chmod 777 android_server
./android_server

3.端口转发(IDA默认端口23946)
adb forward  tcp:23946 tcp:23946

4.IDA调试端口设置
 Debugger ----> Process Option ----> HostName:localhost Port:23946
 
5.以调试方式启动apk
adb shell am start -D -n package/.activitiyname

6.IDA挂接
Debugger ----> Attach to Process

7.jdb connect（需要先打开monitor，类似于java的调试）
jdb  -connect com.sun.jdi.SocketAttach:hostname=127.0.0.1,port=8700
```

