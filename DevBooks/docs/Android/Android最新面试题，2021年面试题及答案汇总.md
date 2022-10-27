# Android最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、在 service 的生命周期方法 onstartConmand()可不可以执行网络操作？如何在 service 中执行网络操作？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#1在-service-的生命周期方法-onstartconmand可不可以执行网络操作如何在-service-中执行网络操作)  


可以的，就在onstartConmand方法内执行。


### [2、简述TCP，UDP，Socket](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#2简述tcpudpsocket)  


TCP是经过3次握手，4次挥手完成一串数据的传送

UDP是无连接的，知道IP地址和端口号，向其发送数据即可，不管数据是否发送成功

Socket是一种不同计算机，实时连接，比如说传送文件，即时通讯


### [3、Android 中如何捕获未捕获的异常](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#3android-中如何捕获未捕获的异常)  


**UncaughtExceptionHandler**

**1、** 自 定 义 一 个 Application ， 比 如 叫 MyApplication 继 承 Application 实 现UncaughtExceptionHandler。

**2、** 覆写 UncaughtExceptionHandler 的 onCreate 和 uncaughtException 方法。 注意：上面的代码只是简单的将异常打印出来。在 onCreate 方法中我们给 Thread 类设置默认异常处理 handler，如果这句代码不执行则一切都是白搭。在 uncaughtException 方法中我们必须新开辟个线程进行我们异常的收集工作，然后将系统给杀死。

**3、** 在 AndroidManifest 中配置该 Application：<application android:name="com.example.uncatchexception.MyApplication"

Bug 收集工具 Crashlytics

Crashlytics 是专门为移动应用开发者提供的保存和分析应用崩溃的工具。国内主要使用的是友盟做数据统计。

**Crashlytics 的好处：**

**1、** Crashlytics 不会漏掉任何应用崩溃信息。

**2、** Crashlytics 可以象 Bug 管理工具那样，管理这些崩溃日志。

**3、** Crashlytics 可以每天和每周将崩溃信息汇总发到你的邮箱，所有信息一目了然。


### [4、android中的动画有哪几类，它们的特点和区别是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#4android中的动画有哪几类它们的特点和区别是什么)  


两种，一种是Tween动画、还有一种是Frame动画。Tween动画，这种实现方式可以使视图组件移动、放大、缩小以及产生透明度的变化;另一种Frame动画，传统的动画方法，通过顺序的播放排列好的图片来实现，类似电影。


### [5、Android 中的动画有哪几类，它们的特点和区别是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#5android-中的动画有哪几类它们的特点和区别是什么)  


Frame Animation(帧动画)主要用于播放一帧帧准备好的图片，类似GIF图片，优点是使用简单方便、缺点是需要事先准备好每一帧图片；

Tween Animation(补间动画)仅需定义开始与结束的关键帧，而变化的中间帧由系统补上，优点是不用准备每一帧，缺点是只改变了对象绘制，而没有改变View本身属性。因此如果改变了按钮的位置，还是需要点击原来按钮所在位置才有效。

Property Animation(属性动画)是3.0后推出的动画，优点是使用简单、降低实现的复杂度、直接更改对象的属性、几乎可适用于任何对象而仅非View类，主要包括ValueAnimator和ObjectAnimator


### [6、java中如何引用本地语言](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#6java中如何引用本地语言)  


可以用JNI（java native interface  java 本地接口）接口 。


### [7、请解释下在单线程模型中Message、Handler、Message Queue、Looper之间的关系。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#7请解释下在单线程模型中messagehandlermessage-queuelooper之间的关系。)  


简单的说，Handler获取当前线程中的looper对象，looper用来从存放Message的MessageQueue中取出Message，再有Handler进行Message的分发和处理.

Message Queue(消息队列)：用来存放通过Handler发布的消息，通常附属于某一个创建它的线程，可以通过Looper.myQueue()得到当前线程的消息队列

Handler：可以发布或者处理一个消息或者操作一个Runnable，通过Handler发布消息，消息将只会发送到与它关联的消息队列，然也只能处理该消息队列中的消息

Looper：是Handler和消息队列之间通讯桥梁，程序组件首先通过Handler把消息传递给Looper，Looper把消息放入队列。Looper也把消息队列里的消息广播给所有的

Handler：Handler接受到消息后调用handleMessage进行处理

Message：消息的类型，在Handler类中的handleMessage方法中得到单个的消息进行处理

在单线程模型下，为了线程通信问题，Android设计了一个Message Queue(消息队列)， 线程间可以通过该Message Queue并结合Handler和Looper组件进行信息交换。下面将对它们进行分别介绍：

**Message**

Message消息，理解为线程间交流的信息，处理数据后台线程需要更新UI，则发送Message内含一些数据给UI线程。

**Handler**

Handler处理者，是Message的主要处理者，负责Message的发送，Message内容的执行处理。后台线程就是通过传进来的 Handler对象引用来sendMessage(Message)。而使用Handler，需要implement 该类的 handleMessage(Message)方法，它是处理这些Message的操作内容，例如Update UI。通常需要子类化Handler来实现handleMessage方法。

**Message Queue**

Message Queue消息队列，用来存放通过Handler发布的消息，按照先进先出执行。

每个message queue都会有一个对应的Handler。Handler会向message queue通过两种方法发送消息：sendMessage或post。这两种消息都会插在message queue队尾并按先进先出执行。但通过这两种方法发送的消息执行的方式略有不同：通过sendMessage发送的是一个message对象,会被 Handler的handleMessage()函数处理；而通过post方法发送的是一个runnable对象，则会自己执行。

**Looper**

