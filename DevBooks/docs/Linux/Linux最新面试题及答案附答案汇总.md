# Linux最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Unix和Linux有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#1unix和linux有什么区别)  


Linux和Unix都是功能强大的操作系统，都是应用广泛的服务器操作系统，有很多相似之处，甚至有一部分人错误地认为Unix和Linux操作系统是一样的，然而，事实并非如此，以下是两者的区别。

**1、开源性**

Linux是一款开源操作系统，不需要付费，即可使用；Unix是一款对源码实行知识产权保护的传统商业软件，使用需要付费授权使用。

**2、跨平台性**

Linux操作系统具有良好的跨平台性能，可运行在多种硬件平台上；Unix操作系统跨平台性能较弱，大多需与硬件配套使用。

**3、可视化界面**

Linux除了进行命令行操作，还有窗体管理系统；Unix只是命令行下的系统。

**4、硬件环境**

Linux操作系统对硬件的要求较低，安装方法更易掌握；Unix对硬件要求比较苛刻，按照难度较大。

**5、用户群体**

Linux的用户群体很广泛，个人和企业均可使用；Unix的用户群体比较窄，多是安全性要求高的大型企业使用，如银行、电信部门等，或者Unix硬件厂商使用，如Sun等

相比于Unix操作系统，Linux操作系统更受广大计算机爱好者的喜爱，主要原因是Linux操作系统具有Unix操作系统的全部功能，并且能够在普通PC计算机上实现全部的Unix特性，开源免费的特性，更容易普及使用！


### [2、如何用awk查看第2行倒数第3个字段?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#2如何用awk查看第2行倒数第3个字段)  


```
?  apache awk 'NR==3{print $(NF-2)}' story
this
?  apache cat story
Long ago a lion and a bear saw a kid.
They sprang upon it at the same time.
The lion said to the bear, “I caught this kid first, and so this is mine.”
```

### [3、哪一个bash内置命令能够进行数学运算。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#3哪一个bash内置命令能够进行数学运算。)  


**答案：**

bash shell 的内置命令let 可以进行整型数的数学运算。

```
#! /bin/bash
…
…
let c=a+b
…
…
```


### [4、less （lese：较少的意思）分页查看文件命令（可以快速定位到最后一页）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#4less-lese：较少的意思分页查看文件命令可以快速定位到最后一页)  


```
less -m 显示类似于more命令的百分比。
less -N 显示每行的行号。(大写的N)
两参数一起使用如：less -mN 文件名，如此可分页并显示行号。

空格键：前下一页或page down。
回车：向下一行。
b：后退一页 或 page up。
q：退出。
d：前进半页。
u：后退半页
```


### [5、Linux 性能调优都有哪几种方法？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#5linux-性能调优都有哪几种方法)  


**1、** Disabling daemons (关闭 daemons)。

**2、** Shutting down the GUI (关闭 GUI)。

**3、** Changing kernel parameters (改变内核参数)。

**4、** Kernel parameters (内核参数)。

**5、** Tuning the processor subsystem (处理器子系统调优)。

**6、** Tuning the memory subsystem (内存子系统调优)。

**7、** Tuning the file system (文件系统子系统调优)。

**8、** Tuning the network subsystem（网络子系统调优)。


### [6、如何规划一台 Linux 主机，步骤是怎样？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#6如何规划一台-linux-主机步骤是怎样)  


确定机器是做什么用的，比如是做 WEB 、DB、还是游戏服务器。

> 不同的用途，机器的配置会有所不同。


**1、** 确定好之后，就要定系统需要怎么安装，默认安装哪些系统、分区怎么做。

**2、** 需要优化系统的哪些参数，需要创建哪些用户等等的。


### [7、复制文件](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#7复制文件)  


语法: cp source target

如果target不存在则直接创建，如果存在，默认不会提醒你是否需要覆盖，需要加-i就会询问你是否覆盖,n否y是。

```
?  xktest cp a c
?  xktest cp -i a c
overwrite c? (y/n [n]) y
?  xktest ls
a c
```


### [8、什么是网站数据库注入？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#8什么是网站数据库注入)  


**1、** 由于程序员的水平及经验参差不齐，大部分程序员在编写代码的时候，没有对用户输入数据的合法性进行判断。

**2、** 应用程序存在安全隐患。用户可以提交一段数据库查询代码，根据程序返回的结果，获得某些他想得知的数据，这就是所谓的 SQL 注入。

**3、** SQL注入，是从正常的 WWW 端口访问，而且表面看起来跟一般的 Web 页面访问没什么区别，如果管理员没查看日志的习惯，可能被入侵很长时间都不会发觉。

**如何过滤与预防？**

数据库网页端注入这种，可以考虑使用 nginx_waf 做过滤与预防。


### [9、实时监测进程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#9实时监测进程)  


与ps相比，top可以实时监控进程信息。

![80_3.png][80_3.png]image-20200421114633852

平均负载有3个值:最近1分钟的、最近5分钟的和最近15分钟的平均负载。值越大说明系统 的负载越高。由于进程短期的突发性活动，出现最近1分钟的高负载值也很常见，但如果近15分 钟内的平均负载都很高，就说明系统可能有问题。


### [10、查看文件类型?字符编码？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新面试题及答案附答案汇总.md#10查看文件类型字符编码)  


语法: file destination

```
?  apache file tomcat
tomcat: ASCII text
```

可以看出，file命令可以显示文件的类型text以及字符编码ASCII


### 11、MySQL数据备份工具
### 12、把后台任务调到前台执行使用什么命令?把停下的后台任务在后台执行起来用什么命令?
### 13、使用什么命令查看磁盘使用空间？ 空闲空间呢?
### 14、MySQL的innodb如何定位锁问题，MySQL如何减少主从复制延迟？
### 15、Linux系统安装多个桌面环境有帮助吗？
### 16、查看时间命令：
### 17、file （可查看文件类型）
### 18、制表符自动补全？
### 19、tail（尾巴） 查看文件命令（看最后多少行）
### 20、如何停止一个进程?
### 21、top 命令
### 22、压缩工具有哪些?
### 23、终端是哪个文件夹下的哪个文件？黑洞文件是哪个文件夹下的哪个命令？
### 24、重新命名文件？移动文件？
### 25、怎么查看当前进程？怎么执行退出？怎么查看当前路径？
### 26、哪个命令专门用来查看后台任务?
### 27、如何查看当前主机名？如何修改？如何重启后生效？
### 28、什么是Linux？
### 29、怎么使一个命令在后台运行?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




