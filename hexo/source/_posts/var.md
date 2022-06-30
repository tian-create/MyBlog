---
title: JavaScript - 变量提升
tags: ['变量提升', '全局变量', '局部变量', '作用域']
categories: javascript
---
## 变量提升

##### **基础知识** 

**在顶级的区域内声明的变量为 window级别的变量。 也就是说var a=100 等价于 window.a=100;** 

 **全局作用域和局部作用域** 

​	全局作用域：整个JS执行环境

​	局部作用域：通过创建一个函数就开辟出了一个局部作用域
<!--more-->
 **全局变量和局部变量** 

​	全局变量：在全局作用域都可以访问的变量

​	局部变量：只能在当前局部作用域访问的

 **变量声明提升：** 

​	如果变量声明在函数里面，则将变量声明提升到函数的开头

​	如果变量声明是一个全局变量，则将变量声明提升到全局作用域的开头

 **变量运行（搜索）机制：** 

​	首先看，有没有局部作用域

​	如果有，查找是不是这个局部作用域定义的变量

​	如果不是，寻找上一级作用域，直到找到全局作用域

​	如果全局作用域也找不到这个变量，这个变量就是未定义的 undefined

------

##### 1.在JS中只有两种作用域

a：全局作用域

b：函数作用域

什么是没有块级作用域？

```javascript
var i=1;
if(true){
	var a = '李天';
}
console.log(a);
// 变量a是声明在if的{}里面，但在js里面，因为没有块级作用域，所以此时的变量a的作用域是全局作用域。
```

------

##### 2.什么是变量提升？

在我们js中，代码执行时,分两步走：

解析、执行。

例如：我们习惯将 var a=2; 看做是一个声明，而实际上js引擎并不这么认为。它将var a（变量声明） 和 a = 2（初始化）看做事两个单独的声明，第一个是编译的任务，而第二个则是执行阶段的任务。

> 这意味着无论作用域中的声明出现在什么地方，都将在代码本身被执行前首先进行处理，可以将这个过程形象地想象成所有的声明（变量和函数）都会被“移动”到各自作用域的最顶端，这个过程被称为提升。
>
> 也就是该变量不管是在作用域的哪个地方声明的，都会提升到作用域的最顶上去。

```javascript
// 变量提升
console.log(a); // undefined
var a = 'hello';
console.log(a); // hello

//---- 上面等价于 -----
var a;
console.log(a);
a = 'hello';
console.log(a);
```

```javascript
function test(){
	console.log(a); // undefined
	var a = 123;
}
test();

//------ 实际执行顺序 -----
function test(){
	var a;
	console.log(a);
	a = 123;
}
test();

// 继续
var b=2;
function test2(){
    window.b=3; // 全局变量b
    console.log(b);//值为3
}
test2();
// 任何通过附加在window上的变量都相当于声明一个全局变量，或者是给全局变量赋值

// 再继续 根据变量声明提升和变量搜索机制：
c=5; 
function test3(){
    window.c=3;
    console.log(c);
    var c;
    console.log(window.c);
}
test3();
--------- 分析 --------
c=5;//声明一个全局变量c 
function test3(){
    var c;//变量声明提升，声明一个局部变量
    window.c=3;//改变全局变量c的值
    console.log(c);//由于此时的c是一个局部变量c，并且没有被赋值 c就是undefined    
    console.log(window.c);//此时的c就是一个全局变量c，也就是值为3
}
test3();
```

下面看一道经典面试题：

```javascript
var v1; // 全局变量提升
console.log(v1); // ? undefined
v1 = 100;
function foo(){
    var v1; // 局部变量提升
	cosole.log(v1); // ? undefined
	v1 = 200;
	console.log(v1); // ? 200
}
foo();
console.log(v1); // ? 100
```

把上面的例子稍微改动一下：

```javascript
// 前提 - 没有 var 声明就找上级作用域
var a = 100;
function ccc(){
    a = 200;
    function ddd(){
    	console.log(a);
    }
    ddd();
}
ccc();

//--------- 改动之后 --------
/* foo函数里面没有变量声明，所以foo里面的变量v1，其实都是访问的全局变量v1 */
var v1 = 100;
function foo(){
	console.log(v1); // 100
	v1 = 200; // 等于给全局变量v1重新赋值为200
	console.log(v1); // 200
}
foo();
console.log(v1); // 200
```

再看一个例子：

```JavaScript
var a = 1;
if(true){
	console.log(a); //1
	var a = 2;
	console.log(a); // 2
}
console.log(a); // 2
// 在js里面没有块级作用域，所以此处是在全局作用域重复声明了两次，那么第二次声明会被忽略，仅用于赋值。
```

------

##### 3.什么是函数提升？

```javascript
// 函数声明式
function a(){}
// 函数表达式（函数字面量式）
var b = function(){}
```



###### 函数声明式会被提升

>  函数字面量式的声明和变量提升的结果是一样的，函数只是一个具体的值； 

但是函数声明式的提升现象和变量提升略有不同

```javascript
console.log(bar);
function bar () {
  console.log(1);
}
/*
打印结果：
ƒ bar () {
  console.log(1);
}
*/
执行顺序相当于：
function bar(){
    console.log(1);
}
console.log(bar);
```

> 函数声明式提升，会将函数的整个代码块一起提升到作用域的最顶上去



######  **出现同名的函数声明，变量声明的时候， 函数声明会被优先提升，变量声明会被忽略** 

如果函数声明和变量声明使用的是同一个变量名称，函数声明的优先级高于变量声明的优先级。

```javascript
function fn(){}
console.log(fn);

var fn = 'hello';
console,log(fn);
/*
	结果：
	function fn(){}
	hello
*/
```

------

总结：

1. 所有的声明都会提升到作用域的最顶上去。
2. 同一个变量只会声明一次，其他的会被忽略掉。
3. 函数声明的优先级高于变量声明的优先级，并且函数声明和函数定义的部分是一起被提升的。

------

练习：

```javascript
// 1.
console.log(a); //?
console.log(b); //?
var a = 1;
function a(){}
var b= function(){};
console.log(a) //?

// 2.
(function(){
    a = 5;
    console.log(window.a); // ?
    var a = 10;
    console.log(a); // ?
})();
```