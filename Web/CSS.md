# CSS的基本属性

### 1、CSS简介

英文全名：cascading style sheets

定义:  层叠样式表,  是WEB标准中的表现标准语言,  表现标准语言在网页中主要对网页信息的显示进行控制，简单说就是如何修饰网页信息的显示样式。

目前推荐遵循的是W3C发布的CSS3.0.
用来表现XHTML或者XML等样式文件的计算机语言。

1998年5月21日由w3C正式推出的css2.0

### 2.css语法

CSS语法：选择符{属性：属性值；属性：属性值；} 

|       属性       |               属性值                |     功能     |
| :--------------: | :---------------------------------: | :----------: |
|    text-align    |        center,  left,  right        | 文字居中格式 |
|    font-size     |                18px                 | 设置文字大小 |
|   font-family    |          微软雅黑,  宋体等          |   设置字体   |
|   font-weight    | normal(默认), bold(粗体), 100px ,等 | 设置字体加粗 |
|    font-style    |     normal(默认), italic(斜体)      | 设置字体样式 |
|      color       |               颜色值                | 设置文字颜色 |
| background-color |               颜色值                | 设置背景颜色 |

### 3.样式的创建

#### (1)  内部样式:

```html
<head>
	<style type="text/css">
        css语句
    </style>
</head>
```

#### (2)  外部样式:

```html
第一种:
<head>
	<link rel="stylesheet" type="text/css" href="目标文件的路径及文件名全称" />
</head>

rel（relation）：用于定义文档关联，表示关联样式表；
type：定义文档类型

第二种:
<head>
    <style type="text/css">
        @import url(目标文件的路径及文件名全称);
    </style>
</head>
注意:a.  @和import之间没有空格 url和小括号之间也没有空格；必须结尾以分号结束
	b.  @import是CSS2.1提出的，所以老的浏览器不支持，@import只有在IE5以上的才能识别，而link标签无此问题。
```

#### (3)内联样式:

```html
语法：<标签 style="属性：属性值;属性:属性值;"></标签>
```

### 4.样式表的优先级

```html
A、内联样式表的优先级别最高
B、内部样式表与外部样式表的优先级和书写的顺序有关，后书写的优先级别高。
```

### 5.css选择器

| 序号 |   选择器    | 语法                                     |
| :--: | :---------: | :--------------------------------------- |
|  1   | 标签选择器  | 标签名称{属性：属性值；}                 |
|  2   |  id选择器   | \#id名{属性：属性值;}                    |
|  3   | class选择器 | .class名{属性：属性值;}                  |
|  4   |   通配符    | *{属性：属性值；}                        |
|  5   | 群组选择器  | 选择符1，选择符2，选择符3{属性：属性值;} |
|  6   | 包含选择器  | 选择符1 选择符2{属性：属性值;}           |
|  7   | 伪类选择器  | 如下 : 注意3                             |

**注意1: class选择器 定义类名称要规范:**    如下表格是常见的命名:

|   部位   |  命名   |
| :------: | :-----: |
|    头    | header  |
|   内容   | content |
|    尾    | footer  |
|   导航   |   nav   |
|  侧边栏  | sidebar |
|   标志   |  logo   |
|   广告   | banner  |
| 页面主体 |  main   |

**注意2 : 包含选择器**选择符之间是用空格隔开,并且选择符1>大于选择符2;
	     而群组选择器选择符之间是用逗号隔开.

#### 注意3.  伪类选择器

```html
语法 ：
a:link{属性：属性值;}超链接的初始状态;
a:visited{属性：属性值;}超链接被访问后的状态;
a:hover{属性：属性值;}鼠标悬停，即鼠标划过超链接时的状态;
a:active{属性：属性值;}超链接被激活时的状态，即鼠标按下时超链接的状态;

例如:
a:hover{color: red;}
a{text-decoration: none;}   /*去掉超链接的下划线*/
```

### 6.css选择器的权重

```html
css中用四位数字表示权重，权重的表达方式如：0，0，0，0
标签选择器的权重为0001
class选择器的权重为0010
id选择器的权重为0100
伪类选择器的权重为0001 
包含选择器的权重：为包含选择符的权中之和
内联样式的权重为1000
!important 语法是提升指定样式条目的应用优先权
```

### 7.浮动属性的应用

**A.  语法:**  float : none / left / right ;

