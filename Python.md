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

## 数据类型

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
"""
单分支：
1.if 条件 ：
     语句1
     
二分支结构：
1.if 条件 ：
      语句1
   else ：
      语句2
2.表达式1  if  条件  else  表达式2

多分支结构：
1.if  条件1：
      语句1
  elif 条件2:
      语句2
   else：
      语句块3
      
条件组合：
1.x and y     两个条件x和y的逻辑与
2.x  or  y      两个条件x和y的逻辑或
3.not x         条件x的逻辑非
"""
```

### 循环

```python
"""
遍历循环：
1.for  循环变量  in  遍历结构：
          语句块
2.应用：
   计数循环
   for  i  in  range(N)：           //循环0到N-1的次数
   for  i  in  range(M,N,K)：    //循环M到N-1步长为K的次数
   字符串遍历循环
   for  c  in  s：                      //从s字符串中逐一取出字符c
   列表遍历循环
   for  item  in  ls：                //从列表ls中逐一取出元素item
   文件遍历
   for  line  in  fi：                  //遍历文件fi的每一行
   
无限循环：
while  条件：
           语句块
           
关键字：
1.break         //跳出并结束当前整个循环执行循环后的语句
2.continue    //结束当次循环，执行接下来的次数

扩展：
1.for  循环变量  in  遍历结构：
          语句块1
   else：
          语句块2
2.while  条件：
           语句块1
   else：
           语句块2
//以上当循环没有被break语句退出时，执行else语句块
"""
```


## 1.5、异常捕捉

```python
"""
1.try：
       语句块1
   except：
       语句块2
2.try：
       语句块1
   except 异常类型：   //捕获指定异常
       语句块2
3.try：
       语句块1
   except：
       语句块2
    else：                   //对应语句块3在不发生异常是执行
        语句块3
    finally：                //对应语句块4一定执行
         语句块4
"""
```

# 二 数据类型

python不需要显示声明类型，语法：变量名=变量值

## 2.1、整型

```python
'''
1.十进制
2.二级制，以0b或0B开头
3.八进制，以0o或0O开头
4.十六进制，以0x或0X开头
'''

a = 5
c = a + 10
print(c)   //结果为15
```

## 2.2、浮点型

```python
"""
2/2结果为1.0
1.浮点数间运算存在不确定尾数，不是bug
0.1+0.2=0.30000004   
0.1+0.2==0.3   False
2.round(0.1+0.2) ==0.3 True
round(x,d):对x四舍五入，d是小数截取位数
3.科学计数法
4.3e-3  值为0.0043   9.6E5 值为960000.0
"""
```

## 2.3、复数型

```python
"""
z=bj-a   a为实部，b为虚部
"""
```

## 2.4、字符串

```python
"""
表示方法：
1、单引号或者双引号
表示单行字符串
2、三单引号或者三双引号
表示多行字符串
3、字符串中要存在单引号或者双引号字符
双引号在最外层表示，单引号在内部表示字符。反之亦然。
4、字符串中要即存在单引号和双引号字符
则使用三单引号或者三双引号表示

序号：
1、正向递增序号
0 1 2 3 4 5
2、反向递减序号
-6 -5 -4 -3 -2 -1

基本操作：
1、索引
返回字符串中单个字符
str[0]="1"
2、切片
str[:3]="012" 最开始到第三个数为止
str[-2:]="56" 最后面到第-2个数为止
str[1:5:2]="24" 第一个数到第五个数步长为2的那几个数
str[::-2]="531" 最开始到结尾步长为2的数逆序取出

特殊字符：
1、\b 回退
2、\n 换行
3、\r 回车

操作符
1、 x+y          连接两个字符串
2、 n*x或x*n  复制n次字符串
3、 x in s       如果x是s的字串，返回True，否则返回False
"""
d = "abc"    #使用双引号表示字符串
e = 'acd'    #使用单引号表示字符串
f = '''      #使用三单引号输出多行字符串 
1111
1222
444
'''
print(d)
print(e)
print(f)

输出：
abc
acd

