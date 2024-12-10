### 变量
> let const var

- 变量提升
> 将变量的声明提升到当前作用域的最顶层
- - var存在变量提升，let和const不存在变量提升
- 重复声明
> 对同一变量进行多次声明
- - var可以重复声明，最新一次会覆盖上一次的声明，let和const不可以，只能声明一次，重复声明会报错
- 作用域
> 作用域（Scope）是程序中用来定义(变量、函数和对象)的**可见性**和**生命周期**的一套规则。它决定了代码中哪些部分可以访问或使用特定的变量和函数。
> js的作用域类型：全局作用域、函数作用域、块级作用域、静态作用域
- - 作用域链
- - var声明的变量属于函数作用域，let和const声明的变量属于块级作用域
- 全局对象
> 全局对象（Global Object）是一个特殊的对象，在 JavaScript 中，所有在全局范围内声明的变量和函数都作为该全局对象的属性和方法存在。它为 JavaScript 代码提供了一个全局的执行环境。
>不同的 JavaScript 执行环境（如浏览器和 Node.js）中，全局对象有所不同(浏览器的全局对象是window，Node的全局对象是Global)，但它们都有一个共同点：它们包含了全局作用域中的变量和函数。
- - var声明的全局变量属于全局对象的属性，let和const声明的全局变量不属于全局对象的属性
- 暂时死区
> 暂时死区（Temporal Dead Zone，简称 TDZ）是 JavaScript 中的一个概念，指的是 let 和 const 声明的变量在代码执行过程中，从变量声明之前到变量初始化之前的一段时间，在这段时间内，变量是不可访问的，即使它已经声明了。
> 在这个“暂时死区”内，如果你尝试访问这些变量，将会抛出 ReferenceError 错误。
- - var不存在暂时死区，let和const存在
### 数据类型
> Number String Boolean Array Object Undefined Null Symbol Bigint
### 数据结构
> Set Map Arraay Object Weakset Weakmap
### proxy Reflect
### promise
### 迭代器 生成器
### 模块化
### 解构赋值
> "解构赋值是一种打破数据结构，将其拆分为更小部分的过程。"
> 自己的理解：将数据**拆分**成更小数据。
> 解构：解析重构，例如将一个数组类型的数据拆分成简单类型的数据。
- 例：
```javascript
let arr = [0,1,2,3,4];
let [num1,num2,num3,num4,num5] = arr;
console.log(num1, typeOf num1); // 0,Number
console.log(num2, typeOf num2); // 1,Number
console.log(num3, typeOf num3); // 2,Number
console.log(num4, typeOf num4); // 3,Number
console.log(num5, typeOf num5); // 4,Number
```
- 什么样的数据可以解构？
- - >数据是由不同的数据类型组成的，从数据类型的角度出发，看看哪些数据类型可以被解构
```javascript
// 数组
// 数组
let up = [10,4,13,73];

// 所有开销加起来得到总开销
let total = null;

// 记录数字用Number类型
let car = 10;
let breakfast = 4;
let coffee = 13;
let recreation = 73;
// 
```

