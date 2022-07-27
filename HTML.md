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
span标签也是用来布局的,可以一行放多个,小盒子-->
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


