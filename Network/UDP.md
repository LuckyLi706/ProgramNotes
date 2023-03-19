# UDP

+ UDP是无连接的，减少了建立和释放连接的开销
+ UDP尽最大能力交付，不保证可靠交付
+ 因此不需要维护一些复杂的参数，首部只有8个字节（TCP的首部至少20个字节）

## 数据包格式

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_transport_udp_format.png)

+ UDP长度（Length）占16位

  首部的长度+ 数据的长度

+ 检验和的计算内容：伪首部+ 首部+ 数据

  伪首部：仅在计算检验和时起作用，并不会传递给网络层

  ![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_transport_udp_checksum.png)

+ 端口（Port）

  - UDP首部中端口是占用2字节，端口范围在0~65535

  - 客户端的源端口是临时开启的随机端口

  - 防火墙可以设置开启\关闭某些端口来提高安全性

  - 常用命令行

    ```
    netstat –an：查看被占用的端口
    netstat –anb：查看被占用的端口、占用端口的应用程序
    telnet 主机端口：查看是否可以访问主机的某个端口
    
    安装telnet：控制面板– 程序– 启用或关闭Windows功能– 勾选“Telnet Client” – 确定
    ```

## 