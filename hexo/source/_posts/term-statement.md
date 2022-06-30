---
title: JavaScript - 条件语句
tags: js条件语句
categories: javascript
---

### 条件语句

条件语句某些其它的编程里面它也属于分支语句，它是根据一些条件来选择不同的代码去执行

条件语句在编程里面当作是 if...else...语句
<!--more-->
语法格式

```javascript
// 只做一次的条件判断
if(条件){
    // 执行代码
} else{
    // 执行
}
```

例子：

```javascript
// a是正数还是负数
var a=10;
if(a>=0){
    console.log('a是正数');
} else{
    console.log('a是负数');
}
```

> 在上面的例子里面，我们把 if...else 这种情写法当成条件语句，它是根据某一个判断条件来执行的，这个判断条件返回一个 Boolean 类型的值（这个地方的 Boolean 不一定真的是 Boolean 类型）

针对 if 后面的条件，我们看一下下面的问题

```javascript
var a=8;
// 如果a不为null，undefined，“”，我们就赋值给b，否则就给b一个默认值520
var b=a||520; // a 为true返回a，否则返回520
// Boolean(8) true 返回第一个a
```

在上面的写法里面，我们是根据的逻辑运算符来进行的（要当于这个地方的 a 也做了一次 Boolean(a)的转换）

上面的写法，可以转换成如下写法

```javascript
var a=8;
// Boolean(a); 得到true
if(a){
    var b=a;
} else{
    var b=520;
}

这一个时候的a放进去的不是一个布尔类型，但是我们可以通过Boolean去转换一次，得到Boolean类型的值，把这个值看成是它的结果
```

条件语句是代码应该根据不同的条件去进行执行，当有多个条件的时候，我们应该怎么办呢？

```javascript
if(条件1){
    //代码1
}
else if(条件2){
    //代码2
}
//.......后面还可以有很多很多
else{
    //最后条件都不成立的结果
}

if(username == ''){
	console.log('不为空')
	return false;
}
else if(tel == ''){
	console.log('不为空');
	return false;
}
else{
	// username tel都有值
	// ajax
}



条件语句可以进行多个条件的叠加
else是可以省略的
花括号可以省略，但是只是在条件语句执行的代码块里面只有一行代码的时候才可以
if(xxx) return;
```

案例：
现有全班学生的分数，我们希望通过这些分数做一次统计对比，划分层次，100 ~ 90 算优秀，89 ~ 80 算良好,79 ~ 70 算中等,69 ~ 60 算及格,60 分以下算不及格

```javascript
var score=88;
var leave;   //等级
if(score>=90&&score<=100){
    leave=" 优秀";
}
else if(score>=80&&score<=89){
    leave="良好";
}
else if(score>=70&&score<=79){
    leave="中等";
}
else if(score>=60&&score<=69){
    leave="及格";
}
else{
    leave="不及格";
}
//在条件限制完整的情况之下，我们是可以更改if的顺序的，但else必须放在最后
```

> 上面的代码就是一个多条件的 if 语句执行，它根据不同的条件去做了一次判断

**思考：**上在的代码是否可以简化掉

```javascript
var score=88;
var levae;   //等级
if(score>=90&&score<=100){
    leave="优秀";
}
else if(score>=80){
    leave="良好";
}
else if(score>=70){
    leave="中等";
}
else if(score>=60){
    leave="及格";
}
else{
    leave="不及格";
}
```

如果我们把上面的代码的 if 条件转一下顺序，结果就会有影响了

```javascript
var score = 85;
var leave; //等级
if (score >= 90 && score <= 100) {
   leave = "优秀";
} else if (score >= 70) {
   leave = "中等";
} else if (score >= 80) {
   leave = "良好";
}  else if (score >= 60) {
   leave = "及格";
} else {
   leave = "不及格";
}
document.write(leave);   //正确的结果应该是”良好“，结果确是'中等'

上面的代码就不准确了，时候显示的结果就出错了
这个时候 条件的顺序是不能够去进行顺序切换
```

---

