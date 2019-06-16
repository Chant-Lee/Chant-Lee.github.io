---
title: JavaScript简写总结
date: 2017-10-24 11:31:59
tags: [js经验]
---
## JS简写技巧总结
### 1 三目运算符
### 2 循环语句
 循环的时候采用foreach方法之类，尽量不用for循环。
 
<!--more-->

### 3 声明变量

	let x;
	let y;
	let z = 3;
	简写为
	let x, y, z=3;

### 4 变量赋值或者默认值
当将一个变量的值赋给另一个变量时，首先需要确保原值不是 null、未定义的或空值。

	if (a !== null || a !== undefined || a !== '') {
	     let b = a;
	}
	简写
	const b = a  || '';
	
### 5 对象属性
ES6 提供了一个很简单的办法，来分配属性的对象。如果属性名与 key 名相同，则可以使用简写。

	const obj = { x:x, y:y };
	简写为：
	const obj = { x, y };
	
### 6 箭头函数

	function sayHello(name) {
	  console.log('Hello', name);
	}
	简写为：
	sayHello = name => console.log('Hello', name);
	
### 7 函数默认参数值

	function test(a, b, c) {
	  if (a === undefined)
	    a = 3;
	  if (b === undefined)
	    b = 4;
	  return a + b * c;
	}	
	
	test = (a, b = 2, c= 4 ) => ( a+ b* c);
	
### 8 解构赋值
解构赋值是一种表达式，用于从数组或对象中快速提取属性值，并赋给定义的变量。

在代码简写方面，解构赋值能达到很好的效果。	

	let { log, sin, cos } = Math;
上面代码将Math对象的对数、正弦、余弦三个方法，赋值到对应的变量上，使用起来就会方便很多。	

* 1交换变量值

		[x, y] = [y, x];
	上面代码交换变量x和y的值，这样的写法不仅简洁，而且易读，语义非常清晰。	
	
* 2 从函数返回多个值

函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。

	// 返回一个数组
	
	function example() {
	  return [1, 2, 3];
	}
	var [a, b, c] = example();
	
	// 返回一个对象
	
	function example() {
	  return {
	    foo: 1,
	    bar: 2
	  };
	}
	var { foo, bar } = example();


* 3 函数参数定义
解构赋值可以方便地将一组参数与变量名对应起来。

		// 参数是一组有次序的值
		function f([x, y, z]) { ... }
		f([1, 2, 3]);
		
		// 参数是一组无次序的值
		function f({x, y, z}) { ... }
		f({z: 3, y: 2, x: 1});

* 4 提取json数据


解构赋值对提取JSON对象中的数据，尤其有用。

	var jsonData = {
	  id: 42,
	  status: "OK",
	  data: [867, 5309]
	};
	
	let { id, status, data: number } = jsonData;
	
	console.log(id, status, number);
	// 42, "OK", [867, 5309]
上面代码可以快速提取JSON数据的值。
* 5 函数参数默认值

		jQuery.ajax = function (url, {
		  async = true,
		  beforeSend = function () {},
		  cache = true,
		  complete = function () {},
		  crossDomain = false,
		  global = true,
		  // ... more config
		}) {
		  // ... do stuff
		};
指定参数的默认值，就避免了在函数体内部再写var foo = config.foo || 'default foo';这样的语句。

* 6 遍历map结构
任何部署了Iterator接口的对象，都可以用for...of循环遍历。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和键值就非常方便。
		
		var map = new Map();
		map.set('first', 'hello');
		map.set('second', 'world');
		
		for (let [key, value] of map) {
		  console.log(key + " is " + value);
		}
		// first is hello
		// second is world
		如果只想获取键名，或者只想获取键值，可以写成下面这样。
		
		// 获取键名
		for (let [key] of map) {
		  // ...
		}
		
		// 获取键值
		for (let [,value] of map) {
		  // ...
	}

* 7 输入模板指定的方法
加载模块时，往往需要指定输入那些方法。解构赋值使得输入语句非常清晰。

	const { SourceMapConsumer, SourceNode } = 			require("source-map");
	
### 9 展开运算符
展开运算符是在 ES6 中引入的，使用展开运算符能够让 JavaScript 代码更加有效和有趣。

使用展开运算符可以替换某些数组函数。

	// joining arrays
	const odd = [1, 3, 5];
	const nums = [2 ,4 , 6].concat(odd);
	 
	// cloning arrays
	const arr = [1, 2, 3, 4];
	const arr2 = arr.slice( )
	
		// joining arrays
		const odd = [1, 3, 5 ];
		const nums = [2 ,4 , 6, ...odd];
		console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]
		 
		// cloning arrays
		const arr = [1, 2, 3, 4];
		const arr2 = [...arr];
		
		
### 10 Object [key]

虽然将 foo.bar 写成 foo ['bar'] 是一种常见的做法，但是这种做法构成了编写可重用代码的基础。

请考虑下面这个验证函数的简化示例

		function validate(values) {
		  if(!values.first)
		    return false;
		  if(!values.last)
		    return false;
		  return true;
		}
		console.log(validate({first:'Bruce',last:'Wayne'})); // true
上面的函数完美的完成验证工作。但是当有很多表单，则需要应用验证，此时会有不同的字段和规则。如果可以构建一个在运行时配置的通用验证函数，会是一个好选择
		// object validation rules
		const schema = {
		  first: {
		    required:true
		  },
		  last: {
		    required:true
		  }
		}
		 
		// universal validation function
		const validate = (schema, values) => {
		  for(field in schema) {
		    if(schema[field].required) {
		      if(!values[field]) {
		        return false;
		      }
		    }
		  }
		  return true;
		}
		console.log(validate(schema, {first:'Bruce'})); // false
		console.log(validate(schema, {first:'Bruce',last:'Wayne'})); // true		