# socket



### 进程

程序运行之后叫进程



### 知名端口

```
80端口http
21端口 FTP
```

### 动态端口

1024-65535

六万多个端口，足够用了，电脑上不可能运行这么多的程序



## socket知识

要实现进程之间的通信，首先要解决的问题是如何唯一标识一个进程 ，否则通信无从谈起。

在1台电脑上可以通过进程号(PID)来唯一标识一个进程，但是在网络中这是行不通的。

其实TCP\IP协议族已经帮我们解决了这个问题，网络层的IP地址可以唯一标识网络中的主机，而传输层的"协议+端口"可以唯一标识主机中的应用进程。

这样利用==IP地址+协议+端口==就可以标识网络的进程了，网络中的进程通信就可以利用这个标识与其他进程进行交互。



## 私有ip

在这么多网络中，国际规定有一部分IP地址是用于我们的局域网使用，也就是属于私网IP，不在公网中使用的，他们的范围是：

```python
10.0.0.0~10.255.255.255
172.16.0.0~172.31.255.255
192.168.0.0~192.168.255.255
```

在这里面的数据，是不能上互联网的，

我在家里通过路由器连接上一个网，这个路由器给我分配的一个IP地址，这个地址就是私有IP，是不能互联网的

在百度上搜IP，给出的本机IP才是在互联网中本机的IP



## socket使用方法

与文件的使用流程很类似

1. 创建套接字
2. 使用套接字收\发数据
3. 关闭套接字



### 创建socket

在python中使用socket模块的函数socket就可以完成

```python
import socket
socket.socket(AddressFamily,Type)
```

#### 说明：

函数socket.socket创建一个socket，该函数带有两个参数

- Address Family：可以选择AF_INET（用于Internet进程**间**通信）或者AF_UNIX（用于同一台及其进程间通信），实际工作中常用AF_INET
- Type：套接字类型，可以是SOCK_STREAM（流式套接字，主要用于TCP协议）或者SOCK_DGRAM（数据包套接字，主要用于UDP协议）

创建一个tcp socket

```python
import socket
#创建TCP的套接字
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)

#这里是使用套接字的功能...

#不用的时候，关闭套接字
s.close()
```

udp套接字类似

SOCK_DGRAM



### 发送数据

```python
s.sendto(发什么,发给谁  ip+端口号)  后面的发给谁用元组表示
```

**发送的数据类型必须是byte类型的，不能是字符串**



检验该IP地址是否通畅

```bash
ping IP地址
```



若不通畅，修改ubuntu的网络模式为桥接（自动检测）   

若还是不行  则使用命令  `sudo dhclient`：等待别人给你分配一个IP，只要你保证是桥接状态了（自动检测），就基本可以保证和相邻的计算机处于同一个子网下



```python
s = socket(AF_INET,SOCK_DGRAM)#使用udp发送报文
s.sendto(b"hahahahah",("10.35.42.108",8000))
s.close()
```



#### 更通用的方式

将用户输入的数据发送到Windows上，使用exit退出

```python
while True:
	udp_data = input("请输入你要发送的信息:")
    if(udp_data=="exit")
    	break;
    udp_socket.sendto(udp_data.encode("utf-8"),("10.35.42.108"),8000)
```





## 接收udp

使用工具向ubuntu接收数据，ubuntu接收数据必须要有一个**固定的端口号**



一个简单的接收案例

```python
# coding=utf-8
from socket import *

# 1.创建套接字
udp_socket = socket(AF_INET,SOCK_DGRAM)
# 2.绑定本地的相关信息，如果一个网络程序不绑定，则系统会随机分配
localaddr = ("",7788) # ip地址和端口号，ip地址一般不用写，表示本机的任何一个ip，端口号为自己规定的任意一个端口号，大于1024小于65535即可，是本接收程序的端口号
# 必须绑定自己电脑的ip和port，否则不行
udp_socket.bind(localaddr)

while True:

    # 3.等待接收对方发送的数据
    recv_data = udp_socket.recvfrom(1024) #1024表示本次接收的最大字节数
    # 4.显示接收到的数据
    # 接收到的recv_data是一个元组
    # [0]是数据  [1]是发送ip+端口  [2]是接收端口
    print(recv_data[0].decode('gbk'))
    recv_msg = recv_data[0]

    send_addr = recv_data[1] # 源地址
    dest_addr = recv_data[2] # 目的地址
    print("%s:%s"%(str(send_addr),recv_msg.decode('utf-8'))

# 5.关闭套接字
udp_socket.close()
```



windows中默认的中文编码：GBK编码     ubuntu中的默认编码：utf-8

win发送的默认编码都是GBK，只要是从win发送的，用GBK解码decode









### 绑定端口号

发送方不一定要分配端口号，接收方必须分配一个端口号

同一时刻，一个端口号只能由一个程序使用，不能被多个应用程序占用，操作系统不允许



## 聊天器

### 写代码思想

正着推，倒着推 写程序的思路，正着推推不出来了再倒着推

### 好习惯

