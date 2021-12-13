# Vue.js

`安装(这里使用2的版本)`

#### 兼容性

Vue **不支持** IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)。

#### 语义化版本控制

Vue 在其所有项目中公布的功能和行为都遵循[语义化版本控制](https://semver.org/lang/zh-CN/)。对于未公布的或内部暴露的行为，其变更会描述在[发布说明](https://github.com/vuejs/vue/releases)中。

#### [Vue Devtools](https://cn.vuejs.org/v2/guide/installation.html#Vue-Devtools)

在使用 Vue 时，我们推荐在你的浏览器上安装 [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools)。它允许你在一个更友好的界面中审查和调试 Vue 应用。

#### [CDN](https://cn.vuejs.org/v2/guide/installation.html#CDN)

对于制作原型或学习，你可以这样使用最新版本：

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
```

对于生产环境，我们推荐链接到一个明确的版本号和构建文件，以避免新版本造成的不可预期的破坏：

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14"></script>
```

如果你使用原生 ES Modules，这里也有一个兼容 ES Module 的构建文件：

```
<script type="module">
  import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.esm.browser.js'
</script>
```

你可以在 [cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue/) 浏览 NPM 包的源代码。

#### [NPM](https://cn.vuejs.org/v2/guide/installation.html#NPM)

在用 Vue 构建大型应用时推荐使用 NPM 安装[[1\]](https://cn.vuejs.org/v2/guide/installation.html#footnote-1)。NPM 能很好地和诸如 [webpack](https://webpack.js.org/) 或 [Browserify](http://browserify.org/) 模块打包器配合使用。同时 Vue 也提供配套工具来开发[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)。

```
# 最新稳定版
$ npm install vue
```

#### [命令行工具 (CLI)](https://cn.vuejs.org/v2/guide/installation.html#命令行工具-CLI)

Vue 提供了一个[官方的 CLI](https://github.com/vuejs/vue-cli)，为单页面应用 (SPA) 快速搭建繁杂的脚手架。它为现代前端工作流提供了开箱即用的构建设置。只需要几分钟的时间就可以运行起来并带有热重载、保存时 lint 校验，以及生产环境可用的构建版本。更多详情可查阅 [Vue CLI 的文档](https://cli.vuejs.org/)。

CLI 工具假定用户对 Node.js 和相关构建工具有一定程度的了解。如果你是新手，我们强烈建议先在不用构建工具的情况下通读[指南](https://cn.vuejs.org/v2/guide/)，在熟悉 Vue 本身之后再使用 CLI。



### 遇到问题解决

###### 刷新页面闪屏

遇到这样的问题可以考虑创建一个标签，然后使用css样式显示默认为none

``` html
<style> [v-clock]{display:none;} </style>
...
<div id="app" v-clock>
    ....
</div>
```

###### computed计算属性和watch监听的区别

``` 
computed计算属性
	用来声明式描述一个值依赖了其它的值
	当在模板里把数据绑定到一个计算属性上时，Vue会在其依赖的任何值导致该计算属性改变时更新DOM。这个功能非常强大，可以让代码更加声明式、数据驱动并且易于维护

watch侦听器
	当监听的变量的值发生变化时，调用对应的方法。
	在watch里当变量的值发生变化时，就会调用变量的方法，方法里面的形参对应的是变量的新值和旧值，而计算属性computed计算的是变量依赖的值,它不能计算在变量中已经定义过的变量
```



## Vue基本语法

#### v-bind:title 悬浮显示消息 `<span v-bind:title=“message”><span>`

例如v-bind:= OR {{}} 称为指令

``` javascript
//首先我们要有一个基本架构
<div id="app">
    </div>
<script>
    var app = new Vue({
        el:'#app',
        data:{
            message:''
        }
    })
    </script>
```

`< v-if=" " 	v-else-if=" "		v-else=" "></>`

`< v-for=" item in 数组名"	v-for=" (item,index) in 数组名"></>`

``` HTML
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>
            <!-- <span v-if="ok">
                这里是正确时候的输出</span>
            <span v-else>
                这里是错误时候的输出</span> -->

            <span v-if="num==1">A</span>
            <span v-else-if="num===2">B</span>
            <span v-else=>C</span>
        </div>
        <button v-on:click="sayHi">Click me now!</button>
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                num:3,
                ok:true
            }
        })
    </script>
</body>
</html>
```



## Vue绑定事件

#### v-on 可以监听DOM事件

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div v-bind:title="message">
            这里是正确时候的输出
        </div>
        <div>
            这里是错误时候的输出
        </div>
        <button v-on:click="sayHi">Click me now!</button>
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                message:'This is Vue learn now',
            },
            methods:{
                sayHi:function(){
                    alert(this.message)
                }
            }
        })
    </script>
</body>
</html>
```

### v-bind详细

|   指令    |            作用            | 缩写形式 |
| :-------: | :------------------------: | :------: |
|  v-once   |           单元格           |          |
|  v-html   |           单元格           |          |
|  v-bind   |    为HTML标签绑定属性值    |             |
|   v-if    |          条件渲染          |               |
| v-else-if |          条件渲染          |                  |
|  v-show   |    拥有切换DISPLAY的值     |                  |
|   v-for   |          遍历数组          |                 |
|   v-on    |       为HTML绑定事件       |                  |
|  v-model  | 表单元素上创建双向数据绑定 |                 |

## 数组

| 方法名 | 简述 |
| :-------------: | :------------------------: |
| push() | 往数组最后面添加一个元素，成功后返回当前数组的长度 |
| pop() |  删除数组的最后一个元素，成功后返回删除元素的值 |
| shift()  | 删除数组的第一个元素，成功后返回删除元素的值 |
| unshift() | 往数组最前面添加一个元素，成功后返回当前数组的长度 |
| splice() | 第一个参数是想要删除的／元素下标（必选），第二个参数是想要删除的个数（必选），第三个参数是删除后想要在原位置替换的值sort() |
| sort() |  使数组按照字符编码默认从小到大排序,成功返回排序后的数组reverse() |
| reverse() | 将数组倒序，成功后返回倒序后的数组 |

## Vue双向绑定

####  v-model

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>
            <span>请输入用户名:</span>
            <input type="text" value="" v-model="message"/>{{message}}
        </div>
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                message:'',
            },
        })
    </script>
</body>
</html>
```

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>
            <input type="radio" name="sex" value="男" v-model="message"/>男
            <input type="radio" name="sex" value="女" v-model="message"/>女
            {{message}}
        </div>
            
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                message:'',
            },
        })
    </script>
