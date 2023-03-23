# [Flutter](https://flutter.dev/ )

## 开发

### 入门

+ [Dart网站](https://www.dartcn.com/)
+ [官方文档](https://dart.cn/guides/language/language-tour)
+ [Dart入门](../Dart.md)

#### 环境搭建

+ AndroidStudio搭建环境

  1. [下载flutter资源](https://flutter.dev/docs/development/tools/sdk/releases#windows)

  3. Android Studio添加Flutter插件（Flutter和Dart），完成之后重启AS：

  4. 配置AS的Flutter插件的路径（选择flutter的bin目录）
  
  5. 执行flutter doctor 查看当前可以支持的设备
  
  6. 让flutter支持桌面
  
     ```
     flutter config --enable-linux-desktop    
     flutter config --enable-macos-desktop
     flutter config --enable-windows-desktop
     ```
  
  7. flutter create xxx 命令行创建工程
  
  7. 使用Android Studio或者VSCode打开工程即可

#### pubspec.yaml（配置文件）

##### Application（应用）

```yaml
name: test_app    # 表示包名,引入自己创建的类,都会带入这个路径
description: A new Flutter project.  # 对当前项目的介绍，作为应用用处不大

publish_to: 'none' # 插件有效，作为应用可以不需要

# 在 Android 中 对应 versionName + versionCode
version: 1.0.0+1

environment:
  # 约束dart sdk 版本，当前dart版本必须大于等于2.16.2并且小于3.0.0版本
  sdk: ">=2.16.2 <3.0.0"
  # 约束flutter sdk 版本，当前flutter版本必须大于3.0.1版本
  flutter: ">=3.0.1"

# 依赖版本约束说明
# name：包名 version：版本号
# ^符号  ^version：版本号要与指定的版本兼容  ^1.2.3相当于 '>=1.2.3 <2.0.0'  ^0.1.2相当于'>=0.1.2 <0.2.0'
# 其他符号 any 1.2.3 >=1.2.3 >1.2.3 <=1.2.3<1.2.3
dependencies:
  flutter:
    sdk: flutter

  # 依赖方式
  # 1、依赖 pub.dev 上的第三方库是最常用的一种方式
  #  path_provider: ^1.6.22
  # 2、依赖本地库
  # flutter_package:
  #   path: ../flutter_package
  # 3、依赖Git仓库的库
  # bloc:
  #   git:
  #     url: https://github.com/felangel/bloc.git    仓库地址
  #     ref: bloc_fixes_issue_110    表示git引用，可以是 commit hash, tag 或者 branch
  #     path: packages/bloc  如果 git 仓库中有多个软件包，则可以使用此属性指定软件包
  # 4、依赖我们自己的 pub 仓库
  # bloc: 
  #   hosted:
  #     name: bloc
  #     url: http://your-package-server.com
  #   version: ^6.0.0
  cupertino_icons: ^1.0.2

# 开发使用的依赖，例如test、代码生成，仅仅是运行期间的包，比如自动生成代码的库
dev_dependencies:
  flutter_test:
    sdk: flutter

  flutter_lints: ^1.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter.
flutter:

  # 确保您的应用程序中包含Material Icons字体，以便您可以使用material Icons类中的图标
  uses-material-design: true

  # 添加资源
  assets:
    - images/a_dot_burr.jpeg  #images目录下的本地图片
    - images/a_dot_ham.jpeg

  # 添加字体资源
  fonts:
    - family: Schyler
      fonts:
        - asset: fonts/Schyler-Regular.ttf
        - asset: fonts/Schyler-Italic.ttf
          style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/custom-fonts/#from-packages

```

##### Plugin（插件）

### 进阶

+ [Widgets（UI）](FlutterWidgets.md)
+ [开源库](FlutterOpenSource.md)
+ [与原生交互](FlutterNative.md)
+ [路由](FlutterRoute.md)

## 学习资料

+ [Flutter中文网](https://flutterchina.club/)
+ [非常全的组件集合](https://github.com/toly1994328/FlutterUnit)

## 问题

1. [Waiting for another flutter command to release the startup lock](https://blog.csdn.net/lucynie/article/details/106929170)

2. flutter pub get一直卡住

   + 方案一：使用镜像

     ```
     //由于在国内访问Flutter有时可能会受到限制，Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中
     
     mac：
     ～/.bash_profile 文件中加入以下
     export PUB_HOSTED_URL=https://pub.flutter-io.cn
     export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
     
     windows
     环境变量加入
     PUB_HOSTED_URL   https://pub.flutter-io.cn
     FLUTTER_STORAGE_BASE_URL    https://storage.flutter-io.cn
     ```

   + 方案二：使用代理，终端开代理，然后执行命令

3. flutter2.x版本每次编译安卓遇到网络错误都会删除.gradle文件，.gradle目录存放的是下载的第三方开源库和gradle文件（flutter3.x问题已修复）

   + 出现原因：https://github.com/flutter/flutter/issues/89959

   + 解决方案：

     1. ` ~/flutter/packages/flutter_tools/lib/src/android/gradle_errors.dart` and open it for editing.

        ```dart
        @visibleForTesting
        final GradleHandledError networkErrorHandler = GradleHandledError(
          test: _lineMatcher(const <String>[
            'java.io.FileNotFoundException: https://downloads.gradle.org',
            'java.io.IOException: Unable to tunnel through proxy',
            'java.lang.RuntimeException: Timeout of',
            'java.util.zip.ZipException: error in opening zip file',
            'javax.net.ssl.SSLHandshakeException: Remote host closed connection during handshake',
            'java.net.SocketException: Connection reset',
            'java.io.FileNotFoundException',
            "> Could not get resource 'http",
          ]),
          handler: ({
            required String line,
            required FlutterProject project,
            required bool usesAndroidX,
            required bool multidexEnabled,
          }) async {
            globals.printError(
              '${globals.logger.terminal.warningMark} Gradle threw an error while downloading artifacts from the network. '
              'Retrying to download...'
            );
            //删除以下代码
            // try {
            //   final String? homeDir = globals.platform.environment['HOME'];
            //   if (homeDir != null) {
            //     final Directory directory = globals.fs.directory(globals.fs.path.join(homeDir, '.gradle'));
            //     ErrorHandlingFileSystem.deleteIfExists(directory, recursive: true);
            //   }
            // } on FileSystemException catch (err) {
            //   globals.printTrace('Failed to delete Gradle cache: $err');
            // }
            return GradleBuildStatus.retry;
          },
          eventLabel: 'network',
        );
        ```

     2. 去 ~/flutter/bin/cache这个目录去删除flutter_tools.stamp 和 flutter_tools.snapshot文件。

     3. 然后执行命令flutter doctor。然后.gradle目录就不会被删除了。

4. 
