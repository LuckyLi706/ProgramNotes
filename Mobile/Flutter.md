# [Flutter](https://flutter.dev/ )

## 入门

### 环境搭建

+ AndroidStudio搭建环境

  1. [下载flutter资源](https://flutter.dev/docs/development/tools/sdk/releases#windows)

  2. 配置环境变量

     ```
     //由于在国内访问Flutter有时可能会受到限制，Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中
     PUB_HOSTED_URL=https://pub.flutter-io.cn
     FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
     ```
  
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
  
  8. 使用Android Studio或者VSCode打开工程即可

### 学习

+ [Flutter中文网](https://flutterchina.club/)
+ [非常全的组件集合](https://github.com/toly1994328/FlutterUnit)

