# TypeScript
> 安装：npm install -g typescript
> 查看是否安装成功： tsc -v

### 创建ts文件
> ts文件以 `.ts` 后缀命名

### 编译ts文件
> 浏览器和node只能运行js代码不能运行ts所以ts代码需要编译成js代码
> TypeScript 的编译过程，实际上就是把“类型代码”全部拿掉，只保留“值代码”。
> TypeScript 官方提供的编译器叫做 tsc，可以将 TypeScript 脚本编译成 JavaScript 脚本。

- 安装tsc `npm install -g typescript`
- 检查安装成功否 `tsc -v`,出现版本号就表明安装成功
- 查看tsc帮助信息 `tsc -h`,查看完整帮助信息`tsc --all`
- 编译ts文件 `tsc 文件`
- - 假如有一个ts文件`a.ts`,编译时执行`tsc a.ts`
- - 执行编译命令成功后会生成一个相同名称的`.js`文件
- - tsc命令也可以一次编译多个ts文件，文件之间用空格隔开即可
- - - `tsc a.ts b.ts`
#### 编译报错处理
> 如果编译报错了，会输出一段错误信息，如果是正确的什么都不会输出，不管是报错还是不报错最终都会生成js文件
> 希望报错时不生成js文件就在编译时添加`--noEmitOnError`参数
> 如果只想检查类型是否正确不生成文件可以使用`--noEmit`参数

### 编译配置文件`tsconfig.json`
> 配置文件可以配置编译命令，减少命令行输入

- 例：有一个`tsc file1.ts file2.ts --outFile dist/app.js`这样的编译命令,每次编译都要输入这么长很麻烦，可以将这行命令配置在配置文件里

```json
{
  "files": ["file.ts","file2.ts"],
  "compilerOptions":{
    "outFile":"dist/app.js"
  }
}
```
- 这样一来再次编译时只需要执行`tsc`就可以了
### 语法
> TypeScript 对 JavaScript 添加的最主要部分，就是一个独立的类型系统。
> 数据类型
>> any、unknown、never
>> 类型声明
>> 类型推断
> 变量声明
> 元组
> 联合类型
> 接口
> 泛型

- `any`
> 类型，表示没有任何限制，也就是值可以是任何
> 类型的声明方式是 关键字 变量名:类型
> ts的类型声明必须复制后才可使用，否则报错

```ts
let x:any;
console.log(x);// 报错，因为没有赋值
x = 1;// yes
x = 'ab'; //yes
x = false; // yes
```
变量类型一旦设为any，TypeScript 实际上会关闭这个变量的类型检查。即使有明显的类型错误，只要句法正确，都不会报错。
