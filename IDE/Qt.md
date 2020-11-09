# Qt

+ 安装篇
  - [Qt下载（多种下载通道+所有版本）](http://c.biancheng.net/view/3851.html)
  - [Qt地址](http://download.qt.io/)
  - [Qt安装各组件说明](https://www.cnblogs.com/xiang--liu/p/11641736.html)
  - [Android配置](https://blog.csdn.net/weixin_43698364/article/details/105187950)

```
问题点：
一、添加或移除组件时出现至少需要一个有效且已启用的储存库
解决：
1、选择左下角的设置，进入如图界面，然后选择“临时存储库”
2、添加地址 http://download.qt.io/static/mirrorlist/online/qtsdkrepository/windows_x86/root/qt/

二、Android编译时出现The minimum API level required by the kit is 21.
将Adnroidminfest.xml的Minimum required SDK改为21
```

