---
title: JavaScript -函数
tags: 函数
categories: js
---

## 函数

**概念**：

将任意多条代码组装在一起，可以在任何地方经过任意多次的**调用执行**，多次组装在一起的代码需要通过 关键字**function**来定义
<!--more-->
```javascript
- 变量是通过 var 来定义的
- 函数是通过 function 拉定义的
程序是通过一行一行的语句来组成的，语句是组成代码最基本的单位，同时这些基本单位，我们也可以把它组合在一起分成一个一个的小模块，将这些语句分成一个一个小模块的功能，我们叫方法
```

---

#### 定义函数的方式

##### 通过关键字 function 定义

函数定义需要通过关键字 function，定义的语法格式如下：
```javascript
function 方法名(参数1，参数2....){
    // 代码体
}
function a(参数1，参数2){
    // 代码体
}
//----------------------
通过上面的语法格式，我们可以自己尝试着去定义一个方法

function sayHello(a,b){
    console.log('世界，你好');
}
typeof sayHello; // 类型结果为“function”

```

代码分析：
1. function 是定义方法的关键字
2. sayHello 则是这个方法的名字
3. a 和 b 是方法的参数
4. 花括号里面的东西就是代码体

##### 通过函数表达式来定义

我们知道所有变量的定义都使用关键字 var 来进行， var 定义的变量后面跟什么数据，这个变量就是什么数据类型，比如：
```javascript
var a="hello";   //string类型
var b=123;  	 //number类型
var c=true;      //Boolean
var d=null;      //object
var f=undefined; //undefined;
//我们给什么样的值，它就是一个什么类型

//---------------------------
如果给一个变量赋值成一个function，是什么样子？

var sayHello = function(参数1,参数2...){
    // 代码体
}
typeof sayHello; // function
```

代码分析：
1. 所有变量的定义，我们都可以使用 var 来进行，变量后面跟什么数据 ，它就是什么类型
2. sayHello 后面根的是一个 function，所以 sayHello 它应该是一个 方法

##### 通过 Function 来进行定义

> 小写的 function 是关键字，大字的 Function 是系统自已定义了方法
```javascript
var sayHello = new Function();
typeof sayHello;   //function

// 这一种方式不建议大家去使用，它的使用场景是在后期方法动态创建里面
```

_三种定义函数的方式我们都要接触了解，但是在日常工作当中，你们所经常使用的方式就是第一种与第二种情况_

**思考**：既然我们在工作当中经常会使用到第一种与第二种的情况，那么请各位同学注意，第一种情况的定义与第二种情况的定义有啥区别？
```javascript
sayHello2();    //这一句代码它不会报
sayHello1();    //这一句代码会报错

var sayHello1=function(){
    console.log("hello world");
}
function sayHello2(){
    console.log("吃了没，世界");
}

1.function 关键字定义的方法可以在调用之前调用（任何地方，前后都行）
2.var 定义的方法只能在定义的代码之后去调用（执行上下文）

// 建议大家前期先用第一种，也就是function定义的方式
```

---

#### 函数的代码体，会形成作用域

用 var 定义的变量没有作用域，但是定义在 function 的花括号里面的代码，它是有作用域的
```javascript
function a(){
    // userName定义到了方法里面，所以它是有作用域的
    // 它的作用域是方法的花括号开始 ，到方法的花括号结束
    var userName = "天天";
    //在作用域的范围里面，我们可以随意的调用变量，但是一旦出了这个花括号 ，就不行了
}
console.log(userName); // 报错，提示 userName 没有被定义
```
**总结**：方法体里面定义的东西在方法体外边是不能够被使用的，如果真的要使用，可以使用后面我们学习的一另一个关键字 return

**终上所述**：如果你希望变量既能够在方法里面使用，也能够在方法外边使用，那么你就定义到方法的外边，如果你仅仅只是希望这个变量在方法里面使用，而不希望它在方法外边使用，则把它定义在方法的里面

我们一般把定义在方法里面的变量叫**局部变量**

把定义在方法外边的变量叫**全局变量**

---

#### 方法的调用

方法（函数）通过上面的三种方式定义好了以后，你不调用它，它就不会执行，因为方法是调用执行的

