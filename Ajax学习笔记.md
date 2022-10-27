###  1 Ajax简介

Ajax  全称Asynchronous JavaScript And XML，异步的JS和XML。

通过Ajax可以在浏览器中向服务器发送异步请求，最大的优势：无刷新获取数据。

### 2 原生Ajax实现步骤

1. 创建Ajax对象

   ```js
   var xhr = new XMLHttpRequest()
   ```

2. 告诉Ajax请求地址以及请求方式

   ```js
   xhr.open('get', 'http://www.example.com')
   ```

3. 发送请求

   ```js
   xhr.send()
   ```

4. 获取服务器端给予客户端的响应数据

   ```js
   xhr.onload = function() {
       console.log(xhr.responseText)
   }
   ```

   

### 3 服务器端响应的数据格式

在实际项目中，服务器端大多数情况下会以JSON对象作为响应数据的格式。

在http请求与响应的过程中，无论是请求参数还是响应内容，如果是对象类型，都会被转换为对象字符串进行传输。

### 4 XML简介

XML可扩展标记语言，被设计用于传输和存储数据。

> XML和HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，都是自定义标签。
>
> 一个学生数据:
>
> name="孙悟空";age=18;gender="男";
>
> 用XML表示：
>
> ```xml
> <student>
>     <name>孙悟空</name>
>     <age>18</age>
>     <gender>男</gender>
> </student>
> ```
>
> 现在已被JSON取代。
>
> 用JSON表示：
>
> ```json
> {"name":"孙悟空","age":"18","gender":"男"}
> ```

### 5 AJAX的特点

#### 	5.1 AJAX的优点

	1) 可以无需刷新页面与服务器端进行通信。
	1) 允许根据用户时间来更新部分页面内容。

#### 	5.2 AJAX的缺点

	1.  没有浏览历史，不能回退
	2.  存在跨域问题
	3.  SEO不友好

### 6 请求传递参数

传统网站通过表单form提交，GET请求参数会被拼接到请求地址（url）后，POST请求参数会被放在请求体（send()方法内）当中。

在Ajax中，

- GET请求方式

  ```js
  xhr.open('get','http://www.example.com?name=zs&age=20')
  ```

- POST请求方式
  
  1. application/x-www-form-urlencoded方法
  
     ```js
     xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
     xhr.send('name=zs&age=20')
     ```
  
  2. application/json 方法
  
     ```js
     xhr.setRequestHeader('Content-Type', 'application/json')
     xhr.send(JSON.stringify({name:'zx',age:50}))
     // JSON.stringify() 方法将一个JavaScript对象或值转换为JSON字符串。
     ```
  
  在服务器端，要设置中间件来解析传递指定格式的请求数据。
  
  application/x-www-form-urlencoded格式对应的是：app.use(express.urlencoded({extended: ture}));
  
  application/json格式对应的是：app.use(express.json())

### 7 请求报文

在HTTP请求和响应的过程中传递的数据块叫做报文，包括传递的数据以及一些附加信息，并要遵守规定好的格式

### 8 请求参数的格式

1. application/x-www-form-urlencoded

   ```
   name=zhangsan&age=20&sex=男
   ```

2. application/json

   ```
   {name: 'zhangsan', age: '20', sex: '男'}
   ```

   在请求头中指定Content-Type属性的值时application/json，告诉服务器端当前请求参数的格式是json。

   ```js
   JSON.stringify() // 将json对象转换为json字符串
   ```

   **注意：get请求不能提交json对象数据格式，传统网站的表单提交也不支持json对象数据格式**

### 9 获取服务器端的响应(淘汰，仅做了解)

```js
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        // ...
    }
}
```



### 10 Ajax错误处理

- Ajax状态码：表示Ajax请求的过程，为Ajax对象返回
- Http状态码：表示请求的处理结果，为服务器端返回

### 11 Ajax封装

```js
ajax({
    type:'get',
    url: 'http://www.example.com',
    success: function (date) {
        console.log(date);
    }
})
```

将请求参数传递到ajax函数内部，要根据请求方式的不同将请求参数放置在不同的位置

- get：  放在请求地址的后面
- post：放在send方法中

1. 请求格式参数的问题
   application/x-www-form-urlencoded
       参数名称=参数值&参数名称=参数值
   application/json
       {name: 'zhangsan', age: 20}
2. 传递对象数据类型对于函数的调用者更友好
3. 在函数内部对象数据类型转换为字符串较为容易

回顾：使用Ajax技术向服务器端发送请求时，服务器端一般都返回JSON类型的数据，但客户端拿到的通常是一个JSON字符串，如果想要使用该JSON数据，则要将JSON字符串转换成JSON对象，针对此操作，希望封装于函数当中，那么函数的调用者就不需要关心是否是JSON对象。

