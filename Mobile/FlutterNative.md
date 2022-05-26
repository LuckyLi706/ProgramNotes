# Flutter与原生交互

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

