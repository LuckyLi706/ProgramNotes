<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Widgets](#widgets)
  - [MaterialApp](#materialapp)
    - [例子](#%E4%BE%8B%E5%AD%90)
  - [CupertinoApp](#cupertinoapp)
  - [容器类组件](#%E5%AE%B9%E5%99%A8%E7%B1%BB%E7%BB%84%E4%BB%B6)
    - [Scaffold](#scaffold)
      - [AppBar（顶部导航栏）](#appbar%E9%A1%B6%E9%83%A8%E5%AF%BC%E8%88%AA%E6%A0%8F)
      - [BottomNavigationBar（底部导航）](#bottomnavigationbar%E5%BA%95%E9%83%A8%E5%AF%BC%E8%88%AA)
      - [FloatingActionButton（悬浮按钮）](#floatingactionbutton%E6%82%AC%E6%B5%AE%E6%8C%89%E9%92%AE)
      - [Drawer（侧滑栏）](#drawer%E4%BE%A7%E6%BB%91%E6%A0%8F)
      - [例子](#%E4%BE%8B%E5%AD%90-1)
  - [基础类组件](#%E5%9F%BA%E7%A1%80%E7%B1%BB%E7%BB%84%E4%BB%B6)
    - [Text（文本）和RichText（富文本）](#text%E6%96%87%E6%9C%AC%E5%92%8Crichtext%E5%AF%8C%E6%96%87%E6%9C%AC)
    - [Button（按钮）](#button%E6%8C%89%E9%92%AE)
    - [Image（图片）](#image%E5%9B%BE%E7%89%87)
    - [Switch（单选框）](#switch%E5%8D%95%E9%80%89%E6%A1%86)
    - [Checkbox（复选框）](#checkbox%E5%A4%8D%E9%80%89%E6%A1%86)
    - [TextField（输入框）](#textfield%E8%BE%93%E5%85%A5%E6%A1%86)
    - [Form（表单）](#form%E8%A1%A8%E5%8D%95)
    - [LinearProgressIndicator（线性进度条）](#linearprogressindicator%E7%BA%BF%E6%80%A7%E8%BF%9B%E5%BA%A6%E6%9D%A1)
    - [CircularProgressIndicator（圆形进度条）](#circularprogressindicator%E5%9C%86%E5%BD%A2%E8%BF%9B%E5%BA%A6%E6%9D%A1)
  - [布局类](#%E5%B8%83%E5%B1%80%E7%B1%BB)
    - [约束布局](#%E7%BA%A6%E6%9D%9F%E5%B8%83%E5%B1%80)
      - [BoxConstraints](#boxconstraints)
      - [ConstrainedBox](#constrainedbox)
      - [SizedBox](#sizedbox)
      - [UnconstrainedBox](#unconstrainedbox)
    - [线性布局](#%E7%BA%BF%E6%80%A7%E5%B8%83%E5%B1%80)
      - [Row（水平布局）](#row%E6%B0%B4%E5%B9%B3%E5%B8%83%E5%B1%80)
      - [Column（垂直布局）](#column%E5%9E%82%E7%9B%B4%E5%B8%83%E5%B1%80)
    - [弹性布局](#%E5%BC%B9%E6%80%A7%E5%B8%83%E5%B1%80)
      - [Flex](#flex)
      - [Expanded（比例平分）](#expanded%E6%AF%94%E4%BE%8B%E5%B9%B3%E5%88%86)
    - [流式布局](#%E6%B5%81%E5%BC%8F%E5%B8%83%E5%B1%80)
      - [Wrap](#wrap)
      - [Flow](#flow)
    - [层叠布局](#%E5%B1%82%E5%8F%A0%E5%B8%83%E5%B1%80)
      - [Stack](#stack)
      - [Positioned](#positioned)
    - [对齐和相对定位布局](#%E5%AF%B9%E9%BD%90%E5%92%8C%E7%9B%B8%E5%AF%B9%E5%AE%9A%E4%BD%8D%E5%B8%83%E5%B1%80)
      - [Align](#align)
      - [Center](#center)
  - [容器类](#%E5%AE%B9%E5%99%A8%E7%B1%BB)
    - [填充（Padding）](#%E5%A1%AB%E5%85%85padding)
    - [装饰容器（DecoratedBox）](#%E8%A3%85%E9%A5%B0%E5%AE%B9%E5%99%A8decoratedbox)
    - [变换（Transform）](#%E5%8F%98%E6%8D%A2transform)
    - [容器组件（Container）](#%E5%AE%B9%E5%99%A8%E7%BB%84%E4%BB%B6container)
    - [剪裁（Clip）](#%E5%89%AA%E8%A3%81clip)
  - [可滚动组件](#%E5%8F%AF%E6%BB%9A%E5%8A%A8%E7%BB%84%E4%BB%B6)
    - [ScrollBar（滚动条）](#scrollbar%E6%BB%9A%E5%8A%A8%E6%9D%A1)
    - [SingleChildScrollView](#singlechildscrollview)
    - [ListView](#listview)
      - [ListView.builder](#listviewbuilder)
      - [ListView.separated](#listviewseparated)
  - [GridView](#gridview)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Widgets

## 状态管理

### Stateful

Flutter具有响应式编程

```dart
class _CheckBox extends StatefulWidget {   //借助StatefulWidget来管理状态
  @override
  _CheckBoxState createState() {
    return _CheckBoxState();
  }
}

class _CheckBoxState extends State<_CheckBox> {
  bool _isCheck = false;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Checkbox(
        value: _isCheck,
        onChanged: (bool? value) {
          setState(() {     //状态发生改变会调用,同时刷新当前UI
            _isCheck = value!;
          });
        },
      ),
    );
  }
}
```

## MaterialApp

使用纸墨设计（Material Design）风格的应用。里面包含了纸墨设计风格应用所需要的基本控件

```dart
const MaterialApp({
    Key? key,
    this.navigatorKey,
    this.scaffoldMessengerKey,
    this.home,    //应用默认展示的Widget
    Map<String, WidgetBuilder> this.routes = const <String, WidgetBuilder>{},  //应用的顶级导航表格，这个是多页面应用用来控制页面跳转的，类似于网页的网址
    this.initialRoute,   //第一个显示的路由名字，默认值为 Navigator.defaultRouteName  
    this.onGenerateRoute,  //生成路由的回调函数，当导航的命名路由的时候，会使用这个来生成界面
    this.onGenerateInitialRoutes,
    this.onUnknownRoute,
    List<NavigatorObserver> this.navigatorObservers = const <NavigatorObserver>[],
    this.builder,
    this.title = '',   //在安卓任务管理窗口中所显示的应用名字，其他平台无效
    this.onGenerateTitle,
    this.color,   //应用的主要颜色值（primary color），也就是安卓任务管理窗口中所显示的应用颜色
    this.theme,   //应用各种 UI 所使用的主题颜色
    this.darkTheme,
    this.highContrastTheme,
    this.highContrastDarkTheme,
    this.themeMode = ThemeMode.system,
    this.locale,
    this.localizationsDelegates,
    this.localeListResolutionCallback,
    this.localeResolutionCallback,   //获取当前使用的语言，或者切换语言时
    this.supportedLocales = const <Locale>[Locale('en', 'US')],
    this.debugShowMaterialGrid = false,   //是否显示 纸墨设计 基础布局网格，用来调试 UI 的工具
    this.showPerformanceOverlay = false,  //显示性能标签
    this.checkerboardRasterCacheImages = false,   //检查缓存的图像开关，检测在界面重绘时频繁闪烁的图像（调试开关）
    this.checkerboardOffscreenLayers = false,
    this.showSemanticsDebugger = false,   //是否打开Widget边框，类似Android开发者模式中显示布局边界（调试开关）
    this.debugShowCheckedModeBanner = true,  //是否显示右上角DEBUG标签 （调试开关）
    this.shortcuts,
    this.actions,
    this.restorationScopeId,
    this.scrollBehavior,
    this.useInheritedMediaQuery = false,
}   
```

### 例子

```dart
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '333',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: '解析视频'),
      localeResolutionCallback: (deviceLocale, supportedLocales) {   //App启动或者语言切换时都会回调，可以获取当前语言环境
              print(deviceLocale?.languageCode);
              if (deviceLocale != null &&
                  deviceLocale.languageCode == "zh") {
                Constants.isChinese = true;
              } else {
                Constants.isChinese = false;
              }
            },
    );
  }
}
```

## CupertinoApp

Cupertino（ios）风格与之相对应，是的Cupertino风格的是CupertinoApp

## 容器类组件

### Scaffold

Scaffold定义了一个 UI 框架，这个框架包含 头部导航栏，body，右下角浮动按钮，底部导航栏等

```dart
//Scaffold
const Scaffold({
    Key? key,
    this.appBar,    //页面上方导航条
    this.body,   //页面容器
    this.floatingActionButton,  //悬浮按钮
    /**
    FloatingActionButtonLocation.startTop,FloatingActionButtonLocation.miniStartTop 显示在左上角
FloatingActionButtonLocation.endFloat 显示在右下角但是离底部有距离
FloatingActionButtonLocation.endDocked 显示在右下角紧挨着底部
FloatingActionButtonLocation.centerFloat 显示在底部中间但是离底部有距离
FloatingActionButtonLocation.centerDocked 显示在底部中间紧挨着底部
FloatingActionButtonLocation.endTop 显示在右上角 
    **/
    this.floatingActionButtonLocation,  //悬浮按钮位置
    this.floatingActionButtonAnimator,  //移动到一个新的位置时的动画.系统内置了FloatingActionButtonAnimator.scaling动画
    this.persistentFooterButtons,  //在页面的最底部添加按钮，添加底部切换按钮我们使用bottomNavigationBar,所以一般不会去使用persistentFooterButtons
    this.drawer,  //左侧菜单
    this.onDrawerChanged,  
    this.endDrawer,  //右侧菜单
    this.onEndDrawerChanged,
    this.bottomNavigationBar, //底部导航条
    this.bottomSheet,  //一个持久停留在body下方，底部控件上方的控件
    this.backgroundColor,  //背景色
    this.resizeToAvoidBottomInset, //默认为 true，防止一些小组件重复
    this.primary = true,  //是否在屏幕顶部显示Appbar, 默认为 true，Appbar 是否向上延伸到状态栏，如电池电量，时间那一栏
    this.drawerDragStartBehavior = DragStartBehavior.start,  //控制 drawer 的一些特性
    this.extendBody = false,  //body 是否延伸到底部控件
    this.extendBodyBehindAppBar = false,  //默认 false，为 true 时，body 会置顶到 appbar 后，如appbar 为半透明色，可以有毛玻璃效果
    this.drawerScrimColor,  //侧滑栏拉出来时，用来遮盖主页面的颜色
    this.drawerEdgeDragWidth,  //设置可拖拽区域宽度，在区域内才能拖拽出抽屉,设置0.0禁止手势侧滑出Drawer
    this.drawerEnableOpenDragGesture = true,   //左侧侧滑栏是否可以滑动
    this.endDrawerEnableOpenDragGesture = true,  //右侧侧滑栏是否可以滑动
    this.restorationId,
  })
```

#### AppBar（顶部导航栏）

```dart
//AppBar
AppBar({
    Key? key,
    this.leading,  //在标题前面显示的一个控件，在首页通常显示应用的 logo；在其他界面通常显示为返回按钮
    this.automaticallyImplyLeading = true,
    this.title,  //Toolbar 中主要内容，通常显示为当前界面的标题文字。（可以配合TabBar来实现顶部导航栏）
    this.actions, //一个 Widget 列表，代表 Toolbar 中所显示的菜单，对于常用的菜单，通常使用 IconButton 来表示；对于不常用的菜单通常使用 PopupMenuButton 来显示为三个点，点击后弹出二级菜单。
    this.flexibleSpace, //一个显示在 AppBar 下方的控件，高度和 AppBar 高度一样，可以实现一些特殊的效果，该属性通常在 SliverAppBar 中使用
    this.bottom,  //一个 AppBarBottomWidget 对象，通常是 TabBar。用来在 Toolbar 标题下面显示一个 Tab 导航栏。
    this.elevation, //控件的 z 坐标顺序，默认值为 4，对于可滚动的 SliverAppBar，当 SliverAppBar 和内容同级的时候，该值为 0， 当内容滚动SliverAppBar 变为 Toolbar 的时候，修改 elevation 的值。
    this.shadowColor,
    this.shape,
    this.backgroundColor,  //Appbar 的颜色，默认值为 ThemeData.primaryColor。改值通常和下面的三个属性一起使用。
    this.foregroundColor,
    @Deprecated(
      'This property is no longer used, please use systemOverlayStyle instead. '
      'This feature was deprecated after v2.4.0-0.0.pre.',
    )
    this.brightness,  //Appbar 的亮度，有白色和黑色两种主题，默认值为 ThemeData.primaryColorBrightness。
    this.iconTheme,   //Appbar 上图标的颜色、透明度、和尺寸信息。默认值为 ThemeData.primaryIconTheme
    this.actionsIconTheme,
    @Deprecated(
      'This property is no longer used, please use toolbarTextStyle and titleTextStyle instead. '
      'This feature was deprecated after v2.4.0-0.0.pre.',
    )
    this.textTheme,  //TextTheme - Appbar 上的文字样式。
    this.primary = true,
    this.centerTitle, //标题是否居中显示，默认值根据不同的操作系统，显示方式不一样
    this.excludeHeaderSemantics = false,
    this.titleSpacing,
    this.toolbarOpacity = 1.0,
    this.bottomOpacity = 1.0,
    this.toolbarHeight,  //Appbar的高度
    this.leadingWidth,
    @Deprecated(
      'This property is obsolete and is false by default. '
      'This feature was deprecated after v2.4.0-0.0.pre.',
    )
    this.backwardsCompatibility,
    this.toolbarTextStyle,
    this.titleTextStyle,
    this.systemOverlayStyle,
  })
    
//顶部导航的实现（TabBar+TabBarView）
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: TabBar(
          tabs: [
            //指定两个Tab
            Tab(   
              text: "Android",
            ),
            Tab(
              text: "IOS",
            ),
          ],
          controller: tabController,
        ),
      ),
      body: TabBarView(
        physics: NeverScrollableScrollPhysics(),
        children: [AndroidRightPanel(), IOSRightPanel()],   //两个Tab对应的内容
        controller: tabController,
      ),
    );
  }
}
```

#### BottomNavigationBar（底部导航）

```dart
//BottomNavigationBar（底部导航栏）
BottomNavigationBar({
    Key? key,
    required this.items,   //底部导航栏的展示，List<BottomNavigationBarItem>
    this.onTap,   //
    this.currentIndex = 0,  //当前选中 item 下标
    this.elevation, //控制阴影高度，默认为 8.0
    this.type,  //BottomNavigationBarType，默认 fixed，设置为 shifting 时，建议设置选中样式，和为选中样式，提供一个特殊动画
    Color? fixedColor,  //选中 item 填充色
    this.backgroundColor, //整个 BottomNavigationBar 背景色
    this.iconSize = 24.0,  //图标大小，默认 24.0
    Color? selectedItemColor,  //选中 title 填充色
    this.unselectedItemColor,  //未选中 title 填充色
    this.selectedIconTheme,   //选中 item 图标主题
    this.unselectedIconTheme,  //未item 图标主题
    this.selectedFontSize = 14.0,  //选中 title 字体大小，默认14.0
    this.unselectedFontSize = 12.0,   //未选中 title 字体大小，默认12.0
    this.selectedLabelStyle,  //选中 title 样式 TextStyle
    this.unselectedLabelStyle,  //未选中 title 样式 TextStyle
    this.showSelectedLabels,  //是否展示选中 title，默认为true
    this.showUnselectedLabels,  //是否展示未选中 title，默认为true
    this.mouseCursor,   //鼠标悬停，Web 开发可以了解
    this.enableFeedback,
    this.landscapeLayout,
  })
```

#### FloatingActionButton（悬浮按钮）

```
//FloatingActionButton（悬浮按钮）
const FloatingActionButton({
    Key? key,
    this.child,    //子控件，通常为 Icon
    this.tooltip,  //长按时显示的提示语
    this.foregroundColor,   //Icon 与 Text 颜色
    this.backgroundColor,   //背景色
    this.focusColor,   //聚焦色
    this.hoverColor,   //悬浮色
    this.splashColor,  //点击时的颜色
    this.heroTag = const _DefaultHeroTag(),  //标记
    this.elevation,   //阴影高度
    this.focusElevation,  //聚焦时阴影高度
    this.hoverElevation,  //悬浮时阴影高度
    this.highlightElevation,   //高亮时阴影高度
    this.disabledElevation,    //不可用时阴影高度
    required this.onPressed,  //点击事件
    this.mouseCursor,   //鼠标悬停，Web可以了解
    this.mini = false,  //默认 false，默认按钮为 56 * 56，当mini 为 true 时，默认大小为 40 * 40，边框padding 各为 4，所以布局大小为 48 * 48
    this.shape,  //自定义形状
    this.clipBehavior = Clip.none,  //边缘裁剪方式，默认为 Clip.none
    this.focusNode,   //焦点节点，例如监听 focusNode 可以实现输入框的开始、结束输入
    this.autofocus = false,  //自动聚焦，默认为 false
    this.materialTapTargetSize,  //点击区域大小，MaterialTapTargetSize.padded时最小点击区域为48*48，MaterialTapTargetSize.shrinkWrap 时为子组件的实际大小。
    this.isExtended = false, //默认为 false，当使用 extended 方法时为 true
    this.enableFeedback,
  })
```

#### Drawer（侧滑栏）

```dart
//Drawer（侧滑栏）
//如果没有设置AppBar的leading属性，则当使用Drawer的时候会自动显示一个IconButton来告诉用户有侧边栏（在 Android 上通常是显示为三个横的图标）。
```

#### 例子

```dart
class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key, required this.title}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _selectedIndex = 0;

  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  void _onAdd() {

  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      extendBodyBehindAppBar: true,
      drawer: SizedBox(
        child: Drawer(child: HomeBuilder.homeDrawer()), //设置侧滑栏的宽度
        width: 600,
      ),
      drawerEdgeDragWidth: 200,
      bottomNavigationBar: BottomNavigationBar(
        // 底部导航
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(
              icon: Icon(Icons.business), label: 'Business'),
          BottomNavigationBarItem(icon: Icon(Icons.school), label: 'School'),
        ],
        currentIndex: _selectedIndex,
        fixedColor: Colors.blue,
        onTap: _onItemTapped,
      ),
      floatingActionButton: FloatingActionButton(
          //悬浮按钮
          child: const Icon(Icons.add),
          onPressed: _onAdd),
      appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        actions: <Widget>[
          //导航栏右侧菜单
          IconButton(icon: const Icon(Icons.share), onPressed: () {}),
        ],
      ),
      body: const Center(   //设置中间的内容

      ),
    );
  }
}

//侧滑栏显示的内容
class HomeBuilder {
  static Widget homeDrawer() {
    return ListView(padding: const EdgeInsets.only(), children: <Widget>[
      _drawerHeader(),
      ClipRect(
        child: ListTile(
          leading: const CircleAvatar(child: Text("A")),
          title: const Text('Drawer item A'),
          onTap: () => {},
        ),
      ),
      ListTile(
        leading: const CircleAvatar(child: Text("B")),
        title: const Text('Drawer item B'),
        subtitle: const Text("Drawer item B subtitle"),
        onTap: () => {},
      ),
      AboutListTile(
        icon: const CircleAvatar(child: Text("Ab")),
        child: const Text("About"),
        applicationName: "Test",
        applicationVersion: "1.0",
        applicationIcon: Image.asset(
          "images/ymj_jiayou.gif",
          width: 64.0,
          height: 64.0,
        ),
        applicationLegalese: "applicationLegalese",
        aboutBoxChildren: const <Widget>[
          Text("BoxChildren"),
          Text("box child 2")
        ],
      ),
    ]);
  }

  static Widget _drawerHeader() {
    return UserAccountsDrawerHeader(
//      margin: EdgeInsets.zero,
      accountName: Text(
        "SuperLuo",
        // style: HStyle.titleNav(),
      ),
      accountEmail: Text(
        "super_luo@163.com",
        //  style: HStyle.bodyWhite(),
      ),
      currentAccountPicture: const CircleAvatar(
          // backgroundImage: AssetImage("images/ymj_jiayou.gif"),
          ),
      onDetailsPressed: () {},
      otherAccountsPictures: const <Widget>[
        CircleAvatar(
            // backgroundImage: AssetImage("images/ymj_shuijiao.gif"),
            ),
      ],
    );
  }
}
```

## 基础类组件

### Text（文本）和RichText（富文本）

```dart
const Text(
    String this.data, {
    Key? key,
    this.style,
    this.strutStyle,
    /**
    TextAlign.center	将文本对齐容器的中心。
TextAlign.end	对齐容器后缘上的文本。
TextAlign.start	对齐容器前缘上的文本。
TextAlign.justify	拉伸以结束的文本行以填充容器的宽度。即使用了decorationStyle才起效
TextAlign.left	对齐容器左边缘的文本。
TextAlign.right	对齐容器右边缘的文本。
    **/
    this.textAlign,   //对齐方式
    /**
    相对TextAlign中的start、end而言有用（当start使用了ltr相当于end使用了rtl，也相当于TextAlign使用了left）
    TextDirection.ltr	ltr从左至右，
TextDirection.rtl	rtl从右至左
    **/
    this.textDirection,
    this.locale,
    this.softWrap,   //是否自动换行（true自动换行，false单行显示，超出屏幕部分默认截断处理）
    /**
    TextOverflow.clip	剪切溢出的文本以修复其容器。
TextOverflow.ellipsis	使用省略号表示文本已溢出。
TextOverflow.fade	将溢出的文本淡化为透明。
    **/
    this.overflow,   //文字超出屏幕之后的处理方式
    this.textScaleFactor,  //字体显示倍率
    this.maxLines,   //文字显示最大行数
    this.semanticsLabel,
    this.textWidthBasis,
    this.textHeightBehavior,
  }) 
    
const TextStyle({
    this.inherit = true,
    this.color,     //字体颜色 如自定义颜色：Color.fromRGBO(155, 155, 155, 1) 也可以使用Colors类里面自带的属性
    this.backgroundColor,  //文本的背景颜色
    this.fontSize,    //字体大小，默认14像素
    /**
字体厚度，可以使文本变粗或变细
FontWeight.bold 常用的字体重量比正常重。即w700
FontWeight.normal 默认字体粗细。即w400
FontWeight.w100 薄，最薄
FontWeight.w200 特轻
FontWeight.w300 轻
FontWeight.w400 正常/普通/平原
FontWeight.w500 较粗
FontWeight.w600 半粗体
FontWeight.w700 加粗
FontWeight.w800 特粗
FontWeight.w900 最粗
    **/
    this.fontWeight,  //字体厚度
    /**
    字体变体：
FontStyle.italic 使用斜体
FontStyle.normal 使用直立
    **/
    this.fontStyle,  //字体变体
    this.letterSpacing,   //水平字母之间的空间间隔（逻辑像素为单位）。可以使用负值来让字母更接近。
    this.wordSpacing,     //单词之间添加的空间间隔（逻辑像素为单位）。可以使用负值来使单词更接近。
    /**
    对齐文本的水平线:
TextBaseline.alphabetic：文本基线是标准的字母基线
TextBaseline.ideographic：文字基线是表意字基线；
如果字符本身超出了alphabetic 基线，那么ideograhpic基线位置在字符本身的底部。
    **/
    this.textBaseline,    //对齐文本的水平线
    this.height,     //文本行与行的高度，作为字体大小的倍数（取值1~2，如1.2）
    this.leadingDistribution,   //
    this.locale,   
    this.foreground,  //文本的前景色，不能与color共同设置（比文本颜色color区别在Paint功能多，后续会讲解）
    this.background,   //文本背景色Paint()…color = backgroundColor
    this.shadows,   //文本的阴影可以利用列表叠加处理，例如shadows: [Shadow(color:Colors.black,offset: Offset(6, 3), blurRadius: 10)], color即阴影的颜色， offset即阴影相对文本的偏移坐标，blurRadius即阴影的模糊程度，越小越清晰
    this.fontFeatures,
    this.decoration,   //文字的线性装饰，比如 TextDecoration.underline 下划线， TextDecoration.lineThrough删除线
    this.decorationColor,  //文本装饰线的颜色
    this.decorationStyle,  //文本装饰线的样式，比如 TextDecorationStyle.dashed 虚线
    this.decorationThickness,
    this.debugLabel,
    String? fontFamily,
    List<String>? fontFamilyFallback,
    String? package,
    this.overflow,
  })
    
//一个富文本Text，可以显示多种样式的text。这个组件跟Text.rich()差不多
RichText({
    Key? key,
    @required this.text,//显示文本的组件
    this.textAlign = TextAlign.start,//对齐方式
    this.textDirection,//文本的方向
    this.softWrap = true,//文本是否应该在软换行处换行
    this.overflow = TextOverflow.clip,//溢出处理方式
    this.textScaleFactor = 1.0,//每个逻辑像素的字体像素数
    this.maxLines,//最大行数
    this.locale,
    this.strutStyle,//strut样式
    this.textWidthBasis = TextWidthBasis.parent,//文本的宽度
    this.textHeightBehavior,
  })
    
const TextSpan({
    this.text,   //String类型的文本
    this.children,  //子组件
    TextStyle? style,  //TextStyle类型的文本样式可以设置文字的大小、颜色、样式等
    this.recognizer,   //指定手势交互recognizer: TapGestureRecognizer()..onTap = () {},可以监听点击事件
    MouseCursor? mouseCursor,
    this.onEnter,
    this.onExit,
    this.semanticsLabel,
    this.locale,
    this.spellOut,
  }) 
```

### Button（按钮）

```dart
//普通按钮
const TextButton({
    Key? key,
    required VoidCallback? onPressed,    //点击事件监听
    VoidCallback? onLongPress,      //长按事件监听
    ValueChanged<bool>? onHover,   //鼠标悬停时回调
    ValueChanged<bool>? onFocusChange,   //焦点改变时的回调
    ButtonStyle? style,
    FocusNode? focusNode,
    bool autofocus = false,
    Clip clipBehavior = Clip.none,
    required Widget child,
  })

//带有外边框的按钮    
const OutlinedButton({
    Key? key,
    required VoidCallback? onPressed,
    VoidCallback? onLongPress,
    ValueChanged<bool>? onHover,
    ValueChanged<bool>? onFocusChange,
    ButtonStyle? style,
    FocusNode? focusNode,
    bool autofocus = false,
    Clip clipBehavior = Clip.none,
    required Widget child,
  })

//浮起来的按钮    
const ElevatedButton({
    Key? key,
    required VoidCallback? onPressed,
    VoidCallback? onLongPress,
    ValueChanged<bool>? onHover,
    ValueChanged<bool>? onFocusChange,
    ButtonStyle? style,
    FocusNode? focusNode,
    bool autofocus = false,
    Clip clipBehavior = Clip.none,
    required Widget? child,
  }) 

//图标按钮
const IconButton({
    Key? key,
    this.iconSize,
    this.visualDensity,
    this.padding = const EdgeInsets.all(8.0),
    this.alignment = Alignment.center,
    this.splashRadius,
    this.color,
    this.focusColor,   //获取焦点时按钮颜色
    this.hoverColor,  //当指针悬停在按钮上时的填充颜色
    this.highlightColor,  //水波纹的高亮颜色
    this.splashColor,  //水波纹效果的初始化颜色
    this.disabledColor,    //禁用按钮时颜色
    required this.onPressed,
    this.mouseCursor,
    this.focusNode,
    this.autofocus = false,
    this.tooltip,
    this.enableFeedback = true,
    this.constraints,
    required this.icon,
  }) 
    
//按钮样式 
const ButtonStyle({
    this.textStyle,
    this.backgroundColor,   //按钮背景色
    this.foregroundColor,
    this.overlayColor,  //水波纹颜色
    this.shadowColor,  //阴影的颜色
    this.elevation,   //阴影高度
    this.padding,  //内间距
    this.minimumSize,  //按钮的大小
    this.fixedSize,
    this.maximumSize,
    this.side,   //边框
    this.shape,  //边框样式
    this.mouseCursor,
    this.visualDensity,
    this.tapTargetSize,
    this.animationDuration,
    this.enableFeedback,
    this.alignment,
    this.splashFactory,
  });    
```

### Image（图片）

```dart
/**
Image组件的构造方法：

1、Image：通过ImageProvider来加载图片
2、Image.asset：用来加载本地资源图片
3、Image.file：用来加载本地（File文件）图片
4、Image.network：用来加载网络图片
5、Image.memory：用来加载Uint8List资源（byte数组）图片
**/
Image.network(
    String src, {
    Key? key,
    double scale = 1.0,
    this.frameBuilder,
    this.loadingBuilder,
    this.errorBuilder,
    this.semanticLabel,
    this.excludeFromSemantics = false,
    this.width,   //指定显示图片区域的宽(不是指图片的宽)	
    this.height,  //指定显示图片区域的高(不是指图片的高)	
    this.color,  //和colorBlendMode两个属性需要配合使用，就是颜色和图片混合	
    this.opacity,
    this.colorBlendMode,
    /**
    BoxFit.contain
全图居中显示但不充满，显示原比例
BoxFit.cover
图片可能拉伸，也可能裁剪，但是充满容器
BoxFit.fill
全图显示且填充满，图片可能会拉伸
BoxFit.fitHeight
图片可能拉伸，可能裁剪，高度充满
BoxFit.fitWidth
图片可能拉伸，可能裁剪，宽度充满
BoxFit.scaleDown
效果和contain差不多， 但是只能缩小图片，不能放大图片
    **/
    this.fit,   //属性用来控制图片的拉伸和挤压，这都是根据父容器来	
    /**
    //如果图片没有填充满容器的话，图片的对齐方式，值为一个 AlignmentGeometry 对象，Alignment 是它的一个实现类
            //可选值同 Container 的 Alignment 取值一样。
            //Alignment.topLeft：垂直靠顶部水平靠左对齐
            //Alignment.topCenter：垂直靠顶部水平居中对齐
            //Alignment.topRight：垂直靠顶部水平靠右对齐
            //Alignment.centerLeft：垂直居中水平靠左对齐
            //Alignment.center：垂直和水平居中都对齐
            //Alignment.centerRight：垂直居中水平靠右对齐
            //Alignment.bottomLeft：垂直靠底部水平靠左对齐
            //Alignment.bottomCenter：垂直靠底部水平居中对齐
            //Alignment.bottomRight：垂直靠底部水平靠右对齐
            //除了上面的常量之外，还可以创建 Alignment 对象指定 x、y 偏移量
    **/
    this.alignment = Alignment.center,   //设置对齐方式, 跟container 里面对齐方式一样
    /**
    ImageRepeat.noRepeat	不重复
ImageRepeat.repeat	X、Y 轴都重复
ImageRepeat.repeatX	只在 X 轴重复
ImageRepeat.repeatY	只在 Y 轴重复
    **/
    this.repeat = ImageRepeat.noRepeat,  //设置图片重复显示	
    this.centerSlice,
    this.matchTextDirection = false,
    this.gaplessPlayback = false,
    this.filterQuality = FilterQuality.low,
    this.isAntiAlias = false,
    Map<String, String>? headers,
    int? cacheWidth,
    int? cacheHeight,
  })
```

### Switch（单选框）

```dart
const Switch({
    Key? key,
    required this.value,     //默认是否选中
    required this.onChanged, //选中状态改变时的事件
    this.activeColor,   //打开状态下滑块颜色
    this.activeTrackColor,   //打开状态下轨道颜色
    this.inactiveThumbColor,  //关闭状态下滑块颜色
    this.inactiveTrackColor,   //关闭状态下轨道颜色
    this.activeThumbImage,    //打开状态下滑块图片
    this.onActiveThumbImageError,   //打开状态下滑块图片加载失败回调
    this.inactiveThumbImage,    //关闭状态下滑块图片
    this.onInactiveThumbImageError,   //关闭状态下滑块图片加载失败回调
    this.thumbColor,  //滑块颜色
    this.trackColor,  //轨道颜色
    this.materialTapTargetSize,  //内边距，默认最小点击区域为 48 * 48，MaterialTapTargetSize.shrinkWrap 为组件实际大小
    this.dragStartBehavior = DragStartBehavior.start,  //启动阻力，默认为 DragStartBehavior.start
    this.mouseCursor,  //鼠标光标
    this.focusColor,  //聚焦颜色
    this.hoverColor,  //悬停颜色
    this.overlayColor,
    this.splashRadius,
    this.focusNode,  //焦点控制，Flutter 组件之 FocusNode 详解
    this.autofocus = false,  //自动聚焦，默认为 false
  })
```

### Checkbox（复选框）

```dart
const Checkbox({
    Key? key,
    required this.value,
    this.tristate = false,   //默认false，如果为true，复选框的值可以为true、false或null。
    required this.onChanged,
    this.mouseCursor,
    this.activeColor,  //选中此复选框时要使用的颜色
    this.fillColor,
    this.checkColor,
    this.focusColor,
    this.hoverColor,
    this.overlayColor,
    this.splashRadius,
    this.materialTapTargetSize,
    this.visualDensity,
    this.focusNode,
    this.autofocus = false,
    this.shape,
    this.side,
  })

//自带标题和副标题CheckboxListTile复选框
const CheckboxListTile({
    Key? key,
    required this.value,
    required this.onChanged,
    this.activeColor,
    this.checkColor,
    this.tileColor,
    this.title,    //列表主标题
    this.subtitle,   //列表副标题
    this.isThreeLine = false,
    this.dense,   //此列表平铺是否是垂直密集列表的一部分。
    this.secondary,  //显示在复选框前面的小部件
    this.selected = false,   //选中后文字高亮，默认false
    this.controlAffinity = ListTileControlAffinity.platform,   //控件相对于文本的位置，默认ListTileControlAffinity.platform
    this.autofocus = false,
    this.contentPadding,
    this.tristate = false,
    this.shape,
    this.selectedTileColor,
    this.side,
    this.visualDensity,
    this.focusNode,
    this.enableFeedback,
  })
```

### TextField（输入框）

```dart
const TextField({
    Key? key,
    this.controller,    //控制器，可以控制 textField 的输入内容，也可以监听 textField 改变
    this.focusNode,     //焦点控制
    this.decoration = const InputDecoration(),  //textField 装饰
    TextInputType? keyboardType,    //TextInputType，键盘类型
    this.textInputAction,   //键盘完成按钮样式
    this.textCapitalization = TextCapitalization.none,  //大小写，默认为 TextCapitalization.none
    this.style,    //字体样式
    this.strutStyle,  //字体的布局样式
    this.textAlign = TextAlign.start,   //文字对齐方式，默认为 TextAlign.start
    this.textAlignVertical,   //文字纵轴对齐方式
    this.textDirection,   //TextDirection.ltr 是居左，TextDirection.rtl 是居右，和 textAlign 效果一致
    this.readOnly = false,   //只读属性，默认为 false
    ToolbarOptions? toolbarOptions,  //长按时弹出的按钮设置，（如赋值，粘贴，全部选中等）
    this.showCursor,   //是否显示光标，默认为 true
    this.autofocus = false,   //是否自动聚焦，默认为 false
    this.obscuringCharacter = '•',   //加密输入时的替换字符，默认为 '•'
    this.obscureText = false,   //是否加密，默认为 false
    this.autocorrect = true,   //是否自动更正，默认为 true
    SmartDashesType? smartDashesType,  //SmartDashesType 智能替换破折号，例如连续输入三个'-' 会自动替换成一个'——'，当 obseretext == true 时，smartDashesType 默认不可用
    SmartQuotesType? smartQuotesType,  //SmartQuotesType 智能替换引号，根据文字情况智能替换为左引号或者右引号，当 obseretext == true 时，SmartQuotesType 默认不可用
    this.enableSuggestions = true,  //是否在用户输入时显示输入建议，此标志仅影响Android，默认为 true
    this.maxLines = 1,   //最大行数
    this.minLines,     //最小行数
    this.expands = false,    //是否填充父控件，默认为 false
    this.maxLength,    //最大长度
    @Deprecated(
      'Use maxLengthEnforcement parameter which provides more specific '
      'behavior related to the maxLength limit. '
      'This feature was deprecated after v1.25.0-5.0.pre.',
    )
    this.maxLengthEnforced = true,   //是否强制限制，或者只提供字符计数器和警告，默认为 true
    this.maxLengthEnforcement,    
    this.onChanged,   //输入框文字改变回调
    this.onEditingComplete,  //输入框完成回调
    this.onSubmitted,   //提交按钮点击回调
    this.onAppPrivateCommand, 
    this.inputFormatters,   //格式化输入，注意这里比 onChanged 先执行
    this.enabled,   //是否可用
    this.cursorWidth = 2.0,  //光标宽度，默认为 2.0
    this.cursorHeight,    //光标高度
    this.cursorRadius,   //光标圆角 
    this.cursorColor,    //光标颜色
    this.selectionHeightStyle = ui.BoxHeightStyle.tight,   //选中高度样式，默认为 ui.BoxHeightStyle.tight
    this.selectionWidthStyle = ui.BoxWidthStyle.tight,     //选中宽度样式，默认为 ui.BoxWidthStyle.tight
    this.keyboardAppearance,    //键盘外观，此设置仅适用于iOS设备，iOS的白色以及黑色风格键盘
    this.scrollPadding = const EdgeInsets.all(20.0),   //滚动后距离边缘的距离，默认为 EdgeInsets.all(20.0)
    this.dragStartBehavior = DragStartBehavior.start,  //启动阻力，默认为 DragStartBehavior.start
    this.enableInteractiveSelection = true,   //默认为True，如果为false，则大多数辅助功能支持选择文本、复制和粘贴，移动插入符号将被禁用。
    this.selectionControls,  
    this.onTap,    //点击事件
    this.mouseCursor,   //鼠标悬停，Web可以了解
    this.buildCounter,  //InputDecorator.counter 自定义小工具
    this.scrollController,  //滚动控制器
    this.scrollPhysics,     //滚动物理效果
    this.autofillHints = const <String>[],   //自动填充
    this.clipBehavior = Clip.hardEdge,
    this.restorationId,
    this.enableIMEPersonalizedLearning = true,
  }) 
    
const InputDecoration({
    this.icon,     //位于输入框外侧坐标的图标
    this.iconColor,
    this.label,
    this.labelText,   //提示语,位于输入框上方
    this.labelStyle,  //提示语样式 TextStyle
    this.floatingLabelStyle,
    this.helperText,   //辅助文本，位于输入框下方，errorText 为空时显示
    this.helperStyle,  //辅助文本样式 TextStyle
    this.helperMaxLines,   //辅助文本最大展示行数
    this.hintText,    //占位文本，位于输入框光标后，输入内容为空时展示
    this.hintStyle,   //占位文本样式 TextStyle
    this.hintTextDirection,    //
    this.hintMaxLines,   //占位文本最大展示行数
    this.errorText,   //错误文本，位于输入框下方
    this.errorStyle,  //错误文本样式 TextStyle
    this.errorMaxLines,  //错误文本最大展示行数
    //floatingLabelBehavior auto : labelText 显示在输入框中，当开始输入时，会有一个动画，字体变小并显示在输入框上方。 never : labelText 显示在输入框中，当开始输入时，labelText 隐藏。 always: LabelText 永远显示在最上方。
    this.floatingLabelBehavior,
    this.floatingLabelAlignment,
    this.isCollapsed = false,  //是否为InputDecoration.collapsed，默认为 false，为true时，需要使用
    this.isDense,   //输入框是否为密集形式，默认为false
    this.contentPadding,   //内间距，默认值与 border 以及 isDense 有关，下方会贴源码备注
    this.prefixIcon,   //头部图标，位于输入框内部最左侧
    this.prefixIconConstraints,   //头部图标盒约束，效果不是很明显
    this.prefix,   //头部组件 Widget，位于光标左侧，与 prefixText 不能同时使用
    this.prefixText,   //头部文本，位于光标左侧，与 prefix 不能同时使用
    this.prefixStyle,  //头部文本样式 TextStyle
    this.prefixIconColor, //尾部图标，位于输入框内部最右侧
    this.suffixIcon,  //尾部组件 Widget，位于输入框右侧，与 suffixText 不能同时使用
    this.suffix,  
    this.suffixText,  //尾部文本，位于输入框右侧，与 suffix 不能同时使用 
    this.suffixStyle,  //尾部文本样式 TextStyle
    this.suffixIconColor,
    this.suffixIconConstraints,  //尾部图标盒约束，效果不是很明显
    this.counter,   //备注组件 Widget，位于输入框右下角外侧，与 counterText 不能同时使用
    this.counterText,  //备注文本，位于输入框右下角外侧，与 counter 不能同时使用
    this.counterStyle,  //备注文本样式 TextStyle
    this.filled,    //是否填充
    this.fillColor,   //填充色
    this.focusColor,   //聚焦色
    this.hoverColor,   //鼠标悬停色
    this.errorBorder,  //错误边框，errorText不为空，输入框没有焦点时显示
    this.focusedBorder,  //输入框开始输入时的边框，errorText为空时生效
    this.focusedErrorBorder,    //errorText不为空时，输入框有焦点时的边框
    this.disabledBorder,   //输入框禁用时的边框，errorText为空时生效
    this.enabledBorder,    //输入框可用时的边框，errorText为空时生效
    this.border,   //边框
    this.enabled = true,   //输入框是否可用，默认为 true
    this.semanticCounterText,  
    this.alignLabelWithHint,    //当 textField 为多行时，居中对齐行为，默认为 false
    this.constraints,
  }) 
```

### Form（表单）

### LinearProgressIndicator（线性进度条）

```dart
const LinearProgressIndicator({
    Key? key,
    double? value,  //具体进度值，取值范围0-1
    Color? backgroundColor,  //背景色
    Color? color,  
    Animation<Color?>? valueColor,  //进度条指示器的颜色值
    this.minHeight,  //最小高度
    String? semanticsLabel,
    String? semanticsValue,
  }) 
```

### CircularProgressIndicator（圆形进度条）

```dart
const CircularProgressIndicator({
    Key? key,
    double? value,
    Color? backgroundColor,
    Color? color,
    Animation<Color?>? valueColor,
    this.strokeWidth = 4.0,
    String? semanticsLabel,
    String? semanticsValue,
  }) 
```

## 布局类

### 约束布局

#### BoxConstraints

BoxConstraints 是盒模型布局过程中父渲染对象传递给子渲染对象的约束信息，包含最大宽高信息，子组件大小需要在约束的范围内

```dart
/**
首先，上层 widget 向下层 widget 传递约束条件。
然后，下层 widget 向上层 widget 传递大小信息。
最后，上层 widget 决定下层 widget 的位置。


**/

const BoxConstraints({
  this.minWidth = 0.0, //最小宽度
  this.maxWidth = double.infinity, //最大宽度，double.infinity为有多大就设置多大
  this.minHeight = 0.0, //最小高度
  this.maxHeight = double.infinity //最大高度，double.infinity为有多大就设置多大
})
```

#### ConstrainedBox

```dart
ConstrainedBox({
    Key? key,
    required this.constraints,   //BoxConstraints对象
    Widget? child,
  }) 
```

#### SizedBox

SizedBox用于给子元素指定固定的宽高

```dart
const SizedBox({ 
    Key? key, 
    this.width,    //宽 
    this.height,   //高
    Widget? child  //子元素，可以不指定子元素，相当于指定的宽和高的空隙
})
```

#### UnconstrainedBox

去除父限制

```dart
/**
如果没有中间的UnconstrainedBox，那么根据上面所述的多重限制规则，那么最终将显示一个90×100的红色框。但是由于UnconstrainedBox “去除”了父ConstrainedBox的限制，则最终会按照子ConstrainedBox的限制来绘制redBox，即90×20
**/
ConstrainedBox(
  constraints: BoxConstraints(minWidth: 60.0, minHeight: 100.0),  //父
  child: UnconstrainedBox( //“去除”父级限制
    child: ConstrainedBox(
      constraints: BoxConstraints(minWidth: 90.0, minHeight: 20.0),//子
      child: redBox,
    ),
  )
)

//定义一个redBox，它是一个背景颜色为红色的盒子，不指定它的宽度和高度
Widget redBox = DecoratedBox(
  decoration: BoxDecoration(color: Colors.red),
);
```

### 线性布局

#### Row（水平布局）

```dart
Row({
    Key? key,
    /**
   主轴的排序方式
MainAxisAlignment.start主轴顶部(默认X轴左边)
MainAxisAlignment.end主轴底部(默认X轴右边)
MainAxisAlignment.center主轴中间(默认X轴轴中间)
MainAxisAlignment.spaceBetween 间距相同 首尾没有间距
MainAxisAlignment.spaceAround子元素平均充满
MainAxisAlignment.spaceEvenly间距相同 首尾有间距
    **/
    MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
    /**
MainAxisSize.min容器空间需要根据内容的大小而撑开的时候用
MainAxisSize.max则相反默认就是最大可占用的空间
    **/
    MainAxisSize mainAxisSize = MainAxisSize.max,
    /**
    次轴的排序方式
CrossAxisAlignment.start次轴的顶部(默认Y轴上部)
CrossAxisAlignment.end次轴的底部(默认Y轴下部)
CrossAxisAlignment.center次轴的中部(默认Y轴中间)
CrossAxisAlignment.stretch子元素宽充满
CrossAxisAlignment.baseline子控件基线匹配
    **/
    CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
    /**
TextDirection.ltr排列方式从左到右
TextDirection.rtl排列方式从右到左
    **/
    TextDirection? textDirection,   
    //表示Row纵轴（垂直）的对齐方向，默认是VerticalDirection.down，表示从上到下。
    VerticalDirection verticalDirection = VerticalDirection.down,
    TextBaseline? textBaseline, // 基线对齐方式
    List<Widget> children = const <Widget>[],
  })
```

#### Column（垂直布局）

```dart
Column({
    Key? key,
    /**
    主轴的排序方式
MainAxisAlignment.start主轴顶部(默认Y轴左边)
MainAxisAlignment.end主轴底部(默认Y轴右边)
MainAxisAlignment.center主轴中间(默认Y轴轴中间)
MainAxisAlignment.spaceBetween 间距相同 首尾没有间距
MainAxisAlignment.spaceAround子元素平均充满
MainAxisAlignment.spaceEvenly间距相同 首尾有间距
    **/
    MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
    /**
MainAxisSize.min容器空间需要根据内容的大小而撑开的时候用
MainAxisSize.max则相反默认就是最大可占用的空间
    **/
    MainAxisSize mainAxisSize = MainAxisSize.max,
    /**
    次轴的排序方式
CrossAxisAlignment.start次轴的顶部(默认X轴上部)
CrossAxisAlignment.end次轴的底部(默认X轴下部)
CrossAxisAlignment.center次轴的中部(默认X轴中间)
CrossAxisAlignment.stretch子元素宽充满
    **/
    CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
    TextDirection? textDirection,
    VerticalDirection verticalDirection = VerticalDirection.down,
    TextBaseline? textBaseline,
    List<Widget> children = const <Widget>[],
  })
```

### 弹性布局

#### Flex

```dart
/**
Flex组件可以沿着水平或垂直方向排列子组件，如果你知道主轴方向，使用Row或Column会方便一些，因为Row和Column都继承自Flex，参数基本相同，所以能使用Flex的地方基本上都可以使用Row或Column。Flex本身功能是很强大的，它也可以和Expanded组件配合实现弹性布局。接下来我们只讨论Flex和弹性布局相关的属性(其它属性已经在介绍Row和Column时介绍过了)。
**/
Flex({
    Key? key,
    required this.direction,   ////弹性布局的方向, Row默认为水平方向，Column默认为垂直方向
    this.mainAxisAlignment = MainAxisAlignment.start,
    this.mainAxisSize = MainAxisSize.max,
    this.crossAxisAlignment = CrossAxisAlignment.center,
    this.textDirection,
    this.verticalDirection = VerticalDirection.down,
    this.textBaseline, // NO DEFAULT: we don't know what the text's baseline should be
    this.clipBehavior = Clip.none,
    List<Widget> children = const <Widget>[],
  })
```

#### Expanded（比例平分）

Expanded 只能作为 Flex 的孩子（否则会报错），它可以按比例“扩伸”`Flex`子组件所占用的空间。因为 `Row`和`Column` 都继承自 Flex，所以 Expanded 也可以作为它们的孩子

```dart
const Expanded({
    Key? key,
    int flex = 1,   //指定比例（不填写的话将平分父容器）
    required Widget child,  //指定控件
  })
```

### 流式布局

这是因为Row默认只有一行，如果超出一行将报溢出错误，如果超出屏幕不会折行。我们把超出屏幕显示范围会自动折行的布局称为流式布局

#### Wrap

Wrap是一个可以使子控件自动换行的控件，默认的方向是水平的，使用起来也很简单。

```dart
Wrap({
    Key? key,
    this.direction = Axis.horizontal,      //排列方向，默认水平方向排列
    this.alignment = WrapAlignment.start,  //子控件在主轴上的对齐方式
    this.spacing = 0.0,    //主轴上子控件中间的间距
    this.runAlignment = WrapAlignment.start,   //子控件在交叉轴上的对齐方式
    this.runSpacing = 0.0,     //交叉轴上子控件之间的间距
    this.crossAxisAlignment = WrapCrossAlignment.start,  //交叉轴上子控件的对齐方式
    this.textDirection,   //textDirection水平方向上子控件的起始位置
    this.verticalDirection = VerticalDirection.down,  //垂直方向上子控件的其实位置
    this.clipBehavior = Clip.none,
    List<Widget> children = const <Widget>[],
  }) 
    
//例子
 Wrap(
   spacing: 8.0, // 主轴(水平)方向间距
   runSpacing: 4.0, // 纵轴（垂直）方向间距
   alignment: WrapAlignment.center, //沿主轴方向居中
   children: <Widget>[
     Chip(
       avatar: CircleAvatar(backgroundColor: Colors.blue, child: Text('A')),
       label: Text('Hamilton'),
     ),
     Chip(
       avatar: CircleAvatar(backgroundColor: Colors.blue, child: Text('M')),
       label: Text('Lafayette'),
     ),
     Chip(
       avatar: CircleAvatar(backgroundColor: Colors.blue, child: Text('H')),
       label: Text('Mulligan'),
     ),
     Chip(
       avatar: CircleAvatar(backgroundColor: Colors.blue, child: Text('J')),
       label: Text('Laurens'),
     ),
   ],
)
```

#### Flow

很少会使用`Flow`，因为其过于复杂。暂不了解。

### 层叠布局

类似于 Web 中的绝对定位、Android 中的 Frame 布局

#### Stack

```dart
Stack({
    Key? key,
    /**
    所有子组件摆放的位置
    AlignmentDirectional.topStart 默认开始位置的上面
    **/
    this.alignment = AlignmentDirectional.topStart,
    this.textDirection,
    /**
    此参数用于确定没有定位的子组件如何去适应Stack的大小。
    StackFit.loose       //表示使用子组件的大小，
    StackFit.expand      //表示扩伸到Stack的大小。
    **/
    this.fit = StackFit.loose,
    @Deprecated(
      'Use clipBehavior instead. See the migration guide in flutter.dev/go/clip-behavior. '
      'This feature was deprecated after v1.22.0-12.0.pre.',
    )
    this.overflow = Overflow.clip,
    /**
    此属性决定对超出Stack显示空间的部分如何剪裁
    Clip.hardEdge    表示直接剪裁
    **/
    this.clipBehavior = Clip.hardEdge,
    List<Widget> children = const <Widget>[],
  })
```

#### Positioned

绝对定位，用于确定子组件的位置

```dart
/**
left、top 、right、 bottom分别代表离Stack左、上、右、底四边的距离。width和height用于指定需要定位元素的宽度和高度。注意，Positioned的width、height 和其它地方的意义稍微有点区别，此处用于配合left、top 、right、 bottom来定位组件，举个例子，在水平方向时，你只能指定left、right、width三个属性中的两个，如指定left和width后，right会自动算出(left+width)，如果同时指定三个属性则会报错，垂直方向同理。
**/
const Positioned({
  Key? key,
  this.left, 
  this.top,
  this.right,
  this.bottom,
  this.width,
  this.height,
  required Widget child,
})
```

### 对齐和相对定位布局

#### Align

调整一个子元素在父元素中的位置，使用Align组件会更简单一些

```dart
const Align({
    Key? key,
    this.alignment = Alignment.center,   //需要一个AlignmentGeometry类型的值，表示子组件在父组件中的起始位置
    /**
    widthFactor和heightFactor是用于确定Align 组件本身宽高的属性；它们是两个缩放因子，会分别乘以子元素的宽、高，最终的结果就是Align 组件的宽高。如果值为null，则组件的宽高将会占用尽可能多的空间
    **/
    this.widthFactor,
    this.heightFactor,
    Widget? child,
  })
```

#### Center

```dart
/**
我们可以认为Center组件其实是对齐方式确定（Alignment.center）了的Align
**/
class Center extends Align {
  const Center({ Key? key, double widthFactor, double heightFactor, Widget? child })
    : super(key: key, widthFactor: widthFactor, heightFactor: heightFactor, child: child);
}
```

## 容器类

### 填充（Padding）

Padding可以给其子节点添加填充（留白），和边距效果类似

```dart
const Padding({
    Key? key,
    required this.padding,    //padding是EdgeInsetsGeometry对象，EdgeInsetsGeometry是抽象类，一般都使用EdgeInsets类
    Widget? child,
  })
    
//EdgeInsets的便捷方法
1. fromLTRB(double left, double top, double right, double bottom)：分别指定四个方向的填充。
2. all(double value) : 所有方向均使用相同数值的填充。
3. only({left, top, right ,bottom })：可以设置具体某个方向的填充(可以同时指定多个方向)。
4. symmetric({ vertical, horizontal })：用于设置对称方向的填充，vertical指top和bottom，horizontal指left和right。
```

### 装饰容器（DecoratedBox）

DecoratedBox可以在其子组件绘制前(或后)绘制一些装饰（Decoration），如背景、边框、渐变等。

```dart
const DecoratedBox({
    Key? key,
    required this.decoration,  //代表将要绘制的装饰，它的类型为Decoration。Decoration是一个抽象类，它定义了一个接口 createBoxPainter()，子类的主要职责是需要通过实现它来创建一个画笔，该画笔用于绘制装饰。一般会使用BoxDecoration
    this.position = DecorationPosition.background, //此属性决定在哪里绘制Decoration，它接收DecorationPosition的枚举类型，该枚举类有两个值：background：在子组件之后绘制，即背景装饰。foreground：在子组件之上绘制，即前景。
    Widget? child,
  }) 
    
BoxDecoration({
  Color color, //颜色
  DecorationImage image,//图片
  BoxBorder border, //边框
  BorderRadiusGeometry borderRadius, //圆角
  List<BoxShadow> boxShadow, //阴影,可以指定多个
  Gradient gradient, //渐变
  BlendMode backgroundBlendMode, //背景混合模式
  BoxShape shape = BoxShape.rectangle, //形状
})
```

### 变换（Transform）

Transform可以在其子组件绘制时对其应用一些矩阵变换来实现一些特效。Matrix4是一个4D矩阵，通过它我们可以实现各种矩阵操作

```dart
const Transform({
    Key? key,
    required this.transform,
    this.origin,
    this.alignment,
    this.transformHitTests = true,
    this.filterQuality,
    Widget? child,
  })
```

### 容器组件（Container）

```dart
Container({
    Key? key,
    this.alignment,
    this.padding,  //容器内补白，属于decoration的装饰范围
    this.color,  // 背景色
    this.decoration,    // 背景装饰
    this.foregroundDecoration,   //前景装饰
    double? width,  //容器的宽度
    double? height,  //容器的高度
    BoxConstraints? constraints,  //容器大小的限制条件
    this.margin,  //容器外补白，不属于decoration的装饰范围
    this.transform,  //变换
    this.transformAlignment,
    this.child,
    this.clipBehavior = Clip.none,
  })
```

### 剪裁（Clip）

```dart
ClipOval	//子组件为正方形时剪裁成内贴圆形；为矩形时，剪裁成内贴椭圆
ClipRRect	//将子组件剪裁为圆角矩形
ClipRect	//默认剪裁掉子组件布局空间之外的绘制内容（溢出部分剪裁）
ClipPath	//按照自定义的路径剪裁
```

## 可滚动组件

### ScrollBar（滚动条）

Scrollbar是一个Material风格的滚动指示器（滚动条），如果要给可滚动组件添加滚动条，可以修改滚动条的风格

```dart
const Scrollbar({
    Key? key,
    required this.child,
    this.controller,
    this.isAlwaysShown,    //是否总是显示，true需要设置ScrollController
    this.trackVisibility,
    this.showTrackOnHover,
    this.hoverThickness,
    this.thickness,    //Scrollbar宽度
    this.radius,      //Scrollbar圆角
    this.notificationPredicate,
    this.interactive,
    this.scrollbarOrientation,
  })
```

### SingleChildScrollView

类似于Android中的`ScrollView`，超出屏幕不太多的时候使用，所以如果预计视口可能包含超出屏幕尺寸太多的内容时，性能差劲。此时应该使用一些支持Sliver延迟加载的可滚动组件，如`ListView`

```dart
SingleChildScrollView({
  this.scrollDirection = Axis.vertical, //滚动方向，默认是垂直方向
  this.reverse = false,   //是否倒序
  this.padding,    //内边距
  bool primary,    //当内容不足以滚动时，是否支持滚动；
  this.physics,    //控制用户滚动视图的交互
  this.controller,  //滑动控制器
  this.child,
})
    
//例子
class SingleChildScrollViewTestRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    return Scrollbar( // 显示进度条 
      child: SingleChildScrollView(   //可以直接使用SingleChildScrollView，不需要Scrollbar
        padding: EdgeInsets.all(16.0),
        child: Center(
          child: Column( 
            //动态创建一个List<Widget>  
            children: str.split("") 
                //每一个字母都用一个Text显示,字体为原来的两倍
                .map((c) => Text(c, textScaleFactor: 2.0,)) 
                .toList(),
          ),
        ),
      ),
    );
  }
}
```

### ListView

```dart
ListView({
    Key? key,
    Axis scrollDirection = Axis.vertical,    //滚动方向
    bool reverse = false,
    ScrollController? controller,    // 滚动控制 主要是控制滚动位置和监听滚动事件
    bool? primary,
    ScrollPhysics? physics,    //接收ScrollPhysics类型的对象，决定可滚动组件如何响应用户操作
    bool shrinkWrap = false,   //是否根据子组件的总长度来设置ListView的长度
    EdgeInsetsGeometry? padding,   //内边距
    this.itemExtent,    //该参数如果不为null，则会强制children的高度为itemExtent的值 横向为宽度 纵向为高度
    this.prototypeItem,
    bool addAutomaticKeepAlives = true,
    bool addRepaintBoundaries = true,
    bool addSemanticIndexes = true,
    double? cacheExtent,
    List<Widget> children = const <Widget>[],
    int? semanticChildCount,
    DragStartBehavior dragStartBehavior = DragStartBehavior.start,
    ScrollViewKeyboardDismissBehavior keyboardDismissBehavior = ScrollViewKeyboardDismissBehavior.manual,
    String? restorationId,
    Clip clipBehavior = Clip.hardEdge,
  }) 
    
//例子
ListView(
  shrinkWrap: true, 
  padding: const EdgeInsets.all(20.0),
  children: <Widget>[
    const Text('I\'m dedicating every day to you'),
    const Text('Domestic life was never quite my style'),
    const Text('When you smile, you knock me out, I fall apart'),
    const Text('And I thought I was so smart'),
  ],
);
```

#### ListView.builder

```dart
//ListView.builder (ListView.builder适合列表项比较多或者列表项不确定的情况)
ListView.builder({
  // ListView公共参数已省略  
  ...
  //itemBuilder：它是列表项的构建器，类型为IndexedWidgetBuilder，返回值为一个widget。当列表滚动到具体的index位置时，会调用该构建器构建列表项
  required IndexedWidgetBuilder itemBuilder,
  //itemCount：列表数量
  int itemCount,
  ...
})
    
//例子
ListView.builder(
  itemCount: 100,
  itemExtent: 50.0, //强制高度为50.0
  itemBuilder: (BuildContext context, int index) {
    return ListTile(title: Text("$index"));
  }
);
```

#### ListView.separated

`ListView.separated`可以在生成的列表项之间添加一个分割组件，它比`ListView.builder`多了一个`separatorBuilder`参数，该参数是一个分割组件生成器

```dart
class ListView3 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //下划线widget预定义以供复用。  
    Widget divider1=Divider(color: Colors.blue,);
    Widget divider2=Divider(color: Colors.green);
    return ListView.separated(
      itemCount: 100,
      //列表项构造器
      itemBuilder: (BuildContext context, int index) {
        return ListTile(title: Text("$index"));
      },
      //分割器构造器
      separatorBuilder: (BuildContext context, int index) {
        return index%2==0?divider1:divider2;
      },
    );
  }
}
```

### AnimatedList

AnimatedList 和 ListView 的功能大体相似，不同的是， AnimatedList 可以在列表中插入或删除节点时执行一个动画，在需要添加或删除列表项的场景中会提高用户体验。

### GridView

网格布局是一种常见的布局类型，GridView 组件正是实现了网格布局的组件