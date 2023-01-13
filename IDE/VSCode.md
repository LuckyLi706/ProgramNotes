# VisualStudioCode

## 插件

+ Code Runner

  代码一键运行，并支持了 Node.js, Python, C++, Java, PHP, Perl, Ruby, Go等超过40种的语言。

  - Run in Terminal（支持输入）

    选择 文件 -> 首选项 -> 设置，打开VS Code设置页面，找到 Run Code configuration，勾上 Run In Terminal 选项。设置之后，代码就会在 Terminal 中运行了。

  - 自定义运行逻辑

    对于一些语言，用户希望能自定义代码的运行逻辑。比如说，在 Code Runner 中，C++的默认编译器用的是 g++，也许你希望使用 Clang。那么你可以在 VS Code 设置页面，找到 Executor Map 设置项，并且选择 在settings.json中编辑。

  - 

+ 

## Shell（插件）

+ shellman

  提供智能提示和自动补全功能。

+ shell-format

  shell脚本代码格式化。

  + vscode设置（mac不需要设置）

    文件->首选项->设置"shellformat.path": "E:/01soft/shfmt/shfmt_v2.6.3_windows_amd64.exe"

  + 使用

    右键->format document （格式化文档）进行格式化