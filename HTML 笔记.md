# HTML 笔记

## 1. HTML基础介绍

### 1.1 HTML(Hyper Text Markup Language): 

超文本标记语言（包括文字，图片，音频，视频，动画等）

### 1.2 W3C标准包括

结构化标准语言: HTML,XML,结构用于对网页元素进行整理和分类

表现标准语言: CSS，表现用于设置网页元素的版式，颜色和大小等外观样式，主要指的是CSS

行为标准: DOM,ECMAScript，行为是指网页模型的定义和交互的编写

```html
<!--DOCTTYPE: 告诉浏览器，我们要使用什么规范-->
<!DOCTYPE html>
<!--总标签>
<html lang="en">
<!--head标签代表网页头部-->
<!--快捷键crtl+/-->
<head>
    <!--meta描述性标签，用来描述我们的网站的一些信息-->
     <!--meta一般用来做SEO-->
    <meta charset="UTF-8">
    <!-网页标题-->
    <title>First Website</title>
</head><!--闭合头部文件-->
<body>

</body>
</html>
```

### 1.3网页基本标签

==**包含关系**==和==**并列关系**==

包含关系：

```html
<html>
    <title></title>
</html>
```



并列关系：

```html
<head>
    
</head>
<body>
    
</body>
```



**标题标签**

```html
<h1>一级标签</h1>
```

**段落标签**

```html
<p></p>
```

**换行标签**

```html
<br/>
```

**水平线标签**

```html
<hr/>
```

**字体样式标签**

```html
粗体 <strong></strong> or <b></b> 
斜体 <em></em> or <i></i>
下划线<u></u> or <ins></ins>
删除线<del></del> or <s></s>
```

**注释和特殊符号**

```html
<!--特殊符号-->
空格：空&nbsp;格
&gt; 大于号
&lt; 小于号
&copy; 版权符号

```

### 1.4 图片

```html
<!--../表示上一级目录./同级目录,title表示悬停在图片上的文字-->
<!--只设置一个变量的话会等比例缩放，两个都设置的话可能会损坏比例-->
<img src="../resource/image/Jackson.png" alt="Jackson的头像" title="Jackson" weight = "200" height = "100">

```

### 1.5链接

#### 1.5.1超链接

```html
<!--a+tab直接生成链接标签-->
<!--href: 必填表示要跳到哪个界面-->
<!--ctrl+d: 复制上一行-->
<!--target表示窗口在哪里打开
_blank在新标签页打开
_self在自己标签页打开-->
<a href="https://www.google.ca/"target="_blank">点击跳转到Google</a>
```

#### 1.5.2 锚链接

```html
<!--锚链接-->
<!--1. 需要一个锚标记
    2. 跳转到锚标记
    3. 使用#回到锚标记-->
<!--使用name作为标记-->
<a name = "top">顶部</a>
<!--href可以等于其他界面甚至再加#top-->
<a href="#top">回到顶部</a>
```

#### 1.5.3 功能性链接

```html
<!--功能性链接-->
<!--邮件链接: mail to:
    QQ链接: -->
<a href="mailto:yya216@sfu.ca">点击发送邮件</a>
```

### 1.6 列表

**有序列表，无序列表，自定义列表**

```html
<!--有序列表
    引用范围:问答,试卷-->
<ol>
    <li>Java</li>
    <li>C/C++</li>
    <li>Python</li>
    <li>HTML</li>
    <li>SQL</li>
</ol>
<hr/><br/>
<!--无序列表
    应用范围:导航,侧边栏-->
<ul>
    <li>Java</li>
    <li>C/C++</li>
    <li>Python</li>
    <li>HTML</li>
    <li>SQL</li>
</ul>
<!--自定义列表
    dl:是标签
    dt:是列表名称
    dd:是选项内容
    应用官网:网站底部内容-->
<dl>
    <dt>编程语言</dt>
    <dd>C</dd>
    <dd>Java</dd>
    <dd>Python</dd>
```

### 1.7表格

```html
<!--表格table
    行: tr
    列: td-->
<table border="1px">
    <tr>
        <!--colspan 跨列-->
        <td colspan="4">1-1</td>
        <td>1-2</td>
        <td>1-3</td>
        <td>1-4</td>
    </tr>
    <tr>
        <!--rowspan 跨行-->
        <td rowspan="2">2-1</td>
        <td>2-2</td>
        <td>2-3</td>
        <td>2-4</td>
    </tr>

</table>
```

### 1.8 媒体元素

