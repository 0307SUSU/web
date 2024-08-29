# ES6语法

## let&const

> 声明变量的关键字

### let

```js
/**
 * 基础用法
 */
let num = 10;
console.log(num); // 会在控制台打印num的值
```

1. 只在声明的块级作用域中有效

```js
/**
 * 只在所声明的块级作用域内有效，全局作用域下声明的变量在全局有效
 * 什么是块级作用域？
 * 块级作用域（Block Scope）是指由一对花括号 {} 包围的代码块所创建的作用域。
 */
let name = '张三'; // 全局声明变量
console.log(name,'打印全局声明的let变量'); // 会打印name的值
{
  console.log(name,'在块内打印全局声明的let变量'); // 会打印name的值
  
  let age = 100;
  console.log(age,'块级作用域'); // 会打印age的值
}
console.log(age,'在全局打印块内声明的变量'); // 报错ReferenceError: age is not defined
```

2. 没有变量提升

```js
/**
 * 不会变量提升
 * 什么是变量提升？
 * 变量提升（Hoisting）指的是在代码执行之前，JavaScript引擎会将变量和函数的声明提升到它们所在作用域的顶部。var关键字有变量提升，无论在哪声明的var变量都会被提升至全局作用域。
 */
console.log(num2,'在声明之前打印let变量'); // 会报错ReferenceError: Cannot access 'num2' before initialization
console.log(hot,'在声明之前打印var变量hot'); // 会打印undefined，不会报错
console.log(hotUpdate,'在全局作用域打印块内声明的var变量hotUpdate');//会打印undefined，不会报错


let num2 = true;
var hot = true;
{
  console.log(money,'块内打印声明之前的let变量money'); // 报错ReferenceError: Cannot access 'money' before initialization
  let money = 13000;
  console.log(hotUpdate,'在块内打印声明之前的var变量hotUpdate');//会打印undefined，不会报错
  var hotUpdate = false;
}
```

3. 同一作用域下变量不能重复声明

```js
/**
 * 同一作用域下let变量不能重复声明
 * var变量可以多次声明
 */
{
  var two = 30;
  var two = 40;
  console.log(two,'第二次声明的two会覆盖上一次声明的值'); // 输出40;
  
  let one = 10;
  let one = 20; // 多次声明同一变量会报错SyntaxError: Identifier 'one' has already been declared (at index.js:46:7)
  console.log(one);
  
}
```

4. 全局声明的let变量不会成为全局对象的属性

```js
/**
 * 当使用 let 在全局作用域中声明变量时，变量并不会成为全局对象（window 对象，浏览器环境下）的属性。换句话说，全局声明的 let 变量在全局范围内可用，但不会挂载到全局对象上。var会成为全局对象的属性
 * 什么是全局对象？
 * 在JavaScript中，全局对象（Global Object）是一个在所有作用域中都可以访问的特殊对象
 * 全局对象在不同的运行环境中有不同的表现形式，例如：

浏览器环境：全局对象是 window。
Node.js 环境：全局对象是 global。
 */

let x = 10;
console.log(x); // 输出: 10
console.log(window.x); // 输出: undefined (在浏览器环境下)

var y = 20;
console.log(y); // 输出: 20
console.log(window.y); // 输出: 20 (在浏览器环境下)
```

### const

> let的特性在const中一样适用

1. 必须声明并初始化

```js
/**
 * 基础用法
 */

const PI = 3.1415926;
console.log(PI,'定义一个const常量'); // 输出PI的值


/**
 * const声明时必须初始化
 */

const colors = '#ff6700'; // 声明并初始化
const blue; // 只声明未初始化，报错：SyntaxError: Missing initializer in const declaration
```

## 解构赋值

> **解构赋值**（Destructuring Assignment）是一种从数组或对象中提取值，并将其赋值给变量的简便方法。

### 数组解构赋值