- 函数与函数之间空两行
- 第一个函数与前面的额代码也要空两行
- 注释# 后面加一个空格



一个套接字可以同时收，同时发

用同一个套接字，收和发

- 单工：百分之百的只能指定一个方向走：比如收音机
- 半双工：发的时候收不了，收的时候发不了，同一时刻只能有同一个方向，比如：对讲机
- 全双工：同一个时刻既可以发，也可以收

socket特性是**全双工**，只是在目前的程序中没有体现全双工而已



### lo本地回环地址

本机数据发送给127.0.0.1就相当于发送给自己电脑，可以实现本机上的两个应用程序的通信

```bash
127.0.0.1
```



### recvfrom的特点

当数据没有到来时，他会阻塞，等待数据的到来

有数据发送来时，若还没有调用recvfrom 则操作系统会先默认将数据存起来，相当于操作系统代收快递，等到recvfrom调用之后再从操作系统中取出，

**这里可能会出现程序漏洞**：操作系统大管家，来者不拒

![image-20211124185907034](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20211124185907034.png)

如  我把小明电脑上的所有端口扫描一遍，发现他的8080端口在开着，那么我忘他的8080端口发 一个好几G的大文件，操作系统来者不拒，那么操作系统的缓存区被占满，正常的数据就无法再被操作系统接收

所以，如果调用recvfrom，就一定要while true  一直recvfrom





接收信息时的decode ，若在win上接收消息，则decode成gbk；在除win以外的系统上，使用utf-8





## tcp

udp想象成写信的过程



### tcp客户端

```python
# 创建tcp套接字

# 连接服务器

# 发送数据 接收数据
# send 不是sendto  而且send中只有数据

# 关闭端口
```

客户端一般不绑定端口



### tcp服务器

```python
# socket创建一个套接字

# bind绑定ip和port

# listen使套接字变为可以被动链接

# accept等待客户端的链接

# recv\send接收发送数据
```



#### 生活中的电话机

1. 买个手机

2. 插上手机卡

3. 设计手机为正常接听状态(即能够响铃)

4. 静静的等待别人打(accept)
   accept返回值是一个元组，其中有两个参数
   第一个变量用来接收一个新的套接字，第二个变量用来接收链接**客户端的地址（谁给你打的电话）**

   新的套接字相当于找了一个人工智障找了一个新的人工客服，客户端的地址相当于客户的电话号码

   **监听套接字**和**服务套接字**是两个套接字

   - 监听套接字：是tcp_server_socket，处于listen状态，时刻用于监听来自四面八方的请求   **监听套接字只负责监听**，负责等待有新的客户端进行链接

     监听套接字默认处于阻塞状态，当有新的客户链接时，也就是有人给你打电话时，会解阻塞

   - 服务套接字：是accept返回的第一个参数，表示另开一个套接字，用来向申请请求的客户端提供服务。直白点讲，有多少个客户，服务器中就有多少个套接字   **服务套接字用来通信**，用来为客户端服务

     接下来收发数据，用的都是这个新生成的套接字，一开始创建的套接字已经被用作监听了



**注意** ：拆包！！等号左边是两个变量，等号右边是一个元组  python特性

```python
a,b = (10,20) # 拆包
```



recv默认是堵塞，有两个条件可以解阻塞

- 接收到从客户端发来的数据
- 客户端点击关闭

服务器要怎么区别这两种解阻塞的方法呢？

看recv_data是否为空。若recv_data为空，则一定是客户端关闭了链接，调用了close；若不为空，则一定是客户端调用了send方法发送来了数据（因为send无法发送空的数据）



python中，if后面：

- 是数字：不是0就是True
- 是元组，字典，列表，集合，字符串：不是空 就是True
- None，False不成立



#### tcp服务器源代码

```python
from socket import *

def main():
    # 1.买个手机(socket)
    tcp_server_socket = socket(AF_INET,SOCK_STREAM)

    # 2.插入手机卡(bind)
    server_addr = ("",7788)
    tcp_server_socket.bind(server_addr)

    # 3.将手机设置为正常的响铃模式（让默认的套接字有主动变为被动） 创建套接字的默认目的是为了链接别人(listen)
    tcp_server_socket.listen(128) # 

    while True:
        print("等待一个客户的链接....")
        # 4.等待别人的电话(accept)
        new_client_server,client_addr = tcp_server_socket.accept()

        print("成功收到客户的链接请求!")
        print("打印客户的地址如下:")
        print(client_addr)
        while True:
            # 接受客户发来的信息
            tcp_recv_msg = new_client_server.recv(1024) # 同recvfrom方法一样，但是这个recv之返回数据，端口号不需要了，链接的时候已经有了
            if tcp_recv_msg : # tcp_recv_msg解阻塞并且返回值为空，验证客户已经下线
                print("客户发来的信息如下:")
                print(tcp_recv_msg.decode("gbk"))
                # 服务器回一个收到
                new_client_server.send("收到".encode("gbk"))
            else:
                # 服务器说再见
                new_client_server.send("再见!".encode("gbk"))
                break;

        # 关闭套接字
        new_client_server.close()
        print("已经为这个客户端服务完毕!")

    tcp_server_socket.close()

if __name__ == "__main__":
    main()
```





