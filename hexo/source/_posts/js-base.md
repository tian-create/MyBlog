---
title: JavaScript - 基础语法
tags: js基础语法
categories: javascript
---
## 基本语法
1. JavaScript是区分大小写的（HTML和CSS不区分大小写）
2. JavaScript必须写在<==script==>标签里面，并且制定正确的类型（type）
```html
<script type="text/javascript"></script>
```
<!--more-->
3. JavaScript如果语法出现了错误，那么会在页面上的控制台（console）报错
4. JavaScript里面，一句代码写完了以后，请加上分号结束 “ ; ” ，不加理论上市可以的，但是不推荐

---
#### 标识符
用来标明某一些对象或事物的特征，主要应用于**关键字**与**变量名**

> 标识符一般是指变量名，方法名，关键字或保留字

> 变量名相当于人的姓名，它可以变，关键字则是系统自己使用的

> if,else,for,while等这些都是系统关键字，而我们用户在写代码的过程当中，自己取得名字我们叫变量名

**注意：**
1. 标识符的开头必须是字母、_下划线、$开头，不能以数字开头，后面的则没有要求，可以使用任何字符
    - 一般我们建议把 - 换成 _ 下划线
    - 不要使用中文做变量名，如：
```js
性别 = '男';
年龄 = 25;
```
2. 标识符应该遵循**见名知意**的原则，JavaScript默认以**驼峰命名**为原则：
```js
userName = 'tiantian'; // 账号
userNickName = '天天'; // 昵称
passWord = '123456'; // 密码
```
> **说明**：上面的代码就很好的说明了驼峰命名的原则 ，首字母小写，后面的每个英文单词字母大写
以下情况请注意：
```js
// 如果在定义的时候，我们的标识符是一个单词，那么首字母大写
Add(),List(),Edit(),Query(),Insert(),addUserInfo(),getUserList()

var liuserAge = 18;
// l: local 局部的
// i: int 整数
// userAge: 变量名

var _gstrPwd = '123456';
// _代表临时变量
// g: global 全局的
// str: 字符串string
// pwd：密码
```
3. 不能以**关键字**或**保留字**为标识符
最常见的关键字，我们现在只学到了 **==var==** 定义变量

我们不能以关键字做变量名，如 var，do，while等，也不能以保留字作标识符，如 const，'import'等(参考ECMA-262)

---
#### 变量标识符
什么是变量：变量就是在描述事情特征（属性）当中，可以变化的数据，我们叫做变量
> 使用关键字 var 来定义的标识符，我们叫变量标识符，变量标识符用于存放一定的数据在代码当中
```js
var userName = '天天';
```
语法格式如下：
```js
var 变量名1 = 变量值1;
var 变量名2 = 变量值2；
```
> **说明：** 在上面的代码中，var 是定义变量的**关键字**，userName 是变量标识符（变量名），“天天”则是这个变量标识符的值（变量值）；
> 所有的变量都是像上面定义的，但是，有一种情况是像下面这种方式（多个变量一起定义的时候）
```js
var userName="天天";
var userAge=18;
var userSex="女";

/* 上面的代码当中，我们定义了三个变量，这是可以的 */

> 注意：在JavaScript当中，所有的语句如果写完以后要使用分号 ; 结束

还可以使用如下的语法格式：

```js
var 变量名=变量1,变量名=变量2......，变量名n=变量值n;

/* 上面这种方式就把之前的var进行了省略，然后中间使用了逗号进行隔开 */
/* 当我们定义多个变量的时候，我们就会使用这一种方式 */

