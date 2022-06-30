---
title: JavaScript - 定时器
tags: [setTimeout, setInterval]
categories: javascript
---
## 定时器

JavaScript 提供定时执行代码的功能，叫做定时器（timer），主要由`setTimeout()`和`setInterval()`这两个函数来完成。它们向任务队列添加定时任务。

### setTimeout()

`setTimeout`函数用来指定某个函数或某段代码，在多少毫秒之后执行。它返回一个整数，表示定时器的编号，以后可以用来取消这个定时器。
<!--more-->
```jsx
var timerId = setTimeout(func|code, delay);
```

上面代码中，`setTimeout`函数接受两个参数：

- 第一个参数`func|code`是将要推迟执行的函数名或者一段代码，

- 第二个参数`delay`是推迟执行的毫秒数。

  

```jsx
console.log(1);
setTimeout('console.log(2)',1000);
console.log(3);
// 1
// 3
// 2
```

上面代码会先输出1和3，然后等待1000毫秒再输出2。**注意，console.log(2)必须以字符串的形式，作为setTimeout的参数。**



**如果推迟执行的是函数，就直接将函数名，作为`setTimeout`的参数。**

```jsx
function f() {
  console.log(2);
}

setTimeout(f, 1000);
```

`setTimeout`的第二个参数如果省略，则默认为0。

```jsx
setTimeout(f)
// 等同于
setTimeout(f, 0)
```



除了前两个参数，`setTimeout`还允许更多的参数。它们将依次传入推迟执行的函数（回调函数）。

```jsx
setTimeout(function (a,b) {
  console.log(a + b);
}, 1000, 1, 1);
```

上面代码中，`setTimeout`共有4个参数。最后那两个参数，将在1000毫秒之后回调函数执行时，作为**回调函数的参数**。



> 还有一个需要注意的地方，如果回调函数是对象的方法，那么`setTimeout`使得方法内部的`this`关键字指向全局环境，而不是定义时所在的那个对象。

```jsx
var x = 1;

var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
      console.log(this);
  }
};

setTimeout(obj.y, 1000) // 1
// 上面代码输出的是1，而不是2。因为当obj.y在1000毫秒后运行时，this所指向的已经不是obj了，而是全局环境。
//由setTimeout()调用的代码运行在与所在函数完全分离的执行环境上。到了定时时间，this没有指向，默认指向window对象。
```

为了防止出现这个问题，**一种解决方法是将`obj.y`放入一个函数。**

```jsx
var x = 1;

var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
  }
};

setTimeout(function () {
  obj.y();
}, 1000);
// 2
// 上面代码中，obj.y放在一个匿名函数之中，这使得obj.y在obj的作用域执行，而不是在全局作用域内执行，所以能够显示正确的值。
```

另一种解决方法是，**使用`bind`方法，将`obj.y`这个方法绑定在`obj`上面。**

```jsx
var x = 1;

var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
  }
};

setTimeout(obj.y.bind(obj), 1000);
// 2
```

------



### setInterval()

`setInterval`函数的用法与`setTimeout`完全一致，区别仅仅在于`setInterval`指定某个任务每隔一段时间就执行一次，也就是无限次的定时执行。

语法格式：

```javascript
setInterval(handler,timeout,...arguments);

```

```jsx
var i = 1
var timer = setInterval(function() {
  console.log(2);
}, 1000)
```

上面代码中，每隔1000毫秒就输出一个2，会无限运行下去，直到关闭当前窗口。

与`setTimeout`一样，除了前两个参数，`setInterval`方法还可以接受更多的参数，它们会传入回调函数。

------



### clearTimeout()，clearInterval()

`setTimeout`和`setInterval`函数，都返回一个整数值，表示计数器编号。将该整数传入`clearTimeout`和`clearInterval`函数，就可以取消对应的定时器。

```jsx
var id1 = setTimeout(f, 1000);
var id2 = setInterval(f, 1000);

clearTimeout(id1);
clearInterval(id2);
```

上面代码中，回调函数`f`不会再执行了，因为两个定时器都被取消了。

`setTimeout`和`setInterval`返回的整数值是连续的，也就是说，第二个`setTimeout`方法返回的整数值，将比第一个的整数值大1。

```jsx
function f() {}
setTimeout(f, 1000) // 10
setTimeout(f, 1000) // 11
setTimeout(f, 1000) // 12
// 上面代码中，连续调用三次setTimeout，返回值都比上一次大了1。
```



练习：

 1. 请使用定时器，在控制台每隔1s打印一个数，这个数是1~10,打印到10就结果

    ```javascript
    for(var i=1;i<=10;i++){
        setTimeout(function(i){
            console.log(i)
        },i*1000,i)
    }
    ```

 2. 做一个60s的倒计时

    ```jsx
    var num = 60;
    var timer = setInterval(function(){
        num--;
        console.log(num);
        if(num == 0){
        	clearInterval(timer);
        }
    }, 1000);
    ```

    

------



### 运行机制

`setTimeout`和`setInterval`的运行机制，是将指定的代码移出本轮事件循环，等到下一轮事件循环，再检查是否到了指定时间。如果到了，就执行对应的代码；如果不到，就继续等待。

这意味着，`setTimeout`和`setInterval`指定的回调函数，必须等到本轮事件循环的所有同步任务都执行完，才会开始执行。由于前面的任务到底需要多少时间执行完，是不确定的，所以没有办法保证，`setTimeout`和`setInterval`指定的任务，一定会按照预定时间执行。



```jsx
setTimeout(someTask, 100);
veryLongTask();
```

> 上面代码的`setTimeout`，指定100毫秒以后运行一个任务。但是，如果后面的`veryLongTask`函数（同步任务）运行时间非常长，过了100毫秒还无法结束，那么被推迟运行的`someTask`就只有等着，等到`veryLongTask`运行结束，才轮到它执行。



再看一个`setInterval`的例子。

```jsx
setInterval(function () {
  console.log(2);
}, 1000);

sleep(3000);
```

> 上面代码中，`setInterval`要求每隔1000毫秒，就输出一个2。但是，紧接着的`sleep`语句需要3000毫秒才能完成，那么`setInterval`就必须推迟到3000毫秒之后才开始生效。注意，生效后`setInterval`不会产生累积效应，即不会一下子输出三个2，而是只会输出一个2。

------





