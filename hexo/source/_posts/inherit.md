---
title: JavaScript - 对象的继承
tags: ['对象的继承', '内置对象', prototype, constructor]
categories: javascript
---
## 对象的继承

面向对象编程很重要的一个方面，就是对象的继承。

A 对象通过继承B对象，集能直接拥有B对象的所有属性和方法。

 大部分面向对象的编程语言，都是通过“类”（class）实现对象的继承。 javascript语言的继承不通过 class，而是通过”原型对象“（prototype）实现。
<!--more-->
------

### 原型对象

#### 构造函数的缺点

 JavaScript 通过构造函数生成新对象，因此构造函数可以视为对象的模板。实例对象的属性和方法，可以定义在构造函数内部。 

```jsx
function Person(name, age){
    this.name = name;
    this.age = age;
}
var p1 = new Person('陈昭文', 10);
var p2 = new Person('天天', 20);

p1.name; // 陈昭文
p1.age; // 10

p2.name;
p2.age;
```

 上面代码中，`Person`函数是一个构造函数，函数内部定义了`name`属性和`age`属性，所有实例对象（上例是`p1`）都会生成这两个属性，即这两个属性会定义在实例对象上面。 

 通过构造函数为实例对象定义属性，虽然很方便，但是有一个缺点：

​	 **同一个构造函数的多个实例之间，无法共享属性，从而造成对系统资源的浪费。** 

```jsx
function Person(name, age){
    this.name = name;
    this.age = age;
    this.fn = function(){
        console.log('大家好');
    }
}
var p1 = new Person('陈昭文', 10);
var p2 = new Person('杨欢', 20);

p1.fn === p2.fn; // false
```

 上面代码中，`p1`和`p2`是同一个构造函数的两个实例，它们都具有`fn`方法。由于`fn`方法是生成在每个实例对象上面，所以两个实例就生成了两次。也就是说，每新建一个实例，就会新建一个`fn`方法。这既没有必要，又浪费系统资源，因为所有`fn`方法都是同样的行为，完全应该共享。 

 这个问题的解决方法，就是 JavaScript 的原型对象（prototype）。 



#### prototype 属性的作用

 JavaScript 继承机制的设计思想就是：**原型对象的所有属性和方法，都能被实例对象共享。** 

 也就是说，如果属性和方法定义在原型上，那么所有实例对象就能共享，不仅节省了内存，还体现了实例对象之间的联系。 

JavaScript 规定，每个**函数**都有一个`prototype`属性，指向一个对象。 先看怎么为对象指定原型。

```jsx
function f(){}
typepf f.prototype // object
```

 上面代码中，函数`f`默认具有`prototype`属性，指向一个对象。 

 对于普通函数来说，该属性基本无用。但是，**对于构造函数来说，生成实例的时候，该属性会自动成为实例对象的原型。** 

```jsx
function Person(name){
    this.name = name;
}
Person.prototype.age = 20;

var p1 = new Person('陈昭文');
var p2 = new Person('杨欢');

p1.age; // 20
p2.age; // 20
```

 上面代码中，构造函数`Person`的`prototype`属性，就是实例对象`p1`和`p2`的原型对象。原型对象上添加一个`age`属性，结果，实例对象都共享了该属性。 

 如果实例对象自身就有某个属性或方法，它就不会再去原型对象寻找这个属性或方法。 

```jsx
Person.prototype.age = 30;

p1.age; // 30
p2.age; // 30
```

 上面代码中，原型对象的`age`属性的值变为`30`，两个实例对象的`age`属性立刻跟着变了。这是因为实例对象其实没有`age`属性，都是读取原型对象的`age`属性。

也就是说，**当实例对象本身没有某个属性或方法的时候，它会到原型对象去寻找该属性或方法。**这就是原型对象的特殊之处。 

 **如果实例对象自身就有某个属性或方法，它就不会再去原型对象寻找这个属性或方法。** 

```jsx
p1.age = 23;

p1.age; // 23
p2.age; // 30
Person.prototype.age; // 30
```

 上面代码中，实例对象`p1`的`age`属性改为`23`，就使得它不再去原型对象读取`age`属性，后者的值依然为`30`。 

