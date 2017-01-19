# 一、 fdisk磁盘分区管理命令简介
<br/>

如果我们想要在系统里面新增一块硬盘时，应该做哪些改动呢？
1. 对磁盘进行分区，以新建可用的分区
2. 对该分区进行格式化(format)，以创建系统可用的文件系统。
3. 若想仔细一点，则可对刚才新建好的文件系统进行检查
4. 在Linux系统上，需要创建挂载点（也就是目录），并将它挂载上来。

在上述过程当中，还有很多需要考虑的，例如磁盘分区需要定多大、是否需要加入journal的功能、inode与block的数量应该如何规划等的问题。但是这些问题的决定都需要和你的主机用途来加以考虑的。

由于每个人的环境都不一样，因此每台主机的磁盘数量也不相同。所以你可以先使用 `df` 这个命令找出可用磁盘文件名，然后再用fdisk来查阅。

<br/>
<br/>

# 二、语法
<br/>


    fdisk [-l] 设备名称


<br/>
<br/>

# 三、 选项与参数
<br/>


    -l  : 输出后面接的设备所有的分区内容。若仅有fdisk -l 时，则系统将会把整个系统内能够找到的设备的分区均列出来。
    -p  : 显示分区表
    -n  : 新建一个分区
    -d  : 删除一个分区
    -w  : 将刚才的操作写入分区表，并离开
    -q  : 不存储，直接离开
    -t  : 更改分区的系统类型


<br/>
<br/>

# 四、范例
<br/>

## 1. 查看设备的分区情况


    # fdisk -l
    Disk /dev/vda: 214.7 GB, 214748364800 bytes
    255 heads, 63 sectors/track, 26108 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00078f9c

       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *           1       26109   209713152   83  Linux

    Disk /dev/vdb: 834.3 GB, 834297397248 bytes
    16 heads, 63 sectors/track, 1616554 cylinders
    Units = cylinders of 1008 * 512 = 516096 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00000000


<br/>
## 2. 对未分区的磁盘 /dev/sdb 进行分区并格式化 
<br/>

#### 1、格式化磁盘：
    # fdisk /dev/sdb
    p 列出分区表
    n 添加一个分区
    p 创建主分区
    1 选择盘符1
    回车 默认其实扇道
    回车 默认结束扇道

    t 改变分区类型
    8e 选择 linux lvm 分区类型

    w 保存更改退出


#### 2、对分区进行格式化，以及加载：


    # mkfs.ext3 /dev/sdb1


3、将分区挂在到webrtc目录下ls

    cd /home/
    # mv webrtc/ webrtc_bak
    # mkdir webrtc
    # mount /dev/sdb1 /home/webrtc









