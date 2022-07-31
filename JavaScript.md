# JavaScript

+ [HTML和CSS](HTMLCSS.md)
## 基础

```javascript
let myVariable = '李雷';
myVariable = '韩梅梅';
console.log("Hello,World")    //不需要使用;号结尾
```

## 数据类型

### typeof 运算符
JavaScript 有三种方法，可以确定一个值到底是什么类型。

+ typeof运算符
+ instanceof运算符
+ Object.prototype.toString方法

instanceof运算符和Object.prototype.toString方法，将在后文介绍。这里介绍typeof运算符。

typeof运算符可以返回一个值的数据类型。

数值、字符串、布尔值分别返回number、string、boolean。
```
typeof 123 // "number"
typeof '123' // "string"
typeof false // "boolean"
函数返回function。
```
```
function f() {}
typeof f
// "function"
undefined返回undefined。
```
```
typeof undefined
// "undefined"
利用这一点，typeof可以用来检查一个没有声明的变量，而不报错。
```
```
v
// ReferenceError: v is not defined
```
```
typeof v
// "undefined"
```
上面代码中，变量v没有用var命令声明，直接使用就会报错。但是，放在typeof后面，就不报错了，而是返回undefined。

实际编程中，这个特点通常用在判断语句。
```
// 错误的写法
if (v) {
  // ...
}
// ReferenceError: v is not defined

// 正确的写法
if (typeof v === "undefined") {
  // ...
}
对象返回object。
```
```
typeof window // "object"
typeof {} // "object"
typeof [] // "object"
```
上面代码中，空数组（[]）的类型也是object，这表示在 JavaScript 内部，数组本质上只是一种特殊的对象。这里顺便提一下，instanceof运算符可以区分数组和对象。instanceof运算符的详细解释，请见《面向对象编程》一章。
```
var o = {};
var a = [];

o instanceof Array // false
a instanceof Array // true
null返回object。
```
```
typeof null // "object"
```
null的类型是object，这是由于历史原因造成的。1995年的 JavaScript 语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串和布尔值），没考虑null，只把它当作object的一种特殊值。后来null独立出来，作为一种单独的数据类型，为了兼容以前的代码，typeof null返回object就没法改变了

### 数值类型(Number)
```javascript
let myAge = 17;   //定义数值类型
```

#### 相关方法

```javascript
//数值转换为字符串
let myNum = 123;
let myString = myNum.toString();   //调用toString()方法
typeof myString;

//将字符串转为数字（parseInt()方法）
//字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。
//如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回NaN。
//如果字符串以0x或0X开头，parseInt会将其按照十六进制数解析。
//parseInt方法还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。默认情况下，parseInt的第二个参数为10，即默认是十进制转十进制。
parseInt('123') // 123
如果字符串头部有空格，空格会被自动去除。

parseInt('   81') // 81
如果parseInt的参数不是字符串，则会先转为字符串再转换。

parseInt(1.23) // 1
// 等同于
parseInt('1.23') // 1

//用于将一个字符串转为浮点数（parseFloat()方法）

//isFinite() isFinite方法返回一个布尔值，表示某个值是否为正常的数值。
```

### 布尔类型（Boolean）

```javascript
let iAmAlive = true;  //布尔类型
```

### 字符串（string）

```javascript
let dolphinGoodbye = 'So long and thanks for all the fish';
```

#### 相关方法

```javascript
//字符串拼接
let one = 'Hello, ';
let two = 'how are you?';
let joined = one + two;
joined;


//字符串转为数值类型
let myString = '123';
let myNum = Number(myString);
typeof myNum;

//字符串转换为数组
let myData = 'Manchester,London,Liverpool,Birmingham,Leeds,Carlisle'
let myArray = myData.split(',')   //使用分隔符,来分解字符串将其拼接成数组
console.log(myArray)

//获取字符串长度
let browserType = 'mozilla';
browserType.length;   //使用length方法

//检索特定字符串字符
browserType[0];
browserType[browserType.length-1];

//在字符串中查找子字符串并提取它
browserType.indexOf('zilla');   //返回位置

//提取子串
browserType.slice(0,3);   //0，3分别代表开始位置和结束位置
browserType.slice(2);   //表示从提取第三个字符开始到后面的字符串

//大小写转换
let radData = 'My NaMe Is MuD';
radData.toLowerCase();
radData.toUpperCase();

//替换
browserType.replace('moz','van');
```

### 数组（Array）

```javascript
let myNameArray = ['Chris', 'Bob', 'Jim'];
let myNumberArray = [10,15,40];

//取值
myNameArray[0]; // should return 'Chris'
myNumberArray[2]; // should return 40
```

