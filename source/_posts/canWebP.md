---
title: 图片是否支持canWebP格式
date: 2017-08-07 14:27:57
tags: [图片]
---
### 关于图片加载是否支持webp格式
* js前端检测：

利用img标签加载时候触发的onload以及onerror事件，判断图片是否具有宽高，若有，则表示支持WebP，否则，就不支持。

* 后台判断：

判断浏览器的请求头Accept是否支持WebP。

具体实施方案：

<!--more-->
最终采用了js检测方法来检测是否支持WebP，采用img标签对一个透明/无损的base64（减少图片请求）WebP图片发起请求（保证浏览器是完全，而非部分支持WebP），再根据成功时候的onload或者失败时候onerror事件，来判断浏览器是否支持WebP。同时将浏览器支持的结果放入到window变量中，方便之后来进行判断。

       window.canWebP=false;
		function  isWebp(){
		var img = new Image();
		    img.onload = function () {
		        window.canWebP = (img.width > 0) && (img.height > 0);
		    };
		    img.onerror = function () {
		        window.canWebP = false;
		    }
		    img.src = 'data:image/webp;base64,UklGRkoAAABXRUJQVlA4WAoAAAAQAAAAAAAAAAAAQUxQSAwAAAARBxAR/Q9ERP8DAABWUDggGAAAABQBAJ0BKgEAAQAAAP4AAA3AAP7mtQAAAA==';
		}
		
		
### vue-lazyload源码判断参考

	const inBrowser = typeof window !== 'undefined';
	function supportWebp () {
	  if (!inBrowser) return false;
	
	  let support = true
	  const d = document
	
	  try {
	    let el = d.createElement('object')
	    el.type = 'image/webp'
	    el.style.visibility = 'hidden'
	    el.innerHTML = '!'
	    d.body.appendChild(el)
	    support = !el.offsetWidth
	    d.body.removeChild(el)
	  } catch (err) {
	    support = false
	  }
	
	  return support
	}		