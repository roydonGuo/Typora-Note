# 简介

- 官网：https://baomidou.com

- 研发团队：苞米豆

- github地址：https://github.com/baomidou/mybatis-plus

***

[MyBatis-Plus](https://github.com/baomidou/mybatis-plus)（简称 MP）是一个 [MyBatis](https://www.mybatis.org/mybatis-3/)的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

![](C:\Users\31330\Pictures\Typora\mybatis.png)

小蓝鸟代表Mybatis，小红鸟代表MP，就像魂斗罗两兄弟，基友搭配，效率翻倍。

## 特性（来自官网）

- **无侵入**：只做增强不做改变，引入它不会对现有工程产生影响，如丝般顺滑
- **损耗小**：启动即会自动注入基本 CURD，性能基本无损耗，直接面向对象操作
- **强大的 CRUD 操作**：内置通用 Mapper、通用 Service，仅仅通过少量配置即可实现单表大部分 CRUD 操作，更有强大的条件构造器，满足各类使用需求
- **支持 Lambda 形式调用**：通过 Lambda 表达式，方便的编写各类查询条件，无需再担心字段写错
- **支持主键自动生成**：支持多达 4 种主键策略（内含分布式唯一 ID 生成器 - Sequence），可自由配置，完美解决主键问题
- **支持 ActiveRecord 模式**：支持 ActiveRecord 形式调用，实体类只需继承 Model 类即可进行强大的 CRUD 操作
- **支持自定义全局通用操作**：支持全局通用方法注入（ Write once, use anywhere ）
- **内置代码生成器**：采用代码或者 Maven 插件可快速生成 Mapper 、 Model 、 Service 、 Controller 层代码，支持模板引擎，更有超多自定义配置等您来使用
- **内置分页插件**：基于 MyBatis 物理分页，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询
- **分页插件支持多种数据库**：支持 MySQL、MariaDB、Oracle、DB2、H2、HSQL、SQLite、Postgre、SQLServer 等多种数据库
- **内置性能分析插件**：可输出 SQL 语句以及其执行时间，建议开发测试时启用该功能，能快速揪出慢查询
- **内置全局拦截插件**：提供全表 delete 、 update 操作智能分析阻断，也可自定义拦截规则，预防误操作

## 支持的数据库

常用的如MySQL，Oracle，DB2，SQLite等等。

## 框架结构

![](C:\Users\31330\Pictures\Typora\mybatis-plus-framework.jpg)

# mapper CRUD接口

## 引入``MP``依赖

新建springboot项目，引入依赖：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.3</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>roydon.xyz</groupId>
    <artifactId>Mybatis-Plus-Demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>Mybatis-Plus-Demo</name>
    <description>Mybatis-Plus-Demo</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--mybatis-plus-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.1.1</version>
        </dependency>
        <!--ali数据库连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.12</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <scope>4.12</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
    
</project>
```

## yml配置文件

yml配置：

```yml
server:
  port: 9090

spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://127.0.0.1:3306/mybatis-plus-first?serverTimezone=GMT%2b8
    username: root
    password: qwer1234

mybatis-plus:
  global-config:
    db-config:
      id-type: auto # id自增长配置，不用再每个实体每个主键单独配置。
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl #sql日志打印
  mapper-locations: classpath:mapper/*.xml  #自定义方法映射的sqlmapper文件路径
  type-aliases-package: roydon.xyz.mybatisplusdemo.entity
```

## 数据库

新建数据库文件：

![image-20220922171050762](C:\Users\31330\Pictures\Typora\image-20220922171050762.png)

```sql
CREATE TABLE `tb_user` (
  `id` bigint NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `user_name` varchar(20) NOT NULL COMMENT '用户名',
  `password` varchar(20) NOT NULL COMMENT '密码',
  `name` varchar(30) DEFAULT NULL COMMENT '姓名',
  `age` int DEFAULT NULL COMMENT '年龄',
  `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;
```

导入数据：

```sql
INSERT INTO `tb_user` (`id`, `user_name`, `password`, `name`, `age`, `email`) VALUES
('1', 'zhangsan', '123456', '张三', '18', 'test1@itcast.cn');
INSERT INTO `tb_user` (`id`, `user_name`, `password`, `name`, `age`, `email`) VALUES
('2', 'lisi', '123456', '李四', '20', 'test2@itcast.cn');
INSERT INTO `tb_user` (`id`, `user_name`, `password`, `name`, `age`, `email`) VALUES
('3', 'wangwu', '123456', '王五', '28', 'test3@itcast.cn');
INSERT INTO `tb_user` (`id`, `user_name`, `password`, `name`, `age`, `email`) VALUES
('4', 'zhaoliu', '123456', '赵六', '21', 'test4@itcast.cn');
INSERT INTO `tb_user` (`id`, `user_name`, `password`, `name`, `age`, `email`) VALUES
('5', 'sunqi', '123456', '孙七', '24', 'test5@itcast.cn');
```

## 实体类User

项目新建实体类``User``：

![image-20220922171654056](C:\Users\31330\Pictures\Typora\image-20220922171654056.png)

注意下方注解用法：

- @Data
  @AllArgsConstructor
  @NoArgsConstructor // 简化set，get
- @TableName("tb_user") // 指定表名
- @TableField // 下方已给出作用

```java
package roydon.xyz.mybatisplusdemo.entity;

import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.annotation.TableField;
import com.baomidou.mybatisplus.annotation.TableId;
import com.baomidou.mybatisplus.annotation.TableName;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

/**
 * Created by Intellij IDEA
 * Author: yi cheng
 * Date: 2022/9/21
 * Time: 20:14
 **/
@Data
@AllArgsConstructor
@NoArgsConstructor
@TableName("tb_user")
public class User {

    // @TableId(type = IdType.AUTO) // 主键自增长
    private Long id;

    private String userName;

    @TableField(select = false) // 忽略查询，查询结果无此字段
    private String password;

    @TableField(value = "name") // 指定数据库字段
    private String nickName;
    private Integer age;
    private String email;

    @TableField(exist = false) // 数据库是否存在此字段，关联查询时用到
    private String address;

}
```

## UserMapper

新建``UserMapper``

```java
package roydon.xyz.mybatisplusdemo.mapper;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import roydon.xyz.mybatisplusdemo.entity.User;

/**
 * Created by Intellij IDEA
 * Author: yi cheng
 * Date: 2022/9/21
 * Time: 20:18
 **/
// 通过继承BaseMapper就可以获取到各种各样的单表操作
public interface UserMapper extends BaseMapper<User> {

	// 可自定义方法，sql语句需写在resources对应的mapper下

}
```

通过继承BaseMapper就可以获取到各种各样的单表操作，如下：

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.baomidou.mybatisplus.core.mapper;

import com.baomidou.mybatisplus.core.conditions.Wrapper;
import com.baomidou.mybatisplus.core.metadata.IPage;
import java.io.Serializable;
import java.util.Collection;
import java.util.List;
import java.util.Map;
import org.apache.ibatis.annotations.Param;

public interface BaseMapper<T> extends Mapper<T> {
    int insert(T entity);

    int deleteById(Serializable id);

    int deleteByMap(@Param("cm") Map<String, Object> columnMap);

    int delete(@Param("ew") Wrapper<T> wrapper);

    int deleteBatchIds(@Param("coll") Collection<? extends Serializable> idList);

    int updateById(@Param("et") T entity);

    int update(@Param("et") T entity, @Param("ew") Wrapper<T> updateWrapper);

    T selectById(Serializable id);

    List<T> selectBatchIds(@Param("coll") Collection<? extends Serializable> idList);

    List<T> selectByMap(@Param("cm") Map<String, Object> columnMap);

    T selectOne(@Param("ew") Wrapper<T> queryWrapper);

    Integer selectCount(@Param("ew") Wrapper<T> queryWrapper);

    List<T> selectList(@Param("ew") Wrapper<T> queryWrapper);

    List<Map<String, Object>> selectMaps(@Param("ew") Wrapper<T> queryWrapper);

    List<Object> selectObjs(@Param("ew") Wrapper<T> queryWrapper);

    IPage<T> selectPage(IPage<T> page, @Param("ew") Wrapper<T> queryWrapper);

    IPage<Map<String, Object>> selectMapsPage(IPage<T> page, @Param("ew") Wrapper<T> queryWrapper);
}
```

## UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace：命名空间，指向的就是对应接口的全限定名-->
<mapper namespace="roydon.xyz.mybatisplusdemo.mapper.UserMapper">

    <select id="getById" resultType="user">
        select *
        from tb_user
        where id = #{id};
    </select>
</mapper>
```



## MybatisPlusConfig

新建``MP``配置文件

```java
package roydon.xyz.mybatisplusdemo.config;

import com.baomidou.mybatisplus.extension.plugins.PaginationInterceptor;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * Created by Intellij IDEA
 * Author: yi cheng
 * Date: 2022/9/21
 * Time: 20:49
 **/
@Configuration
@MapperScan("roydon/xyz/mybatisplusdemo/mapper") // 扫描mapper包
public class MybatisPlusConfig {

    /**
     * page分页插件，分页查询使用
     * @return
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }

}
```



## Test

```java
package roydon.xyz.mybatisplusdemo;

import com.baomidou.mybatisplus.core.conditions.query.QueryWrapper;
import com.baomidou.mybatisplus.core.conditions.update.UpdateWrapper;
import com.baomidou.mybatisplus.core.metadata.IPage;
import com.baomidou.mybatisplus.extension.plugins.pagination.Page;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import roydon.xyz.mybatisplusdemo.entity.User;
import roydon.xyz.mybatisplusdemo.mapper.UserMapper;

import javax.annotation.Resource;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

@SpringBootTest
class MybatisPlusDemoApplicationTests {

    @Resource
    private UserMapper userMapper;


    /**
     * select---------------------------------------------------------------
     */
    @Test
    public void testSelectById() {
        // 根据 ID 查询
        userMapper.selectById(2L);
    }

    @Test
    public void testSelectOne() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.eq("name", "张三"); //查询条件
        // 根据 entity 条件，查询一条记录。查询的数据超过一条时，会抛出异常(例如：wrapper.eq("password", "123456");)
        userMapper.selectOne(wrapper);
    }

    @Test
    void testSelectBatchIds() {
        // 查询（根据ID 批量查询），返回 List<User> 集合，若ID 不存在像100L，那么只会查出存在的ID
        userMapper.selectBatchIds(Arrays.asList(1L, 2L, 3L));
//        userMapper.selectBatchIds(Arrays.asList(1L, 2L, 3L,100L)); // 只会查出1，2，3
    }

    @Test
    public void testSelectList() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //设置查询条件
        wrapper.like("email", "itcast");
        userMapper.selectList(wrapper);
    }

    @Test
    public void testSelectByMap() {
        Map<String, Object> map = new HashMap<>();
        map.put("user_name", "zhangsan");
        map.put("password", "123456");
        // 查询（根据 columnMap 条件）
        userMapper.selectByMap(map);
    }

    @Test
    public void testSelectPage() {

        IPage<User> page = new Page<>(0, 2); // 第一页，两条数据

        QueryWrapper<User> queryWrapper = new QueryWrapper<>();
        queryWrapper.like("password", "123456");

        userMapper.selectPage(page, queryWrapper);

        System.out.println("数据总条数" + page.getTotal());
        System.out.println("数据总页数" + page.getPages());
        System.out.println("当前页数" + page.getCurrent()); // getRecords为数据list
    }

    @Test
    public void testSelectCount() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.gt("age", 20); // 条件：年龄大于20岁的用户
        // 根据 Wrapper 条件，查询总记录数，返回整数类型
        userMapper.selectCount(wrapper);
    }

    /**
     * update---------------------------------------------------------
     */
    @Test
    public void testUpdateById() {
        // 根据 ID 修改，返回整型，表示影响的行数
        User user = new User();
        user.setId(1L); //条件，根据id更新
        user.setAge(19); //更新的字段
        user.setPassword("666666");

        userMapper.updateById(user);
    }

    @Test
    public void testUpdate() {
        User user = new User();
        user.setAge(20); //更新的字段
        user.setPassword("8888888");

        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.eq("user_name", "zhangsan"); //匹配 user_name = zhangsan 的用户数据

        // 根据 whereWrapper 条件，更新记录
        userMapper.update(user, wrapper);
    }

    @Test
    public void testUpdate2() {
        UpdateWrapper<User> updateWrapper = new UpdateWrapper<>();
        updateWrapper.set("age", 21).set("password", "999999") //更新的字段
                .eq("user_name", "zhangsan"); //更新的条件
        userMapper.update(null, updateWrapper);
    }

    /**
     * insert--------------------------------------------------------
     */
    @Test
    public void testInsert() {
        User user = new User();
        user.setUserName("baomidou");
        user.setNickName("苞米豆");
        user.setPassword("123456");
        user.setAge(30);
        user.setEmail("insert@itcast.cn");
        user.setAddress("北京");
        userMapper.insert(user); //result数据库受影响的行数
        //获取自增长后的id值, 自增长后的id值会回填到user对象中
        System.out.println("id => " + user.getId());
    }

    /**
     * delete---------------------------------------------------------
     */
    @Test
    public void testDelete() {

        //用法一：
//        QueryWrapper<User> wrapper = new QueryWrapper<>();
//        wrapper.eq("user_name", "baomidou")
//                .eq("password", "123456");

        //用法二：
        User user = new User();
        user.setUserName("baomidou");
        user.setPassword("123456");

        QueryWrapper<User> wrapper = new QueryWrapper<>(user);
        // 根据包装条件做删除
        userMapper.delete(wrapper);
    }

    @Test
    public void testDeleteById() {
        // 根据id删除数据
        userMapper.deleteById(5L);
    }

    @Test
    public void testDeleteByMap() {
        Map<String, Object> map = new HashMap<>();
        map.put("user_name", "lisi");
        map.put("password", "123456");

        // 根据map删除数据，多条件之间是and关系
        userMapper.deleteByMap(map);
    }

    @Test
    public void testDeleteBatchIds() {
        // 根据id批量删除数据
        userMapper.deleteBatchIds(Arrays.asList(3L, 4L));
//        userMapper.deleteBatchIds(Arrays.asList(3L, 4L,100L));
    }

    /**
     * 自定义方法
     */
    @Test
    void selById() {
        userMapper.getById(1L);
    }

    /**
     * 自定义的方法
     */
