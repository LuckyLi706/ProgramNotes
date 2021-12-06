<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [基础](#%E5%9F%BA%E7%A1%80)
  - [基础示例](#%E5%9F%BA%E7%A1%80%E7%A4%BA%E4%BE%8B)
  - [css创建](#css%E5%88%9B%E5%BB%BA)
    - [外部样式表](#%E5%A4%96%E9%83%A8%E6%A0%B7%E5%BC%8F%E8%A1%A8)
    - [内部样式表](#%E5%86%85%E9%83%A8%E6%A0%B7%E5%BC%8F%E8%A1%A8)
    - [内联样式](#%E5%86%85%E8%81%94%E6%A0%B7%E5%BC%8F)
    - [例子](#%E4%BE%8B%E5%AD%90)
- [选择器](#%E9%80%89%E6%8B%A9%E5%99%A8)
  - [派生选择器](#%E6%B4%BE%E7%94%9F%E9%80%89%E6%8B%A9%E5%99%A8)
  - [id 选择器](#id-%E9%80%89%E6%8B%A9%E5%99%A8)
  - [class选择器](#class%E9%80%89%E6%8B%A9%E5%99%A8)
  - [属性选择器](#%E5%B1%9E%E6%80%A7%E9%80%89%E6%8B%A9%E5%99%A8)
  - [例子](#%E4%BE%8B%E5%AD%90-1)
- [块和内联函数](#%E5%9D%97%E5%92%8C%E5%86%85%E8%81%94%E5%87%BD%E6%95%B0)
  - [块级元素(block)特性：](#%E5%9D%97%E7%BA%A7%E5%85%83%E7%B4%A0block%E7%89%B9%E6%80%A7)
  - [内联元素(inline)特性：](#%E5%86%85%E8%81%94%E5%85%83%E7%B4%A0inline%E7%89%B9%E6%80%A7)
  - [块级元素主要有：](#%E5%9D%97%E7%BA%A7%E5%85%83%E7%B4%A0%E4%B8%BB%E8%A6%81%E6%9C%89)
  - [内联元素主要有：](#%E5%86%85%E8%81%94%E5%85%83%E7%B4%A0%E4%B8%BB%E8%A6%81%E6%9C%89)
  - [可变元素(根据上下文关系确定该元素是块元素还是内联元素)：](#%E5%8F%AF%E5%8F%98%E5%85%83%E7%B4%A0%E6%A0%B9%E6%8D%AE%E4%B8%8A%E4%B8%8B%E6%96%87%E5%85%B3%E7%B3%BB%E7%A1%AE%E5%AE%9A%E8%AF%A5%E5%85%83%E7%B4%A0%E6%98%AF%E5%9D%97%E5%85%83%E7%B4%A0%E8%BF%98%E6%98%AF%E5%86%85%E8%81%94%E5%85%83%E7%B4%A0)
  - [CSS中块级、内联元素的应用：](#css%E4%B8%AD%E5%9D%97%E7%BA%A7%E5%86%85%E8%81%94%E5%85%83%E7%B4%A0%E7%9A%84%E5%BA%94%E7%94%A8)
  - [主要用的CSS样式有以下三个：](#%E4%B8%BB%E8%A6%81%E7%94%A8%E7%9A%84css%E6%A0%B7%E5%BC%8F%E6%9C%89%E4%BB%A5%E4%B8%8B%E4%B8%89%E4%B8%AA)
- [样式](#%E6%A0%B7%E5%BC%8F)
    - [背景](#%E8%83%8C%E6%99%AF)
    - [文本](#%E6%96%87%E6%9C%AC)
    - [字体](#%E5%AD%97%E4%BD%93)
    - [链接](#%E9%93%BE%E6%8E%A5)
    - [列表](#%E5%88%97%E8%A1%A8)
    - [表格](#%E8%A1%A8%E6%A0%BC)
    - [轮廓](#%E8%BD%AE%E5%BB%93)
- [盒子模型](#%E7%9B%92%E5%AD%90%E6%A8%A1%E5%9E%8B)
  - [概述](#%E6%A6%82%E8%BF%B0)
  - [内边距](#%E5%86%85%E8%BE%B9%E8%B7%9D)
  - [边框](#%E8%BE%B9%E6%A1%86)
  - [外边距](#%E5%A4%96%E8%BE%B9%E8%B7%9D)
- [定位](#%E5%AE%9A%E4%BD%8D)
  - [相对定位](#%E7%9B%B8%E5%AF%B9%E5%AE%9A%E4%BD%8D)
  - [绝对定位](#%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D)
  - [浮动](#%E6%B5%AE%E5%8A%A8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 基础

## 基础示例

```css
body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
  }
```

## css创建

### 外部样式表

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

### 内部样式表

```
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```

### 内联样式

```
<p style="color: sienna; margin-left: 20px">
This is a paragraph
</p>
```

### 例子

```css
<!--优先级:内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式-->
<html>
<head>
<!--当样式需要应用于很多页面时，外部样式表将是理想的选择,以下是定义方式，2.css在当前文件下-->
<link rel="stylesheet" type="text/css" href="2.css">

<!--当单个文档需要特殊的样式时，就应该使用内部样式表,定义如下-->
<style>
p
{
    text-align:center;
	color:blue;
}
</style>
</head>
<body>
<h4>欢迎光临</h4>
<p>HELLO</p>
<!--由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势。请慎用这种方法-->
<p style="color:red;text-align:center">Hello,World</p>
</body>
</html>
```

# 选择器

## 派生选择器

```css
strong {
     color: red;
     }

h2 {
     color: red;
     }

h2 strong {     //只会对h2标签下的strong标签有效
     color: blue;
     }

<p>The strongly emphasized word in this paragraph is<strong>red</strong>.</p>
<h2>This subhead is also red.</h2>
<h2>The strongly emphasized word in this subhead is<strong>blue</strong>.</h2>
```

## id 选择器

```css
 #dog{     //id选择器是以#开头
        background-color: aqua;
    }
    
 <div class="to">
    <p id="dog">指定具有id元素的样式</p>
```

## class选择器

```css
.center {    //class选择器是以.开通
    text-align: center
    }

<h1 class="center">
This heading will be center-aligned
</h1>

<p class="center">
This paragraph will also be center-aligned.
</p>
```

## 属性选择器

```css
//为带有 title 属性的所有元素设置样式
[title]
{
color:red;
}

//下面的例子为 title="W3School" 的所有元素设置样式：
[title=W3School]
{
border:5px solid blue;
}
```

## 例子

```html
<!--css注释使用/* */的方式-->
<html>
<head>
<title>id和class选择器</title>
<style>
/* p标签使用以下的样式 */
p
{
	color:yellow;
	text-align:center;
}
/* 使用#id的形式来用来给id声明的元素 */
#html
{
    color:red;
	text-align:center;
} 
/* 使用.class的形式来用来给有class声明的元素 */
.html2
{
    color:blue;
	text-align:center;
}
</style>
</head>
<body>
<p>Hello World!</p>
<!--使用id来起个名字，不能以数字开头，只能有一个id-->
<p id="html">Hello,id!</p>
<!--使用class来起个名字，不能以数字开头，可以在多个元素中使用-->
<p class="html2">Hello,class!</p>
</body>
</html>
```

# 块和内联函数

## 块级元素(block)特性：
总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示;
宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制;

## 内联元素(inline)特性：
和相邻的内联元素在同一行;
宽度(width)、高度(height)、内边距的top/bottom(padding-top/padding-bottom)和外边距的top/bottom(margin-top/margin-bottom)都不可改变，就是里面文字或图片的大小;

## 块级元素主要有：
address , blockquote , center , dir , div , dl , fieldset , form , h1 , h2 , h3 , h4 , h5 , h6 , hr , isindex , menu , noframes , noscript , ol , p , pre , table , ul , li

## 内联元素主要有：
a , abbr , acronym , b , bdo , big , br , cite , code , dfn , em , font , i , img , input , kbd , label , q , s , samp , select , small , span , strike , strong , sub , sup ,textarea , tt , u , var

## 可变元素(根据上下文关系确定该元素是块元素还是内联元素)：
applet ,button ,del ,iframe , ins ,map ,object , script

## CSS中块级、内联元素的应用：
利用CSS我们可以摆脱上面表格里HTML标签归类的限制，自由地在不同标签/元素上应用我们需要的属性。

## 主要用的CSS样式有以下三个：
display:block  -- 显示为块级元素
display:inline  -- 显示为内联元素
display:inline-block -- 显示为内联块元素，表现为同行显示并可修改宽高内外边距等属性
我们常将<ul>元素加上display:inline-block样式，原本垂直的列表就可以水平显示了。

# 样式

### 背景

```css
/**
background    简写属性，作用是将背景属性设置在一个声明中。
background-color  设置元素的背景颜色。
background-image  background-image
**/
```

### 文本

```css
/**
color:文本颜色
direction：文本方向
letter-spacing：字符间距
text-align：对齐元素中的文本
word-spacing：字间距
**/
```

### 字体

```css
/**
font：设置所有字体属性
font-family:设置文本字体系列
font-size:设置文本的字体大小
font-style：文本的字体样式
font-weight:字体的粗细
**/

//例子
font:italic bold 12px/30px Georgia, serif;

```

### 链接

```css
/**
a:link - 普通的、未被访问的链接
a:visited - 用户已访问的链接
a:hover - 鼠标指针位于链接的上方
a:active - 链接被点击的时刻

a:hover 必须跟在 a:link 和 a:visited后面
a:active 必须跟在 a:hover后面
**/

例子：
a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */
```

### 列表

```css
/**
list-style	用于把所有用于列表的属性设置于一个声明中。
list-style-image	将图象设置为列表项标志。
list-style-position	设置列表中列表项标志的位置。
list-style-type	设置列表项标志的类型。
**/
```

### 表格

```css
/**
border-collapse	设置是否把表格边框合并为单一的边框。
border-spacing	设置分隔单元格边框的距离。
caption-side	设置表格标题的位置。
empty-cells	设置是否显示表格中的空单元格。
table-layout	设置显示单元、行和列的算法。
**/
```

### 轮廓

```css
/**
轮廓（outline）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。
outline-color	设置轮廓的颜色。	
outline-style	设置轮廓的样式。	
outline-width	设置轮廓的宽度。
**/
```

# 盒子模型

## 概述

<img src="images\css_box_model.png" style="zoom:80%;" />

## 内边距

```css
/**
padding	简写属性。作用是在一个声明中设置元素的所内边距属性。
padding-bottom	设置元素的下内边距。
padding-left	设置元素的左内边距。
padding-right	设置元素的右内边距。
padding-top	设置元素的上内边距。
**/
```

## 边框

```css
/**
border	简写属性，用于把针对四个边的属性设置在一个声明。
border-style	用于设置元素所有边框的样式，或者单独地为各边设置边框样式。
border-width	简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。
border-color	简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。
border-bottom	简写属性，用于把下边框的所有属性设置到一个声明中。
border-bottom-color	设置元素的下边框的颜色。
border-bottom-style	设置元素的下边框的样式。
border-bottom-width	设置元素的下边框的宽度。
border-left	简写属性，用于把左边框的所有属性设置到一个声明中。
border-left-color	设置元素的左边框的颜色。
border-left-style	设置元素的左边框的样式。
border-left-width	设置元素的左边框的宽度。
border-right	简写属性，用于把右边框的所有属性设置到一个声明中。
border-right-color	设置元素的右边框的颜色。
border-right-style	设置元素的右边框的样式。
border-right-width	设置元素的右边框的宽度。
border-top	简写属性，用于把上边框的所有属性设置到一个声明中。
border-top-color	设置元素的上边框的颜色。
border-top-style	设置元素的上边框的样式。
border-top-width	设置元素的上边框的宽度。
**/
```

## 外边距

```css
/**
margin	简写属性。在一个声明中设置所有外边距属性。
margin-bottom	设置元素的下外边距。
margin-left	设置元素的左外边距。
margin-right	设置元素的右外边距。
margin-top	设置元素的上外边距。
**/
```

# 定位

## 相对定位

```css
/**
相对定位是一个非常容易掌握的概念。如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动。

如果将 top 设置为 20px，那么框将在原位置顶部下面 20 像素的地方。如果 left 设置为 30 像素，那么会在元素左边创建 30 像素的空间，也就是将元素向右移动。
**/

#box_relative {
  position: relative;
  left: 30px;
  top: 20px;
}
```

## 绝对定位

```css
/**
绝对定位使元素的位置与文档流无关，因此不占据空间。这一点与相对定位不同，相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。

普通流中其它元素的布局就像绝对定位的元素不存在一样：
**/
#box_relative {
  position: absolute;
  left: 30px;
  top: 20px;
}
```

## 浮动

```css
/**
float属性：
left	元素向左浮动。
right	元素向右浮动。
none	默认值。元素不浮动，并会显示在其在文本中出现的位置。
inherit	规定应该从父元素继承 float 属性的值。
**/
```

