# Node.js



前提·需要掌握

![image-20220809172613764](C:\Users\31330\Pictures\Typora\image-20220809172613764.png)

![image-20220809172800095](C:\Users\31330\Pictures\Typora\image-20220809172800095.png)

![image-20220809173304478](C:\Users\31330\Pictures\Typora\image-20220809173304478.png)

Node.js  is a JavaScript runtime built on Chrome's V8 JavaScript engine.
Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

Node.js 的官网地址： https://nodejs.org/zh-cn/

![image-20220809173543073](C:\Users\31330\Pictures\Typora\image-20220809173543073.png)

- 浏览器是 JavaScript 的前端运行环境。
- Node.js 是 JavaScript 的后端运行环境。Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API。

使用 tab 键，能够快速补全路径
使用 esc 键，能够快速清空当前已输入的命令
输入 cls 命令，可以清空终端



# fs 文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。
例如：

- **fs.readFile()** 方法，用来读取指定文件中的内容
- **fs.writeFile()** 方法，用来向指定的文件中写入内容 

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

![image-20220809180041915](C:\Users\31330\Pictures\Typora\image-20220809180041915.png)

## 1. fs.readFile() 的语法格式

使用 fs.readFile() 方法，可以读取指定文件中的内容，语法格式如下：

![image-20220809180124763](C:\Users\31330\Pictures\Typora\image-20220809180124763.png)

参数解读：

- 参数1：必选参数，字符串，表示文件的路径。
- 参数2：可选参数，表示以什么编码格式来读取文件。
- 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

## 2. fs.writeFile() 的语法格式

使用 fs.writeFile() 方法，可以向指定的文件中写入内容，语法格式如下：

![image-20220809181143249](C:\Users\31330\Pictures\Typora\image-20220809181143249.png)

参数解读：

- 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
- 参数2：必选参数，表示要写入的内容。
- 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
- 参数4：必选参数，文件写入完成后的回调函数。

==路径动态拼接的问题==

在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。
原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。
解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。

![image-20220809183810930](C:\Users\31330\Pictures\Typora\image-20220809183810930.png)

***

# path 路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。
例如：

- **path.join() **方法，用来将多个路径片段拼接成一个完整的路径字符串 
- **path.basename()** 方法，用来从路径字符串中，将文件名解析出来

如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

![image-20220809184211833](C:\Users\31330\Pictures\Typora\image-20220809184211833.png)

## 1. path.join() 的语法格式

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

![image-20220809184239876](C:\Users\31330\Pictures\Typora\image-20220809184239876.png)

参数解读：

- ...paths <string> 路径片段的序列
- 返回值: <string>

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串：

> 注意： '../'  表示回退一层路径
>
> 涉及到路径拼接的操作，都要使用 path.join() 方法进行处理。不要直接使用 + 进行字符串的拼接。

![image-20220809184320487](C:\Users\31330\Pictures\Typora\image-20220809184320487.png)

## 2. path.basename() 的语法格式

使用 path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

![image-20220809184534302](C:\Users\31330\Pictures\Typora\image-20220809184534302.png)

参数解读：

- path <string> 必选参数，表示一个路径的字符串 
- ext <string> 可选参数，表示文件扩展名
- 返回: <string> 表示路径中的最后一部分

使用 path.basename() 方法，可以从一个文件路径中，获取到文件的名称部分：

![image-20220809184630257](C:\Users\31330\Pictures\Typora\image-20220809184630257.png)

## 3. path.extname() 的语法格式

使用 path.extname() 方法，可以获取路径中的扩展名部分，语法格式如下：

![image-20220809184740369](C:\Users\31330\Pictures\Typora\image-20220809184740369.png)

参数解读：

- path <string>必选参数，表示一个路径的字符串
- 返回: <string> 返回得到的扩展名字符串

![image-20220809184824198](C:\Users\31330\Pictures\Typora\image-20220809184824198.png)

