# 调试

## H5

### Chrome调试手机Safari

[ios-webkit-debug-proxy](https://github.com/google/ios-webkit-debug-proxy/releases)

//手机的Safari已经Web检查器已经打开

```
使用windows：
下载对应的release包
执行ios_webkit_debug_proxy -f chrome-devtools://devtools/bundled/inspector.html

在chrome浏览其中打开 location:9221
可能出现的错误：
device_listener: connect function failed with        error 10061
No device found, is it plugged in?
下载Itunes，确保电脑和手机连上
Unable to attach abddec8eb6da9b05f07348cc4c82998d3584b55f inspector
好像是数据线没插紧
```

```
使用mac:
brew install ios-webkit-debug-proxy
ios_webkit_debug_proxy -f chrome-devtools://devtools/bundled/inspector.html

IOS12以上（详细查看github）
brew update
brew reinstall --HEAD usbmuxd
brew reinstall --HEAD libimobiledevice
brew reinstall -s ios-webkit-debug-proxy
可能出现的问题：
Could not connect to lockdownd. Exiting.: Permission denied
sudo chmod +x /var/db/lockdown
brew upgrade libimobiledevice --HEAD
```

### 调试微信以及其他浏览器

​    附件IPAPatch，替换Assets目录下的app.ipa，需要越狱后的ipa，重新打包签名，就可以使用

​    Safari浏览器调试了。

​    具体方法：

​    + http://jichaowu.com/2017/07/25/remote_debug/

​    2. http://www.cnblogs.com/imwtr/p/8675701.html



​    [IPAPatch](https://github.com/Naituw/IPAPatch)

   [Hook神器](https://github.com/AloneMonkey/MonkeyDev)