#### 相关方法

```javascript
//获取数组长度
sequence.length;

//遍历数组
let sequence = [1, 1, 2, 3, 5, 8, 13];
for (let i = 0; i < sequence.length; i++) {
  console.log(sequence[i]);
}

//数组转换为字符串
let myArray=["111","222"];
let myNewString=myArray.join('.')  //使用.来将数组拼接成字符串，可以使用不同的分隔符拼接字符串
console.log(myNewString)     //输出111.222

let myArray=["111","222"]
let myNewString=myArray.toString()  //也可以使用toString方法来进行拼接
console.log(myNewString)   //输出111,222

//添加和删除数组项
let myArray = ['Manchester', 'London', 'Liverpool', 'Birmingham', 'Leeds', 'Carlisle'];
myArray.push('Bristol')   //添加到结尾
myArray.pop();  //删除最后一项
myArray.unshift('Edinburgh');  //添加到开始
myArray.shift()   //删除最开始一项
```

# 条件语句和循环语句

JavaScript 提供if结构和switch结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。循环语句用于重复执行某个操作，它有多种形式。

## if 结构
if结构先判断一个表达式的布尔值，然后根据布尔值的真伪，执行不同的语句。所谓布尔值，指的是 JavaScript 的两个特殊值，true表示真，false表示伪。
```javascript
if (布尔值)
  语句;
// 或者
if (布尔值) 语句;
```
上面是if结构的基本形式。需要注意的是，“布尔值”往往由一个条件表达式产生的，必须放在圆括号中，表示对表达式求值。如果表达式的求值结果为true，就执行紧跟在后面的语句；如果结果为false，则跳过紧跟在后面的语句。
```javascript
if (m === 3)
  m = m + 1;
```
上面代码表示，只有在m等于3时，才会将其值加上1。

这种写法要求条件表达式后面只能有一个语句。如果想执行多个语句，必须在if的条件判断之后，加上大括号，表示代码块（多个语句合并成一个语句）。
```javascript
if (m === 3) {
  m += 1;
}
建议总是在if语句中使用大括号，因为这样方便插入语句。
```
注意，if后面的表达式之中，不要混淆赋值表达式（=）、严格相等运算符（===）和相等运算符（==）。尤其是赋值表达式不具有比较作用。
```javascript
var x = 1;
var y = 2;
if (x = y) {
  console.log(x);
}
// "2"
```
上面代码的原意是，当x等于y的时候，才执行相关语句。但是，不小心将严格相等运算符写成赋值表达式，结果变成了将y赋值给变量x，再判断变量x的值（等于2）的布尔值（结果为true）。

这种错误可以正常生成一个布尔值，因而不会报错。为了避免这种情况，有些开发者习惯将常量写在运算符的左边，这样的话，一旦不小心将相等运算符写成赋值运算符，就会报错，因为常量不能被赋值。
```javascript
if (x = 2) { // 不报错
if (2 = x) { // 报错
```
至于为什么优先采用“严格相等运算符”（===），而不是“相等运算符”（==），请参考《运算符》章节。

## if...else 结构
if代码块后面，还可以跟一个else代码块，表示不满足条件时，所要执行的代码。
```javascript
if (m === 3) {
  // 满足条件时，执行的语句
} else {
  // 不满足条件时，执行的语句
}
```
上面代码判断变量m是否等于3，如果等于就执行if代码块，否则执行else代码块。

对同一个变量进行多次判断时，多个if...else语句可以连写在一起。
```javascript
if (m === 0) {
  // ...
} else if (m === 1) {
  // ...
} else if (m === 2) {
  // ...
} else {
  // ...
}
```
else代码块总是与离自己最近的那个if语句配对。
```javascript
var m = 1;
var n = 2;

if (m !== 1)
if (n === 2) console.log('hello');
else console.log('world');
```
上面代码不会有任何输出，else代码块不会得到执行，因为它跟着的是最近的那个if语句，相当于下面这样。
```javascript
if (m !== 1) {
  if (n === 2) {
    console.log('hello');
  } else {
    console.log('world');
  }
}
```
如果想让else代码块跟随最上面的那个if语句，就要改变大括号的位置。
```javascript
if (m !== 1) {
  if (n === 2) {
    console.log('hello');
  }
} else {
  console.log('world');
}
// world
```
## switch 结构
多个if...else连在一起使用的时候，可以转为使用更方便的switch结构。
```javascript
switch (fruit) {
  case "banana":
    // ...
    break;
  case "apple":
    // ...
    break;
  default:
    // ...
}
```
上面代码根据变量fruit的值，选择执行相应的case。如果所有case都不符合，则执行最后的default部分。需要注意的是，每个case代码块内部的break语句不能少，否则会接下去执行下一个case代码块，而不是跳出switch结构。
```javascript
var x = 1;

switch (x) {
  case 1:
    console.log('x 等于1');
  case 2:
    console.log('x 等于2');
  default:
    console.log('x 等于其他值');
}
// x等于1
// x等于2
// x等于其他值
```
上面代码中，case代码块之中没有break语句，导致不会跳出switch结构，而会一直执行下去。正确的写法是像下面这样。
```javascript
switch (x) {
  case 1:
    console.log('x 等于1');
    break;
  case 2:
    console.log('x 等于2');
    break;
  default:
    console.log('x 等于其他值');
}
```
switch语句部分和case语句部分，都可以使用表达式。
```javascript
switch (1 + 3) {
  case 2 + 2:
    f();
    break;
  default:
    neverHappens();
}
```
上面代码的default部分，是永远不会执行到的。

