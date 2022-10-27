前后端分离项目

springBoot——Vue

需要的环境：

- IDEA代码开发环境，自行根据喜好即可
- 安装node（会集成npm，所以只安装node即可，npm切换为淘宝镜像源）
- jdk1.8+
- vue-cli 4.0+

首先创建Vue前端模板框架在项目中

![image-20220912221127595](C:\Users\31330\Pictures\Typora\image-20220912221127595.png)

新建文件夹spring-vue-first存放前后端项目代码

目录：``D:\JAVA\IDEA\IDEAProjects\spring-vue-first``

查看vue-cli版本``vue -V``，没有安装的用下面命令安装：``npm i -g @vue/cli``

用cli命令创建vue文件夹存放前端模板

![image-20220912221543181](C:\Users\31330\Pictures\Typora\image-20220912221543181.png)

选择最后一行Manually select features

![image-20220912221638434](C:\Users\31330\Pictures\Typora\image-20220912221638434.png)

选择两个一个是babel，一个是router，上下键是移动光标，空格键选择

![image-20220912221745182](C:\Users\31330\Pictures\Typora\image-20220912221745182.png)

然后回车键后选择vue2.0就行

然后提示确定否，直接键入y，然后回车，在选择最后一项In package.json

![image-20220912221939440](C:\Users\31330\Pictures\Typora\image-20220912221939440.png)

回车后提示输入确定否，此处可以选择不保存此种创建vue方案，所以直接键入n回车

![image-20220912222154825](C:\Users\31330\Pictures\Typora\image-20220912222154825.png)

之后出现上图就代表vue项目正在创建，有点慢，可以自行设置淘宝镜像源加速创建。

如下图，wait a minute即可完成创建：

![image-20220912222306029](C:\Users\31330\Pictures\Typora\image-20220912222306029.png)

查看文件夹项目结构：

![image-20220912222437015](C:\Users\31330\Pictures\Typora\image-20220912222437015.png)

之后就可以用IDEA直接打开spring-vue-first里的vue这个项目了，注意，是打开vue这个前端项目

![image-20220912222812444](C:\Users\31330\Pictures\Typora\image-20220912222812444.png)

由于使用到elementUI所以前往命令行安装element

```bash
npm i element-ui -S
```

![image-20220912223332297](C:\Users\31330\Pictures\Typora\image-20220912223332297.png)

然后就可以运行了：

```bash
npm run serve
```

![image-20220912223652386](C:\Users\31330\Pictures\Typora\image-20220912223652386.png)

element整合vue具体上手请前往官网-->[https://element.eleme.cn/#/zh-CN/component/quickstart](https://element.eleme.cn/#/zh-CN/component/quickstart)









