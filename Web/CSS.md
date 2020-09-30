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

# 样式

### 背景

```css
p {background-color: gray;}
```

### 文本

```css
/**
color:文本颜色
direction：文本方向
letter-spacing：字符间距
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