需要注意的是，switch语句后面的表达式，与case语句后面的表示式比较运行结果时，采用的是严格相等运算符（===），而不是相等运算符（==），这意味着比较时不会发生类型转换。
```javascript
var x = 1;

switch (x) {
  case true:
    console.log('x 发生类型转换');
    break;
  default:
    console.log('x 没有发生类型转换');
}
// x 没有发生类型转换
```
上面代码中，由于变量x没有发生类型转换，所以不会执行case true的情况。这表明，switch语句内部采用的是“严格相等运算符”，详细解释请参考《运算符》一节。

## 三元运算符 ?:
JavaScript 还有一个三元运算符（即该运算符需要三个运算子）?:，也可以用于逻辑判断。
```javascript
(条件) ? 表达式1 : 表达式2
```
上面代码中，如果“条件”为true，则返回“表达式1”的值，否则返回“表达式2”的值。
```javascript
var even = (n % 2 === 0) ? true : false;
```
上面代码中，如果n可以被2整除，则even等于true，否则等于false。它等同于下面的形式。
```javascript
var even;
if (n % 2 === 0) {
  even = true;
} else {
  even = false;
}
```
这个三元运算符可以被视为if...else...的简写形式，因此可以用于多种场合。
```javascript
var myVar;
console.log(
  myVar ?
  'myVar has a value' :
  'myVar does not have a value'
)
// myVar does not have a value
```
上面代码利用三元运算符，输出相应的提示。
```javascript
var msg = '数字' + n + '是' + (n % 2 === 0 ? '偶数' : '奇数');
```
上面代码利用三元运算符，在字符串之中插入不同的值。

## while 循环
While语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。
```javascript
while (条件)
  语句;

// 或者
while (条件) 语句;
```
while语句的循环条件是一个表达式，必须放在圆括号中。代码块部分，如果只有一条语句，可以省略大括号，否则就必须加上大括号。
```javascript
while (条件) {
  语句;
}
```
下面是while语句的一个例子。
```javascript
var i = 0;

while (i < 100) {
  console.log('i 当前为：' + i);
  i = i + 1;
}
```
上面的代码将循环100次，直到i等于100为止。

下面的例子是一个无限循环，因为循环条件总是为真。
```javascript
while (true) {
  console.log('Hello, world');
}
```
## for 循环
for语句是循环命令的另一种形式，可以指定循环的起点、终点和终止条件。它的格式如下。
```javascript
for (初始化表达式; 条件; 递增表达式)
  语句

// 或者

for (初始化表达式; 条件; 递增表达式) {
  语句
}
```
for语句后面的括号里面，有三个表达式。

初始化表达式（initialize）：确定循环变量的初始值，只在循环开始时执行一次。
条件表达式（test）：每轮循环开始时，都要执行这个条件表达式，只有值为真，才继续进行循环。
递增表达式（increment）：每轮循环的最后一个操作，通常用来递增循环变量。
下面是一个例子。
```javascript
var x = 3;
for (var i = 0; i < x; i++) {
  console.log(i);
}
// 0
// 1
// 2
```
上面代码中，初始化表达式是var i = 0，即初始化一个变量i；测试表达式是i < x，即只要i小于x，就会执行循环；递增表达式是i++，即每次循环结束后，i增大1。

所有for循环，都可以改写成while循环。上面的例子改为while循环，代码如下。
```javascript
var x = 3;
var i = 0;

while (i < x) {
  console.log(i);
  i++;
}
```
for语句的三个部分（initialize、test、increment），可以省略任何一个，也可以全部省略。
```javascript
for ( ; ; ){
  console.log('Hello World');
}
```
上面代码省略了for语句表达式的三个部分，结果就导致了一个无限循环。