var userName="天天",userSex="女",userAge=18;
var a,b=10,c;   //这个比较特殊，a,c都没有赋值，b直接赋值了
var nickName="Lucy";
var isTeacher=true;
var money=null;  //赋空值
```
> **说明**：上面的代码当中，我们在定义多个变量的时候，我们使用逗号隔开，每个变量在定义的时候可以赋值，也可以不赋值，如果赋值则使用=进行赋值

> =是赋值的意思，把=等号右边的东西赋值给左边

> 目前阶段，所有变量的定义，我们都通过 var 来进行

---
## 数据类型
当我们定义变量以后，再向变量赋值的过程当中，会存以几种情况的值，例如姓名是汉字，年龄又是数字等

汉字：一二三四五六七八九

数字：123456789

变量后面接的值的数据类型主要有以下几种

1. 字符串（String）
指的是汉字，英文等其他的字符
当定义变量赋值字符串值的时候，我们一定要加上引号 （单引号与双引号都是用来形容字符串）
加了引号了数字不是数字类型，是字符串类型
```js
var userName = '天天';
```
2. 数字（Number）
指的是0~9之间的数组成的数字（可以是整数，也可以是小数，还有负数）
```js
var userAge = 18;
```
3. 布尔类型（Boolean）
它只有两个值true/false;
```js
var flag = true;
```
4. 空值（Null）
当我们在定义一个变量的时候，我们如果不想给它赋值可以直接给一个null的空值
注意它通过typeof检测出来的结果是object
```js
var timer = null;
```
5. 未定义（Undefined）
当一个变量在定义的时候，没有赋值，那么，它就是会出现undefined
```js
var a;
console.log(a)
```
> 上面的五个数据类型是JavaScript当中的**基本数据类型**

**总结：**

变量有5种基本的数据类型，1种复杂的数据类型

---

#### JavaScript数据类型检测
在JS当中，我们有五种基本数据类型 ，后期我们还会根据这五种基本数据类型去完成**复杂的数据类型**（对象，数组【它是属于对象的一种】，方法）

在JS里在，当我们定义了一个变量标识符以后，我们这个变量就存在了，但是有时候，如果我们需要去检测一下这个变量的类型就需要使用我们的typeof去检测

---

##### typeof 关键字
这个关键字是用于检测JS当中的变量数据类型，它的语法格式如下

```js
typeof 变量名
```
> 上面的代码运行以后就会得出我们的数据类型

通过typeof我们可以检测出如下的几种数据类型
1. number 数字类型
2. string 字符串类型
3. boolean 布尔类型
4. undefined 未定义类型
5. object 对象类型（null，数组，对象，正则表达式）
6. function 方法类型

> **说明**：typeof可以检测出任何数据类型，不管是基本的数据类型，还是复杂的数据类型

> **注意**：关于对象的数据类型检测，我们后面有其它的方法进一步检测(instanceof,isArray等）

---
##### JavaScript数据类型的可变性
JS的数据类型并不是一定不变的，它的数据类型是由后面的值来决定的，你进行什么类型的赋值，这个变量就是一个什么数据类型

```js
var a=123;
typeof a;//得到的是number数据类型
a="hello world";
typeof a; //得到的是string数据类型
```
**注意**：在其它的C/Java/C++/C#等编程语言里面，数据类型是不可变的，定义变量标识符必须在变量的前面先指定变量的数型如（int,string,boolean等）,可是在JS里面，所以的变量定义都是使用var来进行的，这个时候，变量的数据类型就不由前面的关键var决定了，而是由后面的值来决定的，后面接什么值就指定了它是什么类型。

通过这一种区别，我们可以把JS语言和其它的语言做一个区分

如果在定义变量的时候，变量的类型由前面的关键字决定的，我们把这种编程语言叫**强类型编程语言**

如果变量的数据类型是由后面的值来决定的，这种编程语言我们叫**弱类型编程语言**

---
#### JavaScript 数据类型转换
##### 字符串string转数字number
1. 使用Number这个方法来进行
```js
var a = '123';
var b = Number(a);
console.log('b', b); // 123
console.log(typeof b); // number

var c = '123.45';
var d = Number(c);
console.log('d', d); // 123.45
console.log(typeof d); // number

var e = '123.45.67';
var f = Number(e);
console.log('f', f); // NaN 
console.log(typeof f); // number

var g = '项目1';
var h = Number(g);
console.log('h', h); // NaN
console.log(typeof h); // number

var i = '1号教室';
var j = Number(i);
console.log('j', j); // NaN
console.log(typeof j); // number
```
> NaN：全称 Not a Number(不是一个数字)，当一个运算经过计算本来应该得到一个Number数的时候结果报错了，就会出现NaN, typeof NaN得到的结果是"number"
**Number在进行转换的时候，必须是一个合法的数字字符串，不然就会报NaN**

2. 使用 parseInt() / parseFloat() 方法来进行转换
```js
var a = '123';
var b = parseInt(a);
console.log('b', b); // 123
console.log(typeof b); // number

