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

