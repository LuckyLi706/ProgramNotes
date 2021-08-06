# 基础

## npm命令

### 安装npm

+ mac安装

  ```javascript
  # 1、将之前用 brew 安装的 node 先卸载掉
  rm -rf /usr/local/lib/node_modules
  brew uninstall node
  
  # 2、使用 brew 安装 nvm
  brew update
  brew install nvm
  
  # 3、安装成功后（会有稍长时间等待）
  # 需要配置一下 .zshrc（没有就创建一个，目录 ~/）
  # .nvm 文件夹需要创建的话也直接创建了（也是在 ~/）
  touch ~/.zshrc
  
  # 4、创建后（本来就有这个文件），往里面添加 nvm 的配置
  # 直接拷贝就行，我是从 nvm 的 github 找到的
  # 添加完之后记得 source 一下
  export NVM_DIR="/Users/liminglin/.nvm"
    [ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
    [ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
    
  # 5、然后使用 nvm 安装 node（完成后升级就👌了）
  nvm install node
  ```

+ linux安装

### 安装依赖命令

1. npm install 模块名 -g  //全局安装，但是代码中，直接通过require()的方式是没有办法调用全局安装的包的。全局的安装是供命令行使用的

2. npm install 模块名      //本地安装，默认安装最新版，也可以跟版本号指定版本。当前目录存在package.json，会安装到当前目录的node_modules目录下。如果没有则会放到C:/Users/用户名/node_modules下。

3. npm install 模块1 模块2 模块3   //一次安装多个模块

### 查看安装目录

1. npm root       //查看当前包的安装路径

2. npm root -g  //查看全局的包的安装路径

### 更新模块

1. npm update  模块名    

2. npm update 模块名 @版本号   //当然你也可以update 该模块到指定版本

3. npm install 模块名@latest        //如果安装到最新版本可以使用以下命令

### 卸载模块

npm uninstall 模块名  

### 路径

1. npm的缓存目录在哪里？

​      npm config get cache

2. npm的全局node包在哪里？

​      npm config get prefix

### 更换源地址

+ npm config get registry  查看镜像源

//更换为淘宝的镜像源

1. npm config set registry https://registry.npm.taobao.org --global

2. npm config set disturl https://npm.taobao.org/dist --global

3. npm install -g cnpm --registry=https://registry.npm.taobao.org     //使用cnpm加速

### package.json 和 package-lock.json 作用

```javascript
package.json:
主要用来定义项目中需要依赖的包,npm init之后会自动生成。

package-lock.json：
在 `npm install`时候生成一份文件，用以记录当前状态下实际安装的各个npm package的具体来源和版本号。

'^' :

放在版本号之前，表示向后兼容依赖，说白了就是在大版本号不变的情况下，下载最新版的包。

项目中引入的包版本号之前经常会加^号，每次在执行npm install之后，下载的包都会发生变化，为了系统的稳定性考虑，每次执行完npm install之后会对应生成package-lock文件，该文件记录了上一次安装的具体的版本号，相当于是提供了一个参考，在出现版本兼容性问题的时候，就可以参考这个文件来修改版本号即可。
```

