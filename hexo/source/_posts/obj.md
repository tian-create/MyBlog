---
title: JavaScript - 面向对象
tags: 面向对象编程
categories: javascript
---

## 面向对象程序设计

在程序员眼中，在日常的工作与生活当中，那些能够看得见，摸得着，想象得出来的，就都是对象。只要是物体它就是一个对象。

如果它是一个对象，那么它必然会具备以下几个特点

1. 对象具备属性

   属性是用于描述对象的特征的

2. 对象具备方法

   这些方法可以提供给我们去调用

3. 对象应该可以继承

   父级对象的某些方法与属性可以在子级对象里面去继承
   ```javascript
   //请同学们将班上学生的信息记录下来
   var userName = "张三";
   var age = 18;
   var sex = "男";
   //-----------上面的三个变量都是属于张三的--------------------
   var userName1 = "李四";
   var age1 = 19;
   var sex1 = "男";
   //----------上面的三个变量又同于是属于李四-----------------
   ```

如果没有对象，那么上面的东西就很难实现归类，并且对数据的管理会非常麻烦，我们迫切需要一个集中式的数据管理方法
<!-- more-->
---

### 对象的创建

对象的创建过程 ，我也可以理解成对象封装过程

#### 使用键值对创建

他用键值对来创建对象，是 JS 里面最简单一种对象创建方式，它的语法格式如下

```javascript
var 对象名 = {
	属性名1: 属性值1,
	属性名2: 属性值2,
};
```

> 在上面的创建方式里面， 我们为什么叫键值对创建呢？
>
> 通常情况下，我们会把对象的属性名叫"键(key)",把对象的属性值叫"值(value)"

我们试着用对象的形式去解决刚刚数据不能集中化管理的问题

```javascript
var stu1 = {
	userName: "张三",
	age: 18,
	sex: "男",
};

var stu2 = {
	userName: "李四",
	age: 19,
	sex: "男",
};
```

> 在上面的代码里面，我们可以看到定义了两个变量分别就 stu1 与 stu2，在每个变量里面，我们又给它定义了三个属性分别是 userName,age,sex，这三个东西都是用于描述当前 stu1 或 stu2 这个变量的相当特征

对象除了具备属性以外，它还应该具备方法，所以怎么样在对象当中去创建方法呢

_在变量里面，我们变量的数据类型不由前面的 var 来决定，而通过后面赋的值来决定，这句话我同样要应用到对象 的属性上面_

```javascript
var stu = {
	userName: "张三",
	age: 18,
	sex: "男",
	//把后面的方法赋值给前面的sayHello属性
	sayHello: function () {
		console.log("大家好啊，我是一个对象");
	},
};
```

通过上面的案例，我们可以看到，对象里面即有属性，也有方法，这个 sayHello 它就是我们的方法

我如果现在希望这个方法里面打印一句放在，“我叫 userName,我的性别是 sex,我的年龄是 age”(userName,sex,与 age 要换成当前具体的值)

**第一个版本**

```javascript
var stu = {
	userName: "张三",
	age: 18,
	sex: "男",
	sayHello: function () {
		console.log(
			"大家好，我叫" +
				stu.userName +
				",我的性别是" +
				stu.sex +
				",我的年龄是" +
				stu.age
		);
	},
};
```

> 在上面的代码当中，我们已经实现了最基本的要求，但是有没有什么需要注意的地方呢
>
> 如果用户把对象名 stu 换成了 stu1，会有什么结果

当我们把 stu 这个对象名换成 stu1 以后，后面方法 sayHello 里面所有使用了 stu 的地方都需要进行改变。如果我们更改了变量名（对象名）以后，后面所有使用了对象名的地方全部都要同步的进行改变，这个时候，怎么办呢？

**第二个版本**

```javascript
var stu = {
	userName: "张三",
	age: 18,
	sex: "男",
	sayHello: function () {
		//我们在这里无非就是要取到【当前对象】下对面的userName等属性
		console.log(
			"大家好，我叫" +
				this.userName +
				",我的性别是" +
				this.sex +
				",我的年龄是" +
				this.age
		);
	},
};
```