//    @Test
//    public void testFindById(){
//        User user = this.userMapper.findById(2L);
//        System.out.println(user);
//    }
    @Test
    public void testAllEq() {

        Map<String, Object> params = new HashMap<>();
        params.put("name", "李四");
        params.put("age", "20");
        params.put("password", null);

        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE password IS NULL AND name = ? AND age = ?
//        wrapper.allEq(params);
        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? AND age = ?
//        wrapper.allEq(params, false);

        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE age = ?
//        wrapper.allEq((k, v) -> (k.equals("age") || k.equals("id")) , params);
        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? AND age = ?
        wrapper.allEq((k, v) -> (k.equals("age") || k.equals("id") || k.equals("name")), params);
        userMapper.selectList(wrapper);
    }

    @Test
    public void testEq() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //SELECT id,user_name,password,name,age,email FROM tb_user WHERE password = ? AND age >= ? AND name IN (?,?,?)
        wrapper.eq("password", "123456")
                .ge("age", 20)
                .in("name", "李四", "王五", "赵六");
        userMapper.selectList(wrapper);

    }

    @Test
    public void testLike() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        // SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name LIKE ?
        // 参数：%五(String)
        wrapper.likeLeft("name", "五");
        userMapper.selectList(wrapper);
    }

    @Test
    public void testOrderByAgeDesc() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //按照年龄倒序排序
        // SELECT id,user_name,name,age,email AS mail FROM tb_user ORDER BY age DESC
        wrapper.orderByDesc("age");
        userMapper.selectList(wrapper);

    }

    @Test
    public void testOr() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        // SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? OR age = ?
        wrapper.eq("name", "王五").or().eq("age", 21);
        userMapper.selectList(wrapper);
    }

    @Test
    public void testSelect() {
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //SELECT id,name,age FROM tb_user WHERE name = ? OR age = ?
        wrapper.eq("name", "王五")
                .or()
                .eq("age", 21)
                .select("id", "name", "age"); //指定查询的字段
		userMapper.selectList(wrapper);
       
    }
}
```



# 条件构造器

指路-->官方文档：[https://baomidou.com/pages/10c804/#abstractwrapper](https://baomidou.com/pages/10c804/#abstractwrapper)

## allEq

```java
allEq(Map<R, V> params)
allEq(Map<R, V> params, boolean null2IsNull)
allEq(boolean condition, Map<R, V> params, boolean null2IsNull)
```

- 全部[eq](https://baomidou.com/pages/10c804/#eq)(或个别[isNull](https://baomidou.com/pages/10c804/#isnull))

> 个别参数说明:
>
> `params` : `key`为数据库字段名,`value`为字段值
> `null2IsNull` : 为`true`则在`map`的`value`为`null`时调用 [isNull](https://baomidou.com/pages/10c804/#isnull) 方法,为`false`时则忽略`value`为`null`的

- 例1: `allEq({id:1,name:"老王",age:null})`--->`id = 1 and name = '老王' and age is null`
- 例2: `allEq({id:1,name:"老王",age:null}, false)`--->`id = 1 and name = '老王'`

```java
allEq(BiPredicate<R, V> filter, Map<R, V> params)
allEq(BiPredicate<R, V> filter, Map<R, V> params, boolean null2IsNull)
allEq(boolean condition, BiPredicate<R, V> filter, Map<R, V> params, boolean null2IsNull) 
```

>个别参数说明:
>
>`filter` : 过滤函数,是否允许字段传入比对条件中
>`params` 与 `null2IsNull` : 同上



- 例1: `allEq((k,v) -> k.indexOf("a") >= 0, {id:1,name:"老王",age:null})`--->`name = '老王' and age is null`
- 例2: `allEq((k,v) -> k.indexOf("a") >= 0, {id:1,name:"老王",age:null}, false)`--->`name = '老王'`

***

## 基本比较操作

- eq

  > 等于 = 

- ne 

  > 不等于 <> 

- gt 

  > 大于 > 

- ge 

  > 大于等于 >=

- lt 

  > 小于 < 

- le 

  > 小于等于 <= 

- between 

  > BETWEEN 值1 AND 值2 

- notBetween 

  > NOT BETWEEN 值1 AND 值2 

- in 

  > 字段 IN (value.get(0), value.get(1), ...)

- notIn 

  > 字段 NOT IN (v0, v1, ...)

## 模糊查询

- like 

> LIKE '%值%' 
>
> 例: like("name", "王") ---> name like '%王%' 

- notLike 

  > NOT LIKE '%值%'
  >
  > 例: notLike("name", "王") ---> name not like '%王%' 

- likeLeft 

  > LIKE '%值' 
  >
  > 例: likeLeft("name", "王") ---> name like '%王' 

- likeRight 

  > LIKE '值%' 
  >
  > 例: likeRight("name", "王") ---> name like '王%'

## 排序

- orderBy

> 例: orderBy(true, true, "id", "name") ---> order by id ASC,name ASC

- orderByAsc

> 例: orderByAsc("id", "name") ---> order by id ASC,name ASC

- orderByDesc

> 例: orderByDesc("id", "name") ---> order by id DESC,name DES

## 逻辑查询

- or

> 拼接 OR 
>
> 主动调用 or 表示紧接着下一个方法不是用 and 连接!(不调用 or 则默认为使用 and 连接)

- and

> AND 嵌套 
>
> 例: and(i -> i.eq("name", "李白").ne("status", "活着")) ---> and (name = '李白' and status <> '活着')

## select

在MP查询中，默认查询所有的字段，如果有需要也可以通过select方法进行指定字段。

```java
@Test
public void testSelect() {
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //SELECT id,name,age FROM tb_user WHERE name = ? OR age = ?
    wrapper.eq("name", "王五")
            .or()
            .eq("age", 21)
            .select("id", "name", "age"); //指定查询的字段
    userMapper.selectList(wrapper);
}
```

***

# 代码生成器（新）







# service CRUD

[https://baomidou.com/pages/49cc81/#service-crud-%E6%8E%A5%E5%8F%A3](https://baomidou.com/pages/49cc81/#service-crud-%E6%8E%A5%E5%8F%A3)







