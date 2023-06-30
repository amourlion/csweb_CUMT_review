# 计算机网络
## 第一章 概述
### 互联网基础定义
- ISP定义: 互联网服务提供商

基于ISP的三层结构的互联网
![Alt text](./assets/uTools_1686621616204.png)

![Alt text](./assets/uTools_1686621717153.png)
### 三种交换方式
- 电路交换

引例: 电话交换
![Alt text](./assets/uTools_1686621817588.png)
电路交换的三个步骤:
1. 建立连接
2. 通话
3. 释放连接
但是，电路交换的缺点是: 通话时间长，占用资源多，不适合数据传输，不适合计算机之间交换。
- 报文交换
主要用于早期的电报通信网，现在被较先进的分组交换所取代。
- 分组交换
![Alt text](./assets/uTools_1686622057915.png)

三种交换方式的比较:
![Alt text](./assets/uTools_1686622352647.png)

计算机网络的分类：
![Alt text](./assets/uTools_1686623110166.png)

### 计算机网络性能指标
- 速率(注意存储单位的换算)
![Alt text](./assets/uTools_1686623341024.png)
- 带宽(两种表示可以互换)
![Alt text](./assets/uTools_1686623438383.png)
- 吞吐量
定义：单位时间内通过某个网络的数据量
例如:带宽1Gb/s的以太网，吞吐量可能有700Mb/s。
![Alt text](./assets/uTools_1686623555991.png)
- 时延
![Alt text](./assets/uTools_1686623678621.png)
传播时延和发送实验对比:具体问题具体分析
- 时延带宽积
![Alt text](assets/uTools_1686705199964.png)
- 往返时间RTT
![Alt text](assets/uTools_1686705278608.png)
- 利用率

根据排队论，并非利用率越高越好，更高的利用率会导致时延变大。
![Alt text](assets/uTools_1686705416740.png)

- 丢包率
![Alt text](assets/uTools_1686705510556.png)

### 计算机网络体系结构
![Alt text](assets/uTools_1686705665037.png)
OSI体系结构过于冗杂，缺少市场支持。TCP/IP体系结构是实际应用的体系结构。

综合OSI和TCP/IP体系结构，可以得到如下的原理体系结构:重新划分了网络接口层，将其变为数据链路层和物理层
![Alt text](assets/uTools_1686705992047.png)

#### 分层的必要性
每个模块分别负责什么？
![Alt text](assets/uTools_1686706990499.png)
![Alt text](assets/uTools_1686706952691.png)
![Alt text](assets/uTools_1686707113568.png)
![Alt text](assets/uTools_1686707265064.png)
![Alt text](assets/uTools_1686707345436.png)
模块化思想:
![Alt text](assets/uTools_1686707383801.png)

实例:chrome访问apache服务器
![Alt text](assets/Screenshot%202023-06-14%20095813.png)

#### 专用术语
- 实体
![Alt text](assets/uTools_1686708658588.png)
- 协议
![Alt text](assets/uTools_1686708755611.png)
![Alt text](assets/uTools_1686708999866.png)
- 服务
下层给上层提供接口
![Alt text](assets/uTools_1686709219389.png)
![Alt text](assets/uTools_1686709284399.png)

- PDU:protocol data unit 对等实体逻辑通信传送的数据包
- SDU:service data unit 同系统内上下层实体交换的数据包

#### 例题
![Alt text](assets/uTools_1686710167110.png)

## 第二章 物理层
### 物理层的基本概念
物理层为数据链路层屏蔽了各种传输媒体和通信手段的差异，使数据链路层只需要考虑本层协议和服务。

物理层协议的主要任务:
- 机械特性: 机械特性是指接口的几何形状、引线数目、引线排列、引线的功能等。
- 电气特性: 电气特性是指接口的电压、电流、功率等。
- 功能特性: 电平电压的意义
- 过程特性: 事件的出现顺序
### 传输媒体
- 导引型传输媒体
- 非导引型传输媒体

![Alt text](uTools_1686726589071.png)
### 传输方式
串并行:远距离常用串行传输,计算机内部常用并行
![Alt text](uTools_1686726954561.png)
同异步:
![Alt text](uTools_1686726932435.png)
通信通道分类:
![Alt text](uTools_1686726873595.png)