条件语句也叫分支语句，最终他们的代码都 会从上向下顺序执行，但是有一种语句它却是循环执行的

### 循环语句

```javascript
/* 重复去执行一段代码（重复的去干某一些事情，如搬水等）

为什么需要循环语句？

问题：现在一楼有100桶水，每次只能够搬一桶水，现问要搬要搬多少次，怎么搬？？？

上面的搬水的事情，一次干不完，所以它要干100次，同样，在代码里面，如果某些代码一次干不完，我们循环多次去干 */
```

#### for 循环

for 循环是编程语言里面最常见的一种循环方法，它使用关键字 for 来进行，在里面限定它的开始条件与结束条件，但给一个自变量，就完成了

语法格式：

```javascript
for(开始条件;结束条件;自变量){
    //要执行的代码
}
```

现在我们试着把搬水的方法完成掉

```javascript
/*
	搬水问题分析
	1.它要搬多少桶    100
	2.从第几桶开始搬   1
	3.每次搬几桶      1
*/
for(var i=1;i<=100;i=i+1){
    console.log("搬到了第"+i+"桶水");
}
// 开始条件：var i=1;
// 结束条件：i<=100; 只要这个条件是成立的，我都要执行循环
// 自变量：i=i+1;

上面的代码就是一个最简单的循环语句，它从第1次开始，到100次结果，每次的自变量都是+1
```

##### 循环语句循环执行的到底是哪些代码？

循环语句循环的是三部分：

1. 判断条件
2. 代码体
3. 自变量执行

上面的循环语句，我们试着去做一些规范化的处理

```javascript
for(var i=0;i<100;i++){
    console.log("搬到了第"+i+"桶");
}
```

当循环省略开始条件的时候

```javascript
var i=0;
for(;i<100;i++){
    // 代码段
}

上面的代码，我们把开始条件省略掉，放在外面，这也是可行的
```

当循环省略结束条件的时候

```javascript
for(var i=0;;i++){
    // 代码段
}

这个时候，在这里他没有循环结束条件，所以它会构成一个死循环
如果不想构成死循环，后期我们会使用 break 关键字
```

当循环省略自变量的时候

```javascript
for(var i=0;i<100;){
    //代码段
    console.log('搬到了第'+i+'桶水');
    i++;
}
```

for 循环语句里面的三个条件我们都可以省略掉，所以当我们看到如下的语句的时候，不要认为他错了

```javascript
for(;;){
    //它会执行一次死循环（无限次的循环）
}
```

###### for 循环练习

1. 请计算出 1~1000 的求和
```javascript
var sum=0;   //把求和的结果，放在这个sum里面
for(var i=0;i<=1000;i++){
    // 我要把上一次的计算结果，保存在sum里面，然后在下一次去调用
    sum+=i; //sum=sum+i;
}
console.log('sum', sum);
```

2. 请计算出 1~50 里面能被 3 整除的和
```javascript
var sum2 = 0;
/* 第一种 */
for(var i=1;i<=50;i++){
    //在这里，相当于把每一个数都走了一次
    //看一下这个数能被除3整除 能被整除取余值是0
    if(i%3==0){
        sum2+=i;
    }
}
console.log('sum2', sum2);

/* 第二种 */
for(var i=1;i<=50;i+=3){
    console.log(i);
    // 直接把3的倍数循环出来相加
    sum2+=i;
}
console.log('sum2', sum2)
```

3. 在页面打印九九乘法表
```javascript
document.writeln('打印九九乘法表');
document.writeln('<br>')
for(var j=1; j<=9; j++){
   for(var i=1; i<=j; i++){
    document.writeln(i+"*"+j+"="+i*j)
   }
   document.writeln('<br>')
}
```

#### while 循环

语法格式

```javascript
while(条件表达式){
    //代码体
}
```

> while 循环跟着的是条件表达式，如果这个条件表达式为真，那么，就执行代码体，执行完代码体以后，再继续判断现在的条件是否还是成立的，如果成立，是继续执行，一直偈这样去重复