var c = '123.45';
var d = parseInt(c);
var _d = parseFloat(c);
console.log('d', d); // 123
console.log('_d', _d); // 123.45
console.log(typeof d); // number

var e = '123.45.67';
var f = parseInt(e);
var _f = parseFloat(e);
console.log('f', f); // 123
console.log('_f', _f); // 123.45 
console.log(typeof f); // number

var g = '项目1';
var h = parseInt(g);
console.log('h', h); // NaN
console.log(typeof h); // number

var i = '1号教室';
var j = parseInt(i);
console.log('j', j); // i
console.log(typeof j); // number
```
> parseInt是直接去掉小数，不做四舍五入的处理
> parseInt或parseFloat只要前面是字符串的数字，都可以尝试去转，转换到非数字的地方就结束

---
##### 其它类型转字符串（string）类型

```js
var a = 101;
```
要将上面的a转换成字符串有以下几种方法
1. 将任何类型的数据转换成字符串，有一个最简便的方法就是直接加上一个空的字符串
```js
a+"";  //结果为字符串"101"
```

2. 通过调用String方法来进行转换
```js
// 数字转字符串
var a = 101;
var b = String(a);
console.log('b', b); // 字符串 101
console.log(typeof b); // string

// null类型转字符串
var c = null;
var d = String(c);
console.log('c', c); // null
console.log(typeof c); // object

// 布尔值转字符串
var e = true;
var f = String(e);
console.log('f', f); // 字符串 true
console.log(typeof f); // string

// undefined类型转字符串
var g = undefined;
var h = String(g);
console.log('h', h); // undefined
console.log(typeof h); // string
```
这一种方式与第一种方式计算结果一样，只是方法不一样而已

3. 调用toString()方法来进行转换
```js
var a=10;
a.toString();   //结果为"10"
var b=true;    
b.toString();    //结果为字符串的“true”
var c=null;    
var d=undefined;
```

**注意**：null与undefined 没有 toString()的方法

---
##### 数字与布尔Boolean类型的转换
1. 数字的0与1转换成boolean类型
```js
var a=0;
var b=Boolean(a);   //得到布尔类型false
var c=1;
var d=Boolean(c);   //得到布尔类型true
var e=5;
var f=Boolean(e);   //得到布尔类型true
```
> 数字转Boolean的时候，如果这个数是明确的0，那么就是false,否则一律是true

2. 字符串数字的"0"与"1"转boolean类型
```js
var a="0";
var b=Boolean(a);   //得到布尔true
var c="1";			
var d=Boolean(c);   //得到布尔类型true
```
针对上面的情况，我们需要将字符串的"0"与'1'先转换成数字的0和1，再进行操作
```js
var a="0";
var _a=Number(a);   //先转换成数字0
var b=Boolean(_a);  //得到结果false

var c="1";
var _c=Number(c);	//先转在数字1
var d=Boolean(_c);  //再转换成布尔true
```

3. 布尔类型转成数字 0 或 1
```js
var a=true;
var b=Number(a);   //得到数字1

var c=false;
var d=Number(c);   //得到数字0
```

4. 字符串的"true" 与 "false"能否转换成 true/false 或 0/1
```js
var a="true";

var c="false";
```

---
#### 变量的区域性（作用域）
1. 使用 var 定义的变量**没有块级作用域**
```js
/* 没有块级作用域指的是如果用花括号{}包裹起来，形成不了作用域（function里面的花括号除外） */

/* JS里面的花括号形成不了变量的封闭环境 */

{
    var a=123;
    //var定义的变量没有块级作用域
}
console.log(a);   //这是不会报错的
```
花括号形成不了封闭环境，所以你在前面无论加上什么如我们后期的if/else/for/while等都不会形成封闭环境
但是加上function以后就会有封闭环境
```js
function m(){
    var a=123;
    //当var定义在function的花括号里面，就会有作用域了
}
console.log(a); //报错 a is not defined
```

2. script标签形成不了作用域
```js
/* 在一个页面里面，可以有多个script标签，但是它们仍然不具备封闭环境 */

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>变量区域性</title>
    <script>
        var a=101;
    </script>
