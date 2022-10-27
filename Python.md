# 单行注释与多行注释

单行注释用```#```-->一个井号，vacode快捷键```ctrl+/```

多行注释用```"""```-->三个双引号，vacode快捷键```ctrl+shift+/```

```python
print('hello python') #现在这个是单行注释
"""这个是多行注释
print('hello python')
print('hello python')
"""
```

---



# 输入输出



## 输入

使用`input`函数可以获得用户输入在控制台窗口上输入的**一行**的**字符串**，使用`变量 = input()`的形式将其赋值给一个变量：

```python
str1 = input()
print("输入的是%s" % str1)
```

![image-20220902234950887](C:\Users\31330\Pictures\Typora\image-20220902234950887.png)

还可以在`input()`的括号内，加入一些提示信息：

```python
str1=input("请输入:")
print("输入的是%s" % str1)
```

![](C:\Users\31330\Pictures\Typora\8-16621340604561.gif)

还可以一次输入多个值：

```python
a,b=input().split() #字符串，split() 不加参数表示默认空格隔开
```

指定输入类型：

```python
a=int(input())
b=float(input())
```



---



## 输出

### `print`的函数

将要输出的内容放在`print()`的括号内，就可以输出：

```python
print("hello world") #单引号包裹也是可行的
#控制台打印：hello world
```

`print`函数可以同时输出多个内容，只需要将它一起放在`print`的括号内，并用逗号隔开：

```python
print("hello","world")
#控制台打印：hello world
```

==注意==：此时同时输出的多个内容之间，会有**空格**隔开。

类似于 C/C++ 的`printf`，Python 的`print`也能实现格式化输出，方法是使用`%`操作符，它会将左边的字符串当做**格式字符串**，将右边的参数代入格式字符串：

```python
print("1 + 1 = %d" % 2) 
#2会替换掉 %d 。控制台输出：1 + 1 = 2
print("hello %s" % "world")
#左边 %s 被替换成右边的 world 。控制台输出：hello world
```

一般不用担心占位格式字符由于代码多肉眼难以区分和查看的问题，一般的编译器会带高亮提示。例如：博主用的 vsCode：

（我vsCode使用了主题，所以可能和大众的代码颜色不同）

![image-20220903000459990](C:\Users\31330\Pictures\Typora\image-20220903000459990.png)

如果要带入多个参数，则需要用`()`包裹代入的多个参数，参数与参数之间用逗号隔开。

==注意==：**参数的顺序应该对应格式字符串中的顺序**：

```python
print("%d + %d = %d" % (1,1,2))
#控制台打印：1 + 1 = 2
print("%s %s" % ("world","hello"))
#控制台打印：world hello
```

### 格式化输出

通过`format()`方法将待输出变量整理成期望输出的格式，如：

```python
name=input("请输入姓名：")
country=input("请输入国家：")
print("{}来自{}".format(name,country))
# 控制台输出：张三来自中国
```



### 格式字符串（占位符）

格式字符串中，不同**占位符**的含义：

| 占位符 | 表示                                     |
| :----: | ---------------------------------------- |
|   %s   | 作为字符串                               |
|   %d   | 作为有符号十进制整数                     |
|   %u   | 作为无符号十进制整数                     |
|   %o   | 作为无符号八进制整数                     |
|   %x   | 作为无符号十六进制整数，a～f采用小写形式 |
|   %X   | 作为无符号十六进制整数，A～F采用大写形式 |
|   %f   | 作为浮点数                               |
| %e，%E | 作为浮点数，使用科学计数法               |
| %g，%G | 作为浮点数，使用最低有效数位             |

**注意:** `print`函数输出数据后会换行，如果不想换行，需要指定```end=""```：

```python
print("hello" , end="")
print("world" , end="")
#控制台输出helloworld
```

### 字符串转换

`input`函数接收的是用户控制台输入的**字符串**，此时还不能作为整数或者小数进行数学运算，需要使用函数将字符串转换成想要的类型。

- 转换成整数，使用`int()`函数：`num1 = int(str1)`
- 转换成小数，使用`float()`函数：`f1 = float(str1)`