​	在定义上述函数时，无法确定服务器端返回的数据类型，所以要使用xhr.getResponseHeader()方法来获取服务器端返回的数据。

### 12 art-template模板引擎使用步骤（可能已淘汰）

1. 下载 art-template 模板引擎库文件并在HTML页面中引入库文件

   ```html
   <script src="/js/art-template-web.js"></script>
   ```

2. 准备 art-template 模板引擎

   ```html
   <script id="tpl" type="text/html">
   	<div class="box"></div>
   </script>
   ```

   

3. 告诉模板引擎将哪一个模板和哪一个数据进行拼接

   ```js
   let html = template('tp1', {username: 'zhangsan', age: '20'})
   ```

   

4. 将拼接好的HTML字符串添加到页面中

   ```js
   document.getELementById('container').innerHTML = html
   ```

   

5. 通过模板语法告诉模板引擎，数据和HTML字符串要如何拼接

   ```html
   <script id="tp1" type="text/html">
   	<div class="box">{{username}}</div>
   </script>
   ```

   

### 13 req.params、req.query和req.body 三者区别

**req.params,req.query是用在get请求当中，而req.body是用在post请求中的**

### 14 FormData

#### **1. FormData对象的作用**

1. 模拟HTML表单，相当于将HTML表单映射成表单对象，自动将表单对象中的数据拼接成请求参数的格式。
2. 异步上传二进制文件（如图片、视频文件）

#### **2. FormData对象的使用**

1. 准备 HTML 表单

   ```html
   <form id='form'>
       <input type="text" name="username" />
       <input type="password" name="password" />
       <input type="button" />
   </form>
   ```

2. 将 HTML 表单转化为 formData 对象

   ```js
   let form = document.getElementById('form');
   let formData = new FormData(form);
   ```

3. 提交表单对象

   ```js
   xhr.send(formData);
   ```

   **Note: **formData对象不能用于 GET 请求，因为此对象需被放置在 send() 方法中， GET 请求方式的请求参数只能放置在请求地址的后面 
   
4. formidable模块
   由于bodyparser模块**不能处理**客户端向服务器端发送的formData对象，改用 formidable 模块（A Node.js module for parsing form data, especially file uploads.）
   包管理npm主页：https://www.npmjs.com/package/formidable
   在Express下的使用方式：

   ```js
   const express = require('express')
   const formidable = require('formidable')
   
   const app = express()
   
   app.post('/formData', (req, res) =>{
       // const form = formidable({multiples: true})
       const form = new formidable.IncomingForm()
       form.parse(req, (err, fields, files) => {
           if (err) throw err('error!')
           // ...
           res.json({fields, files})
           // res.send(fields)
       })
   })
   app.listen(3000, ()=>{
       // ....
   })
   ```

#### **3. FormData 对象的实例方法**

1. 获取表单对象中属性的值

   ```js
   formData.get('key')
   ```

2. 设置表单对象中属性的值

   ```js
   formData.set('key', 'value')
   ```

3. 删除表单对象中属性的值

   ```js
   forData.delete('key')
   ```

4. 向表单对象中追加属性值

   ```js
   formData.append('key', 'value')
   ```

5. 注意事项
   set 方法 与 append 方法的区别是，在属性名已存在的情况下， set 会覆盖已有键名的值，append会保留两个值。

#### **4. FormData 二进制文件上传**

```html
<input type="file" id="file" />
```

```js
let file = document.quertSelector('.file')
file.onchange = function() {
    // 创建空 FormData 对象
    let formData = new Formdata()
    // 将用户选择的二进制文件追加到表单对象中
    formData.append('attrname', this.files[0])
    // 配置ajax 对象，请求方式必须为 POST
    xhr.open('post', 'www.example.com');
    xhr.send(formData);
}
```

#### **5. FormData 文件上传进度展示**

新版本的XMLHttpRequest 对象中 ，可以通过监听xhr.upload.onprogress 事件，来获取到文件的上传进度，具体的语法格式如下：

```js
let xhr = new XMLHttpRequest();
xhr.upload.onprogress = function(e) {
    // e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算的长度
    if (e.lenghtComputable) {
        // e.loaded ：已传输的字节
        // e.total : 需传输的总字节
        let percentComplete = Math.ceil((e.loaded / e.total) * 100);
    }
}
```



```js
// 当用户选择文件的时候
file.onchange = function() {
	// 文件上传过程中持续触发onprogress事件
	xhr.upload.onprogress = function (ev) {
        bar.style.width = (ev.loaded / ev.total) * 100 + '%'
    }
}
```

#### **6. FormData 文件上传图片即时预览**

