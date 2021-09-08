# summer plan - Markdown
how to write Markdown?[^快捷键]

<svg t="1626158047738" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1648" width="18" height="18"><path d="M0 0h1024v1024H0z" fill="#FFFFFF" p-id="1649"></path><path d="M944 896H80.213333a31.189333 31.189333 0 0 1-27.306666-16.213333l-5.845334-9.813334a33.493333 33.493333 0 0 1 0-32.426666l431.36-736.426667a32.597333 32.597333 0 0 1 27.733334-15.786667h12.8a32.554667 32.554667 0 0 1 27.733333 15.786667l430.506667 736.426667a33.28 33.28 0 0 1 0 32.426666l-5.930667 9.813334a31.232 31.232 0 0 1-27.264 16.213333z m-453.205333-256a21.333333 21.333333 0 0 0-21.333334 21.333333v42.666667a21.333333 21.333333 0 0 0 21.333334 21.333333h42.666666a21.333333 21.333333 0 0 0 21.333334-21.333333v-42.666667a21.333333 21.333333 0 0 0-21.333334-21.333333z m-7.722667-256a21.333333 21.333333 0 0 0-21.333333 23.893333l17.066666 137.386667a10.666667 10.666667 0 0 0 10.581334 9.386667h45.354666a10.709333 10.709333 0 0 0 10.666667-9.386667l17.066667-137.386667a21.333333 21.333333 0 0 0-21.333334-23.893333h-58.069333z" p-id="1650"></path></svg>warning

> 1. 你无法在Typora里用`Tab`生成textarea 因为它用的Tab是`<0x200b>`是种隐形空格
>    你要用正常的tab生成textarea 只能用它的`ctrl`+`shift`+`k`生成
> 2. 我不建议你用Typora的代码块来书写代码,原因看这:`；`=；`;`=;

## 1. 区分
### Title
> Ctrl+1 至 Ctrl+6 插入一级至六级标题

### 区块
> 它们通常以>+space激活
> >还可以多个> + num(>)嵌套
> >> 但是并没有快捷键
> >> > 似乎也能套6层
> >> >
> >> > > 不过如果套这么多写起来是真的麻烦,希望能做个人

### 代码块
> 有两种方式
> 一种如(使用```来包裹)
    ```javascript
    //this is the JS code sample
    var new Day = Date();
    var Hour = Date.Hour();
    //blablabla
    ```
> 另一种便是(<?开头)
    <?javascript
    var a = test;
建议为了语义化 选前面这种,有头有尾 

### 标注
#### 片段标注
`list of devices adb devices detected 80f34a40y`
    
    list of devices
    adb devices detected 80f34a40y
&nbsp;

    下面的方法(TAB)支持换行 比单纯用``功能强 以牺牲书写时的简约度 但会隔行链接
    需要自行&nbsp; 顺带如果用这个是直接转换str 不会关联任何转义符号
#### 字体标注
经典标注 B I U link S
> **bold** or __bold__

    **bold** or __bold__

> *italic* or _italic_

    *italic* or _italic_

> [link](https://meiyan.tech/note_home)

    [link](https://meiyan.tech/note_home)
> ~~strike through~~

	~~strike through~~

#### Extra

> 实现区块的换行
> 
> 即增行并空着换行就能实现

## 2. 列表
###  有序列表 注意不能按数字键的enter键来继续,要跳过需要按`↓`键
> 1. 就能直接排序 就类似于你>之后+空格就能接着排序

> > 1. __25__
> > 2. 4
> > 3. 5
> > 4. 6
> > MDE不支持嵌套快捷键(Tab)？

### 无序列表 同上(起始为-/*/+)
> + 5
> + 4
> + 5
> + 
### Extra
* 第一项
    > 列表里调用区块
    > ?
* 第二项

### task fill
- [ ] textarea 
- or
- [x] textarea

### table列表
Example: The table with alignment.

| Align left | Align center  | Align Right |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

> 成型主要符号 :--|:--|:--|
> 
创建脚注格式类似这样 [^RUNOOB].
> 
> __?__

### 图片插入
传统的有`![](imgsrc_write_here)`这样插入图片

    但我更建议用HTML写法<img src="">语义化明显比上面的好
tech

[^快捷键]: #### 快捷键
### 字体快捷键
> Alt+b 选中的内容转换为粗体
> Alt+i 选中的内容转换为斜体
### 功能快捷键
> Ctrl+Win+V 选中的内容将自动转换为行内式超链接，链接到剪贴板中的内容(失效)
> 
> Ctrl+Win+R 选中的内容将自动转换为参考式超链接，链接到剪贴板中的内容
> 
> Ctrl+Alt+R 弹出提示框插入一个参考式超链接，在提示框中输入链接内容和定义参考ID[^3]
> 
> Ctrl+Win+K 插入一个标准的行内式超链接
> 
> Win+Shift+K 插入一个标准的行内式图片,链接到剪贴板中的内容(此快捷键可能与输入法有冲突)
> 
> 
> 
> Ctrl+Shift+6 自动插入一个脚注，并跳转到该脚注的定义中。[^???]
> 
> Alt+Shift+F 查找没有定义的脚注并自动添加其定义链接
> 
> Alt+Shift+G 查找没有定义的参考式超链接并自动添加其定义链接
> 
> Ctrl+Alt+S 脚注排序
> 
> Ctrl+Shift+. 缩进当前内容
> 
> Ctrl+Shift+, 提前当前内容





[^RUNOOB]: 3



