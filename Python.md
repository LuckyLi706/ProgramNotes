# 一 基础

## 1.1、输出

```python
"""
注释：
1、单行注释，#注释内容
2、多行注释

"""
注释内容
"""

或者

'''
注释内容
'''

python不需要使用使用分号结尾,需要注意代码之间的间距
"""
print("Hello,World")
```

## 1.2、pip介绍

```python
pip freeze > <目录>/requirements.txt   //导出requirements.txt,requirements.txt文件包含了所有需要安装的依赖
pip install <包名> 或 pip install -r requirements.txt  //在线安装依赖
pip uninstall <包名> 或 pip uninstall -r requirements.txt //卸载依赖
pip install --upgrade package_name  升级依赖
pip install -U pip  //升级pip
```

## 1.3、pipenv介绍

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

## 1.4、条件判断和循环

### 1.4.1、条件判断

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

### 1.4.2、循环

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