**B.  float:**  定义网页中其它文本如何环绕该元素显示 

**C.  浮动的目的:**  就是让竖着的东西横着来  

**D.  浮动的三个取值:**

```html
left:元素活动浮动在文本左面
right:元素浮动在右面
none:默认值，不浮动。
```

**E.  清除浮动的三种方法 :**

​	a.  语法：.clear{clear:both;}         不常用

​	b.  语法：.clear{overflow:hidden;}       不建议使用

​	c.  语法：最流行、最常用、可兼容所有浏览器 , 开发时推荐使用

```html
clear：after{
	display:block;
	clear:both;
	content:".";
	visibility:hidden;
	height:0;}
clear{zoom:1;} 

牢记:对于CSS的清除浮动(clear)，这个规则只能影响使用清除的元素本身，不能影响其他元素
```

### 8.css文本属性

| 序号 |     功能     |                             语法                             |
| :--: | :----------: | :----------------------------------------------------------: |
|  1   |   文本大小   |                      font-size : value                       |
|  2   |   文本颜色   |                        color : 颜色值                        |
|  3   |   文本字体   |              font-family : 字体1，字体2，字体3               |
|  4   |   文字加粗   | font-weight : bolder(更粗的) / bold（加粗）/ normal（常规）/100—900 |
|  5   |   文字倾斜   | font-style：italic / oblique / normal（取消倾斜，常规显示）  |
|  6   | 水平对齐方式 |              text-align : left / right / center              |
|  7   |   文字行高   |                 line-height : normal / value                 |
|  8   |   文本修饰   | text-decoration : none / underline(添加下划线) / overline / line-through |
|  9   |   首行缩进   |      text-indent : value   (例如:  text-indent : 2em )       |
|  10  |    字间距    |                    letter-spacing : value                    |

**注意: 文字属性可简写**

```html
font属性的简写：字号，行高，字体
font:12px/24px "宋体";
font-size:12px; line-height:24px; font-family:”宋体”;

说明:font的属性值应按以下次序书写(各个属性之间用空格隔开)
顺序: font-style font-weight font-size / line-height font-family
```

### 9.css列表属性

| 序号 |         功能         |                             语法                             |
| :--: | :------------------: | :----------------------------------------------------------: |
|  1   |   定义列表符号样式   | list-style-type：disc(实心圆) / circle(空心圆) / square(实心方块) / none(去掉列表符号)；list-style-type : none===list-style : none; |
|  2   | 使用图片作为列表符号 |       list-style-image：url(所使用图片的路径及全称)；        |
|  3   |  定义列表符号的位置  |     list-style-position : outside(外边) / inside(里边)；     |

### 10.css背景属性

| 序号 |       功能       |                             语法                             |
| :--: | :--------------: | :----------------------------------------------------------: |
|  1   |     背景颜色     |                 background-color : 颜色值 ;                  |
|  2   |  背景图片的设置  |        background-image：url(背景图片的路径及全称)；         |
|  3   | 背景图片平铺属性 | background-repeat : no-repeat(不平铺)/repeat(平铺)/repeat-x(横向平铺)/repeat-y(纵向平铺) ; |
|  4   |   背景图的固定   |     background-attachment : scroll(滚动) / fixed(固定) ;     |
|  5   |  背景图片的位置  | background-position : left / center/right/(水平向上)或数值 top/center/bottom/(水平向下)或数值 |

### 11.css边框属性

| 序号 |                功能                 |                             语法                             |
| :--: | :---------------------------------: | :----------------------------------------------------------: |
|  1   | border : 边框宽度 边框风格 边框颜色 |                    border : 5px solid red                    |
|  2   |           边框圆角(倒角)            |                     border-radius : 25px                     |
|  3   |              边框阴影               |             box-shadow : 10px 10px 5px #888888;              |
|  4   |              边框样式               |          border-style :  solid(实线)/  dashed(虚线)          |
|  5   |            单独设置各边             | border-top-style : dotted ;  border-right-style : solid ; border-bottom-style : dotted ;  border-left-style : solid; |
|  6   |              边框宽度               |                     border-width : 20px                      |

#### 补充 : 锚点连接

```html
1.<dt><a href="#step1">HTML标签</a></dt>
2.<p id="top"></p>
3.<p id="step1">
4.<a href="#top">回到顶部</a>

执行效果: 点击4跳转到2, 点击1跳转到3.
```