### 编码与调制
![Alt text](uTools_1686728483618.png)

**常用编码:**

曼彻斯特编码:向上跳变为0，向下跳变为1(不一定，具体情况具体分析)

差分曼彻斯特编码:跳变仅表示时钟，码元开始处变化表示0，开始处不变表示1
![Alt text](uTools_1686729835605.png)
10Base代表10Mb/s
![Alt text](uTools_1686730018454.png)

将信号混合调制，格雷码，一个码元表示四个bit
![Alt text](uTools_1686730376725.png)
![Alt text](uTools_1686730330269.png)

### 信道的极限容量
香农定理:信道的极限容量与信道带宽和信噪比有关

奈奎斯特定理:理想低通/带通信道的极限传输速率与信道带宽有关
![Alt text](uTools_1686730645403.png)
![Alt text](uTools_1686730813586.png)

一般来说都是低通信道
![Alt text](<Screenshot 2023-06-14 162302.png>)
数据传输速率=波特率(码元传输速率) * 每个码元的比特数
![Alt text](uTools_1686731061305.png)

## 第三章 数据链路层
### 本章重点问题
- 封装成帧
- 差错检测
- 可靠传输
- 广播信道的协议
- 网桥，交换机，集线器

![Alt text](uTools_1686733648420.png)
### 差错检测
误码率BER：误码率是指在传输过程中，二进制数据中出现的错误比特数与总的比特数之比。
差错检测码:通过增加冗余信息，使得接收方可以检测出差错的编码。

奇偶校验码:一般不采用
![Alt text](uTools_1686883583662.png)

- 循环冗余校验CRC:生成多项式

题型1:构造发送信息
![Alt text](uTools_1686883814412.png)
题型2:检测接收信息
![Alt text](uTools_1686883869868.png)

### 可靠传输
- 可靠传输的基本概念:可靠传输是指在数据链路层，使得接收方收到发送方发送的数据后，能够检测出差错，且不丢失数据，不重复数据，且按正确的顺序接收数据。

- 不可靠传输:不可靠传输是指在数据链路层，使得接收方收到发送方发送的数据后，不能够检测出差错，且可能丢失数据，重复数据，乱序接收数据。
![Alt text](uTools_1686884018869.png)
可靠传输服务不仅仅局限于数据链路层
![Alt text](uTools_1686884138910.png)

### 可靠传输——停止等待协议 Stop-and-wait
- ACK : Acknowledgement 确认
- NAK : Negative Acknowledgement 否定确认

这些协议可以应用到各层体系结构当中

四种问题以及相关解决办法:
![Alt text](uTools_1686884611835.png)

该协议问题:往返时间大时，信道利用率低
![Alt text](uTools_1686884910284.png)

### 可靠传输———回退N帧协议 Go-Back-N
发送发送窗口内的帧，接收方按照接收窗口接收分组
![Alt text](uTools_1686885494445.png)

- 累计确认:接受几个数据分组后，发送ACKn表示序号n之前的分组已经正确接收

有差错情况:分组5未正确传输，导致接收方抛弃剩下4个分组，并发送**四个ACK4**（异常情况)，告诉发送方需要重传这些分组，发送方立即重传，不需要看重传计时器超时。(回退N帧，一个分组牵连四个分组)
![Alt text](uTools_1686885602461.png)

如果分组发送窗口内分组数量大于分组序号范围：假如接收方一次性接受0，1，2，3，4，5，6，7，返回ACK7失败，这样会导致发送方超时重传，接收方会无法分辨新，旧分组。(为什么Window range不能大)
![Alt text](uTools_1686885881902.png)

接受到一个ACK，发送端就移动滑动窗口到ACK后的位置
![Alt text](uTools_1686886075143.png)

信道质量不好时，会频繁牵连其他分组，导致信道利用率低。

### 可靠传输——选择重传协议 Selective Repeat
不累计确认，当且仅当按序发送/接收时才滑动窗口,不按序划不动

