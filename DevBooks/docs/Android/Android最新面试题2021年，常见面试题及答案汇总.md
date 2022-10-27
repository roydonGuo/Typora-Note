# Android最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、dagger2](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#1dagger2)  


Dagger2是一个主要用于依赖注入的框架，减少初始化对象操作，降低耦合度


### [2、Android中touch事件的传递机制是怎样的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#2android中touch事件的传递机制是怎样的)  


**1、** Touch事件传递的相关API有dispatchTouchEvent、onTouchEvent、onInterceptTouchEvent

**2、** Touch事件相关的类有View、ViewGroup、Activity

**3、** Touch事件会被封装成MotionEvent对象，该对象封装了手势按下、移动、松开等动作

**4、** Touch事件通常从Activity#dispatchTouchEvent发出，只要没有被消费，会一直往下传递，到最底层的View。

**5、** 如果Touch事件传递到的每个View都不消费事件，那么Touch事件会反向向上传递,最终交由Activity#onTouchEvent处理、

**6、** onInterceptTouchEvent为ViewGroup特有，可以拦截事件、

**7、** Down事件到来时，如果一个View没有消费该事件，那么后续的MOVE/UP事件都不会再给它


### [3、Android中任务栈的分配](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#3android中任务栈的分配)  


Task实际上是一个Activity栈，通常用户感受的一个Application就是一个Task。从这个定义来看，Task跟Service或者其他Components是没有任何联系的，它只是针对Activity而言的。

Activity有不同的启动模式, 可以影响到task的分配


### [4、说说mvc模式的原理，它在android中的运用,android的官方建议应用程序的开发采用mvc模式。何谓mvc？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#4说说mvc模式的原理它在android中的运用,android的官方建议应用程序的开发采用mvc模式。何谓mvc)  


mvc是model,view,controller的缩写，mvc包含三个部分：

**1、** 模型（model）对象：是应用程序的主体部分，所有的业务逻辑都应该写在该层。

**2、** 视图（view）对象：是应用程序中负责生成用户界面的部分。也是在整个mvc架构中用户唯一可以看到的一层，接收用户的输入，显示处理结果。

**3、** 控制器（control）对象：是根据用户的输入，控制用户界面数据显示及更新model对象状态的部分，控制器更重要的一种导航功能，响应用户出发的相关事件，交给m层处理。

**android鼓励弱耦合和组件的重用，在android中mvc的具体体现如下：**

**1、** 视图层（view）：一般采用xml文件进行界面的描述，使用的时候可以非常方便的引入，当然，如果你对android了解的比较的多了话，就一定可以想到在android中也可以使用JavaScript+html等的方式作为view层，当然这里需要进行java和javascript之间的通信，幸运的是，android提供了它们之间非常方便的通信实现。

**2、** 控制层（controller）：android的控制层的重任通常落在了众多的acitvity的肩上，这句话也就暗含了不要在acitivity中写代码，要通过activity交割model业务逻辑层处理，这样做的另外一个原因是android中的acitivity的响应时间是5s，如果耗时的操作放在这里，程序就很容易被回收掉。

**3、** 模型层（model）：对数据库的操作、对网络等的操作都应该在model里面处理，当然对业务计算等操作也是必须放在的该层的。


### [5、内存泄露如何查看和解决](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#5内存泄露如何查看和解决)  


概念：有些对象只有有限的生命周期，当他们的任务完成之后，它们将被垃圾回收，如果在对象的生命周期本该结束的时候，这个对象还被一系列的引用，着就会导致内存泄露。

解决方法：使用开源框架LeakCanary检测针对性解决

**常见的内存泄露有：**

**1、** 单例造成的内存泄露，例如单例中的Context生命周期大于本身Context生命周期

**2、** 线程使用Hander造成的内存卸扣，当activity已经结束，线程依然在运行更新UI

**3、** 非静态类使用静态变量导致无法回收释放造成泄露

**4、** WebView网页过多造成内存泄露

**5、** 资源未关闭造成泄露，例如数据库使用完之后关闭连接


### [6、推送到达率如何提高](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#6推送到达率如何提高)  


判手机系统，小米使用小米推送，华为使用华为推送，其他手机使用友盟推送


### [7、简述JNI](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#7简述jni)  


是java和c语言之间的桥梁，由于java是一种半解释语言，可以被反编译出来，一种重要涉及安全的代码就使用了C编程，再者很多底层功能调用C语言都实现了Java没必要重复造轮子，所以定义了JNI接口的实现


### [8、Fragment中add与replace的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#8fragment中add与replace的区别)  


add不会重新初始化fragment,replace每次都会；

添加相同的fragment时，replace不会有任何变化，add会报IllegalStateException 异常；

replace 先 remove 掉相同 id 的所有 fragment，然后在add 当前的这个 fragment，而 add 是覆盖前一个fragment。所以如果使用 add 一般会伴随 hide()和show()，避免布局重叠；

使用 add，如果应用放在后台，或以其他方式被系统销毁，再打开时，hide()中引用的 fragment 会销毁，所以依然会出现布局重叠 bug，可以使用 replace 或使用 add时，添加一个 tag 参数；


### [9、Android root机制](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#9android-root机制)  


root指的是你有权限可以再系统上对所有档案有 "读" "写" "执行"的权力。root机器不是真正能让你的应用程序具有root权限。它原理就跟linux下的像sudo这样的命令。在系统的bin目录下放个su程序并属主是root并有suid权限。则通过su执行的命令都具有Android root权限。当然使用临时用户权限想把su拷贝的/system/bin目录并改属性并不是一件容易的事情。这里用到2个工具跟2个命令。把busybox拷贝到你有权限访问的目录然后给他赋予4755权限，你就可以用它做很多事了。


### [10、内存溢出和内存泄漏有什么区别？何时会产生内存泄漏？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新面试题2021年，常见面试题及答案汇总.md#10内存溢出和内存泄漏有什么区别何时会产生内存泄漏)  


内存溢出：当程序运行时所需的内存大于程序允许的最高内存，这时会出现内存溢出；

内存泄漏：在一些比较消耗资源的操作中，如果操作中内存一直未被释放，就会出现内存泄漏。比如未关闭io,cursor。


### 11、如何切换 fragement,不重新实例化
### 12、Android中的ANR
### 13、谈谈Android的IPC（进程间通信）机制
### 14、让Activity变成一个窗口
### 15、如果Listview中的数据源发生改变，如何更新listview中的数据
### 16、如何将SQLite数据库(dictionary.db文件)与apk文件一起发布
### 17、广播接受者的生命周期？
### 18、Activity启动模式
### 19、属性动画
### 20、android 中有哪几种解析xml的类？官方推荐哪种？以及它们的原理和区别。
### 21、Intent 传递数据时，可以传递哪些类型数据？
### 22、开发中都使用过哪些框架、平台
### 23、什么是 IntentService？有何优点？
### 24、如何启用Service，如何停用Service。
### 25、请介绍下Android的数据存储方式。
### 26、sim卡的EF文件是什么？有何作用
### 27、activity与fragment区别
### 28、wait和 sleep 的区别
### 29、谈MVC ，MVP，MVVM





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




