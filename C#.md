# 基础

## 输出

```c#
Console.WriteLine()   //输出
```

## const和static关键字

```c#
/**
C#中的static 和Java中的static
简单，两者用法完全是一致的。从两方面讨论：
1. 变量是属于类的，不是实例级别的。只能通过类名调用，不能通过实例调用。
2. 如果在定义时就赋值了，那么在类初始化的时候，最先完成所有静态变量的赋值。但是要注意，所有静态变量的初始化顺序是无法确定的。

C# 中的const 和Java中的finnal
很长一段时间我一直认为两者是相同的作用，无非是变量初始化后不能更改，即只能在定义时或者构造函数中赋值。然而这仅仅只是片面的，下面将为大家详细分析：
1.修饰变量
准确的说C#中的const 等价于 Java中的static final，也就是说，Java中final不具有static的功能。而C#中的const具有static的功能。因此在C#中 public static const string 等将于 public const string。
2.修饰类和方法
此时Java中的final类似C#中的sealed，就是说，final修饰的类不能被继承，final修饰的方法不能被覆盖。
而C#中的const不能修饰类和方法。
**/
```

# 数据类型

## 整型

| 类型    | 描述                                 | 范围                                                    | 默认值 |
| ------- | ------------------------------------ | ------------------------------------------------------- | ------ |
| decimal | 128 位精确的十进制值，28-29 有效位数 | (-7.9 x 1028 到 7.9 x 1028) / 100 到 28                 | 0.0M   |
| int     | 32 位有符号整数类型                  | -2,147,483,648 到 2,147,483,647                         | 0      |
| long    | 64 位有符号整数类型                  | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 | 0L     |
| sbyte   | 8 位有符号整数类型                   | -128 到 127                                             | 0      |
| short   | 16 位有符号整数类型                  | -32,768 到 32,767                                       | 0      |
| uint    | 32 位无符号整数类型                  | 0 到 4,294,967,295                                      | 0      |
| ulong   | 64 位无符号整数类型                  | 0 到 18,446,744,073,709,551,615                         | 0      |
| ushort  | 16 位无符号整数类型                  | 0 到 65,535                                             | 0      |

## 浮点型

| 类型   | 描述              | 范围                                  | 默认值 |
| ------ | ----------------- | ------------------------------------- | ------ |
| double | 64 位双精度浮点型 | (+/-)5.0 x 10-324 到 (+/-)1.7 x 10308 | 0.0D   |
| float  | 32 位单精度浮点型 | -3.4 x 1038 到 + 3.4 x 1038           | 0.0F   |

## 布尔型

```c#
//bool	默认为False
```

## 字符型

```c#
//char	16 位 Unicode 字符	U +0000 到 U +ffff	默认为'\0'
```

## 字符串

```c#
//可以使用string或者String来修饰变量表示字符串
```

### 相关方法

```c#
/**
1	public static int Compare( string strA, string strB )
比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。该方法区分大小写。
2	public static int Compare( string strA, string strB, bool ignoreCase )
比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。但是，如果布尔参数为真时，该方法不区分大小写。
3	public static string Concat( string str0, string str1 )
连接两个 string 对象。
4	public static string Concat( string str0, string str1, string str2 )
连接三个 string 对象。
5	public static string Concat( string str0, string str1, string str2, string str3 )
连接四个 string 对象。
6	public bool Contains( string value )
返回一个表示指定 string 对象是否出现在字符串中的值。
7	public static string Copy( string str )
创建一个与指定字符串具有相同值的新的 String 对象。
8	public void CopyTo( int sourceIndex, char[] destination, int destinationIndex, int count )
从 string 对象的指定位置开始复制指定数量的字符到 Unicode 字符数组中的指定位置。
9	public bool EndsWith( string value )
判断 string 对象的结尾是否匹配指定的字符串。
10	public bool Equals( string value )
判断当前的 string 对象是否与指定的 string 对象具有相同的值。
11	public static bool Equals( string a, string b )
判断两个指定的 string 对象是否具有相同的值。
12	public static string Format( string format, Object arg0 )
把指定字符串中一个或多个格式项替换为指定对象的字符串表示形式。
13	public int IndexOf( char value )
返回指定 Unicode 字符在当前字符串中第一次出现的索引，索引从 0 开始。
14	public int IndexOf( string value )
返回指定字符串在该实例中第一次出现的索引，索引从 0 开始。
15	public int IndexOf( char value, int startIndex )
返回指定 Unicode 字符从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。
16	public int IndexOf( string value, int startIndex )
返回指定字符串从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。
17	public int IndexOfAny( char[] anyOf )
返回某一个指定的 Unicode 字符数组中任意字符在该实例中第一次出现的索引，索引从 0 开始。
18	public int IndexOfAny( char[] anyOf, int startIndex )
返回某一个指定的 Unicode 字符数组中任意字符从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。
19	public string Insert( int startIndex, string value )
返回一个新的字符串，其中，指定的字符串被插入在当前 string 对象的指定索引位置。
20	public static bool IsNullOrEmpty( string value )
指示指定的字符串是否为 null 或者是否为一个空的字符串。
21	public static string Join( string separator, string[] value )
连接一个字符串数组中的所有元素，使用指定的分隔符分隔每个元素。
22	public static string Join( string separator, string[] value, int startIndex, int count )
连接接一个字符串数组中的指定位置开始的指定元素，使用指定的分隔符分隔每个元素。
23	public int LastIndexOf( char value )
返回指定 Unicode 字符在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。
24	public int LastIndexOf( string value )
返回指定字符串在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。
25	public string Remove( int startIndex )
移除当前实例中的所有字符，从指定位置开始，一直到最后一个位置为止，并返回字符串。
26	public string Remove( int startIndex, int count )
从当前字符串的指定位置开始移除指定数量的字符，并返回字符串。
27	public string Replace( char oldChar, char newChar )
把当前 string 对象中，所有指定的 Unicode 字符替换为另一个指定的 Unicode 字符，并返回新的字符串。
28	public string Replace( string oldValue, string newValue )
把当前 string 对象中，所有指定的字符串替换为另一个指定的字符串，并返回新的字符串。
29	public string[] Split( params char[] separator )
返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。
30	public string[] Split( char[] separator, int count )
返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。int 参数指定要返回的子字符串的最大数目。
31	public bool StartsWith( string value )
判断字符串实例的开头是否匹配指定的字符串。
32	public char[] ToCharArray()
返回一个带有当前 string 对象中所有字符的 Unicode 字符数组。
33	public char[] ToCharArray( int startIndex, int length )
返回一个带有当前 string 对象中所有字符的 Unicode 字符数组，从指定的索引开始，直到指定的长度为止。
34	public string ToLower()
把字符串转换为小写并返回。
35	public string ToUpper()
把字符串转换为大写并返回。
36	public string Trim()
移除当前 String 对象中的所有前导空白字符和后置空白字符
**/
```

