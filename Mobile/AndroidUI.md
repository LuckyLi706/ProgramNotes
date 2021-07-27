# View的工作原理

+ 每个activity都对应一个窗口window，这个窗口是PhoneWindow的实例，PhoneWindow对应的布局是DecirView，是一个FrameLayout，DecorView内部又分为两部分，一部分是ActionBar，另一部分是ContentParent，而我们自己设置的布局则是contentParent 里面的一个子元素
+ 绘制会从根视图ViewRoot(具体类ViewRootImpl,他是连接WindowManager和DecoView的纽带)的performTraversals()方法开始
+ 从上到下遍历整个视图树，每个View控件负责绘制自己，而ViewGroup还需要负责通知自己的子View进行绘制操作，
+ ViewRootImpl内部调用performMeasure、performLayout、performDraw三个方法，这三个方法分别完成DecorView的measure、layout、和draw这三大流程
+ 其中performMeasure()中会调用View的measure()方法，在measure()方法中又会调用onMeasure()方法(布局比如LinearLayout自实现了onMeasure方法,为了去遍历子View)，在onMeasure()方法中会对所有子元素进行measure过程

## DecorView
- DecorView就是我们的 Activity（或者整个Window界面）的最顶级View。
- DecorView extends FrameLayout,它里面只有一个子元素为 LinearLayout,代表整个 Window 界面。
- LinearLayout布局也包裹了两个FrameLayout。
  + 上面的Framelayout是标题栏（TitleBar或ActionBar）。具体形式和android版本及主题有关。它默认包括了一个TextView，当然我们也可以自定义标题栏。
  + 下面的 FrameLayout 就是内容栏。它的id就是 content,我们通过setContentView所设置的布局文件其实就是添加在内容栏当中，所以这个方法就是叫做 setContentView

## 三大过程说明
- measure过程决定了View的宽和高，Measure完成后，可以通过getMeasuredWidth和getMeasuredHeight方法来获取到View测量后的宽高，在几乎所有的情况下它都等同于View的最终宽高。
- layout过程决定了View的四个顶点的坐标和实际的View的宽高，完成后，可以通过getTop、getBottom、getLeft、getRight来拿到View的四个顶点的位置，并可以通过getWidth和getHeight方法来拿到View的最终宽高。
- draw过程则决定了View的显示，只有draw方法完成以后View的内容才能呈现在屏幕上。

## 三大过程解析
### [measure(测量过程)](https://www.cnblogs.com/yaoxiaowen/p/7045931.html)
+ 理解MeasureSpec
  1. 该类封装了一个View的规格尺寸，包括View的宽和高的信息，但是要注意，MeasureSpec并不是指View的测量宽高，这是不同的，是根据MeasueSpec而测出测量宽高。
  2. 作用是在Measure流程中，系统会将View的LayoutParams和根据父容器所施加的规则转换成对应的MeasureSpec，然后在onMeasure方法中根据这个MeasureSpec来确定View的测量宽高。
  3. 
+ 理解LayoutParams
  1. 主要用来动态控制子view的摆放位置
  2. 三种参数：
     - 固定数值，单位px
     - ViewGroup.LayoutParams.MATCH_PARENT ，意思为宽度和父view相同
     - ViewGroup.LayoutParams.WRAP_CONTENT，意思为自适应
  3. 就是当前view设置的layout_height和layout_width两个属性
+ MeasureSpec和LayoutParams的关系
  1. 一个View的尺寸受到父容器(ParentSpecMode)和本身LayoutParams双重影响
```
如果ParentSpecMode是MeasureSpec.EXACTLY,子View的LayoutParams是Match_parent或者具体的dp,那么是MeasureSpec.EXACTLY

如果ParentSpecMode是MeasureSpec.EXACTLY,子View的LayoutParams是wrap_content,那么是MeasureSpec.AT_MOST

如果ParentSpecMode是MeasureSpec.AT_MOST,子View的LayoutParams是具体的dp,那么是MeasureSpec.EXACTLY

如果ParentSpecMode是MeasureSpec.AT_MOST,子View的LayoutParams是wrap_content或者match_parent,那么是MeasureSpec.AT_MOST

如果ParentSpecMode是MeasureSpec.UNSPECIFIED,子View的LayoutParams是具体的dp,那么是MeasureSpec.EXACTLY

如果ParentSpecMode是MeasureSpec.UNSPECIFIED,子View的LayoutParams是wrap_content或者match_parent,那么是MeasureSpec.UNSPECIFIED
```
+ 在onCreate、onResume、onStart获取View的宽和高
```
1.Activity/View的onWindowsFocusChanged方法,会被多次调用
2.view.post(runnabe)方法,
3.ViewTreeObserver
4.view.measure(int widthMeasureSpec, int heightMeasureSpec)
```
+ 在view内部获取View的宽和高
```
1、不要在onMeasure方法中获取,可能会测量多次
2、最好在onLayout方法里面去获取

```

### layout(布局过程)

### draw(绘制过程)

