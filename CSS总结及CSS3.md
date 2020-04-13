### 1. 块与行内

1. 块：默认宽度100%，可以设置长度高度

2. 行内块：可以设置长度高度，默认跟文字同长

3. 行内元素：不能设置长度高度，跟文字同长

### 2. 浮动与清除浮动

1. 浮动，绝对定位，固定定位可以转换为行内块，所以本身要加这些语句就不用写 display：block，就可以直接	给宽度高度

2. 设置浮动时，框框就不占位置了，但是里面东西如文字图片还会占位置，其他框框就会顶上位置，但是就会被文字或图片挤开。

3. clear：left 设置了这个属性的框框左边就不允许存在浮动元素，所以如果存在，这个框框会下移。

#### 让宽度自适应浏览器的方法：

``` 
{
position:absolute;
height:1
}
```

#### 高度塌陷与BFC

1. 高度塌陷：父元素包含了子元素，并且父元素没有设置高度，是被子元素撑开的，如果子元素脱离文档流，那么父元素高度就会塌陷为零，

   **解决方法：**
   
   - 触发BFC,(最好方法:设置overflow：hidden)
   - 在父元素最后添加一个空白div
   - 在父元素使用一个after伪类，对其清除浮动，与2类似。
     content："”，display：block，clear：both

2. **BFC **:Block Formatting Context  "块级格式化上下文"

	**-- 开启BFC的时候的特性**
	
	- 内部的Box会在垂直方向，一个接一个地放置。
	- Box垂直方向的距离由margin决定。**属于同一个BFC的两个相邻Box的margin会发生重叠。**
	- 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
	- BFC的区域不会与float box重叠。
	- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
	- 计算BFC的高度时，浮动元素也参与计算。
	
	**-- BFC的开启方法**
	
	- 设置float
	- 设置overflow非visible
	- 设置position：absolute或fixed
	- 设置display：inline-block
3. **解决外边距重叠办法**

   - 底部元素设置为浮动 float:left;
   - 底部元素的position的值为absolute/fixed
   - 在设置margin-top/bottom值时统一设置上或下

   **注：对于父子垂直外边距重叠解决方法：**

   * 父元素添加padding

   * 父元素 overflow:hidden;

   * 父元素透明边框 border:1px solid transparent;

   * 父元素绝对定位 postion:absolute:

   * 子元素 加float:left;或display:inline-block; 触发BFC(只有这两个属性可以通过子元素触发BFC防止塌陷)

### 3.  伪类和伪元素

下列中，孩子，lang是伪类选择，其余是伪元素

~~~
:link	        a:link	    	  选择所有未访问链接
:visited	    a:visited		  选择所有访问过的链接
:active  	    a:active		  选择正在活动链接
:hover  	    a:hover			  把鼠标放在链接上的状态
:focus      	input:focus	      选择元素输入后具有焦点
:first-letter	p:first-letter    选择每个<p> 元素的第一个字母
:first-line	    p:first-line	  选择每个<p> 元素的第一行
:first-child    p:first-child	  选择器匹配含p的父元素的第一个子元素的是 <p> 的元素
:nth-child      p:nth-child(2)    选择器匹配含p的父元素的第n个子元素的是 <p> 的元素
:before	        p:before		  在每个<p>元素之前插入内容
:after	        p:after			  在每个<p>元素之后插入内容
:lang(language)	p:lang(it)		  为<p>元素的lang属性选择一个开始值
~~~

其中，链接伪类是之前就有，孩子伪类，before，after是css3

css3中规定：`:`表示伪类 `::`表示伪元素

### 4.表单元素补充

1. 单选框的用法

   ~~~
   <form>
   		//label可以设置内容与框绑定，name属性相同，用来单选
           <input type="radio" id="aaa" name="name">
           <label for="aaa">ada</label>
           <input type="radio" id="bbb" name="name">
           <label for="bbb">ada</label>
   </form>
   ~~~

### 5. 补充

`li+li：before{}`：意思是给相邻的li之间加元素

如：在两个li之间添加一个斜杆

~~~
 li+li:before {
    padding: 8px;
    color: black;
    content: "/\00a0";
}
~~~

### 6. css3

