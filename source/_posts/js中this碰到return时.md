---
title: this碰到return时
date: 2016-06-27 22:31:08
tags: [技术,前端]
---
## 2 this碰到return时
* 例子1

```
function fn()  
{  
    this.user = '追梦子';  
    return {};  
}
var a = new fn;  
console.log(a.user); //undefined
```

<!-- more -->
* 例子2

```
function fn()  
{  
    this.user = '追梦子';  
    return function(){};
}
var a = new fn;  
console.log(a.user); //undefined
```
* 例子3

```
function fn()  
{  
    this.user = '追梦子';  
    return 1;
}
var a = new fn;
console.log(a.user); //追梦子

function fn()  
{  
    this.user = '追梦子';  
    return undefined;
}
var a = new fn;  
console.log(a.user); //追梦子
```
什么意思呢？
### 如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。

```
function fn()  
{  
    this.user = '追梦子';  
    return undefined;
}
var a = new fn;  
console.log(a); //fn {user: "追梦子"}
```
### 还有一点就是虽然null也是对象，但是在这里this还是指向那个函数的实例，因为null比较特殊。


```
function fn()  
{  
    this.user = '追梦子';  
    return null;
}
var a = new fn;  
console.log(a.user); //追梦子
```
## 知识点补充：

　　1.在严格版中的默认的this不再是window，而是undefined。

　　2.new操作符会改变函数this的指向问题，虽然我们上面讲解过了，但是并没有深入的讨论这个问题，网上也很少说，所以在这里有必要说一下。

```
function fn(){
    this.num = 1;
}
var a = new fn();
console.log(a.num); //1
```
### 为什么this会指向a？首先new关键字会创建一个空的对象，然后会自动调用一个函数apply方法，将this指向这个空对象，这样的话函数内部的this就会被这个空的对象替代。
