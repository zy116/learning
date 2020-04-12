# HTML的补充学习

### 1. meta与base

```
<meta http-equiv="refresh" content="2" >     2秒刷新一次
<base href="https://www.baidu.com" target="_blank">    设置默认跳转地址以及跳转方式
<link rel="icon" sizes="any" mask href="https://www.baidu.com/img/baidu_85beaf5496f291521eb75ba38eacbd87.svg"> 设置title的图标

```

### 2. img

```
<img src="https://www.runoob.com/try/demo_source/planets.gif" alt="行星图" title="行星图" usemap="#planetmap">   引入一张图片
<map name="planetmap">  map绑定这张图片
<area shape="rect" coords="0,0,82,126" //shape还有其他形状，这是方形
href="https://www.runoob.com/try/demo_source/sun.htm" alt="sun"> 可以选择一个区域，进行跳转
</map>
```

### 3. 表单

~~~
1. 表单元素都是用form包裹，fieldset是一个框框，legend是框框的标题
2. label元素的属性for绑定的是id
3. 单选框的name属性一样的话，就是同时只能选一个
~~~

### 4. iframe

~~~
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
在一个页面内部开一个小窗口
~~~

### 6. 块元素与行内元素

1. 块级元素

   ~~~
     <address>...</adderss>   
   
     <center>...</center>  地址文字
   
     h1-h6
   
     <hr>  水平分割线
   
     <p>...</p>  段落
   
     <pre>...</pre>  预格式化
   
     <blockquote>...</blockquote>  段落缩进   前后5个字符
   
     <marquee>...</marquee>  滚动文本
   
     <ul>...</ul>  无序列表
   
     <ol>...</ol>  有序列表
   
     <dl>...</dl>  定义列表
   
     <table>...</table>  表格
   
     <form>...</form>  表单
   
     <div>...</div>
   ~~~

2. 行内元素

   ~~~
     <span>...</span>
   
     <a>...</a>  链接
   
     <br>  换行
   
     <b>...</b>  加粗
   
     <strong>...</strong>  加粗
   
     <img >  图片
   
     <sup>...</sup>  上标
   
     <sub>...</sub>  下标
   
     <i>...</i>  斜体
   
     <em>...</em>  斜体
   
     <del>...</del>  删除线
   
     <u>...</u>  下划线
   
     <input>...</input>  文本框
   
     <textarea>...</textarea>  多行文本
   
     <select>...</select>  下拉列表
   ~~~

   

### 7.自带属性元素

~~~
th {font-weight: bolder; text-align: center }/*默认为表格标题显示，呈现加粗居中状态*/
caption {text-align: center }/*默认为表格标题显示，呈现居中状态*/
body {margin: 8px; line-height: 1.12 }
h1 {font-size: 2em; margin: .67em 0 }
h2 {font-size: 1.5em; margin: .75em 0 }
h3 {font-size: 1.17em; margin: .83em 0 }
h4, p,blockquote, ul, fieldset, form, ol, dl, dir, menu { margin: 1.12em 0 }
h5 {font-size: .83em; margin: 1.5em 0 }
h6 {font-size: .75em; margin: 1.67em 0 }
h1, h2,h3, h4, h5, h6, b,strong { font-weight: bolder }
blockquote{ margin-left: 40px; margin-right: 40px }
i, cite,em,var, address { font-style: italic }
big {font-size: 1.17em }
small,sub, sup { font-size: .83em }
sub {vertical-align: sub }/*定义sub元素默认为下标显示*/
sup {vertical-align: super }/*定义sub元素默认为上标显示*/
table {border-spacing: 2px; }
thead,tbody, tfoot { vertical-align: middle }/*定义表头、主体表、表脚元素默认为垂直对齐*/
td, th {vertical-align: inherit }/*定义单元格、列标题默认为垂直对齐默认为继承*/
ol, ul,dir, menu, dd { margin-left: 40px }
ol {list-style-type: decimal }
ol ul, ulol, ul ul, ol ol { margin-top: 0; margin-bottom: 0 }
~~~

### 8.补充元素

`object`：定义了在文档中嵌入的对象，可以是flash，html，图片

~~~
<object width="400" height="50" data="bookmark.swf"></object>//插入flash
~~~

`embed`：与object用法差不多

~~~
embed width="400" height="50" src="bookmark.swf">
~~~



# H5学习

H5适配ie9以上版本，包含ie9

### 1. 适配低版本

为了给低版本使用h5，在head标签里加

~~~
<!--[if lt IE 9]>
<script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js></script>
<![endif]->
~~~

