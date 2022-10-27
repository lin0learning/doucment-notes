### 1. Terminal 常用命令

1. 使用 ↑ 键，可以快速定位到上一次执行的命令
2. 使用 tab 键，能够快速补全路径
3. 使用 Esc 键，能够快速清空当前已输入的命令
4. 输入 cls 命令，可以清空终端

### 2. fs 模块

fs模块是Node.js官方提供的、用来操作文件的模块。

- fs.readFile()，读取指定文件中的内容
- fs.readFile()，向指定的文件中写入内容

如果要在JavaScript代码中，使用fs模块来操作文件，则需要使用如下的方式导入它：

```js
const fs = require('fs')
```

#### 2.1 fs.readFile() 语法格式

```js
fs.readFile(path[, options], callback)
```

[,options]为可选参数options，callback为必选参数，文件读取完成后，通过回调函数拿到读取的结果

#### 2.2 fs.writeFlie() 语法格式

```js
fs.writeFlie(file, data[, options],callback)
```

#### 2.3 fs模块 - 路径动态拼接的问题

在使用fs模块操作文件时，如果提供的操作路径是以 ./ 或者 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。

原因： 代码在运行的时候，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径

解决方法：提供文件的完整绝对路径，缺点是移植性差

#### 2.4 __dirname 

表示当前文件所处的目录（绝对路径），它所代表的的值不会随着调用者执行node命令时所处目录的变化而变化

### 3. path 路径模块

path模块是由Node.js官方提供的、用来处理路径的模块。

- path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename() 方法，用来从路径字符串中，将文件名解析出来

```js
const path = require('path')
```

#### 3.1 路径拼接

path.join() 的语法格式

```js
path.join([...paths])
```

- ...paths <string>路径片段的序列
- 返回值：<string>

```js
const pathStr = path.join('/a','/b/c','../','./d','e')
console.log(pathStr) // \a\b\d\e

const pathStr2 = path.join(__dirname,'./files/1.txt')
console.log(pathStrs) // 输出当前文件所处目录
```

**凡是涉及到路劲拼接的操作，都要使用path.join()方法进行处理**

#### 3.2 获取路径中的文件名

1. path.basename() 的语法格式
   使用此方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名

   ```js
   path.basename(path[, ext])
   ```

   

#### 3.3 获取路径中的文件扩展名

1. path.extname() 的语法格式

   ```js
   path.extname(path)
   ```

   

### 4. http模块

http模块是 Node.js 官方提供的、用来创建web服务器的模块。通过http.createServer()方法，将普通电脑变成一台Web服务器。

```js
const http = require('http')
```

IP地址和域名是一一对应的关系，这份对应关系存放在一种叫做域名服务器（DNS）的电脑中，域名服务器为IP地址和域名之间的转换提供服务。

实际应用中，URL中的80端口可以被省略。

**http server:**

1. http server是一种支持http协议的服务器;

2. http server监听在一个端口上面，等待客户端的http连接;

3. 客户端，创建一个TCP socket 连接到服务器;
4. 客户端像服务器发送一个 http协议的请求数据包;
5. 服务器获得这个请求，然后返回一个http响应数据包;

6. 服务器关闭Tcp socket, 客户端也关闭TCP socket;

7. Connection:keep-alive 如果有再次访问这个服务器上的网页，会继续使用这一条已经建立的连接，Keep-Alive不会永久保持连接，它有一个保持时间，默认是马上关闭;

**express 安装与搭建**

1. express是一个node.js的轻量级 高效的webserver;
2. npm install express;

3. 配置express网站根目录,提供静态网页服务;

4. 配置express的GET url响应地址;

5. 获取GET所携带的参数 req.query;
6. 获取POST所携带的参数req.body.

#### 4.1 创建最基本的的Web服务器

1. 导入http模块

   ```js
   const http = require('http')
   ```

2. 创建web服务器实例

   ```js
   const server = http.createServer()
   ```

3. 为服务器实例绑定request事件，监听客户端的请求

   ```js
   server.on('request', (req,res) => {
       console.log('Someone vist our web server.')
   })
   ```

4. 启动服务器

   ```js
   server.listen(80, () => {
       console.log('http server running at http://120.0.0.1')
   })
   ```

域名为localhost的（本地）IP地址为120.0.0.1。

req请求对象，包含了与客户端相关的数据和属性，例如：

- req.url 是客户端请求的 URL 地址

- req.method 是客户端的 method 请求类型

当调用res.end()方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

### 5. 根据不同的 url 响应不同的 html 内容

1.**核心实现步骤**

1. 获取请求的 URL 地址
2. 设置默认的响应内容为 404 Not found
3. 判断用户请求的 是否为 / 或 /index.html 首页
4. 判断用户请求的是否为 /about.html 关于页面
5. 设置 Content-Type 响应头， 防止中文乱码
6. 使用 res.send() 把内容响应给客户端

### 6. 模块化

