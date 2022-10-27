# NoSQL

​		NoSQL，泛指非关系型的数据库。随着互联网web2.0网站的兴起，传统的关系数据库在处理web2.0网站，特别是超大规模和高并发的SNS类型的web2.0纯动态网站已经显得力不从心，出现了很多难以克服的问题，而非关系型的数据库则由于其本身的特点得到了非常迅速的发展。NoSQL数据库的产生就是为了解决大规模数据集合多重数据种类带来的挑战，特别是大数据应用难题。

​		**Ø易扩展**。NoSQL数据库种类繁多，但是一个共同的特点都是去掉关系数据库的关系型特性。数据之间无关系，这样就非常容易扩展。无形之间也在架构的层面上带来了可扩展的能力。

​		**Ø 大数据量，高性能**。NoSQL数据库都具有非常高的读写性能，尤其在大数据量下，同样表现优秀。这得益于它的无关系性，数据库的结构简单。一般MySQL使用Query Cache。NoSQL的Cache是记录级的，是一种细粒度的Cache，所以NoSQL在这个层面上来说性能就要高很多。

​		**Ø灵活的数据模型**。NoSQL无须事先为要存储的数据建立字段，随时可以存储自定义的数据格式。而在关系数据库里，增删字段是一件非常麻烦的事情。如果是非常大数据量的表，增加字段简直就是——个噩梦。这点在大数据量的Web 2.0时代尤其明显。 

​		**Ø 高可用**。NoSQL在不太影响性能的情况，就可以方便地实现高可用的架构。比如Cassandra、HBase模型，通过复制模型也能实现高可用。

NoSQL数据库分类：

![NoSQL数据库分类](C:\Users\31330\AppData\Roaming\Typora\typora-user-images\image-20220605120916746.png)

# 1. Redis

<img src="C:\Users\31330\Pictures\Typora\redis_v.jpg" alt="redis" style="zoom:50%;" />

## 1.1. Redis的安装

​		大多数企业都是基于Linux服务器来部署项目，而且Redis官方也没有提供Windows版本的安装包。本教程会在Linux下部署redis。

​		Linux版本为CentOS 7。

​		Redis的官方网站地址：[https://redis.io/](https://redis.io/)

### 1.1.1. Windows安装

​		首先下载Redis压缩包，直接解压到指定目录即可，redis.conf配置文件

### 1.1.2. Linux安装

​		首先去Redis官网 [download](https://redis.io/download/)下载linux压缩包，官网只提供**.tar.gz**格式在linux环境下部署的压缩包。

Redis是基于C语言编写的，因此首先需要安装Redis所需要的gcc依赖：

```sh
yum install -y gcc tcl
```

下载好的Redis安装包需要上传到虚拟机的指定目录，如此处我们上传的目录为根目录下的==/JavaTools/Redis-5.0.14==,可以使用==Xftp==上传。

>下载好的redis-5.0.14.tar.gz压缩包上传到Linux后解压缩
>
>解压命令```tar -xzf redis-5.0.14.tar.gz```
>
>得到redis-5.0.14

![JavaTools]()

进入redis目录

```sh
cd redis-5.0.14
```

运行编译命令：

```sh
make && make install
```

> 注意：
>
> >可能会出现错误：jemalloc/jemalloc.h：没有那个文件或目录，执行如下命令即可： 
> >
> >```sh
> >make MALLOC=libc
> >```

make install可将redis的相关运行文件复制一份放到==/usr/local/bin/==下，这样就可以在任意目录下执行redis的命令了

![ll]()

- redis-cli：是redis提供的命令行客户端
- redis-server：是redis的服务端启动脚本
- redis-sentinel：是redis的哨兵启动脚本

***

#### 启动Redis

这样就可以启动Redis服务了，启动方式例如：

- 默认启动
- 指定配置启动
- 开机自启

***

1.默认启动：

在任意目录下输入redis-server命令即可启动Redis

```sh
redis-server
```

启动成功

![启动了redis]()

这种属于`前台启动`，会阻塞整个会话窗口，窗口关闭或者按下`CTRL + C`则Redis停止。不推荐使用。

***

2.指定配置文件启动：

需要将Redis以**后台**方式启动，需要修改redis.conf配置文件，就在解压的目录```/JavaTools/redis-5.0.14```下：

![conf]()

进入redis-5.0.14编辑redis.conf

```sh
cd redis-5.0.14
```

先将配置文件备份一份：

```sh
cp redis.conf redis.conf.bck
```

然后修改redis.conf文件中的一些配置：

```sh
vi redis.conf
```

```sh
# 允许访问的地址，默认是127.0.0.1，会导致只能在本地访问。修改为0.0.0.0则可以在任意IP访问，生产环境不要设置为0.0.0.0
bind 0.0.0.0
# 守护进程，修改为yes后即可后台运行
daemonize yes
# 密码，设置后访问Redis必须输入密码
requirepass qwer1234
```

Redis的其它常见配置：

```properties
# 监听的端口
port 6379
# 工作目录，默认是当前目录，也就是运行redis-server时的命令，日志、持久化等文件会保存在这个目录
dir .
# 数据库数量，设置为1，代表只使用1个库，默认有16个库，编号0~15
databases 1
# 设置redis能够使用的最大内存
maxmemory 512mb
# 日志文件，默认为空，不记录日志，可以指定日志文件名
logfile "redis.log"
```

用配置文件启动Redis：

```sh
redis-server redis.conf
```

停止服务：

```sh
# 利用redis-cli来执行 shutdown 命令，即可停止 Redis 服务，
# 因为之前配置了密码，因此需要通过 -u 来指定密码
redis-cli -u qwer1234 shutdown
```

***

3.开机自启：

我们也可以通过配置来实现开机自启。

首先，新建一个系统服务文件：

```sh
vi /etc/systemd/system/redis.service
```

内容如下：

```conf
[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/bin/redis-server /usr/local/src/redis-6.2.6/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

然后重载系统服务：

```sh
systemctl daemon-reload
```

现在，我们可以用下面这组命令来操作redis了：

```sh
# 启动
systemctl start redis
# 停止
systemctl stop redis
# 重启
systemctl restart redis
# 查看状态
systemctl status redis
```

执行下面的命令，可以让redis开机自启：

```sh
systemctl enable redis
```

***



## 1.2.Redis客户端cli



### 1.2.1.Redis命令行客户端

Redis安装完成后就自带了命令行客户端：redis-cli，使用方式如下：

```sh
redis-cli [options] [commonds]
```

其中常见的options有：

- `-h 127.0.0.1`：指定要连接的redis节点的IP地址，默认是127.0.0.1
- `-p 6379`：指定要连接的redis节点的端口，默认是6379
- `-a qwer1234`：指定redis的访问密码 

其中的commonds就是Redis的操作命令，例如：

- `ping`：与redis服务端做心跳测试，服务端正常会返回`pong`

不指定commond时，会进入`redis-cli`的交互控制台：

![image-20211211110439353](C:\Users\31330\Pictures\1.png)

可以使用命令连接cli客户端

```sh
redis-cli -h 本机地址 -p 6379
```

配置文件设置有密码时，cli启动后需要输入密码

```sh
 AUTH qwer1234 #redis密码
```

启动失败，尝试开放6379端口

```sh
/sbin/iptables -I INPUT -p tcp --dport 6379 -j ACCEPT
```

***

**其他硬知识**

- 查看redis进程是否存在
  `ps -ef |grep redis`
- 检测6379端口是否在监听
  `netstat -lntp | grep 6379`
- 停止redis，使用ctrl+c快捷键或者使用客户端 ```redis-cli shutdown```



