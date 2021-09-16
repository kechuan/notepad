> 本md以*为假想变量



```bat
@echo off
echo I.Shinji@ZeN Presents
setlocal enabledelayedexpansion 
for /f %%a in ('dir/s/b/a-d *.flac^|find /c /v ""') do set f=%%a
for /f "tokens=*" %%a in ('dir/s/b/a-d *.flac') do (
"D:\工具\FlacV1.3.3\win64\flac.exe" -8 -f -e "%%a"
set /a n+=1
set /a p=100*!n!/%f%
echo 共%f%个文件,已完成!p!﹪)
pause
```

这是代码原文 

实际作用是**扫描**当前文件夹里的所有flac文件 然后顺序让flac程序**执行**Level8 encode

期间在flac执行完后**汇报**工作进度...

它是怎么实现的？



#### 基础

输出结果

**echo**

echo 除了基础的off/on 以切换命令输入显示和单纯的输出文字之外

还有输出变量的功能

`%*%`



设立变量

同一堆强口令的编程语言一样 它必须设立变量才能够对变量执行操作

**set**

> SET /A expression
> SET /P variable=[promptString]



/a 指定一个变量成为一串运算符(alu?)

具体可以是单纯的定义变量 也可以是计算

注:在这里9/2的这种计算会被直接舍去掉即为4



/p 请君输入..



> set (/a) a = 123
>
> echo %a%
>
> << 123



#### **setlocal**

环境变量本地化

具体来说是

> setlocal enabledelayedexpansion

cmd的运行环境默认规定 已经设置好的变量不能再继续变动 即所有变量都应是固定的



所以又诞生了这种延迟环境变量这种概念



想要遵循该规则的变量 必须带上`!*!`的声明来去使用

(又一个示例)

```bat
goto
REM 2
@echo off
set /a a=123
setlocal enableDelayedExpansion
if !a! equ 123 (
  set /a a=!a!*2
  echo !a!
) else (
  echo !a! not equal to 123 
)
pause
246
如果去掉setlocal呢? 那自然就还是123
::REM 2
```



#### 循环

`for (%%a) in (exp) do(exp)...`

```bat
@echo off
for %%a in (ABC) do (echo %%a)
ABC
pause
```

而当为内容打上`,`隔开时,就会把它们分割开处理

```bat
@echo off
for %%a in (A,B,C) do (echo %%a)
A
B
C
pause
```



#### 基础完成



至此 最初的批处理框架已经出来了

```bat
@echo off
for %%a in (*.flac) do (set /a f+=1)
for %%a in (*.flac) do ("你的flac.exe" -8 -f -e "%%a")
echo 共有%f%个文件
pause

如果仅仅只是需求批处理的话 就是这么简单
关键代码甚至只有Line 3
```

****



你怎么可能就这么满足于此(



#### 复原开始

那么 难度上升 开始(

> for /f ("skip=* delims=* tokens=*") %%i in () do ()

首先你要知道`/f`是file的意思 你用上了这个参数 就意味着你循环的对象会是文件.

而不再是目录的文件名称这种东西



按照官方的说法是，for /f会依次将file中的文件打开，并且在进行到下一个文件之前将每个文件读取到内存，按照每一行分成一个一个的元素，忽略空白的行



- for /f

  skip=

  eol(end of line)=

  delims=

  tokens=



> *不管你引用的是什么 你必须要用""将它们括起来
>
> skip=
>
> for循环文本内容是以行为单位,从上至下进行的,skip=1意思就是跳过文本的第一行,即不循环第一行
> 那么skip=2 自然就是跳过前两行了,依次类推.........
>
> 
>
> eol=
>
> 指定当一行以什么符号开始时，就忽略它
>
> "eol=."(忽略以.开头的行数)
>
> 
>
> delims=
>
> 自定义分割符 for读取的文件分割符 默认为(space)/(Tab)
>
> "delims= "意味着读取到空格之后 就不再读取本行 而开始转到下一行
>
> 如果说默认的分割至少是以EOL的形式 那这个就是真分割
>
> 
>
> tokens=
>
> 名义上和delims搭配 
>
> 它的作用就是当你通过delims将每一行分为更小的元素时，由它来控制要取哪一个或哪几个。
>
> "tokens=1,2","token=2-10"...(支援通配符)
>
> "tokens=*" 就是把这一行全部或者这一行的剩余部分当作一个元素
>
> (意义:这样如果你想取除第一个之外的元素 只用delims= 和 tokens=* 就完事了 传统条件下 你可能还需要 2-EOL(?)这样子)
>
> 
>
> 注:当你选择多个token时 相应你要调用的变量也必须是多个(%%i %%j..)
>
> ​	for /f "tokens=2,3 delims= " %%i in (a.txt) do echo %%i %%j
>
> **且！ 这些变量的名字不能随意排序 要按照字母顺序表排序**



Extra:

`%%*`是什么玩意?

它同样是"延迟环境变量"的产物

是在循环过程中取代%原有的作用,将循环体中被调用的值保留循环内所做过的修改

> 在cmd/bat里%%1-%%9被指定为特殊指向(指代参数) 不要去占用它们

注:另外在cmd窗口里 仅需要表示为%a



#### 罗列指定文件

> 'dir /a-d /b `*.*`' |findstr "*" >nul

为什么需要这东西存在？

你想找文件难道`(*.*)`不够用吗



当然？

那还用说!

****

最直观的 你想要2020的文件

然后列表里混杂着17-21年的文件

而 且

有些文件混杂在更下级的目录里面



这不麻烦的要死

****

问题是 怎么筛选？



按照逻辑 你得先知道 文件列表里所有找到的**文件名** 然后才能根据你写的**筛选条件**进行筛选



dir参数

> /a 显示具有指定属性的文件
>
> /b 显示文件名
>
> /s 显示指定目录和所有子目录中的文件。
>
> /d就是指目录（指定属性）
>
> /a-d 显示文件
> /a d 显示目录



findstr/find

> ```
> findstr "test"
> ```

寻找文件名存在test字符串的文件



find -?

> /C 仅显示包含字符串的行数
>
> /V 只打印不包含匹配的行



那么 开始分析代码

```bat
setlocal enabledelayedexpansion
for /f %%a in ('dir/s/b/a-d *.flac^|find /c /v ""') do set f=%%a
for /f "tokens=*" %%a in ('dir/s/b/a-d *.flac') do (
"D:\工具\FlacV1.3.3\win64\flac.exe" -8 -f -e "%%a"
set /a n+=1
set /a p=100*!n!/%f%
echo 共%f%个文件,已完成!p!﹪)
pause
```

L1 不必多说 只是为了让f,p的值实现可变动 同时将下一级for套进去 以便读取到所有的flac进`%%a`

便于被下一级for处理

L2 设置循环变量a 

读取 **顺序读取当前文件夹里的所有包括子属性文件的文件名**

然后寻找包含与不包含""(即寻找全部文件的意思)的flac文件

干嘛呢

设立变量F 让它接收a的变量



L3 读取文件"**本dir里当前文件夹里的所有包括子属性文件的文件名**" 所有的内容(文件名)当作一个**元素**(防止读取断层)读取

干嘛呢

L4

调用flac 以及参数去处理当前的文件(%%a)

L5/L6

设立赋值变量 n每次循环多+1 p每次循环重新根据n变动计算

L7...

END



2021了 还会有人用外置bat来批量处理文件吗(