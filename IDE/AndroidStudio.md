# AndroidStudio

## 环境变量

+ 修改模拟器目录和gradle默认目录

  ```
  新建环境变量ANDROID_HOME指向SDK目录
  新建环境变量ANDROID_SDK_HOME指向AVD目录
  在Android Studio的bin目录下的idea.properties修改配置文件所指向的目录
  Android Studio下的Setting修改gradle的默认目录
  
  https://developer.android.com/studio/command-line/variables.html#envar
  ANDROID_SDK_HOME：D:\Android\AndroidAVD   （设置模拟器根目录）
  ANDROID_AVD_HOME：D:\Android\AndroidAVD\.android\avd（设置模拟器镜像目录）
  ANDROID_SDK_ROOT：D:\Android\AndroidSDK   （SDK目录）
  ```

## 插件

+ [ECTranslation（Android Studio 开发工具的一个翻译插件, 可以将英文翻译为中文, 英语基础差的童鞋装上它就可以轻松阅读 Android 源码啦）](https://github.com/Skykai521/ECTranslation)

+ [AndroidWiFiADB（无线调试应用）](https://github.com/pedrovgs/AndroidWiFiADB)

+ [gradle自动提示插件（提示快捷键Crtl+Shitf+空格）](https://plugins.jetbrains.com/plugin/7299-gradle-dependencies-helper/versions)
+ AndroidLocalize (生成各国语言的strings.xml)

## 错误集锦

+ AS开了代理，平时ss都能用，都没问题，今天ss挂了，关闭了AS的代理，还是下载不了，用浏览器是能下载的，报的错误ssl error。

  解决方案：C:\Users\jacky\.gradle\gradle 文件下面移除代理（https://blog.csdn.net/coderder/article/details/82347320）