### 案例：文件下载器

什么是下载？

下载就是在本地先建一个同名文件，然后将数据从服务器传送到本地主机，再写入创建的文件    在本地创建一个文件，服务器发什么，客户端收什么，发什么收什么

分为两部分

- 服务器的发送方
- 客户端的接收方（一般比较简单）



如果使用`with`  open文件，如果在打开或者读写文件时出现异常，则百分之百保证调用close方法，不用再写try  except了，比较方便

```python
with open("xxx","wb") as f: # 打开该文件，用f指向这个文件，若出现异常，则调用close方法
    f.read()/write()
```





**注意**：

- 只要发送数据，就要检查是不是字节流，如果不是（如是字符串），就要encode
- 只要接收数据，也要检查是不是字节流，如果不是，就要decode



with只有在确保能够打开文件的时候，才会使用，这时确保能打开文件，若文件读写的过程中出现了异常，则with确保文件能够调用close方法，而不会死掉。若是连文件都打不开，则不能使用with方法，而是要使用一个标志变量，先指向None，若文件打开成功则指向该文件；若文件打开不成功则还是None，最后判断该变量是否还是None即可。





#### client

```python
from socket import *

def main():
    # 1.创建套接字
    tcp_socket = socket(AF_INET,SOCK_STREAM)

    # 2.获取服务器的ip port
    dest_ip = ""
    dest_port = 9999

    # 3.链接服务器
    tcp_socket.connect((dest_ip,dest_port))

    # 4.让客户输入要下载的文件的名字
    download_file_name = input("请输入要下载的文件的名称:")

    # 5.将文件名发送到服务器，告诉服务器我要下载哪一个文件
    tcp_socket.send(download_file_name.encode("utf-8"))

    # 6.接收服务器传来的该文件中的数据
    recv_data = tcp_socket.recv(1024)

    # 7.保存接收的数据到本地文件
    with open("recv"+download_file_name,"wb") as f:
        f.write(recv_data)

    # 8.关闭套接字
    tcp_socket.close()

if __name__ == "__main__":
    main()
```



#### server

```python
from socket import *

def main():
    # 1.创建套接字
    tcp_socket = socket(AF_INET,SOCK_STREAM)

    # 2.服务器绑定端口
    tcp_socket.bind(("",9999))

    # 3.listen监听数据
    tcp_socket.listen(128) # 这里的128表示最多允许128个设备同时访问服务器

    # 不停地等待客户端链接
    while True:
        # 4.accept接收数据，并拆包
        new_client_socket,client_addr = tcp_socket.accept()
        
        file_content = None
        # 注意这里接收的是文件的名称
        # 5.尝试打开文件，并读其中的数据
        file_name = new_client_socket.recv(1024).decode("utf-8")
        try:
            with open(file_name,"rb") as f:
                file_content = f.read()
                f.close()
        except Exception as ret:
            print("没有要下载的文件!")

        if file_content: # 如果读到了内容
            new_client_socket.send(file_content)
            client_ip,client_port = client_addr # 拆包
            print(client_ip+"成功下载文件"+file_name)
            # 若file_content为空则证明服务器没有找到该文件

        # 6.关闭这个服务套接字
        new_client_socket.close()

    # 7.关闭tcp套接字
    tcp_socket.close()

if __name__ == "__main__":
    main()
```





### tcp注意点

1. tcp服务器一般情况下需要绑定端口，而tcp客户端一般情况下不需要绑定，请问为什么？
   tcp服务器绑定端口是为了让客户端能够找到这个服务器
   tcp客户端没有必要绑定端口，若绑定端口则不能双开，甚至若该端口已经被占用，会导致tcp客户端打开失败。

2. tcp服务器中通过listen可以将socket创建出来的主动套接字变为被动的，这是做tcp服务器时必须要做的

3. 当客户端需要链接服务器时，就需要使用connect进行链接，udp是不需要链接的而是直接发送，但是tcp必须先链接，只有连接成功才能通信

4. 当一个tcp客户端连接服务器时，服务器端会有一个新的套接字，这个套接字用来标记这个客户端，单独为这个客户端服务

5. listen后的套接字是被动套接字，用来接收新的客户端的链接请求，而accept返回的套接字是标记这个新的客户端的

6. 关闭listen后的套接字意味着被动套接字关闭了，会导致新的客户端不能够链接服务器，但是之前已经链接成功的客户端正常通信

7. 关闭accept返回的套接字意味着这个客户端已经服务完毕

8. 当客户端的套接字调用close后，服务器端会recv解阻塞，并且返回的长度为0，因此服务器可以通过返回数据的长度来区别客户端是否已经下线。

   服务器端recv解阻塞的两种情况

   - 收到一个发送来的数据
   - 客户端调用close，此时返回的长度为0