```js
// 在xhr.onload() 事件中
let result = JSON.parse(xhr.responseText)
let img = document.createElement('img')
img.src = result.path
img.onload = function() {
    chooseBox.appendChild(img)
}
```

#### 7.  阻止form表单的默认提交事件

HTML中的 form表单标签，一点击提交按钮（类型为submit）会跳转页面，如果表单的action 为空也会跳转到自己的页面，即效果为刷新当前页面。

以下几种阻止表单的默认提交事件方法：

1. 将 <input> 标签内按钮类型从 type="submit" 修改为 type="button"
2. 表单内 <button> 未指定类型时，默认的类型为 submit，可以显式的修改为 <button type='button'>
3. 利用JavaScript DOM中的 preventDefault()方法来阻止

### 15 onload() 事件与 onreadystatechange() 事件的区别

1. 兼容性
   IE的script元素只支持onreadystatechange，不支持onload

2. XHMHttpRequest.onreadystatechange
   只要 readyState 属性发生变化，就会调用相应的处理函数。这个回调函数会被用户线程所调用。XHMHttpRequest.onreadystatechange 会在 XMLHttpRequest 的 readyState 属性发生改变时触发 readystatechange。
   当XMLR请求 被 abort() 方法取消， 对应的 readystatechange 事件不会被触发

3. XMLHttpRequest.readyState
   **XMLHttpRequest.readyState** 属性返回一个 XMLHttpRequest 代理当前所处的状态。一个 XHR 代理总是处于下列状态中的一个：

4. | 值   | 状态               | 描述                                                |
   | ---- | ------------------ | --------------------------------------------------- |
   | `0`  | `UNSENT`           | 代理被创建，但尚未调用 open() 方法。                |
   | `1`  | `OPENED`           | `open()` 方法已经被调用。                           |
   | `2`  | `HEADERS_RECEIVED` | `send()` 方法已经被调用，并且头部和状态已经可获得。 |
   | `3`  | `LOADING`          | 下载中；`responseText` 属性已经包含部分数据。       |
   | `4`  | `DONE`             | 下载操作已完成。                                    |

5. 事件调用方式

   ```js
   xhr.onload = function(){
       if (xhr.status == 200){
           console.log(xhr.responseText)
       }
   }
   ```

   ```js
   xhr.onreadystatechange = function(){
       if (this.readyState == 4 && this.status === 200){
           console.log(xhr.status);//状态码
           console.log(xhr.statusText);//状态字符串
           console.log(xhr.getAllResponseHeaders());//所有响应头
           console.log(xhr.response);//响应体
           console.log(xhr.responseText)
       }
   }
   ```

### 16 原生JS设置允许跨域方法

   在路由配置模块中设置响应头 设置允许跨域

   ```js
   res.setHeader('Access-Control-Allow-Origin', '*')
   ```

   

### 17 同源策略

一、**同源策略（Same-Origin policy）**，是浏览器的一种安全策略。

1. 同源（即url相同）：协议、域名、端口号 须完全相同。
2. 跨域：违背了同源策略，即跨域。
3. ajax 请求是遵循同源策略的。

二、解决跨域（JSONP、CORS）

1. 非官方解决途径JSONP
   （1）JSONP
   JSONP（JSON with Padding），是一个非官方的跨域解决方法，**只支持get请求**。
   （2）JSONP工作原理
   利用script的路径src属性作为请求路径，只需要服务端 返回的数据封装成 js代码。因为src属性在引入外部数据时不受同源策略的约束。
   例：

   ```js
   // 服务端处理
   app.get('/jsonp', (req, res) => {
       res.send('console.log("hello world")')
   })
   
   ```

   ```html
   <!-- 客户端处理 -->
   <script src-"http://127.0.0.1:9000/jsonp"></script>
   ```

2. 官方解决途径 CORS
   （1）CORS: Cross-Origin Resource Sharing 跨域资源共享, 即服务端设置响应头是允许跨域的
   （2）CORS的MDN文档：[跨源资源共享（CORS） - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)

   ```js
   res.setHeader('Access-Control-Allow-Origin','*')
   ```

   

### 18 JSON和JS 对象的互转

实现从 JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法：

```js
let obj = JSON.parse('{"a":"Hello", "b":"World"}')
// 结果是 {a:'Hello', b:'World'}
```

实现从 JS 对象转换为 JSON字符串，使用 JSON.stringify() 方法：

```js
let json = JSON.stringify({a:'Hello', b:'World'})
// 结果是 {"a":"Hello", "b":"World"}
```

Note：把数据对象转换为字符串的过程，叫做序列化；把字符串转换为数据对象的过程，叫做反序列化。

### 19 Axios

Axios是专注于**网络数据请求**的库。

