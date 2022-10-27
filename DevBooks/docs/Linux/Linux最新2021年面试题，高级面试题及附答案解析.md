# Linux最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、终止进程用什么命令? 带什么参数?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#1终止进程用什么命令-带什么参数)  


**答案：**

kill [-s <信息名称或编号>][程序] 或 kill [-l <信息编号>]

kill-9 pid


### [2、8.迷路，我的当前位置在哪？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#28迷路我的当前位置在哪)  


pwd 显示当前目录

```
[root@iz2ze76ybn73dvwmdij06zz local]# pwd
/usr/local
```


### [3、利用 ps 怎么显示所有的进程? 怎么利用 ps 查看指定进程的信息？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#3利用-ps-怎么显示所有的进程-怎么利用-ps-查看指定进程的信息)  


**答案：**

```
ps -ef (system v 输出) 

ps -aux bsd 格式输出

ps -ef | grep pid
```


### [4、复制文件用哪个命令？如果需要连同文件夹一块复制呢？如果需要有提示功能呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#4复制文件用哪个命令如果需要连同文件夹一块复制呢如果需要有提示功能呢)  


**答案：**

cp cp -r ?？？？？


### [5、统计ip访问情况，要求分析nginx访问日志，找出访问页面数量在前十位的ip](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#5统计ip访问情况要求分析nginx访问日志找出访问页面数量在前十位的ip)  


cat access.log | awk '{print $1}' | uniq -c | sort -rn | head -10


### [6、vim编辑器几种操作模式？基本操作?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#6vim编辑器几种操作模式基本操作)  


操作模式:

**1、** 普通模式

**2、** 插入模式

基础操作:

**1、** h:左移一个字符。

**2、** j:下移一行(文本中的下一行)。

**3、** k:上移一行(文本中的上一行)。

**4、** l:右移一个字符。

vim提供了一些能够提高移动速度的命令:

**1、** PageDown(或Ctrl+F):下翻一屏

**2、** PageUp(或Ctrl+B):上翻一屏。

**3、** G:移到缓冲区的最后一行。

**4、** num G:移动到缓冲区中的第num行。

**5、** gg:移到缓冲区的第一行。

退出vim:

**1、** q:如果未修改缓冲区数据，退出。

**2、** q!:取消所有对缓冲区数据的修改并退出。

**3、** w filename:将文件保存到另一个文件中。

**4、** wq:将缓冲区数据保存到文件中并退出。


### [7、Linux 有哪些系统日志文件？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#7linux-有哪些系统日志文件)  


比较重要的是 `/var/log/messages` 日志文件。

该日志文件是许多进程日志文件的汇总，从该文件可以看出任何入侵企图或成功的入侵。

> 另外，如果胖友的系统里有 ELK 日志集中收集，它也会被收集进去。



### [8、查看整个文件？按照有文本显示行号？无文本显示行号？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#8查看整个文件按照有文本显示行号无文本显示行号)  


语法 : cat destination

-n 显示行号，-b 有文本的显示行号。 （默认是不显示行号的)

```
?  apache cat -n tomcat
     1    text
     2    text
     3
     4    start
     5    stop
     6    restart
     7    end
?  apache cat -b tomcat
     1    text
     2    text
```

3 ? ?start

4 ? ?stop

5 ? ?restart

6 ? ?end



### [9、Linux 开机启动过程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#9linux-开机启动过程)  


了解即可。

**1、** 主机加电自检，加载 BIOS 硬件信息。

**2、** 读取 MBR 的引导文件(GRUB、LILO)。

**3、** 引导 Linux 内核。

**4、** 运行第一个进程 init (进程号永远为 1 )。

**5、** 进入相应的运行级别。

**6、** 运行终端，输入用户名和密码。


### [10、你的系统目前有许多正在运行的任务，在不重启机器的条件下，有什么方法可以把所有正在运行的进程移除呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Linux/Linux最新2021年面试题，高级面试题及附答案解析.md#10你的系统目前有许多正在运行的任务在不重启机器的条件下有什么方法可以把所有正在运行的进程移除呢)  


**答案：**

使用linux命令 ’disown -r ’可以将所有正在运行的进程移除。


### 11、Grep 命令有什么用？ 如何忽略大小写？ 如何查找不含该串的行?
### 12、什么是BASH？
### 13、ping （用于检测与目标的连通性）语法：ping ip地址
### 14、通过什么命令查找执行命令?
### 15、一台 Linux 系统初始化环境后需要做一些什么安全工作？
### 16、简述DNS进行域名解析的过程？
### 17、默认进程信息显示?
### 18、Linux的基本组件是什么？
### 19、pwd （print working directory：显示当前工作目录的绝对路径）
### 20、cat （concatenate：显示或把多个文本文件连接起来）查看文件命令（可以快捷查看当前文件的内容）（不能快速定位到最后一页）
### 21、vim （VI IMproved：改进版视觉）改进版文本编辑器 （不管是文件查看还是文件编辑 按 Shift + 上或者下可以上下移动查看视角）
### 22、mv（move单词缩写，移动功能，该文件名称功能）
### 23、关机linux
### 24、哪个文件包含了主机名和ip的映射关系?
### 25、发现一个病毒文件你删了他又自动创建怎么解决
### 26、怎样查看一个linux命令的概要与用法？假设你在/bin目录中偶然看到一个你从没见过的的命令，怎样才能知道它的作用和用法呢？
### 27、使用哪一个命令可以查看自己文件系统的磁盘空间配额呢？
### 28、登陆后你在的位置？
### 29、查看部分文件





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




