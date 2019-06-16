---
title: Date交互
date: 2017-07-06 11:27:17
tags: [技术,经验,前端]
---
## 关于Date对象的使用经验
YY-MM-DD

	JSON.stringify( new Date()  ).replace(/T.*|"/g, "")
	//2017-07-06
	
yyyy-mm-dd HH:mm:ss:fff
	
	JSON.stringify(
	        new Date()
	      ).replace(/T|"|\..*/g," ").trim()	//2017-07-06 03:25:11
