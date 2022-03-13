body本身也是有自带的margin属性 初始值为8 这个默认值总比直接贴上去屏幕左上角好看这没问题

但是这会对开发时的像素计算有很大的误导性(-16)

建议每次开发页面前 都直接赋值body的margin为0.



另外body不是元素块 所以你不能直接对body标签设置overflow属性



### css布局排列

#### 以往的排列元素

1. **块级元素（block elements）**,来源于CSS盒子模型。块级元素包含width height,padding,border与margin，他们的排列方式是从上到下排列。 行内元素，排列方式是水平排列。(*但是一个div就将直接占用一行的长度,所以实际结果便是从上往下排)




2. **行内元素（inline elements）**排列方式是水平排列。(*大小完全受限于文字/以及图标实际占用空间)



3. **行内块元素（inline-block elements）**在内部他的表现类似block元素，比如他拥有block元素的width height,即可以设定自己的高宽值，亦可以设定自己的padding,border与margin，而外部的排列方式有类似行内元素，即水平排列，而不是像块级元素一样从上到下排列。

(大小不完全受文字限制 可以自定义大小)

　　之所以称之为inline-block。是因为它兼具行内元素(inline-element)和块级元素(block-element)的特征。

**Replaced element 置换元素**

　　说到这，有必要提的就是**置换元素**。何为置换元素，在html中，有类特殊的元素如:

　　\<img>|\<input>|\<button>|\<select>|\<textarea>|\<label>

　　他们被称为可置换元素（Replaced element）

​		他们的性质同设置了display:inline-block的元素一致。上述六个标签在现代浏览器中即为

​		**天生的inline-block元素。**



#### 现在的趋势(flex)

4. **弹性布局(flex/inline-flex)**

   注:设为Flex布局以后，子元素的**float**、**clear**和**vertical-align**(因为会有justify-content/align-item属性替代)

   属性将失效

   采用Flex布局的元素，称为Flex容器（flex container），简称”容器”。它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称”项目”。

   ![img](https://www.runoob.com/wp-content/uploads/2015/07/3791e575c48b3698be6a94ae1dbff79d.png)

   容器默认存在两根轴：

   **水平**的主轴（main axis）主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；

   **垂直**的交叉轴（cross axis）交叉轴的开始位置叫做cross start，结束位置叫做cross end。

   
   
   好了 主要疑问来了
   
   我们到底什么时候才会用得上flex?
   
   > aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word “flex”).
   >
   > 这是flex布局描述的原话
   >
   > 诚然 如果你只是想简简单单水平排列inline-block就能做的到
   >
   > 但是容器里的项目 并不永远都是规规矩矩的大小相同 直接排序 很有可能造成间距排列不当 影响正常观感
   
   
   
   <img src=".\images\image-20211011162021738.png" alt="image-20211011162021738" style="zoom: 80%;" />
   
   
   
   从这可以看到 作者直接把顶部栏直接用flex布局整体包裹 以此兼容各类项目的大小差异
   
   而如果是单纯的inline-block布局 光是让其他元素能够随意的排列就得针对padding/margin或者是postion调各种设置
   
   这显然是各种意义上的开销更大
   
   
   
   那么本md的flex旨在理解怎么做出这样的效果(顺带看看能不能把我之前写的ul li给用更高效的排列方法替换掉)
   
   
   
   项目默认沿**主轴排列**。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

和inline-block有点类似但是它还要更多的子属性可供调节:

display:flex/inline-flex

排列 flex允许你对一组/一个项目进行统一排列 这样就能更弹性的控制项目的位置

****



##### **容器框架**

排列方向

- flex-direction: row | row-reverse | column | column-reverse| ltr-rtl/top-down

在容器某一个坐标满载之后 你可以将溢出的项目移动到下一个"合理"的地方

- flex-warp:nowrap(默认)|wrap(top-down)|wrap-reverse

- align-content

该属性只对整体flex内容有效(?)

![image-20211014105426872](.\images\image-20211014105426872.png)

****



![image-20211014105135117](.\images\image-20211014105135117.png)

****

间隔

- gap

用法和普通的margin一样 不过还能够自适应所有flex容器内的项目

