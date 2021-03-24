## Web_开发规范

Last edited by **曾华智** 1 year ago

[Page history](http://192.168.0.176:9000/dev_group/dev_rule/dev_rule/wikis/Web_开发规范/history)

## 一．前端技术选型

### 1.1开发环境：

nodejs @10.15.3 npm @6.4.1

### 1.2 开发工具：

VSCodeUserSetup-x64-1.33.1

### 1.3 版本管理工具：

Git-2.21.0-64

### 1.4前端代码打包工具：

Webpack @3.6.0

Node-sass @4.12.0 sass-loader @7.1.0 scss-loader @0.0.1 ...

### 1.5前端框架选型：

Vue @2.5.2(采用vue-cli 2x 构建前端vue开发打包环境，不使用vue-cli 3以上 版本构建开发环境)

### 1.4 前端开发插件：

前端UI采用element-ui@2.2.2

前端数据管理采用vuex@3.1.1

前端路由管理采用vue-router@2.0.3

前端图片懒加载采用 vue-lazy@1.0.1

前端发送异步请求采用 axios@0.18.0

### 1.5前端样式技术选型

scss模块化开发

### 1.6前端代码调试工具：

chrome等插件

### 1.7 前端接口调试工具：

server-json, postman

### 1.8 前端静态资源服务管理：

cdn管理待定

### 1.9 前端单元测试 ：

待定

## 二.目录构建规范

### 前端目录构建规范

1.1根目录（src）结构按职能划分

assets//静态文件目录

compoents//存放与网站业务逻辑无关的公共基本组件

layout//存放与网站公共布局的单例组件

view//存放与网站展示页紧密性解耦的父子组件

router//配置网站路由的目录

store//配置网站前端数据管理的vuex目录

**Src**

└── **assets**//静态文件目录

```
 └── image 图片目录  

 └──Style 样式目录

     ├── reset.css//全局样式

 └── js javascript 目录

     ├── axios.js//二次封装的axios
```

└── **compoents** //该目录存放与网站业务逻辑无关的组件

```
     ├── VLong.vue//加载组件

     ├── VNotification.vue//弹框组件
```

└── **layout** //该目录防止与页面公共布局的单例组件

```
     ├── TheHeader.vue

     ├── TheFooter.vue
```

└── **view** //前端网站页面模板组件目录放置与展示页面紧密性解耦的子组件

```
└── home //网站首页组件目录

    ├── index.vue//index.vue为在该显示页面的入口组件

    ├── HomeHeader.vue

    ├──HomeFooter.vue

└──detail //网站首页组件目录

   ├── index.vue//index.vue为在该显示页面的入口组件

   ├── DetailHeader.vue

   ├── DetailFooter.vue
```

└──**router** //配置网站的路由的目录

└──**store**//配置网站的vuex数据管理的目录

```
├──index.js //整个store的导出文件

└──Home //管理首页网站的数据目录

    ├──state.js

    ├──getters.js

    ├──mutations.js

    ├──actions.js

    ├──index.js//该模块的导出文件
```

## 三.代码规范

### Vue规范

vue文件基本结构

```
        <template>
          <div>
            <!--必须在div中编写页面-->
          </div>
        </template>
        <script>
          export default {
            components : {
            },
            data () {
              return {
              }
            },
            methods: {
            },
            mounted() {

            }
         }
        </script>
        <!--声明语言，并且添加scoped-->
        <style lang="less" scoped>
        </style>
```

vue文件方法声明顺序

```
    - components   
    - props    
    - data     
    - created
    - mounted
    - activited
    - update
    - beforeRouteUpdate
    - metods   
    - filter
    - computed
```

**1.组件的命名：**

只要有能够拼接文件的构建系统，就把每个组件单独分成文件。

当你需要编辑一个组件或查阅一个组件的用法时，可以更快速的找到它。

**基础组件名**

应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，在这里采用V+””

└── Compoents //该目录存放与网站业务逻辑无关的组件

```
 ├── VLong.vue//加载组件
```

**单例组件名**

只应该拥有单个活跃实例的组件应该以 The 前缀命名，以示其唯一性。这不意味着组件只可用于一个单页面，而是每个页面只使用一次。这些组件永远不接受任何 prop，因为它们是为你的应用定制的，而不是它们在你的应用中的上下文。如果你发现有必要添加 prop，那就表明这实际上是一个可复用的组件，只是目前在每个页面里只使用一次。

└── layout //该目录防止与页面公共布局的单例组件

```
 ├── TheHeader.vue  单例组件名

 ├── TheFooter.vue
```

**紧密耦合的组件名**

和父组件紧密耦合的子组件应该以父组件名作为前缀命名。如果一个组件只在某个父组件的场景下有意义，这层关系应该体现在其名字上。因为编辑器通常会按字母顺序组织文件，所以这样做可以把相关联的文件排在一起。

└── home //网站首页组件目录

```
  ├── HomeHeader.vue
```

**组件的定义，声明，引用**

1.每个Vue组件在定义的时候需要添加name属性代表该组件的名称,组件名为多个单词组合，并且用连接线（-）连接，首字母小写，避免与 HTML 标签冲突，

2.组件在其他组件运用的时候组件以首字母大写的驼峰命名，组件在模板的引用横线（“-”）连接首字母大写

3.Vue组件方法的引入顺序，引入node_modules包的模块或第三方组件组件引入放在上面，自定义相对路径的组件放在下面,以免以后应用eslint报错

组件定义：

```
{name:'page-component'}
```

组件应用

```
<template><Page-Component></Page-Component></template>
import vueAwesome from 'Vue-Awesome-Swiper'//第三方组件
import PageComponent from './PageComponent.vue'//自定义组件
components:{PageComponent}
```

**子组件的data 必须是一个函数，返回值必须是一个对象**

**组件的复用与继承采用extends**

子组件应用：

**1.子组件定义 prop 的时候应该始终以驼峰格式（camelCase）命名，在父组件赋值的时候使用连接线（-）。**

```
props:articleStatus: Boolean
<article-item :article-status="true"></article-item>
```

**2.prop 的定义需要指定其类型**

反例：

```
props: ['attrM', 'attrA', 'attrZ']
```

正例：

```
props: {

    attrM: Number,

    attrA: {

        type: String,

        required: true

    },}
```

**3.父组件传递给子组件的的值，子组件接受保存，子组件只能get,不能set,子组件如要改变父组件传过来的值需要同事件派发的形式改变，采用 this.$emit(...)**

反例：

```
props:{attrM:String}
mouted(){this.attrM=c//子组件不允许直接改父组件的传递的值，vue会报warning}
```

正例：

```
mouted(){this.$emit("changeAttrM",'传递需要改变的值')}
```

**4.v-for** 在执行 v-for 遍历的时候，总是应该带上 key 值,key值不能使用index索引，需要使用后端传递过来唯一的ID或其他值，使更新 DOM 时渲染效率更高。

反例： `<li v-for="（item , index)  in list" :key='index'>`

正例：

```
<li v-for="（item , index)  in list" :key='item.id'>
```

**5.v-for 应该避免与 v-if 在同一个元素**

（例如：

）上使用，因为 v-for 的优先级比 v-if 更高，为了避免无效计算和渲染，应该尽量将 v-if 放到容器的父元素之上。)