</head>
<body>    
</body>
<script>
    console.log(a);
</script>
</html>
```
> 这个时候的代码不会报错，因为script形成不了封闭的环境，页面最终还是会将之个 script的代码合并在一起执行

---
#### JavaScript 中的操作符
##### 加法操作符 +
1. 数字与数字相加
```js
var a=10;
var b=15;
var c=a+b; // c = 25
```
在数值与数值相加的情况下，以下特殊情况需要单独处理
```js
var c = NaN+NaN;   //结果还是NaN
```
> NaN在五种基本数据类里面，除了String字符串以外，其它的都是NaN
在JS里面，Infinity代表了无穷大正数，-Infinity代表了无穷大的负数，当它们进行运算的时候，要特别注意
```js
var a = Infinity+Infinity;   //得到的结果仍然是无穷大
var b = 6 / 0; // 得到也是 Infinity
```

2. 字符串与数字相加
```js
// 字符串与数字相加，结果是字符串，它会把数字先转成字符串，然后连接在一起
var a = "hello"+123;  //结果"hello123"
var b = "456"+123;    //结果"456123"
```

3. 字符串与字符串相加
```js
//指的就是字符串的拼接
var a = "hello"+"world";   //结果"hello world"
var b = "你好"+"520";       //结果 "你好520"
```

4. 其他类型数据相加
```js
var a = 1+null;				//得到结果1
var b = 1+undefined;			//NaN
var c = 1+false;			//结果为1
var d = 1+true;				//结果为2
```
> 可以把false与null看成是0,undefined会报NaN,true可以看成是1
> 五种基本数据类型里面，只有string字符串与undefined相加不为NaN

##### 减法操作符 -
```js
var a = 10-1;  //9
var b = 20-false;  //20
var _b = 20-true;  //19
var c = 15-null;   //15
var d = 11-undefined;   //NaN
var f = 12-NaN;    //NaN

var g = "hello"-1;  //NaN
var f = "a"-"b";    //NaN
```

##### 乘法操作符 *
```js
var a = 10*1;  //10
var b = 20*false;  //   0
var _b = 20*true;  //  20
var c = 15*null;   //  0
var d = 11*undefined;   //NaN
var f = 12*NaN;    //NaN

var g = "hello"*1;  //NaN
var f = "a"*"b";    //NaN
```

##### 除法操作符 /
除法与乘法保持一致，唯独多了一个0的处理问题
```js
var a = 0/0;   //结果NaN
var b = 10/0   //Infinity
```

##### 取余操作符 %
一个整数操作另外一个整数的时候，取它的余数
```js
var a = 10%3;   //结果1
var b = 10%null;   //NaN
var c = 10%undefined;//NaN
var d = 10%true;	//结果为0
var e = 10%false;   //NaN
```

##### 相等操作符 ==
在JavaScript当中，我们的相等是使用等号==来进行的，如果要判断两个变量（对象）是否相等，这个时候，我们就要使用相等操作符
相等操作符与赋值操作符非常相像，都是使用等号，但是赋值操作符使用一个等号=，而相等操作符使用两个等号==
```js
var a=1;
var b=1;
a==b;  //这句话是成立的
```
**注意以下代码**
```js
var a=1,b="1",c=true;
a==b; //true
b==c; //true
a==c; //true
```
> **重点说明**：使用相等操作符去判断两个变量（对象）是否相等的时候，我们如果只有两个等号 == 去操作，这个时候，它会把两个等号 == 左右两边的值做类型转换（这个过程系统自动转换）以后再去执行判断操作

##### 严格相等操作符 ===
在JavaScript当中，当我们使用相等操作符==去操作的时候，这会自动的进行数据类型的转换，但是有时候，我们又不希望它进行数据类型转换 ，这个时候，我们就需要使用严格相等操作符 ===
```js
var a=1,b="1",c=true;
a===b; //false;
b===c; //false
```
> 普通相等 == 与严格相等 === 对比，普通相等 == 只判断变量的值是否相等，而不判断变量的类型是否相等，而 ===，即要判断值相等，也要判断类型相等

**注意：**NaN不与任何东西作比较，只要一比较就是false

> 上面的东西如果有严格相等，全都不成立 ，都是false

== 与 === 都是判断相等操作，还有一个不等的操作符 != , !== ,它跟等号反着判断就行了

##### 一元操作符
只能操作一个值的操作符，我们叫一元操 作符
```js
var a=10;
a=a+1;  
console.log(a);  //控制台会输出11
```
上面的代码如果转换成自加或自减的一元操作符以后，会变成如下代码
```js
var a=10;
a++;
console.log(a);  //这个时候控制台会输出11
```
**注意事项**：当我们在进行自加运算或自减运算的时候，我们可以把这个符号放在前面，也可以放在后面
- 如果自加运算符在后面，则代表先使用自己，使用完以后再+1
- 如果自加运算符在前面，则代表前把自己+1，然后再使用自己
```js
var a=10;
console.log(a++); // 10
console.log(a); // 11

