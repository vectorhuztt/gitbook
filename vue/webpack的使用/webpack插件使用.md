## Webpack插件使用

### 1、ES6转ES5的babel

1. 安装babel

   > 注意：babel使用7版本的,使用官方文档给的babel安装方法，会有少部分ES6语法无法被转化，这里推荐使用下面版本

   ```
   npm install babel@7 babel-core babel-preset-es2015
   ```

2. 配置babel

   ```javascript
   {
       test: /\.js$/,
       exclude: /(node_modules|bower_components)/,
       use: {
       	loader: "babel-loader",
       options: {
       	presets: ["es2015"]
       	}
       }
   }
   ```

### 2、添加头部信息插件[BannerPlugin]

> 本插件是webpack内部自带的， 所以需要在config中引入webpack

1. 在config.js的头部引入webpack

   ```javascript
   const webpack = require('webpack');
   ```

2. 在config.plugins 配置BannerPlugin

   plugins以数组形式编写。

   配置的头部文件可以任意编写

   ```javascript
   plugins: [
       new webpack.BannerPlugin('(c) Vector Hu'),
   ]
   ```

### 3、打包index.html的插件[htmlWebPackPlugin]

> 本插件不是webpack内部插件， 需要使用npm安装

1. 安装html-webpack-plugin

   ```
   npm install html-webpack-plugin --save-dev
   ```

2. 在config.js头部引用htmlWebPackPlugin

   ```javascript
   const HtmlWebpackPlugin = require('html-webpack-plugin')
   ```

3. 在config.plugin中配置htmlWebPackPlugin

   ```javascript
   plugins: [
       new HtmlWebpackPlugin({
       	template: 'index.html'
       })
   ]
   ```

   运行npm run build 

   打包后的index.html会自动加载已经解析后的boudule.js

### 4、js压缩插件(uglifyJsPlugin)

> 本插件不是webpack内部插件， 需要使用npm安装

1. 安装uglify插件，需指定版本号

   ```
   npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
   ```

2. 在config.js头部引用uglify插件

   ```javascript
   const uglifyJsPlugin = require('uglifyjs-webpack-plugin')
   ```

3. 在config.plugins配置uglifyJsPlugin

   ```javascript
    new uglifyJsPlugin()
   ```

4. 运行npm run buid， 原有的bundle.js已经被压缩一下样式：

   ```javascript
   !function(e){var t={};function n(r){if(t[r])return t[r].exports;var o=t[r]={i:r,l:!1,exports:{}};return e[r].call(o....
   ```

   

