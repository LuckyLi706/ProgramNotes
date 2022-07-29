<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Python](#python)
  - [入门](#%E5%85%A5%E9%97%A8)
    - [pip](#pip)
    - [pipenv](#pipenv)
    - [异常](#%E5%BC%82%E5%B8%B8)
    - [包和模块](#%E5%8C%85%E5%92%8C%E6%A8%A1%E5%9D%97)
  - [数据类型](#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [常量](#%E5%B8%B8%E9%87%8F)
    - [type函数](#type%E5%87%BD%E6%95%B0)
    - [id函数](#id%E5%87%BD%E6%95%B0)
    - [isinstance函数](#isinstance%E5%87%BD%E6%95%B0)
    - [数字类型](#%E6%95%B0%E5%AD%97%E7%B1%BB%E5%9E%8B)
    - [布尔类型](#%E5%B8%83%E5%B0%94%E7%B1%BB%E5%9E%8B)
    - [字符串（str）](#%E5%AD%97%E7%AC%A6%E4%B8%B2str)
    - [列表（list）](#%E5%88%97%E8%A1%A8list)
    - [元组（tuple）](#%E5%85%83%E7%BB%84tuple)
    - [集合（set）](#%E9%9B%86%E5%90%88set)
    - [dict（字典）](#dict%E5%AD%97%E5%85%B8)
    - [值类型和引用类型](#%E5%80%BC%E7%B1%BB%E5%9E%8B%E5%92%8C%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8B)
  - [运算符](#%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [算数运算符](#%E7%AE%97%E6%95%B0%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [关系（比较）运算符](#%E5%85%B3%E7%B3%BB%E6%AF%94%E8%BE%83%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [逻辑运算符](#%E9%80%BB%E8%BE%91%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [成员运算符](#%E6%88%90%E5%91%98%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [身份运算符运算符](#%E8%BA%AB%E4%BB%BD%E8%BF%90%E7%AE%97%E7%AC%A6%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [位运算符](#%E4%BD%8D%E8%BF%90%E7%AE%97%E7%AC%A6)
  - [条件判断和循环](#%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD%E5%92%8C%E5%BE%AA%E7%8E%AF)
    - [条件判断](#%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD)
    - [循环](#%E5%BE%AA%E7%8E%AF)
  - [函数](#%E5%87%BD%E6%95%B0)
    - [定义](#%E5%AE%9A%E4%B9%89)
    - [参数](#%E5%8F%82%E6%95%B0)
    - [返回值](#%E8%BF%94%E5%9B%9E%E5%80%BC)
    - [作用域](#%E4%BD%9C%E7%94%A8%E5%9F%9F)
      - [局部变量和全局变量](#%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E5%92%8C%E5%85%A8%E5%B1%80%E5%8F%98%E9%87%8F)
      - [global关键字](#global%E5%85%B3%E9%94%AE%E5%AD%97)
  - [类和对象](#%E7%B1%BB%E5%92%8C%E5%AF%B9%E8%B1%A1)
    - [类的定义](#%E7%B1%BB%E7%9A%84%E5%AE%9A%E4%B9%89)
    - [构造函数](#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
    - [类变量和实例变量](#%E7%B1%BB%E5%8F%98%E9%87%8F%E5%92%8C%E5%AE%9E%E4%BE%8B%E5%8F%98%E9%87%8F)
    - [类方法](#%E7%B1%BB%E6%96%B9%E6%B3%95)
    - [静态方法](#%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95)
    - [可见性](#%E5%8F%AF%E8%A7%81%E6%80%A7)
    - [继承](#%E7%BB%A7%E6%89%BF)
    - [super关键字](#super%E5%85%B3%E9%94%AE%E5%AD%97)
    - [类的内置方法](#%E7%B1%BB%E7%9A%84%E5%86%85%E7%BD%AE%E6%96%B9%E6%B3%95)
  - [正则表达式](#%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [例子](#%E4%BE%8B%E5%AD%90)
    - [普通字符和元字符](#%E6%99%AE%E9%80%9A%E5%AD%97%E7%AC%A6%E5%92%8C%E5%85%83%E5%AD%97%E7%AC%A6)
    - [字符集](#%E5%AD%97%E7%AC%A6%E9%9B%86)
    - [数量词](#%E6%95%B0%E9%87%8F%E8%AF%8D)
    - [匹配0次1次或者无限多次](#%E5%8C%B9%E9%85%8D0%E6%AC%A11%E6%AC%A1%E6%88%96%E8%80%85%E6%97%A0%E9%99%90%E5%A4%9A%E6%AC%A1)
    - [边界匹配](#%E8%BE%B9%E7%95%8C%E5%8C%B9%E9%85%8D)
    - [组](#%E7%BB%84)
    - [匹配模式参数](#%E5%8C%B9%E9%85%8D%E6%A8%A1%E5%BC%8F%E5%8F%82%E6%95%B0)
    - [正则替换](#%E6%AD%A3%E5%88%99%E6%9B%BF%E6%8D%A2)
    - [match和search](#match%E5%92%8Csearch)
    - [group分组](#group%E5%88%86%E7%BB%84)
  - [json](#json)
  - [高级语法](#%E9%AB%98%E7%BA%A7%E8%AF%AD%E6%B3%95)
    - [枚举](#%E6%9E%9A%E4%B8%BE)
    - [闭包](#%E9%97%AD%E5%8C%85)
- [开源库](#%E5%BC%80%E6%BA%90%E5%BA%93)
  - [xlrd（操作Excel）](#xlrd%E6%93%8D%E4%BD%9Cexcel)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Python

+ [官方文档](https://docs.python.org/zh-cn/3/)

## 入门

```python
# 单行注释
"""
多行注释
"""
或者
'''
多行注释
'''

# python不需要使用使用分号结尾,需要注意代码之间的间距,不需要显示声明变量类型
print("Hello,World")   # 使用print输出内容


# py的main方法（只有作为主入口函数时执行,作为模块不会被执行该函数）
if __name__ == '__main__':
    print('main')

```

### pip

```python
pip freeze > <目录>/requirements.txt   //导出requirements.txt,requirements.txt文件包含了所有需要安装的依赖
pip install <包名> 或 pip install -r requirements.txt  //在线安装依赖
pip uninstall <包名> 或 pip uninstall -r requirements.txt //卸载依赖
pip install --upgrade package_name  升级依赖
pip install -U pip  //升级pip

国内镜像：
清华：https://pypi.tuna.tsinghua.edu.cn/simple
阿里云：https://mirrors.aliyun.com/pypi/simple/
豆瓣：https://pypi.doubanio.com/simple/
中国科学技术大学: http://pypi.mirrors.ustc.edu.cn/simple/

临时使用：
可以在使用pip的时候在后面加上-i参数，指定pip源
pip3 install -i https://pypi.doubanio.com/simple/ 包名    //使用镜像安装单个包
pip3 install  -r requirements.txt -i https://pypi.doubanio.com/simple/   //使用镜像安装requirements.txt包含的镜像

永久修改：
linux:
修改 ~/.pip/pip.conf (没有就创建一个)， 内容如下：
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

windows:
直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下:
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

//关于安装Python会在Python\Scripts目录下发现有三个pip开头的exe（pip、pip3和pip3.7）
如果同时装有 python2 和 python3
pip 默认给 python2 用。
pip3 指定给 python3 用。
如果同时安装多个3的版本的话，比如3.5 3.6 3.7。则用pip3明显不合适，这个时候就可以用pip+版本后缀来明确指出具体版本的pip了。
如果只装有 python3
```

### pipenv

```python
目的：
隔离不同项目不同的依赖版本
经典：隔离python2、python3的项目

安装：
pip install pipenv

与项目绑定：
pipenv install(在项目目录下安装虚拟环境)
pipenv shell(在项目目录进入虚拟环境)
pipenv install 包名(安装包)
```

### 异常

```python
# 异常捕捉
"""
try：
    语句块1
except：
    语句块2
"""

# 指定异常捕捉
"""
try：
    语句块1
except 异常类型：
    语句块2
"""

# 异常捕捉(try...except....else....finally)
"""
try：
    语句块1
except：
    语句块2
else：                   //对应语句块3在不发生异常是执行
    语句块3
finally：                //对应语句块4一定执行
    语句块4
"""
```

### 包和模块
+ 模块
  ```python
  # import 模块名   导入模块
  # import 模块 as 名字    导入模块并重命名模块名
  # from 模块 import 方法或者名  form import语句允许编写人员只导入模块的一部分（如方法和变量）
  ```
+ 包
  ```python
  # 要想包作为模块,在包下面必须创建__init__.py文件,然后就可以像模块那样导入了

  # 关于__init__.py文件
  # 导入包的时候__init__.py文件会自动被执行
  # 使用场景1,可以控制哪些模块可以被导出。可以使用__all__=[]
  # 使用场景2,可以对模块进行批量导出,避免重复导入
  ```

## 数据类型

### 常量
```python
# Python中不存在常量
# 但是有个约定的习惯,对于形式上面的常量,所有的都要大写
ACCOUNT = 'jacky'   # 定义一个形式上的常量
```

### type函数
```python
# 用于获取当前变量的类型
a = 10
type(a)
# 输出int
```

### id函数
```python
# 用于获取变量的内存地址
a = 10 
id(a)  # 输出内存地址
```

### isinstance函数
```python
# 用于判断变量属于哪种类型
a = 10 
isinstance(a,int)  # 输出True
```

### 数字类型
```python
# python里中用int表示整型,用float表示浮点型,只有这两种类型
a : int = 10 # 可以这样定义,但是python会自动推断该类型,所以可以省略变量类型

# /和//
a = 2/2  # /表述除。输出1.0,相除都会为浮点型float
a = 1//2 # //表示整除。输出0

# 二进制、八进制、十六进制表示方法
a = 0b10  # 前缀使用0b表示二进制
b = 0o10  # 前缀使用0o表示八进制
c = 0x10  # 前缀使用0x表示十六进制

# 进制间的转换
bin()  # 使用bin函数可以实现其他进制转换为二进制
int()  # 使用int函数可以实现其他进制转换为十进制
hex()  # 使用hex函数可以实现其他进制转换为十六进制
oct()  # 使用oct函数可以实现其他进制转换为八进制
```

### 布尔类型
```python
# python中布尔类型为bool,只有True和Flase两种,记住要大写,小写会报错
bool(1) # 输出True,不是0的数字类型都是True
bool(0) # 输出False,只有为0的数字类型是False

bool('abc') # 输出为True,不为空的字符串为True
bool('') # 输出为False,为空的字符串为False

# 还有其他类型,空值的情况下都会被认为为False（重要知识点）
bool(None)  # 也是为False
```

### 字符串（str）
```python
# python中字符串类型为str,可以使用单引号,双引号,三引号

# 为什么需要单引号和双引号两种,见如下例子：
a = "let's go"  # 输出let's go
b = 'let"s go'  # 输出let"s go

# ord函数（求对应ascii值）
ord('w')   # 输出119

# 三引号主要是为了多行字符串

# 转义字符（\n表示换行,\t表示横向制表符,\r表示回车）
a = 'let\'s go' # 输出let's go,也可以使用转移字符\来输出

# 原始字符串
a = r'let\ns go'  # 输出let\ns go,前面加个r,内部的转义字符不生效,作为原始字符串存在

# 字符串表达式
b = 10
print(f'Hi, {b}')  # 输出Hi, 10 ,使用{}包裹,里面可以是变量,可以是表达式,可以调用方法

# 字符串取值（切片）
a = 'Hello,World'
a[0]  # 输出H
a[-1]  # 输出d,表示从最后一个取
a[0:3]  # 输出Hel,表示取从第0到第二个2个字符
a[-5:-1] # 输出Worl,表示从第-5位置取到第-2个字符
a[6:]  # 输出Wrold,表示从第6位置到后面所有的字符

# 相关方法
"""
1. len(x)       长度，返回字符串x的长度
2. str(x)        将任意类型x转换为字符串形式
3. hex(x)或oct(x)  将整数x转换为十六进制或者八进制小写形式字符串
4. chr(x)       x为Unicode编码，返回其对应的字符
5. ord(x)       x为字符，返回其对应的Unicode编码
"""

# 常用函数
"""
1.str.lower()或str.upper()    返回字符串的副本，全部字符为小写或大写
2.str.split(sep=None)         返回一个列表，由sep的分割字符来处理
3.str.count(sub)                 返回字串sub在str中出现的次数
4.str.replace(old,new)        返回字符串str副本，所有old字串被替换为new
5.str.center(width,fillchar)  字符串根据width居中，fillchar可选，为剩余左右的空间由fillchar字符填充
6.str.strip(chars)                 去掉str字符串中其左侧和右侧chars中列出的所有字符
7.str.join(iter)                     在iter变量除最后一个元素外每个元素后增加一个str 
"""

# 字符串格式化
"我是字符串:{}".format("123")     # {}为槽，用format函数里面的数据代替
"{0:=^20}".format("PYTHON")    
#槽内可以添加类型，0:  表示引导符   ^为居中  还有<左对齐 >右对齐  20为槽设定的宽度   结果为=======PYTHON=======
```

### 列表（list）
```python
# python中列表类型为list,里面可以添加任意类型（列表是动态数组，它们可变且可以重设长度（改变其内部元素的个数））
a = [1,2,3,"22"] # 使用[]来表示列表

# 取值（类似于字符串）
a[0]  # 输出1
a[0:2] # 输出[1,2]
a[1:4:2]   # 输出[2,"22"]  #后面一个2表示步长

# 两个列表相加
b = [1,2]
a + b # 输出[1,2,3,"22",1,2]

# 乘法运算
b * 3  # [1,2,1,2,1,2]

# 相关方法
"""
1.ls[i]=x               //替换列表ls第i元素为x
2.ls[i:j:k]=lt          //用列表lt替换ls切片后所对应元素子列表
3.del ls[i]             //删除列表ls中第i元素
4.del ls[i:j:k]         //删除列表ls中第i到j以k为步长的元素
5.ls+=lt               //更新列表ls，将列表lt元素增加到列表ls中
"""

# 常用函数
"""
1.ls.append(x)      //在列表ls最后增加一个元素x
2.ls.clear()            //删除列表ls中所有元素
3.ls.copy()            //生成一个新列表
4.ls.insert(i,x)        //在列表ls的第i位置增加元素x
5.ls.pop(i)             //在列表ls中第i位置取出并删除该元素
6.ls.remove(x)       //将列表ls中出现的第一个元素x删除
7.ls.reverse()         //将列表ls中的元素反转
"""
```

### 元组（tuple）
```python
# python中列表类型为tupe,里面可以添加任意类型（元组是静态数组，它们不可变，且其内部数据一旦创建便无法改变）
a = (1,2,3)  # 使用()来表示元组

# 除了可变性,其他和列表差不多
```

### 集合（set）
```python
# python中集合类型为set,集合是无序的（所以不可以使用下标获取值）,并且不重复
a = {1,2,3}  # 使用{}来表示集合

# 定义空集合
a = set{}   # 不能单独使用{},前面不加set表示字典dict

# 获取长度
len(a)   # 输出3

# 求差集
b = {2}
a - b  # 输出{1,3}

# 求交集
b = {2}
a & b  # 输出{2}

# 求合集
b = {2,4}
a | b # 输出{1,2,3,4}

# 常用函数
"""
1.S.add(x)      //如果x不在集合S中，将x增加到S
2.S.discard(x) //移除S中元素x，如果x不在集合S中，不报错
3.S.remove(x) //移除S中元素x，如果x不在集合S中，产生KeyError异常
4.S.clear()       //移除S中所有元素
5.S.pop()        //随机取出S的元素，更新S，如S为空产生KeyError异常
6.S.copy()       //返回集合S的一个副本
7.len(S)          //返回集合S的元素个数
8.x in S          //判断S中元素x，x在集合S中，返回True，否则返回False
9.set(x)          //将其他类型变量x转变为集合类型
"""
```

### dict（字典）
```python
# python中字典类型为dict
a = {'a':1,'b':2,'c':3}  # 使用{}来表示字典,与集合的区别在于里面的数据是以key:value存在的

# key和value（key必须是不可变类型,value可以是任意类型）

# 取值
a['a']  # 输出1

# 相关函数
"""
1.del d[k]        //删除字典d中键k所对应的数据值
2.k in d           //判断键k是否在字典d中，在返回True
3.d.keys()        //返回字典d中所有的键信息
4.d.values()     //返回字典d中所有的值信息
5.d.items()      //返回字典中所有的键值对信息
6.d.get(k,default)  // 键k存在，则返回对应值，不存在则返回default
7.d.pop(k,default)  // 键k存在，则取出对应值，不存在则返回default
8.d.popitem()        //随机从字典d中取出一个键值对，以元祖形式返回
9.d.clear()             //删除所有的键值对
10.len(d)              //返回字典d中的元素个数
"""
```

### 值类型和引用类型
```python
# int str tuple (不可变,是值类型)
# list tuple dict (可变,是引用类型)
```

## 运算符
### 算数运算符
```python
# +(加法)、-(减法)、*(乘法)、/(除法)、//(整除)、%(求余)、**(求幂次方)

a = 10
a ** 3   # 输出100,表示10*10*10

# python中不支持自增,自减的,不支持a++或者a--
```
### 关系（比较）运算符
```python
# ==、!=、>、<、>=、<=
```

### 逻辑运算符
```python
# and(或)、or(且)、not(非)
```

### 成员运算符
```python
# in、not in（用于判断该元素是否在另一组元素的里面）
a = [1,2,3,4]
1 in a  # 输出True
```

### 身份运算符运算符
```python
# is、is not（用于判断该元素是否在另一组元素的里面）
# 如果两个变量取值相同,则is运算符返回True
# 比较的是内存地址
a = 10
a is int  # 输出False
type(a) is int # 输出True
b = 10
a is b # 输出True
```

### 位运算符
```python
# &(按位与)、|(按位或)、^(按位异或)、~(按位取反)、<<(左移)、>>(右移)
```

## 条件判断和循环

### 条件判断

```python
# python中不存在switch语法

# 单分支
"""
单分支：
if 条件 ：
     语句1
"""

# 二分支结构
"""
if 条件 ：
      语句1
else ：
      语句2

表达式1  if  条件  else  表达式2
"""

# 多分支结构
"""
if  条件1：
      语句1
elif 条件2:
      语句2
else：
      语句块3
"""

# 条件组合
"""
1.x and y     两个条件x和y的逻辑与
2.x  or  y      两个条件x和y的逻辑或
3.not x         条件x的逻辑非
"""
```

### 循环

```python
# for循环
"""
for  循环变量  in  遍历结构：
          语句块

计数循环
for  i  in  range(N)：           //循环0到N-1的次数
for  i  in  range(M,N,K)：    //循环M到N-1步长为K的次数
字符串遍历循环
for  c  in  s：                      //从s字符串中逐一取出字符c
列表遍历循环
for  item  in  ls：                //从列表ls中逐一取出元素item
文件遍历
for  line  in  fi：                  //遍历文件fi的每一行
"""   

# 无限循环：
"""
while  条件：
           语句块
"""

# break         跳出并结束当前整个循环执行循环后的语句
# continue    结束当次循环，执行接下来的次数

# 扩展：以下代码当循环没有被break语句退出时，执行else语句块
"""
1.for  循环变量  in  遍历结构：
          语句块1
   else：
          语句块2
2.while  条件：
           语句块1
   else：
           语句块2
"""
```

## 函数
Python一切皆对象,函数也是对象,是function类型

### 定义
```python
"""
def  函数名(参数0个或多个)：
          函数体
          return 返回值
"""
```

### 参数 
```python
# 可选参数放在确定参数后面(默认参数)
"""
如  def  average(a,b=3)
            函数体
            return 返回值
"""

# 可变参数传递 
"""
如  def  average(a,*b)             //*b表示可以有多个参数,实际为一个元组
            函数体
            return 返回值
"""

# 可变关键字参数传递 
"""
如  def  average(a,**b)             //*b表示可以有多个参数,实际一个字典
            函数体
            return 返回值
"""
```
### 返回值
```python
# 返回多个结果
"""
如 def  average(a,b=3)
            函数体
            return c,d,e   //返回的实际为一个元组
"""

# 返回多个结果时可以使用序列解包
c,d,e = averge(1,2)   # 返回值c,d,e对应给的参数c,d,e。使用有意义的变量名称接收函数返回值。避免使用元组的序号来使用。
```

### 作用域
#### 局部变量和全局变量
```python
"""
1.函数内部的变量名如果第一次出现，且出现在=前面，即被视为定义了一个局部变量，不管全局域中有没有该变量名，函数中使用的将是局部变量。(即声明了一个新的局部变量。如果这个变量名字和全部变量名字相同，那么局部变量名字会覆盖全局变量名字。

2.如果局部变量用到了一个变量。该变量是全局存在的，但是局部并没有声明这么一个变量。那么此时参与运算的是全局变量。但是这个参与运算是不能被赋值的，因为你赋值的时候按照python的语法那就是新生成一个局部变量，而且你在右侧使用的话。那就是会报错。

3.如果你想在局部变量修改全局变量。因为本身是不能的，你修改然后赋值的时候会出现矛盾。即你涉及到赋值var = xxx 修改的时候，那么会被语法解析会声明一个新的局部变量var。当然对象类型除外，你可以直接操作他的元素。
"""
```
#### global关键字
```python
# 使用global关键字升级为全局变量
a = 0
b = []


def print_hi():
    global a      # 升级为全局变量（可以对其进行更改）
    a = a + 1     # 现在可以对其进行加操作赋值运算了
    b.append("1")  # 这个只是调用列表的append方法
    print(a, b)


def print_h2():
    global a    # 升级为全局变量（可以对其进行更改）
    a = a + 1   # 现在可以对其进行加操作赋值运算了
    b.append("2")  # 这个只是调用列表的append方法
    print(a, b)


# Press the green button in the gutter to run the script.
if __name__ == '__main__':
    print_hi()     # 输出 1 ['1']
    print_h2()     # 输出 2 ['1', '2']
```

## 类和对象

### 类的定义
```python
# 定义类
class Student():
    name = ''
    age = 0

    # 方法必须self
    def print_file(self):  
        # 方法里面使用全局变量必须要使用self来调用
        print('name :' + self.name)  
        print('age ：'+str(self.age))

# 调用
student = Student()   # 实例化类
student.print_file()  # 调用方法
```

### 构造函数
```python
class Student:
    name = ''
    age = 0

    # 构造函数初始化
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # 定义实例方法时,self必须显示的定义在方法列表里面,调用的时候不需要传入这个参数
    def print_file(self):
        # 方法里面使用全局变量必须要使用self来调用
        print('name :' + self.name)
        print('age ：' + str(self.age))

# 调用
if __name__ == '__main__':
    student = Student("jacky", 17)
    student.print_file()  # 打印name : jacky  age : 17
```

### 类变量和实例变量
```python
class Student:
    # 下面定义的两个变量叫做类变量（和其他语言不同,其他语言在这边定义的都叫实例变量,有点类似于java中static修饰的变量）
    name = 'one'
    age = 0

    # 构造函数初始化
    def __init__(self, name, age):
        # 下面使用self修饰的才是实例变量
        self.name = name
        self.age = age
        # 想访问类变量(下面两种方式都行)
        print(Student.name)
        print(self.__class__.name)

    # 定义实例方法时,self必须显示的定义在方法列表里面,调用的时候不需要传入这个参数
    def print_file(self):
        # 方法里面使用全局变量必须要使用self来调用
        print('name :' + self.name)
        print('age ：' + str(self.age))

# 调用
student = Student("jacky", 17)  # 输出one one
print(student.name)  # 输出jacky
print(Student.name)  # 输出 one

# 内置函数__dict__（打印对象的字典）
print(student.__dict__) # 输出 {'name': 'jacky', 'age': 17}
print(Stduent.__dict__) # 打印类的字典。
```

### 类方法
```python
class Student:
    sum = 0

    # 方法必须self
    def __init__(self):
        # 在实例方法中使用类变量
        self.__class__.sum = self.__class__.sum + 1
        print(Student.sum)

    # 下面是定义类方法的方式(cls参数是必须的)
    @classmethod
    def do_homework(cls):
        cls.sum = cls.sum + 1
        print(cls.sum)

# 调用
student = Student()
student2 = Student()
student3 = Student()
# 调用（可以使用对象点方法也可以使用类的点方法）
Student.do_homework()
# 输出 1 2 3 4
```

### 静态方法
```python
class Student:
    # 下面的定义类的静态方法 （入参不需要self或者cls）
    @staticmethod
    def add(a, b):
        return a + b

# 调用（可以使用对象点方法也可以使用类的点方法）
student = Student()
print(student.add(1, 2))  # 输出3
print(Student.add(2, 3))  # 输出5
```

### 可见性
```python
class Student:
    __a = 10   # 对于变量前面加两个下划线表示私有

    # 对于构造方法,python认为前面和后面都有下划线的也是公开的
    def __init__(self):
        pass
    # 对于方法前面加两个下划线表示私有
    def __add(self, b):
        pass
```

### 继承
```python
class People:
    pass


class Student(People):  # 继承People类
    pass
```

### super关键字

### 类的内置方法
```python
# 类的专有方法：（可以实现运算符充载）
__init__  # 构造函数，在生成对象时调用
__del__ # 析构函数，释放对象时使用
__repr__ # 打印，转换
__setitem__ # 按照索引赋值
__getitem__ # 按照索引获取值
__len__ # 获得长度
__cmp__ # 比较运算
__call__ # 函数调用
__add__ # 加运算
__sub__ # 减运算
__mul__ # 乘运算
__truediv__ # 除运算
__mod__  # 求余运算
__pow__ # 乘方
```

## 正则表达式

### 例子
```python
import re   # 导入re使用正则表达式

if __name__ == '__main__':
    # 字符串中是否存在Python
    a = 'Java|Python|C++|C'
    print(re.findall('Python', a))  # 返回列表['Python'],如果不存在返回空列表
```

### 普通字符和元字符
```python
import re

if __name__ == '__main__':
    # 找出字符串中所有的数字
    a = '1Java2|Python|3C++|4C'
    # \\d表示匹配所有的数字  \\D表示匹配所有的非数字 
    # \\w表示匹配所有数字和字母 \\W表示匹配所有非数字非字母的字符
    # \s 表示匹配所有空白字符  \\S表示匹配所有非空白字符的字符
    # . 匹配除换行符\n之外其他所有字符
    print(re.findall('\\d', a)) # 返回列表[1,2,3,4],没有则返回空列表

# 正则表达式是一个特殊的字符序列（由普通字符或者元字符或者普通字符和元字符组合而成的）
# 第一个例子中'Python'叫普通字符
# 当前例子中'\\d'叫元字符
```

### 字符集
```python
import re

if __name__ == '__main__':
    a = 'abc,acd,acc,afd'
    # []字符集是针对[]里面的每个字符进行匹配,如果前面加上^表示不匹配该字符
    # 匹配所有数字也可以使用[0-9] 对应元字符\\d
    # 匹配字母也可以使用[A-Za-z]  对应元字符\\D
    # 匹配字母和数字可以使用[A-Za-z0-9] 对应元字符\\w
    print(re.findall('a[cf]d', a))   # 左右两边使用a和d限制,中间匹配c或者f
    print(re.findall('a[^c]d', a))   # 左右两边使用a和d限制,中间不匹配c
```

### 数量词
```python
import re

if __name__ == '__main__':
    # 匹配出词组python、java、php
    a = 'python 23java33php'
    # [a-z]{3,6}表示匹配的字符个数是最小3个到最大6个,python最大是6个字符,php最小是3个字符
    print(re.findall('[a-z]{3,6}', a)) # 当前匹配模式贪婪模式
```

### 匹配0次1次或者无限多次
```python
import re

if __name__ == '__main__':
    a = 'pytho222python333pythonn444' 
    # 这里的匹配次数是针对某个字符来说的
    print(re.findall('python*', a))  #  *匹配0次或者无限多次 输出['pytho', 'python', 'pythonn']
    print(re.findall('python+', a))  #  +匹配1次或者无限多次 输出['python', 'pythonn']
    print(re.findall('python?', a))  #  ?匹配0次或者1次     输出['pytho', 'python', 'pythonn']
```

### 边界匹配
```python
import re

if __name__ == '__main__':
    a = '10000000001'
    print(re.findall('^000', a))    # ^表示从字符串开始进行匹配 输出[]
    print(re.findall('000$', a))    # $表示从字符串结束进行匹配 输出[]
    print(re.findall('^000$', a))   # 表示从字符串开始和结束匹配
```

### 组
```python
import re

if __name__ == '__main__':
    a = 'PythonPythonPythonPython'
    # ()是一个且关系,必须要包含里面所有的字符,形成一个组
    print(re.findall('(Python){4}', a))  # 匹配字符串是否存在连续的4个Python,返回['Python']
```

### 匹配模式参数
```python
import re

if __name__ == '__main__':
    a = 'phpC#java'
    print(re.findall('c#', a, re.I))  # 第三个参数是匹配模式
```

### 正则替换
```python
import re

if __name__ == '__main__':
    a = 'phpC#javaC#'
    # 第一个参数正则,第二个参数替换后的字符,第三个参数原始字符串,count默认为0（替换所有匹配的）,1表示替换1次,依此类推
    r = re.sub('C#', 'C', a, count=1)
    print(r)

# 使用函数作为参数
import re


def replace(value):
    matched = value.group()
    return "!!" + matched + "!!"


if __name__ == '__main__':
    a = 'phpC#javaC#'
    # 第二个参数选择函数作为入参
    r = re.sub('C#', replace, a, count=1)
    print(r)
```

### match和search
```python
# re.match()   从第一个字符开始匹配,不匹配立马返回None（只会匹配一次）
# re.search()  从整个字符串搜索,只要有匹配的立马返回（只会匹配一次）
```

### group分组
```python
import re

if __name__ == '__main__':
    a = '***https://www.baidu.com/...'
    # 匹配https链接
    r = re.search('https.*/', a)
    print(r.group())  # 输出'https://www.baidu.com/'

if __name__ == '__main__':
    a = '***https://www.baidu.com/...'
    r = re.search('https(.*)/', a)   # 将中间的数据作为一个组
    print(r.group(1))    # 输出 ://www.baidu.com  group(0)返回的始终的是这个结果,group(1)返回第一个分组
```

## json

```python
import json

if __name__ == '__main__':
    json_str_load = '{"name":"jacky","age":2}'
    json_load = json.loads(json_str_load)   # 将json字符串转换成json

    json_dump = {"name": "jacky", "age": 10}
    json_str_dump = json.dumps(json_dump)  # 将json转换为json字符串
    print(type(json_load))   # 输出<class 'dict'>
    print(type(json_str_dump)) # 输出<class 'str'>
```

## 高级语法

### 枚举
```python
from enum import Enum

# 定义枚举类,必须要继承Enum
# 枚举里面的定义建议大写
class VIP(Enum):
    YELLOW = 1
    # 这个会被看作是YELLOW的别名,遍历时不会被打印出来
    YELLOW = 1
    GREEN = 2
    BLACK = 3
    RED = 4


if __name__ == '__main__':
    VIP.RED = 3  # 这样会报错
    print(VIP.YELLOW.value)   # 输出1
    print(VIP.YELLOW)  # 输出VIP.YELLOW（这是enum类型）
    print(VIP.YELLOW.name)  # YELLOW（这是str类型）
    print(VIP['YELLOW'])  # 输出VIP.YELLOW
    print(VIP(1))  # 枚举的数据转换,输出VIP.YELLOW


# 限制枚举不能取相同值
from enum import IntEnum, unique

@unique
class VIP(IntEnum):
    YELLOW = 1
    GREEN = 2
    BLACK = 3
    RED = 3   # 这边会报错
```

### 闭包
```python
# 闭包 = 函数 + 环境变量
def curve_pre():
    a = 25   # 这个定义在curve的外部,不能是全局变量

    def curve(x):
        return a * x * x

    return curve


if __name__ == '__main__':
    f = curve_pre()
    print(f.__closure__)    # 打印他的闭包
    print(f.__closure__[0].cell_contents)  # 打印他的参数 输出25
    print(f(2))  # 输出100

# 一个小案例
origin = 0


# 非闭包实现
def go(step):
    global origin
    origin = origin + step
    return origin


# 闭包实现（可以不使用全局变量）
def go_2(pos):
    def go_step(step):
        nonlocal pos
        new_pos = pos + step
        pos = new_pos
        return pos

    return go_step


if __name__ == '__main__':
    f = go_2(origin)
    print(f(2))
    print(f(3))
    print(f(5))
```

# 开源库

## xlrd（操作Excel）

```python
# 读取Excel
# This is a sample Python script.
import xlrd


# Press ⌃R to execute it or replace it with your code.
# Press Double ⇧ to search everywhere for classes, files, tool windows, actions, and settings.


def read_excel():
    try:
        # 读取文件
        workbook = xlrd.open_workbook(r'/Users/lijie/Desktop/迁钢气体探测项目车载数据记录（车载1114）.xl')
        # 读取所有sheets
        sheets = workbook.sheet_names()
        print("所有sheet：" + "".join(sheets))

        # 根据sheet索引或者名称获取sheet内容
        sheet1 = workbook.sheet_by_name('Sheet1')

        # 总的行数
        rows_num = sheet1.nrows
        # 总的列数
        cols_num = sheet1.ncols
        # 行数，列数
        print("总行数：" + str(rows_num) + "," + "总列数：" + str(cols_num))

        for i in range(rows_num):
            for j in range(cols_num):
                # 获取单元格的值
                cell_value = sheet1.cell(i, j)
                if str(cell_value.value).strip() != '':
                    if str(cell_value.value) == 'PM2.5':
                        '''
                        如果i=2,j=3
                        数据从行数第三行开始算起，列数不变，直到最后一行
                        '''
                        # row = i + 1
                        for row in range(i + 1, rows_num):
                            print(sheet1.cell_value(row, j))
    except Exception as e:
        print("发生异常：" + str(e))
    pass


# Press the green button in the gutter to run the script.
if __name__ == '__main__':
    read_excel()
```