</body>
</html>
```

``` html 
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>
            <select v-model="message">
                <option value="" disabled>--请选择--</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
            {{message}}
        </div>            
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                message:'',
            },
        })
    </script>
</body>
</html>
```



## Vue组件讲解

#### 什么是组件

组件就是可复用的vue实例，往白了说就是一组可以重复使用的模板，类似JSTL的自定义标签,Thymeleaf 的 th:fragment

#### 第一个Vue组件

一般通过vue-cli 创建.vue 模板文件的方式开发。接下来只展示什么是组件

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <ming></ming>
    </div>
    <script>
        // 定义一个Vue组件Component
        Vue.component("ming",{
            template:"<h1>这里是模板</h1>"
        })
        var app = new Vue({
            el:'#app',
            data:{
                message:'',
            },
        })
    </script>
</body>
</html>
```

#### 第二个Vue组件

这个有点不太好理解，步骤如下：

贴上CDN

``` html
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
```

创建一个根部div的id：app

``` html
    <div id="app">
    </div>
```

老步骤的new Vue,创建一个为了学习用的数组arrays

``` html
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                arrays:["java","linux","c++","c","python"]
            }
        })
    </script>
```

创建Vue组件rong,设置模板，从父级拿值

```html
        Vue.component("rong",{
            props:["xing"],
            template:"<h1>{{xing}}</h1>"
        })
```

在根部div中引用,v-for循环输出, v-bind:XXX 缩写 :XXX

``` html
    <div id="app">
        <rong v-for="item in arrays"
        :xing="item"></rong>
    </div>
```

最后完整文件

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <rong v-for="item in arrays"
        :xing="item"></rong>
    </div>
    <script>
        Vue.component("rong",{
            props:["xing"],
            template:"<h1>{{xing}}</h1>"
        })
        var app = new Vue({
            el:'#app',
            data:{
                arrays:["java","linux","c++"
                ,"c","python"]
            }
        })
    </script>
</body>
</html>
```

有点不太好理解，但是仔细想想，如果想要父组件往子组件传值或者子组件往父组件传值该怎么办呢？

`父组件通过 props 向下传递数据给子组件Axios异步通信，子组件通过 events 给父组件发送消息`

## Axios异步通信

#### How to install

`npm install --save axios vue-axios`

And in your entry file:

``` vue
import Vue from 'vue'

import axios from 'axios'

import VueAxios from 'vue-axios'

Vue.use(VueAxios,axios)
```

#### 为什么使用 Axios

由于Vue.js是一个视图层框架，作者（尤雨溪）严格遵守SoC（关注度分离原则），所以Vue.js不包括AJAX的通信能力。2.0版本之前作者单独开发了vue-resource的插件，但是因为操作Dom太过麻烦。

#### 第一个Axios 应用程序

引入js文件，分别是vue，axios的

`    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>`

`<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

老样子，写出div配上id：app，以及vue实例

``` html
```

mounted()，在Vue的生命周期中，这个方法过去就是渲染了，该方法在整个周期中只会执行一次

``` html
<!DOCTYPE html>
<html>
<head>
    <title>This Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>
<body>
    <div id="app">
        <div v-for="item in info">
            <span>{{item}}</span>
        </div>
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data(){//data 属性 vm , data()是函数
                return{// 请求返回的参数必须与json格式一致,可不写，但不能写错
                    info:[]
                }},
            mounted(){//钩子函数，链式编程
            // mounted函数在整个实例中只会执行一次
            // 一般用来请求Ajax数据
                axios.get('http://118.25.42.197:9930/api/movies/categories').then(response=>(console.log(response.data)));
                axios.get('http://118.25.42.197:9930/api/movies/categories').then(response=>(this.info=response.data));
            }
        })
    </script>
</body>
</html>
```