> .flex container{
>
> display:flex
>
> gap:10px; 
>
> row-gap: 10px; column-gap:20px; | gap: 10px 20px;
>
> }
>
> 



- justify-content(对项目(包括项目内的文字都生效))

  - justify-content: flex-start | flex-end | center | space-between | space-around;

  ![image-20211011172214874](.\images\image-20211011172214874.png)

  center时 体现为**水平垂直**

  (space-evenly)保持间距相等

  注:这些子属性支持基础较差

- align-items

![image-20211013120929357](.\images\image-20211013120929357.png)

其中 

center体现为**纵向垂直**

stretch是尽量填充剩余空间

baseline是让项目尽量切合着 第一行文字的水平线进行排序



> align-items: center;
> justify-content: center;
>
> 结合起来就可以直接实现项目的内容绝对居中



****

<div style="color:red;">集合</div>

- flex-flow(`flex-direction` `flex-wrap`的简括)
  - row nowarp(默认)

****

##### 容器**项目**用

序号排列

- order:1(默认排列是0)

<img src=".\images\image-20211011165440241.png" alt="image-20211011165440241" style="zoom:65%;" />

**必要**时的项目收缩能力(窗口缩小)

- flex-shrink:Num(负数无效)

(优先排列等级似乎低于justify-content?)

**必要**时的项目扩展能力

- flex-grow

(什么是必要时? )

自己看到的情况:

1. 某个项目在两项目之间的时候,如果对单独一个项目使用此属性时会扩充完整个容器的轴(是填充空剩余白内容的好选择)

2. 当前容器的某项长度项目未满的话 搭配flex-wrap生效后会强制生效grow的属性

   造成项目强制扩张

![image-20211012225032304](.\images\image-20211012224717649.png)

****

![](.\images\image-20211012224641472.png)

****

![image-20211012113211689](.\images\image-20211012113211689.png)

也就是说 当整体的容器 **未完全** 占满一个轴的空间时 运用此时属性 某个被选定的项目(们)就会直接占满掉空间



- flex(建议优先直接用这个值)

这是`flex-grow` ,`flex-shrink`和`flex-basis`组合的简写(默认分别的值为0 1 auto)



5.网格布局(grid)



**块级元素：**

块级元素有：div  , p  , form,  ul, li , ol, dl,  form,  address, fieldset,  hr, menu,  table



行内元素就是内联元素。例如<span>、<a>、<label>、<em>、<img>等

text-align针对的就是行内要素

它与 margin 0 auto块要素的调整并不同

而且 设置了行内和块就不代表着什么东西都会居中(浮动？)



这里得提一下table显示

实际上 display:table 是等价于 html标签里的 <table>的

那么既然有table 那必定也有 tr td..

分别对应于

| HTML     | CSS(display)       |
| -------- | ------------------ |
| table    | table              |
| 内联table | inline-table       |
| tr       | table-row          |
| td       | table-cell         |
| tbody    | table-row-group    |
| thead    | table-footer-group |
| tfoot    | table-caption      |
| caption  | table-column       |
| colgroup | table-colmun-group |



为什么不直接用HTML写法？

那当然是css允许一种样式多重使用啊(class/id) 



另外个原因是

CSS的Table能做到许多HTML Table **不能做**的事情，可以从Table中择优选择属性使用。

而且CSS的自由命名 明显 比HTML的默认tr/td更加语义化



到底有什么的不能做的？

**匿名表格元素创建规则**

table表格中的单元格最大的特点之一就是同一行列表元素都等高。所以，很多时候，我们需要等高布局的时候，就可以借助display:table-cell属性。说到table-cell的布局，不得不说一下“匿名表格元素创建规则”



CSS表格除了包含table布局的普通规则之外，同时还有着CSS table布局的超强特性：缺少的表格元素会被浏览器以匿名方式创建。CSS2.1规范中写道：

> CSS2.1表格模型中的元素，可能不会全部包含在除HTML之外的文档语言中。这时，那些“丢失”的元素会被模拟出来，从而使得表格模型能够正常工作。所有的表格元素将会自动在自身周围生成所需的匿名table对象，使其符合table/inline-table、table-row、table-cell的三层嵌套关系。



