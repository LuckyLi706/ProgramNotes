<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Make](#make)
  - [推荐学习](#%E6%8E%A8%E8%8D%90%E5%AD%A6%E4%B9%A0)
  - [什么是make](#%E4%BB%80%E4%B9%88%E6%98%AFmake)
  - [Makefile语法](#makefile%E8%AF%AD%E6%B3%95)
    - [基本格式](#%E5%9F%BA%E6%9C%AC%E6%A0%BC%E5%BC%8F)
    - [变量](#%E5%8F%98%E9%87%8F)
    - [显示规则](#%E6%98%BE%E7%A4%BA%E8%A7%84%E5%88%99)
    - [条件判断](#%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD)
    - [函数](#%E5%87%BD%E6%95%B0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Make

## 推荐学习

+ [九图记住Makefile](https://zhuanlan.zhihu.com/p/163287897)
+ [跟我一起写Makefile](https://seisman.github.io/how-to-write-makefile/index.html)
+ [官网](https://www.gnu.org/software/make/manual/html_node/index.html#SEC_Contents)

## 什么是make

用来整合C/C++代码工程的。make命令执行时，需要一个Makefile文件或者makefile文件，以告诉make命令需要怎么样的去编译和链接程序。

## Makefile语法

### 基本格式

```
target ... : prerequisites ...
    command
    ....
    ....
    
或者

target ... : prerequisites ; command
    command
    ...
    
// command太长, 可以用 "\" 作为换行符

//target  — 目标文件， 可以是Object File 也可以是可执行文件，还可也是标签Label（标签内容在“伪目标”章节）；
//prerequisites —生成target所需的文件或目标；
//command—make需要执行的命令，可以是任何shell命令。

//例子
hello:a.txt b.txt 
a.txt b.txt:
        touch $@
//例子里面我想创建a.txt和b.txt,一共两个目标,使用make（或者 make 目标名）,会从hello目标开始执行,hello这个目标需要下面一个目标的结果,就先去执行下面的目标,然后下面目标是创建文件的语句,然后就执行完成。
```

### 变量

### 显示规则

### 条件判断

### 函数

