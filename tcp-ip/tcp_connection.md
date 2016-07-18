## TCP连接的建立与终止

### 目录 


* [简介](#简介)
* [TCP三次握手](#tcp三次握手)
* [四次挥手](#四次挥手)
* [TCP状态迁移](#tcp状态迁移)

### 简介
TCP发送数据之前，必须在双方之间建立一条连接，建立连接的过程称之为"TCP三次握手"。

### TCP三次握手

![] [tcp-connect]

三次握手过程：

- 第一次握手  
  > 客户端主动发起同步，发送SYN为client_isn的TCP包，要求与服务器建立连接（**SYN位置1**）；
- 第二次握手  
  > 服务器收到客户的同步包，返回SYN为server_isn且ACK为client_isn+1的确认包，同意与客户进行连接（**SYS位置1，ACK位置1**）；
- 第三次握手  
  > 客户端必须确认服务器发送来的SYN包，确认号为server_isn+1（**ACK位置1**）;

TCP很多情况可能出现无法连接的现象（服务器关闭或非正常状态时），一般一个新连接的最长时间限制为75秒。  

### 四次挥手
建立一个TCP连接需要三次握手，而终止一个TCP连接需要四次挥手，这是**由TCP半关闭造成的**。  
TCP连接是双工的，因此**每个方向必须单独关闭**。一个TCP连接收到FIN后仍然能发送数据。  

![] [tcp-close]

四次挥手过程：

- 第一次挥手

  > 主动关闭方向另一端发送序号为M的FIN包；

- 第二次挥手

  > 被动关闭方接收到FIN后，必须对该FIN包进行确认，返回确认号为M+1的ACK包； 同时被动方向应用程序传送一个文件结束符；

- 第三次挥手

  > 被动方数据全部发送完成后，向另一端发送序号为N的FIN包；

- 第四次挥手

  > 主动方接收到被动方的FIN后，必须对该包进行确认，返回确认号为N+1的ACK包；

### TCP状态迁移
**TCP服务端状态迁移**  

![] [tcp-connect-status]

客户端TCP状态迁移：  
CLOSED->SYN_SENT->ESTABLISHED->FIN_WAIT_1->FIN_WAIT_2->TIME_WAIT->CLOSED  
服务器TCP状态迁移：  
CLOSED->LISTEN->SYN_RECV->ESTABLISHED->CLOSE_WAIT->LAST_ACK->CLOSED  
  
各状态的意义：

- CLOSED
  
  > 没有建立连接；

- LISTEN

  > TCP服务器监听远端的连接请求；

- SYN_SENT

  > 客户端主动发起连接后等待服务器确认；

- SYN_RECV

  > 在收到和发送一个连接请求后，服务器等待对方确认时；

- ESTABLISHED

  > 成功建立一个新连接，双方可以发送数据；

- FIN_WAIT_1

  > 主动关闭连接发送FIN包后，等待对方的确认；

- FIN_WAIT_2

  > 主动方收到对方对关闭请求的确认后；
- CLOSED_WAIT

  > 被动关闭方收到关闭请求并返回关闭请求确认后；

- LAST_ACK

  > 被动关闭方关闭连接，等待对方的确认；

- TIME_WAIT

  > 等待足够时间，以确保远端接收到连接关闭请求的确认；


[tcp-connect]: http://hi.csdn.net/attachment/201108/7/0_1312718352k8l6.gif  "TCP三次握手"
[tcp-close]: http://hi.csdn.net/attachment/201108/7/0_1312718564tZXD.gif "TCP四次挥手"
[tcp-connect-status-bak]: http://images.cnitblog.com/blog/88420/201402/181351206012825.png "TCP状态迁移"
[tcp-connect-status]: http://img.my.csdn.net/uploads/201209/24/1348471799_4164.jpg "TCP状态迁移"