接收窗口尺寸应该小于发送窗口尺寸(若大于，则无意义)
![Alt text](uTools_1686913457857-1.png)

### 点对点协议PPP point-to-point protocol
PPPoE ：PPP over Ethernet
![Alt text](uTools_1686914187703.png)

- PPP的帧格式

FCS: frame check sequence 帧检验序列
NCP：network control protocol 网络控制协议
![Alt text](uTools_1686914484692.png)

差错检测:利用CRC(循环冗余校验码)检测差错，若检测到差错，则丢弃该帧，使用PPP的数据链路层提供不可靠传输服务。(利用FCS字段)
![Alt text](uTools_1686915029135.png)

数据部分的转义处理:
![Alt text](uTools_1686914900247.png)
![Alt text](uTools_1686914939553.png)

### 媒体接入控制MAC Medium Access Control
有点抽象，后面再看看书
![Alt text](uTools_1686915452481.png)

### 静态划分信道
![Alt text](uTools_1686915530748.png)

复用线路，经过一个复用器和分用器

具体可分为四种信道复用方法:
- 频分复用FDM:把信号分成不同频率在一根线上传
- 时分复用TDM:一根线上分时间传不同信道的数据
- 波分复用WDM:光纤用，把光混在一起传输
- 码分复用CDM:码片是一串01序列，规定一个特定的01序列位1，这个序列的反码为0

把0写作-1，1写作+1，这样就可以用正交的方式来区分不同的码片
![Alt text](uTools_1686916146448.png)

结论:用收到的码片序列和各站的码片序列做规格化内积(内积后除以维数)，如果内积为0，则表示该码片不是该站发送的，如果内积是1，则表示该码片是该站发送的。如果内积是-1，则表示该码片是该站发送的反码。
![Alt text](uTools_1686916677143.png)

### 动态接入控制——随机接入
#### CSMA/CD:载波监听多点接入/碰撞检测 Carrier Sense Multiple Access with Collision Detection
基础概念:

![Alt text](uTools_1686917131015.png)

96比特:发送96比特所需的时间

![Alt text](uTools_1686917510566.png)

如果帧太短，碰撞后由于发送端已经不再检测碰撞，导致丢帧
![Alt text](uTools_1686918056789.png)

如果帧太长:总线占用时间太长，而且会导致接收端缓存区溢出
![Alt text](uTools_1686918138603.png)

截断二进制指数退避算法:
![Alt text](uTools_1686918507984.png)

信道利用率:

![Alt text](uTools_1686918754410.png)

总体的帧发送/接收流程:
![Alt text](uTools_1686918911503.png)
![Alt text](uTools_1686918875519.png)

#### CSMA/CA 载波监听多点接入/碰撞避免 Carrier Sense Multiple Access with Collision Avoidance
无线局域网使用的协议，同时还要使用停止-等待协议实现可靠传输

由于无线信道的特殊性，无法检测碰撞，只能通过避免碰撞来实现多点接入。还由于隐蔽站问题，无法碰撞检测

![Alt text](<Screenshot 2023-06-17 103831.png>)

- 为什么等待DIFS：可能有其他站关键的帧发送

- 为什么等待SIFS: 最短的帧间间隔，一个站点应当能从发送方式切换到接收方式

- 为什么DIFS之后还要等待随机时间:防止多个站点同时发送数据产生碰撞

![Alt text](<Screenshot 2023-06-17 104700.png>)

退避算法：总要等一个DIFS，有人占坑，别的计时器就冻结
![Alt text](<Screenshot 2023-06-17 105107.png>)

信道预约:RTS/CTS: Request to Send/Clear to Send
![Alt text](<Screenshot 2023-06-17 105434.png>)

如何解决隐蔽站问题:
![Alt text](<Screenshot 2023-06-17 105905.png>)
这样,C接收到CTS后，就知道A和B都在发送数据，就不会发送数据了

概念辨析:
![Alt text](<Screenshot 2023-06-17 110156.png>)

### MAC地址 && IP地址 && ARP协议
#### MAC地址
适用的层次结构:
![Alt text](<Screenshot 2023-06-17 111257.png>)

