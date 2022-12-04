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

##### **1.3.1 作用：**

选择页面上的某一个或者莫一类的元素

##### 1.3.2 选择器

* 标签选择器

```css
<style>
h1{
      color: red;
    }
</style>
```

* 类选择器class: 好处，可以选择多个标签是同一个class，可以复用

```css
<h1 class = "Jackson">
bewteen head
<style>
.Jackson{
    
}
</style>
```

* ID选择器： id必须保证全局唯一

```html
<h1 id = "Jackson">
#Jackson{
    
    }
```

##### 1.3.3 层次选择器

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



**1.3.3.1后代选择器：**在某个元素的后面

```html
  <style>
    body p{
      background: bisque;
    }
  </style>
```

![image-20221109144759873](C:\Users\11358\AppData\Roaming\Typora\typora-user-images\image-20221109144759873.png)

1.3.3.2 子选择器,一代

```css

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

##### 1.3.4  结构伪类选择器

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
```

##### 1.4 属性选择器



### 1.4美化网页（文字，阴影，超链接，列表，渐变）

### 1.5 盒子模型

### 1.6 浮动

### 1.7 网页动画（特效）

www.3cschool.com/菜鸟教程