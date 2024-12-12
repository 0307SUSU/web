# JSX语法
> 主要作用就是使UI完全在JavaScript中定义，充分利用JavaScript提供的强大功能，在JS模板内做各种事情，受到的限制只是JavaScript支持与不支持，而不是模板框架的限制（JavaScript完全支持JSX）。

## JSX基础特性
- JSX实际上是`React.createElement()`的语法糖
- 可以在JSX中嵌入任何有效的JavaScript表达式，使用花括号`{}`包裹
- JSX属性使用驼峰命名法（例如：className而不是class）
- 所有标签必须闭合
- 可以使用`{/* */}`添加注释

## JSX转换示例

```jsx
// JSX代码
const element = (
  <h1 className="greeting">
    Hello, {formatName(user)}!
  </h1>
);

// 转换后的JavaScript代码
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, ',
  formatName(user),
  '!'
);
```

# 组件
> React组件可以分为类式组件和函数组件。组件名必须首字母大写，React组件最核心的作用是调用React.createElement()方法返回React元素。
# hook
# 路由（React Router）
# 状态管理（Redux）
# 状态管理 （Recoil）
# 移动端开发（React Native）