## do...while 循环
do...while循环与while循环类似，唯一的区别就是先运行一次循环体，然后判断循环条件。
```javascript
do
  语句
while (条件);

// 或者
do {
  语句
} while (条件);
```
不管条件是否为真，do...while循环至少运行一次，这是这种结构最大的特点。另外，while语句后面的分号注意不要省略。

下面是一个例子。
```javascript
var x = 3;
var i = 0;

do {
  console.log(i);
  i++;
} while(i < x);
```
## break 语句和 continue 语句
break语句和continue语句都具有跳转作用，可以让代码不按既有的顺序执行。

break语句用于跳出代码块或循环。
```javascript
var i = 0;

while(i < 100) {
  console.log('i 当前为：' + i);
  i++;
  if (i === 10) break;
}
```
上面代码只会执行10次循环，一旦i等于10，就会跳出循环。

for循环也可以使用break语句跳出循环。
```javascript
for (var i = 0; i < 5; i++) {
  console.log(i);
  if (i === 3)
    break;
}
// 0
// 1
// 2
// 3
```
上面代码执行到i等于3，就会跳出循环。

## continue语句
用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。
```javascript
var i = 0;

while (i < 100){
  i++;
  if (i % 2 === 0) continue;
  console.log('i 当前为：' + i);
}
```
上面代码只有在i为奇数时，才会输出i的值。如果i为偶数，则直接进入下一轮循环。

如果存在多重循环，不带参数的break语句和continue语句都只针对最内层循环。

## 标签（label）
JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，标签的格式如下。
```javascript
label:
  语句
```
标签可以是任意的标识符，但不能是保留字，语句部分可以是任意语句。

标签通常与break语句和continue语句配合使用，跳出特定的循环。
```javascript
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
```
上面代码为一个双重循环区块，break命令后面加上了top标签（注意，top不用加引号），满足条件时，直接跳出双层循环。如果break语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。

标签也可以用于跳出代码块。
```javascript
foo: {
  console.log(1);
  break foo;
  console.log('本行不会输出');
}
console.log(2);
// 1
// 2
```
上面代码执行到break foo，就会跳出区块。

continue语句也可以与标签配合使用。
```javascript
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
// i=2, j=0
// i=2, j=1
// i=2, j=2
```
上面代码中，continue命令后面有一个标签名，满足条件时，会跳过当前循环，直接进入下一轮外层循环。如果continue语句后面不使用标签，则只能进入下一轮的内层循环

# 对象

## 第一个例子

```javascript
//创建空对象
let person = {}
//添加数据
let person = {
  name : ['Bob', 'Smith'],
  age : 32,
  gender : 'male',
  interests : ['music', 'skiing'],
  bio : function() {
    alert(this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function() {
    alert('Hi! I\'m ' + this.name[0] + '.');
  }
};

console.log(person.name[0])
console.log(person.age)
console.log(person.interests[1])
person.bio()
person.greeting()

//输出
Bob
32
skiing
```

## 点表示法和括号表示法

#### 点表示法

```javascript
person.age
person.interests[1]
person.bio()

//子命名空间（可以用一个对象来做另一个对象成员的值。例如将name成员）
name : {
  first : 'Bob',
  last : 'Smith'
},
  
//调用
person.name.first
person.name.last  
```

#### 括号表示法

```javascript
person['age']
person['name']['first']
```

## this关键字

```javascript
//关键字"this"指向了当前代码运行时的对象( 原文：the current object the code is being written inside )——这里即指person对象
greeting: function() {
  alert('Hi! I\'m ' + this.name.first + '.');
}
```

## 通过函数创建对象

```javascript
function createNewPerson(name) {
  var obj = {};
  obj.name = name;
  obj.greeting = function () {
    alert('Hi! I\'m ' + this.name + '.');
  }
  return obj;
}

//创建对象
let salva = createNewPerson('salva');
salva.name;   
salva.greeting();

//简写
function Person(name) {
  this.name = name;
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
  };
}

//创建对象
var person1 = new Person('Bob');
var person2 = new Person('Sarah');
person1.name
person1.greeting()
person2.name
person2.greeting()

//带有构造函数的
function Person(first, last, age, gender, interests) {
  this.name = {
    'first': first,
    'last': last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.bio = function() {
    alert(this.name.first + ' ' + this.name.last + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  };
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name.first + '.');
  };
};

//创建对象
var person1 = new Person('Bob', 'Smith', 32, 'male', ['music', 'skiing']);
person1['age']
person1.interests[1]
person1.bio()
```

## 其他创建对象的方式

### Object()构造函数