那么方法到底应该怎么调用呢？？？

> 方法的调用其实指的就是把之前写在 function 花括号里面的代码执行一次

##### 常规调用

这一种方式是最基本的调用方式，当一个方法定义好了以后就会存在一个方法名，我们的常规调用就是通过这一个方法名来进行调用

```javascript
方法名();
//它的调用方式就是方法名加()

//-------------------------
在这种方式里面，我们的调用是需要通过方法名来进行的（ 在调用方法的时候，我们可以给方法的参数赋值，这个赋值过程 ，我们叫传参）

function sayHello(){
    console.log("大家好才是真的好");
}
//现在我们已经在上面的代码时面定义了一个方法，如果我们不去调用它，那么它就永远不会执行，现在我们通过普通的方式去调用它
sayHello();   //调用方法，直接执行方法里面的代码
```

##### 立即执行函数

在某些时间，如果我们希望定义好了这些方法以后立即的执行一次，怎么办呢，这个时候，我们可以使用到立即执行函数

```javascript
//定义方法
function sayHello(){
    console.log("大家好");
}
//调用方法执行
sayHello();

在上面的代码里面， 我们可以看到之前已经定义好了一个方法，它的名子叫sayHello，然后我们又马上调用了它

像这样一种情况，在后期工作的时候如果碰到了，我们可以使用立即执行函数
//------------------------
+ function sayHello(){
    console.log('大家好');
}();
```

**代码分析**：

上面的代码通过 function 关键字定义好了 sayHello 方法以后，它在这个地方前面加了一个 + , 后面又添加上了一个()这个时候，碰到这种情况，大家要知道，这是一个立即执行函数，它定义好以方法以后，会立即执行一次

##### 函数表达式执行

```javascript
var sayHello=function(){
    console.log("大家好");
}
sayHello();

// 上面的代码同步与下面的代码

var sayHello=function(){
    console.log("大家好");
}();
```

**我们把上面的三种情况的调用归为第一大类情况，他们的调用最终都是需要去加括号的**

---

#### 函数的参数

```javascript
//我们在使用function定义方法的时候，除了定义方法名，还可以使用参数

function 方法名(参数1,参数2.....){
   //代码体
}
方法名(参数1,参数2.....)
```
- 定义方法的参数，可以理解成变量
- 定义参数的时候，我们可以把它当成是一个变量，但是，我们不能够再去使用 var 关键字了
```javascript
function sayHello(userName){
    console.log(userName)
}

代码分析：
    在上面的代码里面，我们通过function关键字定义了一个方法名为sayHello的方法，
    同时我们也看到后面的括号里面有userName,我们叫参数，
    你可以理解为，它就相当于在function里面定义的变量

    sayHello(); // undefined ，因为我们在调用方法的时候，如果方法需要参数，我们在调用的过程中给他参数

    sayHello('天天');

    //-----------------------------------

    上面的调用过程首先是先调用了方法sayHello，然后在调用的时候，还给之前定义的参数userName赋值为“天天”

    在调用方法的时候，值会赋值给参数，这个赋值的过程我们叫传参
```

##### a.形式参数

形式参数简称“形参”,指的是方法在定义的过程当中所使用（所出现）的参数

形参默认是没有值的，它的值默认情况下是 undefined

形参可以理解成变量，它的作用域只能在方法里面，不能在方法外边

##### b.实际参数

实际参数简称“实参”，指的是方法调用的时候里面的的真实参数（真实数据）

**重要**：值是由实参赋值给形参（也可以理解为值是由实参传递给形参）

##### c.实参与形参的对应关系

```javascript
function add(a,b){
    console.log(a);
    console.log(b);
}
add(10,20);

// 在上面的代码里面，我们在定义方法的时候，定义了两个形参，在调用方法的时候，我们给了两个实参
```

##### 思考：

​现在有如下三种情况，请同学们判断如何进行
```javascript
function add(a, b) {
	console.log(a);
	console.log(b);
}
```
1. 当实参与形参个数相同的时候
```javascript
add(10, 20);
//当实参与形参相同的时候，它们可以实现一一对应的关系，这个时候的a为10,b为20
```
2.  当实参小于形参个数的时候
```javascript
add(10);
//当实参个数小于形参个数的时候，前面的值实现一一对应，后面多出来的形参的值为undefined;
```
3.  当实参个数大于形参个数的时候
```javascript
add(10, 20, 30);
//前面的值实参与形参可以实现一一对应的效果，多出来的值如果需要获取 ，可以找arguments, 因为当前方法所接收到的所有实参的值都在arguments这个类数组里面
```

