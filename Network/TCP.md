# 传输层

传输层有2个协议

+ TCP（Transmission Control Protocol），传输控制协议
+ UDP（User Datagram Protocol），用户数据报协议

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport.png)

## UDP

+ UDP是无连接的，减少了建立和释放连接的开销
+ UDP尽最大能力交付，不保证可靠交付
+ 因此不需要维护一些复杂的参数，首部只有8个字节（TCP的首部至少20个字节）

### 数据包格式

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_udp_format.png)

+ UDP长度（Length）占16位

  首部的长度+ 数据的长度

+ 检验和的计算内容：伪首部+ 首部+ 数据

  伪首部：仅在计算检验和时起作用，并不会传递给网络层

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_udp_checksum.png)

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

## TCP

### 数据包格式

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_format.bmp)

+ 校验和

  和UDP一样，检验和的计算内容：伪首部+ 首部+ 数据，伪首部：12个字节，仅在计算检验和时起作用，并不会传递给网络层

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_checksum.bmp)

```
数据偏移 4位
取值范围 0x0101~0x1111
乘以4为首部长度，首部长度范围为20～60

保留 6位（也可以说占3位，后面的前三个字节没有用）
目前全为0

标识位（保留位后面的）
1、URG（Urgent）
当URG=1时，紧急指针字段才有效。表明当前报文段中有紧急数据，应优先尽快传送
2、ACK（Acknowledgment）
当ACK=1时，确认号字段才有效
3、PSH（Push）
4、RST（Reset）
当RST=1时，表明连接中出现严重差错，必须释放连接，然后再重新建立连接
5、SYN（Synchronization）
当SYN=1、ACK=0时，表明这是一个建立连接的请求，若对方同意建立连接，则回复SYN=1、ACK=1。
6、FIN（Finish）
当FIN=1时，表明数据已经发送完毕，要求释放连接

序号（Sequence Number）占4字节
首先，在传输过程的每一个字节都会有一个编号
在建立连接后，序号代表：这一次传给对方的TCP数据部分的第一个字节的编号

确认号（Acknowledgment Number）占4字节
在建立连接后，确认号代表：期望对方下一次传过来的TCP数据部分的第一个字节的编号

窗口（Window） 占2字节
这个字段有流量控制功能，用以告知对方下一次允许发送的数据大小（字节为单位）
```

### 可靠传输

1. 重连机制

   如果有个包重传N次还是失败，不会一直重新传输，取决于系统的设置，有的系统比如传送5次还是失败就会发送reset报文断开TCP连接。

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_reconnect.png)

2. 停止等待ARQ协议（ARQ：自动重传请求）（四种情况）

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_arq_1.png)

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_arq_2.png)

3. 连续ARQ协议+滑动窗口协议

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_arq_3.png)

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_arq_4.png)

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_arq_5.png)

4. SACK（选择确认）

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_sack_1.png)

   ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_reliable_transfer_sack_2.png)

5. 思考

   为什么选择在传输层或者应用层就将数据分成很多段，而不是等到网络层在分片传递给数据链路层

   + 因为可以提高重传的性能

   + 需要明确的是：可靠传输是在传输层进行控制的（网络层和物理链路层没有重传功能）

     如果在传输层不分层，一旦出现数据丢失，整个传输层的数据都必须重传

     如果在传输层分层，一旦出现数据丢失，只需要重传丢失的数据即可

### 流量控制

rwnd=receive window（接收窗口）

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_flow_control.png)

+ 如果接收方的缓存存满了，发送方还在疯狂发数据

  - 接收方只能把接收的数据包丢掉，大量的丢包会极大的浪费网络资源
  - 所以要进行流量控制

+ 什么是流量控制

  让发送方的发送速率不要太快，让接收方来得及接收数据

+ 原理

  - 通过确认报文中接收字段来控制发送方的发送速率
  - 发送方的发送窗口大小不能超过接收方的接收窗口大小
  - 当发送发收到接收方窗口大小为0时，发送方就会停止发送数据

