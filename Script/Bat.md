# Bat

+ 脚本是以.bat为后缀的脚本  

+ [Windows官方命令](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/windows-commands)

## 基础

### 第一个例子

+ echo和@

  - @字符放在命令前将关闭该命令回显，⽆论此时echo是否为打开状态
  - echo 输出语句
  - @echo off 表示这条命令后关闭所有命令(包括本身这条命令)的回显
  - @echo on 表示这条命令后打开所有命令(不包括本身这条命令)的回显

+ pause

  会暂停批处理的执行并在屏幕上显示Press any key to continue…的提示，等待用户按任意键后继续

```vbscript
@echo off
:: 输出支持中文
chcp 65001
echo Hello,World
pause
```

### 注释（两种方式）

+ rem
  - rem为注释命令，⼀般⽤来给程序加上注解，该命令后的内容不被执⾏，但能回显。
+ ::
  -  ::后的字符⾏在执⾏时不会回显, ⽆论是否⽤echo on打开命令⾏回显状态, 因为命令解释 器不认为他是⼀个有效的命令⾏。
  - 有效标号：冒号后紧跟⼀个以字母数字开头的字符串，goto语句可以识别。 
  - ⽆效标号：冒号后紧跟⼀个⾮字母数字的⼀个特殊符号，goto⽆法识别的标号，可以起到注释作⽤，所以 :: 常被⽤ 作注释符号，其实 :+ 也可起注释作⽤。

### 变量

#### 系统变量

```
%SystemRoot% === C:\WINDOWS (%windir% 同样)
%ProgramFiles% === C:\Program Files
%USERPROFILE% === C:\Documents and Settings\Administrator (子目录有“桌面”,“开始菜单”,“收藏夹”等)
%APPDATA% === C:\Documents and Settings\Administrator\Application Data
%TEMP% === C:\DOCUME~1\ADMINI~1\LOCALS~1\Temp (%TEM% 同样)
%APPDATA% === C:\Documents and Settings\Administrator\Application Data
%OS% === Windows_NT (系统)
%Path% === %SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem (原本的设置)
%HOMEDRIVE% === C: (系统盘)
%HOMEPATH% === \Documents and Settings\Administrator

%~dp0 “d”为Drive的缩写，即为驱动器，磁盘、“p”为Path缩写，即为路径，目录
cd %~dp0 ：进入批处理所在目录
cd %~dp0bin\ ：进入批处理所在目录的bin目录

枚举当前的环境变量
setlocal enabledelayedexpansion
FOR /F "usebackq delims==" %%i IN (set) DO @echo %%i !%%i!
```

#### 特殊变量

+ %0 %1 %2 %3 %4 %5 ......⼀直到%9 还有⼀个%*

  - %1 %2 %3 %4 %5 ......⼀直到%9

    对应启动bat脚本时候的参数，如Test.bat  3  4 （%1对应3，%2对应4）

  - %*

    他是⼀次返回全部参数的值,不⽤在输⼊%1 %2 来确定⼀个个的

  - %0

    1. 返回批处理所在绝对路径

    2. ⽆限循环执⾏BAT

       ```
       rem 保存为BAT执⾏,他就会⽆限循环执⾏net user这条命令,直到你⼿动停⽌
       @echo off
       net user
       %0
       ```

#### 自定义变量

+ 格式：set 变量名=值

```vbscript
@echo off
:: 定义变量var为abcd
set var=abcd
：：使用%变量名%来使用变量
echo %var%
pause
```

#### 获取用户输入

+ 格式：set /p 变量名=提示输入信息

```vbscript
@echo off
set /p var=请输入变量的值:
echo  您输入了%var%
pause
```

### 数据类型

#### 字符串

##### 字符串替换

+ 格式：%PATH:str1=str2%（将字符串变量%PATH%中的str1 替换为str2）

```vbscript
@echo off
set a= bbs. bathome. cn
echo  替换前的值: "%a%"
:: 将字符串变量a中的空格替换为无空格
set var=%a: =%
echo  替换后的值: "%var%"
pause

:: 输出结果为替换后的值: bbs.bathome.cn
```

##### 字符串截取

+ 格式：%a:~[m[,n]]%（方括号表示可选，%为变量标识符，a为变量名，不可少，冒号用于分隔变量名和说明部分，符号～可以简单理解为“
  偏移”即可，m 为偏移量（缺省为0），n 为截取长度（缺省为全部））