#### 1. 边框

- border-radius
- box-shadow 
- border-image

#### 2. 背景

- background-image  允许有多个图像，简写用逗号分开

~~~
background: url(img_flwr.gif) right bottom no-repeat, url(paper.gif) left top repeat;
~~~

- background-origin

~~~
background-origin:border-box;
background-origin:padding-box;
background-origin:content-box;
~~~

- background-clip属性 

在什么地方加背景，border：从边框开始 padding：从内边距开始  content：从内容开始

~~~
background-clip:border-box;
background-clip:padding-box;
background-origin:content-box;
~~~

- background-size 

#### 3. 渐变

默认从上到下渐变

- 线性渐变

~~~
background: linear-gradient(direction, color-stop1, color-stop2, ...);
如：
background: linear-gradient(to bottom right, red, yellow);

//10%表示红色占据的中心在左上开始的10%位置 后面40%指黄色中心位置，小于前面的会被覆盖
background: linear-gradient(to bottom right, red 10%, yellow 40%);

重复的线性渐变，以下可以表示20%以内渐变，重复5次
background: repeating-linear-gradient(red, yellow 10%, green 20%);
~~~

- 使用角度

~~~
background: linear-gradient(angle, color-stop1, color-stop2);
如：
background: linear-gradient(-90deg, red, yellow)；
~~~

- 使用透明度

~~~
 background: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1));
~~~

- 径向渐变