---

#### arguments 参数集合

在所有的 function 里面，有一个隐藏的内置的对象 ，这个对象是**当前方法所接收到的参数集合，也就是实参的集合**，它就是**arguments**

arguments 仅仅只作用在方法的内部 ，出了方法以后就不能使用

arguments 它是一个**类数组**

**类数组**：
具备数组特性（通过索引取值，通过 length 确定长度），但不具备数组的方法的集合，Array.isArray(类数组) 得到的结果为 false

```javascript
function add(a, b){
    console.log(a);
    console.log(b);
    // 在每个方法方法的内部 ，它都有一个隐藏的内置对象 arguments，它包含了当前方法所接收到的参数
    console.log(arguments);
}
add(10,20);
```

在上面的代码里面，我们通过**add(10,20)** 这种方式来调用了方法，并向方向里面传递了两个参数。这个时候 a 代表的就是 10，b 代表的就是 20

同时，我们也可以看到在方法内部 的 arguments 对象里面，它也保存了此次传递进去的 2 个实参

**小案例**：请编写一个方法，实现多个数的相加，然后打印输出结果

```javascript
function add(){
    //arguments代表所接收到的所有实参
    //现在只需要将这些实参一个一个的加起来就可以了
    //arguments它是一个类数组，它具备数组的特性，索引取值，length代表长度
    var sum=0;
    for(var i=0;i<arguments.length;i++){
        //sum=sum+arguments[i];
        sum+=arguments[i];
    }
    console.log(sum);
}

add(40,34);
```

---

#### 方法的返回值

一个方法经过调用执行完毕以后，它可以通过关键字 return 向外部返回一个值，这个值，我们可以通过变量把它接收到

```javascript
function eat(){
    console.log('我在吃饭');
}

function buy(){
    console.log('我在超市');
    console.log('寻找商品');
    return "糖果";
}

var a = eat();
var b = buy();
console.log(a, b); // undefined "糖果"
// 调用eat的时候，方法没有返回值，所以a得到的是 undefined
// 调用buy的时候，return了一个“糖果”，所以b接受到的值就是“糖果”
```

##### 所有的方法都有返回值

1. JS 无需指定函数的返回值，因为 JS 可以在函数内部的任何地方返回任何类型的值
2. 如果 JS 没有通过 return 语句返回值 ，那么默认返回的就是 undefined;
```javascript
function a(){
    return 1+1;
}

function b(){

}

function c(){
    var x=1;
    return x;
    x=2;
}
var str=a();   //2

var str1=b();  //undefined;

var str2=c();  //1

//--------------------------
方法在调用的过程当中，如果我们需要接收方法的返回值（ 也就是return的值），可以使用一个变量去接收

var 变量名=方法名();
//这样整个方法调用结束以后，方法内部return出来的值就会赋值给变量名
```

##### 方法返回值的用处

1. 结束方法
```javascript
当一个方法的内部发现了return的关键字以后，那么，整个方法就直接结束了，后面的代码始终都不会执行

function buy(){
    console.log("开始买面了");
    return "热干面";     //因为看到了return关键字，所以方法直接 返回一个值以后，结束运行
    console.log("鸡蛋");     //后面的这一行代码因为在return后面，所以不会执行了
}

//-------------------------------

如果仅仅只是想结束方法，而不是去返回值 ，可以直接给一个return关键字

function m(){
    console.log("a");
    return ;   //直接return 结束代码
    console.log("b");
}
```