> 在上面的代码当中，我们使用了**this**关键字，在这个对象的花括号时面，这个关键字在这里它指向了**当前的这一个对象**
>
> 这个时候，你无论怎么去改变变量名，这个 this 都指向当前这个对象

this 可以看成是一个指针，它指向了谁就是谁，而在上面的代码里面，this 指向了当前对象，所以上面的代码当中的 this 指代的就是当前对象

_this 它可以看成指针，那么它就可以指向任何地方，所以 this 的值它是不固定的_

#### 对象属性的调用

1.  通过`.`点调用
    `对象名.属性名`这种方式来调用对象里面的属性以获取属性值或调用方法，例如`stu.sex`
```javascript
stu.userName;
stu.sex;
```
这种方式是一种最常见的调用方式，请各位同学注意，它有一个弊端，**如果一个属性是数字或以数字开头的**，那么则不能使用点来调用
```
var stu={
    0:'我是第一个',
    1:'我是第二个',
    2:'我是第三个'
}
stu.0 //不可以
```

2.  使用中括号去调用索引
    `对象名[属性名]`这种方式去获取属性里面的值，如`stu["userName"]`
```javascript
stu["userName"];
stu["sex"];

// 这一种方式的调用没有限制，它可以调普通属性，也可以调以数字开头或纯数字的属性
var stu = {
	0: "我是第一个",
	1: "我是第二个",
	2: "我是第三个",
};
stu[0]; // 我是第一个
```

#### 对象方法的调用

对象属性的调用与方法的调用保持一致，只需要在后面添加一个小括号就可以了

```javascript
var stu = {
	0: "我是第一个",
	1: "我是第二个",
	2: "我是第三个",
	sayHello: function () {
		console.log("哈哈哈");
	},
};
// 这两种都可以
stu.sayHello();
stu["sayHello"]();
```

---

### 使用 Object 来创建对象

> Object 是所有对象的祖宗，所有的对象都是由 Object 衍生下来的

#### 直接使用 Object 来创建对象

在 JavaScript 的内部，有一个内置的对象叫 Object,它主要的作用都是用来创建对象的

```javascript
var arr = new Array();
var arr = [];
```

上面的方法是创建数组，现在看下面的代码

```javascript
var obj = new Object(); //创建了一个空对象
var obj = {}; //这也创建了一下对象
```

在上面的两段代码里面，我们看到了`new`关键字，<u>new 的本意是指调用当前方法的构造方法去创建一个对象，Object 的构造方法是创建一个空的对象，而 Array 的构造方法就是创建一个空的数组，构造方法执行以后最终返回的都是一个对象</u>

所以上一个方法定义的对象我们可以使用 Object 重新来一次

```javascript
//------------------------------------这是之前的方式--------------------------------
var stu = {
	userName: "张三",
	age: 18,
	sex: "男",
	sayHello: function () {
		//我们在这里无非就是要取到【当前对象】下对面的userName等属性
		console.log(
			"大家好，我叫" +
				this.userName +
				",我的性别是" +
				this.sex +
				",我的年龄是" +
				this.age
		);
	},
};

//------------------------------------这是现在的方式--------------------------------
var stu1 = new Object(); // 创建了一个空对象
stu1.userName = "张三";
stu1.age = 18;
stu1.sex = "男";
stu1.sayHello = function () {
	console.log(
		"大家好，我叫" +
			this.userName +
			",我的性别是" +
			this.sex +
			",我的年龄是" +
			this.age
	);
};

stu1.sayHello(); // 调用stu1的sayHello() 方法

// 这个里面的this也指向你当前跟着的这个属性的对象stu1
```

#### 使用 Object 定义对象的特殊属性

在使用`{}` 或`Object`创建对象的时候，我们可以直接添加属性，也可以在后边追加属性，但是这些属性都是最基本的，它没有相关的配置信息（特性），如果想定义这些属性的详细情况，那么则必须要使用更高级别的方式来定义对象的属性了

##### 数据属性

