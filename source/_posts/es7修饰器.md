---
title: es7修饰器
date: 2018-04-20 11:08:25
tags: [js]
---

## 修饰器

修饰器（Decorator）是一个函数，用来修改类的行为。这是ES7的一个提案，目前Babel转码器已经支持。本文参考阮一峰老师的文章。

### 环境搭建
目前es7还没出，要让es6支持Decorator就需要安装与配置Babel转码器的插件。
<!-- more -->

1 .如果项目已经在用npm管理包
```
npm i --save-dev babel-plugin-transform-decorators-legacy

```
2 . 配置项目目录下的.babelrc 文件（babel配置文件），没有就创建一个
```
//追加大括号内的内容，不懂babel可以搜索相关资料
{
 'plugins': ['transform-decorators-legacy']
}
```

### 使用方式

```
//如果有一个叫,修饰Class
@decoratorA  //修饰类
class Person
{
  @descratorB //修饰方法
  say(message){
     
  }
}  

```
### 修饰器表达
```
//修饰类,以上面的使用为例，实际在编译期间将代码修改成这样
function decoratorA(target){  //Person
    //修改target,添加各种方法或者属性等
}

decoratorA(Person)
//修饰方法
function decoratorB(target, name, descriptor){
  return descriptor;
}
```
### 简单运用
```
function sayable(target){
    target.prototype.say  = function(message){
        console.log(message)
    }
}

@sayable
class Person(){}

var person = new Person();
person.say("good bye");

```