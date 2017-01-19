# 一、wget 文字接口下载器简介
<br/>

wget是一个从网络上自动下载文件的自由工具，支持通过HTTP、HTTPS、FTP三个最常见的TCP/IP协议下载，并可以使用HTTP代理。

 <br/>
 <br/>

# 二、语法
<br/>


    wget [option] [网址]


<br/>
<br/>

# 三、 选项与参数
<br/>

    若想要连接的网站有提供账号与密码保护是，可以利用这两个参数来输入：
    --http-user=username
    --http-password=password

    --quit：不要显示wget在捕获数据时候的显示信息


<br/>
<br/>

# 四、 范例
<br/>

## 1、 下载sipp软件


    $ wget http://218.206.176.135:9099/apk/webrtc/sipp-3.5.1.tar.gz
    --2017-01-19 09:42:50--  http://218.206.176.135:9099/apk/webrtc/sipp-3.5.1.tar.gz
    Connecting to 218.206.176.135:9099... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 608235 (594K) [application/octet-stream]
    Saving to: “sipp-3.5.1.tar.gz”

    100%[===================================================>] 608,235     --.-K/s   in 0.1s    

    2017-01-19 09:42:50 (3.96 MB/s) - “sipp-3.5.1.tar.gz” saved [608235/608235]


<br/>
<br/>

# 五、 配置
<br/>
通过修改/etc/wgetrc 来设置你的代理服务器：


    # You can set the default proxies for Wget to use for http, https, and ftp.
    # They will override the value in the environment.
    #https_proxy = http://proxy.yoyodyne.com:18023/
    #http_proxy = http://proxy.yoyodyne.com:18023/
    #ftp_proxy = http://proxy.yoyodyne.com:18023/






