***

# http 模块

http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。

通过 http 模块提供的`` http.createServer() ``方法，就能方便的把一台电脑变成Web 服务器，从而对外提供 Web 资源服务。

## 1.创建基本的 web 服务器

```javascript
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(8080, function () {  
  console.log('server running at http://127.0.0.1:8080')
})
```

### req 请求对象

只要客户端访问了服务器监听的地址，服务器接收到了客户端的请求，就会调用通过 `server.on()` 为服务器绑定的 request 事件处理函数。

通过函数的 req 参数可以访问与==客户端==相关的数据或属性：

```javascript
server.on('request', (req, res) => {
  // req.url 是客户端请求的 URL 地址。req.method 是客户端请求的 method 类型
  const str = `Your request url is ${req.url}, and request method is ${req.method}`
  console.log(str)
  // 输出结果：Your request url is /, and request method is GET
})
```

### res 响应对象

如果想访问与==服务器==相关的数据或属性：res.end()

```javascript
server.on('request', (req, res) => {
  const str = `Your request url is ${req.url}, and request method is ${req.method}`
  // 调用 res.end() 方法，向客户端响应str。并结束这次请求的处理过程
  res.end(str)
})
```

==注意==：当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

```javascript
server.on('request', (req, res) => {
  const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
  // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  res.end(str)// 模块化之后 end() 全部变 send()
})
```

***

# 模块化

## 1. 模块化的基本概念

类似于电脑主机，你懂我意思吧。

Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：

- **内置模块**（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
- **自定义模块**（用户创建的每个 .js 文件，都是自定义模块）
- **第三方模块**（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

``require() ``方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。例如：

```javascript
const http = require('http')
```

模块作用域:

和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块
作用域。可以有效防止变量污染。

![image-20220829203007219](C:\Users\31330\Pictures\Typora\image-20220829203007219.png)

向外共享模块作用域中的成员：

1. ==module 对象==

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息，打印如下：

![image-20220829203223692](C:\Users\31330\Pictures\Typora\image-20220829203223692.png)

2. ==module.exports 对象==

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准。

![image-20220829203405008](C:\Users\31330\Pictures\Typora\image-20220829203405008.png)

3. ==exports 对象==

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象。默认情况
下，exports 和 module.exports 指向同一个对象。最终共享的结果，还是以 module.exports 指向的对象为准。

![image-20220829203530932](C:\Users\31330\Pictures\Typora\image-20220829203530932.png)

==注意==：

时刻谨记，require() 模块时，得到的永远是 **module.exports** 指向的对象：

不建议同一个模块中同时使用 exports 和 module.exports

![image-20220829203802578](C:\Users\31330\Pictures\Typora\image-20220829203802578.png)

## 2. npm与包

Node.js 中的第三方模块又叫做包。
就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。

国外有一家 IT 公司，叫做 npm, Inc. 这家公司旗下有一个非常著名的网站： https://www.npmjs.com/ ，它是全球最
大的包共享平台，你可以从这个网站上搜索到任何你需要的包，只要你有足够的耐心！
到目前位置，全球约 1100 多万的开发人员，通过这个包共享平台，开发并共享了超过 120 多万个包 供我们使用。
npm, Inc. 公司提供了一个地址为 https://registry.npmjs.org/ 的服务器，来对外共享所有的包，我们可以从这个服务
器上下载自己所需要的包。
注意：
⚫ 从 https://www.npmjs.com/ 网站上搜索自己所需要的包
⚫ 从 https://registry.npmjs.org/ 服务器上下载自己需要的包

包管理工具的名字叫做 Node Package Manager（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安
装包一起被安装到了用户的电脑上。

 npm -v 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号

安装第三方包：

```bash
npm i 包名
```

上述命令默认安装最新版本包

如果需要安装指定版本的包，可以在包名之后通过 ``@ 符号``指定具体的版本，例如：

