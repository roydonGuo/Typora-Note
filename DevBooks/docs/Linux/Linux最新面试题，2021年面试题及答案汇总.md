# Linux最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、ls （ls：list的缩写，查看列表）查看当前目录下的所有文件夹（ls 只列出文件名或目录名）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#1ls-ls：list的缩写查看列表查看当前目录下的所有文件夹ls-只列出文件名或目录名)  


```
ls -a ;显示所有文件夹,隐藏文件也显示出来
ls -R ;连同子目录一起列出来
```


### [2、awk 详解。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#2awk-详解。)  


**答案：**

```
awk '{pattern + action}' {filenames}
#cat /etc/passwd |awk -F ':' '{print 1"\t"7}' //-F 的意思是以':'分隔 root /bin/bash
daemon /bin/sh 搜索/etc/passwd 有 root 关键字的所有行

#awk -F: '/root/' /etc/passwd root:x:0:0:root:/root:/bin/bash
```


### [3、已知 apache 服务的访问日志按天记录在服务器本地目录/app/logs 下，由于磁盘空间紧张现在要求只能保留最近 7 天的访问日志！请问如何解决？请给出解决办法或配置或处理命令](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#3已知-apache-服务的访问日志按天记录在服务器本地目录/app/logs-下由于磁盘空间紧张现在要求只能保留最近-7-天的访问日志请问如何解决请给出解决办法或配置或处理命令)  


创建文件脚本：

#!/bin/bash

for n in `seq 14`

do

date -s "11/0$n/14"

touch access_www_`(date +%F)`.log

done

解决方法：

```
# pwd/application/logs
# ll
-rw-r--r--、1 root root 0 Jan  1 00:00 access_www_2015-01-01.log
-rw-r--r--、1 root root 0 Jan  2 00:00 access_www_2015-01-02.log
-rw-r--r--、1 root root 0 Jan  3 00:00 access_www_2015-01-03.log
-rw-r--r--、1 root root 0 Jan  4 00:00 access_www_2015-01-04.log
-rw-r--r--、1 root root 0 Jan  5 00:00 access_www_2015-01-05.log
-rw-r--r--、1 root root 0 Jan  6 00:00 access_www_2015-01-06.log
-rw-r--r--、1 root root 0 Jan  7 00:00 access_www_2015-01-07.log
-rw-r--r--、1 root root 0 Jan  8 00:00 access_www_2015-01-08.log
-rw-r--r--、1 root root 0 Jan  9 00:00 access_www_2015-01-09.log
-rw-r--r--、1 root root 0 Jan 10 00:00 access_www_2015-01-10.log
-rw-r--r--、1 root root 0 Jan 11 00:00 access_www_2015-01-11.log
-rw-r--r--、1 root root 0 Jan 12 00:00 access_www_2015-01-12.log
-rw-r--r--、1 root root 0 Jan 13 00:00 access_www_2015-01-13.log
-rw-r--r--、1 root root 0 Jan 14 00:00 access_www_2015-01-14.log
# find /application/logs/ -type f -mtime +7 -name "*.log"|xargs rm –f  
##也可以使用-exec rm -f {} ;进行删除
# ll
-rw-r--r--、1 root root 0 Jan  7 00:00 access_www_2015-01-07.log
-rw-r--r--、1 root root 0 Jan  8 00:00 access_www_2015-01-08.log
-rw-r--r--、1 root root 0 Jan  9 00:00 access_www_2015-01-09.log
-rw-r--r--、1 root root 0 Jan 10 00:00 access_www_2015-01-10.log
-rw-r--r--、1 root root 0 Jan 11 00:00 access_www_2015-01-11.log
-rw-r--r--、1 root root 0 Jan 12 00:00 access_www_2015-01-12.log
-rw-r--r--、1 root root 0 Jan 13 00:00 access_www_2015-01-13.log
-rw-r--r--、1 root root 0 Jan 14 00:00 access_www_2015-01-14.log
```


### [4、如果一个linux新手想要知道当前系统支持的所有命令的列表，他需要怎么做？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#4如果一个linux新手想要知道当前系统支持的所有命令的列表他需要怎么做)  


