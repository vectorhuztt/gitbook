## Webpack配置本地服务器

> 配置本地器的目的是可以在修改代码的同时页面可以实时显示，不需要每次都运行npm run build

### 1、安装webpack-dev-server

> 安装的webpack-dev-server的版本必须要和webpack版本一致
>
> 本次使用的webpack版本为3.6.0， 对应的web-dev-server为2.9.1

```
npm install webpack-dev-server@2.9.1
```

### 2、配置实时显示的文件目录

在config.js添加一下代码

contentBase: 实时显示的文件夹目录

inline: 是否实时显示

port：本地访问端口， 默认为8080

```
devServer: {
    contentBase: "./dist",
    inline: true，  
    port: 8080
}
```

### 3、配置webpack-dev-server命令

安装后，直接使用webpack-dev-server是无法使用的， 因为默认是使用全局的命令。此时需要在pakage.json配置本地命令，

```json
"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"build": "webpack",
	"dev": "webpack-dev-server"
},
```

之后直接使用 npm run dev 便可以驱动本地服务器，打开localhost:8080地址便可实时显示页面。