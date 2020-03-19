## Webpack初步使用

### 前提

​	项目结构如下：

```
project
	dist
	src
		css
		img
		js
		vue
		index.js
	index.html
```

### 1、安装本地webpack

1、首先在项目中使用npm安装本地的webpack

```
npm install webpack@3.6.0
```

安装完成后项目中会多一个node_moudles文件夹

2、使用npm初始化项目，之后问价夹会多出 package.json、package-lock.json 两个文件

```
npm init    
npm install  // 添加相应的包
```

### 2、修改package.json的script命令

使用build代替webpack命令，优先使用本地的webpack命令

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
},
```



### 3、创建webpak.config.js文件

格式如下：

```javascript
//使用nodeJs语法获取dist文件夹绝对路径
const path = require("path");
module.exports = {
  	//entry为入口文件， output为解析后的文件  
    // publicPath 定义解析后的文件路径前面都要加上dist/
    entry: "./src/index.js",
    output: {
        path: path.resolve(__dirname, "dist"),
        filename: "bundle.js",
        publicPath: "dist/"
    },
}
```

### 4、使用模块化语法，将静态文件加载在index.js

util.js:

```javascript
function add(a, b) {
    return a + b;
}
function mult(a, b) {
    return a * b;
}
export {add, mult}
```

info.js:

```javascript
export const site='doyoudo.com'
export const name= 'Doyoudo'
export let course = 'vue.js'
```

index.js:

```javascript
// 加载js中的其他js文件
// common JS 或者ES6语法都可以
import { add, mult } from "./js/util.js"
import * as info from "./js/info.js"
```

### 5、在index.html中使用解析后的js

```javascript
...
<body>
    <script src="./dist/bundle.js"></script>
</body>
```

### 6、使用npm命令构建项目

```
npm run build
```