```javascript
var stu1 = new Object();
stu1.sex = "男"; //定义了一个普通的属性sex
//如果我想定义一个学号sid,它不可更改，默认就为H19040001

//defineProperty定义属性，定义哪一个对象的哪一个属性
//数据属性有4个特性，它们又是一个整体对象
Object.defineProperty(stu1, "sid", {
	value: "H19040001", //代表当前属性的默认值
	writable: false, //是否可以写  是否可以更改
	configurable: false, //当前这个属性是否可以被delete
	enumerable: false, //代表当前属性是否可以被遍历
});

console.log(stu1.sid); // H19040001
stu1.id = 2222;
console.log(stu1.sid); // ?
```

- value：代表属性的默认值
- writable：代表当前属性值是否可以修改
- configurable：代表当前属性是否可以被 delete 删除
- enumerable：代表当前属性是否可以被 for...in 去遍历

上面的四个东西，我们叫做数据属性当中的四个特性

##### 访问器属性

所谓的访问器属性其实就是两个方法，分别是 get()与 set()方法，get 代表取值方法，set 代表赋值方法，这两个方法分别是在对属性进行取值与赋值的时候自动调用

```javascript
var stu2 = new Object();
stu2.firstName = "李";
stu2.lastName = "天";

Object.defineProperty(stu2, "userName", {
	get: function () {
		console.log("我自己在执行取值");
		return this.firstName + this.lastName;
	},

	set: function (v) {
		console.log("我在执行赋值操作" + v);
		this.firstName = v;
	},
});
console.log(stu2.userName); // get
stu2.userName = "小"; // set
console.log(stu2.userName);
```

> 1. get 方法是用于取值操作的，而 set 方法在这里是用于赋值操作，它们在操作的过程当中，这两个方法会自动执行,如果没有 get 方法说明这个方法不能取值（即使取到了，它了是 undefined）, 如果没有 set 方法，那么它就不能赋值
> 2. 访问器属性本身不存储任何值（也不能够进行任何值的存储）

下面请看以下个案例 （ 用于根据年龄来判断字是否成年与未成年 ）

```javascript
var stu3 = new Object();
stu3.age = 16;
Object.defineProperty(stu3, "isAge", {
	// 一个人是否成年通过年龄来判断
	get: function () {
		// 当我们对这个属性取值的时候
		if (this.age >= 18) {
			return "成年";
		} else if (this.age < 18 && this.age > 0) {
			return "未成年";
		} else {
			return "未出生";
		}
	},
});
console.log(stu3.isAge);
//判断一个人是否成年应该是通过年龄来决定，不能够说我直接成年了或未成年
```

当我们通过 Object 去定义数据属性与访问器属性的时候都需要经过`Object.defineProperty`来进行，但是，如果我们要同时定义多个属性的时候，怎么办呢？

##### 通过 Object 定义多个特殊属性

```javascript
var stu1 = new Object();
stu1.age = 18;
Object.defineProperty(stu1, "sid", {
	value: "H19040001",
	writable: false,
});
Object.defineProperty(stu1, "sex", {
	value: "男",
	writable: false,
});
```

在上面的代码里面，我们可以看到我通过 `Object.defineProperty`定义了`sex`与`sid`这两个属性,我们现在已经感觉到它非常麻烦 ，每定义一次都要去调用方法。现在它有一个方法与它非常相似

现在通过这个新的属性以后，我们把上面可以写成如下的方式

```javascript
//同时定义多个特性属性
Object.defineProperties(stu1, {
	sid: {
		value: "H19040001",
		writable: false,
	},
	sex: {
		value: "男",
		writable: false,
	},
});
```

**总结**：

单个定义数据属性的语法

```javascript
Object.defineProperty(对象, 属性名, {
	configurable: true, //是否可删
	writable: true, //是否可写
	enumerable: true, //是否可遍历
	value: "", //默认值
});
```

同时定义多个数据属性

```javascript
Object.defineProperties(对象, {
	属性名1: {
		//四个特性
	},
	属性名2: {
		//四个特性
	},
});
```

定义访问器属性

```javascript
Object.defineProperty(对象, "属性名", {
	get: function () {
		//此处代表取值，返回一个有效值
		return "";
	},
	set: function (v) {
		//此处的参数v是一个形参，你赋值的时候是什么值，它就是什么值
	},
	//它不能够定义value与writable,一定要记得，访问器属性不包含任何值
});
```

