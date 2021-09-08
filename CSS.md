css临时

1. **块级元素（block elements）**,来源于CSS盒子模型。块级元素包含width height,padding,border与margin，他们的排列方式是从上到下排列。 行内元素，排列方式是水平排列。(*但是一个div就将直接占用一行的长度,所以实际结果便是从上往下排)

2. 

3. **行内元素（inline elements）**排列方式是水平排列。(*大小完全受限于文字)

4. 

5. **行内块元素（inline-block elements）**在内部他的表现类似block元素，比如他拥有block元素的width height,即可以设定自己的高宽值，亦可以设定自己的padding,border与margin，而外部的排列方式有类似行内元素，即水平排列，而不是像块级元素一样从上到下排列。

   (大小不完全受文字限制 可以自定义大小)

　　之所以称之为inline-block。是因为它兼具行内元素(inline-element)和块级元素(block-element)的特征。



　　**Replaced element 置换元素**

　　说到这，有必要提的就是**置换元素**。何为置换元素，在html中，有类特殊的元素如:

　　<img>|<input>|<button>|<select>|<textarea>|<label>

　　他们被称为可置换元素（Replaced element）。他们区别一般inline元素（相对而言，称non-replaced element）是：这些元素拥有内在尺寸(intrinsic dimensions),他们可以设置width/height属性。他们的性质同设置了display:inline-block的元素一致。上述六个标签在现代浏览器中即为

**天生的inline-block元素。**



关于内容的垂直水平居中显示

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
| initial  | 初始值(?)                                                    |



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



flex的逻辑显示方式



首先基础框架main肯定是

absoulte固定位置 

并设置height

width:1344px;



*其中作者这里运用了动态@media (max-width)调节 所以**height**/**width**属性在非正常大小是被替代的

然后子集modern_main

​		~~显示为inline-block,~~

​		~~并垂直调整到top头部~~	(始方块从上部开始排序,这个其实也是保险)

​		modern_width:1344px	(显然 main的宽度靠它撑开)

​		height:100%属性				(继承main)

​		*width:100%

​		~~*其中作者这里运用了动态@media (max-width)调节 所以**width**属性在非正常大小是被替代的~~



​		(Q:inline-block的理由？ A:也许仅仅只是个保险 因为去除之后也不会有任何崩塌)

​		(Q2:那么它的作用到底是什么？如果只是弹性调整为什么不在main上就设置完宽高

​				而非要父级负责一个属性，而子集又负责另外一个属性？)

​		(A2:给作者一个方便动态调整宽高的”容器“ 如果整合进main的话 会造成main的限制

​				还记得下面的属性的width,height继承的谁属性吗 

​				~~自然根源分别就是media_main 与 main~~

​				~~TM的 我编不下去了 备份走起 8.28修改css~~

​				~~??也许 它这样写 就是为了允许获取你屏幕大小的代码能够更自由的发挥？~~

​				总之 我改成 是继承于main属性

)

****

​		然后子集

​				modern wa h1(这里拆分为modern/wa/h1 后不赘叙)

> 其中modern预先设立好背景颜色 并同样显示为inline-block 
>
> 当然它的位置必须跟随着abs(main)的relative
>
> 它们的高宽来自于modern_main(main)
>
> h1设立好高度 11%
>
> wa 设立好宽度 90%



​				wa占宽度 h1占高度

​				然后子集

​						sub 在这里 提前设立好text-align/font-size/color/cursor等属性操作

​						Q:~~但是这里的sub属性 为什么还要特地说明width/height 100%?~~

​							这个div 到底有什么存在的必要吗？

​						A:也许是设计理念相同 就是更加语义化 多一个sub 来专门负责文字的部分

​						**并列** name 设置背景颜色



​						(?)然后子集(内容繁多的时候就需要)

​						vertical_middle_main

​						此处写明table与width/height

​						而下一个子集

​								自然就是table-cell 以及 vertical-align:middle

​								最后就是内容

​										<p>...

​							(因为上面的class早已规定好文字的各种(sub) 以及面板排序的(table) 以及占用(inline-block) 基本上这里直接填充内容即可)