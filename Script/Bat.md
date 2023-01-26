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

### 系统参数

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

//当前路径
%~dp0 “d”为Drive的缩写，即为驱动器，磁盘、“p”为Path缩写，即为路径，目录
cd %~dp0 ：进入批处理所在目录
cd %~dp0bin\ ：进入批处理所在目录的bin目录

枚举当前的环境变量
setlocal enabledelayedexpansion
FOR /F "usebackq delims==" %%i IN (set) DO @echo %%i !%%i!
```

### 传递参数

```
//%[1-9]表示参数，参数是指在运行批处理文件时在文件名后加的以空格(或者Tab)分隔的字符串。
//变量可以从%0到%9，%0表示批处理命令本身，其它参数字符串用 %1 到 %9 顺序表示

call test2.bat "hello" "haha" (执行同目录下的“test2.bat”文件，并输入两个参数)
在“test2.bat”文件里写:
echo %1 (打印: "hello")
echo %2 (打印: "haha")
echo %0 (打印: test2.bat)
echo %19 (打印: "hello"9)
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

```
//将显示“确认请选Y，否请按N，取消按C. [Y,N,C]?”如果用户3秒内没有作出选择，将默认选择’C’。
@echo off
:START
rem /C choices 指定要创建的选项列表。默认列表是 "YN"
rem /N 在提示符中隐藏选项列表。提示前面的消息得到显示，选项依旧处于启用状态
rem /T timeout 做出默认选择之前，暂停的秒数。可接受的值是从 0到 9999。如果指定了 0，就不会有暂停，默认选项会得到选择。
rem /D choice 在 nnnn 秒之后指定默认选项。字符必须在用 /C 选项指定的一组选择中; 同时，必须用 /T 指定 nnnn。
choice /c YNC /m "确认请选Y，否请按N，取消按C." /T 3 /D C  

::echo %errorlevel%

if errorlevel 3 goto CANCEL
if errorlevel 2 goto NO
if errorlevel 1 goto YES

:YES
echo 你的选择是YES!
goto END

:NO
echo 你的选择是NO!
goto END

:CANCEL
echo 你的选择是CANCEL!

:END
goto START

pause
```

#### for

```
//for %%I in (command1) do command2

@echo off
for  %%I in (ABC) do echo %%I
pause

//搜索当前目录下有哪些文件
@echo off
for %%i in (*.*) do echo "%%i"
pause

//搜索当前目录下所有的文本文件
@echo off
for %%i in (*.txt) do echo "%%i"
pause
```

####  continue 和 break

```
//continue: 在 for 循环的最后一行写上一个标签，跳转到这位置即可
//break: 在 for 循环的外面的下一句写上一个标签，跳转到这位置即可

for /F ["options"] %variable IN (command) DO (
… do command …
if … goto continue
if … goto break
… do command …
:continue
)
:break
```