```html
<!--音频和视频-->
<!--controls控制条   autoplay自动播放-->
    <audio src="../resource/...mp3" controls autoplay></audio>
    <video src="../resource/...mp4" controls autoplay></video>
```

## 2. 页面

### 2.1结构分析

**header:**标题头部区域的内容（用于页面或者页面中的一块区域）

**footer:**标记脚部区域的内容（用于整个页面或者页面中的一块区域）

**section:**Web页面中的一块独立区域

**article:**独立的文章内容

**aside:**相关的内容或者应用（常用于侧边栏）

**nav:**导航类的辅助内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<header><h2>网页头部</h2></header>
<section>网页主体</section>

<footer>网页脚部</footer>
</body>
</html>
```

### 2.2 iframe内联框架

```html
<iframe src="//player.bilibili.com/player.html?aid=55631961&bvid=BV1x4411V75C&cid=97257627&page=10" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

### 2.3 初始表单post和get提交

```html
<!--表单form：用于登录小窗口
    action: 表单提交位置，可以是网站或者请求处理地址
    method： post/get提交方式
    get方式提交：可以在url中看到提交的信息，不安全但是高效
    post方法提交：安全，传输大文件-->
<form action="First%20HTML.html" method="post">
<!--文本输入框 input type= “text”
    密码框 input type  = “password”-->
  <p>名字：<input type ="text" name="username"></p>
  <p>密码：<input type ="password" name="pwd"></p>
<p>
  <input type="submit">
  <input type="reset">
</p>
```

#### 2.3.1表单元素格式

**type：**指定元素的类型。text, password, checkbox, radio单选框, submit, reset, file, hidden, image和button，默认为text

**name：**指定表单元素的名称

**value：**元素的初始值。type为radio时必须指定一个值

**size:** 指定表单元素的初始宽度，当type为text或者password时，表单元素的大小以字符为单位，对于其他类型，宽度以像素为单位

**maxlength:**type为text或者password时，输入的最大字符数

**checked:** type为radio或者checkbox时，指定按钮是否是被选中

#### 2.3.2按钮和多选框

```html
<!--checked表示默认选中-->
    <p>
        <input type = "radio" value ="boy" name = "sex"checked/>男
        <input type="radio" value = "girl" name = "sex"/>女
    </p>
    <p>
        <input type = "checkbox" value="sleep" name = "hobby"/>睡觉
        <input type = "checkbox" value="chat" name = "hobby"/>聊天
        <input type = "checkbox" value="game" name = "hobby"/>游戏
    </p>
```

**按钮**

```html
    <p>
        <input type = "button" name="button1"value="点击转跳">
        <input type = "image" src="...">
    </p>
```

#### 2.3.3列表框文本域和文件域

```html
<!--下拉框，列表框
    option中selected是默认的值-->
    <p>下拉框
        <select name = "列表名称">
            <option value="China">中国</option>
            <option value="India">印度</option>
            <option value="Swiss" selected>瑞士</option>
            <option value="US">美国</option>
        </select>
    </p>
<!--文本域-->
    <p>反馈：
        <textarea name=" comments "  cols = "100" rows = "10">文本内容</textarea>
    </p>
<!--文件域-->
    <p>
        <input type = "file" name="files">
        <input type = "button" name = "upload" value="上传">
    </p>
```

### 2.4 搜索框滑块和简单验证

```html
<!--邮件验证-->
    <p>邮箱：
    <input type="email" name="email">
    </p>
    <!--url验证-->
    <p>网址：
    <input type="url" name="url">
    </p>
    <!--数字验证-->
    <p>网址：
    <input type="number" name="num" max="100" min="0"step="10">
    </p>
<!--滑块-->
    <p>音量<input type = "range" max="100"min="1"step="1"></p>
<!--搜索-->
    <p>搜索:
        <input type="search" name="search">
    </p>
```

### 2.5表单的应用

```html
<!--只读值为admin-->  
<p>名字：<input type ="text" name="username"value="admin"readonly></p>
<!--禁用该按纽-->  
<p>名字：<input type ="text" name="username"value="admin"disabled></p>
<!--隐藏该按纽-->  
<p>名字：<input type ="text" name="username"value="admin"hidden></p>
<!--增强鼠标可用性-->
<p>
    <label for="mark">点击我</label>
    <input type="text" id="mark">
</p>
```

## 3.表单的初级验证

### 3.1为什么要进行表单验证

安全性，方便后端处理

### 3.2表单的验证

```html
    <p>名字：<input type ="text" name="username"placeholder="请输入用户名"required></p>
    <p>邮箱：<input type ="text" name="diyemail"pattern="...."></p>
```

