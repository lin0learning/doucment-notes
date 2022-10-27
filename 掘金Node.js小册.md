## Node.js

#### 1. Node.js介绍

```js
console.log(process.argv);  // demo.js
```

```bash
node demo.js "hello world"
```

process.argv 可以获得命令行调用的信息，以空格分隔。上述process.argv的值是`[node demo.js "hello world"]`



#### 2. Node.js的模块管理

*一个模块的 export default 只能导出一个默认 API。如果这个模块还有其他的 API 需要导出，那么只能使用 export。*

**注意：**

1. Node.js命名 js 模块文件不是用 `.js` 扩展名，而是用 `.mjs` 扩展名。这是因为 Node.js 目前默认用`CommonJS`规范定义 .js 文件的模块，用`ES Modules`定义 .mjs 文件的模块。如果直接将`index.mjs`文件改成`index.js`，然后运行`node index.js`，控制台上将报告错误信息。

2. 如果要用`ES Modules`定义 .js 文件的模块，可以在 Node.js 的配置文件`package.json`中设置参数`type: module`。
   ```json
   {
       "type": "module"
   }
   ```

   

3. `package.json`可以手动创建，也可以通过命令行创建。用 NPM 命令行`npm init -y`可以快速创建一个 package.json 文件.

`CommonJS`采用`module.exports/require`而`ES Modules`则采用`export/import`

import可以作为异步函数异步动态加载模块：

```js
(async function() {
    const {liclo} = require('./liclo.js')
})
```

