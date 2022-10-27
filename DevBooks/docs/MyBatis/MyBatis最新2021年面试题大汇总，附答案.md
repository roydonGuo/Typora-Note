# MyBatis最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Hibernate 和 MyBatis 的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#1hibernate-和-mybatis-的区别)  


**相同点**

都是对jdbc的封装，都是持久层的框架，都用于dao层的开发。

**不同点**

映射关系

MyBatis 是一个半自动映射的框架，配置Java对象与sql语句执行结果的对应关系，多表关联关系配置简单

Hibernate 是一个全表映射的框架，配置Java对象与数据库表的对应关系，多表关联关系配置复杂

**SQL优化和移植性**

Hibernate 对SQL语句封装，提供了日志、缓存、级联（级联比 MyBatis 强大）等特性，此外还提供 HQL（Hibernate Query Language）操作数据库，数据库无关性支持好，但会多消耗性能。如果项目需要支持多种数据库，代码开发量少，但SQL语句优化困难。

MyBatis 需要手动编写 SQL，支持动态 SQL、处理列表、动态生成表名、支持存储过程。开发工作量相对大些。直接使用SQL语句操作数据库，不支持数据库无关性，但sql语句优化容易。


### [2、Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射形式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#2mybatis-是如何将-sql-执行结果封装为目标对象并返回的都有哪些映射形式)  


第一种是使用标签，逐一定义列名和对象属性名之间的映射关系。

第二种是使用 sql 列的别名功能，将列别名书写为对象属性名，比如 T_NAME AS NAME，对

象属性名一般是 name，小写，但是列名不区分大小写，Mybatis 会忽略列名大小写，智能

找到与之对应对象属性名，你甚至可以写成 T_NAME AS NaMe，Mybatis 一样可以正常工

作。

有了列名与属性名的映射关系后，Mybatis 通过反射创建对象，同时使用反射给对象的属性

逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。


### [3、Mybatis编程步骤 ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#3mybatis编程步骤-)  


**1、** 创建SQLSessionFactory

**2、** 通过SQLSessionFactory创建SQLSession

**3、** 通过SQLSession执行数据库操作

**4、** 调用session.commit()提交事物 Step5：调用session.close()关闭会话


### [4、Mapper 编写有哪几种方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#4mapper-编写有哪几种方式)  


**第一种：接口实现类继承 SqlSessionDaoSupport：使用此种方法需要编写mapper 接口，mapper 接口实现类、mapper.xml 文件**

**1、** 在 sqlMapConfig.xml 中配置 mapper.xml 的位置

```
<mappers>
    <mapper resource="mapper.xml 文件的地址" />
    <mapper resource="mapper.xml 文件的地址" />
</mappers>
```

**2、** 定义 mapper 接口

**3、** 实现类集成 SqlSessionDaoSupport

mapper 方法中可以 this.getSqlSession()进行数据增删改查。

**4、** spring 配置

```
<bean id=" " class="mapper 接口的实现">
    <property name="sqlSessionFactory"
    ref="sqlSessionFactory"></property>
</bean>
```

**第二种：使用 org.mybatis.spring.mapper.MapperFactoryBean：**

**1、** 在 sqlMapConfig.xml 中配置 mapper.xml 的位置，如果 mapper.xml 和mappre 接口的名称相同且在同一个目录，这里可以不用配置

**2、** 定义 mapper 接口：

```
<mappers>
    <mapper resource="mapper.xml 文件的地址" />
    <mapper resource="mapper.xml 文件的地址" />
</mappers>
```

**3、** mapper.xml 中的 namespace 为 mapper 接口的地址

**4、** mapper 接口中的方法名和 mapper.xml 中的定义的 statement 的 id 保持一致

**5、** Spring 中定义

```
<bean id="" class="org.mybatis.spring.mapper.MapperFactoryBean">
    <property name="mapperInterface" value="mapper 接口地址" />
    <property name="sqlSessionFactory" ref="sqlSessionFactory" />
</bean>
```

**第三种：使用 mapper 扫描器：**

**1、** mapper.xml 文件编写：

mapper.xml 中的 namespace 为 mapper 接口的地址；

mapper 接口中的方法名和 mapper.xml 中的定义的 statement 的 id 保持一致；

如果将 mapper.xml 和 mapper 接口的名称保持一致则不用在 sqlMapConfig.xml中进行配置。

**2、** 定义 mapper 接口：

注意 mapper.xml 的文件名和 mapper 的接口名称保持一致，且放在同一个目录

**3、** 配置 mapper 扫描器：

```
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <property name="basePackage" value="mapper 接口包地址
    "></property>
    <property name="sqlSessionFactoryBeanName"
    value="sqlSessionFactory"/>
</bean>
```

**4、** 使用扫描器后从 spring 容器中获取 mapper 的实现对象。


### [5、Mybatis 是否可以映射 Enum 枚举类？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#5mybatis-是否可以映射-enum-枚举类)  


Mybatis 可以映射枚举类，不单可以映射枚举类，Mybatis 可以映射任何对象到表的一

