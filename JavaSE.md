# String



用构造函数创建字符串：

```java
String str =new String("Runoob");
//使用关键字：
String str2 = "Runoob";
```

String 创建的字符串存储在公共池中，而 new 创建的字符串对象在堆上：

```java
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建
```

![https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png](https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png)

**注意:**String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了。

如果需要对字符串做很多修改，那么应该选择使用 [StringBuffer & StringBuilder 类](https://www.runoob.com/java/java-stringbuffer.html)。



![image-20220831130223205](C:\Users\31330\Pictures\Typora\image-20220831130223205.png)

![image-20220831130335362](C:\Users\31330\Pictures\Typora\image-20220831130335362.png)

Test的s3 = s2 + “c” 中s2没加引号，结果s3存放在堆内存中

![image-20220831155818050](C:\Users\31330\Pictures\Typora\image-20220831155818050.png)

拼接，反转字符串推荐 StringBuilder

![image-20220831155944865](C:\Users\31330\Pictures\Typora\image-20220831155944865.png)

# ArrayList和LinkedList

集合类型大小不固定，可变，灵活，且增删查改方便。

![image-20220831133003613](C:\Users\31330\Pictures\Typora\image-20220831133003613.png)



对比：

> ArrayList（数组）：有角标，查询快，向指定位置插入和删除，需要角标移位，效率低。需要连续的内存空间。长度不可变。
>
> LinkedList（链表）：头指针和尾指针（内存中的位置）。不需连续空间。查询慢（需要找指针）。插入删除快。

Arrays和Array是什么区别，ArrayList呢？

> 答：Arrays是Java提供的一种操作数组的工具类，Array是数组，ArrayList就是基于数组实现的一种集合容器。

# 日期与时间

## Date 类



```java
Date date = new Date(); //获取当前时间，格式是国际时间
long time  = date.getTime(); //获取时间戳，单位毫秒
```

```java
long time = System.cuttentTimeMillis(); //获取当前时间戳
//time时间戳可以进行运算传入新时间给Date，例如：time+=60*60*24*1000;
Date date = new Date(time); //生成时间对象
```

## SimpleDateFormat 类

-->希望得到时间的格式：：![image-20220831161200717](C:\Users\31330\Pictures\Typora\image-20220831161200717.png)

Date类有自带比较时间方法：

- d1.after(d2); -->boolean
- d2.before(d1);

![image-20220831161052202](C:\Users\31330\Pictures\Typora\image-20220831161052202.png)

![image-20220831161231765](C:\Users\31330\Pictures\Typora\image-20220831161231765.png)

![image-20220831161513898](C:\Users\31330\Pictures\Typora\image-20220831161513898.png)

![image-20220831162019710](C:\Users\31330\Pictures\Typora\image-20220831162019710.png)

---

![image-20220831162751597](C:\Users\31330\Pictures\Typora\image-20220831162751597.png)

![image-20220831162840639](C:\Users\31330\Pictures\Typora\image-20220831162840639.png)

# 正则

matchs()

![image-20220831164223057](C:\Users\31330\Pictures\Typora\image-20220831164223057.png)

![image-20220831165204342](C:\Users\31330\Pictures\Typora\image-20220831165204342.png)

# 数组操作工具类 Arrays 

```java
Arrays.toString({1,2,3,4,5,6});// 输出[1,2,3,4,5,6]
```

```java
Arrays.sort({1,2,3,4,5,6});// 默认升序
```



![image-20220831180252811](C:\Users\31330\Pictures\Typora\image-20220831180252811.png)

降序 sort () 的 Lambda 写法：![image-20220831180949281](C:\Users\31330\Pictures\Typora\image-20220831180949281.png)

![image-20220831172113491](C:\Users\31330\Pictures\Typora\image-20220831172113491.png)

# Lambda 表达式

![image-20220831175839177](C:\Users\31330\Pictures\Typora\image-20220831175839177.png)

![image-20220831180647745](C:\Users\31330\Pictures\Typora\image-20220831180647745.png)

# 集合体系





![image-20220909205615344](C:\Users\31330\Pictures\Typora\image-20220909205615344.png)

![image-20220909205816126](C:\Users\31330\Pictures\Typora\image-20220909205816126.png)

![image-20220909205827669](C:\Users\31330\Pictures\Typora\image-20220909205827669.png)

集合的遍历--迭代器

![image-20220909212309949](C:\Users\31330\Pictures\Typora\image-20220909212309949.png)

或者 forEach 遍历；使用 Lambda 简化写法；

![image-20220909215340186](C:\Users\31330\Pictures\Typora\image-20220909215340186.png)







https://www.bilibili.com/video/BV1Cv411372m?p=131&spm_id_from=pageDriver&vd_source=616a9dd528080cf576646147166fe033




https://www.bilibili.com/video/BV1MU4y1Y7h5?p=9&spm_id_from=pageDriver&vd_source=616a9dd528080cf576646147166fe033