~~~
background: radial-gradient(shape size at position, start-color, ..., last-color);
如：指中心点在中上部，往外扩散，220%往左右，105往上下
background: radial-gradient(220% 105% at top center, #1b2947 10%, #75517d 40%, #e96f92 65%, #f7f7b6);
~~~

#### 4. 文本效果

- text-shadow

- box-shadow

水平阴影，垂直阴影，模糊的距离，以及阴影的颜色：

~~~
text-shadow: 5px 5px 5px #FF0000;
box-shadow: 10px 10px 5px #888888;
~~~

- text-overflow

~~~
text-overflow: clip|ellipsis|string; //修剪|用省略号代替多余|用字符串代替多余
~~~

- word-wrap
- word-break

#### 5. 2D转换

**transform属性**，属性值如下：

- translate(水平移动距离，垂直)：移动到括号内位置 也有translateX/Y(距离)
- rotate(角度如：30deg)：原地顺时针旋转30度
- scale(宽倍数，高倍数)：原位置缩放   scaleX/Y(倍数)
- skew(水平角度，垂直角度)：原位置倾斜  skewX/Y(角度) 变成平行四边形
- matrix()：有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。

#### 6. 3D转换

可以进行3D变换

| 属性                   | 描述                                 | CSS  |
| :--------------------- | :----------------------------------- | :--- |
| transform              | 向元素应用 2D 或 3D 转换。           | 3    |
| transform-origin       | 允许你改变被转换元素的位置。         | 3    |
| transform-style        | 规定被嵌套元素如何在 3D 空间中显示。 | 3    |
| perspective            | 规定 3D 元素的透视效果。             | 3    |
| **perspective-origin** | 可以设置旋转轴                       | 3    |
| backface-visibility    | 定义元素在不面对屏幕时是否可见。     | 3    |

#### 7. 过渡

**transition属性**，有四个值。设定之后，要想有变化效果，如hover，就改变hover里的对应属性值即可

~~~
property：变化的值，如width。 duration：变化时间。 timing-function：变化方式。delay：延迟时间 
transition: property duration timing-function delay;
~~~

可以通过过渡与3D转换做成动画

**注意：**transform属性是设置变换的属性。transition属性是用来设置过渡的，不要弄混

#### 8. 动画


- `@keyframe`规则:关键帧。`@keyframes` 规则内指定一个 CSS 样式和动画将逐步从目前的样式更改为新的样式。
  
  使用方法

~~~
.name{
animation:名字A 
}

//操作一步
@keyframe 名字A{
from{}
to{}
}

//操作几步
@keyframe 名字A{
0%{}
50%{}
100%{}
}
~~~

- `animation`:

~~~
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
~~~

| animation-name            | 指定要绑定到选择器的关键帧的名称                             |
| ------------------------- | ------------------------------------------------------------ |
| animation-duration        | 动画指定需要多少秒或毫秒完成                                 |
| animation-timing-function | 设置动画将如何完成一个周期                                   |
| animation-delay           | 设置动画在启动前的延迟间隔。                                 |
| animation-iteration-count | 定义动画的播放次数。                                         |
| animation-direction       | 指定是否应该轮流反向播放动画。                               |
| animation-fill-mode       | 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。 |
| animation-play-state      | 指定动画是否正在运行或已暂停。                               |

#### 9. 多列

可以做了解

| 属性              | 描述                                     |
| :---------------- | :--------------------------------------- |
| column-count      | 指定元素应该被分割的列数。               |
| column-fill       | 指定如何填充列                           |
| column-gap        | 指定列与列之间的间隙                     |
| column-rule       | 所有 column-rule-* 属性的简写            |
| column-rule-color | 指定两列间边框的颜色                     |
| column-rule-style | 指定两列间边框的样式                     |
| column-rule-width | 指定两列间边框的厚度                     |
| column-span       | 指定元素要跨越多少列                     |
| column-width      | 指定列的宽度                             |
| columns           | 设置 column-width 和 column-count 的简写 |

#### 10. 用户界面

- resize：修改大小

  | 值         | 描述                         |
  | :--------- | :--------------------------- |
  | none       | 用户无法调整元素的尺寸。     |
  | both       | 用户可调整元素的高度和宽度。 |
  | horizontal | 用户可调整元素的宽度。       |
  | vertical   | 用户可调整元素的高度。       |

- box-sizing：以确切的方式定义某个区域的具体内容

不使用box-sizing，默认情况下，元素的宽度与高度计算方式如下：

**width(宽) + padding(内边距) + border(边框) = 元素实际宽度**

**height(高) + padding(内边距) + border(边框) = 元素实际高度**

CSS3的 `box-sizing` 属性在一个元素的 width 和 height 中包含 padding(内边距) 和 border(边框)。

即，如果设置width为300，那么不管内边距是多少，这个盒子内容+边距+border就是300


| 值              | 说明                                                         |
| :----------    | :----------------------------------------------------------- |
| content-box   | 这是 CSS2.1 指定的宽度和高度的行为。指定元素的宽度和高度（最小/最大属性）适用于box的宽度和高度。**元素的填充和边框布局和绘制指定宽度和高度除外，即设定宽高时不包含边距与边框** |
| border-box    | 指定宽度和高度（最小/最大属性）确定元素边框。也就是说，**对元素指定宽度和高度包括了 padding 和 border** 。通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。 |

- outline-offset

  - `outline:2px solid red`：在border外加一个边框
  - `outline-offset:15px`：设定那个边框的偏移量

  以上两句话操作的都是同一个边框，没有设置`outline`就不能设置`outline-offset`

以下是css3新增的用户界面属性

| 属性           | 说明                                           | CSS  |
| :------------- | :--------------------------------------------- | :--- |
| appearance     | 允许您使一个元素的外观像一个标准的用户界面元素 | 3    |
| box-sizing     | 允许你以适应区域而用某种方式定义某些元素       | 3    |
| icon           | 为创作者提供了将元素设置为图标等价物的能力。   | 3    |
| nav-down       | 指定在何处使用箭头向下导航键时进行导航         | 3    |
| nav-index      | 指定一个元素的Tab的顺序                        | 3    |
| nav-left       | 指定在何处使用左侧的箭头导航键进行导航         | 3    |
| nav-right      | 指定在何处使用右侧的箭头导航键进行导航         | 3    |
| nav-up         | 指定在何处使用箭头向上导航键时进行导航         | 3    |
| outline-offset | 外轮廓修饰并绘制超出边框的边缘                 | 3    |
| resize         | 指定一个元素是否是由用户调整大小               | 3    |

#### 11. 图片

补充学习：[css3图片](https://www.runoob.com/css3/css3-images.html)

#### 12. flex-弹性盒子

弹性盒子由**弹性容器**(Flex container)和**弹性子元素**(Flex item)组成，弹性容器通过**设置 display 属性的值**为 flex 或 inline-flex将其定义为弹性容器

