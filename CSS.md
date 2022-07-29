# CSS

## 入门
```css
/* css的基础 */

h1 {
  color: red; 
  font-size: 12px
}

/*
CSS规则主要由两部分组成：选择器以及一条或者多条声明

1.选择器用于指定CSS样式的HTML标签,花括号内是对该对象设置的具体样式
2.属性和属性值是以键值对的形式出现
3.属性是对指定对象设置的样式属性,例如字体大小,字体颜色等
4.属性和属性值之间用英文的":"隔开
5.多个键值对之间用英文的";"隔开
*/
```

## 引入方式

### 内部样式表（嵌入式）
```css
/*
内部样式表是写到html内部,是将所有CSS代码抽取出来,单独放到<style>标签中去

1.理论是可以放到HTML的任意位置,一般是放在<head>标签里面
2.此种方式,可以方便控制当前整个页面中的元素样式设置
3.代码结构清晰,但是结构和样式并没有完全分离
4.这种方式一般是练习时候使用,不推荐
*/
```

#### 例子
```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>内部样式表</title>
    <style>
            div {
                color: pink;
            }
     </style>
</head>
<body>
    <div>所谓内部样式表,就是在html页面内部写样式,但是是单独写到style标签内部.</div>
</body>
</html>
```

### 行内样式表（行内式）
```css
/*
行内样式表是在元素标签内部的style属性中设定CSS样式.适用于简单修改样式

1.style其实就是标签的属性
2.在双引号中间,写法要符合CSS样式
3.可以控制当前的标签设置样式
4.不推荐大量使用,只有对当前元素添加简单样式的时候,可以考虑使用
*/
```

#### 例子
```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>行内样式表</title>
</head>
<body>
        <p>夏天夏天悄悄过去留下小秘密</p>

        <p>压心底压心底不能告诉你</p>
        
        <p> 晚风吹过温暖我心底我又想起你</p>
        
        <p> 多甜蜜多甜蜜怎能忘记</p>
        
        <p>不能忘记你把你写在日记里</p>
        
        <p>不能忘记你心里想的还是你</p>
        
        <p>浪漫的夏季还有浪漫的一个你</p>
        
        <p style="color: pink; font-size: 20px;">给我一个粉红的回忆</p>
</body>
</html>
```

### 外部样式表（链接式）
```css
/*
实际开发都是外部样式表,核心是：样式单独写道CSS中,之后把CSS文件引入到HTML中使用

引入外部样式表步骤：
步骤一：新建一个后缀名为.css的样式文件,把所有CSS代码都放到此文件中
步骤二：在HTML页面中,使用<link>标签引入这个文件,
<link rel="stylesheet"  href="css路径">
*/
```

## 选择器

### 标签选择器
```css
/*
标签选择器是指用HTML标签名称作为选择器,按标签名称分类,为页面中某一类标签指定统一的CSS格式

语法：
标签名{
  属性1：属性值1;
  属性2：属性值2;
  属性3：属性值3;
}
*/
```

#### 例子
```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基础选择器之标签选择器</title>
    <style>
    /* 标签选择器 : 写上标签名 */
    p {
        color: green;
    }
    div {
        color: pink;
    }
    </style>
</head>
<body>
    <p>男生</p>
    <p>男生</p>
    <p>男生</p>
    <div>女生</div>
    <div>女生</div>
    <div>女生</div>
</body>
</html>
```

### 类选择器
```css
/*
类选择器是指可以选一个或多个标签
类选择器在HTML中以class属性表示,在CSS中,类选择器以一个点"."号显示

语法：
.类名{
  属性1：属性值1;
  属性2：属性值2;
}

注意：
1.类选择器使用"."来标识,后面紧跟类名（自定义的名称）
2.可以理解为给这个标签起一个名字
3.长名称或词组可以使用中横线为选择器命名
4.不要使用纯数字、中文等命名,尽量使用英文字母来表示
5.命名要有意义,尽量是别人一眼就能知道这个类名的含义.

类选择器(多类名)
<div class="red font">你好</div>
1.在属性class中写多个类名
2.多个类名中间使用空格隔开
使用场景：
1.可以把一些标签元素相同的的样式（共同的部分）放到一个类里面
2.这些标签都可以调用这个公共的类,然后再调用自己独有的类
*/
```

