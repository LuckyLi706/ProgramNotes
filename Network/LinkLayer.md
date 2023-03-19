# 数据链路层

数据链路层需要在头部和首部加上.

链路：从一个节点到相邻节点的一段物理线路（有线或者无线），中间没有其他交换节点。

数据链路：在一条链路上传输数据时，需要有对应的通信协议来控制数据的传输

不同类型的链路，使用的通信协议可能不同

+ 广播信道：CSMA/CD协议（比如同轴电缆、集电器等组成的网络）
+ 点对点信道：PPP协议（比如两个路由器之间的信道）

## 特性

### 封装成帧

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_frame.png)

+ 帧的数据部分

  就是网络层传递下来的数据包

+ 最大传输单元MTU

  每一种数据链路层协议都规定了所能够传送的帧的数据长度上限，以太网的MTU长度为1500字节

### 透明传输

数据部分一旦出现SOH、EOT，就需要转义

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_tranfer.png)

### 差错校验

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_validate.png)

+ FCS部分是根据数据部分+首部计算得出的。

## CSMA/CD协议

载波侦听多路访问/冲突检测

+ 使用了CSMA/CD的网络可以称为是以太网（Ethernet），它传输的是以太网帧
  - 以太网帧的格式有：Ethernet V2标准、IEEE的802.3标准
  - 使用最多的是：Ethernet V2标准
+ 为了能够检测正在发送的帧是否产生了冲突，以太网的帧至少要64字节
+ 用交换机组建的网络，已经支持全双工通信，不需要再使用CSMA/CD，但它传输的帧依然是以太网帧。所以，用交换机组建的网络，依然可以叫做以太网

### Ethernet V2帧

+ Ethernet  V2帧的格式
  ![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_v2_format.png)
+ Ethernet  V2帧的格式
  ![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_v2_standard.png)

### 网卡

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_network_card.png)

## PPP协议

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_ppp.png)

+ Address字段：图中的值是0xFF，形同虚设，点到点信道不需要源MAC、目标MAC地址
+ Control字段：图中的值是0x03，目前没有什么作用
+ Protocol字段：内部用到的协议类型
+ 帧开始符、帧结束符：0x7E

### 字节填充

![](C:/Users/lijie/Desktop/ProgramNotes/Network/images/network_datalink_byte_fill.png)

