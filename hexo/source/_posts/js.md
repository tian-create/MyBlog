---
title: JavaScript - 什么是JavaScript？
tags: JavaScript历史
categories: javascript
---
#### JavaScript历史
在上个世纪的1995年，当时的网景公司正凭借其Navigator浏览器成为Web时代开启时最著名的第一代互联网公司。

由于网景公司希望能在静态HTML页面上添加一些**动态效果**，于是叫**Brendan Eich**这哥们在两周之内设计出了**JavaScript**语言。

为什么起名叫JavaScript？原因是当时Java语言非常红火，所以网景公司希望借Java的名气来推广，但事实上JavaScript除了语法上有点像Java，其他部分基本上没啥关系。

---
<!--more-->
#### ECMAScript
因为网景开发了JavaScript，一年后**微软**又模仿JavaScript开发了**JScript**，为了让JavaScript成为**全球标准**，几个公司联合**ECMA**（European Computer Manufacturers Association）组织定制了JavaScript语言的标准，被称为**ECMAScript标准**。

> 简单来说，ECMAScript是一种语言标准，而JavaScript是网景公司对ECMAScript标准的一种实现。

如果你遇到ECMAScript这个词，简单把它替换为JavaScript就行了。

---

#### JavaScript版本
由于JavaScript的标准——ECMAScript在不断发展，最新版ECMAScript 6标准（简称**ES6**）已经在2015年6月正式发布了，所以，讲到JavaScript的版本，实际上就是说它实现了ECMAScript标准的哪个版本。

> 由于浏览器在发布时就确定了JavaScript的版本，加上很多用户还在使用IE6这种古老的浏览器，这就导致你在写JavaScript的时候，要照顾一下老用户，不能一上来就用最新的ES6标准写，否则，老用户的浏览器是无法运行新版本的JavaScript代码的。

---

#### JavaScript到底是什么
它是一种脚本语言，提供页面与用户的交互途径，主要包含三个方面的东西：
- ECMSScript（ES）：它主要用来定义JavaScript的语法规范，现在主流的版本是5.1。
- DOM(document object model:文档对象模型)
- BOM(bowser object model:浏览器对象模型)

---

#### JavaScript运行在什么地方
在设计JavaScript这门语言的时候，我们当初的设计者是要让这一门语言运行在浏览器里面的，所以，我们的JavaScript与CSS一样都是运行在页面当中。但是它也有一个特殊的标签进行包裹
```html
<script type="text/javascript"></script>
```
> JS代码与CSS代码有很多的相似之处，主要体现的代码的位置，CSS的代码主要在三个位置，JS代码也就是行内代码，和Script代码，以及我们的外部JS文件

1. 写在标签里面
```html
<button type="button" onclick="alert('hello world')" style="color:red">
    按钮
</button>
```
> 上面的 alert('hello world') 就是我们的JS代码，它直接和HTML代码写在了一起与我们的CSS是一样的，我们的CSS代码是写在了style这个属性里面

2. 写在特定的标签里面，与CSS内部样式块相同
```html
<script type="text/javascript">
	alert('你好');
</script>
<style type="text/css">
    div{
        width:100px;
    }
</style>
```
> 上面的代码 alert('你好') 也是JS代码，但是它写在了我们的script的标签里面

3. 写在外部文件当中
我们的CSS样式如果过多以后，我们会把这些CSS样式单独写在一个文件里面，这个文件以.css结尾，同理，如果一个页面的JS代码过多，我们也可以单独的写在一个文件里面，这个文件以.js结尾
```html
<link rel="stylesheet" type="text/css" href="style.css" />
<script type="text/javascript" src="javascript.js"></script>
```
**特别注意：**
一个script标签如果加了src属性连接到另一个JS文件里面， 这个script标签里面就不能加东西了
```html
<script src="js/javascript.js" type="text/javascript">
    var div1 = document.getElementById("div1");
    div1.innerText="改下你";
</script>
```
**==以上写法是错误的==**

---

#### JavaScript的注释

```Javascript
//单行注释 
/*
	多行注释
*/
```



