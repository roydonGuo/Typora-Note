# MyBatis最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Mybatis的一级、二级缓存](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#1mybatis的一级二级缓存)  


**1、** 一级缓存: 基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为 Session，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。

**2、** 二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap 存储，不同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现Serializable序列化接口(可用来保存对象的状态),可在它的映射文件中配置`<cache/>`

**3、** 对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear。


### [2、简述Mybatis的Xml映射文件和Mybatis内部数据结构之间的映射关系？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#2简述mybatis的xml映射文件和mybatis内部数据结构之间的映射关系)  


Mybatis将所有Xml配置信息都封装到All-In-One重量级对象Configuration内部。在Xml映射文件中，`<parameterMap>`标签会被解析为ParameterMap对象，其每个子元素会被解析为ParameterMapping对象。`<resultMap>`标签会被解析为ResultMap对象，其每个子元素会被解析为ResultMapping对象。每一个`<select>`、`<insert>`、`<update>`、`<delete>`标签均会被解析为MappedStatement对象，标签内的sql会被解析为BoundSql对象。


### [3、Mybatis是否支持延迟加载？如果支持，它的实现原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#3mybatis是否支持延迟加载如果支持它的实现原理是什么)  


Mybatis仅支持association关联对象和collection关联集合对象的延迟加载，association指的就是一对一，collection指的就是一对多查询。在Mybatis配置文件中，可以配置是否启用延迟加载lazyLoadingEnabled=true|false。

它的原理是，使用CGLIB创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用a.getB().getName()，拦截器invoke()方法发现a.getB()是null值，那么就会单独发送事先保存好的查询关联B对象的sql，把B查询上来，然后调用a.setB(b)，于是a的对象b属性就有值了，接着完成a.getB().getName()方法的调用。这就是延迟加载的基本原理。

当然了，不光是Mybatis，几乎所有的包括Hibernate，支持延迟加载的原理都是一样的。


### [4、什么是MyBatis的接口绑定？有哪些实现方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#4什么是mybatis的接口绑定有哪些实现方式)  


接口绑定，就是在MyBatis中任意定义接口,然后把接口里面的方法和SQL语句绑定, 我们直接调用接口方法就可以,这样比起原来了SqlSession提供的方法我们可以有更加灵活的选择和设置。

接口绑定有两种实现方式,一种是通过注解绑定，就是在接口的方法上面加上 @Select、@Update等注解，里面包含Sql语句来绑定；另外一种就是通过xml里面写SQL来绑定, 在这种情况下,要指定xml映射文件里面的namespace必须为接口的全路径名。当Sql语句比较简单时候,用注解绑定, 当SQL语句比较复杂时候,用xml绑定,一般用xml绑定的比较多。


### [5、Mapper 编写有几种方式 ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#5mapper-编写有几种方式-)  


**1、** 接口实现类集成`SQLSessionDaoSupport`** 此方法需要编写`mapper`接口，`mapper`接口的实现类,`mapper.xml`文件。

**2、** 使用`org.mybatis.spring.mapper.MapperFactoryBean`** 此方法需要在`SqlMapConfig.xml`中配置`mapper.xml`的位置，还需定义`mapper`接口。

**3、** 使用`mapper`扫描器** 需要编写`mapper.xml`文件，需要`mapper`接口，配置`mapper`扫描器，使用扫描器从`spring`容器中获取`mapper`的实现对象。


### [6、Mybatis动态sql有什么用？执行原理？有哪些动态sql？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#6mybatis动态sql有什么用执行原理有哪些动态sql)  


Mybatis动态sql可以在Xml映射文件内，以标签的形式编写动态sql，执行原理是根据表达式的值 完成逻辑判断并动态拼接sql的功能。

Mybatis提供了9种动态sql标签：`trim | where | set | foreach | if | choose | when | otherwise | bind`。


### [7、MyBatis实现一对一有几种方式?具体怎么操作的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#7mybatis实现一对一有几种方式具体怎么操作的)  


有联合查询和嵌套查询,联合查询是几个表联合查询,只查询一次, 通过在resultMap里面配置association节点配置一对一的类就可以完成；

嵌套查询是先查一个表，根据这个表里面的结果的 外键id，去再另外一个表里面查询数据,也是通过association配置，但另外一个表的查询通过select属性配置。


### [8、模糊查询like语句该怎么写](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#8模糊查询like语句该怎么写)  


