# 基础

## 输出

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
```



### 布尔类型（Boolean）

```javascript
let iAmAlive = true;  //布尔类型
```

### 字符串（String）

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