```js
/**
 * 解构赋值
 * 数组解构赋值允许你将数组中的值按顺序赋值给变量。语法是使用方括号 []。
 */
const [a, b] = [1, 2]; 
console.log(a); // 输出: 1
console.log(b); // 输出: 2

/**
 * 改变解构出的变量值不会影响原始数组的值
 */
const arr = [1,2,3,4];
let [one,two,three,four] = arr;
console.log(one);
console.log(two);
console.log(three);
console.log(four);
one = 5;
console.log(one); // 打印5
console.log(arr); // 打印[1,2,3,4]

/**
 * 可嵌套解构
 */

let arr2 = [1,2,[3],[[4]]] // 定义一个多维数组

let [w,e,[c],[[r]]] = arr2;
console.log(w,e,c,r); // 1,2,3,4

/**
 * 可解构指定元素
 */

let [,v,,] = arr2; // 只解构第二个元素
console.log(v); // 2


/**
 * 为解构设置默认值
 * 当解构没有匹配值时会输出undefined
  * 当解构没有匹配值但有默认值时输出默认值
 */

let [z,x,[k],[[f]],j=5,o] = arr2;
 console.log(z,x,k,f,j,o); // 1,2,3,4,5,undefined

 /**
  * 剩余运算符解构
  */
 let [pink,tomato,...yellow] = arr2;

 console.log(pink,tomato,yellow); // 1,2,[[3],[[4]]]
 
 /**
  * 解构字符串
  */

 let [y,s,i,t,u] = '友商是傻逼';
 console.log(y); // 友
 console.log(s); // 商
 console.log(i); // 是
 console.log(t); // 傻
 console.log(u); // 逼
 
// let [aa,bb,cc] = 123; // 报错TypeError: 123 is not iterable
// console.log(aa,bb,cc);
// let [dd] = 456; //报错TypeError: 456 is not iterable
// console.log(dd);
```

### 对象解构赋值

```js
/**
 * 对象解构
 */

/**
 * 嵌套和忽略解构
 */

let obj = {
  p: ['hello', {yy: 'world'}]
 };

let {p:[,{yy}]} = obj; // 忽略hello解构yy
console.log(yy); // world
// console.log(p); // 报错ReferenceError: p is not defined

/**
 * 剩余运算符解构
 * 属性重命名解构
 */

let {a:vv, b:gg, ...rest} = {a: 10, b: 20, c: 30, d: 40};
console.log(vv,gg,rest);// 10,20,{c:30,d:40}

/**
 * 为解构设置默认值
 * 当解构没有匹配值时会输出undefined
  * 当解构没有匹配值但有默认值时输出默认值
 */

let {aaa = 10, bbb = 5,ccc} = {aaa: 3};
console.log(aaa,bbb,ccc); // 3,5,undefined

```

## Symbol

## Map&Set(数据结构)

### Map

> 对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。Map类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键
>
> 什么是hash结构？
>
> **哈希结构**，也称为**散列表**或**哈希表**（Hash Table），是一种通过**键（Key）直接访问值（Value）的数据结构。**

```js
/**
 * Map
 * map是构造函数
 */

// 构建一个Map实例
const myMap = new Map();


/**
 * map.set
 * 向map结构中写入或更新键值，
 */

const m = new Map();
m.set('name', '张三') // 第一个参数是键，第二个参数是值
console.log(m.set()); // set方法会返回当前map实例
// 链式写法
let maps = new Map()
.set('age',18)
.set('sex','男')

// 定义任何类型的键
.set(123,'数字类型的键')
.set(undefined,'undeined类型')
.set(false,'布尔类型')
.set(null,'null类型')
.set([1,2],'数组类型')
.set({data:{a:'1'}},'对象类型')
//...
/**
 * map.get
 * 读取键的值，如果找不到键，返回undefined
 */

console.log(maps.get('age'),maps.get(false));

maps.get('age') // 参数是键的名称，输出键值18
maps.get(false) // 布尔类型
//...

/**
 * map.has
 * 判断某个键是否在该map对象中，返回true或false
 */
console.log(maps.has(false),maps.has('name'));

maps.has(false) // true
maps.has('name') // false


/**
 * map.delete
 * 删除某个键，成功返回true，失败返回false
 */
console.log(maps.delete(undefined),maps.delete('name'));

maps.delete(undefined) // true
maps.delete('name') // false

/**
 * map.size
 * map实例的属性，返回map结构的成员总数
 */
console.log(maps.size);// 8

const map = new Map();
map.set('foo',true);
map.set('bar',false);

console.log(map.size); // 2

/**
 * map.clear
 * 清除map所有成员，无返回值
 */

maps.clear();
console.log(maps.size); // 0


/**
 * map.keys()
 * 遍历并返回所有键名
 * 遍历顺序就是插入顺序。
 */

const mapFor = new Map(
  [
    ['a','one'],
    ['b','two']
  ]
)

for(key of mapFor.keys()){
  console.log(key); // a,b 
}

/**
 * map.values()
 * 遍历并返回所有键值
 */
console.log(mapFor.values());

for(value of mapFor.values()){
  console.log(value);// one,two
  
}

/**
 * map.entries
 * 遍历返回所有遍历器
 */
console.log(mapFor.entries()); // 

for(item of mapFor.entries()){
  console.log(item); // ['a','one']  ['b','two']
  
  console.log(item[0],item[1]);// a,one  b,two
  
}


/**
 * map.forEach
 * 便历所有成员
 */

mapFor.forEach((value,key,map)=>{
  console.log("key:%s,value:%s", key,value);
  console.log(map);
  
})

//forEach方法还可以接受第二个参数，用来绑定this。
const reporter = {
  report: function(key, value) {
    console.log("Key: %s, Value: %s", key, value);
  }
};

mapFor.forEach(function(value, key, map) {
  this.report(key, value);
}, reporter);

```

