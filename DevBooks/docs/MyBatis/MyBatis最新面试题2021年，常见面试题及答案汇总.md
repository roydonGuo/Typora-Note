# MyBatis最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、SQLMapConfig.xml中配置有哪些内容？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#1sqlmapconfigxml中配置有哪些内容)  


properties（属性） settings（配置） typeAliases（类型别名） typeHandlers（类型处理器） objectFactory（对象工厂） plugins（插件） environments（环境集合属性对象） environment（环境子属性对象） transactionManager（事务管理） dataSource（数据源） mappers（映射器）


### [2、为什么说Mybatis是半自动ORM映射工具？它与全自动的区别在哪里？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#2为什么说mybatis是半自动orm映射工具它与全自动的区别在哪里)  


Hibernate属于全自动ORM映射工具，使用Hibernate查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取，所以它是全自动的。而Mybatis在查询关联对象或关联集合对象时，需要手动编写sql来完成，所以，称之为半自动ORM映射工具。


### [3、通常一个Xml映射文件，都会写一个Dao接口与之对应](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#3通常一个xml映射文件都会写一个dao接口与之对应)  


**请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？**

Dao接口即Mapper接口。接口的全限名，就是映射文件中的namespace的值；接口的方法名，就是映射文件中Mapper的Statement的id值；接口方法内的参数，就是传递给sql的参数。

Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MapperStatement。在Mybatis中，每一个`<select>、<insert>、<update>、<delete>`标签，都会被解析为一个MapperStatement对象。

**举例：**

`com.mybatis3.mappers.StudentDao.findStudentById`，可以唯一找到namespace为`com.mybatis3.mappers.StudentDao`下面 id 为 findStudentById 的 MapperStatement。

Mapper接口里的方法，是不能重载的，因为是使用 全限名+方法名 的保存和寻找策略。Mapper 接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Mapper接口生成代理对象proxy，代理对象会拦截接口方法，转而执行MapperStatement所代表的sql，然后将sql执行结果返回。


### [4、Mybatis 映射文件中，如果 A 标签通过 include 引用了 B 标签的内容，请问，B 标签能](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#4mybatis-映射文件中如果-a-标签通过-include-引用了-b-标签的内容请问b-标签能)  


否定义在 A 标签的后面，还是说必须定义在 A 标签的前面？

虽然 Mybatis 解析 Xml 映射文件是按照顺序解析的，但是，被引用的 B 标签依然可以

定义在任何地方，Mybatis 都可以正确识别。原理是，Mybatis 解析 A 标签，发现 A 标签引

用了 B 标签，但是 B 标签尚未解析到，尚不存在，此时，Mybatis 会将 A 标签标记为未解

析状态，然后继续解析余下的标签，包含 B 标签，待所有标签解析完毕，Mybatis 会重新

解析那些被标记为未解析的标签，此时再解析 A 标签时，B 标签已经存在，A 标签也就可

以正常解析完成了。


### [5、Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#5mybatis的xml映射文件中不同的xml映射文件id是否可以重复)  


不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复；毕竟namespace不是必须的，只是最佳实践而已。

原因就是namespace+id是作为Map<String, MappedStatement>的key使用的，如果没有namespace，就剩下id，那么，id重复会导致数据互相覆盖。有了namespace，自然id就可以重复，namespace不同，namespace+id自然也就不同。


### [6、请说说MyBatis的工作原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#6请说说mybatis的工作原理)  