Looper是每条线程里的Message Queue的管家。Android没有Global的Message Queue，而Android会自动替主线程(UI线程)建立Message Queue，但在子线程里并没有建立Message Queue。所以调用Looper.getMainLooper()得到的主线程的Looper不为NULL，但调用Looper.myLooper() 得到当前线程的Looper就有可能为NULL。对于子线程使用Looper，API Doc提供了正确的使用方法：这个Message机制的大概流程：

**1、** 在Looper.loop()方法运行开始后，循环地按照接收顺序取出Message Queue里面的非NULL的Message。

**2、** 一开始Message Queue里面的Message都是NULL的。当Handler.sendMessage(Message)到Message Queue，该函数里面设置了那个Message对象的target属性是当前的Handler对象。随后Looper取出了那个Message，则调用 该Message的target指向的Hander的dispatchMessage函数对Message进行处理。在dispatchMessage方法里，如何处理Message则由用户指定，三个判断，优先级从高到低：

**1、** Message里面的Callback，一个实现了Runnable接口的对象，其中run函数做处理工作；

**2、** Handler里面的mCallback指向的一个实现了Callback接口的对象，由其handleMessage进行处理；

**3、** 处理消息Handler对象对应的类继承并实现了其中handleMessage函数，通过这个实现的handleMessage函数处理消息。

由此可见，我们实现的handleMessage方法是优先级最低的！

3\、Handler处理完该Message (update UI) 后，Looper则设置该Message为NULL，以便回收！

在网上有很多文章讲述主线程和其他子线程如何交互，传送信息，最终谁来执行处理信息之类的，个人理解是最简单的方法——判断Handler对象里面的Looper对象是属于哪条线程的，则由该线程来执行！

1\、当Handler对象的构造函数的参数为空，则为当前所在线程的Looper；

2\、Looper.getMainLooper()得到的是主线程的Looper对象，Looper.myLooper()得到的是当前线程的Looper对象。


### [8、广播注册](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#8广播注册)  


首先写一个类要继承BroadCastReceiver

第一种：在清单文件中声明，添加

```
<receive android:name=".BroadCastReceiverDemo">
<intent-filter>
<action android:name="android.provider.Telephony.SMS_RECEIVED">
</intent-filter>
</receiver>
```

第二种：使用代码进行注册如：

```
IntentFilter filter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED");
BroadCastReceiverDemo receiver = new BroadCastReceiver();
registerReceiver(receiver, filter);
```

两种注册类型的区别是：

a.第一种是常驻型广播，也就是说当应用程序关闭后，如果有信息广播来，程序也会被系统调用自动运行。

b.第二种不是常驻广播，也就是说广播跟随程序的生命周期。


### [9、Service生命周期](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#9service生命周期)  


在Service的生命周期里，常用的有：

4个手动调用的方法

```
startService()    启动服务
stopService()    关闭服务
bindService()    绑定服务
unbindService()    解绑服务
```

5个内部自动调用的方法

```
onCreat()            创建服务
onStartCommand()    开始服务
onDestroy()            销毁服务
onBind()            绑定服务
onUnbind()            解绑服务
```

**1、** 手动调用startService()启动服务，自动调用内部方法：onCreate()、onStartCommand()，如果一个Service被startService()多次启动，那么onCreate()也只会调用一次。

**2、** 手动调用stopService()关闭服务，自动调用内部方法：onDestory()，如果一个Service被启动且被绑定，如果在没有解绑的前提下使用stopService()关闭服务是无法停止服务的。

**3、** 手动调用bindService()后，自动调用内部方法：onCreate()、onBind()。

**4、** 手动调用unbindService()后，自动调用内部方法：onUnbind()、onDestory()。

**5、** startService()和stopService()只能开启和关闭Service，无法操作Service，调用者退出后Service仍然存在；bindService()和unbindService()可以操作Service，调用者退出后，Service随着调用者销毁。


### [10、请介绍下 AsyncTask 的内部实现和适用的场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题，2021年面试题及答案汇总.md#10请介绍下-asynctask-的内部实现和适用的场景)  


AsyncTask 内部也是 Handler 机制来完成的，只不过 Android 提供了执行框架来提供线程池来执行相应地任务，因为线程池的大小问题，所以 AsyncTask 只应该用来执行耗时时间较短的任务，比如 HTTP 请求，大规模的下载和数据库的更改不适用于 AsyncTask，因为会导致线程池堵塞，没有线程来执行其他的任务，导致的情形是会发生 AsyncTask 根本执行不了的问题


### 11、说下Activity 的四种启动模式、应用场景 ？
### 12、NDK是什么
### 13、请介绍下Android中常用的五种布局。
### 14、activity在屏幕旋转时的生命周期
### 15、Android中4大组件
### 16、如何对 Android 应用进行性能分析
### 17、ListView 中图片错位的问题是如何产生的
### 18、Fragment与activity如何传值和交互？
### 19、Android本身的api并未声明会抛出异常，则其在运行时有无可能抛出runtime异常，你遇到过吗？诺有的话会导致什么问题？如何解决？
### 20、说说 LruCache 底层原理
### 21、Android数字签名
### 22、Activity的状态有几种？
### 23、android的数据存储
### 24、一条最长的短信息约占多少byte?
### 25、Fragment 的 replace 和 add 方法的区别
### 26、为什么Android引入广播机制?
### 27、如何退出Activity？如何安全退出已调用多个Activity的Application？
### 28、系统上安装了多种浏览器，能否指定某浏览器访问指定页面？请说明原由。
### 29、说说 ContentProvider、ContentResolver、ContentObserver 之间的关系





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