### Set

```js
/**
 * Set
 * 它类似于数组，但是成员的值都是唯一的，没有重复的值。
 * Set本身是一个构造函数，用来生成 Set 数据结构。
 */
const mySet = new Set();

// 初始化set
const set = new Set([1,2,3,4]); // 为set函数设置初始值
console.log([...set]);// [1,2,3,4]


// set不会有重复的值

const set1 = new Set([1,2,3,4,4]);
console.log([...set1]); // [1,2,3,4]  set会忽略掉重复的值



/**
 * Set.add
 * 添加某个值，返回 Set 结构本身
 */

mySet.add(1)
.add(2)
.add(3)

/**
 * Set.delete
 * 删除某个值返回布尔值
 */

mySet.delete(2)

/**
 * Set.has
 * 判断是否为Set成员
 */

mySet.has(2)

/**
 * Set.clear
 * 清除所有成员，没有返回值。
 */
mySet.clear();


/**
 * Set.keys()
 * 遍历返回所有键名
 */

console.log(mySet.keys());

/**
 * Set.values
 * 遍历返回所有键值
 */

console.log(mySet.values());


/**
 * Set.entries
 * 遍历返回所有键值对
 */

console.log(mySet.entries());


/**
 * Set.forEach
 * 回调遍历所有成员
 */

mySet.forEach((value,key)=> {
  console.log(`${key}:${value}`);
  
})
```

## proxy(代理)

> Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

```js
/**
 * proxy
 * 是构造函数，接受两个参数，第一个参数是所要拦截的目标对象，第二个参数是一个对象，用来定义拦截行为
 * Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。
 */
let objPro = new Proxy({},{
get:(target,propkey,receiver)=>{
  return Reflect.get(target,propkey,receiver)
},
set:(target, propKey, value, receiver)=>{
  return Reflect.set(target, propKey, value, receiver)
}
})


/**
 * proxy支持的拦截操作共13个
 * get、set、has、deleteProperty、ownKeys、getOwnPropertyDescriptor、defineProperty、preventExtensions、getPrototypeOf、isExtensible、setPrototypeOf、apply、construct
 */


/**
 * get
 * 拦截属性的读取
 * 接收三个参数，分别为目标对象、属性名、proxy实例(可选)
 */

let myProxy = new Proxy({name:"小米"},{
  get:function(target,propkey){
    if(propkey in target){
      // 判断属性是否存在于目标对象内，如果存在返回该属性的值
      return target[propkey];
    }
    else{
      // 否则抛出错误,如果把else注释掉，访问不存在的属性，只会返回undefined。
      throw new ReferenceError(`属性名${propkey}不存在`)
    }
  }
});
console.log(myProxy.name); // 小米
// console.log(myProxy.boss); // 抛出错误

/**
 * set
 * 拦截属性的赋值
 * 接受四个参数，分别为目标对象、属性名、属性值、proxy实例(可选)
 */


// 数据验证
let myProxy2 = new Proxy({name:"雷军"},{
  set:function(target,propkey,value){
    console.log(propkey,value,target);
    if( propkey=== 'age'){
      if ( !Number.isInteger(value)) {
        throw new TypeError('age值必须为number类型')
      }
      if(value > 200) throw new RangeError('值不能大于200')
    }
  }
})

myProxy2.age = 200;



// 设置内部属性，禁止外部使用内部属性
const handler = {
  get (target,key){
    invariant(key,'get');
    return target[key];
  },
  set(target,key,value){
    invariant(key,'set');
    target[key] = value;
    return true;
  }
};
function invariant (key,action){
  if(key[0] === '_'){
    throw new Error(`内部属性${key} ${action}失败`)
  }
}

const target = {};
const proxy3 = new Proxy(target,handler);
// console.log(proxy3._prop);
// console.log(proxy3._prop = 'c');

// 数据绑定，即每当对象发生变化时，会自动更新 DOM。


/**
 * apply()
 * 拦截函数调用
 * 接受三个参数，目标对象、this、目标对象的参数数组
 */

var target4 = function () { return 'I am the target'; };
var handler4 = {
  apply: function () {
    return 'I am the proxy';
  }
};

var p = new Proxy(target4, handler4);

p()
// "I am the proxy"
```



