# Java最新基础面试题及答案整理


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、String 属于基础的数据类型吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#1string-属于基础的数据类型吗)  


String 不属于基础类型，基础类型有 8 种：byte、boolean、char、short、int、float、long、double，而 String 属于对象。


### [2、如何实现对象克隆？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#2如何实现对象克隆)  




有两种方式：

1)、实现Cloneable接口并重写Object类中的clone()方法；

2)、实现Serializable接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆，代码如下。

```
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

public class MyUtil {

    private MyUtil() {
        throw new AssertionError();
    }

    @SuppressWarnings("unchecked")
    public static <T extends Serializable> T clone(T obj) throws Exception {
        ByteArrayOutputStream bout = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(bout);
        oos.writeObject(obj);

        ByteArrayInputStream bin = new ByteArrayInputStream(bout.toByteArray());
        ObjectInputStream ois = new ObjectInputStream(bin);
        return (T) ois.readObject();

        // 说明：调用ByteArrayInputStream或ByteArrayOutputStream对象的close方法没有任何意义
        // 这两个基于内存的流只要垃圾回收器清理对象就能够释放资源，这一点不同于对外部资源（如文件流）的释放
    }
}
```

下面是测试代码：

```
import java.io.Serializable;

/
 * 人类
 * @author 骆昊
 *
 */
class Person implements Serializable {
    private static final long serialVersionUID = -9102017020286042305L;

    private String name;    // 姓名
    private int age;        // 年龄
    private Car car;        // 座驾

    public Person(String name, int age, Car car) {
        this.name = name;
        this.age = age;
        this.car = car;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Car getCar() {
        return car;
    }

    public void setCar(Car car) {
        this.car = car;
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + ", car=" + car + "]";
    }

}
```

```
/
 * 小汽车类
 * @author 骆昊
 *
 */
class Car implements Serializable {
    private static final long serialVersionUID = -5713945027627603702L;

    private String brand;       // 品牌
    private int maxSpeed;       // 最高时速

    public Car(String brand, int maxSpeed) {
        this.brand = brand;
        this.maxSpeed = maxSpeed;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getMaxSpeed() {
        return maxSpeed;
    }

    public void setMaxSpeed(int maxSpeed) {
        this.maxSpeed = maxSpeed;
    }

    @Override
    public String toString() {
        return "Car [brand=" + brand + ", maxSpeed=" + maxSpeed + "]";
    }

}
```

