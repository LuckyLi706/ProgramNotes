# 一、基础

## 1.1、输入输出

```c++
#include <iostream>  //C++输入输出的库,没有.h后缀，与c的区别

using namespace std;  //使用输入输出的命名空间

int main() {
    int a;
    cin >> a;  //cin为输入函数
    cout << "输入的数为：" << a << endl;   //cout为输出函数，endl为换行符
    return 0;
}
```

## 1.2、命名空间

## 1.3、预处理器

## 1.4、异常处理



# 二、数据类型

## 2.1、整型

short、int、long、long long

- short至少16位
- int至少与short一样长
- long至少32位，至少与int一样长
- long long至少64位，至少与long一样长

### 2.1.1、sizeof运算符

可对类型名或者变量名使用sizeof运算符，输出字节数。

```c++
int a = 0;
cout << sizeof(a) << endl;  
//输出4，表示变量a占四个字节
```

### 2.1.2 limits头文件

包含当前操作系统下的最大值和最小值

```c++
#include <limits>   //头文件

using namespace std;  //使用输入输出的命名空间

int main() {
    cout << INT_MAX << endl;  //输出int类型在当前的最大值
    return 0;
}
```

### 2.1.3 无符号类型

无符号类型只有在非负数情况下才可以使用

unsigned short、unsigned（表示无符号int整形）、unsigned long、unsigned long long

### 2.1.4 十六进制和八进制表示

```c++
int a=0x16;   //这边的16为十六进制
int b=016;    //这边的16为八进制
```

## 2.2、字符型

存储0~128个ASCII码

c++11 新增char16_t和char32_t

## 2.3、布尔型

true和false。true为1，false为0

## 2.4 const关键字

使用const来代替define声明常量。

## 2.5 浮点型

float、double、long double

## 2.6 auto关键字

```c++
auto a = 'a';   //不显示的指明类型，使用auto关键字系统会自动识别
```

## 2.7 字符串（c++的string类，c风格的见C语言）

```c++
#include <iostream>  //C++输入输出的库,没有.h后缀，与c的区别
#include <string>  //c++风格的字符串头文件

using namespace std;  //使用输入输出的命名空间

int main() {
    string str1 = "Hello";  //c++的字符串类使用小写的string表示
    string str2 = "World";
    string str3;
    int  len ;

    str3 = str1;  //字符串的复制
    cout << "str3 : " << str3 << endl;

    str3 = str1 + str2;  //字符串的拼接
    cout << "str1 + str2 : " << str3 << endl;

    len = str3.size();  //字符串的长度
    cout << "str3.size() :  " << len << endl;
}
```

## 2.8 结构体

## 2.9 共用体

## 2.10 枚举

# 三 数据类型（二）

## 3.1、数组

```c++
共同点
（1.）都和数组相似，都可以使用标准数组的表示方法来访问每个元素（array和vector都对下标运算符[ ]进行了重载）
（2.）三者的存储都是连续的，可以进行随机访问
不同点
（0.）数组是不安全的，array和vector是比较安全的（有效的避免越界等问题）
（1.）array对象和数组存储在相同的内存区域（栈）中，vector对象存储在自由存储区（堆）
（2.）array可以将一个对象赋值给另一个array对象，但是数组不行
（3.）vector属于变长的容器，即可以根据数据的插入和删除重新构造容器容量；但是array和数组属于定长容器
（4.）vector和array提供了更好的数据访问机制，即可以使用front()和back()以及at()（at()可以避免a[-1]访问越界的问题）访问方式，使得访问更加安全。而数组只能通过下标访问，在写程序中很容易出现越界的错误
（5.）vector和array提供了更好的遍历机制，即有正向迭代器和反向迭代器
（6.）vector和array提供了size()和Empty()，而数组只能通过sizeof()/strlen()以及遍历计数来获取大小和是否为空
（7.）vector和array提供了两个容器对象的内容交换，即swap()的机制，而数组对于交换只能通过遍历的方式逐个交换元素
（8.）array提供了初始化所有成员的方法fill（）
（9.）由于vector的动态内存变化的机制，在插入和删除时，需要考虑迭代的是否有效问题
（10.）vector和array在声明变量后，在声明周期完成后，会自动地释放其所占用的内存。对于数组如果用new[ ]/malloc申请的空间，必须用对应的delete[ ]和free来释放内存
```

### 3.1.1 c类型数组（不建议使用）

```c++
#include <iostream>  //C++输入输出的库,没有.h后缀，与c的区别
using namespace std;  //使用输入输出的命名空间

int main() {
    int n[10]; // n 是一个包含 10 个整数的数组

    // 初始化数组元素
    for (int i = 0; i < 10; i++) {
        n[i] = i + 100; // 设置元素 i 为 i + 100
        cout << n[i] << endl;
    }
}
```

### 3.1.2 模板类vector动态数组

