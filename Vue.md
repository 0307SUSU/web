#### vue中的Data为什么不是对象而是一个函数？

> 因为在vue中data存放的是组件实例的属性值，并且data中的数据是响应式的
>
> 假如你新建了一个组件且组件中的data为对象，这时你调用了两次这个组件实例，假如你在实例a中更新了data中的数据，那么因为data为对象的缘故，实例b中的数据也会做出更新
>
> 为什么呢？
>
> 因为虽然你创建了两个组件实例，但是因为data是对象的缘故，他会作用于组件全局，当你创建第二个实例的时候组件返回的还是已经改变的的data数据，并不会返回一组新的data数据，所以这时就会导致多个组件实例共用了一套data数据
>
> 而如果新建组件中的data是一个函数，那么当你每次新建一个组件实例的时候组件中的data都会返回一组新的data数据，这时无论你改变哪个实例中的data数据，都不会影响到其它实例，因为每个实例中的data都只作用于当前组件实例
>
> 为什么函数就可以返回一组新的data数据而对象却不会？
>
> 这是因为js的内存机制造成的，因为对象是引用类型数据它存储在堆内存中，而变量是存储在栈内存中的，栈中的对象只是对堆内存中对象的地址引用，所以当你将一个对象存储在不同变量中时只是对堆内存中存储的对象地址引用了两次，当你改变其中一个变量中的属性值时改变的其实是堆内存中对象的属性值所以这时引用了同一个对象的另一个变量也会改变。
>
> 而函数在js中是一种特殊的对象，可以赋值给变量，并且可以作为返回值返回任何数据，每次执行函数js都会创建一个新的函数实例返回一组新的数据，这些数据会存储在不同的内存空间中互不影响。

#### VDOM(虚拟dom)

> 虚拟dom是对浏览器渲染的真实dom的描述对象，描述了真实dom的相关信息
>
> 作用：提高页面渲染性能，简化操作真实dom的复杂度，降低开发成本，利于跨平台开发，提高代码可维护性，实现局部更新
>
> 实现原理：
>
> ​	vue：
>
> ​		编译阶段通过渲染函数生成虚拟dom树描述页面结构
>
> ​		渲染时将虚拟dom转换成真实dom挂载到页面
>
> ​		当数据发生变化时会重新触发渲染函数更新虚拟dom树，vue通过diff算法对比查找到虚拟dom树中被更新的部分，再将这一部分转换成真实dom更新到		页面中实现局部更新
>
> ​		被更新的dom会被放在异步队列中执行

#### 响应式原理

> vue2：
>
> ​	采用Object.defineProperty对属性进行数据劫持，通过触发getter和setter拦截器实现数据的更新
>
> vue3：
>
> ​	采用es6新语法Proxy（数据代理）对数据进行劫持，通过自定义拦截器操作数据实现响应式
>
> 两种响应式区别：
>
> ​	通过Object.defineProperty实现的响应式只能操作单个属性
>
> ​	proxy可以操作整个对象，性能上比defineProperty好

#### vue双向绑定原理

> vue通过数据劫持和发布订阅实现双向绑定
>
> 在vue2中vue通过Object.defineproperty()方法劫持data()中的属性将属性转换为getter和setter监听每一个属性的变化
>
> 当data中的属性值发生变化时会触发setter函数来更新属性的值
>
> vue实例在渲染时会创建一个watcher对象，当setter函数触发时会通知watcher对象数据发生了变化，watcher会触发对应的视图更新。
>
> Vue 3 的双向绑定原理：
>
> Vue 3 中采用了 Proxy 来替代 Object.defineProperty 来实现数据劫持，Proxy 相比于 Object.defineProperty 具有更好的性能和更丰富的功能。 在 Vue 3 中，当数据发生变化时，会通过触发 setter 来通知对应的依赖进行更新。这种方式相比 Vue 2 更加高效和灵活。

#### vue生命周期

> vue组件生命周期被划分为四个阶段，分别是初始化、挂载、更新、销毁，每个阶段都有不同的钩子函数
>
> vue2：
>
> ​		vue2中的钩子函数包括，初始化阶段（beforeCreate、created）挂载阶段（beforeMount、mounted）更新阶段（beforeUpdate、updated）销毁阶段（beforeDestory、destoryed），共八个钩子
>
> ​		每个阶段的钩子作用都有所不同，待更新...
>
> vue3:
>
> ​		vue3中删除了初始化阶段的create和created钩子，并且函数的名字有所变化，挂载阶段（onBeforeMount、onMounted）更新阶段（onBeforeUpdate、onUpdated）销毁阶段（onBeforeUnMount、onUnMounted）
>
> 



