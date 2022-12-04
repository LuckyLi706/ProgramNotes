<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Flutter与原生方法交互](#flutter%E4%B8%8E%E5%8E%9F%E7%94%9F%E6%96%B9%E6%B3%95%E4%BA%A4%E4%BA%92)
  - [Android](#android)
    - [Flutter->Android](#flutter-android)
    - [Android->Flutter](#android-flutter)
  - [IOS](#ios)
  - [Windows](#windows)
  - [Mac](#mac)
  - [Linux](#linux)
  - [Web](#web)
- [Flutter使用原生View并且交互（View插件开发）](#flutter%E4%BD%BF%E7%94%A8%E5%8E%9F%E7%94%9Fview%E5%B9%B6%E4%B8%94%E4%BA%A4%E4%BA%92view%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91)
  - [Android](#android-1)
    - [WebView](#webview)
  - [IOS](#ios-1)
  - [Windows](#windows-1)
  - [Mac](#mac-1)
  - [Linux](#linux-1)
  - [Web](#web-1)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Flutter与原生方法交互

Flutter 定义了三种不同的 Channel

+ MethodChanel：用于传递方法调用（method invocation） 
+ EventChannel：用于事件流的发送（event streams） 
+ MessageChannel：用于传递字符串和半结构化的消息

## Android

### Flutter->Android

Flutter端调用Android端方法

```kotlin
//不带参数的调用
1.Android端
class ToastPlugin(private val context: Context) : MethodCallHandler {     //自己写了类实现MethodCallHandler接口
    override fun onMethodCall(call: MethodCall, result: MethodChannel.Result) {  
        //如果Flutter端调用了getPlatformVersion方法，那么就返回数据；
        //返回数据通过MethodCall的success方法
        if (call.method == "getPlatformVersion") {   //getPlatformVersion这个就是flutter调用的方法名
            Toast.makeText(context, "我收到啦!!", Toast.LENGTH_SHORT).show()
            result.success("Android " + Build.VERSION.RELEASE)    //成功的结果
        } else {
            result.notImplemented()   //错误的结果
        }
    }
}

class MainActivity : FlutterActivity() {    //MainActivity中来绑定
    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)

       MethodChannel(
            flutterEngine.dartExecutor.binaryMessenger,
            "hello"      //这个参数是channel，和flutter那边定义的一样
        ).setMethodCallHandler(ToastPlugin(this))   //绑定方法体
    }
}

2.Flutter端
final MethodChannel _channel = MethodChannel('hello');    //要和Android端定义的channel一样
Future<String?> get platformVersion async {
    //调用原生代码
    final String? version = await _channel.invokeMethod('getPlatformVersion');   //调用getPlatformVersion方法
    return version;
}

//带有参数的调用
1.Android端
class ToastPlugin(private val context: Context) : MethodCallHandler {
    override fun onMethodCall(call: MethodCall, result: MethodChannel.Result) {
        //如果Flutter端调用了getPlatformVersion方法，那么就返回数据；
        //返回数据通过MethodCall的success方法
        if (call.method == "getPlatformVersion") {
            val from = call.argument<String>("from")    //获取来自Flutter端的参数
            Toast.makeText(context, "我收到啦!!${from}", Toast.LENGTH_SHORT).show()
            result.success("Android " + Build.VERSION.RELEASE)
        } else {
            result.notImplemented()
        }
    }
}

class MainActivity : FlutterActivity() {    //MainActivity中来绑定
    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)

       MethodChannel(
            flutterEngine.dartExecutor.binaryMessenger,
            "hello"      //这个参数是channel，和flutter那边定义的一样
        ).setMethodCallHandler(ToastPlugin(this))   //绑定方法体
    }
}

2.Flutter端
final MethodChannel _channel = MethodChannel('hello');    //要和Android端定义的channel一样
Future<String?> get platformVersion async {
   //调用原生代码，invokeMethod第二个参数可以携带个map，调用Android端带有参数的方法
   final String? version =await _channel.invokeMethod('getPlatformVersion', {'from': 'Flutter'});
   return version;
}
```

### Android->Flutter

Android端调用Flutter端方法

```kotlin
1.Android端
class MainActivity : FlutterActivity() {

    private lateinit var methodChannel_toFlutter: MethodChannel

    override fun onStart() {
        super.onStart()
        methodChannel_toFlutter = MethodChannel(
            getFlutterEngine()!!.dartExecutor.binaryMessenger, "toFlutterChannelName"  //需要和Flutter保持一致
        )
        invokeFlutterMethod_toAllFlutter()     //在onStart方法里面去调用该方法
    }

    //传递参数给Flutter
    fun invokeFlutterMethod_toAllFlutter() {
        this.methodChannel_toFlutter.invokeMethod(
            "fluMethod",
            "我是原生Android，我将参数传递给Flutter里面的一个方法",
            object : MethodChannel.Result {
                override fun success(o: Any?) {
                    System.out.println(o)
                }
                override fun error(s: String, s1: String?, o: Any?) {

                }
                override fun notImplemented() {

                }
            })
    }
}

2.Flutter端
static const _platform = MethodChannel('toFlutterChannelName');  //和Android端保持一致

  @override
  void initState() {
    super.initState();
    _platform.setMethodCallHandler(flutterMethod);
  }

  Future<dynamic> flutterMethod(MethodCall methodCall) async{
    switch (methodCall.method) {
      case 'fluMethod':
        print('原生Android调用了flutterMethod方法！！！');
        print('原生Android传递给flutter的参数是：：'+methodCall.arguments);
        break;
    }
  }
```

## IOS

## Windows

## Mac

## Linux

## Web

# Flutter使用原生View并且交互（View插件开发）

交互步骤

1. 定义PlatformView
2. 定义PlatformViewFactory，用来创建上述View
3. 定义FlutterPlugin，注册上述工厂类
4. 向Flutter端注册上述Plugin
5. 创建PlatvormView对应的widget
6. 如果有通信需求，在Widget中创建MethodChannel与native通信
7. 在layout中使用上述widget显示PlatformView

## Android
### WebView
```kotlin
//Android端
//1. 定义FlutterWebView（定义FlutterWebView，使之继承自io.flutter.plugin.platform.PlatformView,内部持有WebView实例，通过MethodChannel接收Flutter传来的URL并打开网页，注意channel_id的定义要与flutter保持一致。
）
package com.example.flutter_webview_demo.webview

import android.annotation.SuppressLint
import android.content.Context
import android.graphics.Bitmap
import android.view.KeyEvent
import android.view.View
import android.webkit.WebChromeClient
import android.webkit.WebResourceRequest
import android.webkit.WebView
import android.webkit.WebViewClient
import com.example.flutter_webview_demo.App
import io.flutter.plugin.common.BinaryMessenger
import io.flutter.plugin.common.MethodCall
import io.flutter.plugin.common.MethodChannel
import io.flutter.plugin.platform.PlatformView;


class FlutterWebView(
    context: Context,
    messenger: BinaryMessenger,
    viewId: Int,
    args: Map<String, Any>?
) : PlatformView, MethodChannel.MethodCallHandler {
    private var webView: WebView = WebView(context);

    //用于Android调用Flutter
    private var channelAndroidToFlutter: MethodChannel = MethodChannel(
        messenger, "webViewChannel"  //需要和Flutter保持一致
    )

    //用于Flutter调用Android
    private var channelFlutterToAndroid: MethodChannel =
        MethodChannel(messenger, "plugins.lucky.views/webview_$viewId")   //需要和Flutter保持一致


    init {
        webView.apply {
            settings.apply {
                // enable Javascript
                javaScriptEnabled = true
                //支持手势
                setSupportZoom(true)
                builtInZoomControls = true
                displayZoomControls = false // no zoom button
                loadWithOverviewMode = true
                useWideViewPort = true
                domStorageEnabled = true
                //允许跨域
                allowFileAccess = true
                allowFileAccessFromFileURLs = true
                allowUniversalAccessFromFileURLs = true
            }
        }
        webView.webViewClient = NewWebViewClient(channelAndroidToFlutter)

        channelFlutterToAndroid.setMethodCallHandler(this)

        if (args != null) {
            val url = args["url"] as String
            webView.loadUrl(url)
        } else {
            throw IllegalArgumentException("args is null.")
        }
    }


    @SuppressLint("SetJavaScriptEnabled")
    override fun getView(): View {
        return webView
    }

    override fun dispose() {
        webView.destroy()
    }

    //Flutter调用Android都会通过这个方法,如果传递过来的有数据通过call.arguments获取
    override fun onMethodCall(call: MethodCall, result: MethodChannel.Result) {
        when (call.method) {
            "reload" -> reload(result)
            "loadUrl" -> loadUrl(call, result)
            else -> result.notImplemented()
        }
    }

    private fun reload(result: MethodChannel.Result) {
        webView.reload()
        result.success(null)
    }

    private fun loadUrl(call: MethodCall, result: MethodChannel.Result) {
        val url = call.arguments as String
        webView.loadUrl(url)
        result.success(null)
    }
}

class NewWebViewClient(private val channelAndroidToFlutter: MethodChannel) : WebViewClient() {


    override fun shouldOverrideUrlLoading(view: WebView?, request: WebResourceRequest?): Boolean {
        return false;
    }

    //加载结束
    override fun onPageFinished(view: WebView?, url: String?) {
        super.onPageFinished(view, url)
        channelAndroidToFlutter.invokeMethod(
            "onPageFinished",
            url,
            object : MethodChannel.Result {
                override fun success(o: Any?) {
                }
                override fun error(s: String, s1: String?, o: Any?) {

                }
                override fun notImplemented() {
                }
            })
    }

    //加载开始
    override fun onPageStarted(view: WebView?, url: String?, favicon: Bitmap?) {
        super.onPageStarted(view, url, favicon)
        channelAndroidToFlutter.invokeMethod(
            "onPageStarted",
            url,
            object : MethodChannel.Result {
                override fun success(o: Any?) {
                }
                override fun error(s: String, s1: String?, o: Any?) {
                }
                override fun notImplemented() {
                }
            })
    }
}
//2.定义WebViewFactory（WebViewFactory继承自PlatformViewFactory。PlatformView必须通过工厂类创建）
package com.example.flutter_webview_demo.webview

import android.content.Context
import io.flutter.plugin.common.BinaryMessenger
import io.flutter.plugin.common.StandardMessageCodec
import io.flutter.plugin.platform.PlatformView
import io.flutter.plugin.platform.PlatformViewFactory

class FlutterWebViewFactory(val messenger: BinaryMessenger) : PlatformViewFactory(
    StandardMessageCodec.INSTANCE) {

    override fun create(context: Context?, viewId: Int, args: Any?): PlatformView {
        val flutterView = FlutterWebView(context!!, messenger, viewId, args as Map<String, Any>?)
        return flutterView
    }
}
//3. 创建WebViewPlugin（继承io.flutter.embedding.engine.plugins.FlutterPlugin，在onAttachedToEngine回调中注册PlatformViewFactory）
package com.example.flutter_webview_demo.webview

import io.flutter.embedding.engine.plugins.FlutterPlugin
import io.flutter.plugin.common.BinaryMessenger

class FlutterWebViewPlugin : FlutterPlugin {

    override fun onAttachedToEngine(binding: FlutterPlugin.FlutterPluginBinding) {
        val messenger: BinaryMessenger = binding.binaryMessenger
        binding
            .platformViewRegistry
            .registerViewFactory(
                "plugins.flutter.lucky/webview", FlutterWebViewFactory(messenger)
            )
    }

    override fun onDetachedFromEngine(binding: FlutterPlugin.FlutterPluginBinding) {

    }
}
//4. 注册WebViewPlugin（在Android入口处通过注册插件。通常我们通过MainActivity来显示Flutter，此时可以在MainActivity获得FlutterEngin，并通过其注册插件）
package com.example.flutter_webview_demo

import com.example.flutter_webview_demo.webview.FlutterWebViewPlugin
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine

class MainActivity : FlutterActivity() {

    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)
        flutterEngine.plugins.add(FlutterWebViewPlugin())
    }
}

//Flutter端
//1.定义WebView的Widget（创建WebView的widget，build时返回AndroidView）
import 'package:flutter/cupertino.dart';
import 'package:flutter/foundation.dart';
import 'package:flutter/services.dart';

class LuckyAndroidWebView extends StatefulWidget {
  final String url;
  Function(String url)? onPageFinished;
  Function(String url)? onPageStarted;
  Function(int id)? onWebViewCreated;

  LuckyAndroidWebView(
      {Key? key,
      required this.url,
      this.onPageFinished,
      this.onPageStarted,
      this.onWebViewCreated})
      : super(key: key);

  @override
  State<StatefulWidget> createState() {
    return _LuckyAndroidWebViewState();
  }
}

class _LuckyAndroidWebViewState extends State<LuckyAndroidWebView> {
  static const _channelAndroidToFlutter =
      MethodChannel('webViewChannel'); //和Android端保持一致

  @override
  Widget build(BuildContext context) {
    if (defaultTargetPlatform == TargetPlatform.android) {
      return AndroidView(
          creationParams: {'url': widget.url},
          creationParamsCodec: const StandardMessageCodec(),
          //需要与Android端保持一致
          viewType: 'plugins.flutter.lucky/webview',
          //PlatformView创建后会通过onPlatformViewCreated进行回调，可以在里面做一些Flutter端的初始化
          onPlatformViewCreated: _onPlatformViewCreated);
    } else {
      throw Exception("not impl:" + defaultTargetPlatform.toString());
    }
  }

  @override
  void initState() {
    super.initState();
    _channelAndroidToFlutter.setMethodCallHandler(fromAndroidMethod);
  }

  //Android端回调回来的方法
  Future<dynamic> fromAndroidMethod(MethodCall methodCall) async {
    switch (methodCall.method) {
      case 'onPageFinished':
        if (widget.onPageFinished != null) {
          widget.onPageFinished!(methodCall.arguments);
        }
        break;
      case 'onPageStarted':
        if (widget.onPageStarted != null) {
          widget.onPageStarted!(methodCall.arguments);
        }
        break;
    }
  }

  void _onPlatformViewCreated(int id) {
    if (widget.onWebViewCreated == null) return;
    widget.onWebViewCreated!(id);
  }
}

//用于调用Android端方法提供的工具类
class WebViewController {
  WebViewController.init(int id)
      : _channel = MethodChannel('plugins.lucky.views/webview_$id');

  final MethodChannel _channel;

  Future<void> loadUrl(String url) async {
    return _channel.invokeMethod('loadUrl', url);
  }

  Future<void> reload() async {
    return _channel.invokeMethod('reload');
  }
}
//2.使用Widget
class _MyHomePageState extends State<MyHomePage> {
  late WebViewController _webViewController;

  void _incrementCounter() {
    _webViewController.reload();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Container(
        width: 500,
        height: 500,
        child: LuckyAndroidWebView(
          url:
              'file:///android_asset/index.html?https://oss-dev.kaigongla.cn/public/file/D05/2022/12/02/ed735696315d4288920be62f9e470a69.pdf',
          onWebViewCreated: (int id) {
            _webViewController = WebViewController.init(id);
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}

```

## IOS

## Windows

## Mac

## Linux

## Web
 



