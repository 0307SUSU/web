# vue

> **Vue.js**，通常简称为Vue，是一个构建用户界面的渐进式框架。它被设计成可以自底向上逐层应用。Vue的核心库只关注视图层，因此它非常容易学习，并且可以与其它库或现有项目整合。

## 在线验证工具

> https://www.cainiaoplus.com/tool/vuejs/
>
> 此地址可以在线验证vue代码，后边所有代码都可在此工具中得到验证

## 语法

> 作为一个前端框架，vue有自己的语法规范
>
> 指令和插值：vue实现了一套自己的指令用于在template模板中做一些事情，(什么是template模板？类似于html标签)

## 组件

> vue中组件可以理解为可复用的模块
>
> 以`.vue`后缀结尾的文件就属于vue组件

### 基本结构

> vue的组件由三部分组成
>
> template   上边说的template模板就是它，用来定义组件的结构
>
> script    看名字就知道，这里肯定是用来处理逻辑写js代码的
>
> style      看名字又知道了，用来写样式的

**代码示范**

```vue
<template>
<!--结构化代码-->
</template>

<script>
// 逻辑代码
</script>

<style>
/*样式代码*/
</style>
```

> 从代码看这三部分都是标签，所以这三个标签在组件中没有书写顺序要求，并且也没规定这三个标签只能写一次，所以...,但一般情况下一个组件里三者各定义一个

#### template

> 上边说了它是用来定义组件的结构的，那么它是怎么定义组件的结构的？写过html吧？html怎么写他就怎么写,连注释写法都一样

**代码示范**

```vue
<template>
	<!--写一个h1标题-->
	<h1>友商是傻逼！</h1>
</template>
```

> 虽然写法完全一致，但template也有自己的规矩啊，他的规矩就是最外层只能有一个标签，不能有平级的第二个标签出现，为什么啊？(有时间去百度一下)

**代码示范**

```vue
<template>
	<!--最外层只能有一个标签-->
	<div>
        <!--既然只能有一个标签，一般情况下所有组件的template最外层都将用一个块标签div包裹-->
       	<h1>友商是傻逼！</h1>
        <h1>干翻华为！！！</h1>
    </div>
</template>
```

#### script

> 这里是用来写js代码的，但是vue能让你在这里边随便写吗？显然是不能的，它也有它的规矩。
>
> vue把js代码的书写分为选项式和组合式两种写法，也叫选项式API和组合式API，选项式API是vue2的写法组合式API是vue3的写法

##### 选项式API

> data、methods、computed、watch、生命周期钩子、props、component、...
>
> 说实话vue封装的东西太多了，光是去学习这些东西的用法就很花时间...,而且写任何代码都要找到对应的地方写，规矩定的有点死了。有时候真有点恶心

**代码示范**

```vue
<template>
	<!--写一个h1标题-->
	<h1>友商是傻逼！</h1>
</template>

<script>
export default{
    // 是不是发现了？为什么要写个export default？(回头百度查查去！)
    props:[''],
    components:{
        
    },
    data(){
        return {
            title:'友商是傻逼！'
        }
    },
    methods:{
        
    },
    computed:{
        
    },
    watch:{
        
    },
    mounted(){
        // 生命周期钩子挂载完成阶段
    },
    
}
</script>
```

> 看代码是不是发现了？js代码不能随便写，对应的代码写在对应的地方，这样的话好像不知道怎么往下写了，方法该定义在哪？属性定义在哪？不知道，得把上边的每个块是干嘛的搞清楚才能去写你的js逻辑

###### **data**

> data从字面意思理解是’数据‘，那从字面意思也能猜到了，它是用来定义组件数据的，那它是怎么定义组件数据的？

**它是这样定义的**

```vue
<template>
	<!--写一个h1标题-->
	<h1>{{title}}</h1>
</template>
<script>
export default{
    data(){
        return{
            title:'友商是傻逼！',
        }
    }
}
</script>
```

> 在代码中可以看出data中return了一个对象，对象中定义了一个title属性，这个return的对象就是定义的组件数据，然后你有没有疑问，对象为什么可以return？发现没data是函数所以可以return，那问题又来了，data为什么是函数而不是对象？为什么要return出去？为什么属性要定义在data里？（这些问题去百度，很重要要搞懂）
>
> 往模板里看发现h1标签的内容变成了`{{title}}`这样，title应该能推理出来，就是刚刚定义的属性，那`{{}}`是什么？它是vue的语法`插值语法`，开始的时候已经介绍过了，vue有自己的语法，指令和插值（也可以叫模板语法）

**插值和指令**

`插值`

> 插值就是将 Vue 实例中的数据插入到 HTML 模板中的过程。Vue 会自动跟踪数据的变化，并在数据更新时更新 DOM。根据这句话的描述是不是就理解上边的代码了？数据要被插值语法包起来才能正确渲染，如果不包是什么情况?（可以自己去试试）。那除了渲染数据它就没别的用处了吗？当然还有，它还可以执行简单的javascript表达式，（哪些属于js表达式，这就涉及js知识了，不清楚再去学学js）。

**代码演示**

```vue
<template>
	<!--渲染数据-->
	<h1>{{title}}</h1>
	<!--执行js表达式-->
	<span>1+1 = {{1+1}}</span>
</template>
<script>
export default{
    data(){
        return{
            title:'友商是傻逼！',
        }
    }
}
</script>
```

`指令`

> Vue 指令（Directive）是一种特殊的属性，以 `v-` 开头，用于在 Vue 组件的模板中对 DOM 进行渲染和操作。它们提供了一种简单的方式来将数据绑定到 DOM，并响应数据的变化。

- 内置指令

`v-text`

> 用于更新元素的文本内容，举例说明

