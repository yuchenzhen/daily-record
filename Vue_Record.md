# Vue.js学习

| Vue               |                     |                                          |
| :---------------- | :-----------------: | :--------------------------------------- |
| **数据绑定语法**        |                     |                                          |
| ├ **插值**          |         文本          | {{ mesg }}                               |
| │                 |                     | {{ * mesg}}  只处理单次插值，少用                  |
| ├ **过滤器**         |                     | {{ mesg \| capitalize }}                 |
| │                 |        串联过滤器        | {{ mesg\| filterA \| filterB }}          |
| └ **缩写**          |       v-bind        | 完整：<a v-bind:href = 'url'></a>           |
|                   |        └  :         | 缩写：<a :href='url'></a>                   |
|                   |        v-on         | 完整：<a v-on:click="doSomething"></a>      |
|                   |         └ @         | 缩写：<a @click="doSomething"></a>          |
| **计算属性**          |      computed       | 属性默认getter                               |
|                   |       ↑（对比） ↓       | 在需要时可以提供一个setter                         |
|                   |       $watch        |                                          |
| **Class与Style绑定** |    v-bind:class     |                                          |
|                   |    v-bind:style     |                                          |
| **条件渲染**          |        v-if         |                                          |
|                   |       v-else        |                                          |
|                   |       v-show        |                                          |
| **列表渲染**          |        v-for        | item in items                            |
|                   |                     | `$index` — items的数组索引                    |
|                   |                     | `$key`     — 键名操作，历遍对象的操作                |
|                   |                     | 可以接收整数                                   |
|                   |                     | <span v-for="n in 10 ">{{ n }}</span>    |
|                   |       Vue数组限制       | 不能检测：1.直接用索引设置元素，如vm.items[0] = {};      |
|                   |                     | 解决: `$set`   vm.items.$set(0, {childMesg:'Changed!'}) |
|                   |                     | 2.修改数据长度，如vm.items.length = 0;           |
|                   |                     | 解决:          用空数组替换                      |
|                   |                     | `splice()` —— `$remove`                  |
| **方法和事件处理**       |        方法处理器        | v-on监听DOM事件                              |
|                   |                     | methods:{}                               |
|                   |        内联处理器        | @click=function($event)                  |
|                   |        事件修饰符        | 解决经常需要调用`event.preventDefault()`和`event.stopPropagation()` 的问题 |
|                   |                     | `.prevent`和`.stop`                       |
|                   |                     | `.capture` 事件监听                          |
|                   |                     | `.self`只当事件在该元素本身（而不是子元素）时触发回调           |
|                   |        按键修饰符        | @keyup.13 / v-on:keyup.13(调用submit)      |
|                   |          │          | @keyup.enter — Vue提供按键别名                 |
|                   |        └ 别名         | `enter` `tab` `delete` `esc` `space` `up` `down` `left` `right` |
|                   |        思考·问题        | 为什么在HTML中监听？                             |
| **表单控件绑定**        |        基础用法         | Text ，Checkbox，Radio，Select              |
|                   |       绑定value       | 问题                                       |
|                   |        参数特性         | `lazy`在 change 事件中同步；默认在input事件重同步       |
|                   |                     | `number` 将输入转为Number类型                   |
|                   |                     | `debounce` 延时同步                          |
| **过渡**            |        CSS过渡        | `transition`特性可以与`v-if`,`v-show`,`v-for`一起使用 |
|                   |                     | [transition='transtionName']  设置好 .transitionName的样式 |
|                   |        Js钩子         | 定义好Vue.transition('transitionName',{...enter,leave等回调 }) |
|                   |                     | [transition='transitionName'] 标签引用       |
|                   |                     | v-for=" item in list \| filterBy query" 通过v-model=query输入筛选item |
| —**重点**—          |        —————        | ———————————————————————————————————      |
| **组件**            |       ┌创建构造器        | 1. var MyComponent = Vue.extend({ template: '<div>hello world</div> '}) |
|                   |      │   注册组件       | 2. Vue.component('my-component',MyComponent) |
|                   |       └创建根实例        | 3. new Vue({el:'#example'})              |
|                   |        注册语法糖        | 将1，2结合——Vue.component('my-div',{template:'<div> hell </div>'}) |
| └ Props           |         注意：         | camelCase 的 prop作特性时，需要转为kabab-case      |
|                   |        绑定类型         | 默认单向绑定 `.sync` 强制双向绑定 ；`.once` 强制单次绑定    |
| └ 父子组件通信          |         父链          |                                          |
|                   |        自定义事件        |                                          |
| └ Slot            |                     |                                          |
|                   |                     |                                          |
| └ 动态组件            |                     |                                          |
| —————             |        —————        | ———————————————————————————————————      |
| **深入响应式原理**       |        追踪变化         | vm.$log()                                |
|                   |        变化检测         | 受ES5限制，Vue.js不能检测到对象属性的添加或删除             |
|                   |                     | 对于Vue实例：vm.$set('temp' , changed )       |
|                   |                     | 对于普通数据：Vue.set(data, 'temp' , changed)   |
|                   |        初始化数据        |                                          |
|                   |       异步更新队列        |                                          |
|                   |                     | 之后好好看清楚，很多细节不清楚                          |
| ——————            |        —————        | ————————————————————————————————————     |
| **自定义指令**         |                     |                                          |
| └ 基础              | **Vue.directive()** | Vue.directive( id, definition ) 注册全局定义指令，接受ID和定义对象两个参数 |
|                   |       └ 钩子函数        | `bind`：第一次绑定时调用，只调用一次                    |
|                   |                     | `updata`：在`bind`之后参数为初始值，*每次* 绑定调用       |
|                   |                     | `unbind`：只调用一次，在指令从元素解绑时调用               |
|                   |      └ 指令实例属性       | `el`：指令绑定的元素                             |
|                   |                     | `vm`： 拥有该指令的上下文ViewModel                 |
|                   |                     | `expression`：指令的表达式，不包括参数和过滤器            |
|                   |                     | `arg`：指令的参数                              |
|                   |                     | `name`：指令的名字，不包括前缀                       |
|                   |                     | `modifiers`：一个对象，包含指令的修饰符                |
|                   |                     | `desription`：一个对象，包含指令的解析结果              |
|                   |       └ 对象字面量       |                                          |
|                   |       └ 字面修饰符       |                                          |
| └ 高级              |                     | `params` `deep` `twoWay` `acceptStatement` `terminal` `priority` |
| **自定义过滤器**        |  **Vue.filter()**   | Vue.filter('fliterName' , function(){//.....}) |
|                   |                     | 双向过滤器，动态参数                               |
| **混合**            |                     | 混合以一种灵活的方式为组件提供分布复用功能。                   |
| **插件**            |                     |                                          |

# Vue-Router  

| Vue-Router |      |      |
| ---------- | ---- | ---- |
|            |      |      |
|            |      |      |
|            |      |      |
|            |      |      |

# Vue.js API

| Vue.js API |                           |                                          |
| ---------- | ------------------------- | ---------------------------------------- |
| **全局配置**   |                           |                                          |
| **全局API**  | Vue.extend                |                                          |
|            | Vue.nextTick(callback)    | 延迟回调在下次 DOM 更新循环之后执行。在修改数据之后立即使用这个方法，等待 DOM 更新。 |
|            | Vue.set(object,key,value) | 设置对象的属性。如果对象是响应的，将触发视图更新。这个方法主要用于解决 不能检测到属性添加的限制。 |
|            |                           |                                          |
|            |                           |                                          |



## Vue.js 快速新建项目

| Vue.js新建项目                       |                   |                 |
| -------------------------------- | ----------------- | --------------- |
| npm install vue -g               | 若安装过Vue，则不用       |                 |
| npm install vue-cli -g           | 若安装过Vue-cli，则不用   | Vue-cli 官方命令行工具 |
| vue init webpack my-project-name | 创建一个基于webpack的项目  |                 |
| cd my-project-name               | 进入 项目目录           |                 |
| npm install                      | 安装                | 可能时间会久          |
| npm run dev                      | 运行项目              |                 |
| **目前问题**                         | 除了index.vue下能实时刷新 | 其他地方暂时不能实时刷新    |



## Vue.js Plan 

| Vue.js 练习计划 |      |      |
| ----------- | ---- | ---- |
| TodoApp     |      |      |
|             |      |      |
|             |      |      |

## Vue.js 遇到问题

| Vue.js问题记录                               |                                          |      |
| ---------------------------------------- | ---------------------------------------- | ---- |
| component 不能用  kabab-case 形式， import加载不了 | 用CamelCase                               |      |
| Vue-devtools                             |                                          |      |
| Recursive components problem:            | 递归问题                                     |      |
|                                          | 要在app.vue上注册tree                         |      |
|                                          | `var tree = require('./tree');`          |      |
|                                          | `Vue.component('ns-tree', tree);`        |      |
|                                          | https://github.com/vuejs/vue/issues/3039 |      |
|                                          |                                          |      |