```python
str1 = input()
num1 = int(str1)
f1 = float(str1)
print("整数%d,小数%f" % (num1,f1))
#控制台输入：114514
#控制台输出：整数114514,小数114514.000000
```

如果输入10，得到的输出是：`整数10,小数10.000000`。

***

# 数据类型

## 常用数据类型 Common Data Types

|     类型     |     例子      |
| :----------: | :-----------: |
|   整型 int   |    `-100`     |
| 浮点型 float |   `3.1416`    |
| 复数 complex |    `2+3j`     |
|    字符串    |   `'hello'`   |
|  布尔 bool   | `True, False` |

使用`type()`函数来查看变量类型：

```python
a=12
type(a) # int
```

### 整型

> 整型数字的最大最小值：
>
> 在 32 位系统中，一个整型 4 个字节，最小值 `-2,147,483,648`，最大值 `2,147,483,647`。
>
> 在 64 位系统中，一个整型 8 个字节，最小值 `-9,223,372,036,854,775,808`，最大值 `9,223,372,036,854,775,807`。
>
> ```python
> import sys
> print(sys.maxsize)
> # 9223372036854775807
> ```

除了10进制外，整数还有其他类型的表示方法。

科学计数法：1e-6

16进制，前面加`0x`修饰，后面使用数字0-9A-F：0xFF

8进制，前面加`0`或者`0o`修饰，后面使用数字0-7：067

2进制，前面加`0b`修饰，后面使用数字0或1：0b101010

### 浮点型

```python
# %f格式化浮点数字，可指定小数后精度
print("%.2f" % (2.5 % 1.2)) 
# 0.10
```

可以用`sys.float_info`来查看浮点数的信息：

```python
import sys
print(sys.float_info)
# sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)
```

例如浮点数能表示的最大值：

``sys.float_info.max``

浮点数能表示的最接近0的值：

``sys.float_info.min``

浮点数的精度：

``sys.float_info.epsilon``

### 复数 Complex Numbers

**Python** 使用 `j` 来表示复数的虚部：

可以查看它的实部，虚部以及共轭：

``a.real``

``a.imag``

``a.conjugate()``

### 布尔型 Boolean Data Type

**为0的数字，包括0,0.0；空字符串' '，""；表示空值的None；空集合，包括空元祖(),空序列[],空字典{} 都认为是False ；其他的值都为True。**

```python
运算时：False —— 0    True —— 1
```

### Python字符串

Python 语言中，字符串是用两个双引号``"example"``或者单引号``'example'``括起来的零个或多个字符。**Pyton 不支持字符类型，单个字符当做字符串使用**

简单操作：

```python
# 加法
s = 'hello ' + 'world' # 'hello world'
#字符串与数字相乘：
"&" * 10 # '&&&&&&&&&&'
#字符串长度：
len(s) # 11
```

字符串方法：

查找``.find()``返回的是下标

```python
source_string = 'The past is gone and static'
# 查看"past"在source_string字符串中的位置
print(source_string.find('past')) # 4
# 查看"love"在source_string字符串中的位置
print(source_string.find('love')) # -1
```

1.分割 split()

``s.split()``将s按照空格（包括多个空格，制表符`\t`，换行符`\n`等）分割，并返回所有分割得到的字符串。

```python
line = '1 2 3 4 5'
numbers = line.split()
print(numbers)
# ['1', '2', '3', '4', '5']
```

2.连接 join()

``s.join(str_sequence)``的作用是**以s为连接符**将字符串序列str_sequence中的元素连接起来，并返回连接后**得到的新字符串**。

```python
numbers = ['1', '2', '3', '4', '5']
s = ' '
s.join(numbers)
# '1 2 3 4 5'得到的是新字符串
```

3.替换  replace()

``s.replace(part1, part2)``将字符串s中指定的部分part1替换成想要的部分part2，并返回新的字符串。

```python
s = "hello world" 
print(s.replace('world', 'python') )  #此时，s的值并没有变化，替换方法只是生成了一个新的字符串。
print(s)
# 控制台顺序输出：
# hello python
# hello world
```

4.大小写转换