说明：上面的代码执行完毕以后，控制台打印出来的结果是10，但是最终a的值为11
a先使用自己（这个时候的a还是10），使用完成以后（控制台打印完毕以后）自已再+1，这个时候最终的值为11
```
```js
var a=10;
console.log(++a); // 11
console.log(a); // 11

说明：上面的代码执行完毕以后，控制台打印出来的结果为11，a的最终值也为11
a在使用之前就要把自己+1（10+1=11），然后再去使用自己（控制台去打印），这个时候控制台的值为11
```
根据一元操作符的特点，我们可以演变成如下的操作
```js
var a=10;
a=a+2;   //a+=2;
a=a-5;   //a-=5;
var b=5;
a+=b;    //a=a+b;
a-=b;    //a=a-b;
a*=b;    //a=a*b;
a/=b;    //a=a/b;
```

##### 逻辑操作符
在JavaScript当中，常用的逻辑操作符有三种，“与”，“或”，“非”
1. 与的操作符是&&
2. 或的操作符是||
3. 非的操作符!

###### 计算过程
- 当运算的符号相同的时候
    - 与的操作，一假一假
    - 或的操作，一真即真
    - 非的操作，非真即假，非假即真
    - 必须遵守**短路原则**，当一个表达式的前面部分已经能够得到结果，就停止计算，返回结果，如果得不到结果，就继续计算，直到最后一个
    - 处理特殊值 NaN 或 null 与 undefined 或 "" 字符串的时候，可以把它看成是false（但本质上并不是false）   
```js
/* 逻辑运算符支持短路原则：
 (表达式1）&&(表达式2) 如果表达式1为假，则表达式2不会进行运算，即表达式2“被短路”
 (表达式1）||(表达式2) 如果表达式1为真，则表达式2不会进行运算，即表达式2“被短路” */

var a=true,b=false,c=null,d=undefined;
a||b||c;   // true
false||b||c;  //null  因为已经计算到最后一个
false||b||true||c;   //true  计算到第3步就已经结束了

//---------------------------------
a&&b&&c;    //false  
a&&c&&b;    //null
d&&c&&b;    //undefined

/* 总结：
a&& b :如果执行a后返回true，则执行b并返回b的值；如果执行a后返回false，则整个表达式返回a的值，b不执行；
a || b :如果执行a后返回true，则整个表达式返回a的值，b不执行；如果执行a后返回false，则执行b并返回b的值； */
```
- 当运算的符号不相同的时候
```js
从左往右
根据优先级来计算 !>&&>||

var a=true,b=false,c=null,d=undefined;
true||b&&c;   //true
false||c&&b;   //null
false||d&&c;   //undefined
!b||c||d&&!a   //true||c||d&&false    得到结果true
```
- 特殊情况特殊对待
我们在计算过程当中，可以把 0当成 false，把1当成true(不是真的是true/false)
```js
第一种情况

var a=true,b=false,c=null,d=undefined;
1||b&&c;     //1
0||b&&c;     //false
```
```js
第二种情况，非0或1的情况