2. 更容易的实现模块化（低耦合）
```javascript
//取arr最大值
function getMax(arr){
    var max=arr[0];
    for(var i=0;i<arr.length;i++){
        if(max<=arr[i]){
            max=arr[i];
        }
    }
    //现在max就是我们的最大值
    //我一定要告诉外边的人，你要我求的最大值是多少
    return max;
}
//排序
function sort(arr){
    var newArr=[];   //新建一个新的数组，用这个新的数组保存排序以后的结果
    while(arr.length!=0){
        var max = getMax(arr);   //求arr数组里面最大的值
        //在新的数组里面添加
        newArr.push(max);
        arr.splice(arr.indexOf(max),1); // 把当前最大值在arr里面删除
    }
    return newArr;
}

var arr1=[1,5,7,9,3,2,4,0,6];
var resultArr=sort(arr1);
console.log('resultArr', resultArr); // 9-0
```

**代码分析：**

本题在这里可以把它分为两个部分，第一部分是求当前数组里面最大的一个值，第二个部分就是把得到的这个最大值重新放到一个新的数组里面去，这每个方法只做一件事情就 OK 了

---

#### 方法的调用者与方法的引用

##### 方法的调用控制

```javascript
如果在某一段程序在调用方法的过程当中，我们希望某一个方法a只能被某另一个方法b调用，怎么办

function a(){
    console.log("我是方法a");
}
function b(){
    console.log("我是方法b");
}
function c(){
   console.log("我是c方法")
}
a();
b();
c();

//---------------------------

在上面，我们定义了两个方法，在定义的两个方法里面，我们a和b是同时存在，我们可以在任何地方调用a，我也可以在任何地方调用b

a();
b();

//----------------------------
```

但是，怎么样让 a 方法只能被 b 方法调用呢，而不能被 c 调用呢?

1. 通过作用域的方式来实现
```javascript
方法的花括号会形成一个作用域 ，定义在方法里面的东西，不能被外部使用，所以我们可以把上面的代码做一些小小的改变

function b(){
    console.log("我是方法b");

    //现在，我把a方法定义在了方法b里面
    function a(){
        console.log("我是方法a");
	}
    a();  //在这里可以调用，因为a定义在了方法b里面
}

function c(){
    console.log("我是c方法")
}

//-------------
代码分析：
当我们把方法a定义到了方法b以后，因为b是一个封闭的作用域 ，所以外边的任何东西都访问不到a,只有b能够访问到
```

2. 通过方法内部属性 caller 来判断
```javascript
在方法的内部除了一个arguments的隐藏对象以外，还有一个属性caller也是方法内部的隐藏属性

通过caller这个属性，我们可以判断出是谁调用了这个方法

如果是全局调用，那么这个caller就是空值null

function a(){
   if (a.caller!=b){
       return;    //如果当前方法不是b在调用，直接结束方法
   }
   console.log("我是方法a");
}

function b(){
   console.log("我是方法b");
   a();
}

function c(){
   console.log("我是c方法")
   a();
}
```

##### 方法的引用

在方法的内部的隐藏对象里面，有一个属性叫 callee，这一个属性指向了当前的方法

```javascript
function a(){
    console.log('hello');
    //本意是指当前方法参数的集合
    console.log(arguments.callee===a);
}

//--------------
代码分析：
在上面的代码里面，callee指向了当前的方法，当前的方法是a，所以callee就是a
```

---

#### 方法的重载

什么是重载：在编程语言里面，方法名相同，但是方法的参数类型或个数不相同，这个时候，同名的方法都会同时存在，这个情况，我们叫方法的重载 。

下面是 java 代码：

```java
class Demo{
   //第一个方法
   public void add(int a,int b){
     	 System.out.println("我是第一次出现");
   }
   //第二个方法
   public void add(int a,int b,int c){
       System.out.println("我是第二次出现");
   }
   //第三个方法
   public void add(String a,int b){
       System.out.println("我是第三次出现");
   }
   add(1,2);   //相当于调用了第一个方法
   add(1,2,3);  //相当于调用了第二个方法
   add("hello",1);  //相当于调用了第三个方法
}
```

在上面的一段 java 代码里面，我们可以看到三个同名的方法，它们的方法名相同

第一个方法与第二个方法的参数类型相同(都是 int 类型),但是它们的个数不相同

第一个方法与第三个方法的参数个数相同，但是它们的类型不相同(一个是 int,一个是 String)类型

针对上面的情况，在 Java 里面是允许，这样它们会构成一个东西叫**方法的重载**

---

#### JS 方法没有重载