```bash
npm i moment@2.22.2
```

初次装包完成后，在项目文件夹下多一个叫做 ==node_modules== 的文件夹和 ==package-lock.json== 的配置文件。

+ node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。
+ package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。

包管理配置文件:

npm 规定，在项目根目录中，必须提供一个叫做 ==package.json== 的包管理配置文件。用来记录与项目有关的一些配置
信息。信息存放在 dependencies  节点中。例如：

- 项目的名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在开发期间会用到
- 那些包在开发和部署时都需要用到

新建项目时进入文件夹使用如下命令即可自动生成 package.json 包管理配置文件

```bash
npm init -y
```

npm 包管理工具会自动把包的名称和版本号，记录到 package.json 中。

当我们拿到一个剔除了 node_modules 的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。
执行下面命令安装所有包。从 package.json 中读取按过的包

```bash
npm i
```

卸载包：

```bash
npm uninstall 包名
```

npm uninstall 命令执行成功后，会把卸载的包，自动从 package.json 的 dependencies 中移除掉。

只在项目开发阶段会用到，在项目上线之后不会用到的包安装命令：

```bash
npm i 包名 -D
```

命令等价于===npm i 包名 --save-dev

这些包将被记录到 devDependencies 节点中。与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

国外服务器，下包慢，切换镜像源到淘宝

- 查看当前镜像源

```bash
npm config get registry
```

- 切换为淘宝镜像源

```bash
npm config set registry=https://registry.npm.taobao.org
```

- 检测镜像源是否下载成功

```bash
npm config get registry
```

为了更方便的切换下包的镜像源，我们可以安装 nrm 这个小工具，利用 nrm 提供的终端命令，可以快速查看和切换下
包的镜像源。

```bash
npm i nrm -g
nrm ls
nrm use taobao
```

---

包的分类：

- 项目包

被安装到项目的 node_modules 目录中的包，都是项目包

项目包又分为两类，分别是：

```bash
npm i 包名 -D  #开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
npm i 包名     #核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）
```

- 全局包

全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。

```bash
npm i 包名 -g 		#全局安装包
npm uninstall 包名    #卸载全局安装包
```

注：只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。

---

# Express

Express 是基于 Node.js 平台，基于http模块，快速、开放、极简的 Web 开发框架。
通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。
Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。
Express 的中文官网： http://www.expressjs.com.cn/

安装：

```bash
npm i express@4.17.1
```

## 基本使用

```javascript
// 1. 导入 express
const express = require('express')
// 2. 创建 web 服务器
const app = express()
// --------------------
// 4. 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 JSON 对象
  res.send({ name: 'zs', age: 20, gender: '男' })
})
app.post('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 文本字符串
  res.send('请求成功')
})
app.get('/', (req, res) => {
  // 通过 req.query 可以获取到客户端发送过来的 查询参数
  // 注意：默认情况下，req.query 是一个空对象
  console.log(req.query)
  res.send(req.query)
})
// 注意：这里的 :id 是一个动态的参数
app.get('/user/:ids/:username', (req, res) => {
  // req.params 是动态匹配到的 URL 参数，默认也是一个空对象
  console.log(req.params)
  res.send(req.params)
})
// --------------------
// 3. 启动 web 服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

 托管静态资源：

``express.static()``

express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器，
例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```javascript
// 在这里，调用 express.static() 方法，快速的对外提供静态资源
app.use('/public', express.static('public'))
```

现在，你就可以通过带有 /public 前缀地址来访问 public 目录中的文件了：
http://localhost/public/images/kitten.jpg
http://localhost/public/css/style.css
http://localhost/public/js/app.js

---

> 在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。
> 现在，我们可以使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件
> 的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试。
>
> ```bash
> npm i -g nodemon
> ```
>
> node app.js 替换为 nodemon app.js

---

## Express 路由

广义上来讲，路由就是映射关系。

在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。
Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数

Express 中的路由的例子：

```javascript
const express = require('express')
const app = express()
// 挂载路由
// 匹配 GET 请求，请求 URL 为 /
app.get('/', (req, res) => {
  res.send('hello world.')
})
// 匹配 POST 请求，请求 URL 为 /
app.post('/', (req, res) => {
  res.send('Post Request.')
})
// 请求类型和请求的URL同时匹配成功，才会调用对应的处理函数
app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

