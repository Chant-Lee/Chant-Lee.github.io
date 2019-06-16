---
title: js纯函数
date: 2017-02-05 21:31:08
tags: [技术,前端]
---
## js纯函数

### javascript纯函数

### 定义

  纯函数是指不依赖于且不改变它作用域之外的变量状态的函数。
  也就是说，纯函数的返回值只由它调用时的参数决定，它的执行不依赖于系统的状态。
  
  纯函数是函数式编程的一个基础。接下来我们看一个简单的例子。
  
<!-- more -->
 
   var values = { a: 1 };
	function impureFunction ( obj ) {
	  var b = 1;
	
	  obj = obj * b + 2;
	
	  return obj.a;
	}
	
	var c = impureFunction( values );
// 现在 `values.a` 变成 3,  impureFunction 改变了它。
在上面的代码中，我们改变了参数对象中的一个属性。由于我们定义的函数改变的对象在我们的函数作用域之外，导致这个函数成为“不纯”的函数。

    var values = { a: 1 };
	function impureFunction ( obj ) {
	  var b = 1;
	
	  obj = obj * b + 2;
	
	  return obj;
	}
	
	var c = impureFunction( values );
上面的代码，我们只计算了作用域内的局部变量，没有任何作用域外部的变量被改变，因此这个函数是“纯函数”。

／／纯函数是这样一种函数，即相同的输出，
    永远会得到相同的输出，而且没有任何可观察的副作用
    var xs  =   [1,2,3,4,5];
        //  纯函数
        xs.slice(0,3);
        //=> [1,2,3]
        xs.slice(0,3);
        //=> [1,2,3]
        xs.slice(0,3);
        //=> [1,2,3]
        
        //  非纯函数
        xs.splice(0,3);
        //=> [1,2,3]
        xs.splice(0,3);
        //=> [4,5]
        xs.splice(0,3);
        //=> []
        
    
     //将splice转换成纯函数
     // 1 自己
    var oldSplice=Array.prototype.splice;
    Array.prototype.splice = function(){
        var newItem=JSON.parse(JSON.stringify(this));
        var obj=Object.prototype.toString;
        if(obj.call(arguments[0])==="[object Boolean]"){
            console.log(arguments.length);
            if(arguments.length>3){
                console.log(111);
               return oldSplice.apply(this,Array.prototype.slice.call(arguments).slice(1));
            }else{
                console.log(22222);
               return  newItem.slice(arguments[1],arguments[2])

            }
        }else{
           return oldSplice.apply(this,arguments);
        }
    }
    
    //参考答案
       Array.prototype.splice = (function () {
        var oldfn = Array.prototype.splice;
        return function () {
            var flag=Object.prototype.toString.call(arguments[0]) === '[object Array]',
                context=flag?this.concat():this,
                arg=flag?arguments[0]:arguments;
            return oldfn.apply(context, arg);
        }
    })();


    var a=[1,2,3,4,5];var c=a.splice(0,3);console.log(a,c);
    -->[4, 5] [1, 2, 3]

    var a=[1,2,3,4,5];var c=a.splice([0,3]);console.log(a,c);
    -->[1, 2, 3, 4, 5] [1, 2, 3]


```
答案一

var spliceFn = Array.prototype.splice;
Array.prototype.splice = function(){
    var isWritable = arguments[0] === false ? false : true;
    var self = isWritable ? this : this.slice(0);
    var n = isWritable ? 0 : 1;
    var args = Array.prototype.slice.call(arguments, n);
    
    答案二

     Array.prototype.splice = (function () {
        var nativeSplice = Array.prototype.splice;
        return function () {
            if (typeof arguments[0] === 'boolean') {
                var orgs = [].slice.call(arguments, 1);
                var newArr = this.concat();
                return nativeSplice.apply(newArr, orgs);
            } else {
                return nativeSplice.apply(this, arguments);
            }
        }
    })()

```




### 使用纯函数的好处
   * 首先它没有副作用，纯函数是不会修改作用域之外的状态，就意味着代码变得足够的简单和清晰；当你在调用一个纯函数的时候，你只要关注它的返回值，不用担心因为其他地方的问题影响里面出问题。
   * 纯函数是健壮的，改变执行次序不会对系统造成影响，因此纯函数的操作可以并行执行。
   * 纯函数非常容易进行单元测试，因为不需要考虑上下文环境，只需要考虑输入和输出。


  
  
    