**问题：**现有 100 块砖需要从砖厂搬过来，一次只能搬一块，现在怎么样通过计算机的编程实现

```javascript
for(var i=0;i<100;i++){
    console.log("杨欢搬到第"+i+"块砖了");
}
//上面的代码就是通过for循环执行 100 次的搬砖效果，现在我们怎么样通过while循环来开始
```

把上面的代码转换 while 循环以后

```javascript
/*
  1.从第几块砖开始搬   1
  2.一次搬多少块        1
  3.一共要搬多少块      100
*/
var i=0;
while(i<100){
    console.log("搬到第"+i+"块砖了");
    i++;
}

while循环与for循环是可以相互转换的
```

在之前的时候， 我们是可以进行一个 for 循环的嵌套的，那么 while 也可以嵌套在一起，现在，可以试着把刚刚的乘法口诀使用 while 来一次

```javascript
document.write('打印九九乘法表');
document.writeln('<br>')
var j=1;
while(j<=9){
    var i=1;
    while(i<=j){
        document.writeln(i+"*"+j+"="+i*j)
        i++;
    }
    document.writeln('<br>')
    j++;
}
```

#### do...while 循环

while 与 do...while 的使用方式很相近，都是一个循环，只是有一点不一样，**while 是先判断循环条件，如果成立则执行循环，而 do...while 在这里是先执行再去判断条件是否成立**

do...while 在这里的语法格式为

```javascript
do{
   //代码段
}while(循环条件判断)

var n = 0;
while(n<=10){
	n=n+1;
}

//------------------

do{
    n=n+1;
}while(n<=10);

/* 建议在 do/while 结构的尾部使用分号表示语句结束，避免意外情况发生。 */
```

它们在使用的过程当中，99%都是相同的，循环的方式也相同，唯一的不同点

- while 是先判断循环条件是否成立，再去执行循环
- do...while 是先执行循环体代码，再去判断循环条件

**总结：**

1. 当循环的初始条件成立的时候，它们执行的循环次数是一样的
2. 当循环的初始条件不成立的时候，do...while 会执行一次，而 while 不会执行，也就是，**do...while 先执行循环中的语句,然后再判断表达式是否为真,如果为真则继续循环；如果为假,则终止循环。因此,do-while 循环至少要执行一次循环语句。**

---

##### continue 关键字

continue 关键字属于配合循环语句一起使用的一个关键字，它主要的作用就是用于跳过当前循环，再次执行下一次循环

```javascript
for(var i=0;i<20;i++){
    if(i==15){
        //假设在搬第15块砖的时候，接了电脑，它要出去接电话
        console.log("在接电话");
        continue;
    }
    console.log("在搬第"+i+"块砖");
}

在上面的代码里面它跳过了第15次的循环，而继续进行后面的循环，一直到循环结果
```

##### break 关键字

这个关键字也与循环语句结合起来一起使用，然后它主要的作用主就相当于中断当前循环（结束循环），后面的循环次数都不做了

```javascript
for(var i=0;i<20;i++){
    if(i==15){
        console.log('接到老爸电话，回家继承一个亿');
        //continue; 相当于拒绝继承一个亿，继续搬砖
        break; // 中断循环，后面没有完成的循环也不做了。相当于同意回家继承一个亿
    }
    console.log('i', i);
}
```

##### label 关键字

默认情况之下，break 与 continue 都是针对于当前循环，但是，我们也可以让它针对指定的循环，这个时候，我们就需要配置另一个语句来一起使用

label 语句用于标明某一段代码的入口

```javascript
for (var j = 1; j <= 9; j++) {
   for (var i = 1; i <= j; i++) {
       if(i==5){
           break;
       }
       document.writeln(i + "*" + j + "=" + i * j);
   }
   document.writeln("<br>");
}
```

现在我们在后面加了一个 break.这个 break 默认针对的就是当前的这个 for 循环

```javascript
out: for (var j = 1; j <= 9; j++) {
    inner: for (var i = 1; i <= j; i++) {
        if(i==5){
            break out;
        }
        document.writeln(i + "*" + j + "=" + i * j);
    }
    document.writeln("<br>");
}
```

