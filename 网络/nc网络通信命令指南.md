# 一、 nc 网络通信命令简介
<br/>
nc命令可以用来作为某些服务的检测，因为它可以连接到某个port来进行通信，此外还可以自行启动一个port来监听其他用户的连接。如果在编译nc软件的时候给予"GAPING_SECURITY_HOME"参数的话，这个软件还可以用来取得客户端的bash。我们的CentOS默认并没有给予上面的参数，所以我们不能够用它来作为黑客软件。

**注：** 有的系统将执行文件nc改名为netcat。
<br/>
<br/>

# 二、 语法
<br/>

    
    发送端：
    nc [-u] [IP|host] [port]
    
    监听端：
    nc -l [IP|port] [port]


<br/>
<br/>

# 三、 选项和参数
<br/>


    -l ：作为监听之用，也就是打开一个 port 来监听用户的连接
    -u ：不使用 TCP 而是使用 UDP 作为连接的数据包状态


<br/>
<br/>

# 四、 范例
<br/>

## 1、 与 telnet 类似，连接本地端的p ort 22 查阅相关信息


    $ nc localhost 22
    SSH-2.0-OpenSSH_5.3

<br/>

## 2、建立两个连接传递数据，测试其间的网络通信状态
首先在服务器启动一个port来进行监听：


    $ nc -l localhost 22222
    123123
    hello!   


然后再开另外一个终端，利用nc来连接我们监听的服务器，这样我们就可以输入内容进行通信了


    $ nc localhost 22222
    123123
    hello!


<br/>