## 类型转换

```c#
/**
以转换为double类型举例,其他类型类似
Convert.ToDouble 与 Double.Parse 的区别。实际上 Convert.ToDouble 与 Double.Parse 较为类似，实际上 Convert.ToDouble内部调用了 Double.Parse：
(1)对于参数为null的时候：
 Convert.ToDouble参数为 null 时，返回 0.0；
 Double.Parse 参数为 null 时，抛出异常。
(2)对于参数为""的时候：
 Convert.ToDouble参数为 "" 时，抛出异常；
 Double.Parse 参数为 "" 时，抛出异常。
(3)其它区别：
 Convert.ToDouble可以转换的类型较多；
 Double.Parse 只能转换数字类型的字符串。
 Double.TryParse 与 Double.Parse 又较为类似，但它不会产生异常，转换成功返回 true，转换失败返回 false。最后一个参数为输出值，如果转换失败，输出值为 0.0。
**/
```

## 结构体

```c#
//定义结构体
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
}; 
//调用结构体
Books book；
book.title="标题"；
```

### 特点

+ C# 中的结构与传统的 C 或 C++ 中的结构不同。

+ 结构可带有方法、字段、索引、属性、运算符方法和事件。

+ 结构可定义构造函数，但不能定义析构函数。但是，您不能为结构定义默认的构造函数。默认的构造函数是自动定义的，且不能被改变。

+ 与类不同，结构不能继承其他的结构或类。

+ 结构不能作为其他结构或类的基础结构。

+ 结构可实现一个或多个接口。

+ 结构成员不能指定为 abstract、virtual 或 protected。

+ 当您使用 New 操作符创建一个结构对象时，会调用适当的构造函数来创建结构。与类不同，结构可以不使用 New 操作符即可被实例化。

+ 如果不使用 New 操作符，只有在所有的字段都被初始化之后，字段才被赋值，对象才被使用。

### 结构和类的适用场合分析

+ 当堆栈的空间很有限，且有大量的逻辑对象时，创建类要比创建结构好一些；

+ 对于点、矩形和颜色这样的轻量对象，假如要声明一个含有许多个颜色对象的数组，则CLR需要为每个对象分配内存，在这种情况下，使用结构的成本较低；

+ 在表现抽象和多级别的对象层次时，类是最好的选择，因为结构不支持继承。

+ 大多数情况下，目标类型只是含有一些数据，或者以数据为主。

## 枚举

```c#
//使用enum关键字
//定义和调用
//枚举列表中的每个符号代表一个整数值，一个比它前面的符号大的整数值。默认情况下，第一个枚举符号的值是 0
//定义：
 enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };
//调用
int WeekdayStart = (int)Days.Mon;    //返回1
```

## 引用类型

### 对象类型

+ （基类为System.Object类）

### 动态类型

+ var是C# 3中引入的，其实它仅仅只是一个语法糖. 
+ var本身并不是一种类型, 其它两者object和dynamic是类型。
+ var声明的变量在赋值的那一刻，就已经决定了它是什么类型。

+ object之所以能够被赋值为任意类型的原因，其实都知道，因为所有的类型都派生自object. 所以它可以赋值为任何类型

+ dynamic是C# 4引入的新类型，它的特点是申明为dynamic类型的变量，不是在编译时候确定实际类型的, 而是在运行时。

+ 可以调用JS(需引入Microsoft.JScript.dll)，以及python的方法

### 指针类型（与C和C++指针类似）

# 集合

