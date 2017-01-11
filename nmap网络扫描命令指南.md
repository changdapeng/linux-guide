# 使用端口扫描程序 nmap（需要下载安装）

<br/>
nmap 是被系统管理员用来进行 系统安全性检查的工具。nmap可以通过程序内部自定义的几个port对应的指纹数据来查出该port的服务为何，所以我们也可以借助此工具来探查prot到底是做什么用的。

默认情况下nmap仅会帮你分析TCP通信协议


<br/>
## 一、用法：
**nmap [扫描类型] [扫描参数] [hosts 地址与范围]**


<br/>
## 二、选项与参数：

<br/>
+ **-sT**：扫描TCP数据包已建立的连接 connect()
+ **-sS**：扫描TCP数据包带有SYN卷标的数据
+ **-sP**：以ping的方式进行扫描
+ **-sU**：以UDP的数据包格式进行扫描
+ **-sO**：以IP的协议（protocol）进行主机的扫描
+ **-PT**：使用TCP里头的ping的方式来进行扫描，可以获知目前有几台计算机存在（较常用）
+ **-PI**：使用实际的ping（带有ICMP数据包的）来进行扫描
+ **-p**：这个是port range，例如1024-， 80-1023 等的使用方式。

+ **[host地址与范围]** ：有几种类似的类型
    + *192.168.1.100*：直接写入 HOST  IP ，仅检查一台
    + *192.168.1.0/24*：为 C class 的形态
    + *192.168*.*.*： 为B Class的形态，扫描范围更大
    + *192.168.1.0-50,60-100,103,200*：这种是变形的主机范围


<br/>
## 三、范例：

<br/>
#### 范例一： 扫描 指定的 IP 和 port 是否打开

**成功：**


    # nmap 173.18.117.67 -p 5000

    Starting Nmap 5.51 ( http://nmap.org ) at 2017-01-11 10:55 CST
    mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
    Nmap scan report for 173.18.117.67
    Host is up (0.00078s latency).
    PORT     STATE SERVICE
    5000/tcp open  unknown

    Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds



**失败：**


    # nmap 173.18.117.68 -p 5000

    Starting Nmap 5.51 ( http://nmap.org ) at 2017-01-11 10:56 CST
    mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
    Nmap scan report for 173.18.117.67
    Host is up (0.00089s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds


<br/>
#### 范例二： 扫描指定的IP都打开了那些可以识别的端口


    # nmap 173.18.117.68 

    Starting Nmap 5.51 ( http://nmap.org ) at 2017-01-11 11:00 CST
    mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
    Nmap scan report for 173.18.117.68
    Host is up (0.00042s latency).
    Not shown: 998 closed ports
    PORT   STATE SERVICE
    21/tcp open  ftp
    22/tcp open  ssh

    Nmap done: 1 IP address (1 host up) scanned in 0.12 seconds



<br/>
#### 范例三： 扫描指定的IP都打开了那些可以识别的端口，同时分析TCP和UDP协议

    # nmap -sTU 173.18.117.68 

    Starting Nmap 5.51 ( http://nmap.org ) at 2017-01-11 11:04 CST
    mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
    Nmap scan report for 173.18.117.68
    Host is up (0.00048s latency).
    Not shown: 1000 open|filtered ports, 998 closed ports
    PORT   STATE SERVICE
    21/tcp open  ftp
    22/tcp open  ssh

    Nmap done: 1 IP address (1 host up) scanned in 21.18 seconds



<br/>
#### 范例四：分析C class 网段内的所有主机：


    # nmap 173.18.117.0/24 -p 5000

    Starting Nmap 5.51 ( http://nmap.org ) at 2017-01-11 11:06 CST
    mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
    Nmap scan report for 173.18.117.1
    Host is up (0.00099s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap scan report for 173.18.117.2
    Host is up (0.00044s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap scan report for 173.18.117.3
    Host is up (0.00045s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap scan report for 173.18.117.4
    Host is up (0.00045s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap scan report for 173.18.117.5
    Host is up (0.00043s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown

    Nmap scan report for 173.18.117.6
    Host is up (0.00044s latency).
    PORT     STATE  SERVICE
    5000/tcp closed unknown
    ... ...