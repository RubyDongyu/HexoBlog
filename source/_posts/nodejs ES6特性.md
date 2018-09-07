---
title: nodejs ES6特性
categories:
  - javascript
tags:
  - javascript,node
date: 2018-09-07 02:23:34
---

## 新特性

ECMAScript 2015(ES6)的新特性

- import
- export
- class
- 箭头函数
- 块级作用域

## [import](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import)
import语句用于导入由另一个模块导出的绑定。无论是否声明了 strict mode ，导入的模块都运行在严格模式下。import语句不能在嵌入式脚本中使用。
### 语法
```
import defaultExport from "module-name";
import * as name from "module-name";
import { export } from "module-name";
import { export as alias } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
```
- defaultExport  
将引用模块默认导出的名称。

- module-name  
要导入的模块。这通常是包含模块的.js文件的相对或绝对路径名，不包括.js扩展名。某些打包工具可以允许或要求使用该扩展；检查你的运行环境。只允许单引号和双引号的字符串。

- name  
引用时将用作一种命名空间的模块对象的名称。

- export, exportN  
要导入的导出名称。

- alias, aliasN  
将引用指定的导入的名称。


## [export](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/export)
export语句用于在创建JavaScript模块时，从模块中导出函数、对象或原始值，以便其他程序可以通过 import 语句使用它们。
### 语法
```
export { name1, name2, …, nameN };
export { variable1 as name1, variable2 as name2, …, nameN };
export let name1, name2, …, nameN; // also var
export let name1 = …, name2 = …, …, nameN; // also var, const
export function FunctionName() {...}
export class ClassName {...}

export default expression;
export default function (…) { … } // also class, function*
export default function name1(…) { … } // also class, function*
export { name1 as default, … };

export * from …;
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
```
- nameN  
导出的标识符（用来被其他脚本的 import 导入）

## [class](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/class)
class 声明创建一个基于原型继承的具有给定名称的新类。  
你也可以使用类表达式定义类。但是不同于类表达式，类声明不允许再次声明已经存在的类，否则将会抛出一个类型错误。
### 语法
```
class name [extends] {
  // class body
}
```
### 示例
```
class Polygon {
  constructor(height, width) {
    this.name = 'Polygon';
    this.height = height;
    this.width = width;
  }
}

class Square extends Polygon {
  constructor(length) {
    super(length, length);
    this.name = 'Square';
  }
}
```

## [箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

箭头函数表达式的语法比函数b表达式更短，并且没有自己的this, arguments, super或new.target.
### 基础语法
```
(参数1, 参数2, ..., 参数N) => {函数声明}
(参数1, 参数2, ..., 参数N) => 表达式(单一)
// 相当于: (参数1, 参数2, ..., 参数N) => {return 表达式;}

// 当只有一个参数时,圆括号是可选的。
(单一参数) => {函数声明}
单一参数 => {函数声明}

// 没有参数的函数应该写成一对圆括号
() => {函数声明}
```

## [块级作用域](https://www.cnblogs.com/giggle/p/5572006.html)
- [let](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)  
let 语句声明一个块级作用域的本地变量，并且可选的将其初始化为一个值。

- [const](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const)  
  常量是块级作用域，很像使用 let 语句定义的变量。常量的值不能通过重新赋值来改变，并且不能重新声明。