我们分别在外边的循环上面添加了一个 out,在里面的循环上面，我们添加了一个 inner

后面当我们需要中断某个循环的时候，我们可以在 break 关键字的后边加上刚刚添加的 label（out 与 inner）

我们刚刚是在 break 的后面添加了 label ，我们可以在 continue 的后面添加 label

```javascript
continue label1;
break label2;
//上面的两种情况都是正常的
```

---

### 选择语句

选择语句指的是 switch...case 语句，主要的语法格式如下

if 语句与它的关系最为密切

```javascript
switch(值){
    case 值1：
        break;
    case 值2：
        break;
    default:
        break;
}
//把switch后面的值与case后面的值做严格相等，如果相等，那么我就选择你
```

现在我们已经知道 if 语句与 switch 非常相近，那么，我们现在就试着把下面的 if 语句转为 switch 语句

```javascript
var weather="sun";
if(weather=="rain"){
    console.log("我们去看电影");
}
else if(weather=="sun"){
    console.log("我们去森林公园");
}
else if(weather=="wind"){
    console.log("我们去放风筝");
}
else{
    console.log("我们回家睡觉");
}
//上面的条件语句指的就是根据某一个条件选择某一段代码去执行

//-----------------------------
var weather = "sun";
switch (weather) {
    case "rain":
        console.log("我们去看电影");
        break;
    case "sun":
        console.log("我们去森林公园");
        break;
    case "wind":
        console.log("我们去放风筝");
        break;
    default:
        console.log("我们回家睡觉");
}
```

1. switch 选择的时候，是从第一个 case 开始找，一直找到匹配，如果找不到就去 default 里面找
2. 如果 switch 找到了 case 以后，那么会执行 case 下面的代码，执行完毕以后，它会看一下，你是否有 break 关键字，如果有，那么，后面的就不选了，如果没有 break，就从你当前选择的这个地方开始，后面每个 case 我都执行一次,直到遇到 break 或代码结束

###### switch 练习

1. 我们现在都知道一年有 12 个月，现在，我们要做一个判断 ，11，12，1，2 这四个月为冬天，3，4，为春天，5,6,7,8,为夏天，9，10 为秋天
```javascript
设计一个程序：现在给一个变量month，根据 month的值输出一句话，判断这个month是在那个季节里面

var month = 12;
switch (month) {
 case 11:
 case 12:
 case 1:
 case 2:
     console.log("冬天");
     break;
 case 3:
 case 4:
     console.log("春天");
     break;
 case 5:
 case 6:
 case 7:
 case 8:
     console.log("夏天");
     break;
 case 9:
 case 10:
     console.log("秋天");
     break;
 default:
     console.log("month的值不对");
}
```

2. 现有全班学生的分数，我们希望通过这些分数 score 做一次统计对比，划分层次 leave，100 ~ 90 算优秀，89 ~ 80 算良好,79 ~ 70 算中等,69 ~ 60 算级格,60 分以下算不级格（使用 switch 来实现）
```javascript
var score = 12;
var num = parseInt(score / 10);
//这个整数只有可能 是0,1,2,3,4,5,6,7,8,9,10
switch (num) {
    case 10:
    case 9:
        console.log("优秀");
        break;
    case 8:
        console.log("良好");
        break;
    case 7:
        console.log("中等");
        break;
    case 6:
        console.log("及格");
        break;
    case 5:
    case 4:
    case 3:
    case 2:
    case 1:
    case 0:
        console.log("不及格");
        break;
    default:
        console.log("分数错误");
}

//----------------
var score = 76;
switch(true){
    case score<=100&&score>=90:       //false
        console.log("优秀");
        break;
    case score<=89&&score>=80:        //false
        console.log("良好");
        break;
    case score<=79&&score>=70:        //true
        console.log("中等");
        break;
    case score<=69&&score>=60:        //false
        console.log("及格");
        break;
    case score<=59&&score>=0:         //false
        console.log("不及格");
        break;
    default:
        console.log("分数不合法");
}
```
