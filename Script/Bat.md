# Bat

+ 脚本是以.bat为后缀的脚本  

+ [Windows官方命令](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/windows-commands)

## 基本命令

### echo

```bash
echo on/off //一般出现在基本最上面,表示在此语句后所有运行的命令都显示/不显示命令行本身

@echo off //此语句后所有运行的命令都不显示命令行本身（包含echo off自己）

@符号只针对单行不显示命令行

echo Hello,World  //打印信息
```

### rem（注释）

```bash
//bat里面使用rem或者::来表示后面是注释语句
rem "我是注释"
:: “我是注释”
```

### pause（暂停）

```
//会暂停批处理的执行并在屏幕上显示Press any key to continue…的提示，等待用户按任意键后继续

pause
```

### call

```
//语法: call [[Drive:][Path] FileName [BatchParameters]] [:label [arguments]]
//参数: [Drive:][Path] FileName 指定要调用的批处理程序的位置和名称。filename 参数必须具有 .bat 或 .cmd 扩展名。调用另一个批处理程序，并且不终止父批处理程序

//call test.bat 11111  //后面的11111是参数,详细见传递参数
```

### start

```
//调用外部程序，所有的 DOS命令 和 命令行程序 都可以由 start命令 来调用
//常用的几个参数
MIN 开始时窗口最小化
SEPARATE 在分开的空间内开始 16 位 Windows 程序
HIGH 在 HIGH 优先级类别开始应用程序
REALTIME 在 REALTIME 优先级类别开始应用程序
WAIT 启动应用程序并等候它结束
parameters 这些为传送到命令/程序的参数

start /WAIT Notepad++.exe  //启动Notepad++并等候它结束
```

### goto

```
//跳转
@echo off
goto Start
echo "goto2"  //这个不会执行
:Start
echo "goto"  //goto跳转的地方
pause

```

## 参数

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

## 判断和循环

### if

```
// 语法: if [not] "参数" == "字符串" 待执行的命令
Sample: if "%1" == "a" format a:
Sample: if {%1} == {} goto noparms

//if exist
//语法: if [not] exist [路径]文件名 待执行的命令
Sample: if exist config.sys edit config.sys (表示如果存在这文件，则编辑它，用很难看的系统编辑器)
Sample: if exist config.sys type config.sys (表示如果存在这文件，则显示它的内容)

//if errorlevel number
//语法: if [not] errorlevel <数字> 待执行的命令
//很多DOS程序在运行结束后会返回一个数字值用来表示程序运行的结果(或者状态)，称为错误码errorlevel或称返回码。常见的返回码为0、1。通过if errorlevel命令可以判断程序的返回值，根据不同的返回值来决定执行不同的命令。
@echo off
XCOPY F:\test.bat D:\
IF ERRORLEVEL 1 (ECHO 文件拷贝失败
) Else IF ERRORLEVEL 0 ECHO 成功拷贝文件
pause

//else
//语法： if 条件 (成立时执行的命令) else (不成立时执行的命令)
如果是多个条件，建议适当使用括号把各条件包起来，以免出错。
Sample: if 1 == 0 ( echo comment1 ) else if 1==0 ( echo comment2 ) else (echo comment3 )
注：如果 else 的语句需要换行，if 执行的行尾需用“^”连接，并且 if 执行的动作需用(括起来)，否则报错
Sample: if 1 == 0 ( echo comment1 ) else if 1==0 ( echo comment2 ) ^
else (echo comment3 )

//比较运算符
EQU - 等于 (一般使用“==”)
NEQ - 不等于 (没有 “!=”,改用“ if not 1==1 ”的写法)
LSS - 小于
LEQ - 小于或等于
GTR - 大于
GEQ - 大于或等于
```

### choice

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

### for

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

###  continue 和 break

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

