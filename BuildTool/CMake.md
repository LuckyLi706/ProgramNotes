# CMake

## 入门

### 什么是CMake

CMake是一个跨平台的安装（编译）工具，可以用简单的语句来描述所有平台的安装(编译过程)。他能够输出各种各样的makefile或者project文件，CMake 的组态档取名为 CMakeLists.txt。也就是在CMakeLists.txt这个文件中写cmake代码。
一句话：cmake就是将多个cpp、hpp文件组合构建为一个大工程的语言。

### 资料

+ [优秀的Demo例子](https://github.com/SFUMECJF/cmake-examples-Chinese)
+ [Cmake官方命令](https://cmake.org/cmake/help/latest/manual/cmake-commands.7.html)

## CMakeLists.txt常用命令

### message

```cmake
# 打印信息
cmake_minimum_required(VERSION 3.17)
project(TestC__)
set(CMAKE_CXX_STANDARD 11)
# 为了分行确定输出内容

# message 消息类型
(none)         = 重要消息
STATUS         = 附带消息
WARNING        = CMake警告，继续处理
AUTHOR_WARNING = CMake警告（dev），继续处理
SEND_ERROR     = CMake错误，继续处理，但跳过生成
FATAL_ERROR    = CMake错误，停止处理和生成
DEPRECATION    = 如果分别启用了变量CMAKE_ERROR_DEPRECATED或CMAKE_WARN_DEPRECATED，则CMake弃用错误或警告，否则无消息

message("CMAKE_SOURCE_DIR = ${CMAKE_SOURCE_DIR}")
message(STATUS "PROJECT_SOURCE_DIR = ${PROJECT_SOURCE_DIR}")
message(WARNING "CMAKE_BINARY_DIR = ${CMAKE_BINARY_DIR}")
//添加日志打印出来
message("AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA>>>")
message("当前CMake的路径是：${CMAKE_SOURCE_DIR}")

message("")

message("1.PROJECT_BINARY_DIR = ${PROJECT_BINARY_DIR}")
message("2.PROJECT_SOURCE _DIR = ${_DIR}")
message("3.CMAKE_CURRENT_SOURCE_DIR = ${CMAKE_CURRENT_SOURCE_DIR}")
message("4.CMAKE_CURRRENT_BINARY_DIR = ${CMAKE_CURRRENT_BINARY_DIR}")
message("5.CMAKE_CURRENT_LIST_FILE = ${CMAKE_CURRENT_LIST_FILE}")
message("6.CMAKE_CURRENT_LIST_LINE = ${CMAKE_CURRENT_LIST_LINE}")
message("7.CMAKE_MODULE_PATH = ${CMAKE_MODULE_PATH}")
message("8.CMAKE_SOURCE_DIR = ${CMAKE_SOURCE_DIR}")
message("9.EXECUTABLE_OUTPUT_PATH = ${EXECUTABLE_OUTPUT_PATH}")
message("10.LIBRARY_OUTPUT_PATH = ${LIBRARY_OUTPUT_PATH}")
message("11.PROJECT_NAME = ${PROJECT_NAME}")
message("12.PROJECT_VERSION_MAJOR = ${PROJECT_VERSION_MAJOR}")
message("13.PROJECT_VERSION_MINOR = ${PROJECT_VERSION_MINOR}")
message("14.PROJECT_VERSION_PATCH = ${PROJECT_VERSION_PATCH}")
message("15.CMAKE_SYSTEM = ${CMAKE_SYSTEM}")
message("16.CMAKE_SYSTEM_NAME = ${CMAKE_SYSTEM_NAME}")
message("17.CMAKE_SYSTEM_VERSION = ${CMAKE_SYSTEM_VERSION}")
message("18.BUILD_SHARED_LIBS = ${BUILD_SHARED_LIBS}")
message("19.CMAKE_C_FLAGS = ${CMAKE_C_FLAGS}")
message("20.CMAKE_CXX_FLAGS = ${CMAKE_CXX_FLAGS}")
message("21.CMAKE_SYSTEM_PROCESSOR   = ${CMAKE_SYSTEM_PROCESSOR}")
# 为了分行确定输出内容
message("")

# 输出结果
1.PROJECT_BINARY_DIR = D:/Projects/ClionProjects/TestC++/cmake-build-debug
2.PROJECT_SOURCE _DIR = 
3.CMAKE_CURRENT_SOURCE_DIR = D:/Projects/ClionProjects/TestC++
4.CMAKE_CURRRENT_BINARY_DIR = 
5.CMAKE_CURRENT_LIST_FILE = D:/Projects/ClionProjects/TestC++/CMakeLists.txt
6.CMAKE_CURRENT_LIST_LINE = 15
7.CMAKE_MODULE_PATH = 
8.CMAKE_SOURCE_DIR = D:/Projects/ClionProjects/TestC++
9.EXECUTABLE_OUTPUT_PATH = 
10.LIBRARY_OUTPUT_PATH = 
11.PROJECT_NAME = TestC__
12.PROJECT_VERSION_MAJOR = 
13.PROJECT_VERSION_MINOR = 
14.PROJECT_VERSION_PATCH = 
15.CMAKE_SYSTEM = Windows-10.0.19041
16.CMAKE_SYSTEM_NAME = Windows
17.CMAKE_SYSTEM_VERSION = 10.0.19041
18.BUILD_SHARED_LIBS = 
19.CMAKE_C_FLAGS = /DWIN32 /D_WINDOWS
20.CMAKE_CXX_FLAGS = /DWIN32 /D_WINDOWS /GR /EHsc
21.CMAKE_SYSTEM_PROCESSOR   = AMD64
```

### project

```cmake
# CMakeLists.txt
cmake_minimum_required (VERSION 3.10.2)
project (mytest)

# project 非必须,可以不指定（默认是当前工程名,默认PROJECT_NAME也是当前工程名）
# 指定project参数，cmake内部会为如下变量赋值：
# 1、PROJECT_NAME：将当前工程的名称赋值给PROJECT_NAME，对于本例子，就是${PROJECT_NAME}=mytest
# 2、<PROJECT-NAME>_SOURCE_DIR：指定工程的源码路径，这个变量和PROJECT_SOURCE_DIR的区别就是，<PROJECT-NAME>_SOURCE_DIR跟具体的工程名字关联起来，若<PROJECT-NAME>就是当前工程，则该变量和PROJECT_SOURCE_DIR相等
# 3、PROJECT_BINARY_DIR：当前工程的二进制路径。
# 4、<PROJECT-NAME>_BINARY_DIR：指定工程的二进制路径，这个变量和PROJECT_BINARY_DIR的区别就是，<PROJECT-NAME>_BINARY_DIR跟具体的工程名字关联起来，若<PROJECT-NAME>就是当前工程，则该变量和PROJECT_BINARY_DIR相等。
# 5、CMAKE_PROJECT_NAME：顶层工程的名称。例如当前调用的CMakeLists.txt位于顶层目录（可以理解为使用cmake命令首次调用的那个CMakeLists.txt），那么工程名还会赋值给CMAKE_PROJECT_NAM
```

### set

```cmake
set(<variable> <value>... [PARENT_SCOPE]) #设置普通变量
set(<variable> <value>... CACHE <type> <docstring> [FORCE]) #设置缓存条目
set(ENV{<variable>} [<value>]) #设置环境变量

# 设置普通变量
cmake_minimum_required (VERSION 3.10.2)
project (set_test)
set (normal_var a)   # 把normal_var设置给a变量
set (normal_var a b c)  # 把normal_var设置给a、b、c变量
set (normal_var)        ## 把normal_var设置为空
message (">>> value = ${normal_var}")

# 设置缓存条目

# 设置环境变量
```

### list

```cmake
list (subcommand <list> [args...])
# subcommand为具体的列表操作子命令，例如读取、查找、修改、排序等。<list>为待操作的列表变量，[args...]为对列表变量操作需要使用的参数表，不同的子命令对应的参数也不一致。
# 列表的操作分为读取、查找、修改、排序等4个大类

# 列表的读取
# 1、LENGTH：子命令LENGTH用于读取列表长度
list (LENGTH <list> <output variable>)  #<output variable>为新创建的变量，用于存储列表的长度。
```

### include_directories

```cmake
include_directories ([AFTER|BEFORE] [SYSTEM] dir1 [dir2 ...]) 
# 将指定目录添加到编译器的头文件搜索路径之下，指定的目录被解释成当前源码路径的相对路径
# 默认情况下，include_directories命令会将目录添加到列表最后，可以通过命令设置CMAKE_INCLUDE_DIRECTORIES_BEFORE变量为ON来改变它默认行为，将目录添加到列表前面。也可以在每次调用include_directories命令时使用AFTER或BEFORE选项来指定是添加到列表的前面或者后面。如果使用SYSTEM选项，会把指定目录当成系统的搜索目录。该命令作用范围只在当前的CMakeLists.txt。

#CMakeLists.txt
cmake_minimum_required(VERSION 3.18.2)
project(include_directories_test)

include_directories(sub) 
include_directories(sub2) #默认将sub2添加到列表最后
include_directories(BEFORE sub3) #可以临时改变行为，添加到列表最前面

get_property(dirs DIRECTORY ${CMAKE_SOURCE_DIR} PROPERTY INCLUDE_DIRECTORIES)
message(">>> include_dirs=${dirs}") #打印一下目录情况

set(CMAKE_INCLUDE_DIRECTORIES_BEFORE ON) #改变默认行为，默认添加到列表前面
include_directories(sub4)
include_directories(AFTER sub5) #可以临时改变行为，添加到列表的最后
get_property(dirs DIRECTORY ${CMAKE_SOURCE_DIR} PROPERTY INCLUDE_DIRECTORIES)
message(">>> SET DEFAULT TO BEFORE, include_dirs=${dirs}")
```

### add_subdirectory

```cmake
add_subdirectory (source_dir [binary_dir] [EXCLUDE_FROM_ALL])   #添加一个子目录并构建该子目录。

# source_dir
必选参数。该参数指定一个子目录，子目录下应该包含CMakeLists.txt文件和代码文件。子目录可以是相对路径也可以是绝对路径，如果是相对路径，则是相对当前目录的一个相对路径。
# binary_dir
可选参数。该参数指定一个目录，用于存放输出文件。可以是相对路径也可以是绝对路径，如果是相对路径，则是相对当前输出目录的一个相对路径。如果该参数没有指定，则默认的输出目录使用source_dir。
# EXCLUDE_FROM_ALL
可选参数。当指定了该参数，则子目录下的目标不会被父目录下的目标文件包含进去，父目录的CMakeLists.txt不会构建子目录的目标文件，必须在子目录下显式去构建。例外情况：当父目录的目标依赖于子目录的目标，则子目录的目标仍然会被构建出来以满足依赖关系（例如使用了target_link_libraries）
```

### add_executable

```cmake
add_executable (<name> [WIN32] [MACOSX_BUNDLE]
      [EXCLUDE_FROM_ALL]
      [source1] [source2 ...])   # 普通可执行目标文件
add_executable (<name> IMPORTED [GLOBAL]) # 导入可执行目标文件
add_executable (<name> ALIAS <target>) # 别名可执行目标文件

# 普通可执行目标文件（参数解释）
# name:可执行目标文件的名字，在一个cmake工程中，这个名字必须全局唯一。
# WIN32:用于windows系统下创建一个以WinMain为入口的可执行目标文件（通常入口函数为main），它不是一个控制台应用程序，而是一个GUI应用程序。当WIN32选项使用的时候，可执行目标的 WIN32_EXECUTABLE会被置位ON。
# MACOSX_BUNDLE:用于mac系统或者IOS系统下创建一个GUI可执行应用程序，当MACOSX_BUNDLE选项使用的时候，可执行目标的MACOSX_BUNDLE会被置位ON。
# EXCLUDE_FROM_ALL:用于指定可执行目标是否会被构建，当该选项使用的时候，可执行目标不会被构建。
# [source1] [source2 ...]:构建可执行目标文件所需要的源文件。也可以通过target_sources()继续为可执行目标文件添加源文件，要求是在调用target_sources之前，可执行目标文件必须已经通过add_executable或add_library定义了。
cmake_minimum_required(VERSION 3.17)
project(TestC__)
set(CMAKE_CXX_STANDARD 11)
add_executable(TestC__ main.cpp)

# 导入可执行目标文件（参数解释）
# 将工程外部的可执行目标文件导入进来，不会有任何构建可执行目标文件的动作发生。如果不指定GLOBAL，则可执行目标文件的范围为文件创建的目录及子目录；指定GLOBAL则会将范围扩大到整个工程。IMPORTED选项指定后，属性IMPORTED会被置为TRUE，在工程内构建的可执行目标文件的属性IMPORTED会被置为FALSE。

# 别名可执行目标文件（参数解释）
# 为可执行目标文件创建一个别名。创建该别名后，可以使用别名进行可执行目标的读、测试操作，但是不能利用别名对可执行目标的修改属性操作。
```

### add_library

```cmake
add_library(<name> [STATIC | SHARED | MODULE]
            [EXCLUDE_FROM_ALL]
            [source1] [source2 ...])  # 普通库（静态库和动态库）
add_library(<name> <SHARED|STATIC|MODULE|OBJECT|UNKNOWN> IMPORTED
            [GLOBAL]) # 导入的库
            
# 普通库（静态库和动态库）（参数解释）
# 该指令的主要作用就是将指定的源文件生成链接文件，然后添加到工程中去
# name属性必须全局唯一生成的library名会根据STATIC或SHARED成为name.a或name.lib这里的STATIC和SHARED可不设置，通过全局的BUILD_SHARED_LIBS的FALSE或TRUE来指定windows下，如果dll没有export任何信息，则不能使用SHARED，要标识为MODULE
# 添加的库会被输出到以下几个目录ARCHIVE_OUTPUT_DIRECTORY, LIBRARY_OUTPUT_DIRECTORY和 RUNTIME_OUTPUT_DIRECTORY
# 常用设定及函数设置EXCLUDE_FROM_ALL，可使这个library排除在all之外，即必须明确点击生成才会生成

# 导入的库


# 静态库
add_library(baz STATIC IMPORTED)
set_target_properties(baz PROPERTIES
IMPORTED_LOCATION_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/libbaz.a
IMPORTED_LOCATION_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/libbazd.a)

# 静态库(添加依赖项)
add_library(bar STATIC IMPORTED)
set_target_properties(bar PROPERTIES
IMPORTED_LOCATION_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/libbar.a
IMPORTED_LOCATION_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/libbard.a
IMPORTED_LINK_INTERFACE_LIBRARIES baz) # <-- dependency is here

# 动态库
add_library(bar SHARED IMPORTED)
set_property(TARGET bar PROPERTY IMPORTED_LOCATION c:/path/to/bar.dll)
set_property(TARGET bar PROPERTY IMPORTED_IMPLIB c:/path/to/bar.lib) # 多了lib信息
add_executable(myexe src1.c src2.c)
target_link_libraries(myexe bar)

# 当然，也可以直接引用库文件
TARGET_LINK_LIBRARIES(skiaSampleCode
debug skiaCored.lib
optimized skiaCore.lib)
```

### link_directories

```cmake
# 该指令的作用主要是指定要链接的库文件的路径，该指令有时候不一定需要。因为find_package和find_library指令可以得到库文件的绝对路径。不过你自己写的动态库文件放在自己新建的目录下时，可以用该指令指定该目录的路径以便工程能够找到
```

### target_link_libraries

```cmake
# 该指令的作用为将目标文件与库文件进行链接。该指令的语法如下：
target_link_libraries( [item1] [item2] […] [[debug|optimized|general] ] …)

target_link_libraries(myProject hello)       # 链接libhello.so库，默认优先链接动态库
target_link_libraries(myProject libhello.a)  # 显示指定链接静态库
target_link_libraries(myProject libhello.so) # 显示指定链接动态库
```

### find_library

```cmake
# 查找库所在目录
find_library (
          <VAR>
          name | NAMES name1 [name2 ...] [NAMES_PER_DIR]
          [HINTS path1 [path2 ... ENV var]]
          [PATHS path1 [path2 ... ENV var]]
          [PATH_SUFFIXES suffix1 [suffix2 ...]]
          [DOC "cache documentation string"]
          [NO_DEFAULT_PATH]
          [NO_CMAKE_ENVIRONMENT_PATH]
          [NO_CMAKE_PATH]
          [NO_SYSTEM_ENVIRONMENT_PATH]
          [NO_CMAKE_SYSTEM_PATH]
          [CMAKE_FIND_ROOT_PATH_BOTH |
           ONLY_CMAKE_FIND_ROOT_PATH |
           NO_CMAKE_FIND_ROOT_PATH]
         )
         
# 例子
find_library(RUNTIME_LIB mylib /usr/lib  /usr/local/lib NO_DEFAULT_PATH) #cmake会在目录中查找，如果所有目录中都没有，值RUNTIME_LIB就会被赋为NO_DEFAULT_PATH
```

### set_target_properties

```cmake
set_target_properties(target1 target2 ...
                      PROPERTIES prop1 value1
                      prop2 value2 ...)
                      
# 1、设置库输出路径
set_target_properties(gmath
                      PROPERTIES
                      ARCHIVE_OUTPUT_DIRECTORY  #输出路径属性
                      "${distribution_DIR}/gmath/lib/${ANDROID_ABI}") #将gmath库输出到下面的路径去
                      
# 2、导入第三方库,配合add_library使用
add_library(lib_gmath STATIC IMPORTED)   # 导入静态库lib_gmath
set_target_properties(lib_gmath PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/gmath/lib/${ANDROID_ABI}/libgmath.a) #设置lib_gmath库的路径
```

### add_custom_command

```cmake
# 1、添加定制命令来生成文件
add_custom_command(OUTPUT output1 [output2 ...]
                   COMMAND command1 [ARGS] [args1...]``
                   [COMMAND command2 [ARGS] [args2...] ...]
                   [MAIN_DEPENDENCY depend]
                   [DEPENDS [depends...]]
                   [BYPRODUCTS [files...]]
                   [IMPLICIT_DEPENDS <lang1> depend1
                                    [<lang2> depend2] ...]
                   [WORKING_DIRECTORY dir]
                   [COMMENT comment]
                   [DEPFILE depfile]
                   [JOB_POOL job_pool]
                   [VERBATIM] [APPEND] [USES_TERMINAL]
                   [COMMAND_EXPAND_LISTS])

cmake_minimum_required(VERSION 3.0)
project(test)
add_custom_command(OUTPUT COPY_RES
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/config ${CMAKE_CURRENT_SOURCE_DIR}/etc
  COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/log.txt ${CMAKE_CURRENT_SOURCE_DIR}/etc
  )
add_custom_target(CopyTask ALL DEPENDS COPY_RES)
# add_custom_target生成一个目标CopyTask，该目标依赖于COPY_RES。而对于COPY_RES而言，它实际上是用来复制文件夹或者复制文件的！也就是COMMAND中定义的操作

# 2、为某个目标(如库或可执行程序)添加一个定制命令
# PRE_BUILD	在目标中执行任何其他规则之前运行
# PRE_LINK	在编译源代码之后，链接二进制文件或库文件之前运行
# POST_BUILD	在目标内所有其他规则均已执行后运行
add_custom_command(TARGET <target>
                   PRE_BUILD | PRE_LINK | POST_BUILD
                   COMMAND command1 [ARGS] [args1...]
                   [COMMAND command2 [ARGS] [args2...] ...]
                   [BYPRODUCTS [files...]]
                   [WORKING_DIRECTORY dir]
                   [COMMENT comment]
                   [VERBATIM] [USES_TERMINAL])

# 这种定制命令可以设置在，构建这个目标过程中的某些时机。也就是就，这种场景可以在目标构建的过程中，添加一些额外执行的命令。这些命令本身将会成为该目标的一部分。注意，仅在目标本身被构建过程才会执行。如果该目标已经构建，命令将不会执行

cmake_minimum_required(VERSION 3.0)
project(test)
add_custom_target(CopyTask)
add_custom_command(TARGET CopyTask
  POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/config ${CMAKE_CURRENT_SOURCE_DIR}/etc
  COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/log.txt ${CMAKE_CURRENT_SOURCE_DIR}/etc
  )
# 这段代码的功能和上一段是一样的，将config文件夹的内容和log.txt文件复制到新的etc文件夹内。需要注意的是，此时add_custom_command需要写在add_custom_target之后，否则将cmake不通过
```

### target_include_directories

```cmake
# 指定目标包含的头文件路径,指定编译目标文件的时候需要包含的路径和内容， <target> 必须是一个已经通过诸如 add_executable()或者add_library()函数创建了的目标，并且不是一个标注成IMPORTED目标
target_include_directories(<target> [SYSTEM] [BEFORE]
  <INTERFACE|PUBLIC|PRIVATE> [items1...]
  [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])
 
```

### file

```cmake
# MAKE_DIRECTORY在指定目录处创建子目录，如果它们的父目录不存在，也会创建它们的父目录。
file(MAKE_DIRECTORY [directory1 directory2 ...])
```

## 例子

### 动态库

```cmake
# 1、直接生成动态库
add_library(hello-jni SHARED
            hello-jni.c)   # 通过hello-jni.c生成动态库libhello-jni.so
            
# 2、链接其他库生成动态库
add_library(hello-jni SHARED
            hello-jni.c)   # 通过hello-jni.c生成动态库libhello-jni.so
target_link_libraries(hello-jni
                      android
                      log) # 链接android和log两个库
                      
# 3、生成动态库,并设置输出位置
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_VERBOSE_MAKEFILE on)
add_library(gperf SHARED src/gperf.c)  #通过src/grerf.c生成动态库
set(distribution_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../../distribution) #设置路径
set_target_properties(gperf
                      PROPERTIES
                      LIBRARY_OUTPUT_DIRECTORY
                      "${distribution_DIR}/gperf/lib/${ANDROID_ABI}") # 设置动态库输出位置
add_custom_command(TARGET gperf POST_BUILD
                   COMMAND "${CMAKE_COMMAND}" -E
                   copy "${CMAKE_CURRENT_SOURCE_DIR}/src/gperf.h"
                   "${distribution_DIR}/gperf/include/gperf.h"
                   COMMENT "Copying gperf to output directory") #复制头文件到指定路径
                   
# 4、添加静态库来生成动态库
cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../distribution) # 导入库的路径

add_library(lib_gmath STATIC IMPORTED)  #导入静态库
set_target_properties(lib_gmath PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/gmath/lib/${ANDROID_ABI}/libgmath.a) # 配置导入静态库的路径

add_library(lib_gperf SHARED IMPORTED)  # 导入动态库
set_target_properties(lib_gperf PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/gperf/lib/${ANDROID_ABI}/libgperf.so) # 配置导入动态库的路径

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11") # 添加C++11支持
add_library(hello-libs SHARED
            hello-libs.cpp)  # 构建动态库
target_include_directories(hello-libs PRIVATE
                           ${distribution_DIR}/gmath/include
                           ${distribution_DIR}/gperf/include)  # 目标添加私有的头文件
target_link_libraries(hello-libs
                      android
                      lib_gmath
                      lib_gperf
                      log)   # 目标hello-libs链接android、lib_gmath、lib_grerf、log库
```

### 静态库

```cmake
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_VERBOSE_MAKEFILE on)
add_library(gmath STATIC src/gmath.c) #通过gmath.c生成静态库
set(distribution_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../../distribution) #设置路径变量
set_target_properties(gmath
                      PROPERTIES
                      ARCHIVE_OUTPUT_DIRECTORY
                      "${distribution_DIR}/gmath/lib/${ANDROID_ABI}") #设置库的输出路径
add_custom_command(TARGET gmath POST_BUILD
                   COMMAND "${CMAKE_COMMAND}" -E
                   copy "${CMAKE_CURRENT_SOURCE_DIR}/src/gmath.h"
                   "${distribution_DIR}/gmath/include/gmath.h"
                   COMMENT "Copying gmath to output directory") #在生成库之后复制头文件到指定目录
```