同时定义多个访问器属性

```javascript
Object.defineProperties(对象,{
    属性名1：{
        get:function(){
			return ""
        },
        set:function(v){

        }
	},
    属性名2：{
        get:function(){
			return ""
        },
        set:function(v){

        }
	}
})
```

#### 获取对象属性的特性

> 用来描述对象属性特征的我们叫特性

我们可以通过 Object 对象里面的一个内置方法`Object.getOwnPropertyDescriptor`

```javascript
var stu1 = new Object();
Object.defineProperty(stu1, "id", {
	value: 1111,
	writable: true,
	configurable: false,
	enumerable: false,
});

var o = Object.getOwnPropertyDescriptor(stu1, "id");
console.log("o", o);

var stu2 = new Object();
Object.defineProperty(stu2, "userName", {
	get: function () {
		console.log("我自己在执行取值");
		return this.firstName + this.lastName;
	},

	set: function (v) {
		console.log("我在执行赋值操作" + v);
		this.firstName = v;
	},
});

var o1 = Object.getOwnPropertyDescriptor(stu2, "userName");
console.log("o1", o1);
```
**应用点**：主要用于检测某一个对象某一些属性里面的特性，例如这个属性是否可以遍历，是否可以删除等相关信息

---

### 工厂模式创建对象

思考：如果现在我们希望将 10 个人的信息保存下来，每个人在这里都有姓名，性别，年龄三个属性，这怎么办呢

```javascript
var stu1={
    userName:"学生1",
    sex:"男",
    age:18
};
var stu2={
    userName:"学生2",
    sex:"男",
    age:19
};
var stu3={
    userName:"学生3",
    sex:"男",
    age:22
};
...
```

单例模式解决了分组的问题，让每个对象有了自己独立的命名空间，但是不能批量生产，每一个新的对象都要重新写一份一模一样的代码。

我们之前在学习方法的时候，已经知道方法是可以任意多次的调用执行，我调用一次，就执行一次，那么，现在我如果希望得到 5 个对象，我可以调用 5 次，所以针对这个思路 ，我们可以把代码写成如下情况

```javascript
function createStudent(userName, sex, age) {
	//var obj = new Object();
	var obj = {
		userName: userName,
		sex: sex,
		age: age,
	};
	return obj;
}

function createPerson(name, age) {
	var obj = {
		name: name,
		age: age,
	};
}

var s1 = createStudent("天天", "女", 18);
var s2 = createStudent("学生2", "男", 19);
console.log(s1, s2);
```

通过上面的方式 ，我们可以快速的创建两个对象，这样就可以很方便的使用对象将班上学生的信息统一集中管理，这种设计模式，我们叫工厂模式

即：把实现同一事情的相同代码，放到一个函数中，以后如果再想实现这个功能，就不需要重新编写这些代码了，只要执行当前的函数即可， 这就是函数的封装，体现了高内聚、低耦合的思想：减少页面的中的冗余代码，提高代码的重复利用率。

缺点： 工厂模式无法实别对象类型（即怎样知道一个对象的类型）

---

### 使用构造函数创建对象

构造函数其实也是一个普通的函数，只是它的调用方法不一样而已，它需要通过关键字`new`去调用

当一个函数通过 new 去调用执行以后，它会返回一个对象类型给我们

```javascript
function Person() {
	console.log("我去执行了");
}
Person(); //常规方式调用
var a = new Person(); //new关键字调用，返回一个对象赋值给了a
```

> new 一个 function 会得到一个对象

#### 什么是构造函数

构造函数就是一个普通函数，当这个函数如果**常规调用**的方式或 call/apply 的调用方式去执行的时候，我们就把它当成是普通函数

但是如果我们通过 new 去调用，那么我们就把这个函数当在是**构造函数**（函数还是那个函数，只是根据调用方式不同我们来叫不同的名字）

#### 构造函数的执行过程