#### 例子
```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基础选择器之类选择器</title>
    <style>
        /* 类选择器口诀: 样式点定义  结构类(class)调用  一个或多个 开发最常用*/
      .red {
          color: red;
      }
      .star-sing {
        color: green;
      }
      .memeda {  
         color: pink;
      }
    </style>
</head>
<body>
    <ul>
        <li class="red">冰雨</li>
        <li class="red">来生缘</li>
        <li>李香兰</li>
        <li class="memeda">生僻字</li>
        <li class="star-sing">江南style</li>
    </ul>
    <div class="red">我也想变红色</div>
</body>
</html>

/*  多类名的使用场景*/
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>利用类选择器画三个盒子</title>
    <style>
        .box {
            width: 150px;
            height: 100px;
            font-size: 30px;
        }
        .red {
        
            /* 背景颜色 */
            background-color: red;
        }
        .green {
           
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="box red">红色</div>
    <div class="box green">绿色</div>
    <div class="box red">红色</div>
</body>
</html>
```

### id选择器
```css
/*
id选择器可以为标有特定id的HTML元素指定特定的样式
HTML元素以id属性来设置id选择器,CSS中id选择器以"#"来定义

语法：
#id名{
  属性:属性值;
  ......
}

id选择器和类选择器的区别：
1.类选择器好比人的名字,一个人可以有多个名字,同时一个名字可以被多个人使用
2.id选择器好比人的身份证号码,全中国是唯一的,不能重复.
3.id选择器和类选择器最大不同是在使用次数上.
4.类选择器在修改样式上使用的最多,id选择器一般用于唯一性的元素上,经常和JavaScript配合使用
*/
```

#### 例子
```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基础选择器之id选择器</title>
    <style>
        /* id选择器的口诀: 样式#定义, 结构id调用, 只能调用一次, 别人切勿使用 */
      #pink {
          color: pink;
      }
    
    </style>
</head>
<body>
    <div id="pink">迈克尔·杰克逊</div>
    <div>pink老师</div>
</body>
</html>
```

### 通配符选择器
```css
/*
通配符选择器使用"*"定义,他表示获取页面所有元素(标签)

语法：
* {
  属性:属性值;
  ......
}
1.通配符不需要调用,自动就给所有元素使用样式
2.特殊情况下使用
*/
```

## 属性

### 字体属性
```css
/*

字体的复合属性：
body{
  font:font-style font-weight font-size/line-height font-family;
}
注意点：
1.使用font属性时,必须按照上面的语法格式的顺序书写,不能跟换顺序,并且各个属性间以空格隔开
2.不需要设置的属性可以省略,单必须保留font-size和font-family属性,否则font属性不起作用
*/
```

#### 例子
```css
/* 设置字体 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS字体属性之字体系列</title>
    <style>
     h2 {
         font-family: '微软雅黑';
     }
     p {
        /* font-family: 'Microsoft YaHei', Arial, Helvetica, sans-serif; */
        font-family: 'Times New Roman', Times, serif;
     }
    </style>
</head>
<body>
    <h2>pink的秘密</h2>
    <p>那一抹众人中最漂亮的颜色,</p>
    <p>优雅,淡然,又那么心中清澈.</p>
    <p>前端总是伴随着困难和犯错,</p>
    <p>静心,坦然,攻克一个又一个.</p>
    <p>拼死也要克服它,</p>
    <p>这是pink的秘密也是老师最终的嘱托.</p>
</body>
</html>

/* 设置字体大小 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS字体属性之字体大小</title>
    <style>
        body {
            font-size: 16px;
        }
        /* 标题标签比较特殊,需要单独指定文字大小 */
        h2 {
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h2>pink的秘密</h2>
    <p>那一抹众人中最漂亮的颜色,</p>
    <p>优雅,淡然,又那么心中清澈.</p>
    <p>前端总是伴随着困难和犯错,</p>
    <p>静心,坦然,攻克一个又一个.</p>
    <p>拼死也要克服它,</p>
    <p>这是pink的秘密也是老师最终的嘱托.</p>
</body>
</html>

/* 设置字体粗细 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS字体属性之字体大小</title>
    <style>
       .bold {
           /* font-weight: bold; */
           /* 这个700 的后面不要跟单位  等价于 bold 都是加粗的效果 */
           /* 实际开发中,我们跟提倡使用数字 表示加粗或者变细 */
           font-weight: 700;    
       }
       h2 {
           font-weight: 400;   
           /* font-weight: normal;    */
       }
    </style>
</head>
<body>
    <h2>pink的秘密</h2>
    <p>那一抹众人中最漂亮的颜色,</p>
    <p>优雅,淡然,又那么心中清澈.</p>
    <p>前端总是伴随着困难和犯错,</p>
    <p>静心,坦然,攻克一个又一个.</p>
    <p class="bold">拼死也要克服它,</p>
    <p>这是pink的秘密也是老师最终的嘱托.</p>
</body>
</html>

/* 设置字体风格（倾斜还是正常）*/
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS字体属性之文字样式(风格)</title>
    <style>
      p {
          font-style: italic;
      }
      em {
          /* 让倾斜的字体不倾斜   就是赶紧脉动回来 */
          font-style: normal;
      }
    </style>
</head>
<body>
    <p>同学,上课时候的你</p>
    <em>下课时候的你</em>
</body>
</html>

/* 设置字体复合属性 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS字体属性之复合属性</title>
    <style>
       /* 想要div文字变倾斜 加粗 字号设置为16像素 并且 是微软雅黑 */
       div {
           /* font-style: italic;
           font-weight: 700;
           font-size: 16px;
           font-family: 'Microsoft yahei'; */
           /* 复合属性: 简写的方式  节约代码 */
           /* font: font-style  font-weight  font-size/line-height  font-family; */
           /* font: italic 700 16px 'Microsoft yahei'; */
           font: 20px '黑体';
       }
    </style>
</head>
<body>
   <div>三生三世十里桃花,一心一意百行代码</div>
</body>
</html>
```

