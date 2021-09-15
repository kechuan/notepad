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
>

- for /f

  skip=

  delims=

  tokens=

首先你要知道`/f`是file的意思 你用上了这个参数 就意味着你循环的对象会是文件.

而不再是目录的文件名称这种东西



> *不管你引用的是什么 你必须要用""将它们括起来
>
> skip=
>
> for循环文本内容是以行为单位,从上至下进行的,skip=1意识就是跳过文本的第一行,即不循环第一行
> 那么skip=2 自然就是跳过前两行了,依次类推.........
>
> 
>
> delims=
>
> 
>
> tokens=
>
> 



Extra:

`%%*`是什么玩意?

它同样是"延迟环境变量"的产物

是在循环过程中取代%原有的作用,将循环体中被调用的值保留循环内所做过的修改

> 在cmd/bat里%%1-%%9被指定为特殊指向(指代参数) 不要去占用它们

注:另外在cmd窗口里 仅需要表示为%a