1111
1222
444
```

### 2.4.1、常用函数

```python
"""
1. len(x)       长度，返回字符串x的长度
2. str(x)        将任意类型x转换为字符串形式
3. hex(x)或oct(x)  将整数x转换为十六进制或者八进制小写形式字符串
4. chr(x)       x为Unicode编码，返回其对应的字符
5. ord(x)       x为字符，返回其对应的Unicode编码
"""
```

### 2.4.2、常用方法

```python
"""
1.str.lower()或str.upper()    返回字符串的副本，全部字符为小写或大写
2.str.split(sep=None)         返回一个列表，由sep的分割字符来处理
3.str.count(sub)                 返回字串sub在str中出现的次数
4.str.replace(old,new)        返回字符串str副本，所有old字串被替换为new
5.str.center(width,fillchar)  字符串根据width居中，fillchar可选，为剩余左右的空间由fillchar字符填充
6.str.strip(chars)                 去掉str字符串中其左侧和右侧chars中列出的所有字符
7.str.join(iter)                     在iter变量除最后一个元素外每个元素后增加一个str 
"""
```

### 2.4.3、格式化

```python
"我是字符串:{}".format("123")      {}为槽，用format函数里面的数据代替
"{0:=^20}".format("PYTHON")    槽内可以添加类型，0:  表示引导符   ^为居中  还有<左对齐 >右对齐  20为槽设定的宽度   结果为=======PYTHON=======
```

## 2.5、集合

### 2.5.1、集合的定义
1. 集合元素之间无序，每个元素唯一，不存在相同元素
2. 集合元素不可更改，不能是可变数据类型
3. 集合用大括号{}表示，元素间用逗号分隔
4. 建立集合类型用{}或set()
5. 建立空集合类型，必须使用set()，不能使用大括号，保留给字典类型

### 2.5.2、集合操作符
```
1.S|T      //返回一个新的集合，包括在集合S和T中的所有元素
2.S-T     //返回一个新集合，包括在集合S但不在T中的元素
3.S&T   //返回一个新集合，包括同时在集合S和T中的元素
4.S^T   //返回一个新集合，包括集合S和T中的非相同元素
5.增强操作符
   1.S|=T      //更新集合S，包括在集合S和T中的所有元素
   2.S-=T     //更新集合S，包括在集合S但不在T中的元素
   3.S&=T   //更新集合S，包括同时在集合S和T中的元素
   4.S^=T   //更新集合S，包括集合S和T中的非相同元素
```

### 2.5.3、集合处理方法
```
1.S.add(x)      //如果x不在集合S中，将x增加到S
2.S.discard(x) //移除S中元素x，如果x不在集合S中，不报错
3.S.remove(x) //移除S中元素x，如果x不在集合S中，产生KeyError异常
4.S.clear()       //移除S中所有元素
5.S.pop()        //随机取出S的元素，更新S，如S为空产生KeyError异常
6.S.copy()       //返回集合S的一个副本
7.len(S)          //返回集合S的元素个数
8.x in S          //判断S中元素x，x在集合S中，返回True，否则返回False
9.set(x)          //将其他类型变量x转变为集合类型
```
### 2.5.4、序列类型的定义
```
1.序列是具有先后关系的一组元素
2.元素可以相同，类型可以不同
3.分类：字符串类型、元祖类型、列表类型
```
### 2.5.5、元祖类型定义
```
1.元祖是一种序列类型，一旦被创建就不能被修改
2.使用小括号()或tuple()创建，元素间用逗号分隔
3.可以使用或不使用小括号
```
### 2.5.6、列表类型
```
1.列表是一种序列类型，创建后可以随意被修改
2.使用方括号[]或list()创建，元素间用逗号分隔
```

#### 2.5.6.1、列表类型操作函数
```python
1.ls[i]=x               //替换列表ls第i元素为x
2.ls[i:j:k]=lt          //用列表lt替换ls切片后所对应元素子列表
3.del ls[i]             //删除列表ls中第i元素
4.del ls[i:j:k]         //删除列表ls中第i到j以k为步长的元素
5.ls+=lt               //更新列表ls，将列表lt元素增加到列表ls中
```

#### 2.5.6.2、列表类型方法
```python
1.ls.append(x)      //在列表ls最后增加一个元素x
2.ls.clear()            //删除列表ls中所有元素
3.ls.copy()            //生成一个新列表
4.ls.insert(i,x)        //在列表ls的第i位置增加元素x
5.ls.pop(i)             //在列表ls中第i位置取出并删除该元素
6.ls.remove(x)       //将列表ls中出现的第一个元素x删除
7.ls.reverse()         //将列表ls中的元素反转
```

### 2.5.7、字典类型
```python
1.键值对：键是数据索引的扩展
2.字典是键值对的集合，键值对之间无序
3.采用大括号{}和dict()创建，键值对用冒号表示
```

#### 2.5.7.1、字典类型操作函数和方法
```python
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
```

# 三 函数(Python一切皆对象,函数也是对象,是function类型)

## 3.1、函数的定义
```python
1.def  函数名(参数0个或多个)：
          函数体
          return 返回值