var a=true,b=false,c=null,d=undefined;
""||b&&c;    //假设""也是false    false
""&&b&&c;    //得到 ""
""&&b||c;    //得到null
!""||b&&c;   //不要想太复杂 !""结果为true    最后结果肯定是true
!undefined||b&&c;   //true
!null||b&&c;  //true
//---------------------------------------------
"a"||b&&c;   //"a"
123||undefined;   //123   Boolean(123)得到true
null||"hello";    //hello;
```
**心得：**
> 在上面的两种情况下面，我们可以把这些值做一次Boolean转换，然后得到true或false以后再去计算（只是把这个值看成是true或false并不是真正的true或false）

> 以下内容会被当成false处理："" , false , 0 , null , undefined , NaN

##### 条件运算符
条件运算符是根据某一个条件来得出某一个结果，它有固定的书写格式
```js
var a = 判断条件?第一个值:第二个值;

/* 在上面的格式上当，如果判断条件成立，则返回第一个值，否则返回第二个值 */
```
示例：
```js
var a=10;
var b=11;
var c=a>b?12:13;
```
案例1：
```js
var a=10;
var b=11;
var c;
//要求，请将a与b作对比以后然后将其中大的一个值赋值给变量C

通过条件运算符，我们可以很好的去判断上面的问题
var c = a>b?a:b;
/* a小于b，所以c取值b */
```

案例2：
```js
var a=10,b=11,c=12;
var d;
//请将a,b,c中最大的一个值赋值给d

//-------------------
思路：首先完成第一次比较，将a与b作比较，返回a与b中大的哪一个数，我们可以定义一个变量temp，然后再拿这个temp去和C做比较（第二次对比），然后再通过条件运算符去返回其中大的一个数
var temp = a>b?a:b;
var max = temp>c?temp:c;
/* max现在就是最大的值 */

//-------------------
现在要求把上面的两行代码换成一行代码去完成
var d = a>b?(a>c?a:c):(b>c?b:c);
/* a 和 b作比较，如果 a 大，取 a 和 c 作比较；如果 b 大，取 b 和 c 作比较 */
```

案例3：
```js
var a = undefined?1:2;
// Boolean(undefined) 为false 取值2

var e = "123"?"hello":"world";
// Boolean("123") 为true 取值"hello"
```
> undefined，NaN可以得到false，所以条件不成立，而"123"不可以得到false,所以条件成立

> 把前面这里的值做一次Boolean()操作，得到true就代表成立，得到false就代表不成立

##### 关系操作符
在JavaScript当中，关系操作符包含大于（>）小于（<），大于等于(>=)，小于等 于（<=）

在强类型的编程语言里面，关系操作符只是对数字类型（Number类型）做比较，但是在JavaScript当中，它不仅仅可以对数字做对比，也可以做其它的类型做对比
1. 数字和数字对比
```js
var result = 1>2;
// 得到false
```
2. 数字和字符串对比
```js
var result = "3">2;
// 得到true
/* 说明：数字型的字符串与数字作对比，那么另一个会自动转换成我么的数字 */
```
3. 特殊数字NaN和其他做对比
```js
var result1 = NaN>3;
var result2 = NaN<=3;
/* 说明：这里结果都是false， 任何数与NaN做对比得到都是false*/
```
4. 字符串数字和数字符数字作对比
```js
var result="78">"9";  
//false 字符串9的ASCII值是57 值越小越大
/* 注意：如果对比的两边都是字符串，则需要去判断它们的字符串编码 */
```
> 字符串编码指是在计算当中，所有的数字，特殊符号，英文字母都有一个特殊的数字编码，这个编码我们叫Acsll编码

ASCII对照表：https://tool.oschina.net/commons?type=4

5. 对象与对象比较
如果这个对象有valueOf()的方法，则用valueOf()的值作对比，如果没有，则用toString()的方法做对比

**思考**：如果null，undefined,""与其它的数做对比的时候，结果如何？

```js
1>null;     //true;
1>undefined;   //false;
1>"";       //true;
null>undefined;  //false
"A"<"b";     //65<98   true
//最复杂的是中文
"我">"你";    //中文字符串对比的是unicode码
//25105 对比 20320  
```
**注意事项：**
> null==undefined，同时1>null成立，所以很多人理所当然就认为1>undefined，但结果不是

> 中文当中var a="我" a.chatCodeAt(0)得到unicode码，然后再去对比

