```javascript
var person1 = new Object();
person1.name = 'Chris';
person1['age'] = 38;
person1.greeting = function() {
  alert('Hi! I\'m ' + this.name + '.');
}
//或者
var person1 = new Object({
  name : 'Chris',
  age : 38,
  greeting : function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
});
```

### 使用create()方法

```javascript
//基于现有对象创建新对象
var person2 = Object.create(person1);
person2.name
person2.greeting()
```

## 原型和原型链（重点）

## 继承（重点）

# 操作DOM

### 节点操作

```javascript
document.getElementById ：根据ID查找元素，大小写敏感，如果有多个结果，只返回第一个；
document.getElementsByClassName ：根据类名查找元素，多个类名用空格分隔，返回一个 HTMLCollection 。注意兼容性为IE9+（含）。另外，不仅仅是document，其它元素也支持 getElementsByClassName 方法；
document.getElementsByTagName ：根据标签查找元素， * 表示查询所有标签，返回一个 HTMLCollection 。
document.getElementsByName ：根据元素的name属性查找，返回一个 NodeList 。
document.querySelector ：返回单个Node，IE8+(含），如果匹配到多个结果，只返回第一个。
document.querySelectorAll ：返回一个 NodeList ，IE8+(含）。
document.forms ：获取当前页面所有form，返回一个 HTMLCollection ；
```

### 节点创建

```javascript
//createElement创建元素
var elem = document.createElement("div");  
elem.id = 'haorooms';  
elem.style = 'color: red';  
elem.innerHTML = '我是新创建的haorooms测试节点';  
document.body.appendChild(elem);  

//createTextNode创建文本节点
var node = document.createTextNode("我是文本节点");  
document.body.appendChild(node); 

//cloneNode 克隆一个节点：
var from = document.getElementById("test");  
var clone = from.cloneNode(true);  
clone.id = "test2";  
document.body.appendChild(clone); 
```

### 节点关系

```javascript
//父关系
parentNode ：每个节点都有一个parentNode属性，它表示元素的父节点。Element的父节点可能是Element，Document或DocumentFragment；
parentElement ：返回元素的父元素节点，与parentNode的区别在于，其父节点必须是一个Element元素，如果不是，则返回null；

//子关系
children ：返回一个实时的 HTMLCollection ，子节点都是Element，IE9以下浏览器不支持；
childNodes ：返回一个实时的 NodeList ，表示元素的子节点列表，注意子节点可能包含文本节点、注释节点等；
firstChild ：返回第一个子节点，不存在返回null，与之相对应的还有一个 firstElementChild ；
lastChild ：返回最后一个子节点，不存在返回null，与之相对应的还有一个 lastElementChild ；

//兄弟关系
previousSibling ：节点的前一个节点，如果不存在则返回null。注意有可能拿到的节点是文本节点或注释节点，与预期的不符，要进行处理一下。
nextSibling ：节点的后一个节点，如果不存在则返回null。注意有可能拿到的节点是文本节点，与预期的不符，要进行处理一下。
previousElementSibling ：返回前一个元素节点，前一个节点必须是Element，注意IE9以下浏览器不支持。
nextElementSibling ：返回后一个元素节点，后一个节点必须是Element，注意IE9以下浏览器不支持。
```

### 元素属性

```javascript
element.setAttribute(name, value);   //给元素设置属性
var value = element.getAttribute("id"); //获取属性值，没有返回null

//是否存在该属性值
var result = element.hasAttribute(name);
var foo = document.getElementById("foo"); 
if (foo.hasAttribute("bar")) { 
    // do something
}

//
```

### 样式

```javascript
//直接修改样式
elem.style.color = 'red';  
elem.style.setProperty('font-size', '16px');  
elem.style.removeProperty('color');  

//动态修改样式
var style = document.createElement('style');  
style.innerHTML = 'body{color:red} #top:hover{background-color: red;color: white;}';  
document.head.appendChild(style);  

//classList获取样式class
// div is an object reference to a <div> element with class="foo bar"
div.classList.remove("foo");
div.classList.add("anotherclass");

// if visible is set remove it, otherwise add it
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10 );

alert(div.classList.contains("foo"));

// add or remove multiple classes
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// add or remove multiple classes using spread syntax
let cls = ["foo", "bar"];
div.classList.add(...cls); 
div.classList.remove(...cls);

// replace class "foo" with class "bar"
div.classList.replace("foo", "bar");

//通过 element.sytle.xxx 只能获取到内联样式，借助 window.getComputedStyle 可以获取应用到元素上的所有样式，IE8或更低版本不支持此方法。
var style = window.getComputedStyle(element[, pseudoElt]);  
```

