## 第一个html

```html
<!--
<!DOCTYPE html> 声明为 HTML5 文档
<html> 元素是 HTML 页面的根元素
<head> 元素包含了文档的元（meta）数据，如 <meta charset="utf-8"> 定义网页编码格式为 utf-8。
<title> 元素描述了文档的标题
<body> 元素包含了可见的页面内容
 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>第一个html</title>
</head>
<body>
<h1>我的第一个标题</h1>
<p>我的第一个段落。</p>
</body>
</html>
```

## 标签

### 通用属性

- class（规定元素的一个或多个类名（引用样式表中的类）。）
- id（规定元素的唯一id）
- style（规定元素的行内CSS样式）

### 基础类

#### 标题标签

```
<h1> - <h6>
<h1>This is a heading</h1>
<h2>This is a heading</h2>
<h3>This is a heading</h3>
```

#### 段落标签

```
<p>
<p>This is a paragraph.</p>
```

### 样式类

### 列表类

#### 无序列表标签

```
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>
```

#### 有序列表标签

```
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```

#### 自定义列表

```
<dl>
<dt>Coffee</dt>
<dd>Black hot drink</dd>
<dt>Milk</dt>
<dd>White cold drink</dd>
</dl>
```

### 表单类

#### 表单标签

```html
<form action="form_action.asp" method="get">
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>
```

#### 输入标签

```html
<!--
type属性：
button    //按钮
checkbox  //单选框
file      //文件
hidden
image     //图片
password  //密码输入框
radio     //音频
reset
submit    //提交
text      //输入框
-->

<!-- 
type为submit，提交按钮
value属性为按钮显示的值
-->
<input type="submit" value="提交" />
```

#### 下拉选择标签

```html
<!--下拉选择,下面展示的拥有四个选择框
name属性用于提交到后台的识别
-->
<select name=“select”>
  <option value ="volvo">Volvo</option>
  <option value ="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select>
```

### 表格类

```html
<table border="1" style="border-collapse: collapse;">
  <caption>这是表格的标题</caption>
  <tr>
     <th>名称</th>
     <th>官网</th>
     <th>性质</th>
  </tr>
   <tr>
     <td>C语言中文网</td>
     <td>http://c.biancheng.net/</td>
     <td>教育</td>
  </tr>
  <tr>
     <td></td>
     <td>http://www.baidu.com/</td>
     <td>搜索</td>
  </tr>
  <tr>
      <td>当当</td>
     <td>http://www.dangdang.com/</td>
      <td>图书</td>
  </tr>
</table>
```

### 样式/节类

#### 样式标签

```html
<html>
<head>
<style type="text/css">
h1 {color:red}
p {color:blue}
</style>
</head>

<body>
<h1>Header 1</h1>
<p>A paragraph.</p>
</body>
</html>
```

#### 分区标签

```html
<div> 标签可以把文档分割为独立的、不同的部分
<div style="color:#00FF00">
  <h3>This is a header</h3>
  <p>This is a paragraph.</p>
</div>
```



### 链接类

#### 链接标签

```
<a>标签
<a href="http://www.w3school.com.cn">This is a link</a>

<link href="">是指引入css文件
```

### 图像类

#### 图像标签

```
<img>
<img src="w3school.jpg" width="104" height="142" />
```