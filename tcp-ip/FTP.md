## FTP:文件传送协议
- - -

### 目录



* * * 

### FTP协议
FTP采用**两个TCP连接**来传输一个文件。  

- 控制连接
  > 服务器监听21端口，等待客户的连接。由于命令通常是用户键入的，所以IP对控制连接的服务特点是“最大限度地减少延迟”。

- 数据连接
  > 该连接用户传输文件，IP对数据连接的服务特点是"最大限度地提高吞吐量"，

### 连接管理
数据连接有以下三个用途：  

- 从客户向服务器发送一个文件；
- 从服务器向客户发送一个文件；
- 从服务器向客户发送文件或目录列表；