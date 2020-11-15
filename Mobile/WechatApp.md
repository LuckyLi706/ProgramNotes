# WechatApp

## 开发

+ 入门（预备知识es6、ts等语法）

+ [微信小程序开发资源汇总](https://github.com/justjavac/awesome-wechat-weapp#%E7%9B%AE%E5%BD%95)

+ 开源库
  
  + [小程序生成二维码](https://github.com/tomfriwel/weapp-qrcode)
  
  + [小程序调用eval函数（执行js）](https://github.com/bramblex/jsjs)
  
    ```
    使用require来引入    
    调用方法：interpreter.run("var x = 1,y=2; console.log(x+y)");
    ```
  
    

## 逆向

+ 小程序位置
  
  + Android（需要Root）
  
    ```
    /data/data/com.tencent.mm/MicroMsg/597a85e1d82c58dc8ecee39da43c72c7/appbrand/pkg
    下的后缀名为wxapkg文件里面（597为UserId 为当前登录的微信账号 Id 的 MD5 值（32 位字符串））
    ```
  
  + IOS（需要越狱）
  
    ```
    /var/mobile/Containers/Data/Application/E5A9B965-9849-43D6-904D-E3CC95A1F335/Library/WechatPrivate/f2b3ad6f35ebcaf70cd74923360eec53/WeApp/LocalCache/release/wx8a3e212c013104b6下的后缀名为wxapkg文件里面
    （E5A为微信应用，手机上可以先使用Filza软件查看各个安装软件对应的值，f2b为UserId 为当前登录的微信账号 Id 的 MD5 值（32 位字符串））
    ```
  
    