当一个函数创建好以后，我们并不知道它是不是构造函数，即使像上面的例子一样，函数名为大写，我们也不能确定。只有当一个函数以 `new` 关键字来调用的时候，我们才能说它是一个构造函数。

执行的过程，也就是 new 关键字来调用的情况。

```jsx
function Person(name, sex) {
	this.name = name;
	this.sex = sex;
}

var p1 = new Person("张三", "男");
p1.name = "张三";
```

此时执行过程为：

1. 当以 new 关键字调用时，会创建一个新的内存空间，标记为 Person 的实例。

   例如：创建新的内存空间：#f1，标记为 Person 的实例

2. 函数体内部的 this 指向该内存，也就是 Person 的实例。

   ```csharp
   // 通过以上两步，我们就可以得出这样的结论。
   var p2 = new Person('刘红', '女');  // 创建一个新的内存 #f2
   var p3 = new Person('杜金雪', '女');  // 创建一个新的内存 #f3
   /*
   	每当创建一个实例的时候，就会创建一个新的内存空间(#f2, #f3)，创建 #f2 的时候，函数体内部的 this 指向 #f2, 创建 #f3 的时候，函数体内部的 this 指向 #f3。
   */
   ```

3. 执行函数体内的代码，给 this 添加属性，就相当于给实例添加属性。

4. 默认返回 this。

   由于函数体内部的 this 指向新创建的内存空间，默认返回 this，就相当于默认返回了该内存空间#f1。此时，内存空间被变量 p1 所接收。也就是说 p1 这个变量，保存的内存空间就是#f1，同时被标记为 Person 实例。

#### 构造函数的返回值

构造函数执行过程的最后一步是默认返回 `this` 。言外之意，构造函数的返回值还有其它情况。

1. **没有手动添加返回值，默认返回 `this` 。**
   ```jsx
   function Person1() {
   	this.name = "张三";
   }

   var p1 = new Person1();

   /*
   	首先，当用 new 关键字调用时，产生一个新的内存空间 #f11，并标记为 Person1 的实例；
   	接着，函数体内部的 this 指向该内存空间 #f11；
   	执行函数体内部的代码；
   	由于函数体内部的 this 指向该内存空间，而该内存空间又被变量 p1 所接收，所以 p1 中就会有一个 name 属性，属性值为 '张三'。
   */
   ```

2. **手动添加一个基本数据类型的返回值，最终还是返回 `this`。**
   ```javascript
   function Person2() {
   	this.age = 28;
   	return 50;
   }

   var p2 = new Person2();
   console.log(p2.age); // 28
   ```

3. **手动添加一个复杂数据类型(对象)的返回值，最终返回该对象** 。
```javascript
function Person3() {
	this.height = "180";
	return ["a", "b", "c"];
}

var p3 = new Person3();
console.log(p3.height); // undefined
console.log(p3.length); // 3
console.log(p3[0]); // 'a'

// 再来一个例子
function Person4() {
	this.gender = "男";
	return { gender: "中性" };
}

var p4 = new Person4();
console.log(p4.gender); // '中性'
```

#### 构造函数与普通函数的区别

1. 返回值不一样

   普通的函数（常规调用的函数）它可以返回一个具体的值，即使我们没有明确的指定 `return`，它也会返回一个`undefined`

   构造函数一般情况下不指定返回类型，它会自动返回一个新建的对象

   ```javascript
   function Person() {
   	console.log("我去执行了");
   }
   Person();
   console.log(Person()); // undefined
   var a = new Person();
   console.log(a); // Person {}
   ```

2. this 的指针发生了偏移

   当这个方法做为普通方法去执行的时候，它内部的 this 指向了`window`全局对象

   当这个方法被当成构造方法`new`去执行时候，它内部的`this`指向了当前对象，正是因为有了一个像这样的特点，所以，我们会大量使用这种方式去创建对象

