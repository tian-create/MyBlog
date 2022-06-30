---
title: JavaScript - 方法调用以及this指向
tags: ['方法调用', 'this指向']
categories: javascript
---
## 方法调用以及 this 指向

### 方法的调用

##### 常规调用

```js
// 定义一个方法
function a(){
    //代码块
}

// 方法名()
a();

// 立即调用
+ function a(){
    //代码块
}()

// 函数表达式调用
var a = function(){
    //代码块
}();
```
<!--more-->
---

#### call() 和 apply()

每个函数都包含两个非继承而来的方法：call()方法和 apply()方法。

call 和 apply 可以用来**重新定义函数的执行环境**，也就是 this 指向；call 和 apply 都是为了改变某个函数运行时的上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向。

##### call() 调用

调用一个对象的方法，用另一个对象替换当前对象，可以继承另外一个对象的属性，语法：

```javascript
Function.call(obj, param1, param2...);
// obj：这个对象将代替Function类里的this 对象
// params：一串参数列表
```

###### 无参数的调用

```javascript
function a() {
	console.log("hello world");
}
a();
a.call();
```

###### 有参数的调用

```javascript
function m(a, b) {
	console.log(a);
	console.log(b);
}
m.call(null, 3, 4);

// 通过call去调用有参数的方法的时候，call里面的第一个参数代表this的指向，而后面的参数则与调用方法的形参实现了一一对应的关系

function m(a, b) {
	console.log(a);
	console.log(b);
	console.log(this);
}
function n() {
	console.log(111111);
}
m.call(null, 3, 4); // 3 4 window
m.call(n, 3, 4); // 3 4 f n(){...}
// call改变了this的指向，使得n可以调用m的方法，也就是n去执行了m的内容
```
> **说明：**call 方法可以用来代替另一个对象调用一个方法，call 方法可以将一个函数的对象上下文从初始的上下文改变为 obj 指定的新对象，如果没有提供 obj 参数，那么 Global（也可以说是 window）对象被用于 obj；

##### apply() 调用

和`call()`方法一样，只是参数列表不同，语法：

```javascript
Function.apply(obj, argArray);
// obj：这个对象将代替Function类里的this 对象
// argArray：这个是数组，他将作为参数传给Function
```

###### 无参数调用

```javascript
function a() {
	console.log("hello world");
}
a();
a.apply();
// 在无参数的情况下，apply和call效果是一样的
```

###### 有参数方法调用

```javascript
function m(a, b) {
	console.log(a);
	console.log(b);
}
m.apply(null, [3, 4]);

// 通过apply去调用有参数的方法的时候，apply里面的第一个参数代表this的指向，第二个参数它是一个数组，它把所有的实参封装成了一个数组，传递到形参里面去，数组里面的元素与形参实现对应关系

function m(a, b) {
	console.log(a);
	console.log(b);
	console.log(this);
}
function n() {
	console.log(111111);
}
m.apply(null, [3, 4]); // 3 4 window
m.apply(n, [3, 4]); // 3 4 f n(){...}
```

> **说明：**如果 `argArray` 不是一个有效的数组或不是一个 `arguments`对象，那么将导致 `TypeError` ，如果没有提供`argArray`和`obj`任何一个参数，那么 Global（window）对象将用作`obj`。

##### 两者的相同点：

```javascript
function People(name, age){
    this.name = name;
    this.age = age;
}
function Student(name, age, grade){
    People.call(this, name, age);
    this.grade = grade;
}
var student = new Student('张三', 21, '大三');
console.log(student.name, student.age, student.grade);
// 张三 21 大三

/*
	在这个例子中，我们并没有给Student的name和age赋值，但是存在这两个属性的值，还是要归功于call()方法，它可以改变this的指向。
	在这里例子里，People.call(this, name, age);中的this代表的是Student，这也就是之前说的，使得Student可以调用People中的方法，因为People中有this.name = name;等语句，这样就将name和age属性创建到了Student中。
*/
```

总结一句话就是`call()`可以让**括号里的对象来继承括号外函数的属性**。

至于`apply()`方法作用也和`call()`方法一样，可以这么写：

```javascript
People.call(this, name, age);
People.apply(this, [name, age]);
// 或者
People.apply(this, arguments);
// 在这里arguments和[name, age]是等价的。
```

##### 两者的不同点：

从定义中也可以看出来，`call()`和`apply()`的不同点就是**接收参数的方式不同**。

```javascript
func.call(this, arg1, arg2); //call传递序列参数
func.apply(this, [arg1, arg2]); //apply传递数组
```

- **apply()方法**接收两个参数，一个是函数运行的作用域（`this`），另一个是参数数组。
- **call()方法**不一定接受两个参数，第一个参数也是函数运行的作用域（`this`），但是传递给函数的参数必须列举出来。

> 在给对象参数的情况下,如果参数的形式是数组的时候,比如之前`apply()`方法示例里面传递了参数`arguments`,这个参数是数组类型,并且在调用`Person`的时候参数的列表是对应一致的(也就是`Person`和`Student`的参数列表前两位是一致的)就可以采用`apply()`方法。