在学习 MyBatis 程序之前，需要了解一下 MyBatis 工作原理，以便于理解程序。MyBatis 的工作原理如下图 ![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/041/14/55_1.png#alt=55%5C_1.png)

**1、** 读取 MyBatis 配置文件：mybatis-config.xml 为 MyBatis 的全局配置文件，配置了 MyBatis 的运行环境等信息，例如数据库连接信息。

**2、** 加载映射文件。映射文件即 SQL 映射文件，该文件中配置了操作数据库的 SQL 语句，需要在 MyBatis 配置文件 mybatis-config.xml 中加载。mybatis-config.xml 文件可以加载多个映射文件，每个文件对应数据库中的一张表。

**3、** 构造会话工厂：通过 MyBatis 的环境等配置信息构建会话工厂 SqlSessionFactory。

**4、** 创建会话对象：由会话工厂创建 SqlSession 对象，该对象中包含了执行 SQL 语句的所有方法。

**5、** Executor 执行器：MyBatis 底层定义了一个 Executor 接口来操作数据库，它将根据 SqlSession 传递的参数动态地生成需要执行的 SQL 语句，同时负责查询缓存的维护。

**6、** MappedStatement 对象：在 Executor 接口的执行方法中有一个 MappedStatement 类型的参数，该参数是对映射信息的封装，用于存储要映射的 SQL 语句的 id、参数等信息。

**7、** 输入参数映射：输入参数类型可以是 Map、List 等集合类型，也可以是基本数据类型和 POJO 类型。输入参数映射过程类似于 JDBC 对 preparedStatement 对象设置参数的过程。

**8、** 输出结果映射：输出结果类型可以是 Map、 List 等集合类型，也可以是基本数据类型和 POJO 类型。输出结果映射过程类似于 JDBC 对结果集的解析过程。


### [7、Mybatis都有哪些Executor执行器？它们之间的区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#7mybatis都有哪些executor执行器它们之间的区别是什么)  


Mybatis有三种基本的Executor执行器，SimpleExecutor、ReuseExecutor、BatchExecutor。

**SimpleExecutor**：

每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。

**ReuseExecutor**：

执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map<String, Statement>内，供下一次使用。简言之，就是重复使用Statement对象。

**BatchExecutor**：

执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。与JDBC批处理相同。

作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。


### [8、简述 Mybatis 的 Xml 映射文件和 Mybatis 内部数据结构之间的映射关系？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#8简述-mybatis-的-xml-映射文件和-mybatis-内部数据结构之间的映射关系)  


Mybatis 将所有 Xml 配置信息都封装到 All-In-One 重量级对象 Configuration 内部。在

Xml 映射文件中，标签会被解析为 ParameterMap 对象，其每个子元素会

被解析为 ParameterMapping 对象。标签会被解析为 ResultMap 对象，其每个子

元素会被解析为 ResultMapping 对象。每一个、、、标签

均会被解析为 MappedStatement 对象，标签内的 sql 会被解析为 BoundSql 对象。


### [9、Mybatis动态sql是做什么的？都有哪些动态sql？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#9mybatis动态sql是做什么的都有哪些动态sql)  


**能简述一下动态sql的执行原理吗？**

Mybatis动态sql可以让我们在Xml映射文件内，以标签的形式编写动态sql，完成逻辑判断和动态拼接sql的功能，Mybatis提供了9种动态sql标签trim|where|set|foreach|if|choose|when|otherwise|bind。

其执行原理为，使用OGNL从sql参数对象中计算表达式的值，根据表达式的值动态拼接sql，以此来完成动态sql的功能。


### [10、MyBatis与hibernate有哪些不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题2021年，常见面试题及答案汇总.md#10mybatis与hibernate有哪些不同)  


**1、** Mybatis MyBatis 是支持定制化 SQL、存储过程以及高级映射的一种持久层框架。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。Mybatis它不完全是一个ORM(对象关系映射)框架；它需要程序员自己编写部分SQL语句。 mybatis可以通过xml或者注解的方式灵活的配置要运行的SQL语句，并将java对象和SQL语句映射生成最终的执行的SQL，最后将SQL执行的结果在映射生成java对象。 Mybatis程序员可以直接的编写原生态的SQL语句，可以控制SQL执行性能，灵活度高，适合软件需求变换频繁的企业。 缺点：Mybatis无法做到数据库无关性，如果需要实现支持多种数据库的软件，则需要自定义多套SQL映射文件，工作量大。

**2、** Hibernate Hibernate是支持定制化 SQL、存储过程以及高级映射的一种持久层框架。 Hibernate对象-关系映射能力强，数据库的无关性好，Hirberate可以自动生成SQL语句，对于关系模型要求高的软件，如果用HIrbernate开发可以节省很多时间。


### 11、通常一个 Xml 映射文件，都会写一个 Dao 接口与之对应, Dao 的工作原理，是否可以重
### 12、一对一、一对多的关联查询 ？
### 13、这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗
### 14、JDBC编程有哪些不足之处，Mybatis是如何解决这些问题的？
### 15、Mybatis 执行批量插入，能返回数据库主键列表吗？
### 16、MyBatis框架的缺点有什么？
### 17、IBatis 和 MyBatis 在细节上的不同有哪些？
### 18、MyBatis和Hibernate的适用场景?
### 19、MyBatis 与 Hibernate 有哪些不同？
### 20、Mybatis如何执行批量操作
### 21、Mybatis是如何进行分页的？分页插件的原理是什么？
### 22、什么是Mybatis？
### 23、Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？
### 24、Mybatis 中如何执行批处理？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