> 总结一下，**原型对象的作用**，就是定义**所有实例对象共享的属性和方法**。这也是它被称为原型对象的原因，而实例对象可以视为从原型对象衍生出来的子对象。

```jsx
Person.prototype.sayHello = function(){
    console.log('你好, '+this.name);
}
```

 上面代码中，`Person.prototype`对象上面定义了一个`sayHello`方法，这个方法将可以在所有`Person`实例对象上面调用。 



#### 原型链

 JavaScript 规定，所有对象都有自己的**原型对象（prototype）**。 

1. 任何一个对象，都可以充当其他对象的原型； 

2. 由于原型对象也是对象，所以它也有自己的原型。 

 因此，就会形成一个“原型链”（prototype chain）：**对象到原型，再到原型的原型……** 

 如果一层层地上溯，所有对象的原型最终都可以上溯到`Object.prototype`，即`Object`构造函数的`prototype`属性。也就是说，所有对象都继承了`Object.prototype`的属性。 

>  读取对象的某个属性时，JavaScript 引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。如果直到最顶层的`Object.prototype`还是找不到，则返回`undefined`。 
>
>  如果对象自身和它的原型，都定义了一个同名属性，那么优先读取对象自身的属性，这叫做“覆盖”（overriding）。 

**注意：**

 一级级向上，在整个原型链上寻找某个属性，对性能是有影响的。所寻找的属性在越上层的原型对象，对性能的影响越大。如果寻找某个不存在的属性，将会遍历整个原型链。 

 举例来说，如果让构造函数的`prototype`属性指向一个数组，就意味着实例对象可以调用数组方法。 

```jsx
var MyArray = function(){}

MyArray.prototype = new Array(); // MyArray的原型指向一个数组
MyArray.prototype.construcor = MyArray; // 原型上的constructor 指向构造函数

var mine = new MyArray();
mine.push(1,2,3);
mine.length; // 3
mine instanceof Array; // true
```

 上面代码中，`mine`是构造函数`MyArray`的实例对象，由于`MyArray.prototype`指向一个数组实例，使得`mine`可以调用数组方法（这些方法定义在数组实例的`prototype`对象上面）。最后那行`instanceof`表达式，用来比较一个对象是否为某个构造函数的实例，结果就是证明`mine`为`Array`的实例 。



#### constructor属性

```prototype```对象有一个```constructor```属性，默认指向 `prototype`对象所在的构造函数。 

```jsx
function P() {}
P.prototype.constructor === P // true
```

 由于`constructor`属性定义在`prototype`对象上面，意味着可以被所有实例对象继承。 

```jsx
function Person() {}
var p1 = new Person();

p1.constructor === Person // true
p1.constructor === Person.prototype.constructor // true
```

 上面代码中，`p1`是构造函数`Person`的实例对象，但是`p1`自身没有`constructor`属性，该属性其实是读取原型链上面的`Person.prototype.constructor`属性。 

 ***`constructor`属性的作用是:***

1. **可以得知某个实例对象，到底是哪一个构造函数产生的。** 
```jsx
function F() {};
var f = new F();

f.constructor === F // true
f.constructor === RegExp // false
```
 上面代码中，`constructor`属性确定了实例对象`f`的构造函数是`F`，而不是`RegExp`。 

