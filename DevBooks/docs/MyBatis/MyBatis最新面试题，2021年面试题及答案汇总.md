# MyBatis最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是 MyBatis？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#1什么是-mybatis)  


MyBatis 是一个可以自定义 SQL、存储过程和高级映射的持久层框架。


### [2、当实体类中的属性名和表中的字段名不一样 ，怎么办 ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#2当实体类中的属性名和表中的字段名不一样-怎么办-)  


第1种： 通过在查询的sql语句中定义字段名的别名，让字段名的别名和实体类的属性名一致。

```
<select id=”selectorder” parametertype=”int” resultetype=”me.gacl.domain.order”>
       select order_id id, order_no orderno ,order_price price form orders where order_id=#{id};
</select>
```

第2种： 通过`<resultMap>`来映射字段名和实体类属性名的一一对应的关系。

```
<select id="getOrder" parameterType="int" resultMap="orderresultmap">
select * from orders where order_id=#{id}
</select>

<resultMap type=”me.gacl.domain.order” id=”orderresultmap”>
    <!–用id属性来映射主键字段–>
    <id property=”id” column=”order_id”>

    <!–用result属性来映射非主键字段，property为实体类属性名，column为数据表中的属性–>
    <result property = “orderno” column =”order_no”/>
    <result property=”price” column=”order_price” />
</reslutMap>
```


### [3、Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#3mybatis是如何将sql执行结果封装为目标对象并返回的都有哪些映射形式)  


第一种是使用`<resultMap>`标签，逐一定义数据库列名和对象属性名之间的映射关系。

第二种是使用sql列的别名功能，将列的别名书写为对象属性名。

有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。


### [4、当实体类中的属性名和表中的字段名不一样 ，怎么办](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#4当实体类中的属性名和表中的字段名不一样-怎么办)  


第1种： 通过在查询的SQL语句中定义字段名的别名，让字段名的别名和实体类的属性名一致。

```
<select id="getOrder" parameterType="int" resultType="com.jourwon.pojo.Order">
       select order_id id, order_no orderno ,order_price price form orders where order_id=#{id};
</select>
```

第2种： 通过`<resultMap>`来映射字段名和实体类属性名的一一对应的关系。

```
<select id="getOrder" parameterType="int" resultMap="orderResultMap">
    select * from orders where order_id=#{id}
</select>
    
<resultMap type="com.jourwon.pojo.Order" id="orderResultMap">
    <!–用id属性来映射主键字段–>
    <id property="id" column="order_id">
    
    <!–用result属性来映射非主键字段，property为实体类属性名，column为数据库表中的属性–>
    <result property ="orderno" column ="order_no"/>
    <result property="price" column="order_price" />
</reslutMap>
```


### [5、使用Mybatis的mapper接口调用时候有哪些要求？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#5使用mybatis的mapper接口调用时候有哪些要求)  


**1、** Mapper接口方法名和Mapper.xml中定义的每个SQL的id相同；

**2、** Mapper接口方法的输入参数类型和mapper.xml中定义的每个sqlparameterType类型相同

**3、** Mapper接口方法的输入输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

**4、** Mapper.xml文件中的namespace，就是接口的类路径。


### [6、MyBatis框架适用场合：](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#6mybatis框架适用场合：)  


**1、** MyBatis专注于SQL本身，是一个足够灵活的DAO层解决方案。

**2、** 对性能的要求很高，或者需求变化较多的项目，如互联网项目，MyBatis将是不错的选择。


### [7、为什么需要预编译](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#7为什么需要预编译)  


**定义：**

SQL 预编译指的是数据库驱动在发送 SQL 语句和参数给 DBMS 之前对 SQL 语句进行编译，这样 DBMS 执行 SQL 时，就不需要重新编译。

**为什么需要预编译**

JDBC 中使用对象 PreparedStatement 来抽象预编译语句，使用预编译。预编译阶段可以优化 SQL 的执行。预编译之后的 SQL 多数情况下可以直接执行，DBMS 不需要再次编译，越复杂的SQL，编译的复杂度将越大，预编译阶段可以合并多次操作为一个操作。同时预编译语句对象可以重复利用。把一个 SQL 预编译后产生的 PreparedStatement 对象缓存下来，下次对于同一个SQL，可以直接使用这个缓存的 PreparedState 对象。Mybatis默认情况下，将对所有的 SQL 进行预编译。

还有一个重要的原因，复制SQL注入


### [8、什么是Mybatis？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#8什么是mybatis)  


**1、** Mybatis是一个半ORM（对象关系映射）框架，它内部封装了JDBC，开发时只需要关注SQL语句本身，不需要花费精力去处理加载驱动、创建连接、创建statement等繁杂的过程。程序员直接编写原生态sql，可以严格控制sql执行性能，灵活度高。

**2、** MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO映射成数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

**3、** 通过xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过java对象和 statement中sql的动态参数进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射为java对象并返回。（从执行sql到返回result的过程）。


### [9、Mybatis是如何进行分页的？分页插件的原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#9mybatis是如何进行分页的分页插件的原理是什么)  


Mybatis使用Row Bounds对象进行分页，它是针对Result Set结果集执行的内存分页，而非物理分页。可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

分页原理：分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据dialect方言，添加对应的物理分页语句和物理分页参数。


### [10、Mybatis 都有哪些 Executor 执行器？它们之间的区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新面试题，2021年面试题及答案汇总.md#10mybatis-都有哪些-executor-执行器它们之间的区别是什么)  


Mybatis 有三种基本的 Executor 执行器，SimpleExecutor、ReuseExecutor、

BatchExecutor。1、SimpleExecutor：每执行一次 update 或 select，就开启一个 Statement 对

象，用完立刻关闭 Statement 对象。2、ReuseExecutor：执行 update 或 select，以 sql 作为

key 查找 Statement 对象，存在就使用，不存在就创建，用完后，不关闭 Statement 对象，

而是放置于 Map3、BatchExecutor：完成批处理。


### 11、MyBatis与Hibernate有哪些不同？
### 12、讲下 MyBatis 的缓存
### 13、MyBatis与Hibernate有哪些不同？
### 14、Xml 映射文件中，除了常见的 select|insert|updae|delete 标签之外，还有哪些标签？
### 15、如何获取自动生成的(主)键值?
### 16、ORM是什么
### 17、简述Mybatis的插件运行原理，以及如何编写一个插件。
### 18、如何执行批量插入?
### 19、模糊查询 like 语句该怎么写
### 20、Mybatis的一级、二级缓存:
### 21、Mybatis与Spring 的整合？
### 22、resultType resultMap 的区别？
### 23、在 mapper 中如何传递多个参数？
### 24、Mybatis的表关联的映射？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




