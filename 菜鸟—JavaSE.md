# print

```java
import java.util.Date;
 
/**
 * 使用printf输出
 */
/**关键技术点
 * 使用java.io.PrintStream的printf方法实现C风格的输出
 * printf 方法的第一个参数为输出的格式,第二个参数是可变长的,表示待输出的数据对象
 */
public class Printf {
 
       public static void main(String[] args) {
              /*** 输出字符串 ***/
              // %s表示输出字符串，也就是将后面的字符串替换模式中的%s
              System.out.printf("%s", new Integer(1212));
              // %n表示换行
              System.out.printf("%s%n", "end line");
              // 还可以支持多个参数
              System.out.printf("%s = %s%n", "Name", "Zhangsan");
              // %S将字符串以大写形式输出
              System.out.printf("%S = %s%n", "Name", "Zhangsan");
              // 支持多个参数时，可以在%s之间插入变量编号，1$表示第一个字符串，3$表示第3个字符串
              System.out.printf("%1$s = %3$s %2$s%n", "Name", "san", "Zhang");
             
              /*** 输出boolean类型 ***/
              System.out.printf("true = %b; false = ", true);
              System.out.printf("%b%n", false);
 
              /*** 输出整数类型***/
              Integer iObj = 342;
              // %d表示将整数格式化为10进制整数
              System.out.printf("%d; %d; %d%n", -500, 2343L, iObj);
              // %o表示将整数格式化为8进制整数
              System.out.printf("%o; %o; %o%n", -500, 2343L, iObj);
              // %x表示将整数格式化为16进制整数
              System.out.printf("%x; %x; %x%n", -500, 2343L, iObj);
              // %X表示将整数格式化为16进制整数，并且字母变成大写形式
              System.out.printf("%X; %X; %X%n", -500, 2343L, iObj);
             
              /*** 输出浮点类型***/
              Double dObj = 45.6d;
              // %e表示以科学技术法输出浮点数
              System.out.printf("%e; %e; %e%n", -756.403f, 7464.232641d, dObj);
              // %E表示以科学技术法输出浮点数，并且为大写形式            
              System.out.printf("%E; %E; %E%n", -756.403f, 7464.232641d, dObj);
              // %f表示以十进制格式化输出浮点数
              System.out.printf("%f; %f; %f%n", -756.403f, 7464.232641d, dObj);
              // 还可以限制小数点后的位数
              System.out.printf("%.1f; %.3f; %f%n", -756.403f, 7464.232641d, dObj);
             
              /*** 输出日期类型***/
              // %t表示格式化日期时间类型，%T是时间日期的大写形式，在%t之后用特定的字母表示不同的输出格式
              Date date = new Date();
              long dataL = date.getTime();
              // 格式化年月日
              // %t之后用y表示输出日期的年份（2位数的年，如99）
              // %t之后用m表示输出日期的月份，%t之后用d表示输出日期的日号
              System.out.printf("%1$ty-%1$tm-%1$td; %2$ty-%2$tm-%2$td%n", date, dataL);
              // %t之后用Y表示输出日期的年份（4位数的年），
              // %t之后用B表示输出日期的月份的完整名， %t之后用b表示输出日期的月份的简称
              System.out.printf("%1$tY-%1$tB-%1$td; %2$tY-%2$tb-%2$td%n", date, dataL);
             
              // 以下是常见的日期组合
              // %t之后用D表示以 "%tm/%td/%ty"格式化日期
              System.out.printf("%1$tD%n", date);
              //%t之后用F表示以"%tY-%tm-%td"格式化日期
              System.out.printf("%1$tF%n", date);
             
              /*** 输出时间类型***/
              // 输出时分秒
              // %t之后用H表示输出时间的时（24进制），%t之后用I表示输出时间的时（12进制），
              // %t之后用M表示输出时间的分，%t之后用S表示输出时间的秒
              System.out.printf("%1$tH:%1$tM:%1$tS; %2$tI:%2$tM:%2$tS%n", date, dataL);
              // %t之后用L表示输出时间的秒中的毫秒
              System.out.printf("%1$tH:%1$tM:%1$tS %1$tL%n", date);
              // %t之后p表示输出时间的上午或下午信息
              System.out.printf("%1$tH:%1$tM:%1$tS %1$tL %1$tp%n", date);
             
              // 以下是常见的时间组合
              // %t之后用R表示以"%tH:%tM"格式化时间
              System.out.printf("%1$tR%n", date);
              // %t之后用T表示以"%tH:%tM:%tS"格式化时间
              System.out.printf("%1$tT%n", date);
              // %t之后用r表示以"%tI:%tM:%tS %Tp"格式化时间
              System.out.printf("%1$tr%n", date);
             
              /*** 输出星期***/
              // %t之后用A表示得到星期几的全称
              System.out.printf("%1$tF %1$tA%n", date);
              // %t之后用a表示得到星期几的简称
              System.out.printf("%1$tF %1$ta%n", date);
             
              // 输出时间日期的完整信息
              System.out.printf("%1$tc%n", date);
       }
}
/**
 *printf方法中,格式为"%s"表示以字符串的形式输出第二个可变长参数的第一个参数值;
 *格式为"%n"表示换行;格式为"%S"表示将字符串以大写形式输出;在"%s"之间用"n$"表示
 *输出可变长参数的第n个参数值.格式为"%b"表示以布尔值的形式输出第二个可变长参数
 *的第一个参数值.
 */
/**
 * 格式为"%d"表示以十进制整数形式输出;"%o"表示以八进制形式输出;"%x"表示以十六进制
 * 输出;"%X"表示以十六进制输出,并且将字母(A、B、C、D、E、F)换成大写.格式为"%e"表
 * 以科学计数法输出浮点数;格式为"%E"表示以科学计数法输出浮点数,而且将e大写;格式为
 * "%f"表示以十进制浮点数输出,在"%f"之间加上".n"表示输出时保留小数点后面n位.
 */
/**
 * 格式为"%t"表示输出时间日期类型."%t"之后用y表示输出日期的二位数的年份(如99)、用m
 * 表示输出日期的月份,用d表示输出日期的日号;"%t"之后用Y表示输出日期的四位数的年份
 * (如1999)、用B表示输出日期的月份的完整名,用b表示输出日期的月份的简称."%t"之后用D
 * 表示以"%tm/%td/%ty"的格式输出日期、用F表示以"%tY-%tm-%td"的格式输出日期.
 */
/**
 * "%t"之后用H表示输出时间的时(24进制),用I表示输出时间的时(12进制),用M表示输出时间
 * 分,用S表示输出时间的秒,用L表示输出时间的秒中的毫秒数、用 p 表示输出时间的是上午还是
 * 下午."%t"之后用R表示以"%tH:%tM"的格式输出时间、用T表示以"%tH:%tM:%tS"的格式输出
 * 时间、用r表示以"%tI:%tM:%tS %Tp"的格式输出时间.
 */
/**
 * "%t"之后用A表示输出日期的全称,用a表示输出日期的星期简称.
 */
```

