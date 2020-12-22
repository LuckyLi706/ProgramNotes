# phpMyAdmin

## 安装

+ [mac系统下安装mysql 和phpmyadmin](https://www.cnblogs.com/yuwensong/p/6658689.html)
+ [关于php7.3.3 连接mysql8 出现 The server requested authentication method unknown to the client](https://blog.csdn.net/qq_36349366/article/details/88796533)
+ [mysql 安装了最新版本8.x版本后的报错： the server requested authentication method unknown to the client](https://blog.csdn.net/youcijibi/article/details/81153789)

### mac

+ apache（mac自带）

  ```
  sudo apachectl start     # 启动apache
  sudo apachectl restart   # 重新启动
  sudo apachectl stop      # 关闭apache
  ```

+ php（mac默认自带7.x版本）

```
1、在/Library/WebServer/Documents下，如果是初次配置应该会看到该文件夹里有三个文件，index.html.en 和两张图片

2、打开sudo vim /etc/apache2/httpd.conf，进行配置

3、找到#LoadModule php7_module libexec/apache2/libphp7.so去除前面的#

4、添加index.php，默认只有index.html
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

5、sudo apachectl restart

//以上方法我没有成功，只要开启php7就localhost没反应，所以改换php5
如果想尝试php7，尝试网址（https://blog.csdn.net/qq_21761149/article/details/109708508）

安装php5
1、cd /tmp/
2、curl -s http://php-osx.liip.ch/install.sh | bash -s 5.6
3、修改apache配置
#LoadModule php7_module libexec/apache2/libphp7.so //系统默认配置
LoadModule php5_module /usr/local/php5/libphp5.so //php5配置
4、sudo apachectl restart
```

+ [mysql](../SQL/MySQL)

+ phpMyAdmin

  ```
  phpMyAdmin 4.x版本兼容低版本PHP
  phpMyAdmin 5.x版本只支持7.x版本PHP
  
  解压phpMyAdmin,放到/Library/WebServer/Documents下面，
  输入http://localhost/phpMyAdmin/setup/设置数据库连接服务，下载里面的配置文件放到phpMyAdmin根目录下。
  然后输入http://localhost/phpMyAdmin管理数据库
  ```