### 文本属性
```css
/*
文本属性可定义文本的外观,比如文本的颜色、对齐文本、装饰文本、文本缩进、行间距等
color 文本颜色
text-align 文本对齐属性
text-decoration 装饰器,可以给文本添加下划线、删除线、上划线等,设置none去除下划线
text-indent 文本缩进
line-geight 行间距
*/
```

#### 例子
```css
/* 文本颜色 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS文本外观属性之颜色</title>
    <style>
       div {
           /* color: deeppink; */
           /* color: #cc00ff; */
           color: rgb(255, 0, 255);
       }
    </style>
</head>
<body>
   <div>听说喜欢pink色的男生,都喜欢男人</div>
</body>
</html>

/* 文本对齐 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS文本外观之文字对齐</title>
    <style>
        h1 {
            /* 本质是让h1盒子里面的文字水平居中对齐 */
            /* text-align: center; */
            text-align: right;
        }
    </style>
</head>
<body>
    <h1>居中对齐的标题</h1>
</body>
</html>

/* 文本装饰 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS文本外观之装饰文本</title>
    <style>
       div {
           /* 下划线 */
           /* text-decoration: underline;   */
         /* 删除线 */
           text-decoration: line-through;
           /* 上划线 */
           text-decoration: overline;

       }
       a {
           /* 取消a默认的下划线 */
           text-decoration: none;
           color: #333;
       }
    </style>
</head>
<body>
    <div>粉红色的回忆</div>
    <a href="#">粉红色的回忆</a>
</body>
</html>

/* 文本缩进 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS文本外观之文本缩进</title>
    <style>
        p {
            font-size: 24px;
            /* 文本的第一行首行缩进 多少距离  */
            /* text-indent: 20px; */
            /* 如果此时写了2em 则是缩进当前元素 2个文字大小的距离  */
            text-indent: 2em;  
        }
    </style>
</head>
<body>
        <p>打开北京、上海与广州的地铁地图，你会看见三张纵横交错的线路网络，这代表了中国最成熟的三套城市轨道交通系统。</p>

       <p> 可即使这样，在北上广生活的人依然少不了对地铁的抱怨，其中谈及最多的问题便是拥挤——对很多人而言，每次挤地铁的过程，都像是一场硬仗。更何况，还都是败仗居多。</p>
        
       <p> 那么，当越来越多的二线甚至三线城市迎接来了自己的地铁，中国哪里的地铁是最拥挤的呢？</p>
</body>
</html>

/* 行间距 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS文本外观之行间距</title>
    <style>
       div {
           line-height: 26px;
       }
       p {
           line-height: 25px;
       }
    </style>
</head>
<body>
    <div>中国人</div>
       <p>打开北京、上海与广州的地铁地图，你会看见三张纵横交错的线路网络，这代表了中国最成熟的三套城市轨道交通系统。</p>

       <p> 可即使这样，在北上广生活的人依然少不了对地铁的抱怨，其中谈及最多的问题便是拥挤——对很多人而言，每次挤地铁的过程，都像是一场硬仗。更何况，还都是败仗居多。</p>
        
       <p> 那么，当越来越多的二线甚至三线城市迎接来了自己的地铁，中国哪里的地铁是最拥挤的呢？</p>
</body>
</html>
```