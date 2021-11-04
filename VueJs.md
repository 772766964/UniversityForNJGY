# Vue.js

### 安装(这里使用2的版本)

#### 兼容性

Vue **不支持** IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)。

#### 语义化版本控制

Vue 在其所有项目中公布的功能和行为都遵循[语义化版本控制](https://semver.org/lang/zh-CN/)。对于未公布的或内部暴露的行为，其变更会描述在[发布说明](https://github.com/vuejs/vue/releases)中。

### [Vue Devtools](https://cn.vuejs.org/v2/guide/installation.html#Vue-Devtools)

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



### [NPM](https://cn.vuejs.org/v2/guide/installation.html#NPM)

在用 Vue 构建大型应用时推荐使用 NPM 安装[[1\]](https://cn.vuejs.org/v2/guide/installation.html#footnote-1)。NPM 能很好地和诸如 [webpack](https://webpack.js.org/) 或 [Browserify](http://browserify.org/) 模块打包器配合使用。同时 Vue 也提供配套工具来开发[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)。

```
# 最新稳定版
$ npm install vue
```

### [命令行工具 (CLI)](https://cn.vuejs.org/v2/guide/installation.html#命令行工具-CLI)

Vue 提供了一个[官方的 CLI](https://github.com/vuejs/vue-cli)，为单页面应用 (SPA) 快速搭建繁杂的脚手架。它为现代前端工作流提供了开箱即用的构建设置。只需要几分钟的时间就可以运行起来并带有热重载、保存时 lint 校验，以及生产环境可用的构建版本。更多详情可查阅 [Vue CLI 的文档](https://cli.vuejs.org/)。

CLI 工具假定用户对 Node.js 和相关构建工具有一定程度的了解。如果你是新手，我们强烈建议先在不用构建工具的情况下通读[指南](https://cn.vuejs.org/v2/guide/)，在熟悉 Vue 本身之后再使用 CLI。



## Vue基本语法

v-bind:title 悬浮显示消息 `<span v-bind:title=“message”><span>`

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



## Vue绑定事件



## Vue双向绑定



## Vue组件讲解



## Axios异步通信



## 计算属性



## 插槽slot



## 自定义内容事件分发



## vue-cli



## 路由