+ 特殊情况

  ```
  一开始，接收方给发送方发送了0窗口的报文段，
  后面接收方又有了一些存储空间，给发送方发送非0窗口的报文段丢失了
  发送方的发送窗口一直为0，双方陷入僵局
  
  //解决方案
  当发送方收到0窗口通知时，这时发送方停止发送报文
  并且同时开启一个定时器，隔一段时间就发个测试报文去询问接收方最新的窗口大小
  如果接收方的窗口大小还是为0，则发送方再次刷新启动定时器
  ```

### 拥塞控制

防止过多的数据注入网络，避免网络中的路由器或链路过载

+ 拥塞过程是个全局性的过程

  - 涉及到所有主机、路由器
  - 以及与降低网络传输性能有关的所有因素
  - 是大家共同努力的结果

+ 相比而言，流量控制是点对点通信的控制

+ 慢开始（slow start，慢启动）

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_block_control_slow_start_1.png)

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_block_control_slow_start_2.png)

+ 拥塞避免（congestion avoidance）

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_block_control_block_avoid.png)

+ 快速重传（fast retransimit）

  ```
  //接收方
  每收到一个失序的分组后就立刻发出重复确认
  使发送方及时知道有分组没有到达
  而不用等待自己发送数据时才进行确认
  
  //发送方
  只要连续收到三个重复确认（总共四个相同的确认），就应当立即重传对方尚未收到的报文段
  而不必等待继续重传计时器到期后再重传
  ```

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_block_control_fast_retransimit.png)

+ 快速恢复（fast recovery）

  ```
  当发送方连续收到三个重复确认，说明网络出现阻塞
  就执行“乘法减小“算法，把ssthresh减小为拥塞峰值的一半
  
  与慢开始不同之处现在不执行慢开始算法，即cwnd现在不恢复到初始值
  而是把cwnd值设置为新的ssthresh值（减小后的值）
  然后开始执行拥塞避免算法（”加分增大“），使拥塞窗口慢慢的线性增大。
  ```

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_block_control_fast_retransimit_recovery.png)

+ 发送窗口的最大值

  ```
  //几个缩写
  MSS（Maximum Segment Size）每个段最大的数据部分大小，在连接时确认
  
  cwnd（congestion window）拥塞窗口
  
  rwnd（receive window）接收窗口
  
  swnd（send window）发送窗口
  swnd=min(cwnd,rwnd)
  当rwnd<cwnd,是接收方的接收能力限制发送窗口的最大值
  当rwnd>cwnd,是网络的拥塞限制发送窗口的最大值
  ```

### 建立连接

+ 三次握手
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_connect_three_hand.png)

+ 状态解读

  ```
  CLOSED：客户端处于关闭状态
  LISTEN：服务器处于监听状态，等待客户端连接
  SYN-RCVD：表示服务端接收到了SYN报文，当收到客户端的ACK报文后，他会进入到ESTABLISHED状态
  SYN-SENT：表示客户端已发送SYN报文，等待服务端的第二次握手
  ESTABLISHED：表示连接已经建立
  ```

+ 前两次握手特点

  ```
  SYN都设置为1
  
  数据部分长度都为0
  
  TCP头部的长度一般都为32字节，固定头部20字节，选项部分12字节
  
  双方会交换确认一些信息
  比如MSS，是否支持SACK、Windows scale(窗口缩放系数)等
  这些数据都存放在头部信息的选项部分中（12字节）
  ```

+ 为什么需要3次握手，2次不行吗？

  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_connect_three_hand_2.png)

+ 第三次握手失败了，怎么处理？

  ```
  此时服务端的状态为SYN-RCVD，如果等不到客户端的ACK，服务端会重新发送SYN+ACK包
  
  如果服务端多次重发SYN+ACK都等不到客户端的ACK，就会发送RST包，强制关闭连接
  ```

### 释放连接

+ 四次挥手
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_four_hand.png)
+ 状态解读
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_state_1.png)
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_state_2.png)
+ 细节
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_detail.png)
+ 相关疑问
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_questions.png)
+ 抓包信息
  ![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_disconnect_wireshark.png)

### 默认端口号

![](C:/Users/test/Desktop/ProgramNotes/Network/images/network_transport_tcp_udp_port.png)

## 