2. 另一方面，有了`constructor`属性，**就可以从一个实例对象新建另一个实例。** 
   ```jsx
   function Constr() {}
   var x = new Constr();
   
   var y = new x.constructor(); // x.constructor == Constr
   y instanceof Constr // true
   
   /*
   	上面代码中，x是构造函数Constr的实例，可以从x.constructor间接调用构造函数。这使得在实例方法中，
       调用自身的构造函数成为可能。
   */
   ```

   ------

   ```jsx
   // instanceof: A instanceof B，判断A是否是B的实例对象或者B子类的实例对象。
   // constructor: A.constructor === B, A是不是B构造出来的。 
   /*
   	根据上面图解得到：
   		p instanceof Person  ===> true
           
           p instanceof Object  ===> true
           
           p.constructor === Person ===> true
           
           p.constructor === Object ===> false    
   */
   /*
   	Person.prototype === p.__proto__
   	Person.prototype.constructor === Person
   	p.__proto__.constructor === Person
   	
   	原型对象的原型：p.__proto__.__proto__ / Person.prototype.__proto__
   */
   function Person(){
       this.name = '我是name';
   }
   var p = new Person();
   ```
   
   
   
   ```jsx
   var 实例 = new 构造函数(); ==> 实例.__proto__ = 构造函数.prototype
   
   构造函数.prototype: 原型对象 + 原型对象.constructor: 构造函数 
   => 构造函数.prototype.constructor : 构造函数
   
   实例.__proto__ ： 原型对象
   ```
   
   
   
   构造函数.prototype.__proto__ === Object.prototype
   
   
   
   对象就是**实例**
   
   
   
   `new` 操作的叫**构造函数**，构造函数可以使用new生成实例。
   
   构造函数也是函数，函数声明的时候会自带`prototype`属性，`prototype`指向的是**原型对象**。原型对象的构造器（`constructor`）指向声明的函数。
   
   
   
   **原型链**：从一个实例对象往上找构造这个实例的相关联的对象，这个相关联的对象往上找，它也有它的上一级的原型对象，以此类推，一直到`object.prototype`
   
   通过`prototype`这个原型和`_proto_`这个属性来完成原型链的查找
   
   
   
   `instanceof`：判断实例对象的`_proto_`属性和构造函数的`prototype`属性是不是引用同一个地址
   
   `constructor`判断比`instanceof`更加严谨
   
   
   
   ```jsx
   // 原型链
   var a1 = new Array();
   /*
   	a1._proto_ === Array.prototype
   	Array.prototype._proto_ === Object.prototype
   */
   ```
   
   

------



### 对象继承对象

 当一个对象继承了另一个对象以后，那么，我们不妨考虑以下几个问题 :

1. 如果用户找子级对象拿东西，如果子级对象有，就不找父级对象要了

2. 如果子级对象没有就找父级对象要
```jsx
/* 
     借助构造函数实现继承
     缺点：无法继承父级原型对象上的方法
*/
function Parent1(){
    this.name = 'parent1';
}
Parent1.prototype.say = function(){};
function Child1(){
    Parent1.call(this); // 重点：将父级的this指向到子级的构造函数上去
    this.type = 'child1';
}
console.log(new Child1);

/* 
    借助原型链实现继承
    缺点：改变一个实例，另一个也会跟着改变
*/
function Parent2(){
    this.name = 'parent2';
    this.play = [1,2,3];
}
function Child2(){
    this.type = 'child2';
}
Child2.prototype = new Parent2();
// console.log(new Child2); // new Child2().__proto__ === Child2.prototype
var c1 = new Child2();
var c2 = new Child2();
c1.play.push(4);
console.log(c1.play, c2.play);

/* 
   借助组合方式实现继承
   缺点：父级被调用了两次
*/
function Parent3(){
    this.name = 'parent3';
    this.play = [1,2,3];
}
function Child3(){
    Parent3.call(this);
    this.type = 'child3';
}
Child3.prototype = new Parent3();
var c3 = new Child3();
var c4 = new Child3();
c3.play.push(4);
console.log(c3.play, c4.play);

/* 
   组合方式优化2
*/
function Parent4(){
    this.name = 'parent4';
    this.play = [1,2,3];
}
function Child4(){
    Parent4.call(this);
    this.type = 'child4';
}
Child4.prototype = Parent4.prototype;
var c5 = new Child4();
console.log(c5);
```

------

### 对象属性的判断

 怎么样判断某一个属性是否存在于当前对象之中 

```javascript
function Person(userName,sex,age){
    this.userName=userName;
    this.sex=sex;
    this.age=age;
    this.sayHello=function(){
        console.log("我在向你问好");
    }
}

function Student(userName,sex,age,sid){
    this.sid=sid;
    this.__proto__=new Person(userName,sex,age);
}

var s1=new Student("张三","男",18,1);
//判断sid这个属性在不在s1里面
//判断userName这个属性在不在s1里面
```

 **第一种方式** 
 判断一个对象是否具备某一个属性，我们可以通过关键字`in`来实现 