```vbscript
a=bbs.bathome.cn
%a:~1,3%    -------- “bs.”        变量a 偏离1位，截取3位字符。
%a:~1,-3%   -------- “bs.bathome” 变量a 偏离1位，截取倒数第3位前的字符。
%a:~-3%    -------- “.cn”        变量a 偏离-3位，截取倒数的3位字符。
%a:~-3,2%   -------- “.c”        变量a 偏离-3位，截取倒数后3位的前两2位字符
%a:~3%     -------- “.bathome.cn”变量a 偏离3位，截取完后面的字符。
%a:~,3%     -------- “bbs”      变量a 偏离0位，截取3位字符。
```

### 运算符

#### 算术运算符

+ \* / %  + -

```vbscript
:: 使用set /a来进行计算

@echo off
set a=123
set b=222
set /a var=a+b
:: 输出345
echo  %var%
pause
```

### 判断和循环

#### if

+ 按照判断内容区分

  - 判断两个字符串是否相等，if "字符串1"=="字符串2" command 语句;
  - 判断两个数值是否相等，if 数值1 equ 数值2 command 语句；
  - 判断驱动器，文件或文件夹是否存在，if exist filename command 语句;
  - 判断变量是否已经定义，if defined 变量 command 语句；
  - 判断上个命令的返回值，if errorlevel 数值 command 语句。

+ 按照嵌套方式区分

  - if

    语法格式：

    if condition commands 

    或者

    if condition (
        commands
    )

    注意点：

    1. 当commands命令有多条语句的时候，需要加()；

    2. 比较数值大小不能使用 > = < 等符号，这些符号在批处理语言中有其他的含义！要使用以下关系符号进行比较：

       EQU - 等于 (一般使用“==”)
       NEQ - 不等于 (没有 “!=”,改用“ if not 1==1 ”的写法)
       LSS - 小于
       LEQ - 小于或等于
       GTR - 大于
       GEQ - 大于或等于

  - if-else

    语法格式：

    if condition (commands) else commands

    或者

    if condition (
    	commands
    ) else (
    	commands
    )

    注意点：

    1. if后面的commands命令必须加()，当else后面的commands命令有多条语句的时候，也需要加()；
    2. if-else必须在语义上同行，所以当else后面有括号的时候，这个括号要紧跟else，不能放在下一行！

  - if if-else else

    语法格式：

    if condition (if condition (commands) else commands) else commands

    或者

    if condition (
        if condition (
            commands
        ) else (
            commands
        )
    ) else (
        commands
    )

  - if-else if-else

    语法格式：

    if condition (commands) else (if condition (commands) else commands)

    或者

    if condition (
    	commands
    ) else (
    	if condition (
    		commands
    	) else (
    		commands
    	)
    )

```vbscript
@echo off
chcp 65001
set /p var1=请输入第一个比较的字符：
set /p var2=请输入第二个比软的字符：
if "%var1%"=="%var2%" (echo 输入的两个字符相同) else echo 输入的两个字符不相同
pause

@echo off
chcp 65001
set /p var1=请输入第一个比较的字符：
set /p var2=请输入第二个比较的字符：
if "%var1%"=="%var2%" (
    echo 输入的两个字符相同
) else (
    echo 输入的两个字符不相同
)
pause
```

#### choice

CHOICE [/C choices] [/N] [/CS] [/T timeout /D choice] [/M text]

参数列表: 

/C choices 指定要创建的选项列表。默认列表是 "YN"。

 /N 在提⽰符中隐藏选项列表。提⽰前⾯的消息得到显⽰， 选项依旧处于启⽤状态。

 /CS 允许选择分⼤⼩写的选项。在默认情况下，这个⼯具 是不分⼤⼩写的。

 /T timeout 做出默认选择之前，暂停的秒数。可接受的值是从 0 到 9999。如果指定了 0，就不会有暂停，默认选项 会得到选择。

 /D choice 在 nnnn 秒之后指定默认选项。字符必须在⽤ /C 选 项指定的⼀组选择中; 同时，必须⽤ /T 指定 nnnn。

 /M text 指定提⽰之前要显⽰的消息。如果没有指定，⼯具只 显⽰提⽰。



ERRORLEVEL: 

ERRORLEVEL 环境变量被设置为从选择集选择的键索引。列出的第⼀个选 择返回 1，第⼆个选择返回 2，等等

+ 例子1: 

  ```
  @echo off
  choice /c YNC /m "确认请选Y，否请按N，取消按C."
  echo %errorlevel%
  
  
  选择Y输出1
  选择N输出2
  选择C输出3
  ```

#### for

