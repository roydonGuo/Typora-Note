# Nginx最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Nginx 是如何实现高并发的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#1nginx-是如何实现高并发的)  


如果一个 server 采用一个进程(或者线程)负责一个request的方式，那么进程数就是并发数。那么显而易见的，就是会有很多进程在等待中。等什么？最多的应该是等待网络传输。其缺点胖友应该也感觉到了，此处不述。

**思考下，Java 的 NIO 和 BIO 的对比哟。**

而 Nginx 的异步非阻塞工作方式正是利用了这点等待的时间。在需要等待的时候，这些进程就空闲出来待命了。因此表现为少数几个进程就解决了大量的并发问题。

Nginx是如何利用的呢，简单来说：同样的 4 个进程，如果采用一个进程负责一个 request 的方式，那么，同时进来 4 个 request 之后，每个进程就负责其中一个，直至会话关闭。期间，如果有第 5 个request进来了。就无法及时反应了，因为 4 个进程都没干完活呢，因此，一般有个调度进程，每当新进来了一个 request ，就新开个进程来处理。

**回想下，BIO 是不是存在酱紫的问题？嘻嘻。**

Nginx 不这样，每进来一个 request ，会有一个 worker 进程去处理。但不是全程的处理，处理到什么程度呢？处理到可能发生阻塞的地方，比如向上游（后端）服务器转发 request ，并等待请求返回。那么，这个处理的 worker 不会这么傻等着，他会在发送完请求后，注册一个事件：“如果 upstream 返回了，告诉我一声，我再接着干”。于是他就休息去了。此时，如果再有 request 进来，他就可以很快再按这种方式处理。而一旦上游服务器返回了，就会触发这个事件，worker 才会来接手，这个 request 才会接着往下走。

**这就是为什么说，Nginx 基于事件模型。**

由于 web server 的工作性质决定了每个 request 的大部份生命都是在网络传输中，实际上花费在 server 机器上的时间片不多。这是几个进程就解决高并发的秘密所在。即：

**webserver 刚好属于网络 IO 密集型应用，不算是计算密集型。**

而正如叔度所说的

**异步，非阻塞，使用 epoll ，和大量细节处的优化**

也正是 Nginx 之所以然的技术基石。


### [2、请解释 Nginx 如何处理 HTTP 请求。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#2请解释-nginx-如何处理-http-请求。)  


Nginx 使用反应器模式。主事件循环等待操作系统发出准备事件的信号，这样数据就可以从套接字读取，在该实例中读取到缓冲区并进行处理。单个线程可以提供数万个并发连接。


### [3、为什么要做动、静分离？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#3为什么要做动静分离)  


