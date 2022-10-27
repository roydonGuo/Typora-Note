# Android最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、如何将SQLite数据库(dictionary.db文件)与apk文件一起发布?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#1如何将sqlite数据库dictionarydb文件与apk文件一起发布)  


可以将dictionary.db文件复制到Eclipse Android工程中的res aw目录中。所有在res aw目录中的文件不会被压缩，这样可以直接提取该目录中的文件。可以将dictionary.db文件复制到res aw目录中


### [2、谈谈对Android NDK的理解](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#2谈谈对android-ndk的理解)  


NDK是一系列工具的集合.NDK提供了一系列的工具,帮助开发者快速开发C或C++的动态库,并能自动将so和java应用一起打包成apk.这些工具对开发者的帮助是巨大的.NDK集成了交叉编译器,并提供了相应的mk文件隔离CPU,平台,ABI等差异,开发人员只需要简单修改 mk文件(指出"哪些文件需要编译","编译特性要求"等),就可以创建出so.

NDK可以自动地将so和Java应用一起打包,极大地减轻了开发人员的打包工作.NDK提供了一份稳定,功能有限的API头文件声明.

Google明确声明该API是稳定的,在后续所有版本中都稳定支持当前发布的API.从该版本的NDK中看出,这些 API支持的功能非常有限,包含有:C标准库(libc),标准数学库(libm ),压缩库(libz),Log库(liblog).


### 3、NDK

**1、** NDK是一系列工具集合，NDK提供了一系列的工具，帮助开发者迅速的开发C/C++的动态库，并能自动将so和Java应用打成apk包。

**2、** NDK集成了交叉编译器，并提供了相应的mk文件和隔离cpu、平台等的差异，开发人员只需要简单的修改mk文件就可以创建出so文件。


### [4、Service和Thread的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#4service和thread的区别)  


servie是系统的组件，它由系统进程托管（servicemanager）；它们之间的通信类似于client和server，是一种轻量级的ipc通信，这种通信的载体是binder，它是在linux层交换信息的一种ipc。而thread是由本应用程序托管。1)、Thread：Thread 是程序执行的最小单元，它是分配CPU的基本单位。可以用 Thread 来执行一些异步的操作。

2)、Service：Service 是android的一种机制，当它运行的时候如果是Local Service，那么对应的 Service 是运行在主进程的 main 线程上的。如：onCreate，onStart 这些函数在被系统调用的时候都是在主进程的 main 线程上运行的。如果是Remote Service，那么对应的 Service 则是运行在独立进程的 main 线程上。

既然这样，那么我们为什么要用 Service 呢？其实这跟 android 的系统机制有关，我们先拿 Thread 来说。Thread 的运行是独立于 Activity 的，也就是说当一个 Activity 被 finish 之后，如果你没有主动停止 Thread 或者 Thread 里的 run 方法没有执行完毕的话，Thread 也会一直执行。因此这里会出现一个问题：当 Activity 被 finish 之后，你不再持有该 Thread 的引用。另一方面，你没有办法在不同的 Activity 中对同一 Thread 进行控制。

举个例子：如果你的 Thread 需要不停地隔一段时间就要连接服务器做某种同步的话，该 Thread 需要在 Activity 没有start的时候也在运行。这个时候当你 start 一个 Activity 就没有办法在该 Activity 里面控制之前创建的 Thread。因此你便需要创建并启动一个 Service ，在 Service 里面创建、运行并控制该 Thread，这样便解决了该问题（因为任何 Activity 都可以控制同一 Service，而系统也只会创建一个对应 Service 的实例）。

因此你可以把 Service 想象成一种消息服务，而你可以在任何有 Context 的地方调用 Context.startService、Context.stopService、Context.bindService，Context.unbindService，来控制它，你也可以在 Service 里注册 BroadcastReceiver，在其他地方通过发送 broadcast 来控制它，当然这些都是 Thread 做不到的。


### [5、如何将打开res aw目录中的数据库文件?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#5如何将打开res-aw目录中的数据库文件)  


**1、** 在Android中不能直接打开res aw目录中的数据库文件，而需要在程序第一次启动时将该文件复制到手机内存或SD卡的某个目录中，然后再打开该数据库文件。

