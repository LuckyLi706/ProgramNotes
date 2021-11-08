# Activity

+ [Activity官网学习](https://developer.android.com/guide/components/activities/intro-activities?hl=zh-cn)

## 生命周期

![](../images/activity_lifecycle.png)

```java
0、onCreate()：
这是 Activity 的第一个生命周期方法，其中必须要做的操作就是 setContentView()。
setContentView()：设置内容视图
setContentView() 里面大概做了这么几件事：
创建 DecorView，并设置 PhoneWindow
解析 xml 布局文件，生成 View 对象并塞到 DecorView 中
此时 DecorView 并没有被绘制，Window 对象也没有被显示到屏幕，Activity 也是不可见的。
DecorView ：布置视图
除此之外，开发者通常也会在 onCreate() 方法中做一些数据的初始化操作。
onCreate() 在一次完整的生命周期中只会回调一次，它也不是一个长驻状态，完成工作只会就会进入 onStart() 。

1、onStart()
onStart() 也不是一个长驻状态，官方文档对于它的描述是这样的：
The onStart() call makes the activity visible to the user, as the app
prepares for the activity to enter the foreground and become
interactive.
在 onStart() 方法中，Activity 对用户可见，应用准备进入前台和用户交互。我对这句 Activity 对用户可见 其实抱有很大的疑问。
不考虑特殊情况，正常启动一个 Activity，onCreate -> onStart ，此时所谓的 “可见”，见到的是什么？
这个问题在下面的 onResume 一节中会详细说明，读者可以先仔细揣摩一下。
onStart() 方法中可以做些什么呢？通常会和 onStop() 搭配做一些资源申请和释放的工作，例如相机的申请和释放。

2、onResume
熟悉 UI 绘制流程的读者肯定知道，onResume() 是真正进行 UI 绘制以及显示的地方。其中的核心逻辑就是 WindowManager.addView() 方法，实际调用的是 WindowManagerGlobal.addView() 方法。它大致干了这么几件事：
1、创建 ViewRootImpl 对象
2、调用 ViewRootImpl.setView() 方法
ViewRootImpl 的构造函数中做了这么几件事：
1、初始化跟 WMS 通信的 WIndowSession 对象，这是一个 Binder 对象
2、初始化 Choreographer 对象
ViewRootImpl.setView() 方法做了这么几件事：
1、调用 requestLayout() 方法，发起绘制
2、Binder 调用 WMS.addToDisplay() 方法，将 window添加到屏幕
requestLayout() 方法中就会进行我们所熟知的 测量、布局和绘制 流程，但并不是直接进行的，它依赖 vsync 信号。requestLayout() 只是通过前面已经初始化了的 Choreographer 对象进行注册监听，当下一个 vsync 信号来临时，会回调 performTraversals() 方法，这其中就会真正的进行测量、布局和绘制。
整个 UI 绘制流程的知识点很多，仅靠以上简单一段文字肯定是无法完全概括的，感兴趣的读者可以自己去翻翻源码。但是我们可以肯定是，onResume 是真正的用户界面可见的时机。
再回到之前的问题，onStart 中可见的是什么？我也无法回答这个问题，或者可能大家都曲解了官方文档的意思，是否应该理解为 “Activity 即将可见”。
同样，onResume() 通常也可以和 onPause() 搭配做一些资源申请和释放的工作。那么，既然 onStart/onStop 和 onResume/onPause 都可以，该如何选择呢？同样放到后面进行解答。

3、onPause
onPause() 是一个很短暂的过程，之后如果用户返回了之前的 Activity，则会回调 onResume 。如果没有，则会回调 onStop 。
给 onPause 一个精准的描述的话，应该是 非前台，不可交互，但不一定不可见 。对于系统来说，无论是手机还是 PC ，同一个时间一定只有一个处于前台，获取焦点，且可与用户交互的活动窗口，所以 非前台，不可交互 很好理解。那 不一定不可见 如何理解呢？其实也很简单，类似 PC 的多窗口，Android 系统也是有多窗口模式的。
最后，注意 onPause 中不建议进行重量级的耗时操作，因为在 Activity 跳转过程中，前一个 Activity 的 onPause() 是发生在后一个 Activity 的任何生命周期之前的。

4、onStop
完全的不可见状态。但此时的 Activity 仍在内存中，只是没有关联到任何 Window 。如果后续有机会再次返回，则会回调 onRestart -> onStart 。

5、onDestroy
onStop 之后没有被用户捞回去，最后就得被销毁。主动的调用 finish 或者系统配置改变也会可能导致销毁。
注意在 onDestroy 中释放所有不需要的资源，否则可能导致内存泄露。
```

### Activity A切换到Activity B的生命周期

```
A:onPause -> B:onCreate -> B:onStart -> B:onResume -> A:onSaveInstanceState-> A:onStop
```

### 返回键从Activity B到Activity A的生命周期

```
B:onPause -> A:onRestart -> A:onStart -> A:onResume -> B:onStop -> B:onDestroy
```

### onSaveInstanceState() 与 onRestoreIntanceState()

```
onSaveInstanceState（）
这两个方法并不是生命周期方法，它们并不一定会被触发。当应用遇到意外情况（如：内存不足、用户直接按Home键）由系统销毁一个Activity时，onSaveInstanceState() 会被调用，该方法的调用在onStop之前，与onPause没有时序关系。但是当用户主动去销毁一个Activity时，例如在应用中按返回键，onSaveInstanceState()就不会被调用。因为在这种情况下，用户的行为决定了不需要保存Activity的状态。
onSaveInstanceState()时机：
（1）用户按下Home键
（2）横竖屏切换
（3）按下电源按钮（关闭屏幕显示）
（4）内存不足导致优先级的Activity被杀死

onRestoreIntanceState()
当被系统异常销毁的Activity被重建时，会调用onRestoreIntanceState或onCreate方法来恢复，而onRestoreInstance与Oncreate方法中传入的Bundle对象是销毁时onSaveInstanceState保存的，onRestoreIntanceState在onStart之后。

onSaveInstanceState()与onPause()的区别？
onSaveInstanceState()只适合用于保存一些临时性的状态，而onPause()适合用于数据的持久化保存。
```

### 屏幕旋转的生命周期

```java
//第一种情况：不设置任何配置会重新走一遍生命周期
onPause -> onSaveInstanceState -> onStop -> onDestroy -> onCreate -> onStart -> onRestoreInstanceState -> onResume
    
//第二种情况：xml设置configChanges属性(android：configChanges = “orientation| screensize”)
@Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig); //系统不会重新创建Activity,会走这个方法
    }    
```

## 启动模式和Flags

### 启动模式

```java
//1.standard模式（标准模式）
标准模式就是我们最常用的模式，在该模式下，每当启动一个新的活动，它就会在返回栈中入栈，并处于栈顶的位置。该模式不会考虑活动是否已经存在栈中，每次启动都会创建该活动的一个新的实例

//2.singleTop（栈顶复用模式）
如果需要新创建的Activity处于栈顶的话，那么Activity的实例就不会重建，而是重用栈顶的实例，并回调onNewIntent方法
//应用场景
1.在通知栏点击收到的通知，然后需要启动一个Activity，这个Activity就可以用singleTop，否则每次点击都会新建一个Activity。
2.防止快速多次点击Activity，多次启动。

//3.singleTask模式（栈内复用模式）
与栈顶复用模式相对的，就是栈内复用模式，即一个栈内只有一个Activity的实例,也会回调onNewIntent方法。可以在AndroidMainfest文件的Activity中指定该Activity需要加载到哪个栈中，即singleTask的Activity可以指定想要加载的目标栈。singleTask和taskAffinity配合使用，指定开启的Activity加入到哪个栈中。
//应用场景
应用于首页或登录页，用户在点击后退键可直接退出应用,或者聊天界面。
多数App的主页。对于大部分应用，当我们在主界面点击回退按钮的时候都是退出应用，那么当我们第一次进入主界面之后，主界面位于栈底，以后不管我们打开了多少个Activity，只要我们再次回到主界面，都应该使用将主界面Activity上所有的Activity移除的方式来让主界面Activity处于栈顶，而不是往栈顶新加一个主界面Activity的实例，通过这种方式能够保证退出应用时所有的Activity都能被销毁。
    
//4、singleInstance（单例模式）
一看singleInstance其实就能想到是单例，以该模式启动Activity，就会直接创建一个新的任务栈，并创建该Activity的实例放入新栈中，一旦该模式的Activity实例已经存在于某个栈中，任何应用激活该Activity时都会重用该栈中的实例。
//应用场景
呼叫来电界面
```

### Flags

+ [Intent.addFlags() 启动Activity的20种flags全解析](https://www.jianshu.com/p/2bdc16cba04f)

```

```

## activity标签

```xml
<activity
    <!--是否允许activity更换从属的任务，比如从短信息任务 切换到浏览器任务，默认false-->
    android:allowTaskReparenting=["true" | "false"]  
    <!--是否保留状态不变，也就是切回home然后再打开，Activity是否处于最后状态-->
    android:alwaysRetainTaskState=["true" | "false"]  
    <!--启动时候是否清空任务栈，默认是false。-->
    android:clearTaskOnLaunch=["true" | "false"]  
    <!--一般用来设置Activity横竖屏切换时，不重新调用生命周期
“mcc“ 移动国家号码，由三位数字组成，每个国家都有自己独立的MCC，可以识别手机用户所属国家。
“mnc“ 移动网号，在一个国家或者地区中，用于区分手机用户的服务商。
“locale“ 所在地区发生变化。
“touchscreen“ 触摸屏已经改变。（这不应该常发生。）
“keyboard“ 键盘模式发生变化，例如：用户接入外部键盘输入。
“keyboardHidden“ 用户打开手机硬件键盘
“navigation“ 导航型发生了变化。（这不应该常发生。）
“orientation“ 设备旋转，横向显示和竖向显示模式切换。
“fontScale“ 全局字体大小缩放发生改变-->
    android:configChanges=["mcc", "mnc", "locale",  
        "touchscreen", "keyboard", "keyboardHidden",  
        "navigation", "orientation", "screenLayout",  
        "fontScale", "uiMode"]  
    <!--activity 是否可以被实例化,-->
    android:enabled=["true" | "false"]  
    <!--是否可被显示在最近打开的activity列表里  -->
    android:excludeFromRecents=["true" | "false"]  
    <!--是否允许activity被其它程序调用-->
    android:exported=["true" | "false"]  
    <!--当重新启动这个任务的时候，是否关闭已打开的Activity-->
    android:finishOnTaskLaunch=["true" | "false"]  
    <!--是否为当前Activity启动硬件加速-->
    android:hardwareAccelerated=["true" | "false"]  
    <!--Activity的图标-->
    android:icon="drawable resource"  
    <!--Activity的标签-->
    android:label="string resource"  
    <!--Activity的启动方式-->
    android:launchMode=["multiple" | "singleTop" | "singleTask" | "singleInstance"]  
    <!--Activity的实例是否可以运行在启动它的组件所在的应用程序进程中，一般与progress搭配使用-->
    android:multiprocess=["true" | "false"]  
    <!--类名，必须是Activity的子类-->
    android:name="string"  
    <!--设置在用户离开该Activity，并且它在屏幕上不再可见的时候，是否应该从Activity的堆栈中删除-->
    android:noHistory=["true" | "false"]  
    <!--别的应用访问当前Activity所需要的权限-->
    android:permission="string"  
    <!--表示该Activity运行的进程名称。 -->
    android:process="string"  
    <!--表示Activity显示的方向（比如纵向，横向-->
    android:screenOrientation=["unspecified" | "user" | "behind" |  
        "landscape" | "portrait" |  
        "sensor" | "nosensor"]  
    <!--Activity是否能被终止以及是否能在还没有保存其状态的情况下成功重启-->
    android:stateNotNeeded=["true" | "false"]  
    <!--Activity有亲和力的任务-->
    android:taskAffinity="string"  
    <!--为Activity定义一个整体主题风格资源的引用-->
    android:theme="resource or theme"  
    <!--Activity的主窗口如何与包含屏幕软键盘的窗口交互。-->
    android:windowSoftInputMode=["stateUnspecified",  
        "stateUnchanged", "stateHidden",  
        "stateAlwaysHidden", "stateVisible",  
        "stateAlwaysVisible", "adjustUnspecified",  
        "adjustResize", "adjustPan"] >     
</activity> 
```

## 隐式启动

### 隐式启动代码

```java
/**
使用setComponent方法
**/
Intent intent=new Intent();
intent.setComponent(new ComponentName(“com.android.calendar”, “com.android.calendar.LaunchActivity”));
intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);

/**
使用setClassName方法
**/
Intent intent=new Intent();
intent.setClassName("com.example.fm", "com.example.fm.MainFragmentActivity");
intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
intent.putExtra("test", "intent1");    //传递值
startActivity(intent);
```

### action标签

Action:Action属性的值是一个字符串，它代表了系统中定义的一系列常用动作。通过setAction()方法或在清单文件AndroidMainfest.xml中设置。默认为：DEFAULT。 

```java
//系统自带的
ACTION_MAIN	默认启动的Activity中使用
ACTION_VIEW	将数据显示给用户，经常用于浏览器中
ACTION_EDIT	可编辑的数据
ACTION_DEAL	启动系统拨号界面时使用
ACTION_CALL	直接打电话时使用
ACTION_SEND	给某人发信息，但未指定收件人
ACTION_SENDTO	给指定的收件人发信息
    
//打开系统浏览器
Intent intent = new Intent();
intent.setAction("android.intent.action.VIEW");
intent.setData(Uri.parse("http://www.baidu.com"));
startActivity(intent);
```

### category标签

Category：Category属性用于指定当前动作(Action)被执行的环境。通过addCategory()方法或在清单文件 AndroidMainfest.xml中设置.默认为:CATEGORY_DEFAULT。 

```java
//系统自带的
CATEGORY_DEFAULT：Android系统中默认的执行方式，按照普通Activity的执行方式执行。　
CATEGORY_HOME：设置该组件为Home Activity。
CATEGORY_PREFERENCE：设置该组件为Preference。　
CATEGORY_LAUNCHER：设置该组件为在当前应用程序启动器中优先级最高的Activity，通常为入口ACTION_MAIN配合使用。　
CATEGORY_BROWSABLE：设置该组件可以使用浏览器启动。　
CATEGORY_GADGET：设置该组件可以内嵌到另外的Activity中。
```

### data标签

Data:Data通常是URL格式定义的操作数据。列如:tel//。通过setData()方法设置。 

```java
/**
data属性解析：android:scheme、android:host、android:port、android:path、android:mimeType
**/


//系统自带的
tel://：号码数据格式，后跟电话号码。　
mailto://：邮件数据格式，后跟邮件收件人地址。
smsto://：短息数据格式，后跟短信接收号码。
content://：内容数据格式，后跟需要读取的内容。　
file://：文件数据格式，后跟文件路径。
market://search?q=pname:pkgname：市场数据格式，在Google Market里搜索包名为pkgname的应用。
geo://latitude,longitude:经纬数据格式，在地图上显示经纬度指定的位置。
```

# Fragment

## 生命周期

![](../images/fragment.webp)

```
onAttach(Contextcontext)：在Fragment和Activity关联上的时候调用，且仅调用一次。在该回调中我们可以将context转化为Activity保存下来，从而避免后期频繁调用getAtivity()获取Activity的局面，避免了在某些情况下getAtivity()为空的异常（Activity和Fragment分离的情况下）。同时也可以在该回调中将传入的Arguments提取并解析，在这里强烈推荐通过setArguments给Fragment传参数，因为在应用被系统回收时Fragment不会保存相关属性。

onCreate：在最初创建Fragment的时候会调用，和Activity的onCreate类似。
View onCreateView(LayoutInflater inflater, ViewGroup container,Bundle savedInstanceState)：在准备绘制Fragment界面时调用，返回值为Fragment要绘制布局的根视图，当然也可以返回null。注意使用inflater构建View时一定要将attachToRoot指明false，因为Fragment会自动将视图添加到container中，attachToRoot为true会重复添加报错。onCreateView并不是一定会被调用，当添加的是没有界面的Fragment就不会调用，比如调用FragmentTransaction的add(Fragment fragment, String tag)方法。

onActivityCreated ：在Activity的onCreated执行完时会调用。

onStart() ：Fragment对用户可见的时候调用，前提是Activity已经started。

onResume()：Fragment和用户之前可交互时会调用，前提是Activity已经resumed。

onPause()：Fragment和用户之前不可交互时会调用。

onStop()：Fragment不可见时会调用。

onDestroyView()：在移除Fragment相关视图层级时调用。

onDestroy()：最终清楚Fragment状态时会调用。

onDetach()：Fragment和Activity解除关联时调用。

```

## 和Activity如何数据交互

```java
Activity->Fragment
Activity中通过setArguments()方法传递给bundle对象，通过getArguments()方法获取bundle对象，然后获取bundle对象中的数据信息

Fragment->Activity
回调方式

Fragment->Fragment

EventBus
```

# Activity原理

+ [3分钟看懂Activity启动流程](https://www.jianshu.com/p/9ecea420eb52)
+ [Android8.0中Activity的启动流程](https://www.jianshu.com/p/459d38ade254)