## Webpack加载静态文件

### 一、加载css文件

> 在使用css文件的时候， 需先用npm安装对应的Loader，然后在config中配置对象的loader

style.css:

```css
body {
	background-color: red
}
```

1. 安装 css-loder和style-loader

   ```
   npm install style-loader css-loader--save-dev
   ```

2. 在config文件中配置loader

   在webpack.config.js的module中加入以下语句:

   ```javascript
   module：{
   	rules: [
   		{
               test: /\.css$/,
               //下面的顺序不可更改，加载顺序为从右到左， css-loader需先加载
               use: ["style-loader", "css-loader"]
           },
   	]
   }
   ```


### 二、加载less文件

> 在使用less文件的时候， 需要先用npm安装less-loder， 并在config的module中配置

font.less:

```less
@fontSize:30px;
@fontColor: #786fa6;

body {
    font-size: @fontSize;
    color: @fontCoor;
}
```

1. 安装less-loader

   ```
   npm install less-loader--save-dev
   ```

2. 在config文件中配置loader

   ```javascript
   {
       test: /\.less$/,
       use: [
           {
               loader: "style-loader" // creates style nodes from JS strings
           },
           {
               loader: "css-loader" // translates CSS into CommonJS
           },
           {
               loader: "less-loader" // compiles Less to CSS
           }
       ]
   },
   ```

### 三、加载图片文件

> 在使用图片文件的时候，需要安装file-loader和url-loader两个loader，用以加载不同情况的图片

1. 安装file-loader与url-loader

   ```
   npm install file-loader url-loader--save-dev
   ```

2. 在config中配置loader

   limit:用来指定图片大小， 默认为8192，单位为字节，

   当加载的图片大小小于等于limit值时， 使用的是url-loader，

   当图片大小大于limit值时，使用file-loader， 若未安装file-loader会报错，

   ```javascript
   {
       test: /\.(png|jpg|gif|jpeg)$/,
       use: [
           {
           	loader: "url-loader",
           	options: {
           		limit: 8192
                   //name: "img/[name].[hash:8].[ext]"
           	}，
               
           }
       ]
   },
   ```

3. 修改图片在dist文件中的名称

   当解析图片时，webpack会默认把图片名称解析成base64编码的名字， 为了保证图片名称的唯一性，但是如此一来图片名将无法辨别，为了区分图片的名称，可保留原有名称再加上8位的base64编码，需在配置中添加name属性, 一定要放在options属性下。

   [name]:  必须加中括号， 代表名称变量，动态获取文件名称

   [hash:8]: 必须加中括号,  代表截取hash的前8位

   [ext]: 必须加中括号， 代表后缀变量， 动态获取图片的后缀名。

   ```
   name: "img/[name].[hash:8].[ext]"
   ```

   

### 四、在index.js中引用静态文件

1. 加载css文件

   ```javascript
   require('./css/style.css')
   ```

2. 加载less文件

   ```javascript
   require('./css/font.less')
   ```

3. 在css文件中引用图片

   ```css
   body {
       background: url('../img/bg.jpg') no-repeat;
       background-size: cover;
   }
   ```

   