# View的事件分发机制

 [参考资料,很生动的讲解了分发机制](https://www.cnblogs.com/net168/p/4165970.html)

## 分发机制（Activity->ViewGroup->View）
### 分发方法解析

```
1、dispatchTouchEvent()  ——用来分发事件所用

　　该方法会将根元素的事件自上而下依次分发到内层子元素中，直到被终止或者到达最里层元素，该方法也是采用一种隧道方式来分发。在其中会调用onInterceptTouchEvent()
和onTouchEvent()，一般不会去重写。返回false则不拦截继续往下分发，如果返回true则拦截住该事件不在向下层元素分发，在dispatchTouchEvent()方法中默认返回false。

2、onInterceptTouchEvent()  ——用来拦截事件所用

　　该方法在ViewGroup源代码中实现就是返回false不拦截事件，Touch事件就会往下传递给其子View。
　　如果我们重写该方法并且将其返回true，该事件将会被拦截，并且被当前ViewGroup处理，调用该类的onTouchEvent()方法。

3、onTouchEvent()  ——用来处理事件

　　返回true则表示该View能处理该事件，事件将终止向上传递（传递给其父View）
　　返回false表示不能处理，则把事件传递给其父View的onTouchEvent()方法来处理
```
### 分发机制代码

1. EventActivity

```
package com.lucky.newsandroid.ui.activity;

import android.view.MotionEvent;

import com.lucky.newsandroid.R;
import com.lucky.newsandroid.base.BaseActivity;
import com.lucky.newsandroid.utils.Logutil;

/**
 * 作者：jacky on 2019/9/27 10:39
 * 邮箱：jackyli706@gmail.com
 */
public class EventActivity extends BaseActivity {
    @Override
    public int getLayoutId() {
        return R.layout.activity_exent;
    }

    /**
     *
     * @param event
     * @return
     */
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        Logutil.d("EventActivity:onTouchEvent:" + event.getAction());
        return super.onTouchEvent(event);
    }

    /**
     * 最先执行
     * 用来分发事件
     * 返回false 向EventLayout分发
     * 返回true表示拦截，不向EventLayout分发
     *
     * @param ev
     * @return
     */
    @Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        Logutil.d("EventActivity:dispatchTouchEvent:" + ev.getAction());
        return super.dispatchTouchEvent(ev);
    }
}

```
  2. EventLayout
```
package com.lucky.newsandroid.ui.view;

import android.content.Context;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.widget.LinearLayout;

import androidx.annotation.Nullable;

import com.lucky.newsandroid.utils.Logutil;

/**
 * 作者：jacky on 2019/9/27 10:40
 * 邮箱：jackyli706@gmail.com
 */
public class EventLayout extends LinearLayout {

    public EventLayout(Context context) {
        super(context);


    }

    public EventLayout(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);

        this.addView(new EventButton(context));
    }

    /**
     * 用来给子View进行下发任务
     * @param ev
     * @return
     */
    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        Logutil.d("EventLayout:onInterceptTouchEvent:" + ev.getAction());
        return super.onInterceptTouchEvent(ev);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        Logutil.d("EventLayout:onTouchEvent:" + event.getAction());
        return super.onTouchEvent(event);
    }

    /**
     * 最先执行
     * 内部执行onInterceptTouchEvent方法
     * @param ev
     * @return
     */
    @Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        Logutil.d("EventLayout:dispatchTouchEvent:" + ev.getAction());
        return super.dispatchTouchEvent(ev);
    }
}

```
  3. EventButton
 ```
 package com.lucky.newsandroid.ui.view;


import android.content.Context;
import android.view.MotionEvent;

import androidx.appcompat.widget.AppCompatButton;

import com.lucky.newsandroid.utils.Logutil;

/**
 * 作者：jacky on 2019/9/27 10:41
 * 邮箱：jackyli706@gmail.com
 */
public class EventButton extends AppCompatButton {
    public EventButton(Context context) {
        super(context);

        this.setText("点击我");
        this.setTextSize(12);
    }

    /**
     * 返回false，表示不能处理,向上传递给父布局处理,父布局调用onTouchEvent
     * 返回true，表示自己能处理，不再向上传递
     * @param event
     * @return
     */
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        Logutil.d("EventButton:onTouchEvent:" + event.getAction());
        return super.onTouchEvent(event);
    }

    /**
     * 没有子View，不进行向下分发,onTouchEvent
     * @param event
     * @return
     */
    @Override
    public boolean dispatchTouchEvent(MotionEvent event) {
        Logutil.d("EventButton:dispatchTouchEvent:" + event.getAction());
        return super.dispatchTouchEvent(event);
    }
}

 ```

## 滑动冲突



# 自定义View和ViewGroup

## 分类
+ 继承View重写onDraw方法（采用这种方法需要自己支持wrap_content）,并且padding也需要自己处理
+ 继承ViewGroup派生特殊的Layout（这种方式稍微复杂,需要合适的处理ViewGroup的测量、布局这两个过程,并同时处理子元素的测量和布局过程）
+ 继承特定的View（比如TextView,好处是不需要自己支持wrap_content）
+ 继承特定的ViewGroup（比如LinearLayout，更常见）

## 须知
+ 让View支持wrap_content（直接继承View和ViewGroup的需要处理）
+ 如果有必要,让View支持padding（如果不在draw方法中处理padding，那么padding属性无法起作用）
+ 尽量不要在View中使用Handler,没必要（View内部本身就提供了post方法）
+ View中如果有线程和动画,需要即时停止（参考View的onDetachedFromWindow方法）
+ View带有滑动嵌套情形时,需要处理好滑动冲突.

# 原生View和ViewGroup

## LinearLayout和RelativeLayout

+ 同等情况下，LinearLayout的性能优于RelativeLayout，所以setContentView()的父布局是LinearLayout

+ 在尽量减少布局嵌套的情况下，RelativeLayout可以比LinearLayout写出更复杂的布局
+ RelativeLayout的对子View测量了两次
+ 在LinearLayout中，是先判断方向，然后onMeasure()。但是如果遇到有weight属性的子View，会对其进行第二次的onMeasure()。

## TextView

### 自动定位到最后一行
```java
textView.append(msg + "\n");
int offset = textView.getLineCount() * textView.getLineHeight();
if (offset > textView.getHeight()) {
   textView.scrollTo(0, offset - textView.getHeight());
}
```

## WebView

### 加载html的几种方式
```java
1、打开本包内assets目录下的index.html文件
webview.loadUrl("file:///android_assets/index.html");

2、打开本包内/data/data/pkg目录下的index.html文件
webview.loadUrl("file:"+getFilesDir()+File.separator+"index.html");

3、打开本包内SD卡目录下的index.html文件
webview.loadUrl("file:"+Environment.getExternalStorageDirectory()+File.separator+"index.html");

4、加载URL,直接输入网址即可
webview.loadUrl("www.google.com");
```
### WebSettings
```java
WebSettings settings = getSettings();
 //默认是false 设置true允许和js交互
 settings.setJavaScriptEnabled(true);
 //  WebSettings.LOAD_DEFAULT 如果本地缓存可用且没有过期则使用本地缓存，否加载网络数据 默认值
 //  WebSettings.LOAD_CACHE_ELSE_NETWORK 优先加载本地缓存数据，无论缓存是否过期
 //  WebSettings.LOAD_NO_CACHE  只加载网络数据，不加载本地缓存
 //  WebSettings.LOAD_CACHE_ONLY 只加载缓存数据，不加载网络数据
 //Tips:有网络可以使用LOAD_DEFAULT 没有网时用LOAD_CACHE_ELSE_NETWORK
 settings.setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);
 //开启 DOM storage API 功能 较大存储空间，使用简单
 settings.setDomStorageEnabled(true);
 //设置数据库缓存路径 存储管理复杂数据 方便对数据进行增加、删除、修改、查询 不推荐使用
 settings.setDatabaseEnabled(true);
 final String dbPath = context.getApplicationContext().getDir("db", Context.MODE_PRIVATE).getPath();
 settings.setDatabasePath(dbPath);
 //开启 Application Caches 功能 方便构建离线APP 不推荐使用
 settings.setAppCacheEnabled(true);
 final String cachePath = context.getApplicationContext().getDir("cache", Context.MODE_PRIVATE).getPath();
 settings.setAppCachePath(cachePath);
 settings.setAppCacheMaxSize(5 * 1024 * 1024);
```

### WebviewClient
```java
1、shouldOverrideUrlLoading(WebView view, String url)
在API 24以后过时，当一个url即将被webview加载时，给Application一个机会来接管处理这个url，方法返回true代表Application自己处理url；返回false代表Webview处理url。
举个例子，项目中需要处理传过来的URL是一个事件还是一个HTTP链接，可以通过自定义协议头 (nativeapi://) 来过滤，如：
@Override
 public boolean shouldOverrideUrlLoading(WebView view, String url) {
     Uri uri = Uri.parse(url);
     String scheme = uri.getScheme();
     if (TextUtils.isEmpty(scheme)) return true;
     if (scheme.equals("nativeapi")) {
         //如定义nativeapi://showImg是用来查看大图，这里添加查看大图逻辑
         return true;
     } else if (scheme.equals("http") || scheme.equals("https")) {
         //处理http协议
         if (Uri.parse(url).getHost().equals("www.example.com")) {
            // 内部网址，不拦截，用自己的webview加载
             return false;
         } else {
             //跳转外部浏览器
             Intent intent = new Intent(Intent.ACTION_VIEW, uri);
             context.startActivity(intent);
             return true;
         }
     }
     return super.shouldOverrideUrlLoading(view, url);
 }

注：如果使用的是Post请求方式，则此方法不会被回调
2、shouldOverrideUrlLoading(WebView view, WebResourceRequest request)
在API 24以后新加的，使用同上。

3、shouldInterceptRequest(WebView view, String url)
在API 21以后过时，通知Application加载资源的请求并返回请求的资源，如果返回值是Null，Webview仍然会按正常加载资源；否则返回的数据将会被使用。
注：回调发生在子线程中,不能直接进行UI操作

4、shouldInterceptRequest(WebView view, WebResourceRequest request)
在API 21以后新加，使用同上。

5、onPageStarted(WebView view, String url, Bitmap favicon)
通知Application页面已经开始加载资源，页面加载过程中，onPageStarted至多会被执行一次。

6、onPageFinished(WebView view, String url)
通知Application页面已经加载完毕。

7、onReceivedError(WebView view, int errorCode, String description, String failingUrl)
通知Application有错误发生，这些错误是不可恢复的(即主要的资源不可用)。errorCode参数对应于一个ERROR_ *常量
```

### WebChromeClient
```java
1、onProgressChanged(WebView view, int newProgress)
通知Application的加载进度，newProgress取值范围[0,100]，可以通过这个方法来编写一个带加载进度条的Webview，具体例子请参考：Android 编写一个带进度条的Webview
2、onReceivedTitle(WebView view, String title)
当加载页面标题有改变时会通知Application，title即为新标题。
控制Webview加载历史网页
WebView重写URL加载时,它会自动累积的历史访问的web页面。可以通过向后goBack()和向前goForward()。
举例，可以在Activity中的回退键控制向后回退到前一个页面：

@Override
 public boolean onKeyDown(int keyCode, KeyEvent event) {
     // Check if the key event was the Back button and if there's history
     if ((keyCode == KeyEvent.KEYCODE_BACK) && webview.canGoBack()) {
         webview.goBack();
         return true;
     }
     // If it wasn't the Back key or there's no web page history, bubble up to the default
     // system behavior (probably exit the activity)
     return super.onKeyDown(keyCode, event);
    }
```

### WebView和js交互
```java
js调用java接口
public class WebAppInterface {
    Context mContext;

    /** Instantiate the interface and set the context */
    WebAppInterface(Context c) {
        mContext = c;
    }

    /** Show a toast from the web page */
    @JavascriptInterface
    public void showToast(String toast) {
        Toast.makeText(mContext, toast, Toast.LENGTH_SHORT).show();
    }
}
//SDK>=17（Android4.2）以上，必须添加@JavascriptInterface声明，然后通过 addJavascriptInterface() 方式供Js调用，如：
webView.addJavascriptInterface(new WebAppInterface(this), "android");

js内调用：
<input type="button" value="Say hello" onClick="showAndroidToast('Hello Android!')" /> 
<script type="text/javascript">
 function showAndroidToast(toast) { 
//调用Android中的showToast方法 
Android.showToast(toast); 
}
 </script>


java调用js接口
可以通过webview.loadUrl("javascript:JsMethod()")方式加载Js接口，如果有参数，直接加到JsMethod()里面即可，下面封装了两个方法，分别是加载带参数和不带参数的Js函数：
/**
     * 加载带参数的JS函数
     *
     * @param JsName JS函数名
     * @param params 不定参数
     */
    public void loadJSWithParam(String JsName, String... params) {
        String TotalParam = "";
        for (int i = 0; i < params.length; i++) {
            if (i == params.length - 1) {
                //最后一个
                TotalParam += (params[i]);
            } else {
                TotalParam += (params[i] + "','");
            }
        }
        this.loadUrl("javascript:" + JsName + "('" + TotalParam + "')");
    }

    /**
     * 加载不带参数的JS函数
     *
     * @param JsName JS函数名
     */
    public void loadJS(String JsName) {
        this.loadUrl("javascript:" + JsName + "()");
    }
```

### 优化和坑
```java
1、Webview打开一个链接，播放一段音乐，退出Activity时音乐还在后台播放，可以通过在Activity的onPause中调用webview.onPause()解决，并在Activity的onResume中调用webview.onResume()恢复，如下：
@Override
    protected void onPause() {
       h5_webview.onPause();
       h5_webview.pauseTimers();
       super.onPause();
    }
 @Override
    protected void onResume() {
       h5_webview.onResume();
       h5_webview.resumeTimers();
       super.onResume();
    }

Webview的onPause()方法官网是这么解释的：
Does a best-effort attempt to pause any processing that can be paused safely, such as animations and geolocation. Note that this call does not pause JavaScript. To pause JavaScript globally, use pauseTimers(). To resume WebView, call onResume().
通知内核尝试停止所有处理，如动画和地理位置，但是不能停止Js，如果想全局停止Js，可以调用pauseTimers()全局停止Js，调用onResume()恢复。

2、5.0 以后的WebView加载的链接为Https开头，但是链接里面的内容，比如图片为Http链接，这时候，图片就会加载不出来，解决方法：
 if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) { 
 webSetting.setMixedContentMode(webSetting.getMixedContentMode());
  }

原因是5.0之后不支持Https和Http的混合模式，具体可参看：Android5.0 WebView中Http和Https混合问题

3、WebView与JavaScript相互调用时，如果是debug没有配置混淆时，调用时没问题的，但是当设置混淆后发现无法正常调用了，解决方法：
在proguard-rules.pro文件中配置：
-keepattributes *Annotation*  
-keepattributes *JavascriptInterface*
-keep public class org.mq.study.webview.DemoJavaScriptInterface{
    public <methods>;
}

如果是内部类
-keepattributes *Annotation*  
-keepattributes *JavascriptInterface*
-keep public class org.mq.study.webview.webview.DemoJavaScriptInterface$InnerClass{
    public <methods>;
}


4、WebView中存在的漏洞，参看：[你不知道的 Android WebView 使用漏洞](https://note.youdao.com/)
```
4、WebView中存在的漏洞，参看：[你不知道的 Android WebView 使用漏洞](https://blog.csdn.net/carson_ho/article/details/64904635)

# 原生扩展View和ViewGroup

引入方式

```java
implementation 'com.google.android.material:material:1.2.1'
```

## ConstraintLayout （约束布局）

```xml
implementation 'androidx.constraintlayout:constraintlayout:2.0.1'  //添加依赖
```

## DrawerLayout（侧滑）

```
<androidx.drawerlayout.widget.DrawerLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        //android:layout_gravity="start" 子控件设置这个属性左边侧滑
        //android:layout_gravity="end" 子控件设置这个属性右边侧滑


</androidx.drawerlayout.widget.DrawerLayout>
    
//禁止手势滑动
mDrawer_layout.setDrawerLockMode(DrawerLayout.LOCK_MODE_LOCKED_CLOSED);

//打开手势滑动
mDrawer_layout.setDrawerLockMode(DrawerLayout.LOCK_MODE_UNLOCKED);

//java代码打开和关闭
mDrawerLayout.openDrawer(GravityCompat.START);  //打开左边
mDrawerLayout.openDrawer(GravityCompat.END);  //打开右边
mDrawerLayout.closeDrawer(GravityCompat.START); //关闭左边
mDrawerLayout.closeDrawer(GravityCompat.END); //关闭右边
mDrawerLayout.closeDrawers(); //关闭所有

//事件监听
        mDrawerLayout.addDrawerListener(new DrawerLayout.DrawerListener() {
            @Override
            public void onDrawerSlide(@NonNull View view, float v) {
                Log.i("---", "滑动中");
            }

            @Override
            public void onDrawerOpened(@NonNull View view) {
                Log.i("---", "打开");
            }

            @Override
            public void onDrawerClosed(@NonNull View view) {
                Log.i("---", "关闭");
            }

            @Override
            public void onDrawerStateChanged(int i) {
                Log.i("---", "状态改变");
            }
        });
```

## NavigationView（滑动菜单）

```xml
<com.google.android.material.navigation.NavigationView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_gravity="start"  //展示在侧滑的左边
            app:menu="@menu/nav_menu"  //下面的菜单项
            app:headerLayout="@layout/nav_head"/>  //头部布局

//nav_menu.xml
<menu xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    tools:ignore="ExtraText">
    用一个group来放item，checkableBehavior设置为single表示为一个组
    <group android:checkableBehavior="single">
        <item
            android:id="@+id/friends"
            android:title="我的好友" />
        <item
            android:id="@+id/mail"
            android:title="我的邮件" />
        <item
            android:id="@+id/location"
            android:title="我的位置" />
    </group>
</menu>

//nav_head.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="180dp">

</androidx.constraintlayout.widget.ConstraintLayout>

//菜单点击事件
//设置默认选中的菜单
mNavigationView.setCheckedItem(R.id.friends);
//给菜单设置监听
        mNavigationView.setNavigationItemSelectedListener(new NavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected( MenuItem item) {
                //关闭弹出菜单
                drawerLayout.closeDrawers();
                return true;
            }
        });
```

## CardView（卡片布局）

```
//常用属性
card_view:cardElevation	阴影的大小
card_view:cardMaxElevation	阴影最大高度
card_view:cardBackgroundColor	卡片的背景色
card_view:cardCornerRadius	卡片的圆角大小
card_view:contentPadding	卡片内容于边距的间隔
card_view:contentPaddingBottom	卡片内容与底部的边距
card_view:contentPaddingTop	卡片内容与顶部的边距
card_view:contentPaddingLeft	卡片内容与左边的边距
card_view:contentPaddingRight	卡片内容与右边的边距
card_view:contentPaddingStart	卡片内容于边距的间隔起始
card_view:contentPaddingEnd	卡片内容于边距的间隔终止
card_view:cardUseCompatPadding	设置内边距，V21+的版本和之前的版本仍旧具有一样的计算方式
card_view:cardPreventCornerOverlap	在V20和之前的版本中添加内边距，这个属性为了防止内容和边角的重叠

<androidx.cardview.widget.CardView
            android:id="@+id/cardview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="14dp"
            app:cardBackgroundColor="@color/colorAccent"
            app:cardCornerRadius="10dp"
            app:cardElevation="5dp"
            app:contentPadding="8dp">
            <!--子布局控件-->
        </androidx.cardview.widget.CardView>
```

## NestedScrollView（滑动）

用于处理滑动嵌套的，滑动冲突替代ScrollView

```xml
<androidx.core.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_behavior="@string/appbar_scrolling_view_behavior">

            //添加子控件
        </androidx.core.widget.NestedScrollView>

layout_behavior这是一个系统behavior, 从字面意思就可以看到, 是为appbar设置滚动动作的一个behavior. 没有这个属性的话, Appbar就是死的, 有了它就有了灵魂
```

## FloatingActionButton（悬浮按钮）

```java
<com.google.android.material.floatingactionbutton.FloatingActionButton
                android:id="@+id/btn_camera_exit"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_alignParentEnd="true"
                android:layout_centerInParent="true"
                android:layout_centerVertical="true"
                android:layout_marginRight="20dp"
                android:layout_marginBottom="20dp"
                android:clickable="true"
                android:focusable="true"
                android:src="@drawable/ftb_photo_exit"
                app:backgroundTint="@color/white"
                app:borderWidth="0.0dip"
                app:elevation="5.0dip"
                app:fabSize="normal"
                app:layout_anchor="@id/container"
                app:layout_anchorGravity="right|bottom"
                app:pressedTranslationZ="10.0dip"
                app:rippleColor="#a6a6a6"
                tools:ignore="UnknownId" />
                
1. app:elevation="8dp"：阴影的高度，elevation是Android5.0中引入的新属性，设置该属性使控件有一个阴影，感觉该控件像是“浮”起来一样，这样达到3D效果。对应的方法：setCompatElevation(float)
2. app:fabSize="normal"：FAB的大小，为normal时，大小为：56 * 56dp ，为mini时，大小为： 40 * 40 dp。
3. app:backgroundTint="#31bfcf"：FAB的背景颜色。
4. app:rippleColor="#e7d16b"：点击FAB时，形成的波纹颜色。
5. app:borderWidth="0dp"：边框宽度，通常设置为0，用于解决Android5.X设备上阴影无法正常显示的问题
6. app:pressedTranslationZ="16dp":点击按钮时，按钮边缘阴影的宽度，通常设置比elevation的数值大!
7. app:maxImageSize="21dp" 设置中心图片的具体大小,不然不管图片多大像素都是24x24dp
8. app:layout_anchor="@id/container" FloatingActionButton   Google推荐是放在CoordinatorLayout里面,也可以在FramLayout
```

## BottomNavigationView（底部导航栏）



## Toolbar

### 介绍
+ Toolbar是谷歌在2014年Google IO 大会上推出的一套全新的设计规范Material Design,在v7包下面
+ 最新androidx在androidx.appcompat.widget.Toolbar包

### ActionBar、TitleBar、ToolBar、StatusBar之间的关系
1. StatusBar
```
StatusBar,也就是状态栏，它处于屏幕的最顶部，正常情况下它是显示的，它和TitleBar和ActionBar、ToolBar之间没有直接的关系。
可设置隐藏、颜色，获取高度等。
```
2. TitleBar
```
TitleBar，也就是标题栏,它紧挨状态栏的下面，正常情况下它的布局和主题样式都是使用系统定义好的，且默认情况下只显示图标和文本,在3.0之前的。
```
3. ActionBar(3.0之后推出)
```java
ActionBar 是android 3.0的推出的，当时Google 想要逐渐改善过去 android 纷乱的界面设计，希望让终端使用者尽可能在 android 手机有个一致的操作体验。
可设置标题、图标、样式、按钮、menu等。

Action bar被包含在所有的使用Theme.Hole主题的Activity（或者是这些Activity的子类）中。

开发API11以下的程序，首先必须在AndroidManifest.xml中指定Application或Activity的theme是Theme.Holo或其子类，否则将无法使用ActionBar。

删除actionbar
方法一：
如果不想用ActionBar，那么只要在theme主题后面" .NoActionBar", 就可以了。
方法二：
在onCreate方法中添加一句代码: 
requestWindowFeature(Window.FEATURE_NO_TITLE);
不过这句代码一定要添加到setContentView(R.layout.activity_main); 之前
方法三：
用getActionBar()/getSupportActionBar()得到ActionBar对象，用对象调用hide()方法；
注意配置清单文件中最低版本改为11以上；

public class MainActivity extends Activity {
    ActionBar  actionBar;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
 
        setContentView(R.layout.activity_main);
        actionBar=getActionBar();
        actionBar.hide();
    }
}
```
4. ToolBar(5.0之后推出，代替ActionBar，推荐)
```java
Toolbar 是android 5.0的推出的，放在了v7包中作为控件，它是为了取代actionbar而产生的.由于ActionBar在各个安卓版本和定制Rom中的效果表现不一，导致严重的碎片化问题，ToolBar应运而生。
优点：自定义视图的操作更加简单，状态栏的颜色可以调（Android 4.4以上）。
setSupportActionBar ，Toolbar即能取代原本的 actionbar 了.

Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
setSupportActionBar(toolbar);

//基本属性
<androidx.appcompat.widget.Toolbar
     android:id="@+id/toolbar"
     android:layout_width="match_parent"
     android:layout_height="?attr/actionBarSize"
     android:background="@color/purple_500"
     android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
     app:popupTheme="@style/ThemeOverlay.AppCompat.Light"   //菜单弹出样式
     app:title="标题"  //显示的标题
     app:logo="@mipmap/ic_launcher" //显示的logo
     app:navigationIcon="@mipmap/ic_launcher_round" //左边显示的图标
     app:titleMarginStart="90dp"  //标题的距离
     app:titleTextAppearance="@style/ToolbarTitle"  //标题的字体属性
     app:titleTextColor="@color/white/>    //标题的颜色
//toolbar作为独立控件点击左边的图标的事件         
toolbar.setNavigationOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this,"33",Toast.LENGTH_SHORT).show();
            }
        });

//菜单栏
1.在res下新建menu文件夹用来存放菜单资源xml
    <item />标签属性
    icon：菜单项图标
    title：菜单项标题
    showAsAction：菜单项展示的位置,五个属性值
always 总是显示在Toolbar上。
ifRoom 如果Toolbar上还有空间，则显示，否则会隐藏在溢出列表中。
never 永远不会显示在Toolbar上，只会在溢出列表中出现。
withText 文字和图标一起显示。
collapseActionView 声明了这个操作视窗应该被折叠到一个按钮中，当用户选择这个按钮时，这个操作视窗展开。一般要配合ifRoom一起使用才会有效
    
2.展示和事件
    Toolbar作为ActionBar使用
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    return super.onOptionsItemSelected(item);
}

     Toolbar作为独立控件使用
toolbar.inflateMenu(R.menu.menu_main);
toolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
    @Override
    public boolean onMenuItemClick(MenuItem item) {
        return true;
    }
});
```

### AppBarLayout和CoordinatorLayout

AppBarLayout是LinearLayout的子类，必须在它的子view上设置app:layout_scrollFlags属性或者是在代码中调用setScrollFlags()设置这个属性。

AppBarLayout的子布局有5种滚动标识：

scroll：所有想滚动出屏幕的view都需要设置这个flag， 没有设置这个flag的view将被固定在屏幕顶部。

enterAlways：这个flag让任意向下的滚动都会导致该view变为可见，启用快速“返回模式”。

enterAlwaysCollapsed：假设你定义了一个最小高度（minHeight）同时enterAlways也定义了，那么view将在到达这个最小高度的时候开始显示，并且从这个时候开始慢慢展开，当滚动到顶部的时候展开完。

exitUntilCollapsed：当你定义了一个minHeight，此布局将在滚动到达这个最小高度的时候折叠。

snap：当一个滚动事件结束，如果视图是部分可见的，那么它将被滚动到收缩或展开。例如，如果视图只有底部25%显示，它将折叠。相反，如果它的底部75%可见，那么它将完全展开。



CoordinatorLayout主要通过Behavior来实现协调者，一般我们会给相应的子View添加一个类似app:layout_behavior="@string/appbar_scrolling_view_behavior"。当然我们这里也可以自定义。

```xml
<androidx.coordinatorlayout.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
 
    <com.google.android.material.appbar.AppBarLayout
        android:id="@+id/appbar_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <androidx.appcompat.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="?attr/colorPrimary"
            app:title="标题"
            app:layout_scrollFlags="scroll|enterAlways"/>
    </com.google.android.material.appbar.AppBarLayout>
 
    <androidx.core.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_behavior="@string/appbar_scrolling_view_behavior">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:lineSpacingMultiplier="2"
                android:text="@string/text" />
        </androidx.core.widget.NestedScrollView>
</androidx.coordinatorlayout.widget.CoordinatorLayout>


```

### CollapsingToolbarLayout

是提供了一个可以折叠的Toolbar，它继承自FrameLayout，给它设置layout_scrollFlags，它可以控制包含在CollapsingToolbarLayout中的控件(如：ImageView、Toolbar)在响应layout_behavior事件时作出相应的scrollFlags滚动事件(移除屏幕或固定在屏幕顶端)。CollapsingToolbarLayout可以通过app:contentScrim设置折叠时工具栏布局的颜色，通过

app:statusBarScrim设置折叠时状态栏的颜色。默认contentScrim是colorPrimary的色值，statusBarScrim是colorPrimaryDark的色值。CollapsingToolbarLayout的子布局有3种折叠模式（Toolbar中设置的app:layout_collapseMode）

```xml
<androidx.coordinatorlayout.widget.CoordinatorLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:fitsSystemWindows="true"
        >

        <com.google.android.material.appbar.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="250dp"
            tools:ignore="MissingConstraints">

            <com.google.android.material.appbar.CollapsingToolbarLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                app:layout_scrollFlags="scroll|exitUntilCollapsed"
                android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
                android:fitsSystemWindows="true"
                app:titleEnabled="false"
                app:contentScrim="@color/purple_700"
                >

                <ImageView
                    android:id="@+id/img_activity_info"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_gravity="center"
                    android:fitsSystemWindows="true"
                    android:scaleType="centerCrop"
                    android:background="@mipmap/ic_launcher"
                    app:layout_collapseMode="parallax"/>


                <androidx.appcompat.widget.Toolbar
                    android:id="@+id/toolbar"
                    android:layout_width="match_parent"
                    android:layout_height="?attr/actionBarSize"
                    app:logo="@mipmap/ic_launcher"
                    app:layout_collapseMode="pin"
                    app:navigationIcon="@mipmap/ic_launcher_round"
                    app:popupTheme="@style/ThemeOverlay.AppCompat.Light"
                    app:title="标题" />
            </com.google.android.material.appbar.CollapsingToolbarLayout>
        </com.google.android.material.appbar.AppBarLayout>

        <androidx.core.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_behavior="@string/appbar_scrolling_view_behavior">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:lineSpacingMultiplier="2"
                android:text="@string/text" />
        </androidx.core.widget.NestedScrollView>
    </androidx.coordinatorlayout.widget.CoordinatorLayout>
```

### [沉浸式效果](https://github.com/laobie/StatusBarUtil)

### [详细使用](https://blog.csdn.net/da_caoyuan/article/details/79557704)

## RecyclerView

### 设置

```java
setLayoutManager(new LinearLayoutManager(context))  //默认条目垂直展示

//修改为水平展示    
LinearLayoutManager layoutManager = new LinearLayoutManager(getActivity());
layoutManager.setOrientation(LinearLayoutManager.VERTICAL);
setLayoutManager(layoutManager);    

//刷新库    
mPullDownLoadView.setRefreshFooter(new ClassicsFooter(context));
mPullDownLoadView.setEnableAutoLoadMore(false);   //取消滚动到底部刷新
mPullDownLoadView.setEnableRefresh(false);
//mPullDownLoadView.setEnableRefresh(false);//是否启用下拉刷新功能
mPullDownLoadView.setOnLoadMoreListener(refreshLayout -> {
           
});    
```

### 布局

```xml
//添加底部刷新和头部刷新
implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.1.0-andx-4'
implementation 'com.scwang.smartrefresh:SmartRefreshHeader:1.1.0-andx-4'

//
<com.scwang.smartrefresh.layout.SmartRefreshLayout
            android:id="@+id/smartRefreshLayout"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_below="@+id/ll_head">

            <androidx.recyclerview.widget.RecyclerView
                android:id="@+id/rv_data_query_show"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:fadeScrollbars="false"
                android:scrollbars="vertical"
                android:scrollbarThumbVertical="@color/login_blue"   <!-- 设置下滑bar展示的颜色 -->
                />

</com.scwang.smartrefresh.layout.SmartRefreshLayout>
```

### SwipeRefreshLayout（下拉刷新）

```
//添加依赖   
implementation "androidx.swiperefreshlayout:swiperefreshlayout:1.0.0"
<androidx.swiperefreshlayout.widget.SwipeRefreshLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">
            
            <androidx.recyclerview.widget.RecyclerView
                android:layout_width="match_parent"
                android:layout_height="match_parent"/>
        </androidx.swiperefreshlayout.widget.SwipeRefreshLayout>

//刷新事件
swip_refresh_layout.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
    @Override
    public void onRefresh() {
        
    }
});    

//修改进度条颜色
swip_refresh_layout.setColorSchemeResources(R.color.colorPrimary);     //转圈圈的颜色 swip_refresh_layout.setProgressBackgroundColorSchemeColor(R.color.colorPrimaryDark); //进度条背景色
```



### 适配器

```java
public class BlueScanAdapter extends RecyclerView.Adapter<BlueScanAdapter.MyViewHolder> {

    private Context context;
    private List<BluetoothDevice> mDatas;


    public BlueScanAdapter(Context context, List<BluetoothDevice> mDatas) {
        this.mDatas = mDatas;
        this.context = context;
    }

    @NonNull
    @Override
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        return new MyViewHolder(LayoutInflater.from(context).inflate(R.layout.activity_blue_scan_sub, parent, false));
    }


    @SuppressLint({"SetTextI18n", "ResourceAsColor"})
    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder, int position) {

    }


    @Override
    public int getItemCount() {
        return mDatas == null ? 0 : mDatas.size();
    }


    public static class MyViewHolder extends RecyclerView.ViewHolder {

        TextView tv_name;
        TextView tv_mac;
        Button btn_connect;

        public MyViewHolder(@NonNull View itemView) {
            super(itemView);

            tv_name = itemView.findViewById(R.id.tv_name);
            tv_mac = itemView.findViewById(R.id.tv_mac);
            btn_connect = itemView.findViewById(R.id.btn_connect);
        }
    }
}
```

