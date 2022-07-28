<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [HTML](#html)
  - [常用标签](#%E5%B8%B8%E7%94%A8%E6%A0%87%E7%AD%BE)
    - [例子](#%E4%BE%8B%E5%AD%90)
  - [表格标签](#%E8%A1%A8%E6%A0%BC%E6%A0%87%E7%AD%BE)
  - [列表标签](#%E5%88%97%E8%A1%A8%E6%A0%87%E7%AD%BE)
    - [无序列表（重要）](#%E6%97%A0%E5%BA%8F%E5%88%97%E8%A1%A8%E9%87%8D%E8%A6%81)
    - [有序列表（理解）](#%E6%9C%89%E5%BA%8F%E5%88%97%E8%A1%A8%E7%90%86%E8%A7%A3)
    - [自定义列表（重点）](#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%88%97%E8%A1%A8%E9%87%8D%E7%82%B9)
  - [表单标签](#%E8%A1%A8%E5%8D%95%E6%A0%87%E7%AD%BE)
    - [表单元素input](#%E8%A1%A8%E5%8D%95%E5%85%83%E7%B4%A0input)
    - [label标签](#label%E6%A0%87%E7%AD%BE)

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
   </tr>
   <tr> 
     <td>小李</td>
   </tr>
</table>

1.<table></table> 用于定义表格的标签
2.<tr></tr>标签用于定义表格中的行,必须嵌套在<table></table>中
3.<td></td>标签用于定义表格中的单元格,必须嵌套在<tr></tr>中
4.<th></th>标签一般用于表格的第一行第一列的单元格,与td单元格的区别是内容加粗居中显示

table标签属性:(实际开发不常用,一般使用CSS来设置,了解即可)
align   left、center、right  规定表格相对周围元素的对齐方式
border  1或者""  规定表格单元是否有边框,默认为"",没有边框
cellpadding  像素值  规定单元边沿与其内容之间的空白,默认1像素
cellspacing  像素值  规定单元格之间的空白,默认2像素
width   像素值或百分比  规定表格的宽度


<table>
  <thead>
   <tr>
     <th>姓名</th>
   <tr>
  <thead>
  <tbody>  
   <tr>   
     <td>小李</td>
   </tr>
  <tbody> 
</table>

1.<thead></thead> 用于定义表格的头部区域,内部必须拥有tr标签,位于第一行
2.<tbody></tbody> 用于定义表格的主体区域,主要用来存放数据本体


合并单元格：
跨行合并（rowspan="合并单元格个数"）
跨列合并（colspan="合并单元格个数"）
步骤：
1.先确定是跨行还是跨列
2.找到目标单元格,写上合并方式=合并的单元格数量. 比如<td colspan="2">  </td>
3.删除多余的单元格
-->
```

## 列表标签

### 无序列表（重要）
```html
<ul>
  <li>第一项</li>
  <li>第二项</li>
  <li>第三项</li>
</ul>

<!--
<ul></ul> 标签表示无序列表
<li></li> 标签表示列表项

1.无序列表的各个列表项之间没有顺序级别之分,是并列的
2.<ul></ul>只能嵌套<li></li>,直接在<ul></ul>标签中输入其他标签或者文字的做法是不允许的
3.<li></li>之间相当于一个容器,可容纳所有元素
-->
```

### 有序列表（理解）
```html
<ol>
  <li>第一项</li>
  <li>第二项</li>
  <li>第三项</li>
</ol>

<!--
  和无序列表差不多
-->
```

### 自定义列表（重点）
```html
<dl>
  <dt>名词1</dt>
  <dd>名词1解释1</dd>
  <dd>名词1解释2</dd>
</dl>

<!--
<dl></dl> 标签表示自定义列表
<dt></dt> 标签表示定义项目或者名字
<dd></dd> 标签表示描述每一个项目/名字  
-->
```

## 表单标签
```html
<!--
表单=表单域+表单控件+提示信息（三个组成）

一、表单域
<form>标签用于定义表单域,以实现用户信息的收集和传递。<form>会把范围内的表单元素信息提交给服务器

<form action="url地址"  method="提交方式"  name="表单域名称">
   ....各种表单控件
</form>    

属性：
action  url地址  用于指定接收和处理表单数据的服务器url地址
method  get/post 用于设置表单数据的提交方式
name  名称    用于指定表单的名称,以区分同一个页面的多个表单域
-->
```

### input标签
```html
<!--
表单元素<input>标签用于收集用户的信息

<input type="属性值">
type属性不同值用来指定不同的控件类型
type属性值：
text 定义单行的输入字段,用户可以在其中输入文本。默认20个字符
password 定义密码字段。该字段中的字符被掩码。
radio 定义单选按钮
checkbox 定义多选框
submit 定义提交按钮,提交按钮会把表单数据发送给服务器
reset 定义重置按钮,重置按钮会清除表单类的所有数据
button 定义可点击按钮（多数情况下,用于通过JavaScript启动脚本）
file  定义输入字段和浏览按钮,供文件上传.

input属性：（除type属性外）
name    由用户自定义  定义input元素的名称
value   由用户自定义  规定input元素的值
checked  checked     规定此input元素首次加载时应被选中
maxlength 正整数     规定输入的字段中的字符的最大整数
name和value是每个表单元素都有的属性值,主要给后台人员使用
name表单元素的名字,要求单选框和复选框要有相同的name值
-->
```

### label标签
```html
<!--
<label>标签用于绑定一个表单元素,当点击<label>标签的文本时,浏览器会自动将焦点(光标)转到或者选择对应的表单元素上,用来增加用户体验  
-->
```