```vue
<template>
<div>
	<span v-text="msg"></span>
    <!--他会输出‘干翻华为’,它等同于下边的插值语法写法-->
    <span>{{msg}}</span>
    <!--h1只会输出2-->
    <h1 v-text="num">1+1=</h1>
    <!--h2会输出1+1=2-->
    <h2>1+1={{num}}</h2>
    <div>{{su7}}</div>
    <div v-text="su7"></div>
</div>
</template>
<script>
export default{
    data(){
        return {
            msg:'干翻华为',
            num:1+1,
            su7:'<span>su7吊炸天</span>'
        }
    }
} 
    /*
    既然都有插值语法了为什么还要有一个v-text指令？
    因为两者还是有些区别的
    两者有什么区别？该用哪一个？
    先说一下看起来两个的作用很像，都可以把数据绑定到标签得到渲染
    但是
    1. 设置了v-text的标签最终只会渲染v-text绑定的数据，其标签本身的内容会被替换掉，因为v-text是通过设置元素的 textContent 属性来工作，因此它将覆盖元素中所有现有的内容。但是插值就不会，它只会渲染被插值语法包裹的数据，不影响元素定义其他内容，看上边的h1和h2标签。
    2. v-text识别不了html标签，而插值却可以，见代码中的两个su7输出结果
    */
</script>
```

`v-html`

> 更新元素的 [innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)。
>
> 避免使用该指令，因为有XSS 攻击风险：由于 v-html 直接渲染 HTML，如果 `rawHtml` 中包含恶意脚本，就可能导致 XSS 攻击。因此，在使用 v-html 时，**务必确保 `rawHtml` 的内容是可信的**。

```vue
<template>
  <div>
    <div id="editor"></div>
    <div v-html="editorContent"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      editorContent: ''
    }
  },
  mounted() {
    // 初始化富文本编辑器，并将编辑内容赋值给 editorContent
    const editor = new Quill('#editor', {
      // ...
    });
    editor.on('text-change', (delta, oldDelta, source) => {
      this.editorContent = editor.root.innerHTML;
    });
  }
}
</script>
```

`v-show`

> 控制元素的显示或隐藏
>
> 通过设置内联样式的 `display` CSS 属性来工作，当元素可见时将使用初始 `display` 值。当条件改变时，也会触发过渡效果。

```vue
<template>
<div v-show="isShow">这个元素会根据 isShow 的值显示或隐藏</div>
<div v-show="num>2">这个元素会根据判断num>2是否为真来显示或隐藏</div>
</template>
<script>
export default{
    data(){
        return {
            isShow:true,
            num:1+1
        }
    }
}
    // v-show的值可以是任何类型的js值，也可以是表达式，它最终都会转换为真或假，如果为真显示元素，为假隐藏元素
</script>
```

`v-if&v-else-if&v-else`

> 控制元素的显示或隐藏
>
> 当 `v-if` 元素被触发，元素及其所包含的指令/组件都会销毁和重构。如果初始条件是假，那么其内部的内容根本都不会被渲染。
>
> 当同时使用时，`v-if` 比 `v-for` 优先级更高。

```vue
<template>
<div v-show="isShow">这个元素会根据 isShow 的值显示或隐藏</div>
<div v-show="num>2">这个元素会根据判断num>2是否为真来显示或隐藏</div>
</template>
<script>
export default{
    data(){
        return {
            isShow:true,
            num:1+1
        }
    }
}
    // v-if的值可以是任何类型的js值，也可以是表达式，它最终都会转换为真或假，如果为真创建元素，为假删除元素
</script>
```

`v-for`

> 遍历数据并渲染到模板

```vue
<div v-for="item in items">
  {{ item.text }}
</div>
```

`v-on`

> 为元素绑定事件
>
> 可缩写为@
>
> 修饰符：
>
> - `.stop` - 调用 `event.stopPropagation()`。
> - `.prevent` - 调用 `event.preventDefault()`。
> - `.capture` - 在捕获模式添加事件监听器。
> - `.self` - 只有事件从元素本身发出才触发处理函数。
> - `.{keyAlias}` - 只在某些按键下触发处理函数。
> - `.once` - 最多触发一次处理函数。
> - `.left` - 只在鼠标左键事件触发处理函数。
> - `.right` - 只在鼠标右键事件触发处理函数。
> - `.middle` - 只在鼠标中键事件触发处理函数。
> - `.passive` - 通过 `{ passive: true }` 附加一个 DOM 事件。

`v-bind`

> 动态的绑定一个或多个 attribute，也可以是组件的 prop。
>
> 可缩写为：

`v-model`

> 在表单输入元素或组件上创建双向绑定。

`v-slot`

> 用于声明具名插槽或是期望接收 props 的作用域插槽。

`v-pre`

> 跳过该元素及其所有子元素的编译。

`v-once`

> 仅渲染元素和组件一次，并跳过之后的更新。

`v-memo`

> 缓存一个模板的子树。

`v-cloak`

> 用于隐藏尚未完成编译的 DOM 模板

###### **methods**

> 

###### watch

> 

###### props

###### computed

###### emits

###### component

###### 生命周期

> beforeCreate
>
> created
>
> beforeMount
>
> mounted
>
> beforeUpdate
>
> updated
>
> beforeUnmount
>
> unmounted
>
> errorCaptured
>
> activated
>
> deactivated
>
> serverPrefetch

##### **组合式API**

> setup()、ref()、computed()、reactive()、readonly()、watchEffect()、watchPostEffect()、watchSyncEffect()、watch()、isRef()、unref()、toRef()、toValue() 、toRefs()、isProxy()、isReactive()、isReadonly()、生命周期钩子、依赖注入

#### style

> scoped、动态绑定class、动态绑定style
