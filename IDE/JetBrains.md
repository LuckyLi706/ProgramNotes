# JetBrains

+ [特色主题Material Theme UI（需要代理）](https://plugins.jetbrains.com/plugin/8006-material-theme-ui)

## IDEA

### 配置

+ 调整代码提示忽略大小写

  Settings - Editor - Code Completion - None

+ 多彩主题包下载

  + [地址1](https://github.com/guobinhit/intellij-idea-tutorial/tree/master/resources/idea-theme)
  + [地址2](https://github.com/judasn/IntelliJ-IDEA-Tutorial/blob/master/theme-settings.md)

  ```
  Setting - Editor -Color Scheme -Editor - Gutter background (Background 313335)  //修改左侧和下侧颜色
  Separtor line below（Foreground 393A3C） //修改下侧分割线颜色
  Caret row，指的是光标所在行，我一般会修改其 Background 323232。
  ```

### 常见问题

+ [控制台乱码](https://www.cnblogs.com/liaoyanglong/p/6639039.html)
+ [不能自动add library maven](https://segmentfault.com/a/1190000009449467)

## PhpStorm

### 配置

+ 环境配置

  ```
  1.下载XAMPP   https://www.apachefriends.org/download.html
  2.安装XAMPP
  3.打开PhpStorm，File - Setting - Languages&Frameworks - PHP - CLI Interpreter选择路径 - + - Local Path  -  选择xampp下的php.exe就可以了
  ```

## CLion

### 配置

+ 环境配置

  - 使用Cygwin来配置环境

    1. 下载[Cygwin](http://www.cygwin.com/)，安装过程中要下载gcc，g++，cmake，make，gdb等相关
    2.  配置Cygwin的bin目录到系统的环境变量中
    3.  打开CLion，File  ----  Settings  -----  Build，Execution，Deployment ---- Toolchain ----选择Cygwin  ---添加Cygwin目录

  - 使用WSL（ubutun作为windows的软件）来配置环境

    1. [下载地址]( https://www.microsoft.com/zh-cn/p/ubuntu/9nblggh4msv6?activetab=pivot%3Aoverviewtab)

    2. 升级当前win10为最新的系统，否则在“启用或关闭Windows功能”中会找不到“适用于Linux的Windows子系统”勾选安装wsl前提条件：控制面板=>程序和功能=>启用或关闭Windows功能=>勾选 适用于Linux的Windows子系统（当然也可以像网友提供的直接在管理员权限的windown power shell下执行: Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux）

    3. 安装 Clion 依赖

       Jetbrains 官方给出一键安装的脚本，基本上就是安装基本的开发包，并配置了 SSH Server 用于远程调试

       wget https://raw.githubusercontent.com/JetBrains/clion-wsl/master/ubuntu_setup_env.sh && bash ubuntu_setup_env.sh

    4. 在Windows 上安装 CLion 并打开， 在settings -> Build,Excution,Deployment -> Toolchains -> 绿色 + 号 -> Environment 下拉框选择 WSL。

       Credentials 那里，点击右边的菜单按钮，弹出框中输入 ssh 的用户和密码

    5. wsl系统与windwon系统的路面映射关系： 

       ​      windows系统在wsl中的路径都是挂载在/mnt下面 

       ​      wsl在windown中的映射路径在（友情提示不要直接修改其内容）：%localappdata%\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs 

## Pycharm

### 配置

+ 虚拟环境
  1. 先在项目位置创建虚拟环境
  2. 然后在File----Settings----Project Interpreter----+号选择刚才创建的虚拟环境