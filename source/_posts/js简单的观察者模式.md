---
title: js简单的观察者模式
date: 2016-03-27 21:31:02
tags: [技术,前端]
---

# js观察者模式
观察者模式又叫发布订阅模式（Publish/on），它定义了一种一对多的关系，
让多个观察者对象同时监听某一个主题对象，这个主题对象的状态发生变化时就会通知所有的观察者对象，
使得它们能够自动更新自己。 
## 利用原型的模式实现观察者。
<!-- more -->

```bash
//新建一个observer
function Observer() {
    this.fns = [];
}
//原型方法
Observer.prototype = {
//订阅方法
    on: function (fn) {
        this.fns.push(fn);
    },
	//取消订阅
    fail: function (fn) {
        this.fns = this.fns.filter(
                        function (el) {
                            if (el !== fn) {
                                return el;
                            }
                        }
                    );
    },
    update: function (o, thisObj) {
        var scope = thisObj || window;
        this.fns.forEach(
                        function (el) {
						   console.log(el);
                            el.call(scope, o);
                        }
                    );
    }
};

//测试
var o = new Observer;
var person1 = function (message) {
    console.log('person1: ' + message + ', 赶紧收拾东西');
};

var person2 = function (message) {
    console.log('person2: ' + message + ', 去买水');
};

o.on(person1);
o.on(person2);

o.update("女朋友回来了")

//person1退订
o.fail(person1);
//再来发送
o.update("妈妈回来了！");   

```
##其实还有很多方法，比如让多个对象都具有观察者发布订阅的功能，jQuery的on和off也行等等，目前功力还不高，希望能够相互学习，邮箱245922323@qq.com