列上。映射方式为自定义一个 TypeHandler，实现 TypeHandler 的 setParameter()和

getResult()接口方法。TypeHandler 有两个作用，一是完成从 javaType 至 jdbcType 的转换，

二是完成 jdbcType 至 javaType 的转换，体现为 setParameter()和 getResult()两个方法，分别

代表设置 sql 问号占位符参数和获取列查询结果。


### [6、Mybatis是如何进行分页的？分页插件的原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#6mybatis是如何进行分页的分页插件的原理是什么)  


Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页，可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据dialect方言，添加对应的物理分页语句和物理分页参数。

**举例：**

select * from student，拦截sql后重写为：select t.* from (select * from student) t limit 0, 10


### [7、Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#7mybatis-是否支持延迟加载如果支持它的实现原理是什么)  


**1、** Mybatis 仅支持 association 关联对象和 collection 关联集合对象的延迟加载，association

指的就是一对一，collection 指的就是一对多查询。在 Mybatis 配置文件中，可以配置是否

启用延迟加载 lazyLoadingEnabled=true|false。

**2、** 它的原理是，使用 CGLIB 创建目标对象的代理对象，当调用目标方法时，进入拦截器方

法，比如调用 a.getB().getName()，拦截器 invoke()方法发现 a.getB()是 null 值，那么就会单

独发送事先保存好的查询关联 B 对象的 sql，把 B 查询上来，然后调用 a.setB(b)，于是 a 的

对象 b 属性就有值了，接着完成 a.getB().getName()方法的调用。这就是延迟加载的基本原

理。


### [8、什么是 MyBatis 的接口绑定,有什么好处？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#8什么是-mybatis-的接口绑定,有什么好处)  


接口映射就是在 MyBatis 中任意定义接口,然后把接口里面的方法和 SQL 语句绑定,我们

直接调用接口方法就可以,这样比起原来了 SqlSession 提供的方法我们可以有更加灵活的选

择和设置.


### [9、Mybatis中如何指定使用哪一种Executor执行器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#9mybatis中如何指定使用哪一种executor执行器)  


在Mybatis配置文件中，在设置（settings）可以指定默认的ExecutorType执行器类型，也可以手动给DefaultSqlSessionFactory的创建SqlSession的方法传递ExecutorType类型参数，如SqlSession openSession(ExecutorType execType)。

配置默认的执行器。SIMPLE 就是普通的执行器；REUSE 执行器会重用预处理语句（prepared statements）； BATCH 执行器将重用语句并执行批量更新。


### [10、在mapper中如何传递多个参数?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题大汇总，附答案.md#10在mapper中如何传递多个参数)  


**1、** 第一种：

**DAO层的函数**

```java
public UserselectUser(String name,String area);
        对应的xml,#{0}代表接收的是dao层中的第一个参数，#{1}代表dao层中第二参数，更多参数一致往后加即可。
```

```xml
<select id="selectUser"resultMap="BaseResultMap">
    select *  fromuser_user_t   whereuser_name = #{0} anduser_area=#{1}
</select>
```

**2、** 第二种： 使用 [@param ](/param ) 注解:

```java
public interface usermapper {
    user selectuser(@param(“username”) string username,@param(“hashedpassword”) string hashedpassword);
}
```

然后,就可以在xml像下面这样使用(推荐封装为一个map,作为单个参数传递给mapper):

```xml
<select id=”selectuser” resulttype=”user”>
        select id, username, hashedpassword
        from some_table
        where username = #{username}
        and hashedpassword = #{hashedpassword}
        </select>
```

**3、** 第三种：多个参数封装成map

```java
try {
        //映射文件的命名空间.SQL片段的ID，就可以调用对应的映射文件中的SQL
        //由于我们的参数超过了两个，而方法中只有一个Object参数收集，因此我们使用Map集合来装载我们的参数
        Map < String, Object > map = new HashMap();
        map.put("start", start);
        map.put("end", end);
        return sqlSession.selectList("StudentID.pagination", map);
        } catch (Exception e) {
        e.printStackTrace();
        sqlSession.rollback();
        throw e;
        } finally {
        MybatisUtil.closeSqlSession();
        }
```


### 11、传统JDBC开发存在什么问题？
### 12、MyBatis 实现一对一有几种方式?具体怎么操作的？
### 13、MyBatis的功能架构是怎样的
### 14、#{}和${}的区别
### 15、IBatis 和 MyBatis 在核心处理类分别叫什么？
### 16、Mybatis 动态 sql 是做什么的？都有哪些动态 sql？能简述一下动态 sql 的执行原理不？
### 17、Mybatis的编程步骤是什么样的？
### 18、MyBatis框架适用场合：
### 19、Mybatis映射文件中，如果A标签通过include引用了B标签的内容
### 20、Mybatis 的 Xml 映射文件中，不同的 Xml 映射文件，id 是否可以重复？
### 21、MyBatis 的好处是什么？
### 22、使用MyBatis的mapper接口调用时有哪些要求？
### 23、#{}和${}的区别是什么？
### 24、Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？
### 25、JDBC编程有哪些不足之处，MyBatis是如何解决这些问题的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




