# Nginx

## 安装

### Mac

```shell
# M1或者M2安装方式
# nginx安装位置：/opt/homebrew/Cellar/nginx/版本号/
# 配置文件位置：/opt/homebrew/etc/nginx/nginx.conf
# 服务器目录：/usr/local/var/www 
brew install nginx  # 使用brew安装nginx
brew info nginx
sudo nginx #启动服务
sudo nginx -s stop #停止服务（直接走）
sudo nginx -s reload  #重新加载
sudo nginx -s reopen #重新启动
sudo nginx -s quit #退出（处理完事情走）
sudo nginx -c 配置文件路径  # 手动指定nginx的路径位置
```

### Windows

### Linux

## 应用

### 动静分离

### 反向代理

### 负载均衡

### 正向代理