```javascript
console.log("sid" in s1);         //true      存在于当前对象
console.log("userName" in s1);    //true      存在于父级对象
console.log("aaa" in s1);         //false     彻底不存在

// in关键字不仅可以检测我们的当前对象，还跑到父级对象去检测去了
```

 **第二种方式** 
```javascript
s1.hasOwnProperty("sid");    //true
s1.hasOwnProperty("age");    //false

// hasOwnProperty只在当前对象去判断 ，不去父级对象去找
```
>  **总结**：`hasOwnProperty`只在当前对象判断，而`in`关键字会跑到父级对象里面去找。
>
> 如果存在则返回true,如果不存在则返回false。检测属性是否存在的目的就是为了后期更好的去调用这个属性或属性方式 

```javascript
var obj={
    sex:"女"
};
Object.defineProperty(obj,"userName",{
    value:"天天",
    enumerable:false       //不通过被for...in遍历出来
});
console.log("userName" in obj);    //true
obj.hasOwnProperty("userName");    //true
```

>  `enumerable`这个特性仅仅只是用来设置遍历的时候使用的，不是用来设置是否存在这个属性的 

------



### 遍历对象的属性

 在`JS`里面，我们有两种方式遍历对象的属性 



#### 通过`Object.keys()`

 通过这种方式，我们可以获取对象里面所有的 key(属性) 

```javascript
var 属性名数组 = Object.keys(对象);
```

 **第一种情况** 
```javascript
var obj={
    userName:"张三",
    sex:"男",
    age:18
}
Object.keys(obj);   //得到 ["userName", "sex", "age"]
```

**第二种情况** 
```javascript
var obj={
    userName:"张三",
    sex:"男",
    age:18
}

Object.defineProperty(obj,"sid",{
    value: 001,
    enumerable:false
});
Object.keys(obj);   //得到的结果仍然是["userName", "sex", "age"]

/*
上面我们给obj对象添加了一个特殊的属性sid，这个时候，得到的结果是["userName", "sex", "age"],这就说明Object.keys不能够拿到enumerable:false的属性
*/
```

 **第三种情况** 
```javascript
var stu={
    userName:"张三",
    sex:"男",
    age:18
}

var p1={
    addr:"湖北武汉"
}

//设置了stu的父级对象为p1
stu.__proto__=p1;

Object.keys(stu);    //结果仍然是["userName", "sex", "age"]

/*
	上面的stu设置了一个父级对象p1,但是，我们通过Object.keys去获取对象所有的属性的时候，还是获取不到父级的
*/
```

>  **总结**：`Object.keys`只获取当前对象的`enumerable`不为`false`的所有属性，它返回一个数组 

 所以我们使用`Object.keys`去遍历属性的时候，我们可以通过如下代码实现 

```javascript
Object.keys(stu).forEach(function(item,index,a){
    console.log(item);  //打印了所有的属性名
});
```



#### 通过`for...in`来获取对象属性名

 **第一种情况** 
```javascript
var stu={
    userName:"张三",
    sex:"男",
    age:18
}
for(var i in stu){
    //如果是数组，i指的是数组的索引，如果是对象i则指属性名
    console.log(i);
}
```

 **第二种情况** 
```javascript
var stu={
    userName:"张三",
    sex:"男",
    age:18
}

Object.defineProperty(stu,"addr",{
    value:"湖北武汉",
    enumerable:false
});

for(var i in stu){
    console.log(i);    //userName,sex,age
}

// for...in不能去遍历enumerable:false这种属性
```

 **第三种情况** 
```javascript
var stu={
    userName:"张三",
    sex:"男",
    age:18
}

var p1={
    addr:"湖北武汉"
}
//设置了stu的父级对象为p1
stu.__proto__=p1;

for(var i in stu){
    console.log(i);    //userName,sex,age,addr
}

// for...in会到父级对象去遍历属性，这一点与Object.keys是截然不同的
```

 **上面的属性判断与属性遍历，现通过表格总结如下** 