在我们的软件开发中，有些请求是需要后台处理的（如：.jsp,.do等等），有些请求是不需要经过后台处理的（如：css、html、jpg、js等等），这些不需要经过后台处理的文件称为静态文件，否则动态文件。因此我们后台处理忽略静态文件，但是如果直接忽略静态文件的话，后台的请求次数就明显增多了。在我们对资源的响应速度有要求的时候，应该使用这种动静分离的策略去解决动、静分离将网站静态资源（HTML，JavaScript，CSS等）与后台应用分开部署，提高用户访问静态代码的速度，降低对后台应用访问。这里将静态资源放到nginx中，动态资源转发到[tomcat](https://www.wkcto.com/courses/tomcat.html)服务器中,毕竟Tomcat的优势是处理动态请求。



### [4、nginx是如何实现高并发的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#4nginx是如何实现高并发的)  


一个主进程，多个工作进程，每个工作进程可以处理多个请求，每进来一个request，会有一个worker进程去处理。但不是全程的处理，处理到可能发生阻塞的地方，比如向上游（后端）服务器转发request，并等待请求返回。那么，这个处理的worker继续处理其他请求，而一旦上游服务器返回了，就会触发这个事件，worker才会来接手，这个request才会接着往下走。由于web server的工作性质决定了每个request的大部份生命都是在网络传输中，实际上花费在server机器上的时间片不多。这是几个进程就解决高并发的秘密所在。即@skoo所说的webserver刚好属于网络io密集型应用，不算是计算密集型。


### [5、Nginx静态资源?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#5nginx静态资源)  


静态资源访问，就是存放在nginx的html页面，我们可以自己编写


### [6、Nginx配置高可用性怎么配置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#6nginx配置高可用性怎么配置)  


当上游服务器(真实访问服务器)，一旦出现故障或者是没有及时相应的话，应该直接轮训到下一台服务器，保证服务器的高可用

Nginx配置代码：

```
server {
    listen 80;
    server_name www.lijie.com;cc  nginx发送给上游服务器(真实访问的服务器)超时时间
        proxy_send_timeout 1s;###
        nginx接受上游服务器(真实访问的服务器)超时时间
        proxy_read_timeout 1s;
        index index.html index.htm;
    }
}
```


### [7、502错误可能原因](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#7502错误可能原因)  


**1、** FastCGI进程是否已经启动

**2、** FastCGI worker进程数是否不够

**3、** FastCGI执行时间过长

**1、** fastcgi_connect_timeout 300;

**2、** fastcgi_send_timeout 300;

**3、** fastcgi_read_timeout 300;

**FastCGI Buffer不够**

**1、** nginx和apache一样，有前端缓冲限制，可以调整缓冲参数

**2、** fastcgi_buffer_size 32k;

**3、** fastcgi_buffers 8 32k;

**Proxy Buffer不够**

**1、** 如果你用了Proxying，调整

**2、** proxy_buffer_size 16k;

**3、** proxy_buffers 4 16k;

**php脚本执行时间过长**

将php-fpm.conf的0s的0s改成一个时间


### [8、在 Nginx 中，解释如何在 URL 中保留双斜线?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#8在-nginx-中解释如何在-url-中保留双斜线)  


要在 URL 中保留双斜线，就必须使用 merge_slashes_off;

语法:merge_slashes [on/off]

默认值: merge_slashes on

环境: http，server


### [9、Nginx服务器上的Master和Worker进程分别是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#9nginx服务器上的master和worker进程分别是什么)  


Master进程：读取及评估配置和维持 ；Worker进程：处理请求。


### [10、Nginx的优缺点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题大汇总，附答案.md#10nginx的优缺点)  


**优点：**

**1、**  占内存小，可实现高并发连接，处理响应快

**2、**  可实现http服务器、虚拟主机、方向代理、负载均衡

**3、**  Nginx配置简单

**4、**  可以不暴露正式的服务器IP地址

**缺点：**

动态处理差，nginx处理静态文件好,耗费内存少，但是处理动态页面则很鸡肋，现在一般前端用nginx作为反向代理抗住压力，


### 11、nginx和apache的区别？
### 12、令牌桶算法#
### 13、为什么 Nginx 不使用多线程？
### 14、为什么要用Nginx？
### 15、基于端口的虚拟主机
### 16、什么是动态资源、静态资源分离？
### 17、请解释 Nginx 服务器上的 Master 和 Worker 进程分别是什么?
### 18、ngx_http_upstream_module的作用是什么?
### 19、在Nginx中，如何使用未定义的服务器名称来阻止处理请求?
### 20、使用“反向代理服务器”的优点是什么？
### 21、在Nginx中如何在URL中保留双斜线?
### 22、Nginx 常用命令？
### 23、用 Nginx 服务器解释-s 的目的是什么?
### 24、url_hash(第三方插件)
### 25、请解释什么是`C10K`问题?
### 26、为什么Nginx性能这么高？
### 27、Nginx是否支持将请求压缩到上游?
### 28、权重 weight
### 29、Nginx 有哪些负载均衡策略？
### 30、如何通过不同于80的端口开启Nginx?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