``s.upper()``方法返回一个将s中的字母全部大写的新字符串。

``s.lower()``方法返回一个将s中的字母全部小写的新字符串。

``s.title()``方法返回一个将s中单词的首字符大写的新串。

5.去除多余空格

``s.strip()``返回一个将s两端的多余空格除去的新字符串。

``s.lstrip()``返回一个将s开头的多余空格除去的新字符串。

``s.rstrip()``返回一个将s结尾的多余空格除去的新字符串。

字符串是字符的序列，可以按照单个字符或字符片段进行索引，字符串包括两种序号体系：正向递增序号和反向递减序号。

![image-20220908214625279](C:\Users\31330\Pictures\Typora\image-20220908214625279.png)

Python 字符串也可以采用`[N:M]`区间格式获取指定字符串。

表示字符串中从`N`到`M`（不包含`M`，包左不包右）的子字符串，其中，`N`和`M`为字符串的索引序号，可以混合使用正向递增序号和反向递减序号。如果表示中`N`或者`M`索引缺失，则表示字符串把开始或结束索引值设为默认值。

```python
>>>name="Python语言程序设计"
>>>name[0]
'P'
>>>print(name[0],name[7],name[-1])
P 言 计
>>>print(name[2:-4])
thon语言
>>>print(name[:6])
Python
>>>print(name[6:])
语言程序设计
>>>print(name[:])
Python语言程序设计
```

```python
str = "abcdefghijklmnopqrstuvwxyz"
print(str[::-1])
print(str[::3])
print(str[2:5:2])
print(str[-3:-6:-1])
print(str[::2])#偶数
print(str[1::2])#奇数
print(str[:])
# zyxwvutsrqponmlkjihgfedcba
# adgjmpsvy
# ce
# xwv
# acegikmoqsuwy
# bdfhjlnprtvxz
# abcdefghijklmnopqrstuvwxyz
```



### 类型转换

浮点数转整型，只保留整数部分：

```python
int(12.324)
int(-3.32)
```

整型转浮点型：

```python
float(1) # 1.0
```

进制转换：

```python
# 十进制转换为八进制：
x=20
oct(x) # 0o24
# 十进制转换为二进制字符串：
bin(x) # '0b10100'
# 十进制转换为十六进制字符串：
hex(x) # '0x14'
```

将对象x转换为字符串：

```python
str(1) # '1'
```

``eval()`` 将字符串 string 对象 转化为有效的表达式参与求值运算返回计算结果：

```python
eval('1+x') 
```

可以使用 `int` 将字符串转为整数，还可以指定按照多少进制来进行转换，最后返回十进制表达的整数：

```python
int('23') # 23
int('10',2) # 2
```

`float` 可以将字符串转换为浮点数：

```python
float('3.5')
```

强制转换为字符串

- `str(ob)`强制将`ob`转化成字符串。
- `repr(ob)`也是强制将`ob`转化成字符串。

## 其他类型 Others

|     类型      |           例子           |
| :-----------: | :----------------------: |
| 列表（list）  |   `[1, 1.2, 'hello']`    |
| 字典（dict）  | `{'dogs': 5, 'pigs': 3}` |
| 元组（tuple） |     `('ring', 1000)`     |
|  集合（set）  |       `{1, 2, 3}`        |





