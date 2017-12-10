---
title: TCP状态变换——“3次握手4次挥手”
date: 2017-12-10 15:03:50
tags:
  -TCP/IP
---
先放上著名的“3次握手4次挥手”示意图：
![](TCPConnection/Connection.png)
TCP(Transmission Control Protocol)是一种面向连接的、可靠的、基于字节流的传输层通信协议。

TCP连接的建立可以简单地称为3次握手，而连接的中止则可以称为4次挥手。<!--more-->

# 建立连接
在TCP/IP协议中，TCP协议提供可靠的链接服务，采用三次握手建立一个连接。
## 1.第一次握手：建立连接时，客户端发送SYN包（SYN=J）到服务器，并进入SYN_SEND状态，等待服务器确认。
## 2.第二次握手：服务器收到SYN包，必须确认客户的SYN（ACK=J+1），同时自己也发送一个SYN包（SYN=K），即SYN+ACK包，此时服务器进入SYN_RECV状态。
## 3.第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK（ACK=K+1），此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成3次握手。
完成三次握手后，客户端和服务器开始传送数据，也就是ESTABLISHED状态。

# 结束连接
TCP有一个很特别的概念，叫“半关闭”，因为TCP的连接时全双工（可以同时发送和接收）连接，因此在关闭连接的时候，必须关闭发送和接收双方的连接。客户机给服务器发送一个FIN的TCP报文，客户机处于FIN_WAIT_1（主动关闭）服务器收到报文同时返回给客户端一个ACK报文，此时服务器处于CLOSE_WAIT（被动关闭）状态，客户机收到报文后仍处于FIN_WAIT_1状态。服务器发送FIN报文给客户端，客户端收到后处于TIME_WAIT状态，表示已收到对方的FIN报文，并且发送ACK报文，等待2MSL（Maximum Segment Lifetime）后就会回到COLSED可用状态。服务器收到客户端的ACK报文后，就会处于CLOSED状态。

# 标志含义
1. <b>URG标志</b>，表示紧急指针(urgent pointer)是否有效。
2. <b>ACK标志</b>，Acknowledgement Number,  表示确认号是否有效，一般称携带ACK标志的TCP报文段为“确认报文段”。
3. <b>PSH标志</b>，提示接收端应用程序应该立即从TCP接收缓冲区中读走数据，为接收后续数据腾出空间（如果应用程序不将接收到的数据读走，它们会一直停留在TCP接收缓冲区中）。
4. <b>RST标志</b>，表示要求对方重新建立连接，一般称携带RST标志的TCP报文段为“复位报文段”。
5. <b>SYN标志</b>，表示请求建立一个连接，一般称携带SYN标志的TCP报文段为“同步报文段”。
6. <b>FIN标志</b>，表示通知对方本端要关闭连接了，一般称携带FIN标志的TCP报文段为“结束报文段”。

# TCP的连接状态
1. <b>CLOSED</b>: 表示初始状态
2. <b>LISTEN</b>: 表示服务器端的某个socket处于监听转台可以接收连接。
3. <b>SYN_SENT</b>: 在服务端监听后，客户端socket执行CONNECT连接时，客户端发送SYN报文，此时客户端就进入STN_SENT状态，等待服务端的确认。
4. <b>SYN_RCVD</b>: 表示服务端接收到了SYN报文，在正常情况下，这幢状态是服务端的socket在建立TCP连接时的3次握手会话过程中的一个中间状态，很短暂，基本上用网络查询工具netstat很难看到这种状态。
5. <b>ESTABLISHED</b>: 表示连接已经建立了。
6. <b>FIN_WAIT_1</b>: 这是已经建立连接后其中一方请求中止，等待对方FIN报文的状态。
7. <b>FIN_WAIT_2</b>: 有一方要求关闭连接，同时还告诉对方，还有一点数据没有传输完成，请稍后在关闭连接。
8. <b>TIME_WAIT</b>: 表示收到了对方的FIN报文，并已发送出了ACK报文，等待2MSL(Maximum Segment Lifetime)后就会回到CLOSED状态。
9. <b>CLOSING</b>: 比较少见。
10. <b>CLOSE_WAIT</b>: 等待关闭。
11. <b>LAST_ACK</b>: 被动关闭一方在发送FIN报文后，最后等待对方的ACK报文。
12. <b>CLOSED</b>: 当收到ACK报文后，进入CLOSED可用状态。