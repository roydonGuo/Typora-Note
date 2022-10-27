### API 
    api的概述： 就是java替我们写好的一些类，他封装了一些功能，我们仅仅只需要知道如何使用即可

### Object 
    object的概述：
       A、 object是所有的类父类
       B、 object中的所有方法，子类都能使用（接口不是object的子类）
     
### Object 类中常用方法
     A、equals()  
        底层调用其实就是== 方法
        == 方法：
           基本数据类： 比较的是内容(值)
           引用数据类型：比较的是内存地址值
      String 的equals比较的是内容  

     B、String toString()
        问题：为什么要重写toString()方法
         
        答：打印时默认会调用toString()方法
         因为toString()方法来源于object中，object中getClass.getName()+"@" +Integer.toHexString(hasCode() ) --->打印就是内存地址值
        很多时候，我们不想看见内存地址值，想看到的是子类的特有属性值，这时就需要重写toString()方法


### String 
     在String 中认为都是对象，String str = "...";
     所以str 是对象，""也是对象
      String 是一个常量，其本质就是private final 修饰的字符数组     

    String的构造方法:
     new String(byte [] bytes, int offset,int length);
     offset: 数据解锁起始位置
     length:需要解锁的位数
  
    substring(int start ,int end );   包含头，不包含尾。 截取一段字符
    substring(int start);             从某一位到尾
    startsWith(String str)            判断以什么开头
    endsWith(String str)                        判断以什么结尾    
    contains(String str)               判断是否包含
    indexOf（String str）      
    charAt(int index)
    equals()                           注意：要区分大小写
    equalsIgnoreCase                   不区分大小写
    getBytes（）    
    toCharArray()            
    

###StringBuilder && StringBuffer

    1、 StringBuilder 是字符串缓冲对象，底层是一个没有用final修饰的数组，并且长度默认为16,底层是一个"可变数组"

    注意：是底层自动帮我们创建新数组，数组一旦创建，是不可变的

  

------------------------------------------------------------------------------------






### 面试题
    object类有哪些方法
   
    
###　final
　　　A、修饰类 ： 不能被继承
　　　B、修饰方法 ： 不能被重写
     C、修饰变量 ：  基本数据类型： 值不能改变
                    引用数据类型： 地址值不能改变



###  重写和重载
     重写：子类中出现和父类方法声明一模一样的方法,重写
     重载：本类中出现方法名相同，但参数列表不同，注意：与返回值类型无关


### 封装
    封装好处：
     A、提高了代码的复用性
     B、提高了代码的安全性
     C、隐藏了对象实现的细节，仅仅对外提供方法
 
### 继承
    A、提高了代码的复用性
    B、提高了代码的可维护性
    C、是类和类之间耦合起来了，这是多态的前提
    继承的弊端：
    开发的原则：高内聚，低耦合
    内聚：完成一个功能的能力
    耦合：类和类之间的关系   继承的注意事项：
 
     1、 子类继承父类，只能继承父类中非private修饰的成员变量和方法
     2、 简单说：子类有，父类有，找子类，子类没有，父类有，找父类
         
