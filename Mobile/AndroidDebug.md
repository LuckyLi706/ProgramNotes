# Debug

## H5

### Chrome

```java
//webview加上以下代码
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
    if (0 != (getApplicationInfo().flags & ApplicationInfo.FLAG_DEBUGGABLE))
    {
        WebView.setWebContentsDebuggingEnabled(true);
    }
}
if (0 != (getApplicationInfo().flags & ApplicationInfo.FLAG_DEBUGGABLE))
    { 
    WebView.setWebContentsDebuggingEnabled(true); 
    }
}
```

通过 chrome://inspect 访问已启用调试的 WebView 列表即可。[官网地址](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/webviews?hl=zh-cn)

使用Hook该方法来强制调试第三方App内的原生页面的H5：[Xposed的模块](https://github.com/feix760/WebViewDebugHook)

### UC

+ [开发者网址](https://dev.ucweb.com/download/?spm=ucplus.11199946.home-card.1.53974692vNJMgU)

+ [调试说明](http://www.uc.cn/download/u4-developer_NEW.pdf)

### QQ浏览器、微信以及小程序和公众号

调试利器[TBS Studio](https://x5.tencent.com/tbs/guide/debug/download.html)

QQ浏览器需要下载开发版apk，连接studio会自动帮你下载

微信需要打开x5内核开关：微信访问http://debugx5.qq.com或者扫下面的二维码    

小程序：

（1）（2018.6.22~至今）只能查看搜一搜入口的小程序（从chrome-inspector上显示的搜一搜url试出来的）         

（2）（2018.6.22之前）所有入口均能显示小程序页面的url(下拉小程序;搜一搜；微信钱包)

[详细介绍](https://mp.weixin.qq.com/s/U0jFiRsVsChHb8K9995QKQ)

![img](images/android_debug_wechat.png)

### Firefox（火狐）

条件：

1. 一台运行着至少Firefox36或更新版本浏览器的桌面计算机或笔记本电脑，需要安卓ADB Helper插件

2. 一台 [支持运行 Firefox for Android](https://support.mozilla.org/en-US/kb/will-firefox-work-my-mobile-device) 的安卓设备，并且安装运行了 Firefox for Android 35 或更高版本，需要打开远程调试开关，设置----开发者工具

3. 两台设备使用USB连接起来

​       [大于36版本的](https://developer.mozilla.org/en-US/docs/Tools/Remote_Debugging/Debugging_Firefox_for_Android_with_WebIDE)

​       [小于36版本的](https://developer.mozilla.org/en-US/docs/Tools/Remote_Debugging/Firefox_for_Android)

### 百度

同Chrome浏览器

### 其他调试方案

+ [spy-debugger](https://github.com/wuchangming/spy-debugger)

+ [vConsole](https://github.com/Tencent/vConsole/blob/dev/README_CN.md)