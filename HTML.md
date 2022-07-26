<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [基础标签](#%E5%9F%BA%E7%A1%80%E6%A0%87%E7%AD%BE)
  - [例子](#%E4%BE%8B%E5%AD%90)
- [列表标签](#%E5%88%97%E8%A1%A8%E6%A0%87%E7%AD%BE)
  - [例子](#%E4%BE%8B%E5%AD%90-1)
- [表单标签](#%E8%A1%A8%E5%8D%95%E6%A0%87%E7%AD%BE)
  - [例子](#%E4%BE%8B%E5%AD%90-2)
- [表格标签](#%E8%A1%A8%E6%A0%BC%E6%A0%87%E7%AD%BE)
  - [例子](#%E4%BE%8B%E5%AD%90-3)
- [样式和节标签](#%E6%A0%B7%E5%BC%8F%E5%92%8C%E8%8A%82%E6%A0%87%E7%AD%BE)
  - [例子](#%E4%BE%8B%E5%AD%90-4)
- [链接标签](#%E9%93%BE%E6%8E%A5%E6%A0%87%E7%AD%BE)
- [图像标签](#%E5%9B%BE%E5%83%8F%E6%A0%87%E7%AD%BE)
- [音视频标签（H5）](#%E9%9F%B3%E8%A7%86%E9%A2%91%E6%A0%87%E7%AD%BEh5)
- [标签全局属性](#%E6%A0%87%E7%AD%BE%E5%85%A8%E5%B1%80%E5%B1%9E%E6%80%A7)
- [标签事件属性](#%E6%A0%87%E7%AD%BE%E4%BA%8B%E4%BB%B6%E5%B1%9E%E6%80%A7)
  - [Windows事件属性](#windows%E4%BA%8B%E4%BB%B6%E5%B1%9E%E6%80%A7)
  - [Form事件](#form%E4%BA%8B%E4%BB%B6)
  - [Keyboard事件](#keyboard%E4%BA%8B%E4%BB%B6)
  - [Mouse事件](#mouse%E4%BA%8B%E4%BB%B6)
  - [Media事件](#media%E4%BA%8B%E4%BB%B6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
# HTML
## 基础标签

```html
1.<!DOCTYPE> 	定义文档类型。
2.<html>	定义 HTML 文档。
3.<title>	定义文档的标题。
4.<body>	定义文档的主体。
5.<h1> to <h6>	定义 HTML 标题。
6.<p>	定义段落。
7.<br>	定义简单的折行。(是一个独目标记)
8.<hr>	定义水平线。(是一个独目标记)
9.<!--...-->	定义注释。
```

### 例子

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
<p>我的第一个段落。<br>我在下一行</p>
</body>
</html>
```

## 列表标签

```html
<ul>	定义无序列表。
<ol>	定义有序列表。
<li>	定义列表的项目。
<dir>	不赞成使用。定义目录列表。
<dl>	定义定义列表。
<dt>	定义定义列表中的项目。
<dd>	定义定义列表中项目的描述。
```

### 例子

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
    
<ul>
    <li>你好</li>
    <li>hello</li>
</ul>

<ol>
    <li>你好</li>
    <li>hello</li>
</ol>

<!--  分类信息 -->
<dl>
    <dt>lll</dt>
    <dd>我是lll</dd>
    <dt>ddd</dt>
    <dd>我是ddd</dd>
</dl>

</body>
</html>
```

## 表单标签

```html
<form>	定义供用户输入的 HTML 表单。
<input>	定义输入控件。
<textarea>	定义多行的文本输入控件。
<button>	定义按钮。
<select>	定义选择列表（下拉列表）。
<optgroup>	定义选择列表中相关选项的组合。
<option>	定义选择列表中的选项。
<label>	定义 input 元素的标注。
<fieldset>	定义围绕表单中元素的边框。
<legend>	定义 fieldset 元素的标题。
<isindex>	不赞成使用。定义与文档相关的可搜索索引。
<datalist>	定义下拉列表。（H5）
<keygen>	定义生成密钥。(H5)
<output>	定义输出的一些类型。(H5)
```

### 例子

```html
<form action="form_action.asp" method="get">
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>

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

## 表格标签

### 例子

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

## 样式和节标签

```html
<style>	定义文档的样式信息。
<div>	定义文档中的节。  块元素,会单独的占领一行
<span>	定义文档中的节。  行内元素,不会单独的占领一行
<header>	定义 section 或 page 的页眉。（H5）
<footer>	定义 section 或 page 的页脚。(H5)
<section>	定义 section。(H5)
<article>	定义文章。(H5)
<aside>	定义页面内容之外的内容。(H5)
<details>	定义元素的细节。(H5)
<dialog>	定义对话框或窗口。(H5)
<summary>	为 <details> 元素定义可见的标题。(H5)
```

### 例子

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

<div> 标签可以把文档分割为独立的、不同的部分
<div style="color:#00FF00">
  <h3>This is a header</h3>
  <p>This is a paragraph.</p>
</div>
```

## 链接标签

```html
<a>	定义锚。
<link>	定义文档与外部资源的关系。
<nav>	定义导航链接。（H5）
```

## 图像标签

```html
<img>	定义图像。
<map>	定义图像映射。
<area>	定义图像地图内部的区域。
<canvas>	定义图形。配合javascript绘制（H5）
<figcaption>	定义 figure 元素的标题。(H5)
<figure>	定义媒介内容的分组，以及它们的标题。(H5)
```

## 音视频标签（H5）

```html
<audio>	定义声音内容。（H5）
<source>	定义媒介源。(H5)
<track>	定义用在媒体播放器中的文本轨道。(H5)
<video>	定义视频。(H5)
```

## 标签全局属性

```
accesskey	规定激活元素的快捷键。
class	规定元素的一个或多个类名（引用样式表中的类）。
contenteditable	规定元素内容是否可编辑。（H5）
contextmenu	规定元素的上下文菜单。上下文菜单在用户点击元素时显示。(H5)
data-*	用于存储页面或应用程序的私有定制数据。(H5)
dir	规定元素中内容的文本方向。
draggable	规定元素是否可拖动。(H5)
dropzone	规定在拖动被拖动数据时是否进行复制、移动或链接。(H5)
hidden	规定元素仍未或不再相关。(H5)
id	规定元素的唯一 id。
lang	规定元素内容的语言。
spellcheck	规定是否对元素进行拼写和语法检查。(H5)
style	规定元素的行内 CSS 样式。
tabindex	规定元素的 tab 键次序。
title	规定有关元素的额外信息。
translate	规定是否应该翻译元素内容。(H5)
```

## 标签事件属性

### Windows事件属性

应用到<body>标签

```html
onafterprint	script	文档打印之后运行的脚本。（H5）
onbeforeprint	script	文档打印之前运行的脚本。（H5）
onbeforeunload	script	文档卸载之前运行的脚本。(H5)
onerror	script	在错误发生时运行的脚本。（H5）
onhaschange	script	当文档已改变时运行的脚本。（H5）
onload	script	页面结束加载之后触发。
onmessage	script	在消息被触发时运行的脚本。（H5）
onoffline	script	当文档离线时运行的脚本。（H5）
ononline	script	当文档上线时运行的脚本。（H5）
onpagehide	script	当窗口隐藏时运行的脚本。（H5）
onpageshow	script	当窗口成为可见时运行的脚本。（H5）
onpopstate	script	当窗口历史记录改变时运行的脚本。（H5）
onredo	script	当文档执行撤销（redo）时运行的脚本。（H5）
onresize	script	当浏览器窗口被调整大小时触发。（H5）
onstorage	script	在 Web Storage 区域更新后运行的脚本。（H5）
onundo	script	在文档执行 undo 时运行的脚本。（H5）
onunload	script	一旦页面已下载时触发（或者浏览器窗口已被关闭）。（H5）
```

### Form事件

应用到几乎所有 HTML 元素，但最常用在 form 元素中

```html
onblur	script	元素失去焦点时运行的脚本。
onchange	script	在元素值被改变时运行的脚本。
oncontextmenu	script	当上下文菜单被触发时运行的脚本。（H5）
onfocus	script	当元素获得焦点时运行的脚本。
onformchange	script	在表单改变时运行的脚本。（H5）
onforminput	script	当表单获得用户输入时运行的脚本。（H5）
oninput	script	当元素获得用户输入时运行的脚本。（H5）
oninvalid	script	当元素无效时运行的脚本。（H5）
onreset	script	当表单中的重置按钮被点击时触发。HTML5 中不支持。
onselect	script	在元素中文本被选中后触发。
onsubmit	script	在提交表单时触发。
```

### Keyboard事件

```html
onkeydown	script	在用户按下按键时触发。
onkeypress	script	在用户敲击按钮时触发。
onkeyup	script	当用户释放按键时触发。
```

### Mouse事件  

鼠标或类似用户动作触发

```html
onclick	script	元素上发生鼠标点击时触发。
ondblclick	script	元素上发生鼠标双击时触发。
ondrag	script	元素被拖动时运行的脚本。（H5）
ondragend	script	在拖动操作末端运行的脚本。（H5）
ondragenter	script	当元素元素已被拖动到有效拖放区域时运行的脚本。（H5）
ondragleave	script	当元素离开有效拖放目标时运行的脚本。（H5）
ondragover	script	当元素在有效拖放目标上正在被拖动时运行的脚本。（H5）
ondragstart	script	在拖动操作开端运行的脚本。（H5）
ondrop	script	当被拖元素正在被拖放时运行的脚本。（H5）
onmousedown	script	当元素上按下鼠标按钮时触发。
onmousemove	script	当鼠标指针移动到元素上时触发。
onmouseout	script	当鼠标指针移出元素时触发。
onmouseover	script	当鼠标指针移动到元素上时触发。
onmouseup	script	当在元素上释放鼠标按钮时触发。
onmousewheel	script	当鼠标滚轮正在被滚动时运行的脚本。
onscroll	script	当元素滚动条被滚动时运行的脚本。
```

### Media事件

适用于所有 HTML 元素，但常见于媒介元素中，比如 <audio>、<embed>、<img>、<object> 以及 <video>

```html
onabort	script	在退出时运行的脚本。
oncanplay	 script当文件就绪可以开始播放时运行的脚本（缓冲已足够开始时）。（H5）
oncanplaythrough	script当媒介能够无需因缓冲而停止即可播放至结尾时运行的脚本。（H5）
ondurationchange	script	当媒介长度改变时运行的脚本。（H5）
onemptied	script当发生故障并且文件突然不可用时运行的脚本（比如连接意外断开时）。（H5）
onended	script	当媒介已到达结尾时运行的脚本（可发送类似“感谢观看”之类的消息）。（H5）
onerror	script	当在文件加载期间发生错误时运行的脚本。（H5）
onloadeddata	script	当媒介数据已加载时运行的脚本。（H5）
onloadedmetadata	script当元数据（比如分辨率和时长）被加载时运行的脚本。（H5）
onloadstart	script	在文件开始加载且未实际加载任何数据前运行的脚本。（H5）
onpause	script	当媒介被用户或程序暂停时运行的脚本。（H5）
onplay	script	当媒介已就绪可以开始播放时运行的脚本。（H5）
onplaying	script	当媒介已开始播放时运行的脚本。（H5）
onprogress	script	当浏览器正在获取媒介数据时运行的脚本。（H5）
onratechange	script每当回放速率改变时运行的脚本（比如当用户切换到慢动作或快进模式）。（H5）
onreadystatechange	script每当就绪状态改变时运行的脚本（就绪状态监测媒介数据的状态）。（H5）
onseeked	script	当 seeking 属性设置为 false（指示定位已结束）时运行的脚本。（H5）
onseeking	script	当 seeking 属性设置为 true（指示定位是活动的）时运行的脚本。（H5）
onstalled	script	在浏览器不论何种原因未能取回媒介数据时运行的脚本。（H5）
onsuspend	script在媒介数据完全加载之前不论何种原因终止取回媒介数据时运行的脚本。（H5）
ontimeupdate	script当播放位置改变时（比如当用户快进到媒介中一个不同的位置时）运行的脚本。（H5）
onvolumechange	script每当音量改变时（包括将音量设置为静音）时运行的脚本。（H5）
onwaiting	script当媒介已停止播放但打算继续播放时（比如当媒介暂停已缓冲更多数据）运行脚本
```

