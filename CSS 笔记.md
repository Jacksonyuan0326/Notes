# CSS 笔记

## 1. 基本介绍

### 1.1 什么是CSS

Cascading Style Sheet层叠级联样式表

CSS：表现（美化网页）

字体，颜色，边距，布局，高度，宽度，背景图片，网页定位，网页浮动...

### 1.2 怎么使用CSS

#### 1.2.1（发展史）

CSS1.0

CSS2.0 DIV(块)+CSS，提出HTML和CSS结构分离的思想，网页变得简单			 SEO（搜索引擎简化）

CSS2.1 浮动和定位

CSS3.0 圆角边框，阴影，动画---浏览器兼容性

#### 1.2.2 快速入门

```css
<!--<style>可以编写CSS的代码,每一个声明使用;结尾-->
<!--语法
    选择器{
    
    }-->
  <style>
    h1{
      color: red;
    }
  </style>
```

#### 1.2.3 CSS的优势

1. 内容和表现分离
2. 网页表现结构统一，可以使用复用
3. 样式十分的丰富
4. 建议使用独立html的css的文件
5. 利用SEO，容易被搜索引擎目录

#### 1.2.4 CSS的导入方式

![image-20221204013059473](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221204013059473.png)

```html
<!--行内样式：在标签元素中，编写一个style属性，编写样式即可-->
<h1 style="color: red">Draft01</h1>
```

```html
<!--内部样式<style>可以编写CSS的代码,每一个声明使用;结尾-->
  <style>
    h1{
      color: red;
    }
  </style>
```

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--<style>可以编写CSS的代码,每一个声明使用分号结尾-->
<!--语法
    选择器{

    }-->
  <link rel="stylesheet" href="style.css">
</head>
in css file
    h1{
      color: red;
    }
```

**扩展:**外部样式的两种写法

* 链接式: html

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--<style>可以编写CSS的代码,每一个声明使用分号结尾-->
<!--语法
    选择器{

    }-->
  <link rel="stylesheet" href="style.css">
</head>
```



* 导入式:css2.1  

```html
<head>
    <meta charset="UTF-8">
    <meta name = "keywords" content="Jackson Yuan Website">
    <meta name = "descpition" content="This is the website created by Jackson Yuan, there are some information.">
    <title>Jackson Yuan Website</title>
    <style >
        @import url("../CSS/First draft/style.css");
    </style>
</head>
```



**优先级:** 行内样式>内部样式>外部样式



### 1.3 CSS选择器

#### **1.3.1 作用：**

选择页面上的某一个或者莫一类的元素

#### 1.3.2 选择器

* 标签选择器

```css
<style>
h1{
      color: red;
    }
</style>
```

* 类选择器class: 好处，可以选择多个标签是同一个class，可以复用,多个标签用空格隔开

```css
<h1 class = "red size">
bewteen head
<style>
	 .red{
          color: #026969;
      }
      .size{
          font-size: 40px;
      }
</style>
```

* ID选择器： id必须保证全局唯一

```html
<h1 id = "Jackson">
#Jackson{
    
    }
```

#### 1.3.3 层次选择器

```html
<body>

<p>p1</p>
<p>p2</p>
<p>p3</p>
<ul>
  <li>
    <p>p4</p>
  </li>
  <li>
    <p>p5</p>
  </li>
  <li>
    <p>p6</p>
  </li>
</ul>

</body>
```



#### **1.3.3.1后代选择器：**

在某个元素的后面

```html
  <style>
    body p{
      background: bisque;
    }
  </style>
<body>
    <p></p>
</body>
```

![image-20221109144759873](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221109144759873.png)

1.3.3.2 子选择器,一代

```css
div>p{
    
}
```

![image-20221109144623730](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221109144623730.png)

1.3.3.3 相邻兄弟选择器：当前选中元素向下一个元素

```css
  .active+p{
    background: #0eafaf;
  }
```

1.3.3.4 通用兄弟选择器：当前选中元素向下所有同级元素

```css
  .active~p{
    background: #0eafaf;
  }
```

#### 1.3.4  结构伪类选择器

```html
<body>

<p>p1</p>
<p>p2</p>
<p>p3</p>
<ul>
  <li>
    <p>p4</p>
  </li>
  <li>
    <p>p5</p>
  </li>
  <li>
    <p>p6</p>
  </li>
</ul>

</body>
```



```css
  /*ul的第一个子元素*/
    ul li:first-child{

    }
  /*只选中p1；选中父级元素的第一个child*/
/*选中当前p元素的父级元素，选中父级元素的第一个，并且这个元素是当前元素才会生效*/
    p:nth-child(1){
      
    }
        /* 选中第一个元素 */
        li:first-child{
            background-color: green;
        }
        /* 选中第几个 */
        li:nth-child(1){
            background-color: green;
        }
        /* 选中倒数第几个 */
        li:nth-last-child(4){
            background-color: green;
        }
```

