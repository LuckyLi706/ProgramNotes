# 刷机和Root

## 刷机命令

```
#重启进入bootloader
adb reboot bootloader

#解锁unlock状态
fastboot flashing unlock 

#锁定状态 
fastboot flashing lock

#得到锁的状态
fastboot getvar devices-state

#写入boot分区img文件
fastboot flash boot  **.img

#清空data分区数据，根据分区名
fastboot erase data

#格式化data分区数据，根据分区名 
fastboot format data 

#重启
fastboot reboot

#进入bootloader模式
adb reboot bootloader     

#刷入twrp
fastboot boot twrp-3.2.3-1-marlin.img或者fastboot recovery twrp-3.2.3-1-marlin.img
```

## TWRP

+ [TWRP（第三方Recovery）](https://twrp.me/Devices/)

+ [twrp出现需要输入密码（如下图所示）的解决方案](http://www.oneplusbbs.com/thread-3322174-1.html)

## Root

+ [Magisk](https://github.com/topjohnwu/Magisk/releases)
  - 可以Root高版本安卓系统
  - 自带很多优秀的插件
+ Supersu（已经不维护了，高版本无效）

## 小米

### 代号

```
XiaoMi 1/1s mione plus
XiaoMi 2/2s aries白羊座
XiaoMi 2a taurus金牛座
XiaoMi 3td pisces双鱼座
XiaoMi 3/4 cancro巨蟹座
XiaoMi 4i ferrari法拉利
XiaoMi 4c libra天秤座
XiaoMi 4s aqua水瓶座
XiaoMi 5 gemini双子座
XiaoMi 5s capricorn摩羯座
XiaoMi 5c meri矩阵
XiaoMi note virgo处女座
XiaoMi note pro leo狮子座
XiaoMi note 2 scorpio天蝎座
XiaoMi 5s plus natrium钠
XiaoMi max hydrogen氢
XiaoMi max pro helium氦
XiaoMi mix lithium锂
XiaoMi 平板 mocha摩卡
XiaoMi 平板2 latte拿铁
RedMi 1s armani阿玛尼
RedMi 2/2a 无释义
RedMi 3 ido恒信钻石
RedMi 3s/x land衣恋
RedMi pro omega欧米茄
RedMi 4 prada普拉达
RedMi 4a rolex劳力士
RedMi 4x santoni圣东尼
RedMi note dior迪奥
RedMi note双卡版 gucci古驰
RedMi note2 hermes爱马仕
RedMi note3双网通 hennessy轩尼诗
RedMi note3全网通 kenzo凯卓
RedMi note4 nikel耐克（L码？）
RedMi note4x mido美度
RedMi note5  whyred
RedMi 5plus Vince

十二星座是小米系列的命名规则，但并不是十二星座用完了就江郎才尽了。小米max、mix用的是化学元素代号，小米5c则另辟蹊径，meri矩阵作为代号，也许是纪念澎湃处理器的诞生。

最有意思的是红米系列，每个代号都是奢侈大品牌，恶意满满啊！平板系列代号则是咖啡，平板3会不会是卡布奇诺呢？
```

### 版本命名

```
1.稳定版命名和开发版规则
如：XiaoMi Note 2的稳定版本号为V10.0.1.0.OADCNFH
V：这个没什么好说的，即Version。
(1)数字部分
9.5.3.0，9是MIUI的大版本，后面是小版本，这是MIUI ROM内部的版本约定。
(2)字母部分
MBFCNFA，需要分成几个部分。
O： 是Android版本代号，这里M代指Android 8。
BF： 这是小米内部对于机型的代号，XiaoMi Note 2的代号为AD。
CN：是地区代号，表示China。
F： 开发的年份，约定2013为A开始，依此类推，F表示2018年。
H：开发的月份，约定A为八月。
如：XiaoMi Note 2的开发版本号为8.10.18 （MIUI10）
8：2018年
10：10月份
18：18号
```

### 刷机

[小米解锁地址](http://www.miui.com/unlock/index.html)

+ RedMi Note 3（全网通和双网通）（需要解锁）
  - [所有的线刷包和卡刷包，包含开发版本](http://www.miui.com/thread-6988405-1-1.html)
  - 刷第三方ROM，需要先解锁booloader，然后刷入第三方recovery，如TWRP。可以刷入魔趣

[魔趣双网通纯净版本](https://pan.baidu.com/s/1IHWGx_He2hJDv6z3Kncp2g)

[魔趣全网通纯净版本](https://pan.baidu.com/s/1HLADCHaxuOgF_WE8UYHxXQ)

+ RedMi Note 2（不需要解锁）

  - [所有的线刷包和卡刷包，包含开发版本](http://www.miui.com/thread-2916301-1-1.html)

  - [最新开发版本卡刷包](https://pan.baidu.com/s/1BajX2qnESaXJb6oltqFGHw)

+ XiaoMi Note 2
  - [稳定版](https://pan.baidu.com/s/17R8c5N2hTpJt3HpuMGYZOA)

## 三星

### 刷机

进入bootloader模式，需要借助odin软件刷入tar包

+ [三星Note3 N9008官方原厂固件刷机包下载 线刷一体包 4.3/4.4/5.0 ROM](https://www.114shouji.com/show-12724-1-1.html)