```
class CloneTest {

    public static void main(String[] args) {
        try {
            Person p1 = new Person("Hao LUO", 33, new Car("Benz", 300));
            Person p2 = MyUtil.clone(p1);   // 深度克隆
            p2.getCar().setBrand("BYD");
            // 修改克隆的Person对象p2关联的汽车对象的品牌属性
            // 原来的Person对象p1关联的汽车不会受到任何影响
            // 因为在克隆Person对象时其关联的汽车对象也被克隆了
            System.out.println(p1);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

> 注意：基于序列化和反序列化实现的克隆不仅仅是深度克隆，更重要的是通过泛型限定，可以检查出要克隆的对象是否支持序列化，这项检查是编译器完成的，不是在运行时抛出异常，这种是方案明显优于使用Object类的clone方法克隆对象。让问题在编译的时候暴露出来总是好过把问题留到运行时。



### [3、Java最顶级的父类是哪个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#3java最顶级的父类是哪个)  


Object


### [4、如何通过反射创建对象？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#4如何通过反射创建对象)  




**1、** 方法1：通过类对象调用newInstance()方法，例如：String.class.newInstance()

**2、** 方法2：通过类对象的getConstructor()或getDeclaredConstructor()方法获得构造器（Constructor）对象并调用其newInstance()方法创建对象，例如：String.class.getConstructor(String.class).newInstance(“Hello”);


### [5、Java 中堆和栈有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#5java-中堆和栈有什么区别)  


JVM 中堆和栈属于不同的内存区域，使用目的也不同。栈常用于保存方法帧和局部变量，而对象总是在堆上分配。栈通常都比堆小，也不会在多个线程之间共享，而堆被整个 JVM 的所有线程共享。


### [6、volatile 能使得一个非原子操作变成原子操作吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#6volatile-能使得一个非原子操作变成原子操作吗)  


**1、** 关键字volatile的主要作用是使变量在多个线程间可见，但无法保证原子性，对于多个线程访问同一个实例变量需要加锁进行同步。

**2、** 虽然volatile只能保证可见性不能保证原子性，但用volatile修饰long和double可以保证其操作原子性。

**所以从Oracle Java Spec里面可以看到：**

**1、** 对于64位的long和double，如果没有被volatile修饰，那么对其操作可以不是原子的。在操作的时候，可以分成两步，每次对32位操作。

**2、** 如果使用volatile修饰long和double，那么其读写都是原子操作

**3、** 对于64位的引用地址的读写，都是原子操作

**4、** 在实现JVM时，可以自由选择是否把读写long和double作为原子操作

**5、** 推荐JVM实现为原子操作


### [7、为什么选择使用框架而不是原生?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#7为什么选择使用框架而不是原生)  


框架的好处:

**1、** 组件化: 其中以 React 的组件化最为彻底,甚至可以到函数级别的原子组件,高度的组件化可以是我们的工程易于维护、易于组合拓展。

**2、** 天然分层: JQuery 时代的代码大部分情况下是面条代码,耦合严重,现代框架不管是 MVC、MVP还是MVVM 模式都能帮助我们进行分层，代码解耦更易于读写。

**3、** 生态: 现在主流前端框架都自带生态,不管是数据流管理架构还是 UI 库都有成熟的解决方案。

**4、** 开发效率: 现代前端框架都默认自动更新DOM,而非我们手动操作,解放了开发者的手动DOM成本,提高开发效率,从根本上解决了UI 与状态同步问题.


### [8、你能写出一个正则表达式来判断一个字符串是否是一个数字吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#8你能写出一个正则表达式来判断一个字符串是否是一个数字吗)  


一个数字字符串，只能包含数字，如 0 到 9 以及 +、- 开头，通过这个信息，你可以下一个如下的正则表达式来判断给定的字符串是不是数字。

```
首先要import java.util.regex.Pattern 和 java.util.regex.Matcher
public boolean isNumeric(String str){ 
   Pattern pattern = Pattern.compile("[0-9]*"); 
   Matcher isNum = pattern.matcher(str);
   if( !isNum.matches() ){
       return false; 
   } 
   return true; 
}
```


### [9、运行时栈帧包含哪些结构？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#9运行时栈帧包含哪些结构)  


**1、** 局部变量表

**2、** 操作数栈

**3、** 动态连接

**4、** 返回地址

**5、** 附加信息


### [10、什么是Java程序的主类？应用程序和小程序的主类有何不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新基础面试题及答案整理.md#10什么是java程序的主类应用程序和小程序的主类有何不同)  


一个程序中可以有多个类，但只能有一个类是主类。在Java应用程序中，这个主类是指包含main（）方法的类。而在Java小程序中，这个主类是一个继承自系统类JApplet或Applet的子类。应用程序的主类不一定要求是public类，但小程序的主类要求必须是public类。主类是Java程序执行的入口点。


### 11、什么是模板方法模式？
### 12、Java 中应该使用什么数据类型来代表价格？
### 13、本地方法栈
### 14、静态方法和实例方法有何不同？
### 15、JAVA虚引用
### 16、Java应用程序与小程序之间有那些差别？
### 17、sleep方法和wait方法有什么区别?
### 18、普通类与抽象类有什么区别？
### 19、现实生活中的模板方法
### 20、一个线程运行时发生异常会怎样？
### 21、重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
### 22、Java 中怎么创建 ByteBuffer？
### 23、Json是什么？
### 24、JVM调优命令有哪些？
### 25、集合的特点
### 26、Java内存模型
### 27、什么是线程同步和线程互斥，有哪几种实现方式？
### 28、Java 中，throw 和 throws 有什么区别
### 29、运行时常量池溢出的原因？
### 30、假如生产环境CPU占用过高，请谈谈你的分析思路和定位。
### 31、Java的双亲委托机制是什么？
### 32、什么是不可变对象（immutable object）？Java 中怎么创建一个不可变对象？
### 33、char 型变量中能不能存贮一个中文汉字，为什么？
### 34、84.Map有什么特点
### 35、监听器有哪些作用和用法？
### 36、final 在 java 中有什么作用？
### 37、Minor GC与Full GC分别在什么时候发生？
### 38、Minor Gc和Full GC 有什么不同呢？
### 39、Java 中，怎样才能打印出数组中的重复元素？
### 40、一个java类中包含那些内容？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