使用：

为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。
将路由抽离为单独模块的步骤如下：
① 创建路由模块对应的 .js 文件
② 调用 express.Router() 函数创建路由对象
③ 向路由对象上挂载具体的路由
④ 使用 module.exports 向外共享路由对象
⑤ 使用 app.use() 函数注册路由模块

```javascript
const express = require('express')
const app = express()
// 导入路由模块
const router = require('./user_router')
// 5. 注册路由模块，并为路由模块添加前缀 /api
app.use('/api', router)
// 注意： app.use() 函数的作用，就是来注册全局中间件
// 请求地址变为了 http://127.0.0.1/api/......
// app.use('/files', express.static('./files'))
app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

创建的路由模块js文件（user_router.js）

```javascript
// 1. 创建 user_router.js，导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()
// 3. 挂载具体的路由
router.get('/user/list', (req, res) => {
  res.send('Get user list.by URL http://127.0.0.1/api/user/list')
})
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})
// 4. 向外导出路由对象
module.exports = router
```

---

## Express 中间件

中间件（Middleware ），特指业务流程的中间处理环节。

![image-20220829214331133](C:\Users\31330\Pictures\Typora\image-20220829214331133.png)

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

Express 的中间件，本质上就是一个 function 处理函数，Express 中间件的格式如下：

![image-20220829214506369](C:\Users\31330\Pictures\Typora\image-20220829214506369.png)

中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由

![image-20220829214642281](C:\Users\31330\Pictures\Typora\image-20220829214642281.png)

定义中间件函数：

中间件需要在路由之前定义，因为js从上到下读

```javascript
// 定义一个最简单的中间件函数
// const mw = function (req, res, next) {
//   console.log('这是最简单的中间件函数')
//   // 把流转关系，转交给下一个中间件或路由
//   next()
// }
// 将 mw 注册为全局生效的中间件
// app.use(mw)
// *************************
// 这是定义全局中间件的简化形式
app.use((req, res, next) => {
  console.log('这是最简单的中间件函数')
  const time = Date.now()
  // 为 req 对象，挂载自定义属性，从而把时间共享给后面的所有路由。多个中间件之间，共享 req 和 res 对象
  req.startTime = time
  next()
})
// *************************
```

定义局部生效的中间件：

```javascript
const express = require('express')
const app = express()
// 1. 定义中间件函数
const mw1 = (req, res, next) => {
  console.log('调用了局部生效的中间件')
  next()
}
// 2. 创建路由，引入mw1中间件
app.get('/', mw1, (req, res) => {
  res.send('Home page.')
})
// 同时使用多个局部中间件
// app.get('/', [mw1, mw2], (req, res) => {res.send('Home page.')})
// 等价于 app.get('/', mw1, mw2, (req, res) => {res.send('Home page.')})
app.get('/user', (req, res) => {
  res.send('User page.')
})
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：
① 应用级别的中间件
② 路由级别的中间件
③ 错误级别的中间件
④ Express 内置的中间件
⑤ 第三方的中间件

1. 应用级别的中间件

通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件，代码已经给出：

```javascript
// 全局
app.use((req, res, next) => {
  next()
})
// 局部
app.get('/', mw1, (req, res) => {
  res.send('Home page.')
})
```

2. 路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，**应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上**，代码示例如下：

```javascript
const express = require('express')
const app = exoress()
const router = express.Router()
// 路由级别中间件,此处先不必深究
router.use(function(req,res,next){
	next()
})
app.use('/',router)
```

