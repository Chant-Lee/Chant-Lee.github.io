---
title: vue-router
date: 2017-06-28 11:08:25
tags:
---
### 1.入门

#### 1.1 安装使用

`$ npm install vue-router --save-dev`
### 1.1.1 使用vue-cli搭建

<!-- more -->
详情请百度vue-cli搭建

```
|-- build                            // 项目构建(webpack)相关代码
|   |-- build.js                     // 生产环境构建代码
|   |-- check-version.js             // 检查node、npm等版本
|   |-- dev-client.js                // 热重载相关
|   |-- dev-server.js                // 构建本地服务器
|   |-- utils.js                     // 构建工具相关
|   |-- webpack.base.conf.js         // webpack基础配置
|   |-- webpack.dev.conf.js          // webpack开发环境配置
|   |-- webpack.prod.conf.js         // webpack生产环境配置
|-- config                           // 项目开发环境配置
|   |-- dev.env.js                   // 开发环境变量
|   |-- index.js                     // 项目一些配置变量
|   |-- prod.env.js                  // 生产环境变量
|   |-- test.env.js                  // 测试环境变量
|-- src                              // 源码目录
|   |-- components                     // vue公共组件
|   |-- store                          // vuex的状态管理
|   |-- App.vue                        // 页面入口文件
|   |-- main.js                        // 程序入口文件，加载各种公共组件
|-- static                           // 静态文件，比如一些图片，json数据等
|   |-- data                           // 群聊分析得到的数据用于数据可视化
|-- .babelrc                         // ES6语法编译配置
|-- .editorconfig                    // 定义代码格式
|-- .gitignore                       // git上传需要忽略的文件格式
|-- README.md                        // 项目说明
|-- favicon.ico 
|-- index.html                       // 入口页面
|-- package.json                     // 项目基本信息
```


#### 1.2 router/index.js

```js
export default new Router({
  routes: [              //配置路由，这里是个数组
    {                    //每一个链接都是一个对象
      path: '/',         //链接路径
      name: 'Hello',     //路由名称，
      component: Hello   //对应的组件模板
    }
  ]
})
```

#### 1.3 router-link

* 相当于a标签

`<router-link to="/">[显示字段]</router-link>`

to：填写router/index.js文件配置的path值

### 2.配置子路由

* App.vue

* components目录

* router/index.js

```js
children:[
{path:'/',component:xxx},
{path:'xx',component:xxx},
]
//后面的子集不用加‘/’
```

### 3.传递参数

#### 3.1 name

* 有子路由的name是没用的
* `<p>{{ $router.name}}</p>`

#### 3.2 :to

**`<router-link`**`:to="{name:xxx,params:{key:value}}"`**`>`**`valueString`**`</router-link>`**

`{{$route.params.username}}`

### 4.单页面多路由区域

* 一个页面有2个以上的&lt;router-view&gt;
* 非常适合左右分栏，左边操作右边

```js
//App.vue
 <router-view ></router-view>
 <router-view name="left" style="float:left;width:50%;background-color:#ccc;height:300px;"></router-view>
 <router-view name="right" style="float:right;width:50%;background-color:#c0c;height:300px;"></router-view>
 
//router/index.js
{
  path: '/',
  name: 'Hello',
  components: {
    default:Hello,
    left:test01,
    right:test02
  }
 } 
```

### 5.利用url传递参数

* :号传递
* src/router/index.js 配置路由
* 传递的数值在 {{$route.params.showId}}
* 可以使用正则规定传递的数组 path:'/params/:showId\(\\d+\)/:name'




