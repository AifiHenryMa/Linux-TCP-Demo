# Linux-TCP-Demo
用Linux C 写的一个socket TCP例程，采用C/S模式；过程清晰，易于理解

程序中主要语句说明如下：
## 服务器端
1) 建立socket。程序调用socket()函数，该函数返回一个类似于文件描述符的句柄，同时也意味着为一个socket数据结构分配存储空间。用语句实现：
```c
socket(AF_INET,SOCK_STREAM,0);
```
其中，参数AF_INET表示采用IPv4协议进行通信；参数SOCK_STREAM表示采用流式socket，即TCP。

2) 绑定bind。将socket与本机上的一个端口绑定，随后就可以在该端口监听服务请求。用语句实现：
```c
bind(sockfd,(struct sockaddr *)&my_addr,sizeof(struct sockaddr));
```
其中，参数my_addr表示指向包含本机IP地址及端口号等信息。

3) 建立监听listen。使socket出于被动的监听模式，并为该socket建立一个输入数据队列，将到达的服务请求保存在此队列中，直到程序处理它们。用语句实现：
```c
listen(sockfd,BACKLOG);
```
其中，参数BACKLOG表示最大连接数。

4) 响应客户请求accept。用**函数accept生成一个新的套接口描述符，让服务器接收客户的连接请求**。用语句实现：
```c
accept(sockfd,(struct sockaddr *)&remote_addr,&sin_size);
```
其中，参数remote_addr用于接收客户端地址信息；参数sin_size用于存放地址的长度。

5) 发送数据send。该函数用于在面向连接的socket上进行数据发送。用语句实现：
```c
send(client_fd,’连接上了 \n’,26,0);
```
其中，26表示以字节为单位的长度。

6) 关闭close。停止在该socket上的任何数据操作。用语句实现：
```c
close(client_fd);
```

## 客户端
1) 建立socket。程序调用socket()函数，该函数返回一个类似于文件描述符的句柄，同时也意味着为一个socket数据结构分配存储空间。用语句实现：
```c
socket(AF_INET,SOCKET_STREAM,0);
```
2) 请求连接connect。启动和远端主机的直接连接。用语句实现：
```c
connect(sockfd, (struct sockaddr*) &serv_addr, sizeof(struct sockaddr));
```

3) 接收数据recv。该函数用于面向连接的socket上进行数据接收。用语句实现：
```c
recv(sockfd,buf,MAXDATASIZE,0);
```
4) 关闭close。停止在该socket上的任何数据操作。用语句实现：
```c
close(sockfd);
```