```c++
/**
有点类似于Java的ArrayList集合类

1.push_back 在数组的最后添加一个数据
2.pop_back 去掉数组的最后一个数据
3.at 得到编号位置的数据
4.begin 得到数组头的指针
5.end 得到数组的最后一个单元+1的指针
6．front 得到数组头的引用
7.back 得到数组的最后一个单元的引用
8.max_size 得到vector最大可以是多大
9.capacity 当前vector分配的大小
10.size 当前使用数据的大小
11.resize 改变当前使用数据的大小，如果它比当前使用的大，者填充默认值
12.reserve 改变当前vecotr所分配空间的大小
13.erase 删除指针指向的数据项
14.clear 清空当前的vector
15.rbegin 将vector反转后的开始指针返回(其实就是原来的end-1)
16.rend 将vector反转构的结束指针返回(其实就是原来的begin-1)
17.empty 判断vector是否为空
18.swap 与另一个vector交换数据
**/
#include <iostream>  //C++输入输出的库,没有.h后缀，与c的区别
#include <vector>  //vector的头文件

using namespace std;  //使用输入输出的命名空间

int main() {
    vector<int> obj; //创建一个向量存储容器 int
    for (int i = 0; i < 10; i++)  // push_back(elem)在数组最后添加数据
    {
        obj.push_back(i);
        cout << obj[i] << ",";
    }
    for (int i = 0; i < 5; i++)//去掉数组最后一个数据
    {
        obj.pop_back();
    }
    cout << "\n" << endl;
    for (int i = 0; i < obj.size(); i++) //size()容器中实际数据个数
    {
        cout << obj[i] << ",";
    }
    return 0;
}
```

### 3.1.3 模板类array固定数组（c++11）

```c++
#include <array>    //array类头文件

using namespace std;  //使用array需要包含该命名空间

int main() {
    array<int, 5> ai{};    // create array object of 5 ints
    array<double, 4> ad = {1.2, 2.1, 3.43, 4.3};    // 使用普通方式进行初始化
    array<double, 4> ad2{1.2, 2.1, 3.43, 4.3};    // 使用列表的方式进行初始化
}
```

# 四 数据类型（三）对象[重点]

## 4.1 类

```c++
/**
掌握目标：
1、构造函数/析构函数
2、复制构造函数
3、this指针
4、类指针
5、友元函数(有啥用？？？？)
6、内联函数
7、静态成员static关键字

//特殊成员变量初始化
常量变量：必须通过构造函数参数列表进行初始化。
引用变量：必须通过构造函数参数列表进行初始化。
普通静态变量：要在类外通过"::"初始化。
静态整型常量：可以直接在定义的时候初始化。
静态非整型常量：不能直接在定义的时候初始化。要在类外通过"::"初始化
**/
//头文件
#include <iostream>

#ifndef TWOC_PERSON_H
#define TWOC_PERSON_H

using namespace std;

class Person {
public:   //     公有的数据成员和成员函数
    static int count;   //记录构造函数次数,构造static变量

    Person();   //无参构造函数
    ~Person();  //析构函数，
    Person(string food);  //有参构造函数
    Person(string food, string time);

    Person(const Person &person);   //复制构造函数，复制对象用的,深拷贝和浅拷贝
    void eat();   //成员函数

    static int getCount();    //静态函数

private:   //私有的数据成员和成员函数
    string foodName;
    string currentTime;

protected:  //保护的数据成员和和成员函数
};
#endif //TWOC_PERSON_H

//实现文件
#include "Person.h"

int Person::count = 0;   // 初始化类 Box 的静态成员，其实是定义并初始化的过程(必须在类外进行)

void Person::eat() {
    cout << "我正在吃:" << foodName << endl;
}

//初始化列表来进行初始化数据,可以使用默认参数
Person::Person(string food, string time = "now") : foodName(food), currentTime(time) {
    count++;
}

Person::Person(const Person &person) {

}

Person::~Person() {
    cout << "~Person()" << endl;
}

Person::Person() {
    cout << "Person()" << endl;
}

int Person::getCount() {
    return count;
}

//调用
#include <iostream>
#include "Person.h"
#include <string>
int main(int argc, const char * argv[]) {

    
    Person *person1=new Person("汉堡包");   //堆上面分配内存
    person1->eat();
    delete person1;   //需要主动释放内存，会调用析构函数
    
    Person person("薯条");   //栈上面创建对象，程序结束会自动回收内存，然后自动调用析构函数
    person.eat();
    cout << "Total objects: " << Person::count << endl;        //输出2
    cout << "Total objects: " << Person::getCount() << endl;   //输出2

    return 0;
}
```

## 4.2 继承