反例：

```
<li v-for="item in list" :key="item.id" v-if="showList">  {{ item.title }}  </li>
```

正反：

```
<ul v-if="showList"><li v-for="item in list" :key="item.id" >  {{ item.title }}</ul></li>
```

**6.指令缩写**

为了统一规范始终使用指令缩写，使用v-bind，v-on并没有什么不好，这里仅为了统一规范。

```
<input :value="mazeyUser" @click="verifyUser">
```

**6. 模板中尽量不要包含表达式**

组件模板应该只包含简单的表达式，复杂的表达式则应该在computed属性中。

反例：

<div>{{firstName+lastName}}</div>

```
<!--在模板中-->
{{fullName}}


computted:{

  funllName(){

     return this.firstName+this.lastName
}
```

**7.vue-router** 考虑vue组件的复用性和操控性，vue-router 参数的传递不采用在组件内部通过this.$route.params获取路由的参数。而是可采用通过props的设置在路由组件中获取参数更有其组件灵活性。

**8.前端路由采用”history”方式进行路由跳转**

**9非 Flux 的全局状态管理**

Vue数据管理应该优先通过 Vuex 管理全局状态，而不是通过 this.$root 或一个全局事件总线，并且进行数据的模块化管理具体请参考demo

### vue组件注释规范

代码注释在一个项目的后期维护中显的尤为重要，所以我们要为每一个被复用的组件编写组件使用说明，为组件中每一个方法编写方法说明。以下情况，务必添加注释

**1.公共组件使用说明**

**2.各组件中重要函数或者类说明**

**3.复杂的业务逻辑处理说明**

**4.特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的hack、使用了某种算法或思路等需要进行注释描述**

5.`注释块必须以/**（至少两个星号）开头**/`

**6.单行注释使用//；**

例子：

**单行注释**

普通方法一般使用单行注释// 来说明该方法主要作用

**多行注释**

组件使用说明，和调用说明

`<!--公用组件：数据表格      /**      * 组件名称      * @module 组件存放位置      * @desc 组件描述      * @author 组件作者      * @date 2017年12月05日17:22:43      * @param {Object} [title]    - 参数说明      * @param {String} [columns] - 参数说明      * @example 调用示例      *  <hbTable :title="title" :columns="columns" :tableData="tableData"></hbTable>          */       -->`