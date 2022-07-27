<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [HTML](#html)
  - [常用标签](#%E5%B8%B8%E7%94%A8%E6%A0%87%E7%AD%BE)
    - [例子](#%E4%BE%8B%E5%AD%90)
  - [表格标签](#%E8%A1%A8%E6%A0%BC%E6%A0%87%E7%AD%BE)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
# HTML
## 常用标签

```html
<!--
1.<!DOCTYPE> 	定义文档类型。
2.<html>	定义 HTML 文档。
3.<title>	定义文档的标题。
4.<body>	定义文档的主体。
5.<h1> to <h6>	定义 HTML 标题。
6.<p>	定义段落。
7.<br>	定义简单的折行。(是一个独目标记)
8.<hr>	定义水平线。(是一个独目标记)
9.<strong>和<b> 都是加粗标签,更推荐使用strong,语义更强烈
10.<em>和<i> 都是倾斜标签,更推荐使用em,语义更强烈
11.<del>和<s> 都是删除线标签,更推荐使用del,语义更强烈
12.<ins>和<u> 都是下划线标签,更推荐使用ins,语义更强烈
13.<div>和<span> 是没有语意的,他们就是一个盒子,用来装东西的,div标签用来布局的,但是一个div独占一行,大盒子
span标签也是用来布局的,可以一行放多个,小盒子

14.图像标签  格式：<img src="URL路径">
src为图像的属性,必须属性
其他属性：
alt 文本  替换文本,图像不能显示展示的文本
title 文本  提示文本,鼠标放在图像上面显示的文字
width 像素 设置图像的宽度
height 像素 设置图像的高度
border 像素 设置图像的边框粗细

15.超链接标签 （重要） 格式： <a href="跳转目标" target="目标窗口的弹出方式">文本或者图像</a>
href为必须属性,链接目标的url地址,即可以是内部链接也可以是外部链接
traget 为目标 _self为默认值（当前页面打开）,_blank为在新窗口中的打开方式
链接分类：
外部链接 <a href="https://www.baidu.com">百度</a>
内部链接 <a href="index.html">首页</a>  打开当前路径下的index.html
空链接  <a href="#">首页</a>  当前没有确定链接目标
下载链接 如果链接是个文件或者压缩包时,会下载这个文件
网页元素链接 在网页中的各个网页元素,如文本、图像、视频、表格、音频都可以加链接
锚点链接  点击链接,可以快速定位到当前页面的某个位置
锚点链接实现步骤：
步骤一：在链接href属性中,设置属性值为#名字的形式,如<a href="#two">第二集</a>
步骤二：找到目标位置标签,里面添加一个id属性. 如<h3 id="two">第二集介绍></h3>

16.特殊字符
&nbsp;  空格
&lt;  <
&gt;  >
-->
```

### 例子

```html
<!--
<html> 元素是 HTML 页面的根元素
<head> 元素包含了文档的元（meta）数据，如 <meta charset="utf-8"> 定义网页编码格式为 utf-8。
<title> 元素描述了文档的标题
<body> 元素包含了可见的页面内容
 -->
<!DOCTYPE html>   <!--这句代码表示当前页面使用的是HTML5来显示网页,必须放在最上面,他是文档声明标签-->
<html lang="en">  <!--定义当前文档显示的语言,en表示英文,zh-CN表示中文-->
<head>
    <meta charset="UTF-8">   <!--规定HTML文档应该使用哪种字符编码-->
    <title>文档的标题</title>
</head>
<body>
  <h1>我是一级标题</h1>  <!--h标签是head的缩写-->
  <p>我是一个<br />段落</p>  <!--p标签是paragraph的缩写-->   <!--br标签（强制换行）是break的缩写,是个单标签,只有一个-->
  我是一个<strong>加粗</strong>文字  <!--strong标签是个文字加粗标签-->
  我是一个<em>倾斜</em>文字  <!--em标签是个文字倾斜标签-->
  我是一个<del>删除线</del>  <!--del标签是个删除线标签-->
  我是一个<ins>下划线</del>  <!--ins标签是个下划线标签-->

  <div>我是div</div>  <!--div标签是division的缩写,表示分割、分区-->
  <span>我是span</span>  <!--span意思为跨距跨度的意思-->
    第一个HTML
</body>
</html>
```

## 表格标签
```html
<!--
基本语法：
<table>
   <tr>
     <th>姓名</th>
   <tr>
     <td>小李</td>
   </tr>
</table>

1.<table></table> 用于定义表格的标签
2.<tr></tr>标签用于定义表格中的行,必须嵌套在<table></table>中
3.<td></td>标签用于定义表格中的单元格,必须嵌套在<tr></tr>中
4.<th></th>标签一般用于表格的第一行第一列,与td单元格的区别是内容加粗居中显示

table标签属性:(实际开发不常用,一般使用CSS来设置,了解即可)
align   left、center、right  规定表格相对周围元素的对齐方式
border  1或者”“  规定表格单元是否有边框,默认为"",没有边框
cellpadding  像素值  规定单元边沿与其内容之间的空白,默认1像素
cellspacing  像素值  规定单元格之间的空白,默认2像素
width   像素值或百分比  规定表格的宽度
-->
```

