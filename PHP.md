# 基础

## 安装

### mac安装

```
//mac默认自带php7.2，安装其他版本
curl -s http://php-osx.liip.ch/install.sh | bash -s 5.6   //5.6表示版本号，默认安装到/usr/local/php5.6下
```

## 输出

### echo

```php
<?php
$a = "Hello";    //定义变量前面要加$符号
$b = "World";
$c = 5;
echo $a;       //输出Hello
echo $a, $b;   //输出HelloWorld,使用逗号拼接两个变量
```

### print

```php
/**
%% - 返回一个百分号 %
%b - 二进制数
%c - ASCII 值对应的字符
%d - 包含正负号的十进制数（负数、0、正数）
%e - 使用小写的科学计数法（例如 1.2e+2）
%E - 使用大写的科学计数法（例如 1.2E+2）
%u - 不包含正负号的十进制数（大于等于 0）
%f - 浮点数（本地设置）
%F - 浮点数（非本地设置）
%g - 较短的 %e 和 %f
%G- 较短的 %E 和 %f
%o - 八进制数
%s - 字符串
%x - 十六进制数（小写字母）
%X - 十六进制数（大写字母）
附加的格式值。必需放置在 % 和字母之间（例如 %.2f）：

+（在数字前面加上 + 或 - 来定义数字的正负性。默认地，只有负数做标记，正数不做标记）
’ （规定使用什么作为填充，默认是空格。它必须与宽度指定器一起使用。）
-（左调整变量值）
[0-9] （规定变量值的最小宽度）
.[0-9] （规定小数位数或最大字符串长度）
**/
```

## $符号

在PHP中单个美元符号变量($str)，表示一个名为str的普通变量，它可以存储字符串、整数、数组、布尔等任何类型的值。

```php
//例子1（双美元符号的变量($$str)：表示一个可变变量(也可叫做引用变量)，用于存储$str的值）
<?php
$var = 'hello word !';
$str = 'var';
echo $str;
echo $$str;
?>
    
//例子2    
<?php
$a = 'b';
$b = 'c';
$c = 'a';
echo $a; //输出 ：b
echo $b; //输出 ：c
echo $c; //输出 ：a
echo $$a; //输出 ：c
echo $$$a; //输出 ：a
echo $$$$a; //输出 ：b
?>

//例子3（类的动态实例化）
<?php
class data_user {
 function age(){
 return '10';
 }
}
$var = 'data_user';
$a = new $var;
echo $a->age();
?>
//输出结果：10    
```

## 条件判断和循环

### 条件判断

```php
//if语句
if (条件)
{
    条件成立时要执行的代码;
}

//if..else语句
if (条件)
{
条件成立时执行的代码;
}
else
{
条件不成立时执行的代码;
}

//if....elseif....else
if (条件)
{
    if 条件成立时执行的代码;
}
elseif (条件)
{
    elseif 条件成立时执行的代码;
}
else
{
    条件不成立时执行的代码;
}

//switch
<?php
switch (n)
{
case label1:
    如果 n=label1，此处代码将执行;
    break;
case label2:
    如果 n=label2，此处代码将执行;
    break;
default:
    如果 n 既不等于 label1 也不等于 label2，此处代码将执行;
}
?>
```

### 循环

```php
//1、for循环语法
for (初始值; 条件; 增量)
{
    要执行的代码;
}
//例子
<?php
for ($i=1; $i<=5; $i++)
{
    echo "数字为 " . $i . PHP_EOL;
}
?>
    
//foreach 循环
foreach ($array as $value)
{
    要执行代码;
}
foreach ($array as $key => $value)
{
    要执行代码;
}
//例子1
<?php
$x=array("Google","Runoob","Taobao");
foreach ($x as $value)
{
    echo $value . PHP_EOL;
}
?>
输出：
    Google
    Runoob
    Taobao
//例子2
<?php
$x=array(1=>"Google", 2=>"Runoob", 3=>"Taobao");
foreach ($x as $key => $value)
{
    echo "key  为 " . $key . "，对应的 value 为 ". $value . PHP_EOL;
}
?>    
输出：
    key  为 1，对应的 value 为 Google
    key  为 2，对应的 value 为 Runoob
    key  为 3，对应的 value 为 Taobao
    
//2、while循环
while (条件)
{
    要执行的代码;
}
和
do
{
    要执行的代码;
}
while (条件);
```

## 命名空间

## include和require

相同点：
  1、都用来包含文件
  2、include_once 和 require_once 都会先检查文件是否包含过

不同点：
  1、require 包含文件时，若文件存在错误，程序会中断，显示致命错误。
  2、include 包含文件时，若文件存在错误，程序会发出警告，继续执行。
  3、require 一般用于程序开头
  4、include 一般用于程序流程中

简而言之：
  require 会报错，放开头
  include 会警告，放中间
  include_once require_once 只包含一次

## 异常捕捉