## Reflect

> `Reflect`对象与`Proxy`对象一样，也是 ES6 为了操作对象而提供的新 API。

## promise

> 异步编程的一种解决方案
>
> promise之前的异步解决方案，定时器、回调函数、事件机制
>
> 中文直译：承诺
>
> 特点：
>
> 1. 状态不受外界影响。
> 2. 一旦状态确定，就不会再变，任何时候都可以得到这个结果。
>
> 状态：
>
> 1. pending
> 2. fulfilled
> 3. rejected

`基本使用`

> promise对象是构造函数
>
> 接受一个函数作为参数

```js
const promise = new Promise(function(resolve,reject){
    // resolve()成功的回调，将状态从pending变为fulfilled，将成功的结果传递出去
    // reject()失败的回调，将状态从pending变为rejected，将失败的结果传递出去
});

```

### 实例方法

> promise实例提供了一系列方法以供操作
>
> then、catch、finally、all、race、allSettled、any、resolve、reject

`then`

> 状态改变时的回调函数
>
> 接受两个参数，第一个参数是成功状态(fulfilled)的回调函数，第二个参数是失败状态(rejected)的回调函数，
>
> 参数可选
>
> 该方法会返回一个新的promise实例
>
> 可以链式调用

```js
const promise = new Promise(function(resolve,reject){
  if(false){
      resolve('成功');
  }else{
      reject(new Error('失败'))
  }
});

promise.then(function(res){
  // 成功时进入该函数
  console.log(res);
  return '链式调用'
},function(err){
  // 报错时进入该函数
  console.log(err)
  return '上一个函数失败'
}).then(function(res){
  console.log(res); // 打印文字：链式调用
});
```

`catch`

> 该方法是then方法第二个参数的别名，用于指定发生错误时的回调函数,也就是promise实例的状态变为rejected时调用，或者then方法运行错误也会调用该函数，该方法会捕获所有之前promise抛出的错误，Promise 对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止。
>
> 一般来说，不要在`then()`方法里面定义 Reject 状态的回调函数（即`then`的第二个参数），总是使用`catch`方法。
>
> Promise 内部的错误不会影响到 Promise 外部的代码，通俗的说法就是“Promise 会吃掉错误”。
>
> `catch()`方法返回的还是一个 Promise 对象，因此后面还可以接着调用`then()`方法。

```js
const promise = new Promise(function(resolve,reject){
  if(false){
      resolve('成功');
  }else{
      reject(new Error('失败'))
  }
});

promise.then(function(res){
  console.log(res);
  if (res) {
    iii+1
    console.log(i);
    
  }
}).catch(function(err){
  console.log('then函数执行过程中报错',err);
  
})

promise.catch(function(err){
  console.log('实例状态变为rejected',err);
});
```

`finally`