MAC地址存在EEPROM中，又名硬件地址(物理地址)，但并不属于物理层。在发送帧时候，在帧头中加入源MAC地址和目的MAC地址，接收方根据MAC地址来判断是否接收该帧。

MAC地址格式:
![Alt text](<Screenshot 2023-06-17 111730.png>)

多播MAC地址:发送时:多播地址+发送端MAC地址，接受时检测多播地址是否在多播组列表中，如果在则接受，否则丢弃。
![Alt text](<Screenshot 2023-06-17 112445.png>)

广播MAC地址:发送时:广播地址+发送端MAC地址，接受时检测到广播地址，直接接受交由上层
![Alt text](<Screenshot 2023-06-17 112537.png>)

单播地址:发送时:目的MAC地址+发送端MAC地址，接受时检测到目的MAC地址，接受
![Alt text](<Screenshot 2023-06-17 112620.png>)

#### IP地址
IP地址用于标识两部分信息:MAC地址不具备区分不同网络的功能
- 网络号:标识主机所在的网络
- 主机号:标识主机在网络中的位置

IP地址封装于网络层，MAC地址封装于数据链路层

网络层完成大任务，链路层完成小任务
![Alt text](<Screenshot 2023-06-17 115436.png>)

过程中，要通过IP->MAC转换，这一步需要利用ARP(Address Resolution Protocol)协议

### 地址解析协议ARP Address Resolution Protocol
发送一个ARP请求，接收方返回一个ARP应答(单播)，应答中包含目的主机的MAC地址，收到单播帧后，将帧交付上层处理，记录目的主机的IP地址和MAC地址到ARP高速缓存中(类似Cache的思路)，下次发送时，直接从ARP高速缓存中获取MAC地址，不需要再次发送ARP请求。
![Alt text](<Screenshot 2023-06-17 120925.png>)

### 集线器与交换机区别
集线器在物理层，交换机在数据链路层

单播情况下集线器会广播，但交换机能单播。

集线器需要遵循CSMA/CD协议，而交换机不需要。
![Alt text](<Screenshot 2023-06-18 103004.png>)

### 以太网交换机自学习和转发帧流程
例如:主机A给B发送帧，注意此时交换机2内也有A的信息了
![Alt text](<Screenshot 2023-06-18 103814.png>)

然后，主机B给主机A发送帧，此时由于上一次A发送时已经记录了A的MAC地址和接口，所以直接转发给A，无须盲目泛洪
![Alt text](<Screenshot 2023-06-18 104612.png>)

交换机中的帧交换表会定期自动删除，防止网络接口对应的设备更改

总结:
![Alt text](<Screenshot 2023-06-18 105114.png>)

### 以太网交换机的生成树协议STP Spanning Tree Protocol
添加冗余线路增加以太网可靠性，但是又会引入广播风暴(广播帧反复转发)的问题，设计生成树协议，阻塞一些端口，让网络拓扑结构变为最小生成树，来解决这个问题。

![Alt text](<Screenshot 2023-06-18 110018.png>)

### VLAN虚拟局域网
![Alt text](<Screenshot 2023-06-18 110756.png>)

但是，网络中会频繁出现广播信息

可以用路由器分隔广播域，但路由器成本较高，所以采用VLAN来解决这个问题。
![Alt text](<Screenshot 2023-06-18 111022.png>) 

### VLAN的实现机制
![Alt text](<Screenshot 2023-06-18 111840.png>)

打完标签再去标签，Access端口如下:
![Alt text](<Screenshot 2023-06-18 112258.png>)
![Alt text](<Screenshot 2023-06-18 112515.png>)

Trunk端口如下:
![Alt text](<Screenshot 2023-06-18 112757.png>)
如果PVID对不上，直接转发:
![Alt text](<Screenshot 2023-06-18 112852.png>)

## 第四章 网络层
两种服务:
- 虚电路:必须建立连接，类似电话
![Alt text](uTools_1687141562210.png)
- 无连接的数据报服务:不可靠服务
![Alt text](uTools_1687141695562.png)


### IPv4地址
IPv4地址是32位的二进制数，通常用点分十进制表示。
![Alt text](uTools_1687141806699.png)
除二倒取余:

![Alt text](uTools_1687141879712.png)

地址分类:
![Alt text](uTools_1687142047496.png)

A类地址基本分析:注意网络号和主机号全0全1情况
![Alt text](uTools_1687142219707.png)

B类地址:不用考虑网络号全0全1情况
![Alt text](uTools_1687142341482.png)

C类地址:同B类地址分析方法
![Alt text](uTools_1687142443497.png)

判断IPv4地址属于哪一类:看第一个字节的大小，在128(10000000)-191(10111111=255-64)闭区间之间的是B类地址，大的是C类地址，小的是A类地址。

判断是否可以指派:
1. A类网路号0，127不可指派
2. 主机号全0
3. 主机号全1

![Alt text](uTools_1687142892041.png)

### 子网划分
为什么要用子网掩码？为了知道多少位主机号被借用来作为子网号
![Alt text](uTools_1687143509101.png)
用地址和子网掩码与运算，得到网络号和子网号。
![Alt text](uTools_1687143617067.png)
把网络号外的化为二进制，然后看有n位1，就是有2^n个子网
![Alt text](uTools_1687143767002.png)
![Alt text](uTools_1687144043312.png)

### 无分类编址的IPv4
斜杠后面的数字表示用多少位表示网络地址
![Alt text](uTools_1687144455373.png)
![Alt text](uTools_1687144633439.png)

### IPv4应用规划
例子:用定长子网掩码来做子网划分
![Alt text](uTools_1687169439499.png)
本例中要划分五个子网，从主机号借用三位(2^3=8)来做子网号,所以子网掩码为255.255.255.244
![Alt text](uTools_1687169515583.png)

这样分配，由于网络5只需要4个地址，但是实际上有32个地址给它，浪费了
![Alt text](uTools_1687169614962.png)

变长子网掩码:斜杠表示法,按二的幂次分配，向上取二的幂次
![Alt text](uTools_1687170035406.png)

### IP数据报发送和转发过程
通过设置默认网关(路由器端口地址)，当一个网络中的主机要与另一个网络中的主机通信时会发送数据报给网关，网关通过数据报内信息，查表转发数据报。(通过目的地址与地址掩码相与来对比目的网络地址)

![Alt text](uTools_1687178407573.png)
广播数据报情况:目的地址为广播地址
![Alt text](uTools_1687178614431.png)

### 静态路由配置
在路由表中手动配置一些项
![Alt text](uTools_1687184252478.png)
问题一:如果手工配错，则会导致环路
![Alt text](uTools_1687184390399.png)
问题二:聚合环路，但是转发到一个不存在的网络，但这个网络包含于聚合网络的所有可能中。
![Alt text](uTools_1687184649953.png)
![Alt text](uTools_1687184582023.png)
解决办法:添加黑洞路由，将聚合网络的所有可能都转发到黑洞路由，这样就不会出现聚合环路的情况了。
![Alt text](uTools_1687184710493.png)
问题三:网络故障导致的路由环路
![Alt text](uTools_1687184831146.png)
解决办法：哪里坏了，哪里就当黑洞路由

### 路由选择协议
动静态路由选择区别：
![Alt text](uTools_1687185926876.png)
路由器作用:路由选择+分组处理
![Alt text](uTools_1687185893400.png)

### 路由信息协议 RIP Routing Information Protocol
RIP认为好的路由是跳数少的路由，最多15跳，16跳表示不可达
![Alt text](uTools_1687232886723.png)
C发送给D自己的路由表，D对路由表改造后更新自己的路由表
![Alt text](uTools_1687233138781.png)
路由环路问题: 
![Alt text](uTools_1687233459447.png)
![Alt text](uTools_1687233501802.png)
R2听了R1的谣言：
![Alt text](uTools_1687233577814.png)

### OSPF开放最短路径优先协议 open shortest path first
![Alt text](uTools_1687233990958.png)