```php
//try...catch和throw
<?php
// 创建一个有异常处理的函数
function checkNum($number)
{
    if($number>1)
    {
        throw new Exception("变量值必须小于等于 1");
    }
        return true;
}
    
// 在 try 块 触发异常
try
{
    checkNum(2);
    // 如果抛出异常，以下文本不会输出
    echo '如果输出该内容，说明 $number 变量';
}
// 捕获异常
catch(Exception $e)
{
    echo 'Message: ' .$e->getMessage();
}
?>
```



# 数据类型

PHP不需要显示声明数据类型

## 整型

```php
<?php 
$x = 5985;
var_dump($x);      //var_dump()函数用于输出变量的数据类型和值
echo "<br>"; 
$x = -345; // 负数 
var_dump($x);
echo "<br>"; 
$x = 0x8C; // 十六进制数
var_dump($x);
echo "<br>";
$x = 047; // 八进制数
var_dump($x);
?>

/**
输出：
int(5985)
int(-345)
int(140)
int(39)
**/
```

## 浮点型

```php
<?php
$x = 10.365;
var_dump($x);
echo "<br>";
$x = 2.4e3;
var_dump($x);
echo "<br>";
$x = 8E-5;
var_dump($x);
?>
```

## 布尔类型

```php
$x=true;
$y=false;
```

## 字符串

```php
//输出字符串
<?php
$txt="Hello world!";
echo $txt;
?>
    
//并置运算符（使用.将两个字符串拼接）
<?php
$txt1="Hello world!";
$txt2="What a nice day!";
echo $txt1 . " " . $txt2;
?>
    
//strlen()函数
<?php
echo strlen("Hello world!");  //输出12
?>    
    
//strpos()函数（函数用于在字符串内查找一个字符或一段指定的文本的位置）
<?php
echo strpos("Hello world!","world");  //输出6
?>    
```

### htmlspecialchars()函数



## 数组

### 数值数组

```php
//创建数组
$cars=array("Volvo","BMW","Toyota");
//例子
<?php
$cars=array("Volvo","BMW","Toyota");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
?>

//数组长度count()函数
<?php
$cars=array("Volvo","BMW","Toyota");
echo count($cars);  //输出3
?>    
    
//遍历
<?php
$cars=array("Volvo","BMW","Toyota");
$arrlength=count($cars);
 
for($x=0;$x<$arrlength;$x++)
{
    echo $cars[$x];
    echo "<br>";
}
?>    
```

### 关联数组

```php
//创建数组
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
或者
$age['Peter']="35";
$age['Ben']="37";
$age['Joe']="43";

//遍历
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
foreach($age as $x=>$x_value)
{
    echo "Key=" . $x . ", Value=" . $x_value;
    echo "<br>";
}
?>
```

### 数组排序

```php
/**
排序函数：
sort() - 对数组进行升序排列
rsort() - 对数组进行降序排列
asort() - 根据关联数组的值，对数组进行升序排列
ksort() - 根据关联数组的键，对数组进行升序排列
arsort() - 根据关联数组的值，对数组进行降序排列
krsort() - 根据关联数组的键，对数组进行降序排列
**/

```

# 面向对象

```php
<?php

/**
 *   访问控制 public（公有），protected（受保护）或 private（私有）
 *   类属性必须定义为公有，受保护，私有之一。如果用 var 定义，则被视为公有
 *   类中的方法可以被定义为公有，私有或受保护。如果没有设置这些关键字，则该方法默认为公有。
 *   static关键字：声明类属性或方法为 static(静态)，就可以不实例化类而直接访问。
 *   final关键字：PHP 5 新增了一个 final 关键字。如果父类中的方法被声明为 final，则子类无法覆盖该方法。如果一个类被声明为 final，则不能被继承。
 */
class Father
{
    /* 成员变量 */
    var $eat;

    function __construct()    //构造函数的命名,做一些初始化操作
    {
        print "构造函数\n";
    }

    function __destruct()   //析构函数的命名,做一些销毁动作
    {
        print "销毁 ";
    }

    /* 成员函数 */
    function setEat($par)
    {
        $this->eat = $par;
    }

    function getEat()
    {
        echo $this->eat . PHP_EOL;
    }
}

//php接口和抽象类与java很相似
class Son extends Father
{
    //子类 可以对 public 和 protected 进行重定义，但 private 而不能

    //方法重写
}

$a = new Father();
$a->setEat("鸡");
$a->getEat();
?>
```

# 表单

## $_GET变量

```php+HTML
<!--
$_GET 变量用于收集来自 method="get" 的表单中的值
-->

<!--form.php,将输入的值通过get请求提交到welcome.php里面去
点击提交按钮请求地址 http://www.runoob.com/welcome.php?fname=Runoob&age=3
-->
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<form action="welcome.php" method="get">
名字: <input type="text" name="fname">
年龄: <input type="text" name="age">
<input type="submit" value="提交">
</form>
</body>
</html>

<!--welcome.php接收传过来的值-->
欢迎 <?php echo $_GET["fname"]; ?>!<br>
你的年龄是 <?php echo $_GET["age"]; ?>  岁。
```

