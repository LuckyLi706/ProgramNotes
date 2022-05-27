## Routes

路由（Route）在移动开发中通常指页面（Page），这跟 Web 开发中单页应用的 Route 概念意义是相同的，Route 在 Android中 通常指一个 Activity，在 iOS 中指一个 ViewController。所谓路由管理，就是管理页面之间如何跳转，通常也可被称为导航管理。Flutter 中的路由管理和原生开发类似，无论是 Android 还是 iOS，导航管理都会维护一个路由栈，路由入栈（push）操作对应打开一个新页面，路由出栈（pop）操作对应页面关闭操作。

### 静态路由

MaterialApp组件中有一个字段routes参数来注册路由，但是这里注册的路由是静态的，它不可以向下一个页面传递参数

```dart
//静态注册
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '静态路由',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      /**
      使用routes来定义路由表,这边定义了两个路由页面
      MaterialApp还有一个属性，它就是initRoute，这个属性我们前面的章节也提到过，它指的是App启动的默认路由，也就是主页面，如果你使用了这个属性，那么就不需要指定home
      **/
      routes: {
        "/A": (context) => Apage(),    //跳转到Apage页面
        "/B": (context) => Bpage(),    //跳转到Bpage页面
      },
      onUnknownRoute: (RouteSettings setting){
        String name=setting.name;
        print("没有匹配到路由");
        return new MaterialPageRoute(builder: (context){
          return new ErrorPage(title: "没有匹配的页面",);
        });
      },
      home: Page1(title: "主页面",),
    );
  }
}

//跳转（类似于Android中的startActivity）
Navigator.pushNamed(context, "/A");    //跳转到Apage页面
//Apage的实现内容
class Apage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('解析视频'),
      ),
      body: Center(
        child: RaisedButton(
          child: const Text("跳转到B page"),
          onPressed: () {
            Navigator.pushNamed(context, "/B");    //跳转到Bpage页面
          },
        ),
      ),
    );
  }
}

//Bpage的实现内容
class Bpage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('解析视频'),
      ),
      body: const Center(child: Text("Bpage")),
    );
  }
}
```

#### 带返回值的静态路由

```dart
//类似于Android中的onActivityResult，静态路由不能传递参数给下一个页面，但是可以接收返回参数
Navigator.pushNamed(context, routeName).then((value){
  //可以在这使用返回值value
});

//返回上一个页面（类似于Android中的setResult + finish）
Navigator.of(context).pop('这是要返回给上一个页面的数据');
```

### 动态路由

```dart
//动态路由无需在routes中注册即可直接使用
Navigator.push(context, MaterialPageRoute(builder: (context) {
  return FirstPage(title: '这是要传递给下一个页面的参数');
}));

/**
切换动画
Material库中提供了一个MaterialPageRoute，它可以使用和平台风格一致的路由切换动画，如在iOS上会左右滑动切换，而在Android上会上下滑动切换。如果在Android上也想使用左右切换风格，可以直接使用CupertinoPageRout
**/
Navigator.push(context, new CupertinoPageRoute(builder: (context) {
  return new FirstPage();
}));

//自定义动画，可以使用PageRouteBuilder，例如我们想以渐隐渐入动画来实现路由过渡：
Navigator.push(context, PageRouteBuilder(
      transitionDuration: Duration(milliseconds: 500), //动画时间为500毫秒
      pageBuilder: (BuildContext context, Animation animation,
          Animation secondaryAnimation) {
        return new FadeTransition( //使用渐隐渐入过渡, 
          opacity: animation,
          child: FirstPage() 
        );
      }));
}),

//上面的路由都是继承PageRoute，我们可以直接继承PageRoute类来实现自定义路由
class FadeRoute extends PageRoute {
  FadeRoute({
    @required this.builder,
    this.transitionDuration = const Duration(milliseconds: 300),
    this.opaque = true,
    this.barrierDismissible = false,
    this.barrierColor,
    this.barrierLabel,
    this.maintainState = true,
  });
  final WidgetBuilder builder;
  @override
  final Duration transitionDuration;
  @override
  final bool opaque;
  @override
  final bool barrierDismissible;
  @override
  final Color barrierColor;
  @override
  final String barrierLabel;
  @override
  final bool maintainState;
  @override
  Widget buildPage(BuildContext context, Animation<double> animation,
      Animation<double> secondaryAnimation) => builder(context);
  @override
  Widget buildTransitions(BuildContext context, Animation<double> animation,
      Animation<double> secondaryAnimation, Widget child) {
     return FadeTransition( 
       opacity: animation,
       child: builder(context),
     );
  }
//使用
Navigator.push(context, FadeRoute(builder: (context) {
  return FirstPage();
}));
```

### 入栈和出栈（相关方法）

```dart
/** 
 以下是Flutter出栈和入栈的方法，共计13种，当然也有直接是Navigator.push 之类的对照方法共计13种，他们没什么区别，
 因为Navigator.method()这些方法其实也是调用下面的方法实现的。
 **/


 Navigator.of(context).pushReplacement(newRoute);
 /**
  官方的给的demo
 Navigator.push(context, MaterialPageRoute(builder: (BuildContext context) => MyPage()));
 1、适用非静态路由进行跳转。
 2、传递参数只能通过控制器的构造进行传递。
 **/
 Navigator.of(context).push(route);
 Navigator.of(context).pushReplacementNamed(routeName);
 //类似上面的push方法，不过只能打开静态Route,可以通过args传递参数。
 Navigator.of(context).pushNamed(routeName);
 Navigator.of(context).pushNamedAndRemoveUntil(newRouteName, predicate)
 //关闭一个路由，这里可以是Route也可以是Dialog, pop都是可以向上一层返回数据的。
 Navigator.of(context).pop();
 Navigator.of(context).popAndPushNamed(routeName);
 Navigator.of(context).popUntil(predicate);
 //这个Android 开发者很好理解，这个就是唤醒了一个Android返回物理键，如果当前route 没有WillPopScope（）进行包裹（也即是拦截物理返回键&navigatorBar返回键），他就结束当前route。如果进行了包裹，就不结束当前界面。
 Navigator.of(context).maybePop();

 Navigator.of(context).removeRouteBelow(anchorRoute);
 Navigator.of(context).removeRoute(route);

 Navigator.of(context).replace(oldRoute: null, newRoute: null);
 Navigator.of(context).replaceRouteBelow(anchorRoute: null);
```