```c++
/**
子类继承了父类所有方法（public和protected）下列除外
基类的构造函数、析构函数和拷贝构造函数。
基类的重载运算符。
基类的友元函数。
**/

//父类
#ifndef TWOC_SHAPE_H
#define TWOC_SHAPE_H
class Shape {
public:
    void setWidth(int w);

    void setHeight(int h);

protected:
    int width;
    int height;
};
#endif //TWOC_SHAPE_H

#include "Shape.h"

void Shape::setWidth(int w) {
    width = w;
}

void Shape::setHeight(int h) {
    height = h;
}

//子类
#ifndef TWOC_RECTANGLE_H
#define TWOC_RECTANGLE_H
#include "Shape.h"

class Rectangle : public Shape {

public:
    int getArea();
};
#endif //TWOC_RECTANGLE_H

#include "Rectangle.h"

int Rectangle::getArea() {
    return (width * height);
}

//main方法
#include <iostream>
#include "Rectangle.h"

using namespace std;

int main() {

    Rectangle Rect;

    Rect.setWidth(5);
    Rect.setHeight(7);
    cout << "Total area: " << Rect.getArea() << endl;   //输出35
    return 0;
}
```

## 4.3 运算符重载

```c++
/**
Box operator+(const Box&);  //成员函数定义
Box operator+(const Box&, const Box&);  //非成员函数定义

可重载的运算符
双目算术运算符	+ (加)，-(减)，*(乘)，/(除)，% (取模)
关系运算符	==(等于)，!= (不等于)，< (小于)，> (大于>，<=(小于等于)，>=(大于等于)
逻辑运算符	||(逻辑或)，&&(逻辑与)，!(逻辑非)
单目运算符	+ (正)，-(负)，*(指针)，&(取地址)
自增自减运算符	++(自增)，--(自减)
位运算符	| (按位或)，& (按位与)，~(按位取反)，^(按位异或),，<< (左移)，>>(右移)
赋值运算符	=, +=, -=, *=, /= , % = , &=, |=, ^=, <<=, >>=
空间申请与释放	new, delete, new[ ] , delete[]
其他运算符	()(函数调用)，->(成员访问)，,(逗号)，[](下标)
**/

#include <iostream>

using namespace std;

class Box {
public:

    double getVolume(void) {
        return length * breadth * height;
    }

    void setLength(double len) {
        length = len;
    }

    void setBreadth(double bre) {
        breadth = bre;
    }

    void setHeight(double hei) {
        height = hei;
    }

    // 重载 + 运算符，用于把两个 Box 对象相加
    Box operator+(const Box &b) {
        Box box;
        box.length = this->length + b.length;
        box.breadth = this->breadth + b.breadth;
        box.height = this->height + b.height;
        return box;
    }

private:
    double length;      // 长度
    double breadth;     // 宽度
    double height;      // 高度
};

// 程序的主函数
int main() {
    Box Box1;                // 声明 Box1，类型为 Box
    Box Box2;                // 声明 Box2，类型为 Box
    Box Box3;                // 声明 Box3，类型为 Box
    double volume = 0.0;     // 把体积存储在该变量中

    Box1.setLength(6.0);
    Box1.setBreadth(7.0);
    Box1.setHeight(5.0);

    Box2.setLength(12.0);
    Box2.setBreadth(13.0);
    Box2.setHeight(10.0);

    volume = Box1.getVolume();
    cout << "Volume of Box1 : " << volume << endl;  //输出210

    volume = Box2.getVolume();
    cout << "Volume of Box2 : " << volume << endl;  //输出1560

    Box3 = Box1 + Box2;    //使用重载运算符将两个对象相加,执行operator+方法
    volume = Box3.getVolume();
    cout << "Volume of Box3 : " << volume << endl;  //输出5400

    return 0;
}
```

## 4.4 多态

```c++
/**
虚函数：使用virtual关键字
静态链接和动态链接
**/
```

## 4.5 抽象和接口

```
/**
纯虚函数：  virtual double area() = 0;   //不定义任何方法体

抽象类：
其实，在c++中并没有抽象类的概念，要实现抽象类则需要通过纯虚函数实现。纯虚函数指的是只定义函数原型的成员函数。在c++的类中，只要存在纯虚函数，那么该类就变成抽象类。

 (1) 每个具体图形的求面积算法不一样，所以加上virtual关键字，表明该函数是虚函数，在子类中重写时可以发生多态； 
 (2) 为对Shape类求面积无意义，所以加上”= 0”表明该函数声明为纯虚函数，不需要定义函数体。 
 (3) 抽象类不能生成对象，只能用作父类被继承，子类必须实现纯虚函数的具体功能，在子类中，父类的纯虚函数被实现后就变成虚函数，当然，如果子类没有实现父类的纯虚函数，那么子类也是抽象类一个

接口：
c++中接口也是一种抽象类，需要满足： 
 (1) 类中没有定义任何成员变量 
 (2) 类中所有成员函数都是公有且都是纯虚函数
**/
```

# 五 高级

## 5.1 文件处理

## 5.2 模板

## 5.3 信号处理

## 5.4 多线程