```
## 3.2、函数的参数 
```python
1.可选参数放在确定参数后面(默认参数)
如  def  average(a,b=3)
            函数体
            return 返回值
2.可变参数传递 
如  def  average(a,*b)             //*b表示可以有多个参数,实际为一个元组
            函数体
            return 返回值
3.可变关键字参数传递 
如  def  average(a,**b)             //*b表示可以有多个参数,实际一个字典
            函数体
            return 返回值
```
## 3.3、函数的返回值
```python
1.返回多个结果
如 def  average(a,b=3)
            函数体
            return c,d,e   //返回的实际为一个元组
```

## 3.4、作用域
### 3.4.1、局部变量和全局变量
```python
1.函数内部的变量名如果第一次出现，且出现在=前面，即被视为定义了一个局部变量，不管全局域中有没有该变量名，函数中使用的将是局部变量。(即声明了一个新的局部变量。如果这个变量名字和全部变量名字相同，那么局部变量名字会覆盖全局变量名字。
2.如果局部变量用到了一个变量。该变量是全局存在的，但是局部并没有声明这么一个变量。那么此时参与运算的是全局变量。但是这个参与运算是不能被赋值的，因为你赋值的时候按照python的语法那就是新生成一个局部变量，而且你在右侧使用的话。那就是会报错。
3.如果你想在局部变量修改全局变量。因为本身是不能的，你修改然后赋值的时候会出现矛盾。即你涉及到赋值var = xxx 修改的时候，那么会被语法解析会声明一个新的局部变量var。当然对象类型除外，你可以直接操作他的元素。
```
### 3.4.2、总结
```python
1.如果不是明显要局部变量和全局变量纠缠 能不纠缠就不纠缠。也就是定义变量名字的时候 要严格规范。按照开发规范来定义名字。全局大写或者加上“_”开头 这是避免不必要问题的根本 消灭问题
2.如果实在是场景需求,使用global关键字修饰局部变量,可以在外部访问局部变量。
```

# 四 面向对象

```python
#!/usr/bin/python3
"""
__ 符号来表示私有，没有的全是公共方法
@staticmethod 用 @staticmethod 装饰的不带 self 参数的方法叫做静态方法，类的静态方法可以没有参数，可以直接使用类名调用。
@classmethod 用 @staticmethod 装饰的默认有个 cls 参数，可以被类和对象调用。

类的专有方法：（可以实现运算符充载）
__init__ : 构造函数，在生成对象时调用
__del__ : 析构函数，释放对象时使用
__repr__ : 打印，转换
__setitem__ : 按照索引赋值
__getitem__: 按照索引获取值
__len__: 获得长度
__cmp__: 比较运算
__call__: 函数调用
__add__: 加运算
__sub__: 减运算
__mul__: 乘运算
__truediv__: 除运算
__mod__: 求余运算
__pow__: 乘方
"""


# 类定义
class People:
    # 定义基本属性
    name = ''
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁。" % (self.name, self.age))


# 单继承示例,Student继承与People
class Student(People):
    grade = ''

    def __init__(self, n, a, w, g):
        # 调用父类的构函
        People.__init__(self, n, a, w)
        self.grade = g

    # 覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))
        self.__laugh()  # 内部调用私有方法

    def __laugh(self):  # 定义私有方法,外部不能调用
        print("happy")

    @staticmethod
    def fun():
        print('静态方法')

    @classmethod
    def a(cls):
        print('类方法')


# 实例化类
p = People('runoob', 10, 30)
p.speak()
s = Student('ken', 10, 60, 3)
s.speak()
Student.fun()
Student.a()
```

# 五 第三方库

## 操作Excel

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