| 遍历方式       | 当前对象普通属性 | 当前对象enumerable:false | 父级对象 |
| -------------- | ---------------- | ------------------------ | -------- |
| Object.keys    | true             | false                    | false    |
| for...in       | true             | false                    | true     |
| in判断         | true             | true                     | true     |
| hasOwnProperty | true             | true                     | false    |

------



## 常用内置对象

### Math对象

 `Math`是 JavaScript 的原生对象，提供各种数学功能。该对象不是构造函数，不能生成实例，所有的属性和方法都必须在`Math`对象上调用。 

#### 静态属性

 **`Math`对象的静态属性，提供以下一些数学常数。** 

- `Math.E`：常数`e`。

- `Math.LN2`：2 的自然对数。

- `Math.LN10`：10 的自然对数。

- `Math.LOG2E`：以 2 为底的`e`的对数。

- `Math.LOG10E`：以 10 为底的`e`的对数。

- `Math.PI`：常数 Pi。

- `Math.SQRT1_2`：0.5 的平方根。

- `Math.SQRT2`：2 的平方根。

  ```jsx
  Math.E // 2.718281828459045
  Math.LN2 // 0.6931471805599453
  Math.LN10 // 2.302585092994046
  Math.LOG2E // 1.4426950408889634
  Math.LOG10E // 0.4342944819032518
  Math.PI // 3.141592653589793
  Math.SQRT1_2 // 0.7071067811865476
  Math.SQRT2 // 1.4142135623730951
  ```

 **这些属性都是只读的，不能修改。** 



#### 静态方法

 **`Math`对象提供以下一些静态方法。**

- `Math.abs()`：绝对值
- `Math.ceil()`：向上取整
- `Math.floor()`：向下取整
- `Math.max()`：最大值
- `Math.min()`：最小值
- `Math.pow()`：指数运算
- `Math.sqrt()`：平方根
- `Math.log()`：自然对数
- `Math.exp()`：e的指数
- `Math.round()`：四舍五入
- `Math.random()`：随机数



1.  绝对值abs() 方法 
   ```javascript
   Math.abs(-100);    //100;
   Math.abs(100);     //100;
   ```

2.  round() 四舍五入的方法 
   ```javascript
   var a=3.4;
   Math.round(a);   //3
   a=3.6;
   Math.round(a);   //4
   ```
    **注意**：`Math.round()`只能够四舍五入到整数，如果需要保留多位小数的四舍五入，需要乘一个数 
   ```javascript
   var a=3.1415926;
   //现在需要保留三位小数的四舍五入  3.142;
   Math.round(a*1000)/1000;
   ```

3.  floor() 向下取整，返回小于或等于这个数的最大整数 
   ```javascript
   Math.floor(99.2);     //99
   Math.floor(15.5);     //15
   Math.floor(11);       //11
   ```

4.  ceil() 向上取整，返回大于或等于这个数的小最整数 
   ```javascript
   Math.ceil(99.2);     //100
   Math.ceil(11.5);     //12
   Math.ceil(11);       //11
   ```

5.  pow(x,n)函数，返回一个数的x的n次方结果 
   ```javascript
   var i=100;
   var j=3;
   var k = Math.pow(i,j);   //100*100*100
   ```

6.  max(...number[])方法，返回这些数里面的最大值 
   ```javascript
   Math.max(100,77,210);    //210
   ```

7.  min(...number[])方法，返回这些数里面的最小值 
   ```javascript
   Math.min(100,77,210);    //77
   ```

8.  sqrt(n)求数n的平方根 
   ```javascript
   Math.sqrt(9);     //3
   ```

9.  random()随机数，返回0~1之间的随机数 ，能等于0，但是一定小于1。 
   ```javascript
   Math.random();
   //返回随机数0.8154782066518957
   ```
    怎么样返回0-9之间的随机数 
   ```javascript
   var temp = parseInt(Math.random()*10);
   //这个时候得到的随机数是0~9之间的随机数
   // 求 1-10的随机数
   ```

   >  **小技巧**：如果后期要取一个0到某一个数的随机数可以直接`parseInt(Math.random()*num)`,不包含`num` 

------