#### 路由

> 路由模式：
>
> 1. **Hash 模式（Hash History）**：在 URL 中使用 # 符号来作为路由地址的标识。例如，`http://example.com/#/about`。在这种模式下，当 URL 发生变化时，页面不会重新加载，而是通过监听 `hashchange` 事件来改变页面内容。优点是兼容性好，可以在不支持 History API 的浏览器中使用。缺点是 URL 中会出现 `#` 符号，看起来不太美观，并且对 SEO 不友好。
> 2. **History 模式（HTML5 History API）**：利用 HTML5 History API 中的 `pushState` 和 `replaceState` 方法来管理路由。在这种模式下，URL 是真实的 URL，没有 `#` 符号。例如，`http://example.com/about`。当 URL 发生变化时，页面不会重新加载，而是通过调用 History API 来改变页面内容。优点是 URL 更美观，并且对 SEO 更友好。缺点是需要服务器端的配合，以处理在客户端路由变化时的请求。
> 3. **Memory 模式**：仅在内存中保存路由状态，不会改变 URL。这种模式通常用于不需要在浏览器地址栏中显示路由信息的场景，如在一个单页面应用中的弹窗或抽屉组件中切换内容。
>
> 基础路由配置：
>
> 1. 安装路由模块    npm i vue-router
>
>    ```bash
>    npm i vue-router
>    ```
>
> 2. 创建路由文件夹及配置文件router>index.js
>
> 3. 编写配置文件代码
>
>    ```js
>    // 导入路由模块
>    import {createRouter,createWebHistory} from "vue-router"
>    
>    // 导入组件
>    import Home from '@/views/home'
>    
>    // 配置路由信息
>    const routes = [
>        {
>            path:'/',
>            component:Home
>        }
>    ]
>    
>    // 创建路由实例
>    const router = createRouter({
>        history:createWebHistory(), // 配置路由模式
>        routes:routes // 挂载路由信息
>    })
>    
>    // 导出路由实例
>    export default router
>    ```
>
> 4. 挂载配置文件到全局
>
>    ```js
>    import { createApp } from 'vue'
>    import App from './App.vue'
>    import router from '@/router/index' // 导入
>       
>    createApp(App)
>        .use(router) // 挂载
>        .mount('#app')
>    ```
>
> 路由实例中的属性：
>
> - history 定义路由模式
> - routes   定义路由
>
> routes中的路由属性：
>
> - path 路径地址
> - component  对应的组件
> - name  路由名称
> - components  视图命名
> - children  路由嵌套
> - redirect   重定向
> - props    传参
> - alias   别名
>
> 高级用法待更新...

#### 介绍一下vuex和pinia

> ### Vuex：
>
> 1. **核心概念**：Vuex 包含了一些核心概念，如 state（状态）、mutations（同步修改状态的方法）、actions（异步修改状态的方法）、getters（对 state 进行计算属性）、modules（模块化组织 state、mutations、actions、getters）等。
> 2. **严格模式**：Vuex 提供了严格模式，可以帮助开发者更好地调试应用程序中的状态变化。
> 3. **插件**：Vuex 支持插件机制，可以扩展其功能，如持久化存储等。
> 4. **使用场景**：适用于中大型 Vue.js 项目，需要管理较为复杂的状态逻辑和数据流。
>
> ### Pinia：
>
> 1. **Vue 3 的状态管理库**：Pinia 是为 Vue 3 开发的状态管理库，在设计上更符合 Vue 3 的响应式系统。
> 2. **Composition API 风格**：Pinia 的 API 设计借鉴了 Vue 3 的 Composition API，使用起来更加灵活和直观。
> 3. **支持 TypeScript**：Pinia 对 TypeScript 的支持更好，可以提供更好的类型推断和安全性。
> 4. **模块化组织**：Pinia 也支持模块化组织状态，可以更好地管理状态逻辑。
> 5. **轻量级**：相较于 Vuex，Pinia 更轻量级，对于小型项目或简单的状态管理需求更加适合。

#### Keep-alive

> 