- 模块化的优点
- ~~CommonJS规定的内容~~ （被ES6替代）
- Node.js模块的三大分类
- npm管理包
- 规范的包结构
- 模块的加载机制

#### 6.1 模块化

1. 复用性
2. 可维护性
3. 按需加载

#### 6.2 模块的分类

- 内置模块
- 自定义模块
- 第三方模块

通过 require() 方法加载模块，此方法在加载模块的同时默认**执行模块中的代码**，在加载自定义模块时，可以省略 **.js** 后缀名；

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准；

由于 module.exports 单词键入较为复杂，Node 提供了 exports 对象。默认情况下，exports 和 module.exports 指向同一个对象。最终共享的结果，以 module.exports 指向的对象为准；

### 7. npm与包

#### 7.1 包

Node.js中的第三方模块又叫做包。

npm install module 可简化成npm i module

要安装指定版本的包，可以在包名之后，通过@符号指定具体的版本，例：

```
npm install moment@2.22.2
```

#### 7.2 包的语义化版本规范

包的版本号是以“点分十进制”形式进行定义的，其中每一位数字所代表的的含义如下：

第1位数字：大半本

第2位数字：功能版本

第3位数字：Bug修复版本

版本号提升的规则：只要前面的版本号增长了，则后面的版本号归零。

#### 7.3 包管理配置文件

npm规定，在项目根目录中，必须提供一个叫 package.json 的包管理配置文件，用以记录与项目有关的一些配置信息。

1. 快速创建package.json

   ```
   npm init -y
   ```

   上述命令只能在英文的目录下成功运行！

   运行npm install 命令安装包时，npm包管理工具会自动把包的名称和版本号，记录到package.json中。

2. 一次性安装所有包
   当拿到一个剔除了node_modules 的项目后，需要先下载所有当前项目所依赖的包。可以运行npm install命令，一次性安装所有的依赖包：

   ```
   npm install
   ```

3. 卸载包

   ```
   npm uninstall moment
   ```

4. devDependencies 节点
   如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies 节点中。
   与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到dependencies 节点中。
   使用如下命令，将包记录到devDependencies 节点中：

   ```
   npm i module_name -D
   // 完整写法
   npm install module_name --save-dev
   ```

5. npm安装包时的后缀意义

   1. -S :  即 --save （保存） 添加这个后缀安装的包名会被注册在package.json的dependencies中，在生产环境下这个包的依赖依然存在，如vue，react，element等
   2. -D : 即 --dev（生产） 包名会被注册在package.json的devDependencies里面，仅在开发环境下存在的包用-D，如babel，sass-loader这些解析器
   3. -G :  即 --global (全局) 这个后缀用于全局安装，在自己电脑进行开发时，一些插件可以全局安装，这样就不用每次重建项目都要安装下，例如vue-cli脚手架


#### 7.4 切换 npm 的下包镜像源

```
# 查看当前的下包镜像源
npm config get registry
#将下包镜像源切换为淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
#检查镜像源是否下载成功
npm config get registry
```

#### 7.5 nrm

```
# 通过 npm 包管理器，将nrm安装为全局可用的工具
npm i nrm -g
# 查看所有可用的镜像源
nrm ls
# 将下包的镜像源切换为 taobao 镜像
nrm use taobao
```

### 8. 模块的加载机制

1. 模块在第一次加载后会被缓存。这意味着多次调用require() 不会导致模块的代码被执行多次。
2. 内置模块的加载优先级最高。
3. 使用  require() 加载自定义模块时，必须指定以 ./ 或 ../开头的路径标识符。如果没有指定 ./ 或 ../ 这样的路径标识符，则node会把它当做内置模块或第三方模块进行加载。
4. 在使用  require() 导入自定义模块时，如果省略了文件的扩展名，则Node.js会按顺序分别尝试加载以下文件：
   ① 按照确切的文件名进行加载
   ② 补全 .js
   ③ 补全 .json
   ④ 补全 .node 
   ⑤ 加载失败，终端报错

### 9. Express 

#### 9.1 Express 的基本使用

1. 官方概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web开发框架。

2. 监听 GET 请求
   通过 app.get() 方法，监听客户端的 GET 请求

   ```js
   app.get('请求URL', function(req, res) { /*处理函数*/ })
   ```

3. 监听 POST 请求

   通过 app.post() 方法，监听客户端的 POST 请求

   ```js
   app.post('请求URL', function(req, res) { /*处理函数*/ })
   ```

4.  将内容响应给客户端
   通过 res.send() 方法，发送给客户端

5. 通过 req.query 对象， 可以访问到客户端通过查询字符串的形式

6. 通过 req.params 对象，可以访问到 URL中，通过 : 匹配到的动态参数

#### 9.2 托管静态资源

1. express.static()
   通过express.static() 方法，可以方便地创建一个静态资源服务器，例如将指定目录（如下的public）下的图片、CSS文件、JavaScript文件对外开放访问。

   ```js
   app.use(express.static('public')) //路径不严谨
   app.use(express.static(path.join(__dirname, 'public')))
   ```
   
   注意： Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL 中。
   
   如果要托管多个静态资源目录，则需多次调用 express.static() 方法
   
