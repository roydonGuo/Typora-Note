# Nginx最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、漏桶流算法和令牌桶算法知道，漏桶算法#](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#1漏桶流算法和令牌桶算法知道漏桶算法#)  


漏桶算法是网络世界中流量整形或速率限制时经常使用的一种算法，它的主要目的是控制数据注入到网络的速率，平滑网络上的突发流量。漏桶算法提供了一种机制，通过它，突发流量可以被整形以便为网络提供一个稳定的流量。也就是我们刚才所讲的情况。漏桶算法提供的机制实际上就是刚才的案例：**突发流量会进入到一个漏桶，漏桶会按照我们定义的速率依次处理请求，如果水流过大也就是突发流量过大就会直接溢出，则多余的请求会被拒绝。所以漏桶算法能控制数据的传输速率。**

![56_1.png][56_1.png]


### [2、限制并发连接数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#2限制并发连接数)  


Nginx中的ngx_http_limit_conn_module模块提供了限制并发连接数的功能，可以使用limit_conn_zone指令以及limit_conn执行进行配置。接下来我们可以通过一个简单的例子来看下：

```
 http {

     limit_conn_zone $binary_remote_addr zone=myip:10m;
     limit_conn_zone $server_name zone=myServerName:10m;
 }

 server {

     location / {

         limit_conn myip 10;
         limit_conn myServerName 100;
         rewrite / http://www.lijie.net permanent;
     }
 }
```

上面配置了单个IP同时并发连接数最多只能10个连接，并且设置了整个虚拟服务器同时最大并发数最多只能100个链接。当然，只有当请求的header被服务器处理后，虚拟服务器的连接数才会计数。刚才有提到过Nginx是基于漏桶算法原理实现的，实际上限流一般都是基于漏桶算法和令牌桶算法实现的。接下来我们来看看两个算法的介绍：


### [3、fastcgi 与 cgi 的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#3fastcgi-与-cgi-的区别)  


**cgi**

**1、** web 服务器会根据请求的内容，然后会 fork 一个新进程来运行外部 c 程序（或 perl 脚本…）， 这个进程会把处理完的数据返回给 web 服务器，最后 web 服务器把内容发送给用户，刚才 fork 的进程也随之退出。

**2、** 如果下次用户还请求改动态脚本，那么 web 服务器又再次 fork 一个新进程，周而复始的进行。

**fastcgi**

web 服务器收到一个请求时，他不会重新 fork 一个进程（因为这个进程在 web 服务器启动时就开启了，而且不会退出），web 服务器直接把内容传递给这个进程（进程间通信，但 fastcgi 使用了别的方式，tcp 方式通信），这个进程收到请求后进行处理，把结果返回给 web 服务器，最后自己接着等待下一个请求的到来，而不是退出。

综上，差别在于是否重复 fork 进程，处理请求。


### [4、请解释一下什么是 Nginx?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#4请解释一下什么是-nginx)  


Nginx 是一个 web 服务器和反向代理服务器，用于 HTTP、HTTPS、SMTP、POP3

和 IMAP 协议。


### [5、Nginx目录结构有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#5nginx目录结构有哪些)  


```
[root@localhost ~]# tree /usr/local/nginx
/usr/local/nginx
├── client_body_temp
├── conf                             # Nginx所有配置文件的目录
│   ├── fastcgi.conf                 # fastcgi相关参数的配置文件
│   ├── fastcgi.conf.default         # fastcgi.conf的原始备份文件
│   ├── fastcgi_params               # fastcgi的参数文件
│   ├── fastcgi_params.default       
│   ├── koi-utf
│   ├── koi-win
│   ├── mime.types                   # 媒体类型
│   ├── mime.types.default
│   ├── nginx.conf                   # Nginx主配置文件
│   ├── nginx.conf.default
│   ├── scgi_params                  # scgi相关参数文件
│   ├── scgi_params.default  
│   ├── uwsgi_params                 # uwsgi相关参数文件
│   ├── uwsgi_params.default
│   └── win-utf
├── fastcgi_temp                     # fastcgi临时数据目录
├── html                             # Nginx默认站点目录
│   ├── 50x.html                     # 错误页面优雅替代显示文件，例如当出现502错误时会调用此页面
│   └── index.html                   # 默认的首页文件
├── logs                             # Nginx日志目录
│   ├── access.log                   # 访问日志文件
│   ├── error.log                    # 错误日志文件
│   └── nginx.pid                    # pid文件，Nginx进程启动后，会把所有进程的ID号写到此文件
├── proxy_temp                       # 临时目录
├── sbin                             # Nginx命令目录
│   └── nginx                        # Nginx的启动命令
├── scgi_temp                        # 临时目录
└── uwsgi_temp                       # 临时目录
```