## $_POST变量

```php+HTML
<!--
$_POST 变量用于收集来自 method="post" 的表单中的值
-->

<!--
form.php,将输入的值通过post请求提交到welcome.php里面去
点击提交按钮请求地址 http://www.runoob.com/welcome.php
-->
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<form action="welcome.php" method="post">
名字: <input type="text" name="fname">
年龄: <input type="text" name="age">
<input type="submit" value="提交">
</form>
</body>
</html>

<!--welcome.php接收传过来的值-->
欢迎 <?php echo $_POST["fname"]; ?>!<br>
你的年龄是 <?php echo $_POST["age"]; ?>  岁。
```

## $_REQUEST变量

```php+HTML
<!--
$_REQUEST 变量包含了 $_GET、$_POST 和 $_COOKIE 的内容。
$_REQUEST 变量可用来收集通过 GET 和 POST 方法发送的表单数据。
-->

<!--
welcome.php 文件修改为如下代码，它可以接受 $_GET、$_POST等数据
-->
欢迎 <?php echo $_REQUEST["fname"]; ?>!<br>
你的年龄是 <?php echo $_REQUEST["age"]; ?>  岁。
```

# 集成环境

+ [XAMPP（支持Mac、Linux、Window )](https://sourceforge.net/projects/xampp/) 
+ 

# 操作MySQL

[Mysql、Mysqli、Pdo区别](https://blog.csdn.net/Hqs_1020417504/article/details/79670123)

## 连接MySQL

```php
//使用mysqli进行数据库连接,无法访问将在php安装目录下的php.ini 配置文件中的 extension_dir 去掉分号并且将dir改成自己所对应的php目录！
<?php
$servername = "localhost";
$username = "root";
$password = "123456";

// 创建连接
$conn = mysqli_connect($servername, $username, $password);

// 检测连接
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
$conn->close();
echo "连接成功";
?>
```

## 创建数据库和表

```php
//使用mysqli创建数据库和表,面向对象的方式
$servername = "localhost";
$username = "root";
$password = "123456";
$dbname = "mydb";

// 创建连接
$conn = new mysqli($servername, $username, $password);
// 检测连接
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
}

// 创建数据库
$sql = "CREATE DATABASE IF NOT EXISTS myDB";
if ($conn->query($sql) === TRUE) {
    echo "数据库创建成功";
} else {
    echo "Error creating database: " . $conn->error;
}

$conn->select_db($dbname);
// 使用 sql 创建数据表,包含的字段
$sql = "CREATE TABLE IF NOT EXISTS MyGuests (
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
firstname VARCHAR(30) NOT NULL,
lastname VARCHAR(30) NOT NULL,
email VARCHAR(50),
reg_date TIMESTAMP
)";

if ($conn->query($sql) === TRUE) {
    echo "Table MyGuests created successfully";
} else {
    echo "创建数据表错误: " . $conn->error;
}
$conn->close();
```

## 插入数据

```php
//单条数据
$sql = "INSERT INTO mydb.myguests (firstname, lastname, email)   //mydb.myguests表示mydb数据库下的myguests表
VALUES ('John', 'Doe', 'john@example.com')";
if ($conn->query($sql) === TRUE) {
    echo "新记录插入成功";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

//多条数据
$sql = "INSERT INTO mydb.myguests (firstname, lastname, email)
VALUES ('John', 'Doe', 'john@example.com');";
$sql .= "INSERT INTO mydb.myguests (firstname, lastname, email)
VALUES ('Mary', 'Moe', 'mary@example.com');";
$sql .= "INSERT INTO mydb.myguests (firstname, lastname, email)
VALUES ('Julie', 'Dooley', 'julie@example.com')";

if ($conn->multi_query($sql) === TRUE) {
    echo "新记录插入成功";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

//使用预处理插入
$stmt = $conn->prepare("INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)");
$stmt->bind_param("sss", $firstname, $lastname, $email);
 
// 设置参数并执行
$firstname = "John";
$lastname = "Doe";
$email = "john@example.com";
$stmt->execute();
 
$firstname = "Mary";
$lastname = "Moe";
$email = "mary@example.com";
$stmt->execute();
 
$firstname = "Julie";
$lastname = "Dooley";
$email = "julie@example.com";
$stmt->execute();

echo "新记录插入成功";
$stmt->close();

```

## 查询数据

```php
$sql = "SELECT id, firstname, lastname FROM MyGuests";
$result = $conn->query($sql);
 
if ($result->num_rows > 0) {
    // 输出数据
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["firstname"]. " " . $row["lastname"]. "<br>";
    }
} else {
    echo "0 结果";
}
```