### Date对象

 `Date`对象是 JavaScript 原生的时间库。

 JS里面用来表述日期的对象，它可以获取当前系统的时间与日期，每次新得到的对象都指向了当前的时间 

 **Date即是构造函数也是对象** 

```javascript
var d=new Date();
//创建一个日期对象，d是创建好的对象，指向创建这个对象的时候的时间
```



#### 方法

1.  now()方法，返回当前时间，要注意，它返回的是一串数字，这串数字是一个时间戳，指的是从1970-1-1到现在的毫秒数 
   ```javascript
   Date.now(); 
   // 这个时候，这个Date它就是一个对象了
   ```

2.  获取年份的方法getFullYear() 
   ```javascript
   var d=new Date();   //得到当前时间
   //怎么样得到年份呢
   var year=d.getFullYear();   //得到2019
   ```

3.  获取月份的方法getMonth() 
   ```javascript
   d.getMonth();  
   //获取当前时间的月份，从0开始
   ```

4.  获取当前日期的天数getDate(); 
   ```javascript
   d.getDate(); 
   //获取当前时间的天数，从1开始
   ```

5.  获取当前日期的星期getDay() 
   ```javascript
   d.getDay();
   //获取当前星期几，从0开始，星期天才是0
   ```

6.  获取小时数getHours() 
   ```javascript
   d.getHours();  //获取当前小时数
   ```

7.  获取分钟getMinutes() 
   ```javascript
   d.getMinutes();
   ```

8.  获取秒钟数getSeconds() 
   ```javascript
   d.getSeconds();
   ```

9.  获取毫秒数getMilliseconds() 
   ```javascript
   d.getMilliseconds();
   ```
 上面的九个方法都是获取(get)日期与时间的相关信息，与之相对应的还有set赋值的方法 
 如果想设置一个日期相关的信息，我们可以调用相关的set方法就可以了 
```javascript
var d=new Date();  //创建日期对象
d.setFullYear(2000);   //设置年份
d.setMonth(11);     //设置月份为12月，请将这个值设置为0~11之间，它可以大于11，但不推荐赋大于11的值
```



#### `toString`方法

  `Date`实例求值的时候，默认调用的是`toString()`方法。这导致对`Date`实例求值，返回的是一个字符串，代表该实例对应的时间。 

日期函数可以调用toString方法把其转换成字符串，但是在转换的过程当中，我们还需要有一些注意事项 

1.  `toString()` 它会把当前时间转换成字符串 

    `toDateString()`它会把当前时间转换成日期字符串 

    `toTimeString()`它会把当前的时间转换成时间字符串 
   ```javascript
   var d=new Date();
   d.toString();
   d.toDateString();  
   d.toTimeString(); 
   ```

2.  `toLocaleString()`转换成本地时间，也就是你电脑右下角的格式时间 

    `toLocaleDateString()` 转换成本地的日期字符串 

    `toLocaleTimeString()` 转换成本地的时间字符串 
   ```javascript
   var d=new Date();
   d.toLocaleString();  		
   d.toLocaleDateString();    
   d.toLocaleTimeString();     
   ```

3.  `toGMTString()` 将当前时间转换成0时区的时间 
   ```javascript
   var d=new Date();
   d.toGMTString();
   ```

------



### 包装对象

 通过`typeof`检测出来的数据类型有以下几种 

1. string字符串类型

2. number数字类型

3. boolean布尔类型

4. undefined未定义类型

5. object对象类型

6. function方法类型

    

 在上面这些用来表示类型的关键字里面，它们的首字母都是小写

> 但是有些情况，我们发现电脑里面与之有一个同名的首字母大写的英语文单词
>
> ```
> string`-------`String`,`number`-------`Number`,`boolean`-----`Boolean`,`object`-------`Object
> ```

 **概念**：什么是包装对象？包装对象指的是`String`,`Number`以及`Boolean`这些对象，这三种包装对象其实本质上面指的是`string`,`number`以及`boolean`这三种基本数据类型 

 包含对象其实就是为之前的基本数据类型里面的三个类型服务的，因为有了这三个包装对象以后，字符串，数字以及布尔布类型就可以像对象一样去调用它们的属性以及方法了 

