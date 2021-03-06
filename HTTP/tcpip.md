# 七层模型等

## 有关模型

### OSI七层模型

![20180308152048952296938.jpg](http://osmisz4zw.bkt.clouddn.com/20180308152048952296938.jpg)


应用层：网络服务与最终用户的一个接口
协议有：HTTP,FTP,TFTP,SMTP,SNMP,DNS,TELNET,HTTPS,POP3,DHCP

表示层：数据的表示，安全，压缩（在五层模型中合并到了应用层）
格式有：JPEG，ASCII，DECOIC，加密格式等

会话层：建立，管理，终止会话，（在五层模型中合并到了应用层）
对应主机的进程，指的是本地主机和远程主机正在进行的会话

传输层：定义传输数据的协议端口号，以及流控和差错校验。
协议：TCP，UDP，数据一离开网卡便进入网络传输层。

网络层：进行逻辑寻址，实现不同网络之间的路径选择。
协议有：ICMP IGMP IP（IPV4 IPV6） ARP RARP


数据链路层：建立逻辑连接、进行硬件地址寻址、差错校验[2]  等功能。（由底层网络定义协议）
将比特组合成字节进而组合成帧，用MAC地址访问介质，错误发现但不能纠正。

物理层：建立、维护、断开物理连接。（由底层网络定义协议）

TCP/IP 层级模型结构，应用层之间的协议通过逐级调用传输层（Transport layer）、网络层（Network Layer）和物理数据链路层（Physical Data Link）而可以实现应用层的应用程序通信互联。

应用层需要关心应用程序的逻辑细节，而不是数据在网络中的传输活动。应用层其下三层则处理真正的通信细节。在 Internet 整个发展过程中的所有思想和着重点都以一种称为 RFC（Request For Comments）的文档格式存在。针对每一种特定的 TCP/IP 应用，有相应的 RFC[3]  文档。

一些典型的 TCP/IP 应用有 FTP、Telnet、SMTP、SNTP、REXEC、TFTP、LPD、SNMP、NFS、INETD 等。RFC 使一些基本相同的 TCP/IP 应用程序实现了标准化，从而使得不同厂家开发的应用程序可以互相通信


### TCP/IP 五层

![20180308152048954710664.jpg](http://osmisz4zw.bkt.clouddn.com/20180308152048954710664.jpg)

### TCP三次握手四次挥手
![2018030815204896156122.jpg](http://osmisz4zw.bkt.clouddn.com/2018030815204896156122.jpg)
client -> (SYN = 1,SEQ = X) -> SERVER
SERVER -> (SYN = 1,ACK = X+1,SEQ = Y) ->CLIENT
CLIENT -> (ACK = Y+1,SEQ = Z) -> SERVER

两次会发生死锁


![20180308152048962322157.jpg](http://osmisz4zw.bkt.clouddn.com/20180308152048962322157.jpg)


MIAN ->  (FIN = 1,ACK = Z,SEQ = X) -> BEI
BEI  ->  (ACK= X+1,SEQ = Z)        -> MAIN
BEI  ->  (FIN = 1,ACK = X,SEQ = Y) -> MAIN
MAIN ->  (ACK= Y,SEQ = X)          -> BEI

四次是为了保证数据都传输完毕了。


各个层是干什么的

### TCP和UDP的区别以及拥塞控制
以下内容摘自百度经验：
> TCP(传输控制协议)：

1)提供IP环境下的数据可靠传输(一台计算机发出的字节流会无差错的发往网络上的其他计算机，而且计算机A接收数据包的时候，也会向计算机B回发数据包，这也会产生部分通信量)，有效流控，全双工操作(数据在两个方向上能同时传递)，多路复用服务，是面向连接，端到端的传输;

2)面向连接：正式通信前必须要与对方建立连接。事先为所发送的数据开辟出连接好的通道，然后再进行数据发送，像打电话。

3)TCP支持的应用协议：Telnet(远程登录)、FTP(文件传输协议)、SMTP(简单邮件传输协议)。TCP用于传输数据量大，可靠性要求高的应用。

> UDP(用户数据报协议，User Data Protocol)

1)面向非连接的(正式通信前不必与对方建立连接，不管对方状态就直接发送，像短信，QQ)，不能提供可靠性、流控、差错恢复功能。UDP用于一次只传送少量数据，可靠性要求低、传输经济等应用。

UDP支持的应用协议：NFS(网络文件系统)、SNMP(简单网络管理系统)、DNS(主域名称系统)、TFTP(通用文件传输协议)等。
总结：

> TCP：面向连接、传输可靠(保证数据正确性,保证数据顺序)、用于传输大量数据(流模式)、速度慢，建立连接需要开销较多(时间，系统资源)。

> UDP：面向非连接、传输不可靠、用于传输少量数据(数据包模式)、速度快。


![20180308152049049873017.jpg](http://osmisz4zw.bkt.clouddn.com/20180308152049049873017.jpg)

### TCP拥塞控制和流量控制



### HTTP1.0、HTTP1.1和HTTP2.0的区别

[简书HTTP1.0、HTTP1.1和HTTP2.0的区别](https://www.jianshu.com/p/be29d679cbff)

### 拥塞控制和流量控制

[TCP/IP详解--拥塞控制 & 慢启动 快恢复 拥塞避免](http://blog.csdn.net/kinger0/article/details/48206999)

2. 几种拥塞控制方法

    慢开始( slow-start )、拥塞避免( congestion avoidance )、快重传( fast retransmit )和快恢复( fast recovery )。

2.1 慢开始和拥塞避免

    发送方维持一个拥塞窗口 cwnd ( congestion window )的状态变量。拥塞窗口的大小取决于网络的拥塞程度，并且动态地在变化。发送方让自己的发送窗口等于拥塞。