3. 调用的时候是否要加括号

   普通方法是需要通过方法名 ()来进行调用的

   当这个方法被当成构造函数去执行的时候，如果没有参数，这个括号是可以省略
    ```javascript
    function Person(){
        console.log(this);
    }
    Person();  //常规调用
    var a=new Person;   //我没有参数，所以，我可以把括号省略掉
    ```

     同理，下面的代码也是正确的

    ```javascript
    var arr=new Array;
    var obj=new Object;
    ```



    #### 构造函数生成对象

     我们已经知道一个构造函数通过new去执行的时候，内部的this指向当前对象（返回给用户的那个对象），所以我们可以根据这个特点来创建对象

     **案例**：如果假设我们希望所班上所有学生的姓名，性别，年龄封装成对象存储起来

```javascript
function Student(userName, sex, age){
    //我现在要在当前对象上面添加 userName，sex,age三个属性
    //而构造函数在new的时候，this指向了当前对象
    this.userName = userName;
    this.sex=sex;
    this.age=age;
}
var stu1 = new Student("张三","男",18);
var stu2 = new Student("李四","男",22);
var stu3 = new Student("小红","女",26);

1. 新建内存空间，标记为student的实例
2. this指向内存空间（student的实例）
3. 执行函数体内的代码，把属性或者方法添加到this，添加到内存空间（student实例）上去
4. （默认）返回this，也就是返回内存空间（student的实例）,用一个变量来接收这个返回值（this/内存空间），所以变量上就能拥有返回值上的所有属性和方法。

```

```javascript
function Student(name, sex, age, grade) {
	this.name = name;
	this.sex = sex;
	this.age = age;
	this.grade = grade;
	this.fn = function () {
		if (this.grade >= 60) {
			console.log(this.name, this.sex, "及格");
		} else {
			console.log(this.name, this.sex, "不及格");
		}
	};
}

var s1 = new Student("litian", "女", 21, 80);

// 现在我们已经可以得到这三个对象，并且对象里面的属性各不相同，根是根据参数的不同来决定它的属性值的
```

---

### 构造函数创建对象的识别

为什么说构造函数解决了工厂模式无法实别对象的问题

```javascript
function createStudent(userName, sex, age) {
	//var obj = new Object();
	var obj = {
		userName: userName,
		sex: sex,
		age: age,
	};
	return obj;
}

function createPerson(name, age) {
	var obj = {
		name: name,
		age: age,
	};
}
```

在上面的代码里面，我们会看到无论调用`createStudent`还是去调用`createPerson`在这里它的内部都是通过`new Object()`来实现，它们既然都是 Object 来创建的，那么在根本上面就无法实别它们到底是什么类型

```javascript
//学生的构造函数
function Student(name, sex, age) {
	this.name = name;
	this.sex = sex;
	this.age = age;
}

//定义了老师的构造函数
function Teacher(name, sex) {
	this.name = name;
	this.sex = sex;
}

var s1 = new Student("张三", "男", 18);
var s2 = new Student("李四", "男", 19);

var t1 = new Teacher("天天", "女");

// 按照正常的理解，s1与s2应该是属于学生对象，而t1则属于老师对象
s1 instanceof Student; //true;
s2 instanceof Student; //true;
s1 instanceof Teacher; //false;

t1 instanceof Teacher; //true;
t1 instanceof Student; //false
//通过上面的方法，我们可以实现对象的实别
```

上面的方式已经可以实别出对象类型了，但是仍然要记得一点，在 JS 里面，所有的对象都是由 Object 衍生出来，所以会出现以下的情况 ：

1. 在以前的时候，我们理解`instanceof`是 ，`s1`是否是由`Student`这个方法`new`出来
   现在理解为`Student`方法是否衍生出了`s1`这个对象
```javascript
s1 instanceof Object; //true
s2 instanceof Object; //true

t1 instanceof Object; //true
//因为所有对象的祖宗都是Object
```

2.  在每个对象里面都有一个属性`constructor`，这个属性它是指构造函数，指向了当前创建这个对象的构造函数，所以 s1 与 s2 对象它们的`constructor`都指向了 Student 这个构造函数，而 t1 的`constructor`则指向了 Teacher 这个构造函数
```javascript
s1.constructor === Student; //true;
s1.constructor === Object; //false
s1 instanceof Object; //true

// 通过上面的第二行代码与第三行代码，我们可以得出`constructor`的检测比`instanceof`的检测更为严格
```