#### 1.3.4 并集选择器

```css
<style>
p,
div,
span{
    
}
</style>
```

#### 1.3.5 交集选择器

```css
    <style>
        p.box{
            color: red;
        }
    </style>
<body>
    <p class="box">这是P标签</p>
    <div class ="box">这是div的标签</div>
    <p></p>
</body>
```

#### 1.3.6 hover伪类选择器

鼠标悬停的生活是红色

```css
        div:hover{
            color:green;
        }
<body>
    <p class="box">这是P标签</p>
    <div class ="box">这是div的标签</div>
    <p></p>
</body>
```

#### 1.3.7Emment语法

![image-20221206124943671](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221206124943671.png)



### 1.4美化网页（文字，阴影，超链接，列表，渐变）



#### 1.4.1 文字样式

##### 1.4.1.1 **字体大小**

font-size(num+px)，默认16px

```css
      p{
          font-size: 30px;
      }
```

##### 1.4.1.2 字体粗细

font-weight(关键字/数字[整百100~900])

```css
      p{
          font-size: 700;
          /*font-size: bold*/
      }
```

##### 1.4.1.3 字体样式

```css
  	 p{
          font-style:italic;
          /*font-size: bold*/
      }
```

##### 1.4.1.4 字体字体

无衬线字体sans-serif,衬线字体serif, 等宽字体monospace

如果用户电脑没有前置的字体，则往后类推

网页都按照无衬线字体展示

```css
p{
    font-family: Airal, sans-serif;
}
```

##### 1.4.1.5 复合属性

```css
p{
    font: italic 700 30px heiti;
}
```

##### 1.4.1.6 文本缩进

```css
p{
    text-indent: 50px;
    text-indent: 2em;/*两个字符的大小*/
}
```

##### 1.4.1.7 文本水平对齐

![image-20221204220910347](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221204220910347.png)

```css
p{
    text-align:right;
}
```

**center可以让哪些元素居中**

1. 文本
2. span标签, a 标签
3. input和img标签

##### 1.4.1.8 文本修饰

![image-20221204221452773](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221204221452773.png)

```css
p{
    text-decoration: underline;
}
```

##### 1.4.1.9 文本行高

```CSS
p{
    line-height: 50px;
    line-height: 1.5;/*字号的1.5倍*/
}
font: style weight size/line-height family;
font: italic 700 60px/2 heiti
```



#### 1.4.2 扩展标签水平居中

```css
div{
    width:100px;
    height:200px;
    background-color:pink;
    margin: 0 auto;
}
```



#### 1.4.3 背景

##### 1.4.3.2 背景颜色

```css
div{
    background-color: red;
    background-color: #ccc;
    background-color: rgba(0,0,0,0.5);
    
}
```

##### 1.4.3.2 背景图片

```css
div{
    background-image: url('');
}
```

##### 1.4.3.3 背景平铺

![image-20221206165848506](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221206165848506.png)

```css
div{
    background-repeat:
}
```

##### 1.4.3.4 背景位置

![image-20221206170432874](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221206170432874.png)

```css
div{
    background-position: center center;/*水平和垂直都居中*/
    background-position: 50px 50px;
}
```

##### 1.4.3.5 背景相关属性连写

```css
div{
    background: pink url('') no-repeat center bottom;/*背景位置的英文单词的顺序是可以颠倒的*/
}
```

##### 1.4.3.6 img标签和背景图片的区别

**重要的写在img里面，不重要或者可以被替代的图片可以写在背景图片里面。**



#### 1.4.4 元素显示模式

##### 1.4.4.1 块级元素

特点：

1. 独占一行（一行只能显示一个）
2. 宽度默认是父元素的宽度，高度默认由内容撑开
3. 可以设置宽高

代表标签：

div, p, h, ul, li, dl, dt, dd, form,  header, nav, footer...

##### 1.4.4.2 行内元素

特点：

1. 一行可以显示多个
2. 宽度和高度默认由内容撑开
3. 不可以设置宽高

代表标签：

a, span, b, u, i, s, strong, ins, em, del...

##### 1.4.4.3 行内块元素

1. 一行显示多个
2. 可以设置宽高

代表标签

input, textarea,button,select

##### 1.4.4.4 元素显示模式转换

目的: 改变标签的

![image-20221207001149419](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221207001149419.png)

```css
```

TIPs：

1. 块级元素一般作为大容器，可以嵌套：文本，块级元素，行内元素，行内块元素（但是p标签种不要嵌套div,p,h等元素）
2. a标签内部可以嵌套任意元素（a里面不能嵌套a标签）

#### 1.4.5 CSS的继承和层叠性

