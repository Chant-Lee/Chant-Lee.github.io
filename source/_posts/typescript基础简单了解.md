---
title: typescript简单了解一下
date: 2018-05-20 11:08:25
tags: [js,ts]
---
### 简单介绍
TypeScript 扩展了JavaScript语法，任何已经存在的JavaScript程序，可以不加任何改动，在TypeScript环境下运行。TypeScript只是向JavaScript添加了一些新的遵循ES6规范的语法，以及基于类的面向对象编程的这种特性

### 优势
* 支持ES6规范：

    2015年发布的，它指出了未来一段时间内，客户端脚本语音的发展方向。
* 强大的IDE支持：

    体现在三个特性上：1.类型检查，在TS中允许你为变量指定类型。2.语法提示。3.重构。
<!-- more -->

### 基础

JavaScript 的类型分为两种：`原始数据类型（Primitive data types）`和`对象类型（Object types）`。

原始数据类型包括：布尔值、数值、字符串、null、undefined 以及 ES6 中的新类型 Symbol。

 ### 这些类型在typescript中的定义

```
//布尔值 在 TypeScript 中，boolean 是 JavaScript 中的基本类型，而 Boolean 是 JavaScript 中的构造函数。
let isTest: boolean = false
//number
let testNumber: number = 6
//字符串
let name: string = 'Tom'
//空值 在 TypeScirpt 中，可以用 void 表示没有任何返回值的函数
let unusable: void = undefined
// Null 和 Undefined
let u: undefined = undefined
let n: null = null

undefined 类型的变量只能被赋值为 undefined，null 类型的变量只能被赋值为 null。
与 void 的区别是，undefined 和 null 是所有类型的子类型
```
####  任意值

`Any`用来表示允许赋值为任意类型
在任意值上访问任何属性都是允许的
```        
let testAny: any = 'seven'
testAny = 7

```
变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型：
 ```       
let test
test = 'seven'
test = 7

```
#### 类型推断

在ts中，会根据你赋初值来进行类型推断
```          
let test = '1111'
test = 7
//index.ts(2,1): error TS2322: Type 'number' is not assignable to type 'string'
```
上面的代码等价于
```
let test: string = '1111'
test = 7
```

#### 对象类型-接口

可以使用接口（Interfaces）来定义对象的类型、
```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
}
```
####  联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种
```
let test: string | number
test = 'seven'
test = 7
```

#### 数组类型

数组类型有多种定义方式，比较灵活

* 最简单的方法是使用「类型 + 方括号」来表示数组：

```
let test: number[] = [1, 1, 2, 3, 5]

```
* 也可以使用数组泛型（Array Generic） Array<elemType> 来表示数组

```
let test: Array<number> = [1, 1, 2, 3, 5];

```
* any 在数组中的应用
 ```       
let test: any[] = ['dd', 25, { ddd: 'ddd' }]
```
* 接口也可以用来描述数组：

```
interface test {
    [index: number]: number;
}
let ddd: test = [1, 1, 2, 3, 5];
```
#### 函数类型

```
//函数声明
function sum (x, y) {
    return x + y
}

//函数表达式
var sum = function (x, y) {
    return x + y
}
```
* 在tys中可以对输入和输出类型进行控制
```
function sum (x: number, y: number): number {
    return x + y;
}
通过这种输入只能输入两个，输入少于或多余2都会报错，定义参数可传可不传请继续往下看吧
```
* 在ts中，函数表达式还可以这样子
```
let sum = function (x: number, y: number): number {
    return x + y;
}
也可以
let sum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
}
```
`【注意】`在ts中的=>和es6中的=>不一样

| 符号 | ts | es6 |
|-|-|-|
|=>|用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型 | 箭头函数|

* 接口定义函数的情况

```
interface Fun {
    (x: string, y: string): boolean
}

let testFun: Fun
testFun = function (x: string, y: string) {
    return x === y
}
```

* 前面说函数入参少传或多穿都会报错，可以通过?来判断参数选择传递
```

function sum (x: number, y?: number) {
    if (y) {
        return x + y
    } else {
        return x
    }
}
```
`[注意]`可选参数必须接在必需参数后面，也就是说 可选参数后面不允许再出现必须参数了

* 参数默认值的情况

```
function sum(x: number = 2, y: number = 1) {
    return x + y
}

有了默认值就不受「可选参数必须接在必需参数后面」的限制了
```
* 多余参数
在es6中可以通过...rest来解析多余的参数
```
function push (array, ...rest) {
    rest.forEach( function (item) {
        array.push(item)
    })
}
实际上rest就是一个数组
可以这样子

function push (array: any[], ...rest: any[]) {
    rest.forEach(function(item) {
        array.push(item)
    })
}

```
注意，rest 参数只能是最后一个参数，和es6一样

* 重载

重载允许一个函数接受不同数量或类型的参数时，作出不同的处理
```
function reverse (x: number): number
function reverse (x: string): string
function reverse (x: number | string): number | string {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''))
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}
上例中，我们重复定义了多次函数 reverse，前几次都是函数定义，最后一次是函数实现。
如果前面两个不定义，就会有一个缺点，就是不能够精确的表达，输入为数字的时候，输出也应该为数字，输入为字符串的时候，输出也应该为字符串。
注意，ts 会优先从最前面的函数定义开始匹配，所以多个函数定义如果有包含关系，需要优先把精确的定义写在前面
```
### 类型断言

可以用来手动指定一个值的类型 语法就是`<type>name` type就是类型

### 声明文件

当使用第三方库时，我们需要引用它的声明文件

* 声明语句
我们通常使用jQuery是下面这样
```
$('#test');
jQuery('#test');
```
但是在 ts 中，我们并不知道 $ 或 jQuery 是什么东西

这时，我们需要使用 declare 关键字来定义它的类型，帮助 ts 判断我们传入的参数类型对不对
```
declare let jQuery: (string) => any

jQuery('#foo')
```
习惯写法是讲声明文件放在一个js里面，其他页面有用需要///引入就行了

```
//a.js
declare const jQuery: (string) => any
//b.js
/// <reference path="./a.ts" />

jQuery('#test')
```
#### 内置对象
 
 ts也有很多内置对象，需要可以去mdn上面查看
 