```javascript
string.__proto__===String;
number.__proto__===Number;
boolean.__proto__===Boolean;
```

 它具备像上面这种特点以后，那么字符串类型，数字类型以及布尔类型就可以像对象一样去分别调用它们父级里面的方法与属性了 



#### String字符串对象

>  字符串对象也是一个特殊的字符数组,它可以过索引取出里面的每一个字符，字符串对象的单引号与双引号是没有区别的 

1.  `length`属性 

    返回当前字符串的长度，它不能赋值 

   

2.   `charAt`获取某一位置的字符串，相当于string[索引] 
   ```javascript
   var s="hello";
   s.charAt(1);    //"e"
   s[1];           //"e"
   ```

3.  `charCodeAt()`获取某一位置字符串的`unicode`编写，这个编码是0~65535之 
   ```javascript
   var s="我爱你";
   s.charCodeAt(0);    //获取0位置的unicode编码
   //结果是25105
   ```

4.  `concat()`字符串的拼接，返回一个新的字符串，其实没啥用，因为我们都用`+` 

5.  `startsWith()`判断某个字符串是不是以什么开始 
   ```javascript
   var s="我爱北京天安门";
   s.startsWith("我");  //true  说明是以我开头的
   ```

6.  `endsWith()`判断某个字符串是不是以什么结束 
   ```javascript
   var url="http://www.baidu.com";
   url.endsWith(".com"); //true
   ```

7.  `includes()`判断是否包含某个字符串,包含就是true,不包含就是false 
   ```javascript
   var s="我爱北天安门";
   s.includes("北京");   //true
   ```

8.  `indexOf/lastIndexOf;`查找字符串的匹配，与数组里面的用法保持一致，找到以后返回索引，找不到返回-1 
   ```javascript
   var s="我爱北京天安门";
   s.indexOf("天");
   ```

9.  `trim/trimLeft/trimRight`去除空格的方法 

    `trimLeft`去除左边的空格 

    `trimRight`去除右边的空格 

    `trim`去除左右的空格 
   ```javascript
   var s1="  我爱北京天安门  ";
   s1.trimLeft();
   s1.trimRight();
   s1.trim();
   ```

10.  `replace()`查找字符串然后替换成新的字符串，并返回替换以后的结果 
    ```javascript
    var s1="上课啊";
    s1.replace("上","下"); 
    ```

11.  `substr/substring/slice`截取字符串的方法 
    -  slice方法,截取字符串,它的用法与数组相同，第一个参数代表开始索引，第二个参数代表结束索引的前一个,它返回一个新的字符串，原字符串是没有发生改变的 

       开始索引不能大于结束索引 
      ```javascript
      var s="hello world";
      s.slice(3,7);   //"lo w";
      s.slice(3,-1);  //"lo worl";
      s.slice(-4,-1); //"orl";
      s.slice(3);    //从3开始一直到最后一个"lo world";
      ```
        -  `substring`方法，截取字符串,返回一个新的字符串，原字符串不改变 

       它的第一个参数代表开始索引，第二个参数代表结束索引的前一个 
      ```javascript
      var s="hello world";
      s.substring(3,7);  //"lo w";
      // 在这个方法里面，我们不建议使用负值
      ```

        -  `substr`方法，截取字符串，返回一个新的字符串，原字符串不改变 

       它的第一个参数代表开始索引，它的第二个参数代表你要截取的长度 
      ```javascript
      var s="hello world";
      s.substr(3,7);   //"lo worl";
      ```

12.  `split`分割字符串 

     该方法非常重要。它可以将字符串按照指定的字符隔开成数组 
    ```javascript
    var str="你好吗？我很好~";
    str.split("？"); 
    // ["你好吗", "我很好~"]
    ```
    >  split其实就是和数组里面的join方法是相呼应的，join是将数组按指定指定字符隔开转成字符串，而split而是将字符串按指定字符分割成数组 

13.  `toUpperCase/toLowerCase`大小写转换，返回转换以后的新字符串，原来的字符串不做改变 
    ```javascript
    var str="hello world";
    str.toUpperCase();   //得到"HELLO WORLD";
    var str1="HELLO WORLD";
    str1.toLowerCase();
    ```