- 1 ’%${question}%’ 可能引起SQL注入，不推荐
- 2 "%"#{question}"%" 注意：因为#{…}解析成sql语句时候，会在变量外侧自动加单引号’ '，所以这里 % 需要使用双引号" "，不能使用单引号 ’ '，不然会查不到任何结果。
- 3 CONCAT(’%’,#{question},’%’) 使用CONCAT()函数，（推荐）
- 4 使用bind标签（不推荐）

```
<select id="listUserLikeUsername" resultType="com.jourwon.pojo.User">
  <bind name="pattern" value="'%' + username + '%'" />
  select id,sex,age,username,password from person where username LIKE{pattern}
</select>
```


### [9、MyBatis实现一对多有几种方式,怎么操作的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#9mybatis实现一对多有几种方式,怎么操作的)  


有联合查询和嵌套查询。联合查询是几个表联合查询,只查询一次,通过在resultMap里面的collection节点配置一对多的类就可以完成；嵌套查询是先查一个表,根据这个表里面的 结果的外键id,去再另外一个表里面查询数据,也是通过配置collection,但另外一个表的查询通过select节点配置。


### [10、Mapper编写有哪几种方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MyBatis/MyBatis最新2021年面试题，高级面试题及附答案解析.md#10mapper编写有哪几种方式)  


第一种：接口实现类继承SqlSessionDaoSupport：使用此种方法需要编写mapper接口，mapper接口实现类、mapper.xml文件。

**1、** 在sqlMapConfig.xml中配置mapper.xml的位置

```xml
<mappers>
    <mapper resource="mapper.xml文件的地址" />
    <mapper resource="mapper.xml文件的地址" />
</mappers>
```

**1、** 定义mapper接口

**3、** 实现类集成SqlSessionDaoSupport

mapper方法中可以this.getSqlSession()进行数据增删改查。

**4、** spring 配置

```xml
<bean id=" " class="mapper接口的实现">
    <property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
</bean>
```

第二种：使用`org.mybatis.spring.mapper.MapperFactoryBean`：

**1、** 在sqlMapConfig.xml中配置mapper.xml的位置，如果mapper.xml和mappre接口的名称相同且在同一个目录，这里可以不用配置

```xml
<mappers>
    <mapper resource="mapper.xml文件的地址" />
    <mapper resource="mapper.xml文件的地址" />
</mappers>
```

**2、** 定义mapper接口：

**1、** mapper.xml中的namespace为mapper接口的地址

**2、** mapper接口中的方法名和mapper.xml中的定义的statement的id保持一致

**3、** Spring中定义

```xml
<bean id="" class="org.mybatis.spring.mapper.MapperFactoryBean">
    <property name="mapperInterface"   value="mapper接口地址" />
    <property name="sqlSessionFactory" ref="sqlSessionFactory" />
</bean>
```

第三种：使用mapper扫描器：

**1、** mapper.xml文件编写：

mapper.xml中的namespace为mapper接口的地址；

mapper接口中的方法名和mapper.xml中的定义的statement的id保持一致；

如果将mapper.xml和mapper接口的名称保持一致则不用在sqlMapConfig.xml中进行配置。

**2、** 定义mapper接口：

注意mapper.xml的文件名和mapper的接口名称保持一致，且放在同一个目录

**3、** 配置mapper扫描器：

```xml
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <property name="basePackage" value="mapper接口包地址"></property>
    <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
</bean>
```

**4、** 使用扫描器后从spring容器中获取mapper的实现对象。


### 11、MyBatis框架的缺点：
### 12、MyBatis 里面的动态 Sql 是怎么设定的?用什么语法?
### 13、简述Mybatis的插件运行原理，以及如何编写一个插件。
### 14、Mybatis动态SQL？
### 15、使用MyBatis的mapper接口调用时有哪些要求？
### 16、Mybatis 是如何进行分页的？分页插件的原理是什么？
### 17、如何获取自动生成的(主)键值？
### 18、Mybatis 能执行一对一、一对多的关联查询吗？都有哪些实现方式，以及它们之间的区
### 19、简述 Mybatis 的插件运行原理，以及如何编写一个插件？
### 20、模糊查询like语句该怎么写?
### 21、Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？
### 22、Mybatis 中如何指定使用哪一种 Executor 执行器？
### 23、JDBC编程有哪些不足之处，MyBatis是如何解决的？
### 24、Mybatis优缺点
### 25、{}里面的名称对应的是Map里面的key名称。





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




