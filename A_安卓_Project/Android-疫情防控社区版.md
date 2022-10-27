



# TODO 1 git开发环境搭建

## #linux相关命令

```shell

ls(ll): 都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。
touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。
rm: 删除一个文件, rm index.js 就会把index.js文件删除。
mkdir: 新建一个目录,就是新建一个文件夹。
rm -r : 删除一个文件夹, rm -r src 删除src目录
mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。
reset 重新初始化终端/清屏。
clear 清屏。
history 查看命令历史。
help 帮助。
exit 退出。
```

## git协同开发相关命令：

~~~shell
#上传代码到本地仓库 
git add .

#上传代码到中间缓存区 
git commit -m "备注信息"

#上传代码到远程仓库（例如：Gitee） 
git push

#git清理被删除远程分支在本地库的缓存 
#使用git过程中，如果远程分支被删除，在本地使用git branch -a还是可以看到这些被删除分支。可以通过git remote prune 命令实现清理
git remote prune origin 

#更新出远程分支索引
git fetch
```

https://blog.csdn.net/A12115419/article/details/116116418

```shell
#创建分支
git branch 分支名

#查看分支
git branch或者git branch -a

#切换分支
git checkout 分支名

其实，分支的创建和切换只需要下面的一个指令就可以完成了：
git checkout -b 分支名

新建本地分支与远程分支关联
git branch --set-upstream-to=origin/develop develop
~~~

## 个人开发使用git完整指令

```shell
git init  // 初始化仓库
git add .  // 本地文件添加到本地缓存区（注意是’add .‘，点表示添加所有此目录下的文件）
git commit -m "描述"  // 提交到本地缓存区，描述任意写
git remote add origin "地址"  // 添加远端地址,此处的地址改为github复制过来的地址，例如：https://github.com/roydonGuo/MyBlog-Spring.git
git checkout -b main // 切换分支为main
git pull --rebase origin main  //下拉查看是否有内容
git push -u origin main  //推送到main分支
# 若是由于在远端直接更改导致无法push，可以使用强制push命令：git push origin master -f
git status  //查看状态，检查用到
```



## 团队开发操作git

### 成员需要怎么做
首先我们有一个共同开发的仓库。项目组长已经把框架建好。

小组成员此时本地还没有本项目，所以就需要从组长仓库中拉去代码到本地。
首先小组成员在本地找个合适的文件夹进入文件夹打开git bash 进入git面板操作git
下面是从远端拉取代码流程命令：

```shell
git init
git remote add origin https://github.com/gcb1120/google2022.git
#这就表示本地已经关联到远端。接着就是拉代码
#更新出远程分支索引
git fetch
# 先切换分支到develop
git checkout develop
git pull --rebase origin develop
```

## 分支的合并

git merge和git rebase两个命令来进行分支的合并。

1.快速合并
我们把develop分支合并到master分支上，来到master分支后，键入下述命令：

```shell
git merge develop
```

2.普通合并

```shell
git merge --no-ff -m "合并的信息" develop
```

当然，不是每次合并分支都是顺顺利利的，有事会发生合并冲突，这个时候，我们需要处理冲突，完成后才能够进行合并！

合并完之后，你只是把文件合并到了本地的master分支上，而没有上传到远程仓库，所以还要**push**到远程仓库的master分支上。

拉取远程分支到本地：https://blog.csdn.net/wen15191038073/article/details/125310090

```shell
git pull --rebase origin main

#切换仓库
git remote rm origin
git remote add origin https://github.com/gcb1120/google2022.git
```

# TODO 2 sql数据库



![image-20220929130651020](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202209291306119.png)



```sql
CREATE TABLE `sys_resident` (
  `id` int NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` varchar(50) DEFAULT NULL COMMENT '用户名',
  `password` varchar(50) DEFAULT NULL COMMENT '密码',
  `nickname` varchar(50) DEFAULT NULL COMMENT '昵称',
  `phone` varchar(20) DEFAULT NULL COMMENT '电话',
  `id_number` varchar(18) NOT NULL COMMENT '身份证',
  `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
  `address` varchar(255) DEFAULT NULL COMMENT '地址',
  `sex` varchar(2) DEFAULT NULL COMMENT '性别',
  `tenant` int DEFAULT NULL COMMENT '是否为租客：1：租客，0：非租客',
  `update_time` datetime DEFAULT NULL,
  `create_time` datetime DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `avatar_url` varchar(255) DEFAULT NULL COMMENT '头像',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=100010 DEFAULT CHARSET=utf8;
```





# TODO 3 springboot项目后台搭建



居民接口

```java
package edu.zut.epidemic.controller;


import com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper;
import com.baomidou.mybatisplus.extension.plugins.pagination.Page;
import edu.zut.epidemic.common.Result;
import edu.zut.epidemic.entity.Resident;
import edu.zut.epidemic.service.IResidentService;
import lombok.extern.slf4j.Slf4j;
import org.apache.logging.log4j.util.Strings;
import org.springframework.util.DigestUtils;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;
import java.util.List;

/**
 * <p>
 * 前端控制层
 * </p>
 *
 * @author roydon
 * @since 2022-09-28
 */
@Slf4j
@RestController
@RequestMapping("/resident")
public class ResidentController {

    @Resource
    private IResidentService residentService;

    /**
     * 新增或者更新
     *
     * @param resident 居民实体
     * @return
     */
    @PostMapping
    public Result save(@RequestBody Resident resident) {

        //密码password进行md5加密处理
        resident.setPassword(DigestUtils.md5DigestAsHex(resident.getPassword().getBytes()));
        return Result.success(residentService.saveOrUpdate(resident));
    }

    /**
     * 根据id删除
     *
     * @param id
     * @return
     */
    @DeleteMapping("/{id}")
    public Result delete(@PathVariable Integer id) {
        return Result.success(residentService.removeById(id));
    }

    /**
     * 批量删除
     *
     * @param ids id集合
     * @return
     */
    @DeleteMapping("/del/batch")
    public Result deleteBatch(@RequestBody List<Integer> ids) {
        return Result.success(residentService.removeByIds(ids));
    }

    /**
     * 查询所有
     *
     * @return
     */
    @GetMapping
    public Result findAll() {
        return Result.success(residentService.list());
    }

    /**
     * 根据id查询一条数据
     *
     * @param id
     * @return
     */
    @GetMapping("/{id}")
    public Result findOne(@PathVariable Integer id) {
        return Result.success(residentService.getById(id));
    }

    /**
     * mp分页查询
     *
     * @param pageNum
     * @param pageSize
     * @param name     姓名
     * @param phone    手机号
     * @param idNumber 身份证
     * @return
     */
    @GetMapping("/page")
    public Result findPage(@RequestParam Integer pageNum,
                           @RequestParam Integer pageSize,
                           @RequestParam(defaultValue = "") String name,
                           @RequestParam(defaultValue = "") String phone,
                           @RequestParam(defaultValue = "") String idNumber) {
        log.info("当前页码：{}，分页大小：{}", pageNum, pageSize);
        LambdaQueryWrapper<Resident> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.like(Strings.isNotEmpty(name), Resident::getName, name);
        queryWrapper.like(Strings.isNotEmpty(phone), Resident::getPhone, phone);
        queryWrapper.like(Strings.isNotEmpty(idNumber), Resident::getIdNumber, idNumber);
        queryWrapper.orderByDesc(Resident::getUpdateTime);
        return Result.success(residentService.page(new Page<>(pageNum, pageSize), queryWrapper));
    }
}
```







# TODO 4 安卓前端







# TODO 5 安卓后端