![Alt text](uTools_1687234207622.png)
一段时间发送一个hello
![Alt text](uTools_1687234609391.png)
LSDB：Link State Database 链路状态数据库,通过洪泛算法来更新LSDB
![Alt text](uTools_1687234754973.png)
指定路由器DR和备用指定路由器BDR，减少发送信息的数量:
![Alt text](uTools_1687242409063.png)
OSPF划分了区域，这样可以用于大规模网络:
![Alt text](uTools_1687242506071.png)

### BGP边界网关协议 Border Gateway Protocol
IGP和OSPF用于内部网络，BGP用于外部网络
![Alt text](uTools_1687242588671.png)
自治系统之间，缺少统一度量，寻找最佳路由没意义
![Alt text](uTools_1687242660733.png)
![Alt text](uTools_1687242728600.png)
BGP只能力求找到一条比较好的路由，并不是最佳路由

考题:
![Alt text](uTools_1687243261657.png)
封装关系
![Alt text](uTools_1687243308001.png)

### IPv4数据报的首部格式
![Alt text](uTools_1687245025481.png)
长度计算:
![Alt text](uTools_1687245344000.png)
标识为，标志，片偏移
![Alt text](uTools_1687245481076.png)
MF(more fragment)取值为1，表示该数据报后面还有分片。DF(data frame)取值为1，表示不允许分片
![Alt text](uTools_1687246565639.png)
- 同一个数据报的分片，标识符相同，片偏移不同

- TTL：time to live 生存时间，每经过一个路由器，TTL减1，当TTL为0时，路由器丢弃该数据报，并向源主机发送ICMP超时差错报文。

- 协议:占8bit，表示上层协议，例如TCP，UDP，ICMP，IGMP等

- 首部检验和:检测首部是否出错，出错则丢弃该数据报，每经过一个路由器，检验和都要重新计算。

- 源ip和目的ip:32位

例题:
![Alt text](uTools_1687247355507.png)
片偏移量必须为整数
![Alt text](uTools_1687247403987.png)

一个十六进制数等于4bit
![Alt text](uTools_1687247562289.png)

### 网际控制报文协议ICMP Internet Control Message Protocol
终点不可达:
![Alt text](uTools_1687262181713.png)
源点抑制:
![Alt text](uTools_1687262373157.png)
时间超过:TTL归零
![Alt text](uTools_1687262533519.png)
参数问题:
![Alt text](uTools_1687262650685.png)
改变路由(重定向):有更好的路径！
![Alt text](uTools_1687262707293.png)

不发送报文的情况:
![Alt text](uTools_1687262752304.png)

询问报文:
![Alt text](uTools_1687262808107.png)

应用举例:ping 和 tracert(检测经过哪些路由器)

tracert原理:类似BFS，发送TTL=1,2,3...的报文，到达不同的路由后发送ICMP回答报文
![Alt text](uTools_1687263000692.png)

### 虚拟专用网VPN Virtual Private Network
远程访问内网资源
![Alt text](uTools_1687264922246.png)

### 网络地址转换NAT Network Address Translation
背景:IPv4地址不够用，用一个转换协议来拓展

NAT路由起一个转换的作用
![Alt text](uTools_1687265198455.png)
加入端口号(运输层):NAPT
![Alt text](uTools_1687265384605.png)
有NAT后不能由外网主机发起通信:
![Alt text](uTools_1687265417163.png)

## 第五章 运输层
之前的三层:网络层，数据链路层，物理层，完成了主机-主机通信。而运输层是从进程-进程通信。
![Alt text](uTools_1687401024149.png)

### 端口
利用端口号来区分进程
![Alt text](uTools_1687401260934.png)
常用协议及端口号:
![Alt text](uTools_1687402172614.png)
例子:用户PC通过UDP协议封装域名访问DNS服务器，DNS服务器通过UDP协议封装Web服务器ip地址返回用户PC。用户PC再向Web服务器发送HTTP请求报文，Web服务器通过TCP协议封装Web页面返回用户PC。
![Alt text](uTools_1687402637626.png)

### UDP对比TCP
UDP: User Datagram Protocol 用户数据报协议

TCP: Transmission Control Protocol 传输控制协议

UDP无连接，TCP面向连接

以下是一些区别:
![Alt text](uTools_1687417353514.png)
![Alt text](uTools_1687417422597.png)
![Alt text](uTools_1687417617335.png)
![Alt text](uTools_1687417824286.png)
![Alt text](uTools_1687417958412.png)