+ 基本语法

  FOR %%variable IN (set) DO command [command-parameters]

  或者

  FOR %%variable IN (set) DO command (

  ​        [command-parameters]

  )

  - 例子1: 遍历打印

    ```
    @echo off
    for %%a in (1,1,3) do (
    echo %%a
    )
    
    输出
    1
    1
    3
    ```

  - 例子2: 遍历路径下的文件

    ```
    @echo off
    :: 表示在当前目录下，查找所有 txt 文件。如果需要递归查找当前目录下所有文件夹内的txt文件，需要加 /r
    for %%a in (*.txt) do echo %%a
    pause
    ```

+ 参数/D

  语法：FOR /D %%variable IN (set) DO command [command-parameters]

  如果set里面包含通配符，则指定与⽬录名匹配，⽽不与⽂件名匹配。这个参数主要⽤于⽬录搜索,不会搜索⽂件。

  - 例子1: 遍历c盘下所有文件夹

    ```
    @echo off
    :: 通配符*号表⽰任意N个字符
    for /d %%i in (c:\*) do echo %%i
    pause
    ```

  - 例子2: 遍历c盘下所有名字只包含1～3个字符的文件夹

    ```
    @echo off
    :: 通配符?号表⽰任意一个字符
    for /d %%i in (???) do echo %%i
    pause
    ```

+ 参数/R

  语法：FOR /R [[drive:]path] %%variable IN (set) DO command [command-parameters]

  检查以[drive:]path 为根的⽬录树，指向每个⽬录中的FOR 语句。 

  如果在 /R 后没有指定⽬录，则使⽤当前⽬录。 

  如果集仅为⼀个单点(.)字符，则枚举该⽬录树。

  - 例子1: 递归遍历C盘下所有exe结尾的文件路径

    ```
    @echo off
    for /r c:\ %%i in (*.exe) do echo %%i
    pause
    ```

  - 例子2: 递归遍历当前路径下所有exe结尾的文件路径

    ```
    @echo off
    for /r %%i in (*.exe) do @echo %%i
    pause
    ```

  - 例子3:  递归遍历C盘下所有文件，找到Test.bat所在的路径

    ```
    @echo off
    for /r c:\ %%i in (Test.bat) do if exist %%i echo %%i
    pause
    ```

+ 参数/L

  语法：FOR /L %%variable IN (start,step,end) DO command [command-parameters]

  start：开始的值

  step：步距

  end：结束的值

  从start开始，步距为step，直到end结束执行

  - 例子1: 打印1～5的数字

    ```
    @echo off
    for /l %%i in (1,1,5) do @echo %%i
    pause
    
    输出
    1
    2
    3
    4
    5
    ```

+ 参数/F

  语法：

  FOR /F ["options"] %%variable IN (file-set) DO command [command-parameters] 

  FOR /F ["options"] %%variable IN ("string") DO command [command-parameters] 

  FOR /F ["options"] %%variable IN ('command') DO command [command-parameters]

  用于读取文件内容

  带引号的字符串"options"包括⼀个或多个 指定不同解析选项的关键字。

  这些关键字为:

   eol=c - 指⼀个⾏注释字符的结尾(就⼀个)(备注：默认以使⽤；号为⾏⾸字符的为注释⾏) 

  skip=n - 指在⽂件开始时忽略的⾏数，(备注：最⼩为1，n可以⼤于⽂件的总⾏数，默认为1。) 

  delims=xxx - 指分隔符集。这个替换了空格和跳格键的默认分隔符集。 

  tokens=x,y,m-n - 指每⾏的哪⼀个符号被传递到每个迭代的 for 本⾝。这会导致额外变量名称的分配。m-n 格式为⼀个范围。通过 nth 符号指定 mth。如果符号字符串中的最后⼀个字符星号，那么额外的变量将在最后 ⼀个符号解析之后分配并接受⾏的保留⽂本。经测试，该参数最多只能区分31个字段。(备注：默认为1，则表⽰只 显⽰分割后的第⼀列的内容，最⼤是31，超过最⼤则⽆法表⽰) usebackq - 使⽤后引号（键盘上数字1左⾯的那个键`）。 

  未使⽤参数usebackq时：file-set表⽰⽂件，但不能含有空格 

  双引号表⽰字符串，即"string" 

  单引号表⽰执⾏命令，即'command' 使⽤参数usebackq时：file-set和"file-set"都表⽰⽂件 当⽂件路径或名称中有空格时，就可以⽤双引号括起来 单引号表⽰字符串，即'string' 后引号表⽰命令执⾏，即 command

#### goto

在批处理中允许以“:XXX”来构建⼀个标号，然后⽤GOTO XXX跳转到标号:XXX处，然后执⾏标号后的命令

```
@echo off
:start
set /a var+=1
echo %var%
if %var% leq 3 GOTO start
pause

输出：
1
2
3
4
```