3. 错误级别的中间件

错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。
格式：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)。

==注意==：错误级别的中间件，必须注册在所有路由之后！

```javascript
const express = require('express')
const app = express()
// 1. 定义路由
app.get('/', (req, res) => {
  // 1.1 人为的制造错误
  throw new Error('服务器内部发生了错误！')
  res.send('Home page.')
})

// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => { // 必须带4个参数，代码块中没有next()
  console.log('发生了错误！' + err.message)
  // 发送异常给客户端
  res.send('Error：' + err.message)
})

app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

4. Express内置的中间件

自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：
① express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
② express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
③ express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 

![image-20220829221153096](C:\Users\31330\Pictures\Typora\image-20220829221153096.png)

```javascript
// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 解析表单中的 JSON 格式的数据
app.use(express.json())
// 解析表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false }))
app.post('/user', (req, res) => {
  // 在服务器端，可以通过 req,body 来获取来接收客户端发送过来的请求体数据，包括 JSON 格式的表单数据和 url-encoded 格式的数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})
```

5. 第三方的中间件

。。。比如，老版本的 body-parser。功能同 express.urlencoded。后者就是基于前者封装的。

6.  自定义中间件

例如：模拟 express.urlencoded 对请求体进行解析。实现步骤：
① 定义中间件 app.use((req, res, next) => {...})
② 监听 req 的 data 事件
③ 监听 req 的 end 事件
④ 使用 querystring 模块解析请求体数据
⑤ 将解析出来的数据对象挂载为 req.body
⑥ 将自定义中间件封装为模块

```javascript
const express = require('express')
const app = express()
// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring')
// 1. 解析表单数据的中间件
app.use((req, res, next) => {
  // str 字符串存储请求体数据
  let str = ''
  // 2. 监听 req 的 data 事件
  req.on('data', (chunk) => {
    str += chunk
  })
  // 3. 监听 req 的 end 事件
  req.on('end', () => {
    // 4. 把字符串格式的请求体数据解析成对象格式
    const body = qs.parse(str)
    // 5. 对象挂载到自定义属性body上
    req.body = body
    // 交由路由处理
    next()
  })
})

app.post('/user', (req, res) => {
  res.send(req.body)
})
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

==注==：关键字 const 定义常量。let 定义变量。

⑥ 将自定义中间件封装为模块

第一步：新建js文件，内容：

```javascript
// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring')
const bodyParser = (req, res, next) => {
  let str = ''
  req.on('data', (chunk) => {str += chunk})
  req.on('end', () => {
    const body = qs.parse(str)
    req.body = body
    next()
  })
}
module.exports = bodyParser
```

第二步：使用

```javascript
const express = require('express')
const app = express()

// 1. 导入自己封装的中间件模块
const customBodyParser = require('./my-body-parser')
// 2. 将自定义的中间件函数，注册为全局可用的中间件
app.use(customBodyParser)

app.post('/user', (req, res) => {
  res.send(req.body)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

---

## Express 写接口



```javascript
const express = require('express')
const app = express()

// 解析表单数据的中间件
app.use(express.urlencoded({ extended: false }))

// 必须在配置 cors 中间件之前，配置 JSONP 的接口
app.get('/api/jsonp', (req, res) => {
  // 1. 得到函数的名称
  const funcName = req.query.callback
  // 2. 定义要发送到客户端的数据对象
  const data = { name: 'zs', age: 22 }
  // 3. 拼接出一个函数的调用
  const scriptStr = `${funcName}(${JSON.stringify(data)})`
  // 4. 把拼接的字符串，响应给客户端
  res.send(scriptStr)
})

// 一定要路由之前配置 cors 中间件，从而解决***接口跨域***
const cors = require('cors')
app.use(cors())

// 导入路由模块
const router = require('./my-apiRouter')
// 把路由模块注册到 app 上
app.use('/api', router)

// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

路由模块 my-apiRouter.js：

```javascript
const express = require('express')
const router = express.Router()
// 挂载路由
router.get('/get', (req, res) => {
  const query = req.query
  res.send({
    status: 0, // 0 表示处理成功，1 表示处理失败
    msg: 'GET 请求成功！',
    data: query, // 需要响应给客户端的数据
  })
})
router.post('/post', (req, res) => {
  const body = req.body
  res.send({
    status: 0,
    msg: 'POST 请求成功！',
    data: body,
  })
})
// 定义 DELETE 接口
router.delete('/delete', (req, res) => {
  res.send({
    status: 0,
    msg: 'DELETE请求成功',
  })
})

module.exports = router
```

**使用 cors 中间件解决跨域问题**
cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。
使用步骤分为如下 3 步：
① 运行 npm install cors 安装中间件
② 使用 const cors = require('cors') 导入中间件
③ 在路由之前调用 app.use(cors()) 配置中间件

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。
浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头就可以解除浏览器端的跨域访问限制。

![image-20220830000028687](C:\Users\31330\Pictures\Typora\image-20220830000028687.png)

CORS 主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口。CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口.

---

1. CORS 响应头部 - **Access-Control-Allow-Origin**

响应头部中可以携带一个 Access-Control-Allow-Origin 字段，其语法如下:

```tex
Access-Control-Allow-Origin: <origin> | *
```

origin 参数的值指定了允许访问该资源的外域 URL。例如，下面的字段值将只允许来自 https://roydon.xyz 的请求：

```javascript
res.setHeader('Access-Control-Allow-Origin','https://roydon.xyz')
```

如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *，表示允许来自任何域的请求，示例代码如下：

```javascript
res.setHeader('Access-Control-Allow-Origin','*')
```

2. CORS 响应头部 - **Access-Control-Allow-Headers**

默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：

| Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一） |
| ------------------------------------------------------------ |

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

```javascript
res.serHeader('Access-Control-Allow-Headers','Content-Type,X-Custom-Header')
```

3. CORS 响应头部 - **Access-Control-Allow-Methods**

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。
示例代码如下：

```javascript
res.serHeader('Access-Control-Allow-Methods','GET,POST,DELETE,HEAD')
// 允许所有请求
res.serHeader('Access-Control-Allow-Methods','*')
```

***

CORS请求的分类
客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

- ① 简单请求

同时满足以下两大条件的请求，就属于简单请求：
① 请求方式：GET、POST、HEAD 三者之一
② HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、
Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-
urlencoded、multipart/form-data、text/plain）

- ② 预检请求

只要符合以下任何一个条件的请求，都需要进行预检请求：
① 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
② 请求头中包含自定义头部字段
③ 向服务器发送了 application/json 格式的数据
在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一
次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

---



# 数据库

## 基本概念

组织、存储和管理数据的仓库。

除了文本类型的数据，图像、音乐、声音都是数据。

基本操作：增删查改。

推荐：	Mysql（关系型数据库

需要前提知识数据库（由于我做的是后端，了解数据库），此处不多赘述，直接进行node整合mysql。增删查改等Sql语句自行百度。

🥰🥰

## node整合mysql



步骤：

① 安装操作 MySQL 数据库的第三方模块（mysql）

```bash
npm i mysql
```

② 通过 mysql 模块连接到 MySQL 数据库

```javascript
// 1. 导入 mysql 模块
const mysql = require('mysql')
// 2. 建立与 MySQL 数据库的连接关系
const db = mysql.createPool({
  host: '127.0.0.1', // 数据库的 IP 地址
  user: 'root', // 登录数据库的账号
  password: 'qwer1234', // 登录数据库的密码
  database: 'db_1', // 指定要操作哪个数据库
})
```

③ 通过 mysql 模块执行 SQL 语句
下面依次举例（查找、增加、修改、删除）四项：数据表为 users

```javascript
// 1.查找
const sqlStr = 'select * from users'
db.query(sqlStr, (err, results) => {
  // 查询数据失败
  if (err) return console.log(err.message)
  // 查询数据成功
  // 注意：如果执行的是 select 查询语句，则执行的结果是数组
  console.log(results)
})
```

```javascript
// 2.增加
// 写法一：******************
const user = { username: 'guo', password: '123' }
// 定义待执行的 SQL 语句
const sqlStr = 'insert into users (username, password) values (?, ?)'
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password], (err, results) => {
  // 执行 SQL 语句失败了
  if (err) return console.log(err.message)
  // 成功了
  // 注意：如果执行的是 insert into 插入语句，则 results 是一个对象
  // 可以通过 affectedRows 属性，来判断是否插入数据成功
  if (results.affectedRows === 1) {
    console.log('插入数据成功!')
  }
})
// 写法二：推荐**********************
const user = { username: 'roydon', password: '123456' }
// 插入的 SQL 语句，? 为占位符
const sqlStr = 'insert into users set ?'
// 执行 SQL 语句
db.query(sqlStr, user, (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('插入数据成功')
  }
})
```

```javascript
// 3.修改(更新)
// 写法一：********************
const user = { id: 1, username: 'aaa', password: '000' }
// 定义 SQL 语句
const sqlStr = 'update users set username=?, password=? where id=?'
// 执行 SQL 语句
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
  if (err) return console.log(err.message)
  // 注意：执行了 update 语句之后，执行的结果，也是一个对象，可以通过 affectedRows 判断是否更新成功
  if (results.affectedRows === 1) {
    console.log('更新成功')
  }
})
// 写法二：(推荐)****************
const user = { id: 1, username: 'bbb', password: '111' }
// 定义 SQL 语句
const sqlStr = 'update users set ? where id=?'
// 执行 SQL 语句
db.query(sqlStr, [user, user.id], (err, results) => {
  if (err) return console.log(err.message)
  if (results.affectedRows === 1) {
    console.log('更新数据成功')
  }
})
```

```javascript
// 4.删除
const sqlStr = 'delete from users where id=?'
db.query(sqlStr, 2, (err, results) => {
  if (err) return console.log(err.message)
  // 注意：执行 delete 语句之后，结果也是一个对象，也会包含 affectedRows 属性
  if (results.affectedRows === 1) {
    console.log('删除数据成功')
  }
})
```

---

# 前后端的身份认证

目前主流的 Web 开发模式有两种，分别是：

1. 服务端渲染的传统 Web 开发模式

服务端渲染的概念：服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不
需要使用 Ajax 这样的技术额外请求页面的数据。

> 服务端渲染的优缺点
> 优点：
> ① 前端耗时少。因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
> ② 有利于SEO。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO。
> 缺点：
> ① 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
> ② 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于
> 项目高效开发。

2. 前后端分离的新型 Web 开发模式

前后端分离的概念：前后端分离的开发模式，依赖于 Ajax 技术的广泛应用。简而言之，前后端分离的 Web 开发模式，
就是后端只负责提供 API 接口，前端使用 Ajax 调用接口把数据渲染到页面上的开发模式。

> 前后端分离的优缺点
> 优点：
> ① 开发体验好。前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。
> ② 用户体验好。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
> ③ 减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。
> 缺点：
> ① 不利于 SEO。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。（解决方
> 案：利用 Vue、React 等前端框架的 SSR （server side render）技术能够很好的解决 SEO 问题！）

## 身份认证：

身份认证（Authentication）又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。
确保是此用户登录。

对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案：
**服务端渲染推荐使用 Session 认证机制**.

客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie，客户端会自动将 Cookie 保存在浏览器中。随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送给服务器，服务器即可验明客户端的身份。

Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器。
由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

Session 的工作原理：

https://img1.imgtp.com/2022/08/	30/kUmHTFh8.png

![image-20220830165126536](C:\Users\31330\Pictures\Typora\kUmHTFh8.png)

## Express 使用 Session 认证

1. 安装 express-session 插件

```bash
npm i express-session
```

2. 配置 express-session 中间件

 通过 app.use() 来注册 session 中间件:

```javascript
const express = require('express')
const app = express()

const session = require('express-session')
app.use(
  session({
    secret: 'roydon',	// 自定义字符穿
    resave: false,		// 固定写法
    saveUninitialized: true, // 固定写法
  })
)
```

3. 向 session 中存数据

通过 req.session 来访问和使用 session 对象，从而存储用户的关键信息：

例如下面的登录接口：

```javascript
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' })
  }
  // 将登录成功后的用户信息，保存到 Session 中
  req.session.user = req.body // 用户的信息
  req.session.islogin = true // 用户的登录状态

  res.send({ status: 0, msg: '登录成功' })
})
```

4. 从 session 中取数据

可以直接从 req.session 对象上获取之前存储的数据，示例代码如下：

```javascript
app.get('/api/username', (req, res) => {
  // 从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    // session 验证失败
    return res.send({ status: 1, msg: 'fail' })
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  })
})
```

5. 清空 Session 信息：req.session.destroy()

```javascript
app.post('/api/logout', (req, res) => {
  // 清空 Session 信息
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功',
  })
})
```

> 局限性：
>
> Session 认证机制需要配合 Cookie 才能实现。由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接
> 口的时候，需要做很多额外的配置，才能实现跨域 Session 认证。
> 注意：
> ⚫ 当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。
> ⚫ 当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。

---



## Express 使用 JWT

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案

前后端分离推荐使用 JWT 认证机制

JWT 的工作原理：用户信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份。

https://img1.imgtp.com/2022/08/30/f6Q43c6D.png

JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效荷载）、Signature（签名）。
三者之间使用英文的“.”分隔，格式如下：

```bash
Header.Payload.Signature
```

> Payload 部分是真正的用户信息，它是用户信息经过加密之后生成的字符串。
> Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

客户端收到服务器返回的 JWT 之后，通常会将它储存在 localStorage 或 sessionStorage 中。
此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证。推荐的做法是把 JWT 放在 HTTP **请求头的 Authorization 字段**中，格式如下：

```bash
Authorization: Bearer <token>
```



Express 中使用 JWT：

1. 安装包，导入包

 jsonwebtoken 用于生成 JWT 字符串。express-jwt 用于将 JWT 字符串解析还原成 JSON 对象

```bash
npm i jsonwebtoken express-jwt
```

2. 如下：（插件老版本写法如下）

```javascript
const express = require('express')
const app = express()

// 1.安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')

// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// 2.定义 secret 密钥，建议将密钥命名为 secretKey ，值自定义
const secretKey = 'i am roydon'

// 4.注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }))

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // 3.在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
```

插件新版本解析出来的信息好像会挂在到 req.auth 下。写法如下：

```javascript
const express = require('express')
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const { expressjwt: expressjwt } = require('express-jwt')
// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'i am roydon'
// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
app.use(expressjwt({ secret: secretKey, algorithms: ['HS256'] }).unless({ path: [/^\/api\//] }))
// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'roydon' || userinfo.password !== 'roydon') {
    return res.send({
      status: 400,
      message: '登录失败！'
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '60s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  // 获取token头信息值+Bearer
  console.log(req.auth)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.auth // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
```

https://img1.imgtp.com/2022/08/30/Yz4ncrVg.png

客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 **Authorization** 字段，将 Token 字符串发送到服务器进行身份认证。

| Authorization | Bearer+刚才上图生成的 token 字符串(中间空格隔开) |
| :-----------: | :----------------------------------------------- |

https://img1.imgtp.com/2022/08/30/evOCZIwX.png