> `finally()`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。也就是说这个方法里的代码总是会执行
>
> 没有参数

```js
// resolve 的值是 undefined
Promise.resolve(2).then(() => {}, () => {})

// resolve 的值是 2
Promise.resolve(2).finally(() => {})

// reject 的值是 undefined
Promise.reject(3).then(() => {}, () => {})

// reject 的值是 3
Promise.reject(3).finally(() => {})
```

`all`

> 将多个 Promise 实例，包装成一个新的 Promise 实例返回。
>
> 接受一个promise实例数组作为参数

`race`

> 将多个 Promise 实例，包装成一个新的 Promise 实例返回

`allSettled`

> 忽视一组异步操作的状态继续执行下一步操作

`any`

> 只要参数实例有一个变成`fulfilled`状态，包装实例就会变成`fulfilled`状态；如果所有参数实例都变成`rejected`状态，包装实例就会变成`rejected`状态。
>
> any直译：任何，
>
> 这里指的是任何一个实例状态为fulfilled，any包装的实例就会变成fulfilled

`resolve`

> 将现有对象转为 Promise 对象

`reject`

> 返回一个新的 Promise 实例，该实例的状态为`rejected`。

## iterator(遍历器)&for...of

## generator

## async/await

> Generator 函数的语法糖
>
> `async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。
>
> `await`命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

## class

> ES6 的类，完全可以看作构造函数的另一种写法。
>
> 类的数据类型就是函数，类本身就指向构造函数。
>
> 类的所有方法都定义在类的`prototype`属性上面。
>
> 类的属性和方法，除非显式定义在其本身（即定义在`this`对象上），否则都是定义在原型上（即定义在`class`上）。
>
> 类的所有实例共享一个原型对象。
>
> 类相当于实例的原型，所有在类中定义的方法，都会被实例继承。

`类的方法`

> constructor、get、set、

`类的实例属性`

> 实例属性现在除了可以定义在`constructor()`方法里面的`this`上面，也可以定义在类内部的最顶层。

`类的静态方法`

> 如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。
>
> 如果静态方法包含`this`关键字，这个`this`指的是类，而不是实例。
>
> 静态方法可以与非静态方法重名。
>
> 父类的静态方法，可以被子类继承。
>
> 静态方法也是可以从`super`对象上调用的。

`静态属性`

> 静态属性指的是 Class 本身的属性，即`Class.propName`，而不是定义在实例对象（`this`）上的属性。

`私有属性和私有方法`

> 私有方法和私有属性，是只能在类的内部访问的方法和属性，外部不能访问。
>
> [ES2022](https://github.com/tc39/proposal-class-fields)正式为`class`添加了私有属性，方法是在属性名之前使用`#`表示。
>
> in运算符判断某个对象是否为类的实例。

`静态块`

> ES2022 引入了[静态块](https://github.com/tc39/proposal-class-static-block)（static block），允许在类的内部设置一个代码块，在类生成时运行且只运行一次，主要作用是对静态属性进行初始化。
>
> 每个类允许有多个静态块，每个静态块中只能访问之前声明的静态属性。另外，静态块的内部不能有`return`语句。

### 类的继承

> Class 可以通过`extends`关键字实现继承，让子类继承父类的属性和方法。
>
> 子类必须在`constructor()`方法中调用`super()`，否则就会报错。
>
> 父类所有的属性和方法，都会被子类继承，除了私有的属性和方法。
>
> 父类的静态属性和静态方法，也会被子类继承。
>
> 静态属性是通过浅拷贝实现继承的。

`Object.getPrototypeOf()`方法可以用来从子类上获取父类。

#### super关键字

> `super`这个关键字，既可以当作函数使用，也可以当作对象使用。
>
> `super`作为函数调用时，代表父类的构造函数。
>
> `super`作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。

## module

> export导出、import导入、export default默认输出
>
> as（重命名）
>
> *整体加载模块导出内容
>
> `import`命令具有提升效果，会提升到整个模块的头部，首先执行。
>
> `import`语句会执行所加载的模块，可以只执行不输入
>
> 一个模块只能有一个默认输出，因此`export default`命令只能使用一次。
>
> import()动态加载模块方法，`import()`返回一个 Promise 对象