##### 	1. 优先级

​	特性:子元素由默认继承父元素样式的特点（文字控制属性都可以继承）

##### 	2. 层叠性

​	特性：给同一个标签设置不同样式，会层层叠加，共同作用在标签上

​				给同一个标签设置相同的样式，样式会层叠覆盖，最终写在最后的样式会生效

**注意：**当样式冲突时，只有当选择器优先级相同时，才能通过层叠性判断结果

TIPs: alt+shift左键选择可以同事输入

##### 	3. 优先级

不同选择器具有优先级，优先级高的选择器样式会覆盖优先级的低选择器样式

**优先级公式：**

继承<通配符选择器<标签选择器<类选择器<ID选择器<行内样式<!important

选择器的范围越广，他的优先级越低

注意点：

1. ！important写在属性值后面，分号前面
2. ！important不能提升继承的优先级，只要是继承优先级最低！
3. 实际开发中不建议使用！important

#### 1.4.6 权重叠加计算

场景：如果是复合选择器，此时需要通过权重叠加计算方法，判断最终那个选择器优先级最高会生效

（行内选择，ID选择器，类选择器，标签选择器）

相同选择器优先级的时候比较最高选择器的个数

都是继承，谁离的越近，哪个选择器生效

 

### 1.5 盒子模型

#### 1.5.1 盒子模型的介绍

**开发中：从外到内，先宽高背景色，再放内容，调节内容位置，最后控制文字细节**

概念：页面中的每个标签，都可以看作一个盒子，通过盒子的视角更方便进行布局

​			浏览器再渲染网页时，会将网页中的元素看作时一个个的矩形区域，我们也称之为盒子

盒子模型：CSS中规定每个盒子分别由：内容区域(content)，内边距区域(padding)，边框区域(border)，外边距区域(margin)构成，这就是盒子模型

```css
        div.c1 p.c2{
            color: red;
            /*边框线*/
            /*dotted点线
              dashed虚线*/
            border: 1px solid blue;
            /*内边距*/
            padding: 30px;
            /*外边距*/
            margin: 20px;
        }
/*可以被拆分为border-left*/
```

![image-20221207131017422](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221207131017422.png)



```html
    <style>
        .box{
            height: 40px;
            border-top: 3px solid #ff8500;
            border-bottom: 1px solid #edeef0;
        }
        .box a{
            width: 80px;
            height: 40px;
            /* background-color: #edeef0; */
            display: inline-block;
            color:#4c4c4c;
            line-height: 40px;
            font-size: 12px;
            text-decoration: none;
        }
        /* 先宽高背景色，再填内容，设置属性，再去除背景色 */
        .box a:hover{
            color:#edeef0;
            background-color: #ff8400;
        }
    </style>
</head>
<body>
    <div class="box">
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
    </div>
</body>
</html>
```

##### **内边距**

```css
/*四个值: 上 右 下 左*/
/*三个值: 上 左右 下*/
/*两个值：上下 左右*/
```

##### 自动盒子减法

```css
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px soild #000;
            padding: 20px;
            /* 内减模式 */
            /* 变成CSS3的盒子模型，好处：加了border和padding不需要手动减法 */
            box-sizing:border-box;
        }
    </style>
```

```css
    <style>
        div{
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px soild #000;
            margin: 20px;
            /* 内减模式 */
            /* 变成CSS3的盒子模型，好处：加了border和padding不需要手动减法 */
            box-sizing:border-box;
        }
    </style>
```

##### 清除默认间距

需要将padding和margin先设置成0，后续再继续设置

```css
*{
    margin:0;
    padding:0;
}
```

##### 版心居中

```css
*{
    margin:0 auto;
}
```

去掉列表符号

```css
ul{
    list-style:none;
}
```

#### 1.5.2 外边距折叠现象

##### 1.5.2.1合并现象

**垂直布局的块级元素，上下margin会合并,取其中最大的值**

```css
.one{
    margin:50px;
}
.two{
    margin:60px;
}
```

**塌陷现象：** **互相嵌套的块级元素，子元素的margin-top会，导致父元素一起向下移动。**

```css
    <style>
        .father{
            width: 300px;
            height: 300px;
            background-color: blue;

        }
        .son{
            width: 100px;
            height: 100px;
            background-color: green;
            margin-top: 50px;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>
```

![image-20221208011954159](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221208011954159.png)

**行内元素内外边距的问题**如果想要通过margin和padding改变标签的位置，无法生效

```css
        span{
            /* margin: 100px;
            padding: 100px; */
            line-height: 1oopx;
        }       
<!-- 行内的margin-top和bottom不生效
        行内标签的padding-top和bottom不生效 -->
        <span>span</span>
```





### 1.6 浮动

### 1.7 网页动画（特效）

www.3cschool.com/菜鸟教程