2. 挂载路径前缀
   如果希望在托管的静态资源访问路径之前，挂载路径前缀，则使用如下方式：

   ```js
   app.use('/public',express.static('public'))
   ```

   http://localhost:3000/public/index.html

3. nodemon

#### 9.3 Express 路由

在 Express 中，路由指的是客户端的请求与服务器处理函数之前的映射关系。

1. 路由的概念
   etc

2. 模块化路由
   为了方便对路由进行模块化的管理，Express不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。实现步骤如下：
   ① 创建路由模块对应的 .js文件
   ② 调用 express.Router() 函数创建路由对象
   ③ 向路由对象上挂载具体的路由
   ④ 使用 module.exports 向外共享路由对象
   ⑤ 使用 app.use() 函数注册路由模块

3. 创建路由模块

   ```js
   let express = require('express')
   let router = express.Router()
   
   router.get('/user/list', function(req, res) => {
              res.send('Get')
              })
   router.post('/user/add', function(req, res) => {
              res.send('Post')
              })
   
   module.exports = router
   ```

   

4. 注册路由模块
   
   ```js
   // 1.导入路由模块
   const userRouter = require('./router/user.js')
   
   // 2. 使用 app.use() 注册路由模块
   app.use(userRouter)
   ```
   
4. 注意事项：app.use()
   app.use() 函数的作用，就是注册全局中间件

6. 为路由模块添加前缀
   类似于托管静态资源时，为静态资源统一挂载访问前缀一样

   ```js
   // 1. 导入路由模块
   const userRouter = require('./router/user.js')
   
   // 2. 使用app.use() 注册路由模块，并添加统一的访问前缀 /api
   app.use('/api', userRouter)
   ```

#### 9.4 Express 中间件

1. Express中间件的格式
   Express的中间件本质上是一个function 处理函数

   ```js
   app.get('/', function(req, res, next) {
       next();
   })
   ```

   注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

2. next 函数的作用
   next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

3. 定义中间件函数

   ```js
   // 常量 mw 所指向的，就是一个中间件函数
   const mw = function(req, res, next) {
       console.log('中间件函数')
       // 当前中间件的业务处理完后，必须调用next()函数
       // 表示把流转关系转交给下一个中间件或路由
       next()
   }
   ```

4. 全局生效的中间件
   客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。
   通过调用 app.use(中间件函数), 即可定义一个全局生效的中间件

5. 全局中间件简化形式

   ```js
   app.use((req, res, next) =>{
       console.log('最简单的中间件函数')
       next()
   })
   ```

6. 中间件的作用
   多个中间件之间，共享一份 req 和 res。基于这一特性，可以在上游的中间件中，统一为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

7. 局部生效的中间件
   不使用 app.use() 定义的中间件， 叫做局部生效的中间件。

   ```js
   app.get('/', mw1, mw2, (req, res) => { res.send('Home page.')})
   app.get('/', [mw1, mw2], (req, res) => { res.send('Home page.')})
   ```

8. 中间件的分类
   ① 应用级别：通过app.use() 或 app.get() 或 app.post()，绑定到 app 实例上的中间件。 
   ② 路由级别：绑定到 express.Router() 实例上的中间价。
   ③ 错误级别：作用是专门捕获项目中发生的异常错误，防止项目崩溃。function处理函数中，必须有4 个形参，分别是 (err, req, res, next)。

   注意：错误级别的中间件必须注册在所有路由之后！
   ④ Express 内置：① express.static ② express.json ③ express.urlencoded
   
   ⑤ 第三方: body-parser。
   **注意**：Express内置的 express.urlencoded 中间件， 就是基于 body-parser 这个第三方中间件进一步封装的。
   note：body 中 的urlencoded字符，只支持 utf-8编码的字符，返回的对象是一个键值对；当 extended 为 false时，键值对中的值为 'String' 或  'Array' 形式，为 true 时，则可为任何数据类型。

#### 9.5 使用 Express 写接口

note：不使用~~jQuery~~写请求，而使用~~fetch~~，axios

#### 9.5 CORS跨域资源共享

原生设置跨域资源共享：在路由方法中设置响应头，允许来自指定地址的请求进行访问来实现跨域。

```js
res.setHeader('Access-Control-Allow-Origin', '*')
```

cors是Express的一个第三方中间件。使用CORS中间件来解决跨域问题，实现跨域资源共享的使用步骤分为如下3步：

```js
npm install cors
const cors = require('cors')
// 在路由之前调用 app.use(cors())
app.use(cors())
```



1. CORS 响应头部 - Access-Control-Allow-Origin-headers

   ```js
   res.setHeader('Access-Control-Allow-Origin','*')
   res.setHeader('Access-Control-Allow-Origin','http://itcast.cn ')
   ```

   