安装：npm install axios -S

导入：import axios from 'axios'

请求方法：get、delete、post、put、patch。。

get:通过URL或者params选项传参

delete:删除数据，传参格式与get相同

post:提交数据，

+ 通过选项传参数，默认是json格式
+ 通过URLSearchParams传递表单参数

axios请求方法：

axios(config):通用的发送任意类型请求的方式

axios(url[,config]):可以指定url发送get请求

方法有很多，下个方法是通用的

``` vue
this.$axios({
	method:'get',
	url:'/api/get',	
	params:{
		id:12
	}
}).then(res=>{
	this.message=res.data
})
```



## 计算属性

#### 什么叫计算属性

属性是一个名词，计算是一个动词。简单来说就是将计算结果缓存的一个过程

每一次调用方法都会需要进行计算，既然有计算那就有计算过程，必定产生系统开销；如果这个结果不需要经常变化，则可以选择将不常变化的结果缓存起来。

使用computed，如果在这里的方法和methods中的重名，methods的优先级高。

computed中的方法使用不需要加（），而methods中的方法需要使用

## 插槽slot



## 自定义内容事件分发



## vue-cli

vue脚手架，快速生成vue模板。

vue入口在main.js

build目录用来构建，build.js用来构建一些消息 

## webpack的学习使用

webpack打包工具，将ES6部署成ES5。

举例：

——hello.js

``` vue
暴露一个sayHi方法
exports.sayHi = function sayHi(){
    document.write("hhhh");
}
```



——main.js

``` vue
var hello = require('./hello');
hello.sayHi();
```



——webpack.config.js 设置打包配置

``` vue
module.exports = {
    entry:'./module/main.js',
    output:{
        filename:"./js/bundle.js",
    }
}
之后在当前路径下cmd，打出webpack
```



——index.html 最后在HTML中引用即可

``` html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>t</title>
    </head>
    <body>
        <script src="dist/js/bundle.js"></script>
    </body>
</html>
```



## vue-router路由

``` vue
<router-link to=""></router-link>
<router-view></router-view>
```

首先需要安装路由

`npm install vue-router --save-dev`

写几个模块

——Main.vue

``` vue
 <template>
    <h2>这里是首页</h2>
</template>

<script>
  export default {
    name : 'Main'
  }
</script>
```

——About.vue

``` vue
 <template>
    <h2>关于我</h2>
</template>

<script>
  export default {
    name : 'About'
  }
</script>
```

定义一个router文件夹，专门存放路由

**方法一**

``` vue
import VueRouter from 'vue-router'

Vue.use(Router)

const routes = [
  {
    // 路由路径 后端@RequestMapping
    path: '/component',
    //路由名字
    name: 'component',
    // 跳转的组件
    component: Component
  },
  {
    path:'/main',
    name:'main',
    component:Main
  }
]

const router = new VueRouter({
  routes
})
//暴露方法
export default router
```

**方法二**

``` vue
export default new VueRouter({  
  routes: [
    {
      path:'/main',
      name:'main',
      component:Main
    },
    {
      path:'/About',
      name:'about',
      component:About
    }
  ]
})
```

在App.vue中添加路由本课题前两行所写

``` vue
    <router-link to="/main">首页</router-link>
    <router-link to="/about">关于我</router-link>
    <router-view></router-view>
```

前者引入，类似HTML标签<a>

后者则是展示页面类似搭配<a>的框架标签

最后在main.js中渲染，配置路由

``` vue
new Vue({
  // 配置路由
  router,
  render: h => h(App)
}).$mount('#app')
```



## vue+elementUI

### 安装

#### [¶](https://element.eleme.cn/#/zh-CN/component/installation#npm-an-zhuang)npm 安装(推荐)

推荐使用 npm 的方式安装，它能更好地和 [webpack](https://webpack.js.org/) 打包工具配合使用。

```shell
npm i element-ui -S
```

#### [¶](https://element.eleme.cn/#/zh-CN/component/installation#cdn)CDN

目前可以通过 [unpkg.com/element-ui](https://unpkg.com/element-ui/) 获取到最新版本的资源，在页面上引入 js 和 css 文件即可开始使用。

```html
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

我们建议使用 CDN 引入 Element 的用户在链接地址上锁定版本，以免将来 Element 升级时受到非兼容性更新的影响。锁定版本的方法请查看 [unpkg.com](https://unpkg.com/)。

#### 安装SASS 加载器

`cnpm install sass-loader node-sass --save-dev`

## 路由嵌套



## 参数传递及重定向



## 404和路由钩子



##　Vue数据状态管理

### `一个实现组件之间状态共享和状态变更的Vue插件`