相比于原生的XMLHttpRequest对象， axios简单易用。

相比于jQuery，axios更加轻量化，因其只专注于网络数据请求。

#### 1. axios发起GET请求

```js
axios.get('url', {params:{ /*参数*/ }}).then(callback);
```

具体的请求示例如下：

```js
// 请求的 URL 地址
const url = 'http://www.example.com:3000/get';
// 请求的参数对象
let paramsObj = { name: 'zs', age: 20};
// 调用axios.get() 发起GET请求
axios.get(url, {params:paramsObj}).then(function(res) {
    let result = res.data;
    console.log(res);
})
```

注意：res对象并不是服务器响应的真实数据，为axios模块包包装的对象。包含六个属性：

- config
- data
- header
- request
- status
- statusText

其中只有 res.data 为服务器返回的真正的数据。

#### 2. axios 发起POST请求

```js
axios.post('url',{/*参数*/}).then(callback);
```

#### 3. 直接使用axios发起请求

axios也提供了类似于jQuery中 $.ajax() 的函数，语法如下：

```js
axios({
    method: '请求类型',
    url: '请求的URL地址',
    data: { /* POST数据 */ }，
    params: { /* GET参数 */ }
}).then(callback)
```

axios中的.then() 为 ES6中的 Promise对象。后期学习

### 20 HTTP

**HTTP请求消息的组成部分**

1.请求行

2.请求头部

3.空行（回车符 或 换行符）

4.请求体

请求体中存放的，是要通过POST方式提交到服务器的数据。注意：只有POST 请求才有请求体，GET请求没有请求体！

**HTTP响应消息**

响应消息是服务器给客户端的消息内容，也叫作响应报文。

HTTP响应消息由 状态行、响应头部、空行和响应体4个部分组成。

1. 状态行
   状态行由 HTTP 协议版本、状态码和状态码的描述文本 3 个部分组成，它们之间使用空格隔开；
2. 响应头部
   响应头部用来描述服务器的基本信息，由多行 键/值对 组成，键与值之间用英文的冒号分隔。
3. 空行
4. 响应体
   响应体中存放的是服务器给客户端的资源内容。

**HTTP响应状态码**

HTTP 状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字用来对状态码进行细分。

| 分类 | 分类描述                                                     |
| ---- | ------------------------------------------------------------ |
| 1**  | 信息，服务器收到消息，需请求者继续执行操作（实际开发很少用） |
| 2**  | 成功，操作被成功接收并处理                                   |
| 3**  | 重定向，需要进一步的操作以完成请求                           |
| 4**  | 客户端错误，请求包含语法错误或无法完成请求                   |
| 5**  | 服务器错误，服务器在处理请求的过程中发生了错误               |

1.  2** 成功相关的响应状态码

   | 状态码 | 状态码英文名称 | 中文描述                        |
   | ------ | -------------- | ------------------------------- |
   | 200    | OK             | 请求成功。一般用于GET与POST请求 |
   | 201    | Created        | 已创建。常用语POST与PUT请求     |

2.  3** 重定向相关的响应状态码

   | 状态码 | 状态码英文名称    | 中文描述                                                     |
   | ------ | ----------------- | ------------------------------------------------------------ |
   | 301    | Moved Permanently | 永久移动。请求的资源已被永久地移动到新的URI，浏览器会自动定向到新URI |
   | 302    | Found             | 临时移动。                                                   |
   | 304    | Not Modified      | 未修改。所请求的资源未修改，服务器返回次状态码，不会返回任何资源。 |

3.  4** 客户端错误相关的响应状态码
    4** 范围的状态码，表示客户端的请求有非法内容，导致失败。

   | 状态码 | 状态码英文名称  | 中文描述                           |
   | ------ | --------------- | ---------------------------------- |
   | 400    | Bad Request     | 1. 语义错误；2. 请求参数有误。     |
   | 401    | Unauthorized    | 当前请求需要用户验证               |
   | 403    | Forbidden       | 服务器已理解请求，但是拒绝执行它   |
   | 404    | Not Found       | 服务器无法根据客户端的请求找到资源 |
   | 408    | Request Timeout | 请求超时。                         |

4.  5** 服务端错误相关的响应状态码

   | 状态码 | 状态码英文名称        | 中文描述                                                     |
   | ------ | --------------------- | ------------------------------------------------------------ |
   | 500    | internal server error | 服务器内部错误，无法完成请求。                               |
   | 501    | not implemented       | 服务器不支持该请求方式。只有GET和HEAD请求方式要求每个服务器必须支持，其他请求方式在不支持的服务器上会返回501 |
   | 503    | service unavailable   | 由于超载或系统维护，暂时无法处理客户端的请求。               |

   