|                  | **列表（list）**                                             | **元组（tuple）**                                            | **集合（set）**                                              | **字典（dict）**                                             |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Definition       | \- 有索引（indexed）<br/>\- 有序<br/>\- 可修改<br/>\- 允许重复值存在<br/>\- 允许使用不同的数据类型 | \- 有索引（indexed）<br/>\- 有序<br/>\- 不可修改<br/>\- 允许重复值存在<br/>\- 允许使用不同的数据类型 | \- 没有索引（not indexed）<br/>\- 无序<br/>\- 可修改<br/>\- 不允许重复值存在<br/>\- 允许使用不同的数据类型 | \- 没有索引（有`key`）<br/>\- 有序<br/>\- 可修改<br/>\- 不允许重复值存在<br/>\- 允许使用不同的数据类型 |
| 新建             | ``my_list=["apple", "pen"]``                                 | ``my_tpl=("apple", "pen")``                                  | ``my_set={"apple", "pen"}``空集合：``my_set=set()``          | ``my_dict={"my_fruit": "apple",` `"my_thing":"pen"}``        |
| 第一个元素       | ``my_list[0]``                                               | ``my_tpl[0]``                                                | ``-``                                                        | ``my_dict["my_fruit"]``<br/>                                 |
| 某个范围内的元素 | ``my_list[0:2]``                                             | ``my_tpl[0:2]``                                              | ``只能通过for循环``                                          | ``-``                                                        |
| 检查是否存在     | ``if "apple" in my_list...``                                 | ``if "apple" in my_tpl``                                     | ``if "apple" in my_set``                                     | ``if "my_fruit" in my_dict``                                 |
| 更新元素         | ``my_list[1]="cherry"``                                      | ``my_tpl[1]="cherry"``                                       | ``-``                                                        | ``	my_dict["my_fruit"]="cherry"``                         |
| 添加更多元素     | ``my_list.append("orange")``                                 | ``my_tpl+=("orange",)``                                      | ``my_set.add("orange")``<br/>                                |                                                              |
| 删除某个元素     | ``my_list.remove("orange")``                                 | ``-``                                                        | ``my_set.remove("orange")``                                  | ``my_dict.pop("sex")``                                       |
| 其他             |                                                              |                                                              |                                                              |                                                              |



#  运算符

## 简单的数学函数

绝对值：

abs(-12.4)

取整：

round(21.6)

round(21.63,1)

最大最小值：

min(2, 3, 4, 5) max(2, 4, 3)







## （1）算术运算符 

![image-20220910113309383](C:\Users\31330\Pictures\Typora\image-20220910113309383.png)

整数除法，返回的是比结果`小`的最大整数值：

```python
12.3 // -4
# -4.0
```



## （2）关系运算符 

![image-20220910113400511](C:\Users\31330\Pictures\Typora\image-20220910113400511.png)

## （3）逻辑运算符 

![image-20220910113433029](C:\Users\31330\Pictures\Typora\image-20220910113433029.png)

## （4）位运算符 

按位运算符是把数字看作**二进制**来进行计算的。

例如，下方变量 a 为 60，b 为 13：

```python
a   = 0011 1100 # 60
b   = 0000 1101 # 13
# -----------------
a&b = 0000 1100
a|b = 0011 1101
a^b = 0011 0001
~a  = 1100 0011
```

![image-20220910113619562](C:\Users\31330\Pictures\Typora\image-20220910113619562.png)

## （5）赋值运算符 

![image-20220910114048943](C:\Users\31330\Pictures\Typora\image-20220910114048943.png)

## （6）成员运算符 

![image-20220910114142966](C:\Users\31330\Pictures\Typora\image-20220910114142966.png)

## （7）身份运算符

以下实例演示了Python所有身份运算符的操作：

```python
a = 20
b = 20
if ( a is b ):
   print ("1 - a 和 b 有相同的标识") # ✔️
else:
   print ("1 - a 和 b 没有相同的标识")
if ( id(a) == id(b) ):
   print ("2 - a 和 b 有相同的标识") # ✔️
else:
   print ("2 - a 和 b 没有相同的标识")
# 修改变量 b 的值
b = 30
if ( a is b ):
   print ("3 - a 和 b 有相同的标识")
else:
   print ("3 - a 和 b 没有相同的标识") # ✔️
if ( a is not b ):
   print ("4 - a 和 b 没有相同的标识") # ✔️
else:
   print ("4 - a 和 b 有相同的标识")
```

控制台输出：

```shell
1 - a 和 b 有相同的标识
2 - a 和 b 有相同的标识
3 - a 和 b 没有相同的标识
4 - a 和 b 没有相同的标识
```

> is 与 == 区别：
>
> is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。
>
> ```python
> >>>a = [1, 2, 3]
> >>> b = a
> >>> b is a 
> # True
> >>> b == a
> # True
> >>> b = a[:]
> >>> b is a
> # False
> >>> b == a
> # True
> ```