**2、** 复制的基本方法是使用getResources().openRawResource方法获得res aw目录中资源的 InputStream对象，然后将该InputStream对象中的数据写入其他的目录中相应文件中。

**3、** 在Android SDK中可以使用SQLiteDatabase.openOrCreateDatabase方法来打开任意目录中的SQLite数据库文件。


### [6、请介绍下ContentProvider是如何实现数据共享的。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#6请介绍下contentprovider是如何实现数据共享的。)  


一个程序可以通过实现一个Content provider的抽象接口将自己的数据完全暴露出去，而且Content providers是以类似数据库中表的方式将数据暴露。Content providers存储和检索数据，通过它可以让所有的应用程序访问到，这也是应用程序之间唯一共享数据的方法。

要想使应用程序的数据公开化，可通过2种方法：创建一个属于你自己的Content provider或者将你的数据添加到一个已经存在的Content provider中，前提是有相同数据类型并且有写入Content provider的权限。

如何通过一套标准及统一的接口获取其他应用程序暴露的数据？

Android提供了ContentResolver，外界的程序可以通过ContentResolver接口访问ContentProvider提供的数据。


### [7、自定义view的基本流程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#7自定义view的基本流程)  


**1、** 自定义View的属性 编写attr.xml文件

**2、** 在layout布局文件中引用，同时引用命名空间

**3、** 在View的构造方法中获得我们自定义的属性 ，在自定义控件中进行读取（构造方法拿到attr.xml文件值）

**4、** 重写onMesure

**5、** 重写onDraw


### [8、Service 里面可以弹吐司么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#8service-里面可以弹吐司么)  


可以。


### [9、AIDL 的全称是什么?如何工作?能处理哪些类型的数据？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#9aidl-的全称是什么如何工作能处理哪些类型的数据)  


AIDL 全称 Android Interface Definition Language（AndRoid 接口描述语言） 是一种接口描述语言; 编译器可以通过 aidl 文件生成一段代码，通过预先定义的接口达到两个进程内部通信进程跨界对象访问的目的。需要完成两件事情：

**1、** 引入 AIDL 的相关类.;

**2、** 调用 aidl 产生的 class

理论上, 参数可以传递基本数据类型和 String, 还有就是 Bundle 的派生类, 不过在 Eclipse 中,目前的 ADT 不支持 Bundle 做为参数。


### [10、ListView 可以显示多种类型的条目吗](https://gitee.com/souyunku/DevBooks/blob/master/docs/Android/Android最新2021年面试题大汇总，附答案.md#10listview-可以显示多种类型的条目吗)  


这个当然可以的，ListView 显示的每个条目都是通过 baseAdapter 的 getView(int position,View convertView, ViewGroup parent)来展示的，理论上我们完全可以让每个条目都是不同类型的view。

比如：从服务器拿回一个标识为 id=1,那么当 id=1 的时候，我们就加载类型一的条目，当 id=2的时候，加载类型二的条目。常见布局在资讯类客户端中可以经常看到。

除此之外 adapter 还提供了 getViewTypeCount（）和 getItemViewType(int position)两个方法。在 getView 方法中我们可以根据不同的 viewtype 加载不同的布局文件。


### 11、Android与服务器交互的方式中的对称加密和非对称加密是什么?
### 12、Adapter是什么？你所接触过的adapter有那些？
### 13、子线程中能不能 new handler？为什么？
### 14、View
### 15、Framework 工作方式及原理，Activity 是如何生成一个 view 的，机制是什么？
### 16、Android中activity，context，application有什么不同。
### 17、DDMS和TraceView的区别?
### 18、Service 和 Activity 在同一个线程吗
### 19、ListView 如何定位到指定位置
### 20、启动一个程序，可以主界面点击图标进入，也可以从一个程序中跳转过去，二者有什么区别？
### 21、Android i18n
### 22、谈谈你对 Bitmap 的理解, 什么时候应该手动调用 bitmap.recycle()
### 23、SharedPreference跨进程使用会怎么样？如何保证跨进程使用安全？
### 24、注册广播有几种方式，这些方式有何优缺点？请谈谈Android引入广播机制的用意。
### 25、即时通讯是是怎么做的?
### 26、了解IntentServices吗?
### 27、横竖屏切换的Activity 生命周期变化？
### 28、什么是IntentService？有何优点？
### 29、Android中的长度单位详解





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