***

# String

## 构造

```java
// String 类有 11 种构造方法
// 用构造函数创建字符串：
String str =new String("Runoob");
// 使用关键字：
String str2 = "Runoob";
// 使用字符数组：
char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
String helloString = new String(helloArray);  // runoob
// 。。。。。。
```

String 创建的字符串存储在公共池中，而 new 创建的字符串对象在堆上：

```java
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建
```

<img src="https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png" alt="https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png" style="zoom:67%;" />

**注意**：String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了。如果需要对字符串做很多修改，那么应该选择使用 [StringBuffer & StringBuilder 类](https://www.runoob.com/java/java-stringbuffer.html)。

## 字符串长度

String 类的一个访问器方法是 length() 方法，它返回字符串对象包含的字符数。

```java
String site = "runoob";
int len = site.length();
// len = 6
```

## 连接字符串

```java
string1.concat(string2);
"Hello," + " runoob" + "!"
```

## 创建格式化字符串

我们知道输出格式化数字可以使用 printf() 和 format() 方法。

String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

```java
System.out.printf("浮点型变量的值为 " + "%f, 整型变量的值为 " + " %d, 字符串变量的值为 " + "is %s", floatVar, intVar, stringVar);
// 或
String fs;
fs = String.format("浮点型变量的值为 " + "%f, 整型变量的值为 " + " %d, 字符串变量的值为 " + " %s", floatVar, intVar, stringVar);
```

## String 方法

参考文档：[https://www.runoob.com/manual/jdk11api/java.base/java/lang/String.html](https://www.runoob.com/manual/jdk11api/java.base/java/lang/String.html)

***

# StringBuffer 和 StringBuilder

当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

<img src="https://www.runoob.com/wp-content/uploads/2013/12/java-string-20201208.png" alt="https://www.runoob.com/wp-content/uploads/2013/12/java-string-20201208.png" style="zoom: 50%;" />

在使用 StringBuffer 类时，每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象，所以如果需要对字符串进行修改推荐使用 StringBuffer。

## StringBuilder 

StringBuilder 类在 Java 5 中被提出，StringBuilder 的方法不是线程安全的。

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下**建议使用 StringBuilder 类**。

StringBuilder 常用方法：[https://www.runoob.com/manual/jdk11api/java.base/java/lang/StringBuilder.html](https://www.runoob.com/manual/jdk11api/java.base/java/lang/StringBuilder.html)

```java
StringBuilder sb = new StringBuilder(10);
sb.append("Runoob..");
System.out.println(sb); // Runoob..
sb.append("!");
System.out.println(sb); // Runoob..!
sb.insert(8, "Java");
System.out.println(sb); // Runoob..Java!
sb.delete(5,8);
System.out.println(sb); // RunooJava!
```

<img src="https://www.runoob.com/wp-content/uploads/2013/12/2021-03-01-java-stringbuffer.svg" alt="https://www.runoob.com/wp-content/uploads/2013/12/2021-03-01-java-stringbuffer.svg" style="zoom:50%;" />

## StringBuffer

然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

```java
StringBuffer sBuffer = new StringBuffer("www");
sBuffer.append(".runoob");
sBuffer.append(".com");
System.out.println(sBuffer); // www.runoob.com
```

 StringBuffer 常用方法：

| 方法                                        | 描述                                                     |
| ------------------------------------------- | -------------------------------------------------------- |
| ``public StringBuffer append(String s)``    | 将指定的字符串追加到此字符序列。                         |
| ``public StringBuffer reverse()``           | 将此字符序列用其反转形式取代。                           |
| ``public delete(int start, int end)``       | 移除此序列的子字符串中的字符。                           |
| ``public insert(int offset, int i)``        | 将 `int` 参数的字符串表示形式插入此序列中。              |
| ``insert(int offset, String str)``          | 将 `str` 参数的字符串插入此序列中。                      |
| ``replace(int start, int end, String str)`` | 使用给定 `String` 中的字符替换此序列的子字符串中的字符。 |

StringBuffer 其他方法：https://www.runoob.com/manual/jdk11api/java.base/java/lang/StringBuffer.html

***

# 日期时间

java.util 包提供了 Date 类来封装当前的日期和时间。 Date 类提供两个构造函数来实例化 Date 对象。

```java
// 使用当前日期和时间来初始化对象
Date( )
// 接收一个参数，该参数是从 1970 年 1 月 1 日起的毫秒数
Date(long millisec)
```

Date 对象创建以后，可以调用下面的方法：

| 方法                            | **描述**                                                     |
| ------------------------------- | ------------------------------------------------------------ |
| ``boolean after(Date date)``    | 若当调用此方法的Date对象在指定日期之后返回true,否则返回false。同样的还有方法 ``before(Date)`` |
| ``long getTime( )``             | 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
| ``boolean equals(Object date)`` | 当调用此方法的Date对象和指定日期相等时候返回true,否则返回false。 |
| ``void setTime(long time)``     | 用自1970年1月1日00:00:00 GMT以后time毫秒数设置时间和日期。   |
| ``String toString( )``          | String： dow mon dd hh:mm:ss zzz yyyy  [dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)] |

## 获取当前日期时间

```java
Date date = new Date(); // 初始化 Date 对象
System.out.println(date.toString()); // Mon May 04 09:51:52 CDT 2013
```

## 日期比较

Java使用以下三种方法来比较两个日期：

- 使用 getTime() 方法获取两个日期（自1970年1月1日经历的毫秒数值），然后比较这两个值。
- 使用方法 before()，after() 和 equals()。例如，一个月的12号比18号早，则 new Date(99, 2, 12).before(new Date (99, 2, 18)) 返回true。
- 使用 compareTo() 方法，它是由 Comparable 接口定义的，Date 类实现了这个接口。

## SimpleDateFormat 格式化日期

```java
Date dNow = new Date( );
SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
System.out.println(ft.format(dNow)); // 2018-09-06 10:16:34
SimpleDateFormat ft2 =  new SimpleDateFormat ("E yyyy.MM.dd 'at' hh:mm:ss a zzz");
System.out.println(ft2.format(dNow)); // Wed 2016.11.09 at 08:23:19 AM UTC
```

## printf格式化日期

printf 方法可以很轻松地格式化时间和日期。使用两个字母格式，它以 **%t** 开头并且以下面表格中的一个字母结尾。

```java
Date date = new Date(); // 初始化 Date 对象
// c 的使用  
System.out.printf("全部日期和时间信息：%tc%n",date); // 全部日期和时间信息：星期一 九月 10 10:43:36 CST 2012
// F 的使用  
System.out.printf("年-月-日格式：%tF%n",date); // 年-月-日格式：2012-09-10
// D 的使用  
System.out.printf("月/日/年格式：%tD%n",date); // 月/日/年格式：09/10/12
// r 的使用  
System.out.printf("HH:MM:SS PM格式（12时制）：%tr%n",date); // HH:MM:SS PM格式（12时制）：10:43:36 上午
// T 的使用  
System.out.printf("HH:MM:SS格式（24时制）：%tT%n",date); // HH:MM:SS格式（24时制）：10:43:36
// R 的使用  
System.out.printf("HH:MM格式（24时制）：%tR",date); // HH:MM格式（24时制）：10:43
```

***

# 流(Stream)、文件(File)和IO

<img src="https://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png" alt="https://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png" style="zoom: 67%;" />

## FileInputStream

```java
File f = new File("C:/java/hello");
InputStream in = new FileInputStream(f);
```

创建的 InputStream对象，常见方法：

| **方法**                                           | **描述**                                                     |
| -------------------------------------------------- | ------------------------------------------------------------ |
| ``public void close() throws IOException{}``       | 关闭此文件输入流并释放与此流有关的所有系统资源。             |
| ``protected void finalize()throws IOException {}`` | 这个方法清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。 |
| ``public int read(int r)throws IOException{}``     | ** public int read(int r)throws IOException{}** 这个方法从 InputStream 对象读取指定字节的数据。返回为整数值。返回下一字节数据，如果已经到结尾则返回-1。 |
| ``public int read(byte[] r) throws IOException{}`` | 这个方法从输入流读取r.length长度的字节。返回读取的字节数。如果是文件结尾则返回-1。 |
| ``public int available() throws IOException{}``    | 返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取的字节数。返回一个整数值。 |

## FileOutputStream

该类用来创建一个文件并向文件中写数据。如果该流在打开文件进行输出前，目标文件不存在，那么该流会创建该文件。

有两个构造方法可以用来创建 FileOutputStream 对象：

```java
// 使用字符串类型的文件名来创建一个输出流对象：
OutputStream f = new FileOutputStream("C:/java/hello")
// 使用一个文件对象来创建一个输出流来写文件：
File f = new File("C:/java/hello");
OutputStream fOut = new FileOutputStream(f);
```

创建的 OutputStream 对象常用方法：

| 方法                                               | 描述                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| ``public void close() throws IOException{}``       | 关闭此文件输入流并释放与此流有关的所有系统资源。             |
| ``protected void finalize()throws IOException {}`` | 清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。 |
| ``public void write(int w)throws IOException{}``   | 把指定的字节写到输出流中。                                   |
| ``public void write(byte[] w)``                    | 把指定数组中w.length长度的字节写到OutputStream中。           |

下面是一个演示 InputStream 和 OutputStream 用法的例子：

```java
try {
    byte bWrite[] = { 11, 21, 3, 40, 5 };
    OutputStream os = new FileOutputStream("test.txt");
    for (int x = 0; x < bWrite.length; x++) {
        os.write(bWrite[x]); // writes the bytes
    }
    os.close();

    InputStream is = new FileInputStream("test.txt");
    for (int i = 0; i < is.available(); i++) {
        System.out.print((char) is.read() + "  ");
    }
    is.close();
    
} catch (IOException e) {
    System.out.print("Exception");
}
```

## 文件和I/O

### 创建目录：

File类中有两个方法可以用来创建文件夹：

- **mkdir( )**方法创建一个文件夹，成功则返回true，失败则返回false。失败表明File对象指定的路径已经存在，或者由于整个路径还不存在，该文件夹不能被创建。
- **mkdirs()**方法创建一个文件夹和它的所有父文件夹。

如果创建一个 File 对象并且它是一个目录，那么调用 ``isDirectory() ``方法会返回 true。

通过调用该对象上的 ``list()`` 方法，来提取它包含的文件和文件夹的列表。

### 删除目录或文件

删除文件可以使用 **java.io.File.delete()** 方法。当删除某一目录时，必须保证该目录下没有其他文件才能正确删除，否则将删除失败。

测试目录结构：

```shell
/tmp/java/
|-- 1.log
|-- test
```

```java
public static void main(String[] args) {
    // 这里修改为自己的测试目录
    File folder = new File("/tmp/java/");
    deleteFolder(folder);
}

// 删除文件及目录
public static void deleteFolder(File folder) {
    File[] files = folder.listFiles();
    if (files != null) {
        for (File f : files) {
            if (f.isDirectory()) {
                deleteFolder(f);
            } else {
                f.delete();
            }
        }
    }
    folder.delete();
}
```

***

# 集合框架

https://www.runoob.com/java/java-collections.html