### 2. 新增input类型

以下属性，如果ie支持，也必须是ie9以上的版本

`color` ：选择颜色表单元素（不支持ie和火狐，Safari） 

`date` ：选择日历表单元素（不支持ie和火狐）

`datetime`：出现选择本地时间表单元素，比date多时分秒（不支持ie，火狐，谷歌）

`datetime-local`：出现选择本地时间表单元素（不支持ie和火狐）

`email`：只允许输入邮箱地址，否则提交时出现提示（不支持Safari）

`month`：选择日历中，只选择到月份（不支持ie和火狐）

`number`：数字才能输入进去，并且提交时可以设定属性约束，不满足出现提示，如max，min（不支持火狐）`range`：滑动条表单元素（不支持火狐）

`search` ：定义搜索框（不支持火狐，ie）暂时不懂啥意思

`tel`：定义电话号码字段（都不支持）

`time`：选择时间表单元素，时分秒（不支持火狐，ie）

`url`：输入网址框，提交时验证（不支持Safari）

`week`：选择每年的第几个星期（不支持火狐，ie）

### 3. 新增元素



### 4. video，audio

1. 使用video方法，如下，仅设置宽度即可等比缩放，controls可以显示出控制条

~~~
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
您的浏览器不支持Video标签。
</video>
~~~

2. video的API

   `play()`：播放视频    `pause()`：暂停视频   `paused`：判断是否暂停  `width`：宽度

### 5. 拖放

实现图片的推动，可以移动到另一标签中

~~~
// 实现从一个div框中拖图片到另一个div中，主要依靠ondrop,ondragover,ondragstart三个方法
<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
    <img src="https://www.runoob.com/try/images/logo.png" alt="图标" id="img1"    draggable="true" ondragstart="drag(event)">
</div>
<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

function drag(e) {
        e.dataTransfer.setData("Text", e.target.id);
    }

    function allowDrop(e) {
        e.preventDefault();
    }

    function drop(e) {
        e.preventDefault();
        var data = e.dataTransfer.getData("Text");
        e.target.appendChild(document.getElementById(data));
    }
~~~

### 6.新增表单元素

1. datalist元素，在输入框中填写，会出现提示，输入框中的list属性必须与datalist的id属性一致

   ~~~
   <form action="">
       <input type="text" name="" id="" list="browsers">
       <datalist id="browsers">
           <option value="ewqiehq"></option>
           <option value="wqeq"></option>
           <option value="qwqeq"></option>
       </datalist>
   </form>
   ~~~

2. keygen元素，用于生成密钥，表单提交时，会生成私钥和公钥，私钥保存在客户端，公钥保存在服务端（暂时没用到）

3. output元素，用于计算或脚本输出

   ~~~
   <form action="" oninput="x.value = Number(a.value)+Number(b.value)">
       <input type="range" id="a">+
       <input type="number" id="b" value="50">=
       <output name="x" for="a b"></output>
   </form>
   ~~~

### 7. 新增表单属性

[详细解析](https://www.runoob.com/html/html5-form-attributes.html)

### 8. 新增语义元素

使用以下元素，同样用适配低版本方法，以下除了figcaption，都是块级元素

`article`：定义独立的元素                 `nav`：定义导航栏的元素                    `aside`：定义侧边栏的元素

`header`：定义头部的元素                   `footer`：定义底部的元素

`figure`,`figcaption`：figure定义独立的流，比如插入的图片。figcaption定义figure的标题，应放置于figure的第一个或最后一个元素

### 9. Web存储

早期时候本地存储使用的是cookie，但是web存储需要更加安全迅速，这些数据不在服务器上，当请求组网站的时候，这些数据就派上用场。web存储数据以键值对存在，只允许该网页进行使用。

1. localStorage对象

   用于长久保存数据，不会过期，需要手动删除

2. sessionStorage对象

   临时存储同一个窗口的数据，关闭时自动删除

常用API

~~~
保存数据：localStorage.setItem(key,value);
读取数据：localStorage.getItem(key);
删除单个数据：localStorage.removeItem(key);
删除所有数据：localStorage.clear();
得到某个索引的key：localStorage.key(index);
~~~

这是图解，各自包含的是存储需要的条件，sessionStorage必须窗口是一致的。localstorage只需要协议ip端口，即特定网站永久保存

![](C:\Users\12864\Desktop\笔记\前端\1.HTML\media\storage.png)

### 10. HTML5数据库，HTML5缓存，web workers ，SSE ，websocket

有时间补充一下  