**答案：**

使用命令compgen --c，可以打印出所有支持的命令列表。

```
[root@localhost ~]$ compgen -c
l.
ll
ls
which
if
then
else
elif
fi
case
esac
for
select
while
until
do
done
…
```


### [5、du 和 df 的定义，以及区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#5du-和-df-的定义以及区别)  


**答案：**

du 显示目录或文件的大小

**1、** df 显示每个<文件>所在的文件系统的信息，默认是显示所有文件系统。

**2、** （文件系统分配其中的一些磁盘块用来记录它自身的一些数据，如 i 节点，磁盘分布图，间接块，超级块等。这些数据对大多数用户级的程序来说是不可见的，通常称为 Meta Data。） du 命令是用户级的程序，它不考虑 Meta Data，而 df 命令则查看文件系统的磁盘分配图并考虑 Meta Data。

**3、** df 命令获得真正的文件系统数据，而 du 命令只查看文件系统的部分情况。


### [6、什么叫网站灰度发布？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#6什么叫网站灰度发布)  


灰度发布是指在黑与白之间，能够平滑过渡的一种发布方式

AB test就是一种灰度发布方式，让一部用户继续用A，一部分用户开始用B

如果用户对B没有什么反对意见，那么逐步扩大范围，把所有用户都迁移到B上面 来

灰度发布可以保证整体系统的稳定，在初始灰度的时候就可以发现、调整问题，以保证其影响度


### [7、RAID 是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#7raid-是什么)  


RAID 全称为独立磁盘冗余阵列(Redundant Array of Independent Disks)，基本思想就是把多个相对便宜的硬盘组合起来，成为一个硬盘阵列组，使性能达到甚至超过一个价格昂贵、 容量巨大的硬盘。RAID 通常被用在服务器电脑上，使用完全相同的硬盘组成一个逻辑扇区，因此操作系统只会把它当做一个硬盘。

RAID 分为不同的等级，各个不同的等级均在数据可靠性及读写性能上做了不同的权衡。在实际应用中，可以依据自己的实际需求选择不同的 RAID 方案。

当然，因为很多公司都使用云服务，大家很难接触到 RAID 这个概念，更多的可能是普通云盘、SSD 云盘酱紫的概念。


### [8、clear 清屏命令。（强迫症患者使用）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#8clear-清屏命令。强迫症患者使用)  


```
kill 命令用来中止一个进程。（要配合ps命令使用，配合pid关闭进程）
（ps类似于打开任务管理器，kill类似于关闭进程）
kill -5 进程的PID ;推荐,和平关闭进程
kill -9 PID ;不推荐,强制杀死进程
```


### [9、用tcpdump嗅探80端口的访问看看谁最高](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#9用tcpdump嗅探80端口的访问看看谁最高)  


```
tcpdump -i eth0 -tnn dst port 80 -c 1000 | awk -F"." '{print $1"."$2"."$3"."$4}'| sort | uniq -c | sort -nr |head -20
```


### [10、移动文件用哪个命令？改名用哪个命令？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题，2021年面试题及答案汇总.md#10移动文件用哪个命令改名用哪个命令)  


**答案：**

mv mv


### 11、Linux内核主要负责哪些功能
### 12、目录创建用什么命令？创建文件用什么命令？复制文件用什么命令？
### 13、储存用户的文件是?包括哪些信息？
### 14、数据排序?对数字进行排序？对月份排序？
### 15、查看组信息？如何创建组？删除组？
### 16、搜索文件用什么命令? 格式是怎么样的?
### 17、GNU项目的重要性是什么？
### 18、什么是交换空间？
### 19、请写出下面 linux SecureCRT 命令行快捷键命令的功能？
### 20、查看http的并发请求数与其TCP连接状态
### 21、ifconfig命令
### 22、bash shell 中的hash 命令有什么作用？
### 23、重启linux
### 24、列出已经安装的包？安装软件？更新软件？卸载?
### 25、绝对文件路径?相对文件路径？快捷方式？
### 26、什么是CLI？
### 27、什么是root帐户
### 28、什么叫CDN？
### 29、rm（remove：移除的意思）删除文件，或文件夹





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




