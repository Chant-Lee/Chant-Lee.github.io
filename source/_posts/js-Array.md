---
title: es5 and es6 Array
date: 2017-06-28 11:25:22
tags:
---
# 数组
## 目录

  * 1 数组的定义
  * 2 数组对象属性
  * 3 数组对象的方法
     - concat(),pop(),join(),push()
     - reverse(),shift(),unshift(),slice()
     - splice(),toSource(),toString(),sort()
     - toLocaleString(),valueOf()
  * 4 es6数组新增
     - Array.from(),Array.of()
     - copyWihin(), fill()
     - find()和findIndex()
     - entries(),keys(),values()
     - includes()
  * 5 数组的空位
 	 
<!-- more --> 
	 
### 1 数组的定义 
数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。

		var arr = ['a', 'b', 'c'];
		arr[0] // 'a'
		arr[1] // 'b'
		arr[2] // 'c'
	上面代码中的a、b、c就构成一个数组，两端的方括号是数组的标志。a是0号位置，b是1号位置，c是2号位置。
	
本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。

		typeof [1, 2, 3] // "object"
	 
### 2 数组对象属性	 
 * constructor
 
	constructor 属性返回对创建此对象的数组函数的引用。
	
		var a=[1,3,4];
		a.constructor==Array //true
	
 * length
 
   length 属性可设置或返回数组中元素的数目。
   
		  var a=[1,3,4];
		  a.length
	  
 * prototype
 
   prototype 属性使您有能力向对象添加属性和方法。
   
		   Array.prototype.see=12;
		   var a=[1,3,4];
		   a.see //12
	   
		   function employee(name,job,born)
			{
				this.name=name;
				this.job=job;
				this.born=born;
			}
			var bill=new employee("Bill Gates","Engineer",1985);
			employee.prototype.salary=null;
			bill.salary=20000;
		
### 3 Array 对象方法

   - `concat()` 方法用于连接两个或多个数组。
    该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
    
    '语法'arr.concat(arrayX,arrayX,......,arrayX)
    
    arrayX 必需。该参数可以是具体的值，也可以是数组对象。可以是任意多个。
    
	    var a = [1,2,3];
	    a.concat(2,3,4)//[1,2,3,2,3,4]
	    a.concat([1,3])//[1,2,3,1,3]
   - `join()` 方法用于把数组中的所有元素放入一个字符串。
     元素是通过指定的分隔符进行分隔的。
     arr.join(x);//x可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。
	     
	      var a = [1,2,3];
		    a.join('')
   - `pop()` 方法用于删除并返回数组的最后一个元素。
   - `push()` 方法可向数组的末尾添加一个或多个元素，并返回新的长度。
   - `reverse()` 方法用于颠倒数组中元素的顺序。
   - `shift()` 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。
   - `unshift()` 方法可向数组的开头添加一个或更多元素，并返回新的长度。
   - `slice()` 方法可从已有的数组中返回选定的元素。
   
    arr.slice(start,end)
    
   start 必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。
   
   end 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。
    arr.slice(0)可以用来复制
    
    请注意，该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。
   - `sort()` 方法用于对数组的元素进行排序。
   
      arr.sort(sortby)//sortby可选。规定排序顺序。必须是函数。
      
      对数组的引用。请注意，数组在原数组上进行排序，不生成副本。
      
   - `splice()` 方法向/从数组中添加/删除项目，然后返回被删除的项目
   
    arr.splice(index,howmany,item1,.....,itemX)
    
    index必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
    
    howmany必需。要删除的项目数量。如果设置为 0，则不会删除项目。
    
    item1,.....,itemX可选。向数组添加的新项目。
    
    splice() 方法可删除从 index 处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。
如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。
    
   - `toSource()` 方法表示对象的源代码。
   
   该原始值由 Array 对象派生的所有对象继承。
   
   - `valueOf()` 方法返回 Array 对象的原始值。
   
    该原始值由 Array 对象派生的所有对象继承。
    
    valueOf() 方法通常由 JavaScript 在后台自动调用，并不显式地出现在代码中
   - `toLocaleString()` 把数组转换为本地字符串

### 4 es6数组新增
   * `Array.from()`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。
   返回一个新的Array实例。
   
   Array.from（arrayLike [，mapFn [，thisArg]]）
   
   arrayLike将数组转换为数组的数组或可迭代对象。
   
   mapFn映射函数调用数组的每个元素
   
   thisArg this执行时使用的值mapFn。
   
		let arrayLike = {
		    '0': 'a',
		    '1': 'b',
		    '2': 'c',
		    length: 3
		};
		
		// ES5的写法
		var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
		
		// ES6的写法
		let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
Examples		
Array from a String
		
			Array.from('foo'); // ["f", "o", "o"]
Array from a Set			
			var s = new Set(['foo', window]); 
			 Array.from(s); // ["foo", window]
Array from a Map			
	      
	       var m = new Map([[1, 2], [2, 4], [4, 8]]);
			 Array.from(m); // [[1, 2], [2, 4], [4, 8]]
Array from an Array-like object (arguments) 
			 function f() {
			  return Array.from(arguments);}
			f(1, 2, 3);	// [1, 2, 3]
       
       
       
	
	      