### TCP流量控制——滑动窗口
利用rwnd变量来控制发送方发送速率。ACK=1表示确认，ack为累计确认的计数器
![Alt text](uTools_1687418761092.png)
如果收到一个窗口为0的报文，启动持续计时器，每隔一段时间发送零窗口探测报文，验证是否要发送数据。
![Alt text](uTools_1687418904377.png)
例题:滑动窗口
![Alt text](uTools_1687419106671.png)

### TCP拥塞控制
什么是拥塞？
![Alt text](uTools_1687419634079.png)
四种拥塞算法:
1. 慢开始
2. 拥塞避免
3. 快重传
4. 快恢复

如下图:慢开始+拥塞避免
![Alt text](uTools_1687420064209.png)
重传计时器超时，不代表一定拥塞，这时引入快重传算法
![Alt text](uTools_1687420594879.png)
四种算法一起用:
![Alt text](uTools_1687420685060.png)

例题:
![Alt text](uTools_1687420786671.png)

### TCP超时重传时间选择
RTO：Retransmission TimeOut 超时重传时间
![Alt text](uTools_1687422227625.png)

![Alt text](uTools_1687423407225.png)

### TCP可靠传输的实现
TCP为全双工通信，两边都在发送和接受报文，每一方都有自己的发送窗口和接受窗口。
![Alt text](uTools_1687425502214.png)
接受方给发送方的报文信息中包含了窗口的尺寸(发送窗口，大小由上述的算法决定)，而发送方给接收方的报文中就是数据报。
![Alt text](uTools_1687425547025.png)

### TCP连接建立
建立过程:
1. 甲:听得到吗
2. 乙:听得到哦
3. 甲:我也听得到

![Alt text](<Screenshot 2023-06-23 110210.png>)

如果是两次握手:那么这种情况将会导致TCP客户服务进程资源浪费。

例题:
![Alt text](<Screenshot 2023-06-23 110649.png>)
第二次握手是对第一次的确认，所以ack=seq+1

## 第六章 应用层
### C/S 和 P2P 模式
![Alt text](uTools_1688005988773.png)

![Alt text](uTools_1688006030213.png)
### DHCP 动态主机配置协议 Dynamic host config protocol
如果手工配置主机让其联网，工作量较大:
![Alt text](uTools_1688011627388.png)
配置一台DHCP服务器，让主机去获取自己的配置信息：
![Alt text](uTools_1688011668753.png)

第一轮:主机没有配置ip地址，所以先以0.0.0.0发送广播地址，服务器返回的也是广播，然后客户再请求ip地址，获得DHCP同意
![Alt text](uTools_1688012553870.png)
过了0.5租用期后要再次请求续租，如果过了租用期就要停止IP地址并重发送DHCP DISCOVER报文
### DNS 域名系统 Domain name system
![Alt text](uTools_1688006455980.png)

通常采用递归+迭代查询方法
![Alt text](uTools_1688006489148.png)

如果缓存里有DNS信息，直接根据域名访问，如果没有，那么最多需要查询四次(根域名，顶级域名，权限域名，权限域名)
![Alt text](uTools_1688006730541.png)

### FTP 文件传输协议 File Transfer Protocol
![Alt text](uTools_1688010080549.png)

一条TCP用来传输控制命令，一条TCP用来传输数据

![Alt text](uTools_1688010151936.png)
端口号21控制连接，端口号20数据连接，这些端口号都指的是服务器的

### 电子邮件
用户代理+邮件服务器+协议
![Alt text](uTools_1688010272455.png)
采用SMTP发送，POP3读取
![Alt text](uTools_1688010318504.png)

SMTP原理:
![Alt text](uTools_1688010447876.png)
过程中传输7Bit码
![Alt text](uTools_1688010518292.png)
### 万维网 World wide web
统一资源定界符URL uniform resource location
![Alt text](uTools_1688011128031.png)

HTTP协议
![Alt text](uTools_1688011187839.png)

发送HTTP报文
![Alt text](uTools_1688011217487.png)