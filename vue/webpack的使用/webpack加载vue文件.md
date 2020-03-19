## Webpack加载vue文件

### 1、安装本地vue

```
npm install vue
```

### 2、安装vue-loader

```
npm install vue-loader vue-template-compiler --save-de
```

> 此处安装的vue-loader可能版本较高，可在package.json更改一下vue-loader的安装版本

更改版本方式如下：

```
1、在package.json中，找到devDependencies的vue-loader更改为
   "vue-loader": "^13.0.0",
2、重新加载 npm install
```

### 3、配置vue-loader

```javascript
{
    test: /\.vue$/,
    use: {
    	loader: "vue-loader"
    }
}
```

### 4、解决vue版本问题

通过以上配置，运行npm run build后，打开F12,会发现依然报错， 错误内容如下：

```
... You are using the runtime-only build of Vue where the template compiler is not available. Either pre-compile the templates into render functions, or use the compiler-included build.
```

此问题是因为加载的vue版本问题， 可在config中添加一句话进行更改

```javascript
resolve: {
    alias: {
    	vue$: "vue/dist/vue.esm.js"
    }
},
```

### 5、创建vue模块

app.vue:

> template: 为页面加载的模板， 取缔在index.html添加标签语言
>
> script: 类似于之前在html中写的const app = new Vue(...)
>
> style: 可对模板语言增加样式，一定要加上scoped

```vue
<template>
    <div>
        <h2 class="title">{{ message }}</h2>
        <button @clik="btnClick">按钮</button>
    </div>
</template>
<script>
export default {
    name: "app",
    data() {
        return {
            message: "Hello Vue"
        };
    },
    methods: {
        btnClick() {}
    },
    components: {
        cpn
    }
};
</script>
<style scoped>
.title {
    color: #f6b93b;
}
</style>

```

### 6、在index.js中加载vue

1. 首先需要导入vue

   ```javascript
   import Vue from "vue";   // 需要本地Vue创建vue实例
   import app from './vue/app.vue' // 加载已经创建的vue模板
   ```

2. 创建vue实例，使用模板

   ```javascript
   new Vue({
       el: '#app',
       template: '<app></app>',
       components: {
           app
       }
   })
   ```

   