### [6、请解释你如何通过不同于 80 的端口开启 Nginx?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#6请解释你如何通过不同于-80-的端口开启-nginx)  


为了通过一个不同的端口开启 Nginx，你必须进入/etc/Nginx/sites

enabled/，如果这是默认文件，那么你必须打开名为“default”的文件。编辑

文件，并放置在你想要的端口：

Like server { listen 81; }


### [7、解释如何在 Nginx 中获得当前的时间?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#7解释如何在-nginx-中获得当前的时间)  


要获得 Nginx 的当前时间，必须使用 SSI 模块、$$date_gmt 和$$date_local 的变

量。

Proxy_set_header THE-TIME $date_gmt;


### [8、使用“反向代理服务器的优点是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#8使用“反向代理服务器的优点是什么)  


反向代理服务器可以隐藏源服务器的存在和特征。它充当互联网云和web服务器之间的中间层。这对于安全方面来说是很好的，特别是当您使用web托管服务时。


### [9、请解释 Nginx 如何处理 HTTP 请求？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#9请解释-nginx-如何处理-http-请求)  


**1、** 首先，Nginx 在启动时，会解析配置文件，得到需要监听的端口与 IP 地址，然后在 Nginx 的 Master 进程里面先初始化好这个监控的Socket(创建 S ocket，设置 addr、reuse 等选项，绑定到指定的 ip 地址端口，再 listen 监听)。

**2、** 然后，再 fork(一个现有进程可以调用 fork 函数创建一个新进程。由 fork 创建的新进程被称为子进程 )出多个子进程出来。

**3、** 之后，子进程会竞争 accept 新的连接。此时，客户端就可以向 nginx 发起连接了。当客户端与nginx进行三次握手，与 nginx 建立好一个连接后。此时，某一个子进程会 accept 成功，得到这个建立好的连接的 Socket ，然后创建 nginx 对连接的封装，即 ngx_connection_t 结构体。

**4、** 接着，设置读写事件处理函数，并添加读写事件来与客户端进行数据的交换。


### [10、fair(第三方插件)](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题附答案解析，大汇总.md#10fair第三方插件)  


必须安装upstream_fair模块。

对比 weight、ip_hash更加智能的负载均衡算法，fair算法可以根据页面大小和加载时间长短智能地进行负载均衡，响应时间短的优先分配。

```
upstream backserver {
 server server1; 
 server server2; 
 fair; 
}
```

哪个服务器的响应速度快，就将请求分配到那个服务器上。


### 11、如何用Nginx解决前端跨域问题？
### 12、Nginx虚拟主机怎么配置?
### 13、使用“反向代理服务器”的优点是什么?
### 14、ip_hash( IP绑定)
### 15、请解释 ngx_http_upstream_module 的作用是什么?
### 16、请列举Nginx的一些特性？
### 17、基于虚拟主机配置域名
### 18、Nginx配置文件nginx.conf有哪些属性模块?
### 19、Nginx怎么做的动静分离？
### 20、Nginx 有哪些优点？
### 21、解释如何在 Nginx 服务器上添加模块?
### 22、什么是C10K问题?
### 23、Nginx 常用配置？
### 24、location的作用是什么？
### 25、解释如何在Nginx服务器上添加模块?
### 26、请列举 Nginx 的一些特性。
### 27、为什么不使用多线程？
### 28、Nginx 如何实现后端服务的健康检查？
### 29、Rewrite全局变量是什么？
### 30、location的语法能说出来吗？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




