# Nginx最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、请陈述 stub_status 和 sub_filter 指令的作用是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#1请陈述-stub_status-和-sub_filter-指令的作用是什么)  


Stub_status 指令：该指令用于了解 Nginx 当前状态的当前状态，如当前的活

动连接，接受和处理当前读/写/等待连接的总数

Sub_filter 指令：它用于搜索和替换响应中的内容，并快速修复陈旧的数据


### [2、nignx配置](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#2nignx配置)  


```
worker_processes  8;     工作进程个数

worker_connections  65535;  每个工作进程能并发处理（发起）的最大连接数（包含所有连接数）

error_log         /data/logs/nginx/error.log;  错误日志打印地址

access_log      /data/logs/nginx/access.log  进入日志打印地址

log_format  main  'remote_addr"request" ''status upstream_addr "$request_time"'; 进入日志格式

fastcgi_connect_timeout=300; #连接到后端fastcgi超时时间

fastcgi_send_timeout=300; #向fastcgi请求超时时间(这个指定值已经完成两次握手后向fastcgi传送请求的超时时间)

fastcgi_rend_timeout=300; #接收fastcgi应答超时时间，同理也是2次握手后

fastcgi_buffer_size=64k; #读取fastcgi应答第一部分需要多大缓冲区，该值表示使用1个64kb的缓冲区读取应答第一部分(应答头),可以设置为fastcgi_buffers选项缓冲区大小

fastcgi_buffers 4 64k;#指定本地需要多少和多大的缓冲区来缓冲fastcgi应答请求，假设一个php或java脚本所产生页面大小为256kb,那么会为其分配4个64kb的缓冲来缓存

fastcgi_cache TEST;#开启fastcgi缓存并为其指定为TEST名称，降低cpu负载,防止502错误发生

listen       80;                                            监听端口

server_name  rrc.test.jiedaibao.com;       允许域名

root  /data/release/rrc/web;                    项目根目录

index  index.php index.html index.htm;  访问根文件
```


### [3、请列举 Nginx 服务器的最佳用途。Nginx 服务器的最佳用法是在网络上部署动态 HTTP 内容，使用 SCGI、WSGI 应](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#3请列举-nginx-服务器的最佳用途。nginx-服务器的最佳用法是在网络上部署动态-http-内容使用-scgiwsgi-应)  


用程序服务器、用于脚本的 FastCGI 处理程序。它还可以作为负载均衡器。


### [4、为什么要做动静分离？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#4为什么要做动静分离)  


**1、** Nginx是当下最热的Web容器，网站优化的重要点在于静态化网站，网站静态化的关键点则是是动静分离，动静分离是让动态网站里的动态网页根据一定规则把不变的资源和经常变的资源区分开来，动静资源做好了拆分以后，我们则根据静态资源的特点将其做缓存操作。

**2、** 让静态的资源只走静态资源服务器，动态的走动态的服务器

**3、** Nginx的静态处理能力很强，但是动态处理能力不足，因此，在企业中常用动静分离技术。

**4、** 对于静态资源比如图片，js，css等文件，我们则在反向代理服务器nginx中进行缓存。这样浏览器在请求一个静态资源时，代理服务器nginx就可以直接处理，无需将请求转发给后端服务器tomcat。

**5、** 若用户请求的动态文件，比如servlet,jsp则转发给Tomcat服务器处理，从而实现动静分离。这也是反向代理服务器的一个重要的作用。


### [5、Nginx怎么判断别IP不可访问？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#5nginx怎么判断别ip不可访问)  


```
# 如果访问的ip地址为192.168.9.115,则返回403
if  ($remote_addr = 192.168.9.115) {
     return 403;
}
```


### [6、nginx状态码](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#6nginx状态码)  


499：服务端处理时间过长，客户端主动关闭了连接。


### [7、Location正则案例](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#7location正则案例)  


**示例：**

```
#优先级

精确匹配，根路径
location = / {
   return 400;
}

#优先级2,以某个字符串开头,以av开头的，优先匹配这里，区分大小写
location ^~ /av {
    root / data / av / ;
}

#优先级
3，区分大小写的正则匹配，匹配 / media * * * * * 路径location~ / media {
    alias / data / static / ;
}

#优先级
4，不区分大小写的正则匹配，所有的 * * * * .jpg | gif | png都走这里
location~ * .*\.(jpg | gif | png | js | css) $ {
    root / data / av / ;
}

#优先
7，通用匹配
location / {
    return 403;
}
```


### [8、解释 Nginx 是否支持将请求压缩到上游?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#8解释-nginx-是否支持将请求压缩到上游)  


您可以使用 Nginx 模块 gunzip 将请求压缩到上游。gunzip 模块是一个过滤

器，它可以对不支持“gzip”编码方法的客户机或服务器使用“内容编

码:gzip”来解压缩响应。


### [9、使用“反向代理服务器”的优点是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#9使用“反向代理服务器的优点是什么)  


反向代理服务器可以隐藏源服务器的存在和特征。它充当互联网云和web服务器之间的中间层。这对于安全方面来说是很好的，特别是当您使用web托管服务时。


### [10、请解释是否有可能将 Nginx 的错误替换为 502 错误、503?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Nginx/Nginx最新2021年面试题，高级面试题及附答案解析.md#10请解释是否有可能将-nginx-的错误替换为-502-错误503)  


502 =错误网关

503 =服务器超载

有可能，但是您可以确保 fastcgi_intercept_errors 被设置为 ON，并使用错

误页面指令。

Location / {fastcgi_pass 127.0.01:9001;fastcgi_intercept_errors

on;error_page 502 =503/error_page.html;#…}


### 11、用Nginx服务器解释-s的目的是什么?
### 12、轮询(默认)
### 13、Nginx负载均衡的算法怎么实现的?策略有哪些?
### 14、列举Nginx服务器的最佳用途。
### 15、解释`Nginx`是否支持将请求压缩到上游?
### 16、Nginx 如何开启压缩？
### 17、用`Nginx`服务器解释`-s`的目的是什么?
### 18、在 Nginx 中，如何使用未定义的服务器名称来阻止处理请求?
### 19、Nginx应用场景？
### 20、解释如何在Nginx中获得当前的时间?
### 21、请解释`ngx_http_upstream_module`的作用是什么?
### 22、突发限制访问频率（突发流量）
### 23、Nginx如何处理HTTP请求？
### 24、请陈述stub_status和sub_filter指令的作用是什么?
### 25、Nginx怎么处理请求的？
### 26、什么是正向代理和反向代理？
### 27、怎么限制浏览器访问？
### 28、正常限制访问频率（正常流量）
### 29、解释如何在`Nginx`服务器上添加模块?
### 30、限流怎么做的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