这段话的意思是，如果我们为元素使用“display:table-cell;”属性，而不将其父容器设置为“display:table-row;”属性，浏览器会默认创建出一个表格行，就好像文档中真的存在一个被声明的表格行一样。



对table-cell元素设置百分比（如100%）的宽高值时无效的，但是可以将父元素设置display:table，再将父元素设置百分比宽高，子元素table-cell会自动撑满父元素。这就可以做相对于整个页面的水平垂直居中

```
.vertical_middle_main {
    width:100%;
    display:table;
    height:100%;
}

.vertical_middle_box {
    display:table-cell;
    vertical-align:middle;
}
```





white-space属性指定元素内的空白怎样处理

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| normal   | 默认。空白会被浏览器忽略。                                   |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。    |
| nowrap   | *文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。(不传送) |
| pre-wrap | 保留空白符(space)序列，但是正常地进行换行。                  |
| pre-line | 合并空白符(space)序列，但是保留换行符。                      |
| inherit  | *规定应该从父元素继承 white-space 属性的值。                 |
| initial  | 继承父元素的设置值                                           |





首先基础框架main肯定是

absoulte固定位置 

并设置height

width:1344px;



### @media响应用法

除了你隔壁直接暴力resize配jquery的各种伪类封装之外

css也有它自己的动态调整

@media查询

> @media 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的。
>
> 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。



> @media *mediatype(缺省时默认为screen)* and|not|only *(media feature)* {*
>   CSS-Code;
> *}

这串响应由媒体类型&并联关系&媒体功能组成

目前能用的**媒体类型** 说实话也只有screen而已 而screen本身又可以被忽略掉..

**连接词** 顾名思义 符合 什么样的情况时才去触发响应



但是理由就和上文一样 能用的几乎就只有一个 所以大部分也没什么必要

> @media (max-width/height:){
>
> css here..
>
> }



你也可以两个属性共同作用

> @media (max-widht:), and (max-height:)

****



### svg图标的使用

svg本质矢量图 在html解析上本质就是一串path代码来组成这样的图形

因为是矢量图 不会因为图片失真 且容量相对于纯图片要小 常用于各种图标上



图标来源 你可以选择自己在在线网站(iconfont)画一个然后导出svg代码

当然你也可以直接本地下载下来然后symbol导入 etc..



**属性解释**

aria-hidden:true/false

把 `aria-hidden="true"` 加到元素上会把该元素和它的所有子元素从可访问性树上移除。这样做可以通过隐藏下列内容来提升使用辅助技术的用户体验：

- 纯装饰性的内容，如图标、图片
- 重复的内容，如重复的文本
- 屏幕外或被折叠的内容，如菜单



可访问树的移除:包括display:none，以及visibility: hidden

****

**iconfont**

```html
下载下来的downloads.zip
其中css是示例用法 js文件是主导入核心
script引入js 和 一份css即可使用
<svg class="svg1">
<use xlink:href="#?"></use>
</svg>

要自定义名字需要更改js里的预先注入svg id="", 此项对应导入js后的svg xlink
而css则对应一份通用的设置css
```





### 知识增加

发现:

8.27

CSS的class其实在命名时就允许你加入多级关系

```html
例如
<div class="modern">
	<div class="modern w1 h1"></div>
    <div class="modern w2 h1"></div>
</div>

它当然可以当成一个.modern w1 h1{}来配置

不过实际上它还可以在css上直接简写成
.modern.h1{}
.modern.h2{}
.modern{} 等等

顺带 那篇flex里 wa = width all,w3 = width 3个长度..以此类推

这个伪flex的难点就是 怎么兼容h2高的东西？ 唧唧的处理方式是把那个块给独立开来
```



10.17

在css的样式设置中id的优先级是大于class的

避免这种情况时 就可能用到这个`!important`的标识

> ```css
> #Box div{color: red;}
> .text-color{color: blue;}
> .important_true{color: blue !important;}
> ```

其实用途反而不是很明显(指上文直接多css阶梯) 只是提醒你有这么一条id>class的设定(