当在 JS 里面出现了重名的方法以后，我们如何处理

```javascript
/*
    1.方法名相同
    2.参数个数不相同
*/

function one(num) {
	return num + 100;
}
function one(num) {
	return num + 200;
}
var result = one(200);
console.log("result", result);

/**************/
function add(a, b) {
	console.log("我是第一次");
}
function add(a, b, c) {
	console.log("我是第二次");
}
add(1, 2);
add(1, 2, 3);
```

因为 JS 的方法没有重载，所以它不可能像其它的编程语言那样，同名的方法同时存在，这个时候，后面的同名方法肯定会赋盖掉之前的方法，所以这个时候，当我们去掉用 add 的方法的时候，其实就是以后最一次定义的 add 方法为主

---

#### 为什么 JS 没有重载

重载是根据**参数的类型**与**参数的个数来**区别出重名的方法的

- 它不能确定参数类型

  重载是根据参数的类型与参数的个数来区别出重名的方法的，但是因为 JS 在这里是一个弱类型语言，它所有的变量定义都使用 var,它并不能决定变量的类型，它的类型是由它具体的值来决定的

- 它不能确定参数的个数

  我们在定义方法的时候，实参与形参是不需要实现一一对应关系 ，这样我们也确定不了参数的个数

  现在我们既不能确定参数的类型 ，也不能确定参数的个数，所以在 JS 里面的方法是没有重载的，正是因为没有重载，所以当出现同名的方法的时候，后面的方法会覆盖掉之前的方法

---

#### 递归

方法内部如果又调用了当前方法，这样就形成了一个递归

递归的本质可以把它理解成我们之前的循环，所以如果递归没有处理好（没有判断条件），也很容易形成死循环

**案例 1：请输出 0~9 之间的每一个数**

```javascript
for(var i=0;i<10;i++){
    console.log(i);
}
//-------上面是for循环写法------------

var i=0;
function sum(){
    console.log(i);
    i++;
    if(i<10){
        sum();
    }
}
sum();
```

**案例 2：求 1~150 之间偶数的和，不允许使用循环**

```javascript
var sum2 = 0;
var i = 0;
function sumA(){
    sum2+=i; // sum2=sum2+i;
    i+=2;
    if(i<=150){
        sumA();
    }
}
sumA();
console.log(sum2);

//练习：求5的阶乘
 function fn(num){
     if(num<=1) return 1;
     return num * fn(num-1);
 }
 console.log(fn(5));

 num =5 => fn(5) = return 5 * fn(4) = 5 * 4 * 3* 2 * 1 = 5*4*3*2*1
 num =4 => fn(4) = return 4 * fn(3) = 4*3*2*1
 num =3 => fn(3) = return 3 * fn(2) = 3*2*1
 num =2 => fn(2) = return 2 * fn(1) = 2*1
 num =1 => fn(1) = return 1

```

---

#### 匿名函数

匿名函数也可以匿名方法，从名词上面理解就是这个方法没有名字

> 方法如果有了名子以后，我们可以通过方法名去调用执行这个方法，如果没有名子，我们将无法调用

##### a.第一种情况

```javascript
var sayHello = function(){
    console.log('大家好');
}
sayHello();

//---------------------

(function(){
    console.log('大家好');
})()

// 像上面的函数，它没有名字，同时也立即执行了
```

##### b.第二种情况

```javascript
+ function sayHello() {
     console.log('大家好');
 }();

 //------------------

 + function(){
    console.log('大家好');
}()

// 上面的立即执行函数它也没有名字
```

##### 匿名函数的参数

```javascript
(function(a,b){
    console.log(a+b);
})(1,3);

+function(a,b){
    console.log(a+b)
}(1,3);
```

---

#### 回调函数

**一个函数被作为参数传递给另一个函数（在这里我们把另一个函数叫做“otherFunction”），回调函数在 otherFunction 中被调用。**

```javascript
b(a);

function b(callback){
    var names = '天天';
    callback(names)//这个就是回调函数 a(name);
    console.log('我很好');
}

function a(name){
  console.log(name + '，你还好吗？');
}

// 上面的代码，有两个方法，a和b，我们执行了b方法，并把a当做参数传给了b，那么这个时候a就是回调函数

```
