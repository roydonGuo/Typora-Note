# Linux最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、cp（copy单词缩写，复制功能）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#1cpcopy单词缩写复制功能)  


```
cp /opt/java/java.log /opt/logs/ ;把java.log 复制到/opt/logs/下
cp /opt/java/java.log /opt/logs/aaa.log ;把java.log 复制到/opt/logs/下并且改名为aaa.log
cp -r /opt/java /opt/logs ;把文件夹及内容复制到logs文件中
```


### [2、创建文件？创建目录？批量创建?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#2创建文件创建目录批量创建)  


创建文件:touch 文件名

批量创建文件: touch 文件名 文件名 …

```
?  test touch a
?  test ls
a
?  test touch b c
?  test ls
a b c
```

创建目录：mkdir 目录名

批量创建目录: mkdir 目录名 目录名 …

```
?  test mkdir aa
?  test mkdir bb cc
?  test ls
a  aa b  bb c  cc
?  test ls -F
a   aa/ b   bb/ c   cc/
```


### [3、通过什么命令指定命令提示符?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#3通过什么命令指定命令提示符)  


**答案：**

**1、** \u：显示当前用户账号

**2、** \h：显示当前主机名

**3、** \W：只显示当前路径最后一个目录

**4、** \w：显示当前绝对路径（当前用户目录会以~代替）

**5、** $PWD：显示当前全路径

**6、** $$：显示命令行’$$'或者’#'符号

**7、** #：下达的第几个命令

**8、** \d：代表日期，格式为week day month date，例如："MonAug1"

**9、** \t：显示时间为24小时格式，如：HH：MM：SS

**10、** \T：显示时间为12小时格式

**11、** \A：显示时间为24小时格式：HH：MM

**12、** \v：BASH的版本信息 如export PS1=’[\u@\h\w#]$‘


### [4、简述raid0 raid1 raid5 三种工作模式的工作原理及特点](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#4简述raid0-raid1-raid5-三种工作模式的工作原理及特点)  


RAID，可以把硬盘整合成一个大磁盘，还可以在大磁盘上再分区，放数据

还有一个大功能，多块盘放在一起可以有冗余（备份）

RAID整合方式有很多，常用的：0 1 5 10

RAID 0，可以是一块盘和N个盘组合

其优点读写快，是RAID中最好的

缺点：没有冗余，一块坏了数据就全没有了

RAID 1，只能2块盘，盘的大小可以不一样，以小的为准

10G+10G只有10G，另一个做备份。它有100%的冗余，缺点：浪费资源，成本高

RAID 5 ，3块盘，容量计算10*（n-1）,损失一块盘

特点，读写性能一般，读还好一点，写不好

冗余从好到坏：RAID1 RAID10 RAID 5 RAID0

性能从好到坏：RAID0 RAID10 RAID5 RAID1

成本从低到高：RAID0 RAID5 RAID1 RAID10

单台服务器：很重要盘不多，系统盘，RAID1

数据库服务器：主库：RAID10 从库 RAID5RAID0（为了维护成本，RAID10）

WEB服务器，如果没有太多的数据的话，RAID5,RAID0（单盘）

有多台，监控、应用服务器，RAID0 RAID5

我们会根据数据的存储和访问的需求，去匹配对应的RAID级别


### [5、Linux 中进程有哪几种状态？在 ps 显示出来的信息中，分别用什么符号表示的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#5linux-中进程有哪几种状态在-ps-显示出来的信息中分别用什么符号表示的)  


**答案：**

**1、** 不可中断状态：进程处于睡眠状态，但是此刻进程是不可中断的。不可中断， 指进程不响应异步信号。

**2、** 暂停状态/跟踪状态：向进程发送一个 SIGSTOP 信号，它就会因响应该信号 而进入 TASK_STOPPED 状态;当进程正在被跟踪时，它处于 TASK_TRACED 这个特殊的状态。

正被跟踪”指的是进程暂停下来，等待跟踪它的进程对它进行操作。

**3、** 就绪状态：在 run_queue 队列里的状态

**4、** 运行状态：在 run_queue 队列里的状态

**5、** 可中断睡眠状态：处于这个状态的进程因为等待某某事件的发生（比如等待 socket 连接、等待信号量），而被挂起

**6、** zombie 状态（僵尸）：父亲没有通过 wait 系列的系统调用会顺便将子进程的尸体（task_struct）也释放掉

**7、** 退出状态

> D 不可中断 Uninterruptible（usually IO）

R 正在运行，或在队列中的进程

S 处于休眠状态

T 停止或被追踪

Z 僵尸进程

W 进入内存交换（从内核 2.6 开始无效）

X 死掉的进程



### [6、Shell 脚本是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#6shell-脚本是什么)  


一个 Shell 脚本是一个文本文件，包含一个或多个命令。作为系统管理员，我们经常需要使用多个命令来完成一项任务，我们可以添加这些所有命令在一个文本文件(Shell 脚本)来完成这些日常工作任务。


### [7、什么是 Linux 内核？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#7什么是-linux-内核)  


Linux 系统的核心是内核。内核控制着计算机系统上的所有硬件和软件，在必要时分配硬件，并根据需要执行软件。

**1、** 系统内存管理

**2、** 应用程序管理

**3、** 硬件设备管理

**4、** 文件系统管理


### [8、什么是LILO？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#8什么是lilo)  


LILO是Linux的引导加载程序。它主要用于将Linux操作系统加载到主内存中，以便它可以开始运行。


### [9、实时抓取并显示当前系统中tcp 80端口的网络数据信息，请写出完整操作命令](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#9实时抓取并显示当前系统中tcp-80端口的网络数据信息请写出完整操作命令)  


tcpdump -nn tcp port 80


### [10、什么是GUI？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题大汇总，附答案.md#10什么是gui)  


图形用户界面（Graphical User Interface，简称 GUI，又称图形用户接口）是指采用图形方式显示的计算机操作用户界面。

图形用户界面是一种人与计算机通信的界面显示格式，允许用户使用鼠标等输入设备操纵屏幕上的图标或菜单选项，以选择命令、调用文件、启动程序或执行其它一些日常任务。与通过键盘输入文本或字符命令来完成例行任务的字符界面相比，图形用户界面有许多优点。


### 11、什么是 inode ？
### 12、开源的优势是什么？
### 13、Linux系统缺省的运行级别？
### 14、tar （解压 压缩 命令）
### 15、什么是Linux
### 16、怎么清屏？怎么退出当前命令？怎么执行睡眠？怎么查看当前用户 id？查看指定帮助用什么命令？
### 17、查看某端口是否被占用?
### 18、查看已有别名?建立属于自己的别名?
### 19、查看设备还有多少磁盘空间?
### 20、现在给你三百台服务器，你怎么对他们进行管理？
### 21、Squid、Varinsh和Nginx有什么区别，工作中你怎么选择？
### 22、ll （ll：list的缩写，查看列表详情）查看当前目录下的所有详细信息和文件夹（ll 结果是详细,有时间,是否可读写等信息）
### 23、验证网络可链接命令是什么？什么原理？
### 24、查找匹配数据？反向搜？
### 25、yum install -y lrzsz 命令（实现win到Linux文件互相简单上传文件）
### 26、使用tcpdump监听主机为192.168.1.1，tcp端口为80的数据，同时将输出结果保存输出到tcpdump.log
### 27、Linux 的体系结构
### 28、简述raid0 raid1 raid5 三种工作模式的工作原理及特点
### 29、服务器开不了机怎么解决一步步的排查





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




