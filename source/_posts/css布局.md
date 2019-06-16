---
title: css布局
date: 2016-03-14 22:03:08
tags:
---
# 前言
这是一篇讲解css进行布局的文章。作为一个前端开发者，对于css的布局一定要掌握，一下是我的学习心得。

## 一、自适应两栏布局

### 1、margin方式  
 
<!-- more -->
```bash
.content{
     background: yellow;
     margin-left: 100px;
}
.left{
      background: red
      float:left;
      width: 100px;
}
<div class="container">
    <div class="left">
         <p>左边..</p>
     </div>
     <div class="content">
          <p>右边...</p>
      </div>
</div>
   
```
### 2、触发BFC方式

```bash
 .content{
    background: yellow;
    overflow:hidden;    // 触发BFC
    /*
    display:table-cell; // 触发BFC
    width: 9999px;
   */
}
.left{
    background: red;
    float:left;
    width: 100px;
}
```

###  3、弹性盒子方式

```bash
.container{
    display: -webkit-flex;
    display: flex;
}
.content{
     -webkit-flex: 1;
     flex: 1;
}
 .left{
     width: 100px;
     resize: horizontal;
     overflow: auto;
}
```

## 二、列表布局
### 1、float方式(不足：1列表元素高度必须一致，需要清除浮动)。

```bash
 .box {
      background: yellow;
      margin: 1em;
      float: left;
      height: 100px;
      width: 100px;
}
.after-float{
      clear: both;
      background: green;
}
  <div class="container">
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="box">列表项</div>
  <div class="after-float">
      afterfloat
  </div>
```

###  2、display：inline-block方式（优点：列表元素高度可以不一致，不需要清除浮动。不足：如果html源码中元素之间有空格，那么列与列之间会产生空隙【加上margin0可以清除】）
 
```bash  
.box {
    background: yellow;
    margin: 1em;
    display: inline-block;
    vertical-align: top;
    height: 100px;
    width: 100px;
}
 .after-float{
 } 
```

##  三、水平垂直居中布局。

### 1、margin为负的方式（不足：内容区域大小固定）。

```bash
.container{
     width: 500px;
     height: 500px;
     position: relative;
 }
.content{
     width: 200px;
     height: 100px;
     position: absolute;
     left: 50%;
     top: 50%;
     margin-top: -50px;
     margin-left: -100px;
}
    <div class="container">
        <div class="content">
              <p>内容区内容区...</p>
        </div>
    </div>
```

### 2、translate方式 （内容大小可变 、支持IE10）

```bash
.container{
     width: 500px;
     height: 500px;
     position: relative;
 }
 .content{
      width: 200px;
      height: 100px;
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%); /* 50%为自身尺寸的一半  IE10+*/
}
```

### 3、margin：auto方式

```bash
 .container{
      width: 500px;
      height: 500px;
      position: relative;
 }
.content{
      width: 200px;
      height: 100px;
      position: absolute;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      margin: auto;   /*IE8+*/
 }
```

###  4、display：table-cell方式

```bash
.container{
      width: 500px;
      height: 500px;
      display:table-cell;
      text-align:center;
      vertical-align:middle;
}
.content{
      display: inline-block;
      width: 200px;
      height: 100px;
 }
```

###  5、flex布局方式

```bash
 .container{
     width: 500px;
     height: 500px;

     display: flex;
     align-items: center;
    justify-content: center;
 }
 .content{
      width: 200px;
      height: 100px;
 }
```

##   四、css3中的弹性盒子布局

          等高(宽)的栏目
		  
          独立的元素顺序
		  
          指定元素之间的关系
		  
          灵活的尺寸和对齐方式

##  五、多列布局

##   六 、查询兼容性：www.canuse.com

             解决兼容性http://browserhacks.com/
			 
             CSS Hack
			 
            条件注释
			
			Javascript