> 但是如果`Person`的参数列表是这样的`(age,name)`，而 Student 的参数列表是`(name,age,grade)`，这样就可以用`call()`方法来实现了,也就是直接指定参数列表对应值的位置`Person.call(this,age,name)`。

---

#### bind() 方法

语法格式：

```javascript
fun.bind(this,arg1,arg2,...)
```

bind()方法会创建一个新的函数，称为绑定函数,fun 方法在 this 环境下调用
该方法可传入两个参数，第一个参数作为 this，第二个及以后的参数则作为函数的参数调用 （后面传参类似于 call 方法）

```javascript
var test = function () {
	console.log(this.x);
};
var o = {
	x: 1,
};
test(); //undefined
test.bind(o)(); //1
/*
	第一次调用this指向全局，
	第二次test.bind(o)() 这个this指向o，通过观察可以知道test.bind(o)此时是一个函数，说明bind返回的是一个函数。
*/

window.color = "red"; // var color = 'red';
var o2 = {
	color: "blue",
};
function sayColor() {
	console.log(this.color);
}
var objSayColor = sayColor.bind(o2);
objSayColor(); // blue
/*
	sayColor()调用bind()并传入了o2，创建了objSayColor()函数，该函数的this值等于o2，因此即便是在全局作用域中调用这个函数，也能看到“blue”。
*/
```

传参方式：

```javascript
var test = function (a, b, c) {
	console.log("a=" + a, "b=" + b, "c=" + c);
};
var o = {
	x: 1,
};
test.bind(o)(1, 2, 3); //a=1 b=2 c=3
test.bind(o, 1)(2, 3); //a=1 b=2 c=3
test.bind(o, 1)(); //a=1 b=undefined c=undefined
test.bind(o, 1, 2)(); //a=1 b=2 c=undefined
test.bind(o, 1, 2, 3)(); //相当于调用test(1,2,3)   a=1 b=2 c=3
```

**案例：**思考分别为什么值？

```javascript
var name = "小张",
	age = 17;
var obj = {
	name: "小刘",
	objAge: this.age,
	myFun: function (a, b) {
		console.log(this.name, this.age, a, b);
	},
};
var db = {
	name: "开心果",
	age: 99,
};

obj.myFun();
obj.myFun.call();
obj.myFun.call(db);
obj.myFun.apply(db);
obj.myFun.bind(db)();

obj.myFun.call(db, 1, 2);
obj.myFun.apply(db, [1, 2]);
obj.myFun.bind(db, 1, 2)();
obj.myFun.bind(db, [1, 2])();
```

call、 bind、 apply 这三个函数的第一个参数都是 this 的指向对象，第二个参数差别就来了：

- call 的参数是直接放进去的，第二第三第 n 个参数全都用逗号分隔，直接放到后面 obj.myFun.call(db,1,2)。

- apply 的所有参数都必须放在一个数组里面传进去。

- bind 除了返回函数以外，它的参数和 call 一样。 （因为返回的是函数，所以别忘记需要调用才能执行）

  当然，三者的参数不限定是 String 类型，允许是各种类型，包括函数，对象等等。

---

### this 的指向

它是函数运行时，在函数体内部自动生成的一个对象，只能在函数体内部使用。

函数的不同使用场合，`this`有不同的值。总的来说，`this`就是函数运行时所在的环境对象。

1. **全局状态下的 this 指向**

   在全局状态下，this 指向了全局对象（在浏览器里面，全局对象是指浏览器`window`对象，而在`NodeJs`下面则会指向`Global`对象）
   ```javascript
   var x = 1;
   function test() {
   	console.log(this.x);
   }
   test(); // 1
   ```

2. **方法里面的 this 指向**
```javascript
function a(){
    console.log(this.name);
}
var obj={
    name:"天天",
    age:18
}
```

    - 做为常规调用的方法，它的`this`指向了全局对象`window`
  ```javascript
  a(); //这个时候，里面的this就指向了全局对象window
  ```

    - 方法通过 call 与 apply 进行调用的时候，this 则指向传入的第一个参数
  ```javascript
  a.call(obj);
  // 这个时候a方法里面的this就指向了obj,在上面的调用里面，call方法的第一个参数就是设置this的指向

  a.apply(obj);
  //这种情况与call的情况是一样的，它们的第一个参数都是设置this的指向
  ```

    - 对象里面属性方法的 this ， 这时`this`就指这个上级对象。
  ```javascript
  var stu = {
  	name: "张三",
  	sayHello: function () {
  		console.log(this.name);
  	},
  };
  stu.sayHello();
  // sayHello它是一个属性方法，属性方法里面的this指向当前对象
  ```

3.  **作为构造函数调用**

    所谓构造函数，就是通过这个函数，可以生成一个新对象。这时，`this`就指这个新对象。
    ```javascript
    function test() {
    	this.x = 1;
    }

    var obj = new test();
    obj.x; // 1

    // 运行结果为1。为了表明这时this不是全局对象,我们对代码做一些改变：

    var x = 2;
    function Test() {
    	this.x = 1;
    }

    var obj = new Test();
    x; // 2
    // 运行结果为2，表明全局变量x的值根本没变。
    ```
