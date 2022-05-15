notepad for JavaScript

<svg t="1626158047738" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1648" width="18" height="18"><path d="M0 0h1024v1024H0z" fill="#FFFFFF" p-id="1649"></path><path d="M944 896H80.213333a31.189333 31.189333 0 0 1-27.306666-16.213333l-5.845334-9.813334a33.493333 33.493333 0 0 1 0-32.426666l431.36-736.426667a32.597333 32.597333 0 0 1 27.733334-15.786667h12.8a32.554667 32.554667 0 0 1 27.733333 15.786667l430.506667 736.426667a33.28 33.28 0 0 1 0 32.426666l-5.930667 9.813334a31.232 31.232 0 0 1-27.264 16.213333z m-453.205333-256a21.333333 21.333333 0 0 0-21.333334 21.333333v42.666667a21.333333 21.333333 0 0 0 21.333334 21.333333h42.666666a21.333333 21.333333 0 0 0 21.333334-21.333333v-42.666667a21.333333 21.333333 0 0 0-21.333334-21.333333z m-7.722667-256a21.333333 21.333333 0 0 0-21.333333 23.893333l17.066666 137.386667a10.666667 10.666667 0 0 0 10.581334 9.386667h45.354666a10.709333 10.709333 0 0 0 10.666667-9.386667l17.066667-137.386667a21.333333 21.333333 0 0 0-21.333334-23.893333h-58.069333z" p-id="1650"></path></svg> warning

> 1. 在JS修改CSS属性的时候，必须要去掉原本横线，改驼峰命名
>
>    否则就得使用.style['css属性名']='属性';这样修改 比驼峰麻烦
>
> 2. 本md以**`*`**代表着假定的变量名/数据类型
>
> 3. 这玩意既然能翻译html内容 却不能像真正html一样直接设一个\<style>就完事 真麻烦
>
> 4. 而且HTML标签之后的MD语法通通失效(至少在预览上) 你是真的离谱
>
> 5. 总结 专事专办 祝你好用((
>
> 6. 当我写这个的时候 我开始注意到浏览器的适配情况 
>
>    旧浏览器的代表IE11 ES6 几乎只支持到let与const 所以当你用到ES6的东西时
>
>    你就该祈祷不要碰上谁还在用IE打开你网页
>    
> 7. 它虽然不支持unicode码直接转义写入 但还是支持HTML码识别的 通过[unicodewiki](https://unicode-table.com/cn/blocks/control-pictures/)查询
>    
>    
>    

### 0、foundation

通用知识

#### 0.1、符号

`\`转义符号

无论在什么语言里面都有广泛的通用规则 可转义ASCII码 也可反向屏蔽以来实现正确的内容

例如 [^\n \t \b]&nbsp;\&nbsp; 

##### 详细列表

| 转义字符 | 意义                                |
| -------- | ----------------------------------- |
| \b       | 退格(BS)     |
| \f       | 换页(FF)    |
| \n       | 换行(LF) |
| \r       | 回车(CR)   |
| \t       | 水平制表(HT) （跳到下一个TAB位置）  |
| \v       | 垂直制表(VT)                        |
| \\\      | 代表一个反斜线字符''\'              |
| \\'      | 代表一个单引号（撇号）字符          |
| \\"      | 代表一个双引号字符                  |
| \?       | 代表一个问号                        |
| \0       | 空字符(NUL)                         |
| \ddd     | 1到3位八进制数所代表的任意字符      |
| \xhh     | 十六进制所代表的任意字符            |
| \\&      | 表示&                               |
|  ||



#### 0.2、运算

###### 0.2.1、优先级

`i++` 与`++i`并不相同

当使用++i的时候会优先计算自身+1再去运算



###### 0.2.2、判断运算

`&&`and

 `||`or(但是在正则里 一个 `|`就代表着or)

 `!=` not euqal

老生常谈



###### 0.2.3、表达式

三目表达式:省略版的if else结构

```javascript
var1?Y:N;		
1√ 2
1x 3
//也可以在此嵌套
var1?Y:(N?NY:NN);
1√ Y
1x N? NY/NN //它可以一直嵌套下去
```



###### 0.2.4、算术表达式

If&switch&while/do-while

与C语法完全一致

```javascript
if (/* condition include: != == >= <= .... */) 
{
	/* code */
}
```

****


```javascript
switch(var){
case 0:	/*break or not?*/
case 1:
case 2:
case 3: return 0;
deafult: return 1;
}
```

****


```javascript
while(true){
execute code
}
```

****


```
do{
execute code
}

while(true);
```



#### **0.3、 多维数组**

无论是C还是JS 二维多维的数组的表达都是一个方框套一方框..

```javascript
var array = [[1,2],[3,4],[5,6]];
```

然后调用就是array\[1]\[1](结果就为4)这样



#### 0.4、 严格模式 

`"use strict";`(ES5+)

将此写在想要生效部分的代码头部 即可.



此模式下

-  不允许使用全局变量(即不允许不带任何声明生成变量)
-  不允许删除变量/对象(函数)
-  不允许数值8进制特化

- **不允许转义字符**(猜想服务器传到数据库里这个限制会有着很大作用)
- 不可向只读属性写入数据

其实就是增加了严格性规范以避免出现低级错误



#### 0.5、 运算符(所有)

附带 W3S运算顺序表

#### JavaScript 运算符优先级值

| 值   | 运算符     | 描述             | 实例             |
| :--- | :--------- | :--------------- | :--------------- |
| 20   | ( )        | 表达式分组       | (3 + 4)          |
|      |            |                  |                  |
| 19   | .          | 成员             | person.name      |
| 19   | []         | 成员             | person["name"]   |
| 19   | ()         | 函数调用         | myFunction()     |
| 19   | new        | 创建             | new Date         |
|      |            |                  |                  |
| 17   | ++         | 后缀递增         | i++              |
| 17   | --         | 后缀递减         | i--              |
|      |            |                  |                  |
| 16   | ++         | 前缀递增         | ++i              |
| 16   | --         | 前缀递减         | --i              |
| 16   | !          | 逻辑否           | !(x==y)          |
| 16   | typeof     | 类型             | typeof x         |
|      |            |                  |                  |
| 15   | **         | 求幂 (ES7)       | 10 ** 2          |
|      |            |                  |                  |
| 14   | *          | 乘               | 10 * 5           |
| 14   | /          | 除               | 10 / 5           |
| 14   | %          | 模数除法         | 10 % 5           |
|      |            |                  |                  |
| 13   | +          | 加               | 10 + 5           |
| 13   | -          | 减               | 10 - 5           |
|      |            |                  |                  |
| 12   | <<         | 左位移           | x << 2           |
| 12   | >>         | 右位移           | x >> 2           |
| 12   | >>>        | 右位移（无符号） | x >>> 2          |
|      |            |                  |                  |
| 11   | <          | 小于             | x < y            |
| 11   | <=         | 小于或等于       | x <= y           |
| 11   | >          | 大于             | x > y            |
| 11   | >=         | 大于或等于       | x >= y           |
| 11   | in         | 对象中的属性     | "PI" in Math     |
| 11   | instanceof | 对象的实例       | instanceof Array |
|      |            |                  |                  |
| 10   | ==         | 相等             | x == y           |
| 10   | ===        | 严格相等         | x === y          |
| 10   | !=         | 不相等           | x != y           |
| 10   | !==        | 严格不相等       | x !== y          |
|      |            |                  |                  |
| 9    | &          | 按位与           | x & y            |
| 8    | ^          | 按位 XOR         | x ^ y            |
| 7    | \|         | 按位或           | x \| y           |
| 6    | &&         | 逻辑与           | x && y           |
| 5    | \|\|       | 逻辑否           | x \|\| y         |
| 4    | ? :        | 条件             | ? "Yes" : "No"   |
|      |            |                  |                  |
| 3    | =          | 赋值             | x = y            |
| 3    | +=         | 赋值             | x += y           |
| 3    | -=         | 赋值             | x -= y           |
| 3    | *=         | 赋值             | x *= y           |
| 3    | %=         | 赋值             | x %= y           |
| 3    | <<=        | 赋值             | x <<= y          |
| 3    | >>=        | 赋值             | x >>= y          |
| 3    | >>>=       | 赋值             | x >>>= y         |
| 3    | &=         | 赋值             | x &= y           |
| 3    | ^=         | 赋值             | x ^= y           |
| 3    | \|=        | 赋值             | x \|= y          |
|      |            |                  |                  |
| 2    | yield      | 暂停函数         | yield x          |
| 1    | ,          | 逗号             | 7 , 8            |

**注意：**淡红色指示实验性或建议性的技术（ECMASScript 2016 或 ES7）

**提示：**括号中的表达式会在值在表达式的其余部分中被使用之前进行完全计算。



#### 0.6、正则表达式

正则一般用于取得字符串数据后**筛选**你需要的东西然后进行**替换**



在正则里

> `+`在reg之间有着**连接**作用
>
> 而 `|`代表着**或**的作用
>
> 而且正则遵循先来后到的形式

```javascript
/\.\d+/g 这个代表着小数点后至少一位
/\d+\./g 这则代表着至少一位数值带小数点(12. 234. 012. 0.)
/(\.jpg|png|bmp|ico|gif)$/	这代表着匹配以.jpg png ..结尾的字段
()之间并不影响

```

*正则筛选是根据你写的所有规则 对你输入的字符串进行逐字匹配

并且似乎在寻找到特殊符号后 会将之后的内容分到下一元素里继续排列





##### JS正则起作用的function

在JS里面筛选为`*.search()`/ `*.match()`/`reg.test(*)`(返回正误)		

替换为`*.replace()`	//*此处`*`代表字符串*

search和match? 什么时候会用到其中之一呢?

> search方法只关心有无匹配，一旦找到匹配，就提供返回值，并且立刻中断查找的执行。
>
> match也是在目标字串对象中寻找与关键词匹配与否的一个方法，它的强大功能在于通过关键词的规则创建可以实现复杂搜寻功能，非常灵活。

总而言之 search应对一次性的简单寻找可以用 当然你match本身就可以当search用

~~所以还要search干嘛呢~~



match函数会把传来的结果进行筛选后

将筛选出来的结果以数组方式存储 并以寻找到的个体按顺序(`,`)隔开

顺带因其本质也是对str的修改 所以你也可以在它外面`+`其他东西

```javascript
var string = "abcABC123"
var result = string.match(/abc/)+",233";
document.write(result);
//abc,233
```



顺带一提你可以直接这样检验符不符合正则内容

`reg.test(str)`

```javascript
val = "123456"/123456
var isnum = /^\d+$/.test(val);
console.log(isnum)
//true
```



##### 修饰符与表达式

**修饰符**

*修饰符*可用于大小写不敏感的更全局的搜素：

用法:使用`/`符号将需要修饰符的部分包裹 然后在`/`末尾加上修饰符

| 修饰符 | 描述                                                      |
| :----- | :-------------------------------------------------------- |
| i      | 执行对大小写不敏感的匹配。                                |
| g      | *执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m      | 执行多行匹配。(目前没感觉有什么用)                        |



而你可以直接在match里面插入正则

简简单单用法:

```javascript
有请我们的"0x200b/\u200b"
var test2 = "1710000​​​​​​​​​​​​​​​​​​​​1111"
console.log(test2.match(/\u200b/g).length)
//20
如果不带.length的话 会直接返回一个数组对象 对象里面记录着各个元素位置以及length
```

****



以及表达式

**方括号**

| 表达式             | 描述                                  |
| :----------------- | :------------------------------------ |
| [abc]              | 查找方括号之间的任何字符。            |
| [^abc]             | 查找任何不在方括号之间的字符。        |
| [0-9]              | 查找任何从 0 至 9 的数字。            |
| [a-z]              | 查找任何从小写 a 到小写 z 的字符。    |
| [A-Z]              | 查找任何从大写 A 到大写 Z 的字符。    |
| [A-z]              | **查找任何从大写 A 到小写 z 的字符。  |
| [adgk]             | 查找给定集合内的任何字符。            |
| [^adgk]            | 查找给定集合外的任何字符。            |
| (red\|blue\|green) | *查找任何指定的选项。这里的\|就是`or` |
| [\u2010-\201F]     | 它这个也支持unicode码的范围           |
| [\u4e00-\u9fa5]    | 友情提示:汉字的范围是                 |

***括号的正则是可以连续写在一起的**

\**是的,在js里面小写a-z的编码是在大写的A-Z编码**之后**的

小小实例:

E1

还记得c语言里的scanf("%\*\[^\n]%*c");吗

它的意思是

1. 清理输入缓冲区中第一个\n之前的所有字符
2. 清理输入缓冲区中第一个字符，也就是上次遗留下的\n

首先要告诉当时的我是:`*`表示该输入项读入后不赋予任何变量

也就是说其实它的意思只是\[^\n]除了换行+将\n读入char里并且不赋任何值



就是那么简单(恼

E2 方括号连续:

```javascript
var string = "abcABC123"
document.write(string.match(/[0-9a-z]/gi)+",233")
//a,b,c,A,B,C,1,2,3,233

document.write(string.match(/[^0-9a-z]/gi)+",233")
//null,233

document.write(string.match(/[0-9][^a-z]/gi)+",233")
//12,233

//注:你不能将余号放在中间 那会直接失效
document.write(string.match(/[0-9^a-z]/gi)+",233")
//a,b,c,A,B,C,1,2,3,233
```



***这里统一借用Elia大佬的eslyric的正则片段来参考以理解各种用法**

Line 4

```javascript
function processKeywords (str) {
  var s = str
  s = s.toLowerCase()	
  s = s.replace(/'|·|\$|&|–/g, '')
  return s
 }
 
processKeywords("$tupid one!")
//"tupid one!"
```

其实就是or 而且也支持表达式的插入

****



##### **量词**

| 量词   | 描述                                        | 个人理解 |
| :----- | :------------------------------------------ | -------- |
| n+     | 匹配任何包含至少一个 n 的字符串.            | (1,)     |
| n*     | 匹配任何包含零个或多个 n 的字符串.          | any    |
| n?     | 匹配任何包含零个或一个 n 的字符串.          | (0,1)    |
| n{X}   | 匹配包含 X 个 n 的序列的字符串.             | (x)      |
| n{X,Y} | 匹配包含 X 至 Y 个 n 的序列的字符串.        | (x,y)    |
| n{X,}  | 匹配包含至少 X 个 n 的序列的字符串.         | (x,)     |
| ^n     | *匹配任何开头为 n 的字符串。                | n*       |
| n$     | *匹配任何结尾为 n 的字符串。(n前n后)        | *n       |
| ?=n    | 匹配n之前的字符串                           | ()n      |
| ?!n    | 匹配任何其后没有紧接指定字符串 n 的字符串。 | ()!n     |
=======
| 量词   | 描述                                               | 个人理解 |
| :----- | :------------------------------------------------- | -------- |
| n+     | 匹配任何包含至少一个 n 的字符串.                   | (1,)     |
| n*     | 匹配任何包含零个或多个 n 的字符串. 也就是说 任意值 | *        |
| n?     | 匹配任何包含零个或一个 n 的字符串.                 | (0,1)    |
| n{X}   | 匹配包含 X 个 n 的序列的字符串.                    | (x)      |
| n{X,Y} | 匹配包含 X 至 Y 个 n 的序列的字符串.               | (x,y)    |
| n{X,}  | 匹配包含至少 X 个 n 的序列的字符串.                | (x,)     |
| ^n     | *匹配任何开头为 n 的字符串。                       | n*       |
| n$     | *匹配任何结尾为 n 的字符串。(n前n后)               | *n       |
| ?=n    | 匹配n之前的字符串                                  | ()n      |
| ?!n    | 匹配任何其后没有紧接指定字符串 n 的字符串。        | ()!n     |
****

注:要注意的是量词允许你直接**叠加**而无需什么连接符

*开头结尾的标准:以空格为片段



你当初是不是很疑惑/末尾的`+`/是什么意思

Line 6

```javascript
 s = s.replace(/[-/:-@[-`{-~]+/g, '')
```

现在你知道这是筛选任何含有"-/:-@[-{-`~"符号**至少含有一个**的字符串

否则你就得这么写

```javascript
s = s.replace(/(-|\/|:|-|@|\[|-|`|{|-|~)+/g, '')
//其中 为了防止一些符号被转义 还要特地加上"\"来防止被转义
```

是不是巨麻烦

而且上面那写法还匹配绝大多数应用场景





**综合运用**

这些限定词合理排列就组成了一些有意思的reg

**纯数值 正数**

既然是纯数字 那么你开头结尾必是数字 你程序的判断过程也必是从头到尾的

根据限定词的逻辑

1. 第一个放个`^`很合理吧 然后在后面放个`$`也很合理吧
2. 那么中体部分比如是数值 既然要匹配那就肯定是数值即为`[0-9]`
3. 接下来 运用至少出现了?次的reg 根据逻辑互补 更建议用`*` (任意值)
5. result:^[0-9]*$



而有时候比起验证纯数值 你更想知道的是范围 或者说

**特定位数的数值**

E1:四位数

1. 光速吟唱第一句与第二句.jpg
2. 而这个特定位数的数值 自然就是运用了`{x}`
3. result:^[0-9]{4}$

别急着贺电 看看其他人是怎么写的(指菜鸟)

**^\d{4}$**

确实 我都忘了可以直接\d代替

必可活用于下一次(



E2:**带小数的数值**

1. 光速吟唱第一句与第二句.jpg	`^$`

2. 既然是小数 那就必有`.` 而且不能有多个`.` ~~而且`.`不能在头部和尾部~~(步骤一已处理)

3. 既然是小数 那就必然是`\.`  (`.`被占用成为元字符)

4. 且`\.`后面一定跟着至少一位数值 `\.\d+`

5. 对了 小数可没限制正负  `\-?` (不在或者存在负号)

6. 连接(用`+`进行reg连接)

   **result**:`^(\-?\d)+(\.\d+)$`

   

E3:纯汉字

1. 汉字嘛..范围是[\u4e00-\u9fa5] 第一第二句复刻修改 `^[\u4e00-\u9fa5]+$`



E4:以某个词组(2021)开头的

`^(2021)+...`?



E5:文件格式匹配

`/(\.jpg|jpeg|png|bmp|ico|gif)$/`



**元字符**

元字符（Metacharacter）是拥有特殊含义的字符：

| 元字符 | 描述                                                         | 等效于            |
| :----- | :----------------------------------------------------------- | ----------------- |
| .      | **查找单个字符，除了换行和行结束符。                         | ？                |
| \w     | 查找单词英文/数字字符。                                      | [0-9a-zA-Z]       |
| \W     | 查找非单词字符。                                             | [^0-9a-zA-Z]      |
| \d     | 查找数字。(%d?)                                              | [0-9]             |
| \D     | 查找非数字字符。                                             | [^0-9]            |
| \s     | 查找空白字符。(space)                                        | \u0020            |
| \S     | 查找非空白字符。                                             | .                 |
| \b     | *匹配**单词**边界。(border) <br/>当\b放在前面时 视为找前面边界<br/>放到后面时 则为寻找后面边界 | 反向NA用法        |
| \B     | 匹配非单词边界。                                             | .                 |
| \0     | 查找 NUL 字符。                                              | .                 |
| \n     | 查找换行符。                                                 | .                 |
| \f     | 查找换页符。                                                 | .                 |
| \r     | 查找回车符。                                                 | .                 |
| \t     | *查找制表符。                                                | **\u2500—\u257F** |
| \v     | 查找垂直制表符。                                             | .                 |
| \xxx   | 查找以八进制数 xxx 规定的字符。                              | .                 |
| \xdd   | 查找以十六进制数 dd 规定的字符。                             | .                 |
| \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。                  | .                 |



>  大写都为非

*[制表符](https://unicode-table.com/cn/blocks/box-drawing/)



E3.1A `.`

```javascript
var str="hack trick, handst h/t ht h\u200bt h t";
var patt1=/h.t/g;
console.log(str.match(patt1))
//["h/t", "h​t", "h t"]
是的 它就是只能找两个字符之间的一个字符 无论这是什么除了\n的字符
```



*贪婪模式/懒惰匹配(`.*`/`.*?`的用法)

什么是贪婪模式？

> 当正则表达式中包含能接受重复的限定符时，通常的行为是（在使整个表达式能得到匹配的前提下）匹配尽可能多的字符。以这个表达式为例：a.*b，它将会匹配**最长**的以a开始，以b结束的字符串。如果用它来搜索aabab的话，它会匹配整个字符串aabab。这被称为贪婪匹配。
>
> (而且 空格间隔并不会打断？)



贪婪示例

```javascript
var me = "aabab"
me.match(/a.*b/)
//["aabab"]

var me = "aabab aasdddddbdddddda"
me.match(/a.*b/)
//["aabab,aasdddddb"] 
```



但我想 你有时候更需要简单/短 的筛选长度

> 所以 我们更需要懒惰匹配，也就是匹配尽可能少的字符。前面给出的限定符都可以被转化为懒惰匹配模式，只要在它后面加上一个问号?。这样.*?就意味着匹配任意数量的重复，但是在能使整个匹配成功的前提下使用最少的重复
>
> 
>
> 总而言之 就是从字符串头看到尾 到预设好的字符串直接中断 不再寻找新的长度



`.*?`演示段:

```javascript
var me = "aabab"
me.match(/a.*?b/)
//["aab"]

var me = "a000000000000bab"
me.match(/a.*?b/)
//["a000000000000b"] 
```





E3.1N `b`

```javascript
如果说.是两面包夹芝士(主动)
那么border就可以说是栅栏(被动) 探知触发边界的字符串
var str="hack trick, handst h/t ht h\u200bt h t";
console.log(str.match(/ha\b/g))	//没有ha结尾的
//null

console.log(str.match(/\bha/g))
//["ha", "ha"]

console.log(str.match(/ck\b/g))
//["ck", "ck"]
console.log(str.match(/\bck/g))	//没有用ha开头的
//null
```

实际上就是n$/^n的集合 但是只支持英文数字



```javascript
function processKeywords (str) {
  var s = str
  s = s.toLowerCase()	
  s = s.replace(/'|·|\$|&|–/g, '')
  // truncate all symbols
  s = s.replace(/\(.*?\)|\[.*?]|{.*?}|（.*?/g, '')
  //`\(.*?)` `\[.*?]` `{.*?}` `（.*?`
  s = s.replace(/[-/:-@[-`{-~]+/g, '')
  s = s.replace(/将所有被转成Unicode字符转为空格/g, '')
  return s
}
```



F: 一段话 包含有 `space`  `,` `enter`之类的东西 总之你聊天里会有什么 就得包含什么

0. 逗号是/u002C(
1. 因为聊天 你什么符号以开头或结尾都有可能 所以不要加`^$`限定死
2. 因为聊天 你的输入至少包含键盘上的所有东西`\d`+`\w`+`\s`+各种符号
3. 聊天哪有不用汉字的？
4. 因为聊天 上述东西都是可有可无的 甚至随便发个空格都必须识别出来
5. 连接

result:`([\u4e00-\u9fa5]{0,})+(\s{0,})+(\w{0,})+(([\u0021-\u002F]|[\u003A-\u0040]|[\u005B-\u0060]|[\u007B-\u007E]){0,})`

是不是感觉很离谱 毕竟你是要筛选 要不然你直接套个字符串不就得了？

自然而然的 这玩意就不能识别到emoji 以及各种奇奇怪怪的字符



疑惑:

为什么这个会将所有范围外的符号 全部识别成有结果 并返回4个空元素

为什么我单单输入了一个字符 就会显示匹配到两个？

A: 这个大概是和字符串创立是一个道理 即没限定具体长度的情况下 你不能锁死它一个区域的长度？





### 1、变量/对象/属性



JavaScript引入了一个**对象**的概念，实际上JS里几乎都是对象

```javascript
var length = 7;                              	// 数字
var lastName = "Gates";                      	// 字符串
var cars = ["Porsche", "Volvo", "BMW"];      	// 数组/对象
var x = {firstName:"Bill", lastName:"Gates"};   // json/对象
function(){}								    // 对象
```

它允许你像c语言的数据结构一样一次性列一组数据保存在一组变量里，而那一组变量本身也是一个**对象**



##### 属性

对象的成员我们称为**属性**

```javascript
var car = {
    name:"Fiat",
    model:500,
    color:"white"
};

```

疑惑:如果这样改起css属性会比一个个getID然后"ID".style方便的多吧,那是不是可以直接让css套进这个对象属性所有值?

<div id="sign" style="font-size:24px; color:red">很可惜 并不行</div>

 让我们看看它的后果

[^False way:modify CSS string]:  ?

****


判断某个属性是否存在于对象里

` in `/`*.hasOwnProperty('Property_here')`

```javascript
//实例
var student  = {
	sex: "male",
}

"age" in student
//应答 false
"sex" in student
//应答 true 用法就这么简单
```



##### 方法

将函数放入对象里的部分，我们称为**方法**，而且对象里只有**属性**和**方法**这两个构成成分

```javascript
var profile = {
	name:'kechuan',
	PTT:function(){
	return 'unknown';
	}
}
//调用对象的方法需要带括号来调用
//profile.name
//profile.PTT()
```



**动态删减特性**

JS支持你去调用不存在的变量属性 且不会报错

而且也能随时用`delete`删除

 

如果配备上判断是否某个属性在这个对象`in`就能实现对象里属性组的变化 

这就意味着 很多事物(



不过一些配置文件不可能给用户留类似这些的API却把配置入口删了吧

`segatool.ini:???`

所以？意义到底大不大 并不清楚



#### 1.1、全局变量/局部变量

​												为什么要有全局变量和局部变量这两个区别?



这就类似于你在C里面重复使用i这个变量for循环里的`i`和正常赋值里的`i`.如果你去直接这样调用 会导致变量引用出错，在C语言的解决方式是用子模块来规避这问题

而在js里,则有全局变量/局部变量(配function)这一概念来划分

 1. 全局变量(`Window.*`)

    ```javascript
    i = 1;
    console.log(i)
    
    作用域大的跟Window.i一样
    ```
    ****

    你终究会遇到多个js文件挤在一起全局变量到处飞的时候(希望你做个人)

    当然当你遇到这种的时候其实已经没救了 建议重写(

    这里要做的是如何避免到那个情况

    

    **唯一全局变量**

    ```
    x = {};	//定义全局变量
    x.asdasda;
    x.gretgasd;
    没错,定义了全局变量之后，你就能好像在调用属性一样调用你写的js,早日养成习惯，不要随便占用Window
    ```

    

 2. 局部全局变量

    ```javascript
    //var作用域允许各个函数里面调用相同的变量而不冲突，全局变量做不到这点
    function c1(){
        var x;
        return x*x;
    }
    
    function c2(){
        var x;
        return x*x;
    }
    
    
    //但它有个特殊的上下级性质
    //允许内部由外部访问var变量,不允许外部的函数去访问内部函数的var变量
    //如果是两个都有上下级的函数,一个函数c1.1()通过this.c2()调用完整的c2没问题,但是想直接调用c2的子函数
    //c2.2()就不行了
    I P V 4 内 网 现 状
    
    function c1(x){
        var y = 3;
        
        console.log("x的值是");
        console.log(x);
        
        function c2(x){			//内部x取代了外部的x
        console.log(x*y)		//NaN
    	}
    	c2()	//空值传入
        //更别提这种离谱的变量重名时的反应(会直接让变量从内部开始向外寻找变量(要符合内向外的原则))
        //所以C2的x变量为空 即结果为NaN
        //所以你只要去掉c2函数里的'x'就能跑出结果了，因为不再重名变量，自然不需要从内部寻找变量
        //顺带 如果你直接调用c2的话，也会显示c2未定义.毕竟你不能绕过外部去访问内部的函数
    }
    ```



**Extra**

var还有一个奇怪的性质，如果你把声明变量赋值写在末尾，然后把该变量要参与的计算写在前面,它不会报错,而是返回undefined.即它已经被**定义**过了，但与其定义的值并没有被**赋值**上去.

这种情况叫做变量提升



个人**很不建议**用这种情况 这种书写方式非常反语言也反直觉

你看严格模式就不允许你这么写 但为什么会开放这种编写方式？

大抵是在编译器看来 (因为已经自己组合起来了)顺序是没什么必要的罢

```javascript
console.log(y)
var y = "y";
//undefine
//是没有什么用的性质呢(恼)
```



3. 块作用域


   **更高的独立性**

   ```javascript
   let i = 1;
   //不必多说，因为它的性质各个函数肯定相互独立，并且，它无法被任何其他function调用
   for(let x in ?){
       console.log(?[x])
       }
   
   这也是为什么for in会优先考虑用let变量而不是var这种有联系性的变量
   ```



ES6 关键字表示常量

 **const(常量)**

官方定义为**只读**变量,即不可被**修改**

其同样也不属于全局作用域 与`let`同等级的作用域



//ES5 定义常量就是全部大写字母命名的变量就是常量(???

像极了C(#define PI 3.14

```javascript
const PI = '3.14';
PI = '3.1415'; //type error
console.log(PI)
//3.14
```



   但是它们有什么区别？

   首先不必多说全局唯一最大

   但是局部的var的范围又是多大？

   **A:**

   > 用`var`定义就是作用域内变量，不用`var`就是全局变量。(当然你在什么都没有的情况下直接var
   >
   > 那也等效于直接全局作用域了)
   >
   > 
   >
   > 而`var`的变量表示的是当前作用域可用
   >
   > 什么是作用域？
   >
   > **变量（变量作用于又称上下文）和函数生效（能被访问）的区域**
   >
   > 实际上还有一个区别，用var定义的不能用delete删除，不用var的可以用delete删除，也就是说，实际上不用var定义的变量变成了某个对象(全局window或者自定义的全局)的属性。
   >
   > 
   >
   > 而更低作用域的`let`命令范围**只有**在所在的代码块内有效
   >
   > 如果说var的变量能从又内而外的向外访问
   >
   > 那么let就仅局限于它这一层的作用域内可以访问

 

#### 1.2、访问对象(属性)



除了最基础的`.`来访问

```javascript
objectName.property  //me.age
```

访问对象的属性还允许使用中括号(数组形式)访问

```javascript
var dog = {
dog.name:"five",
dog.age:17
}

var unknown_various = "age";
dog[unknown_various]	//中括号能填入变量
//"five"
dog["age"]	//或者是(对象内存在的)字符串
//17
```

但是这样做到底有什么意义呢? 真的会存在不知道对象的属性 却知道中间变量的情况?

我不是很懂(



#### Extra

而在此又引入了一个严格模式`use strict`,强制规定要以var/let局部变量书写否则不生效.且严格模式声明必须写在第一行.
    
```javascript
'use strict'
var i = 1;
```



**Extra2**

//ES6 let与保留关键字的强制使用

```javascript
const carouselList = [         //列表
    {num:"01",desc:"standard"},
    {num:"02"},
    {num:"03"}
]

const standard = carouselList[0];
let status = standard;

>>status
<<{num:"01",desc:"standard"}
```

****



这看着很正常

而当你将let status换成var status的时候

> \>>status
>
> <<[object Object]



还记得之前提到过的let/const的作用域问题吗
在当前的作用域下 var出来的变量属于window/global
而let/const的出来的变量并不属于 所以无法读取



然而即使你把全部变量都以var命名 status依然会是[object Object]
然后更神奇的来了

>window.standard
><<{num:"01",desc:"standard"}
>
>window.status
>
><<[object Object]

这说明status即使以var定义了 也不属于window作用域

这时候情况大概明了了

即 当你想用一个var套另一个var内的属性的时候

第二个var将自动降级为window.var.var 即这个不在作为window作用域 而是类似被套了一层function



怎么解决?

前文说过的 你只要在定义变量的时候始终将他们作为低一级的作用域就行了

即用 let 与 const



现在我发现了更根本的问题

status大概是某个保留关键字 默认直接输入会返回 `""`(草

所以直接var的话会与某段代码抵触的

就当看个乐罢

****

### 2、 数据类型

老生常谈

> <div style="color:red;">string</div>
>
> <div style="color:red">object(function,array,var……………………)</div>
>
> boolean 	true/false
>
> number 	0-9
>
> <div style="color:red;">array(Map/set)</div>
>
> <div style="color:blue;">Null/undefined</div>
>



你可以通过`typeof`来确定数据类型(没错 它并不是方法

7.31更新 

[^bug_of_typeof]:  jump!



#### number(数值)

顾名思义 0-9组成的值

当然分为8 10 16进制

其中八进制的时候 前面必须加个0 (070→56)

十六进制的时候就像C一样需要`0x00b`这样要加0x前缀

数值也会根据有无小数点判断是否浮点值

所以1与1.00含义并不同

你还可以通过`isNan()`来判断是否为数值 等效于 `typeof !== number`



而数值操作 往往直接以ES模块内置Math函数息息相关

直接整几个实用的子函数好了

`Math.random`

返回(0-1)之间的32位浮点



##### **精度丢失**

****

```javascript
var a = 0.1
var b = 0.2
console.log(a+b)
//0.30000000000000004	为什么会有这种情况?
```

JS并没有细分number为 int,float,double 等等

不过在运行环境下 小数循某个IEEE准则以对32位采用float，对64位采用double的计算.

![img](https://pic3.zhimg.com/80/v2-3235ebe5c049136fcd782b5a54d698f6_720w.jpg)

![img](https://pic3.zhimg.com/80/v2-5036be957a2d50373ca74e83bad3e8be_720w.png)

指数偏移量是什么？

> 首先得明白 指数 有正有负 
>
> 以32位的例子来看指数范围应该是在-128-128之间
>
> 那你当然就不能以0当作起始点 所以就将8位的中间值(127)当作起始点
>
> 以全0当作e-127 以全1当作e127
>
> 这就是为啥要先加一个127当作一个偏移量



好了 根据转换规则

> - 首先把这个数字转换为二进制 
> - 再把二进制转换为科学记数法



0.1 →

笑死 根本转不完

```
0.1 *2*2*2*2*2*2*2*2*2*2*2*2*...|*2(100|1)
	 0 0 0 1 1 0 0 1 1 0 0 1 ...1 0 1 0
```

0.2 →

```
0.2  *2*2*2*2*2*2*2*2*...|*2(001|1)
      0 0 1 1 0 0 1 1 ...0 1 0 0
```

这就是问题所在了 小数部分根本转不完 只能受限于环境的32/64位下截止 

截止的位数按四舍五入计入上一位



其实所有语言都会有这问题

曾经C语言考试也有类似这种题 冒出.000003时还以为我整个环境出问题了(



**解决方法**

有简单粗暴的

`.toFixed()`四舍五入	//当然四舍五入的位数还是要靠自己写代码判断

```javascript
function float_cal(a,b){
var str_a = a.toString();
var str_b = b.toString();
    if(str_a.indexOf(".")==-1||str_b.indexOf(".")==-1){
        return "哼哼 啊啊啊啊啊"
    }
var l1 = str_a.split(".")[1].length;
var l2 = str_b.split(".")[1].length;
var c = a+b;
if(l1>l2){
	c.toFixed(l1)
}

else{
	c.toFixed(l2)
}
	return c;
}

```

不过也有根源的解决方法

既然一到浮点计算就会有偏差 那就不用浮点就行了

把几个运算的数字都变成整数就行了 无损乘N倍为整数后计算 最后除回去就行了



有这个基础思路就行 这应该是全部语言通用(费算力)的解法



**问题+**(百炼成仙)

```javascript
float_cal(1.001,2.002)
//3.0029999999999997
(1.001*1000=1000.9...)
float_cal(1.0011,2.0021)
//3.0032 正常

float_cal(1.00111,2.0000021)
//3.0011121000000003
```
Jesus 这些数值运算时 因为原生的数值已经不能够支撑正常四舍五入 

所以还是会出现精度丢失的问题

既然如此 那就直接不让在小数的时候参与运算活动了 
直接预先将小数点抹掉(replace) 完完全全为一个整数 再除小数位就可以了

****

ES6+引入 

```javascript
function float_cal(a,b){
var str_a = a.toString();
var str_b = b.toString();
    if(str_a.indexOf(".")==-1||str_b.indexOf(".")==-1){	//判断整数
        if(str_a.indexOf(".")==-1){
            var l2 = str_b.split(".")[1].length;		//分离小数位
            var a1 =  a*Math.pow(10,l2);
            var b1 = parseInt(str_b.replace(".",""));
            return (a1+b1)/Math.pow(10,l2);
        }
        
        if(str_b.indexOf(".")==-1){
           	var l1 = str_a.split(".")[1].length;
            var b1 =  b*Math.pow(10,l1);
            var a1 = parseInt(str_a.replace(".",""));
            return (a1+b1)/Math.pow(10,l1);
        }    
    } 


    else{
        var l1 = str_a.split(".")[1].length;
        var l2 = str_b.split(".")[1].length;
        var a1 = parseInt(str_a.replace(".",""));	//Str转整数
        var b1 = parseInt(str_b.replace(".",""));

        if(l1>l2){									//比较数位大小
        	var a1 =  a*Math.pow(10,l1);
        	var b1 =  b*Math.pow(10,l1);
        	return (a1+b1)/Math.pow(10,l1)
        }

        else{
        	var a1 =  a*Math.pow(10,l2);
        	var b1 =  b*Math.pow(10,l2);
        	return (a1+b1)/Math.pow(10,l2);
        }
	}
}
//Finish!
```



好康 是新功能噢

##### 新功能引入

ES7引入

`indexOf()` 已经可以切换为更加语义化的`includes()`了

```javascript
//ES6 str_a.indexOf(".")==-1
//ES6+ str_a.includes(".")	//	true/false
还支持从哪个索引值开始搜索
str_a.includes(".",1)
```



`Math.hypot()`//ES6+

等效于计算所有参数的平方和的平方根

```javascript
Math.hypot(3,4)
>>5

//且还会自动将string的数转化为整数 这意味着你可以直接用hypot()计算string的参数
//而不用再一个个parseInt后再计算

Math.hypot("3",4)
>>5

//缺省默认为0
```



`Math.trunc()`//ES6+

返回数值的整数部分

```javascript
// 整数部分为 0 时也会判断符号
Math.trunc(-0.5); // -0
Math.trunc(0.5);  // 0
 
// Math.trunc 会将非数值转为数值再进行处理
Math.trunc("12.3"); // 12

矩阵取值 很有用(
```



****


#### String(字符串)

含义:包括非数字非布尔值的有效存在值即为**字符串**

被定义在变量的字符串有一个特性就是不可被赋值

​																													——"引号其实是可以’嵌"套"‘的"

字符串存在意义为了给我们用来编辑

##### 字符串编辑

我们固然不能直接将变量直接编辑，但它可以先通过一个转变字符串编辑的过程再进行更多操作.

具体详见

[^function-toString]:  jump!

追加 `*.concat()`

```javascript
var str = "abc"
str.concat("def")
```

分割 `*.substring()`

从原本的字符串选取范围分割并返回

```javascript
var str = "&0x200b";
str.substring(1,6)	//没错起始为1,不是0.
console.log(str)
//结果为&0x200
```



以及还有适配正则表达式的方法 

[^function for Regexp]: here

##### Extra

[^$的用法]: here

1. `${}`是什么? 

最简单应用 字符串拼接 引用一下你写的js时间显示代码

```javascript
var myDate = new Date();
	var Day = myDate.getDay();
	var Hour = myDate.getHours().toString().padStart(2,'0');
	var Minute = myDate.getMinutes().toString().padStart(2,'0');
	var Second = myDate.getSeconds().toString().padStart(2,'0');
	document.getElementById("Time").innerHTML ="现在是 "+Hour+":"+Minute+":"+Second;
```

一般来讲，你要拼接字符串就需要各个字符串之间加个`+`号,书写较为麻烦

而`${}`就是直接替代这个关联符号与字符串的包裹

```javascript
var myDate = new Date();
	var Day = myDate.getDay();
	var Hour = myDate.getHours().toString().padStart(2,'0');
	var Minute = myDate.getMinutes().toString().padStart(2,'0');
	var Second = myDate.getSeconds().toString().padStart(2,'0');
	document.getElementById("Time").innerHTML =`现在是${Hour}:${Minute}:${Second}`;
    //注：它需要反单引号来激活转义
```

*这个功能并不需要jQuery的封装 而是js原生代码就能使用*



2. **字符串转数组 `*.split("")`** 	(以及数组转字符串?) [^toarray] :

```javascript
var Str="abc-mng-zhang-mayi";
var newArray=Str.split("-");
console.log(newArray);
//应答为:newArray = ['abc','mng','zhang','mayi']
```



3. (提问) 那它到底怎么控制CSS?

错误方式 我想当然的方式[^False way:modify CSS string]

```javascript
var car2 = {
    color:"pink",
    model:"small",
}

var paper = document.getElementById("paper").style;
paper = car2;
```

想的很好，但并不能这么写

回顾JS的对象方式 

style是一个对象里的属性 其中包括其他的东西 并不仅仅只是上述的东西 而你直接这样覆盖是不行的



**The correct WAY**



> **通过 setAttribute 方法 设置元素的style属性** 
>
> 
>
> **语法：** 
>
> ```javascript
> element.setAttribute(attributename,attributevalue)
> ```
>
> **例如：** 
>
> ```javascript
> var a = document.body;
> a.setAttribute("style","background-color:red;height:100px;");
> 
> 
> ```
>
> 很麻烦，又不怎么语义化的样子，但管用
>
> **注意：**    两个参数都是字符串类型(它可以调用this噢)



****




它当然还可以打包成一组数据

格式要求`{}`包裹,并且分割不是`;` 而是`,`

~~有点像json的编写~~ 不对这就是json的编写(

```javascript
var api = {
  'lyric': 'http://music.163.com/api/song/lyric',
  'query': 'http://music.163.com/api/search/get/'
}
```



而我们把这称为

#### **对象(object)**

在含义上解释为数据的集合 包括上文的json与下文的数组

对象一般包含的内容

> json:**元素**/key &&  **值**/value
>
> (注:你不能对json使用`for of`,json里从`,`为止就是一个句子,即属性里只存在**值**这个概念)
>
> array:数组的构成就是**元素下标**与**值**(for in/of)



关于访问的点，会在下文的**array**讲到



而重点要讲的是JS自带的对象



##### 内建对象



而说到调用它们 就得搬出来一个function

###### **New**

本意创建

> New的过程 到底做了什么?	
>
> var yell = new student("beast",24)
>
> • 创建一个空对象并且this变量引用了该对象,同时还**继承**了该函数的原型。
>
> {
>
> 创建一个新的空对象；																		//var yell
> 将this绑定到该对象,此时任何对`this`的引用就是对`obj`的引用；yell = this
> 添加一个名为`__proto__`的新属性，`obj.__proto__`会指向`Student.prototype`; (yell继承了student库)
> 最终返回该this对象。 从而实现被函数里的this调用
>
> = {var yell = this←(yell) ← <u>yell =  Student.prototype()</u> ← student} = var yell = new Student()
>
> }
>
> • 属性和方法被添加至this引用的对象中。
> • 新创建的对象由this所引用,并且最后隐式地返回 this（如果没有显式的返回其它的对象）

被this绑定的对象 我们称作实例

即通过**构造函数**的new操作创建的对象是**实例对象**



****





###### **Date()** **日期对象**

> 一般常用
>
> ​	var myDate = new Date();
> ​	var Day = myDate.getDay();
> ​	var Hour = myDate.getHours();
> ​	var Minute = myDate.getMinutes();
> ​	var Second = myDate.getSeconds();
>
> 以及特殊的unix时间戳 //1970.01.01.00:00:00
>
>   var unix = myDate.getTime()
>
> 以及 转化字符串(你不转换 你怎么随意修改它的值呢)
>
> //ES6
>
> toString() 虽然也有toDateString()这种etc,但如果你只想要**数值**本身 那当然是直接前者最好
>
> 
>
> 以及ES2017里(ES8)
>
> 增加了PadStart()与PadEnd()
>
> 如果某个字符串不够指定长度，会在头部或尾部补全 
>
> ```
> .PadStart(2,"0")/.PadEnd(2,"0")	 //第二个参数缺省时会以空格代替
> //此处是以多少“位” 所以不会出现0为第一位的现象 头部指左 尾部指右
> 没错 就是 %2d/-%2d
> 
> 另一个用途是动态提示字符串格式.
>  
> '12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
> '09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
> ```



###### **Math对象**

> 有时候还真觉得把所有东西直接开启 不用你再输入什么东西额外开启还挺舒服的



`Math.*`用法以table形式展现

| 方法       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| abs(x)     | 返回数的绝对值。                                             |
| ceil(x)    | 对数进行上舍入。                                             |
| floor(x)   | 对数进行下舍入。                                             |
| sqrt(x)    | 返回数的平方根。                                             |
| min(x,y)   | 返回 x 和 y 中的最低值。                                     |
| max(x,y)   | 返回 x 和 y 中的最高值。                                     |
| pow(x,y)   | 返回 x 的 y 次幂。                                           |
| random()   | 返回 0 ~ 1 之间的随机数。                                    |
|**复杂计算**||
| log(x)     | 返回数的自然对数（底为e）。                                  |
| exp(x)     | 返回 e 的指数。                                              |
| round(x)   | 把数四舍五入为最接近的整数。                                 |
| toSource() | 返回该对象的源代码。                                         |
| valueOf()  | 返回 Math 对象的原始值。                                     |
| **三角函数** ||
| sin(x)     | 返回数的正弦。                                               |
| cos(x)     | 返回数的余弦。                                               |
| tan(x)     | 返回角的正切。                                               |
| asin(x)    | 返回数的反正弦值。                                           |
| acos(x)    | 返回数的反余弦值。                                           |
| atan(x)    | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。     |
| atan2(y,x) | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |



以及基础对象

`Math.PI` 自带的const PI=3.14

> 直接这样调用就行了 var PI = Math.PI;



###### **JSON对象**

什么是json? 为什么它会直接存在于JS规范里面 甚至还独立出来了一个格式？

> 早期时 数据传输都用一种xml的数据文件来传递
>
> 但是因其编写繁冗,因此占用带宽大,因此解析慢,所以再应对大量复杂信息流的时候逐渐不再是主流(场面话)
>
> 
>
> 虽然b站的弹幕以及各种数据库现在还是xml格式来储存，毕竟格式简单 由机器来编写也简单
>
> 流量和解析 以在现在的硬件来说完全不是事..
>
> //私人认为
>
> 所以现在更多的状况是json和xml并用 xml来储存一些简单的信息流 json来储存一些对格式要求
>
> 更为复杂的信息 比如要求非常多的分类etc.. 
>
> 这种看着一目了然的结构 自然更适合应对复杂数据流



**实例**:(某视频的弹幕xml)

 ```xml
<?xml version="1.0" encoding="utf-8"?>
<i>
<chatserver>chat.bilibili.com</chatserver>
<chatid>312258891</chatid>
<mission>0</mission>
<maxlimit>8000</maxlimit>
<state>0</state>
<real_name>0</real_name>
<source>k-v</source>
<d p="493.10000,1,25,16777215,1616410758,0,69d4a0e8,46802447104999431">？关键词察觉</d>
<d p="198.25200,1,25,16777215,1614958556,0,5f5c42b2,46041074962530309">晶姐表示很淦</d>
<d p="583.49500,1,25,16777215,1614958339,0,19e40eb4,46040961134362627">佑树的家</d>
<d p="432.43800,1,25,16777215,1614958305,0,19e40eb4,46040943464808455">可还行，佑树请客</d>
<d p="628.10300,1,25,16777215,1614957889,0,4d1f44b2,46040725128740869">嗨，辛苦了</d>
<d p="160.71200,1,25,16777215,1614957794,0,cd7eecc8,46040675264757765">快进到晶姐发现自己摊子掉进坑里</d>
<d p="596.94700,5,25,16777215,1614957445,0,fa370a04,46040492385763335">快，这里是警察局的近路（</d>
<d p="166.51900,1,25,16777215,1614957068,0,c7854631,46040294927368195">晶：你小子又在干啥</d>
<d p="188.28900,1,25,16777215,1614956239,0,a3b3d975,46039860124319749">说，骑士君经常带女的去好吗</d>
</i>
//除了前面的前缀 就只有弹幕这一种信息(数字代表着发送时间,颜色,位置,用户UID..) 编写生成这样的xml难度也低 就是看着很乱
 ```



**如果是json标示 这段代码应该表示成..**

```json
{
chatserver:"chat.bilibili.com",
chatid:"312258891",
.
.blablabla
danmuku(假设) = [
    {
  		name:"某个UID",
		danmus:{
            danmu1:["时间","位置","各种信息etc","danmu"],
            danmu2:["时间2","位置","各种信息etc","danmu"]
            //etc..
        	}
    },
        
    {
  		name:"某个UID2",
		danmus:{
            danmu1:["时间","位置","各种信息etc","danmu"],
            danmu2:["时间2","位置","各种信息etc","danmu"]
            //etc..
    	}
     }
]


```

是不是看着很整洁 但想也知道在简单数据流情况下把数据分割成几块来写会平白无故给自己添麻烦

所以大概还是专事专办吧



总之我认为json比起传输这些 对于编写存储调用它们的人来说更有意义,且更直观..



**括号**

那么在js/json里括号有着另外的含义

`{}` 花括号 (实际上意为大括号) 意为对象

`[]` 中括号 意味数组

实际上你也可以这样套

```javascript
var array = {name:"me",action:"move",method:["0","1",{select:"A",select2:"B"}]};
```



json对象转成json字符串

> 当数据在浏览器与服务器之间进行交换时，这些数据只能是文本。
>
> 并且我们能够把任何 JavaScript 对象(指你自己正在写的css配置)转换为 JSON，然后将 JSON 发送到服务器。
>

所以需要一个函数

`JSON.stringify(*)`

```javascript
var string = array.stringify();
JSON.stringify(array)
//change
"{"name":"me","action":"move","method":["0","1",{"select":"A","select2":"B"}]}"
实际上就是把括号也包进去使其彻底是一个字符串
```



以及"解压"方式

`JSON.parse(*)` 其实就是还原



#### ***面向对象**

什么是面向对象？

> Javascript是一种基于对象（object-based）的语言，你遇到的所有东西几乎都是对象。但是，它又不是一种真正的面向对象编程（例如java）语言，因为它的语法中没有`class`（类）。但是ES6上补充了class概念
>
> 
>
> 那么，如果我们要把"属性"（property）和"方法"（method），封装成一个对象，甚至要从原型对象生成一个实例对象，我们应该怎么做呢？

或者说 这样做有什么作用呢？



E1:

例如 你心血来潮 想创立两个猫

*本片段以**Cat**作为函数假定 **cat1/cat2..**作为new对象(实例)的假定

```javascript
var cat1 = {}; // 创建一个空对象
　　cat1.name = "大毛"; // 按照原型对象的属性赋值
　　cat1.color = "黄色";

var cat2 = {
     cat2.name = "二毛",
　　　cat2.color = "黑色"
  };

```

****

你有没有想过如果有个属性一样的猫都要重复写上共同的点“黑色” 是不是很麻烦

于是乎你想 直接创立一个function 当请求颜色需求时 直接接入它就好了

Patch E1:

```javascript
function color(){
	return "黑色";
}


var cat1 = {cat1.name="cat1", cat1.color=color()}
var cat2 = {cat2.name="cat2", cat2.color=color()}
//其实也没省多少功夫是吧
```

****

然后你在想 难道就不能在var变量的时候就直接生成好所有对应的属性的值吗？(像内置的Date()一样)

而且你的颜色也不一定只有黑啊 黄 白 之类的怎么办？



Patch E1.1:

```javascript
function Cat(name,color){
	return{
		name:name,
		color:color
	}
}

var cat1 = Cat("me","black")
//{name:"me",color:"black"} 
var cat2 = Cat("it","orange")
//{name:"it",color:"orange"} 

```

至少人性化多了

****

另一个问题 你的猫不可能只有这么两种属性 而且每个猫都有它们的特质

甚至是属性里面还可能包含了你对猫的评价，这些你不可能都挤在一个function里面慢慢输入



怎么办？

所以应该改变这种方式 将输入完善 

方式转变为类似纲目的方式 将绝对会有的性质 写在一个库上

然后将特殊的性质自己写上



还记得this么 正常情况下使用 会自动指向上一层 

然而一旦和实例对象绑定关系(new)后 会自动把调用this的function 给指向实例对象

**(既会认为新的实例对象为上一层)**

从而给实例对象设置属性与值



这就可以直接:

Patch E1.2

```javascript
function Cat(name,color){
    this.nationality="chinese"; //以及你可以额外添加这只猫的“固定属性”
	this.name=name;
	this.color=color;
}
var cat1 = new Cat("me","you")

//Cat{nationality: "chinese",color: "you",name: "me"}

```

****

这种就叫做**构建函数**



隐去掉function部分

这不就是你在调用内置对象时的步骤吗

> var cat1 = new Cat();

而你也没有过往内置对象里面赛新属性的念头，所以构建好的函数也不会接受直接往里赛属性



但是我们可以曲线救国

既然无法往固定好的函数往里面赛属性，那就整个**新变量**把它的函数内容搬过来

然后往新变量再塞**属性**不就行了？

> 待补充 也许是两个库选择性合并 也许是已继承的对象再添加另一个库里对象



E2:

##### 继承对象

 `prototype`(原型)/`__proto__`(原型对象)

prototype即为某个函数的原型,是个函数都会有这个属性

> 构造函数有一个prototype属性，指向实例对象的原型对象。通过**同一个**构造函数**实例**化的多个对象具有相同的原型对象。经常使用**原型对象**来实现继承





什么意思？

你构造出来的函数必有原型属性(`prototype`)指向你new出来实例对象的原型(`__proto__`)



那么`__proto__`又是什么玩意？

这是每个对象(除null外)都会有的属性，叫做`__proto__`，这个属性会指向该对象的原型。



usage1:

```javascript
Cat.prototype.fur = ?;
```

而这个过程到底做了什么?

Cat函数的原型属性多了一个自己新定义的属性重新赋值

你可以理解为Cat的子属性



E2.1:

```javascript
function Cat(name,color,description){
    this.nationality="chinese";
	this.name=name;
	this.color=color;
    this.description=description;
}

Cat.prototype.fur = "white"	//Cat的原型属性fur是指向于你new出来的cat1
Cat.prototype.voice = "loud";

var cat1 = new Cat("sli","orange")
//应答:Cat {nationality: "chinese", name: "sli", color: "orange"}(fur不在这里出现)
cat1.__proto__	//应答fur:"white"

var cat2 = new Cat("sily","black")
Cat.prototype.fur = "sort"
Cat.prototype.voice = "short"
cat2.__proto__
//{fur: "sort", voice: "short"}

//注：这样写会让cat1的__proto__属性多出fur:white，而非直接显示在cat1上
```



其实简单来说 就是除了本体function能存的东西以外

还有一个隐藏的proto存储

凡是调用了该函数的变量都可以访问该函数的prototype来访问proto分区

函数本身也能通过**\__proto__**来查看自己的proto 分区



那么关系明了:

函数的prototype指向了调用这函数(new)的所有对象

所有上文new的函数的`__proto__`属性全部指向了该函数

一旦函数的prototype一修改，下文的new对象的`__proto__`属性**全部都会被修改**

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151322530-1608157973.png)

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708152327825-11086376.png)



Extra:

> 如果你追加new对象的属性是proto的重复名字属性(下文简称const `__proto__` proto)
>
> 则调用该重名属性的时候会优先于你proto属性的属性
>
> 而你想调用proto属性里面的话
>
> 就需要cat1.__proto__.fur



这种方式只适合对种类的修改,并不适合具体描述单独的个体,说白了就是记录物种的特征会有用

除非你直接把特殊个体记录在proto分区里面

那你是真的厉害

****



##### Class类

[集全用法](https://googlechrome.github.io/samples/classes-es6/index.html) 

//**ES6**之后 引入了一个class属性

`class`是什么?

> 在ES6中，class (类)作为对象的模板被引入，可以通过 class 关键字定义类。
>
> class 的本质是 更严格权限管理的 function。类似java里class的作用

*<span style="color:red;">不过function允许被提升 而class不允许你提升</span>*

而`class`的继承对象`constructor`（构造对象）则充当了**实例执行**的作用



###### 构造函数

`constructor(){}`

- 构造函数其实说白了就是创建类的对象，只有对象才能调用一个类中的方法和属性
- 创建类的实例化对象时**默认**被调用 为空时默认为 return this跳出构造函数本体继续执行下一步

****

且class作为继承链 同时拥有 **\__proto__** 与 prototype属性

以及免除了繁冗的增加属性的步骤

```javascript
class Cat{
    constructor(name,color){
    	this.nationality="chinese";
		this.name = name;
		this.color = color;
	}
	
	//在class里 如果你要新增属性 你可以直接写入而不用再去书写*.prototype.*
    fur = "white";
	nationality="unknown"; //如果与构造器的属性冲突 会只使用构造器的值
	
}
var cat1 = new Cat("me","black");	//这样增加特殊属性的流程比单纯的用function快

//应答:Cat {fur: "white", nationality: "chinese", name: "me", color: "black"}
```



###### 关键字

既然是类似java一样的class 那也有class的各种关键字

###### **extends**(继承/扩展)

​	而既然有关于更明确的继承概念 那么`super()`就冒出来了

```javascript
class Polygon {
  constructor(height,width) {
    this.height = height;
    this.width = width;
     console.log(this.height,this.width)	//300 400
  }
   
}

class Square extends Polygon {
  constructor(height, width) {
      
    super(height, width);	//引入父类抛出的绑定属性，将父子类的this将这两个属性绑定

    this.height = 1;		//当然你也可以从父类取值完毕后 直接覆盖掉共同的属性
    this.width = 3;
      console.log(this.height,this.width)	//1 3
  }
	
  get area() {			//子属性划分 其实就是内置对象里的属性建立给外部调用
    return this.height * this.width;
  }
}
var A1 = new Square(300,400)
A1.area

此时 你就可以直接
<<var A1 = new Square(300,400)
<<A1.area
>>120000? 3!

(你当然也可以试着直接在this.func 上写代码 但是不能包括return与括号 所以还不如直接用use导出)

//但不建议直接附上var A1 = new Square(300,400).area
//因为在构造函数的时候默认返回
<<undefined
>>A1
<<3
```

此时作为子类的Square可以通过prototype访问到父类的Polygon

这也能够解释父类的this可以指向到子类 而子类通过super绑定后 直接将this绑定成为双向关系(即共同属性)



`super()`在这里做了什么工作?

在构造器里声明与父类对象this绑定

且从此除了this这个父子类共同继承的属性以外 还有super这种只作用于父类的方法

如果父类需要在构造器里与子类的变量链接的时候

```javascript
class A{
		constructor(x){
			this.x = x;	//3 or undefined
            //如果是this.x = 0
            console.log(this.x+"B")
      
		}
    
  	tips(){
      console.log("trigger")
    }

    
	}

class B extends A{
	constructor(x){
        super(x);	//则super就不需要带上对应的变量
        console.log(this.x)
    	this.x = 5;
        console.log(this.x+"M")
        
    }
    
    tips(){
        console.log(super.tips())	//super导向至父类的tips函数触发trigger
    }

    get use(){
      return this.tips()
    }
}

var C = new B(3)
C.use
```

就应该在super里填入对应的变量 以实现this链接

如果super里存在还未包含的绑定属性 将视作NaN/undefined处理



**注意**

> 1. 不允许父类**绑定**子类未构造的属性
> 2. **super要求出现在构造函数里子属性调用this以及函数之前 以便与父类class的对象串联起来**
> 3. super超类本质是将父子的相同属性用this绑定 并将父类的值引入(父类优先级大于子类)
> 4. 而如果super里未包含的绑定属性 将视作NaN/undefined处理
> 5. 而如果只是常值 则仅需要super();就能全部引入父类的非static对象
> 6. super是固定指向父层 即使子类属性已被this指向修改也会只指向父层的结果



class也允许你直接继承当前环境直接就有的类`Date...`

在这里也出现了之前链式调用没接触到`get`接口

它允许你将函数作为一个子属性抛出

​	<<为什么不直接用 this.xxx属性抛出?

​	\>\>因为属性不允许你直接抛出`return`与`{}` 



****

###### **static**(静态)

类似const 但是是给class内部的函数用的

因为你也不能直接在class内用const 那是外部该用的

不过思维是跟const一致的 一般也应用在函数这类不希望被更改的代码块上



调用规则是

```javascript
class Father {
    test1(){
        console.log("F1");
    }
    
    static test2(){
        console.log("F2");
    }
}

class Child2 extends Father {
    test1(){
        console.log("C1")
    }
    
    constructor(test){
         super();				//调用父类普通方法
         //console.log(super.test2()); 非static无法访问
         console.log(this.test1());	// C1
         console.log(super.test1())	// F1
    }
    
    static test2(){
        console.log("C2")
    }
    
    static test3(){
        return super.test1()+2;	// 调用父类静态方法
        //return super.test()报错 因为父类静态关键字不存在test这个对象！
    }
}

var A = new Child2()
A.test()

```



**注意**

> 1. 实例出来的变量不能像get use出来的接口直接丢给变量用
> 2. 且static关键字的对象仅能在父子类以super的形式调用
> 3. 而super属性固定调用父类的对象(child.static or child.super.fatherprop)
>





****

Extra



#### Array(数组/阵列)

Array可以包含任意的数据类型,同时也可变.

以`[]`来区分单纯的值



```javascript
var array = new Array()	//基本属性
var array = [1,2,3,4,5,6];
```



创建指定长度的数组

```javascript
const array = new Array(9).*fill("");
```



最简单的访问方式就是直接array['元素下标'] [^object_access]



以及**遍历访问**(迭代)

`for(let x in *)`

这允许你去从头顺序访问数组(一般从元素下标0开始)

```javascript
function Jsonchange(style){
        var string = [];
          for(let array in style){
              string.push(`${array}:"${style[array]}"`);
//注:json不允许使用*for of
```



为什么在这里需要用更低作用级别的let?

因为在这里变量实际上是作为数组的下标存在，这也是为什么这个变量叫什么其实都不重要.

反正叫什么都无所谓，但也不能与上级的`var`变量冲突 所以需要使用`let`.

 

而如果采用`for(let x of *)`

则会直接访问元素的**值**本身

对于纯数组 你只能用of来访问 否则你只能得到一堆index



对于json类 你应该要以json[x]\(带中括号的形式来访问值)

> 如果你用.*来访问属性 因为实际上你是在访问对象的元素 而元素 **并不存在** 你let所描述的变量 
>
> var me = {//blablablbalba
>
> }
>
> for(let p of me){console.log(me.p)}
>
> //undefined
>
> 而中括号这种有更好的兼容性 在遍历上let p会套进去循环会自动被当作为[0]然后随着循环的元素位置增加
>
> for(let p of me){console.log(me[p])}





实际上还有forEach	//**ES5.1**

```javascript
//用法是这样的
array.forEach(function(ele){
	console.log(ele)
});
//算是一个反向用法的for of.但你不可能破坏协调性去用吧(
```



> 趣事:如果你给array类型的name属性赋值后
>
> 在调用for in遍历后它会在最终把name这个属性名也给执行一遍(如果是单纯console.log打印会把name也输出在结果上)



以及

#### every

every()方法遍历可以达到break效果。

every的代码块种仍然不能使用break，continue，会抛出异常

```javascript
[1,2,3,4,5].every(function(i){
  if(i===2){
    return false; //return false等同于break
  }else{
    console.log(i)
    return true  // return true 等同于continue
  }
})
```

看着有点反直觉 不过至少也得看得懂



##### Map 和 Set(保留)

**现在的我并不清楚它们的实际意义**





#### 数组属性调用



##### **通用方法**

****


**长度** `*.length`

很合理，既然是一组数组那肯定也会和字符串一样有长度

不过与字符串长度不能被参与赋值计算不同的是，数组可以被增减长度

```javascript
//以上述array为例
array.length = 9;
console.log(a)

//浏览器应答
(9)[1,2,3,4,5,6,empty X3]
```

当然如果减少至超过完整的内容，数组也只会保留到割裂的长度



**索引** `*.indexOf()`	

通过元素获得下标索引 类似python里的`*.index()`

`lastIndexOf()` 方法返回指定文本在字符串中**最后**一次出现的索引



如果未找到文本， `indexOf()` 和 `lastIndexOf()` 均返回 -1。



> 所以一般判断返回有无结果的时候 通常会这样子
>
> if *.indexof() > 0



##### **特殊(数组)**

****

###### **组型变化**

**提取** `*.slice()` 不过其实只要一个数值就可以了	

`slice(?start,?end)`

```javascript
var array = [1,2,3,4]
array.slice(1,2)
//[2]
array()[1,2,3,4]
//注:slice的?start,?end都是代表着间隔之间提取的起终(不是数组的[0])位置 如果起点和终点都为同一个位置时则为空(毕竟是间隔提取)


```

与上文的 `*.substring()`差不多，不过是针对于数组用的

~~其实我更建议统一都用slice(~~



以及**分割/删除 提取**`*.splice`

```javascript
var array = [1,2,3,4];
array.splice(1,2) //此处第二个参数是以第一个参数为起点的多少个个数
//[2,3]
array()[1,4]
```



转为字符串	//ES6

`*.toString()`

没错 这个实际上是在数组对象里面的函数 只是也能对普通的数值生效

```
var ages = [32, 33, 16, 40];
ages = ages.toString()
//"32,33,16,40"
```



###### **值型变化**

**入栈/出栈**(确信)

**尾部**																				

> `*.push()`:追加,与python的append一样(其中不限字符串或者)
>
> 注:它不能用作最末尾添加字符串,会把内容以`""`包裹起来,用`*.join`
>
> `*.pop()`:消除.
>
> `*.join("")`:会临时新生成一个数组把**除最后一个元素之外**各个元素的末尾追加字符，其中内容为追加什么"符号",并且追加之后 数组会直接变成字符串

**头部长度**

> `*.unshift()` 追加,因为是在头部，所以这个操作会让数组长度**增长**一格
>
> `*.shift()`消除,因为是在头部，所以这个操作会让数组长度**减少**一格



****



**排序** `*.sort()`

> ```javascript
> var array2 = ["z","a","4d","4z","&8"]
> 
> array.sort()
> 
> //浏览器应答
> 
> (5)["&8", "4d", "4z", "a", "z"]
> ```

可以看出sort方法排序默认是由总体大到小，再由小到大的排序方法排列.

即先排位数，再排序大小



**逆向** `*.reserve()`	字如其意



**临时数组追加** `*.concat([new_data_here])`

> ```javascript
> array.concat([4,5,6])
> //浏览器返回
> (9)[1,2,3,4,5,6,4,5,6]
> ```
>
> 但是它并不会修改它原本的数组，相当于内存里划分了一个temp给你返回了新的数组.
>
> 适用你去加一些规定好的后缀赋值在另一个新变量里,但是它不适用于string的多个变量(噔噔咚)



fill填充 	//**ES6**

`fill(value,start,end)`

使用固定值填充数组

```javascript
var ages = [32, 33, 16, 40];
ages.fill("null",0,3);
["null", "null", "null", 40]
```

//*start与end都指正常的数组位置



###### **应答**

**过滤** `*.filter(function)`

根据你设立的function返回符合条件的数组

因为filter是为数组设立的function,所以它并不需要你去...rest来接收所有的元素

因为你本来就传了个数组进去 不是分散开来传



简简单单实例

```javascript
var height = [162,156,176,181];

var requirement = function(height){
	return height >= 170
}
height.filter(requirement)
//[176, 181]

如果按照一般方法?
function height_filter(height){
var temp = [];
for(let x of height){
     if(x > 170)    temp.push(x);
    }
return temp;
}
//[176, 181]

//草 你看用filter多简单
```



当然你也可往function里塞正则筛选 这样就能对数组进行等同于字符串的筛选操作了



#### Null&Undefined

之所以把它们摆一起讲 是因为从**值**上来讲它们是**一样**的

但是如果是**数据类型**来讲，它们是**不一样**的

> typeof undefined       // undefined
> typeof null         // object
> null === undefined      // false
> null == undefined      // true





那么它们本身是有什么意义？

> 在JS里 null 代表着什么都没有,所以比较明显的作用就是
>
> 你可以通过将一个对象赋值为null代表**清除**数值以及它的**内存占用**（等效于 `delete Window.*`）
>
> 
>
> 而undefined代表着没有赋值变量的默认值
>
> null是真的清空掉，你可以先赋值null清空，再赋值undefined让这个变量重新存在
>
> 不过鉴于它们的值都是一样，这样做确实没什么意义是了(
>
> *意义还是有的 脚本里要先判断该变量存不存在 再对变量进行赋值以减少出错



##### **Extra**

```
var a 
//undefined
var a = null
typeof a
//返回结果是"object" 这是历史遗留bug
```

 [^bug_of_typeof] 

**为什么对于基本类型的null 却返回了object呢?**

> 对于 null 来说，虽然它是基本类型，但是会显示 object，这是一个存在很久了的 Bug
>
> ```javascript
> typeof null // 'object'
> ```
>
> 为什么会出现这种情况呢？因为在 JS 的最初版本中，使用的是 32 位系统，为了性能考虑使用低位存储了变量的类型信息，000 开头代表是对象，然而 null 表示为全零，所以将它错误的判断为 object 。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是一直流传下来。
>
> 为了避免这种问题，我们可以通过 Object.prototype.toString.call(xx)进行判断类型
>
> ```javascript
> Object.prototype.toString.call()
> ```
>
> //也就是说,在遇到可能出现null的判断里 要使用这个替代掉typeof()
>
> [null为什么会判定会对象？(From CSDN)](https://blog.csdn.net/qq_41969216/article/details/89966801)



### 3、运算符(特殊)

JS里除了基本的运算符号，还有额外的运算符号



**Extra**

`＝`

一个等号是赋值操作

==先转换类型再比较

===先判断类型，如果不是同一类型直接为false



`*` mutli

JS里`**`代表着幂运算等效`Math.pow(x,2)`



and`&&` 

or`||` 

除了和C相同的地方

```javascript
console.log( 5 && 4 );//当结果为真时，返回第二个为真的值4 
console.log( 0 && 4 );//当结果为假时，返回第一个为假的值0 
console.log( 5 || 4 );//当结果为真时，返回第一个为真的值5 
console.log( 0 || 0 );//当结果为假时，返回第二个为假的值0 
console.log((3||2)&&(5||0));//5 
console.log(!5);//false 
console.log(x || y || z || alpha || beta ...)谁真先取谁,全假取最后
console.log(x && y && z && alpha && beta ...)全真取最后,谁假先取谁
```



而在JS定义里

0和`''`空字符串都为默认的false值

什么意思？

你可以

```javascript
var test = function(x,y){
this.x = x;
this.y = y || undefined;
}
var me = new test(3)
//test {x: 3, y: undefined}
```

如果没有参数则返回未定义

想也知道挺实用的 根据其它选项判断undefined就缺省使用某选项...或者直接往上面写字符串都行

它还有另一种用途就是直接调用浏览器属性，如果不支持就执行兼容性更高的属性，以此类推..

```javascript
var w = window.innerWidth	//基本通用
|| document.documentElement.clientWidth	//IE11-
|| document.body.clientWidth;	//IE8-
我倒要看看谁还在用IE.jpg
```



### 4、function(函数) [^function-toString]

#### 构建

function有多种表达形式

有三种，不过我喜欢用这两种

>```javascript
>function sum(a, b){
>var counter = a + b;
>document.write(counter);
>}
>
>sum(a, b);
>```



>```javascript
>var show2 = function(a, b){
>var counter = a + b;
>document.write(counter);
>}
>
>show2(a, b);
>//注 如果调用函数时的参数如果没有对应 缺少会Nan 多出则不参与计算
>//C则更严格 提示few/much arguments.
>
>```

其中 var变量创建的函数 如果你在此函数编写之前调用它 则会被报错(合理)

而直接function的就不会



#### 事件(Event)

名义上来讲 是**触发**function的行动.

这里触发有很多个但分为**行动触发**和**提前规则制定(IIFE)**

常见如:

| 事件          | 描述                                         |
| :------------ | :------------------------------------------- |
| onchange()    | HTML 元素已被改变                            |
| onclick()     | 用户点击了 HTML 元素                         |
| onmouseover() | 用户把鼠标移动到 HTML 元素上                 |
| onmouseout()  | 用户把鼠标移开 HTML 元素                     |
| onkeydown()   | 用户按下键盘按键                             |
| onload()      | 浏览器已经完成页面加载(可以理解为更次的IIFE) |





#### 参数

顾名思义:在调用函数时，您可以向其传递值，这些值被称为参数



**参数名词**

<div id="gap"
    style="
    border:1px solid black;
	height:1px;
	border-top:1px;">
</div>

##### **arguments**对象

本意就是参数，即代表传递进function里的**所有参数**这个属性，最常见用法就是配合for实现**实时**的类似for in效果

```javascript
var rank = function(x){
    for(let i = 0;i<arguments.length;i++){
       //execute code
        console.log(arguments[i])//结果就是你输入的所有内容
    }
}
```

作用:非常大，大到无法说出具体应用(太广泛了) 配合prompt弹窗能烦死你的那种



##### **Rest**

多参数的特定处理

情景:如果你想挑出想要的参数，怎么筛选？

如果说多个参数里面 我嗯要挑倒数第二个

> ES5及以下做法 
>
> ```javascript
> var rank = function(x){
>  if (arguments.length>2){
> 		let i = arguments[arguments.length-2];//因为是数组,它是以0开始
>      console.log(i);
>  }
> }
> 
> ```
>
> 以及我想排除掉第一个参数
>
> ```
> var y = 0;
> var rank = function(x){
>  if (arguments.length>2){
>  var array = [];
> 	for(let i in arguments){
> 		y++;
> 		var x = arguments[y]
> 		array.push(x);
> 	}
> 	array.pop()
>  }
>  else{
>  	console.log(x)
>  }
>  
>  console.log(array);
> }
> //是不是巨麻烦
> 
> ```
>
> 在此 ES6新功能`...rest`
>
> [^三个点的含义]: ?
>
> ```javascript
> var rank = function(x,...rest){
>     
>  //只要倒数第二个
>     
>  //rest功能:if 直接等效if arugments.length>2
> 	let i = arguments[arguments.length-2];  //因为是数组,它是以0开始
>     
>     
>      console.log(i);
>     //4
>  /*同理，前面出现多少个参数就自带判断是否有X个以上的参数，且多余的参数会被归为一个数组里面
>  方便你进行后续的细分操作
>  */
>     
>  	console.log(rest)	//其余的 未划分区域
> }
> rank(1,2,3,4,5)
> //[2,3,4]
> ```
>
> 





#### **错误/条件判断 异常应答**

在C的经验里处理过这些案例，本质上以debug的方式将试错方案写进去

然后以在程序中的方案去应对错误从而规避程序崩溃



如果你仅仅只是因为输入了一个错误的值就导致蓝屏或者程序FC

那确实是个很蠢的应答错误



**`try&catch`**

**try**语句允许我们定义在执行时进行错误测试的代码块。

**catch** 语句允许我们定义当 **try** 代码块发生错误时，所执行的代码块。



***finally** 语句在 try 和 catch 之后无论有无异常都会执行。(类似`switch`语句的`default`)



用法:

```JavaScript
try {
    adddlert("欢迎光临！");
}

catch(err) {
    document.getElementById("demo").innerHTML = err.message;
}
//浏览器应答adddlert is not defined

finally {
    finallyCode - 无论 try / catch 结果如何都会执行的代码块
}
```

> 不过说实话，有直接**F12**审查元素断点的效率高吗(存疑





`Throw` 抛出异常

**throw** 语句能够创建自定义应答错误

```JavaScript
function myFunction() {
    var message, x;
    x = prompt("please input number");
    try { 
        if(x == "")  throw "为空";
        if(isNaN(x)) throw "不是一个数字";
        if(x > 10)   throw "太大了";
        if(x < 5)    throw "太小了";
    }//try throw出的值会被catch接收 此例为err的实参(类似return?)
    catch(err) {
        message.innerHTML = "输入的值 " + err;
    }
}
```



> 本质上就是一个碰到什么情况下抛出什么值的语句，所以你也可以像上面一样当成条件触发语句使用
>
> 不过不同的是 当错误发生时， JavaScript 会停止执行并抛出错误信息。
>
> 也就是说 这只会执行**一次**，并不会出现switch那样执行到break为止







#### This(引用)

它拥有不同的值，具体取决于它的使用位置：

> 在一个方法中，`this` 指的是该对象(var)的所有**属性**。(JavaScript ***方法***是包含*函数定义*的属性。)
>
> 单独的情况下，this 指的是全局对象(当然函数也是个对象)。				  //return `this.*()`
>
> 在函数中，this 指的是全局对象.   															  //return window.*
>
> *在函数中，严格模式下，this 是 undefined。("use strict")
>
> 在事件中，this 指的是接收事件的元素。(?)
>
> 当你使用new的情况下 this是绝对绑定于new的对象



比如

**`This.*()` 指整个<script>里能找到的function**

```javascript
var cal1 = function(s){
	s**s;
	return s;
}

function result(){
	this.cal1()
	balbla
}
```

个人认为的意义：虽然JS允许function嵌套 但有个这个你也不用一个个function里去额外去写 写了一个然后调用就行



还挺像java里的

class a{}

然后int B = new a

就能直接调用class a的内容了

不过这里只有function



**This-对象里的函数**

它也允许你function内直接调用传递进来的实参

```javascript
// 创建对象：
var person = {			
  firstName: "Bill",
  lastName : "Gates",
  fullName : function() {		//函数
    return this.firstName + " " + this.lastName;	//而这里的this即意为
  }
};
//如果你要把属性值写到另一个var上或者只是调用它 请结合call()来使用

```

意义:在于json里多一个交互接口来更新它的值



###### **Extra**

[Return&This(From CSDN)](https://blog.csdn.net/sunhl951/article/details/80023347)

> ***return的是Object。*** **这种情况下，不再返回this对象，而是返回return语句的返回值。**
>

作证语句1

```javascript
function user(){
	this.id = 1;
	this.val = 2;
    var c = 3;
    d = 4;
		console.log(this)//user{id:1,val:2}
	return {x:12};	//return应该只能被执行一次,且如执行中括号内容时,就直接输出(毕竟相当于直接覆盖内容)
    return this;	//user{id:1,val:2}
    //而return this作用 更像是强调必须返回this到new的新变量上 所以我认为只是个语义化的东西..
    //因为你写个return 0也会照绑无误
    
}
var a = new user();
console.log(a.x);
//12;
```

> 在函数中，函数的拥有者默认绑定 this。
> 因此，在函数中，this 指的是全局对象 [object Window]。
>
> 在你new的过程中，this也会指向`a`这个新对象
>



根据顺序 this应该先绑定了对象a 然后再去执行user

结果会是什么?

1. this指向了a
2. a继承了user的属性 
3. user的属性是什么？
4. 是两个this与一个var c 和 Window.d
5. user里的this是什么?
6. 因为new是指向user函数里的全局对象 即user里的含有的`this.*` 
7. 所以结果是返回了user{id:1,val:2} c因为是局部变量不返回 d是全局变量(Window)不返回





#### **Call(调用其他var)**

它可以用来调用**所有者对象**作为参数的方法。

> Call(Object,"argument","argument"....) 
>
> //此处argument意味后续追加的字符串当然也可以空参直接Call(Object)完事



通过call()，能够使用属于另一个对象的方法。

类似this引用，也通常结合this使用

毕竟this在方法里就是意味着调用者的所有属性，这也包括了又call调用来的var



但是是两极反转 是执行者去选择调用**对象** 所以一般于this搭配调用**对象**里面的**属性**

```javascript
var person = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName:"Bill",
    lastName: "Gates",
}
var person2 = {
    firstName:"Steve",
    lastName: "Jobs",
}
person.fullName.call(person1);  // 把person1的属性开放给person调用 使其能被person找到

//思维：你想调用person1，你就应该return this.person1.firstName blabla符合逻辑
//而它又不能直接person.fullName(this.person1)
这样做传不了参数，毕竟 this代表着person这个对象 你不能指望它在外面的对象里面寻找(
//而call就是帮你把其他对象也整合进person这个对象里让你去this引用

```



#### **Apply(修改this的指向)**

由与Call()相似 不过作用对象是**this**本身，Call实际上还是**对象**(Var)本身

所以。。用法是相似的

```javascript
var person = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName:"Bill",
    lastName: "Gates",
}
var person2 = {
    firstName:"Steve",
    lastName: "Jobs",
}
person.fullName.apply(person1);  // 将返回 "Bill Gates"
//没错 只是单纯把上例的call改成了apply,但是作用对象是本person的this指向
//上文的指向是将其他对象给整到请求对象里方便this调用
```



> 除此之外的不同之处就是 Apply支持数组参数的添加 call不行
>
> Apply(person1,["asd","123","0-9",etc..])
>
> Call(person1,"asd","123","234",etc..)
>
> 
>
> 为什么要做这样奇怪的差异..

#### **return**

终止

单意义来讲就是终止函数并返回一个值给调用它的函数.

> return 的结果可以是任何对象
>
> + 可以是一个数值
>
> + 一串字符
>
> + 一个dom节点
>
> + 一个窗口等等
>
> + 也可以renturn 函数本身



return a =  a.value

return "a" = a(str)





**return this的含义**

this是指向当前调用它的对象(当前层)，则return this就是相当于回去上一层

可以返回对象本身这样子可以进行链式调用



##### **链式调用**

然而更日常的使用是 一个按钮就能触发一整套流程

而目前的教程都只能function套一个function 最多最后再return一个function

这明显不够用 更需要一种类似流水式的流程调用



而这种return this就能配合这个使用

```javascript
var float_cal = function(a,b){
    var result = 0;
	return{
		step1:function(){		//step1(){
			result += a;
			return this;		//类似被goto回主菜单 这样你就可以重复选择stepX方法
		},
		
		step2:function(){
            result += b;
            return result;
		}
	}
}

//float_cal(3,4).step1().step1().step1().step2()
//13


```

实际上，链式其实就是JS各种封装后方法的组成 比如Math.pow()什么的

你可以设计一个按钮进入模式 最后以"="按钮导向return result 以终止blabla的





#### 闭包

函数里面的所有变量都是局部作用域 且在函数执行完毕之后 所有局部变量统统被重置

这也是全局变量不可能访问的了局部变量的原因 毕竟执行一次还没返回给你值就被重置 调用出来也没有意义



而闭包 通过局部变量可以访问全局变量的特性

以实例来讲就是用函数再套一层函数 而用更内层的函数的局部变量再丢给外面的全局变量 

```javascript
var result;
var loop = function(){
	var me;
	return function(a){
		var me2 = a;
		me = me2;
        result = me;
		console.log(result) //result成功的继承了内部me2的值
	}
}

loop()(3)
>>3
--
var quick = loop()
quick(3)
>>3

//你也可以在一个function里套多层return function并在每层都整个return this
//只是这样你在代码调用就需要	float_cal().step1()()()()()...etc来调用内层的function
```

有什么用？如果仅仅只是想把内部变量取出 用return不就够了吗?



虽然return确实能达到一种效果 但也只限一次弹出的机会，你当然可以写个数组将里面的临时局部变量全部保存起来然后return弹出(费时费力) 但如果我套多层呢？那工作量岂不是要激增 而且把所有局部变量全想办法堆出去发射的行为不也是闭包的思想么(



比如此例子

```javascript
var loop = function(){
	var me=0;
   
	return function(a){
		var me2 = a;
		me = me2;
        return me
	}
	
    console.log(4)//因为 return 被跳过 无法执行后续命令 这也意味着return这个步骤应推荐最后执行
    
}

loop()(3)
>>3
```

return的能力面对复杂的要求时 总归能力有限



不如直接递给全局/外部变量来处理 还不会被中断



Exp1:函数调用次数

```javascript
var a=0;
var test = function(){
	return function(times){
	a++;
	console.log(a)
	}
}

//快捷调用就直接用
var quick = test()
//毕竟quick已经在test内 再传一个参数的对象那就只有默认的闭包函数了
quick(1)
```



#### ES6额外内容

箭头函数（Arrow Function）`=>`

不需要 function 关键字、return 关键字以及*花括号*。

<div style="color:red">但是</div>
当我们使用箭头函数的时候，箭头函数会默认帮我们绑定外层 this 的值，所以在箭头函数中 this 的值和外层的 this 是一样的。

既然是默认绑定的东西 也就意味着固定 所以它应该适应它的**作用**:拿来写一些简简单单的函数体

使用 const 比使用 var 更安全，因为函数表达式**应该**始终是常量值。

```javascript
// ES5
var Cat = function(name, color) {
    return{
    name:name,
   	color:color 
    }
   
}

// ES6
const Cat = (name,color) => {return {name:name,color:color}}
是的要实现上面的内容得两个花括号(
    一个代表着执行的代码块	//{return }
    一个代表着对象内容
    其实这样还写还挺麻烦的
    
所以建议还是这么用
	//ES5
function flick(x,y){return x+y}
	//ES6
const flick = (x,y) =>  (x+y)	//return x+y

以及这样用
() => counter++ 不需要额外的参数传入 直接空着 也不需要函数名 因为上层会直接调用它
```

如果函数执行体只是单个语句，则能省略 `return` 关键字和`{}` 这样会更简洁



***Extra**

**IIFE()** 类似于提前订好的规则 是一个在定义时就会立即执行的"function"



```javascript
(function () {
   delete window.RTCPeerConnection
})();

```



用途 如果你需要在加载整个网页之前就要调用某个脚本的某功能的话

你就得需要这个规则 来提前部署功能(body标签前的script标签)

 而不是等网页加载完之后(特别是油猴里的一些userscript) 再去调用 这样可能会引起js的不稳定性. 



### 5、操作BOM对象

**浏览器对象模型（Browser Object Model (BOM)）允许 JavaScript 与浏览器对话。**

#### **Window 对象**

所有浏览器都支持 *window* 对象。它代表浏览器的窗口。

所有全局 JavaScript 对象，函数和变量自动成为 window 对象的成员。

全局变量是 window 对象的属性。

全局函数是 window 对象的方法。(From w3school)



它有除了全局对象之外的什么属性呢？

前面说到BOM是JavaScript与浏览器交互的方式 那就当然少不了获取**window**信息了(



#### **窗口大小**

`*.innerHeight/outerHeight`

`*.innerWidth/outerWidth`

感觉用outerHeight更符合使用描述的窗口习惯 就是视窗大小

Inner就是书签/工具栏之下的内容



还有获取该浏览器的运行平台等..

`navigator` 导航(领 航 员) 你缩写的nav的原型就是这个

nav对象有好几个属性 其中我们最常用的获取运行信息和UA(user-agent)

```javascript
navigator.appVersion
"5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36"

navigator.userAgent
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36"
这两种 一般调用的都是UA属性
```

但是对于开发者来说 很少去调用UA属性 因为看看你的via设置(它是可以被修改的

聊胜于无？



#### 屏幕大小

你问为什么有了窗口大小还需要屏幕大小这个信息？

因为不是所有时刻你的窗口都是最大化啊 kora,获取你的屏幕大小 能更好判断出用什么情况用什么css/js适配blablabla

`screen`

```
screen.width/height
//*.colorDepth 色深 8 >= 24 10bit >= 32
```



#### url信息

封装了对当前url的各种操作以及属性查看接口

`location`

除开基本信息host/href之外

```javascript
location.host	应答当前主机名
location.href	应答当前链接
大概用于判断什么链接时就应用什么json
```

对于一些针对某域名的脚本来说

就是会先调用href来储存当前域名

然后再后续的操作里面调用match之类的函数来检测匹配是否在域名下,在时则启用脚本



刷新

> location.reload()	//刷新 它当然是个方法啊(



历史记录

`history`

其实就是浏览器的回退/前进

> history.back()
>
> history.front()





还有个习以为常的封装UI

`document`

这实际上是DOM的侧重点，所以这里只介绍属性

指访问属性能得到的东西

```javascript
document.title
document.cookie
```



****

### 6、操作DOM对象

DOM (Document Object Model) 译为**文档对象模型**，是 HTML 和 XML 文档的编程接口。

HTML DOM 定义了访问和操作 HTML 文档的标准方法。

DOM 以树结构表达 HTML 文档.



什么意思？

事实上你一个tag或一处div id它都是一处DOM节点，没有上面的节点存在，自然也就不会有下面的分支

根据 W3C 的 HTML DOM 标准，HTML 文档中的**所有内容**都是节点：

> - 整个文档是一个文档节点
> - 每个 HTML 元素是元素节点
> - HTML 元素内的文本是文本节点
> - 每个 HTML 属性是属性节点
> - 注释是注释节点

而你要操作DOM节点 那必然要先获得DOM节点



它遵循着这样的加载/**变动后加载**的流程 [^DOM注意事项]

1. 解析HTML结构

2. 加载外部脚本和样式表文件

3. 解析并执行脚本代码

4. 构造HTML DOM模型

5. 加载图片等外部文件

6. 页面加载完毕



从以上顺序可以看出，**js等脚本会在DOM文档构造之前执行，**这样js就无法访问DOM文档对象模型。所以一般把可执行脚本放在页面初始化事件处理(onload/ready)函数中，这样能确保文档加载完毕后再执行脚本。





#### **获取**

经典*document*文档操作

> document.getElementByTagName("p") 对应着从头开始数的p标签 如果往上加上数字 则会对应第X个p标签
>
> 另一种写法
>
> document.getElementsByTagName("p")[1] (代表p标签下的第二个标签/0即为P1它自己)
>
> 和直接调用ID名
>
> document.getElementById("id") 
>



以及querySelector/All 同样用法上都是

document.querySelector(CSS selector)



那到底有啥区别？

1.区别更大在于 querySelector是静态的 getElement是动态的

如果我写一个

> var lis = ul.getElementByTagName("li");
>
> for(var i = 0;i< lis.length;i++){
>
> lis.appendChild(document.createElement("li"));
>
> }
>
>  
>
> 如果一开始就存在一个li标签的话 它会直接无限循环 这也证明了getElement的动态更新特性



而如果替换成querySelector

> var lis = ul.querySelectorAll("li");
>
> for(var i = 0;i< lis.length;i++){
>
> lis.appendChild(document.createElement("li"));
>
> }
>
> 它就仅能按照原本的li数量执行一次
>
> 同样 如果你打开网页之后在控制台上手动创建li元素 也不会被检测到



但是 这种需要特别以静态和动态区分的特性到底有什么用？

> 也许就和某些故意需要const的变量一个道理..
>
> 我可能需要一直使用初始化的值 且不在耗费更多变量的前提下使用



不过说实话 如果想调用一些单独的tag

queryselector()可比tagName()方便 ~~都没有直接引入jQuery $("body")方便~~

如果只是想访问body的属性而非标签表面 还是直接jquery $("body").css() 方便



以及相对关系的父子&兄弟节点

parent、child、sibling(同胞节点即为拥有相同父节点的节点)

![Node tree](https://www.runoob.com/wp-content/uploads/2013/09/dom_navigate.gif)

> parentNode.children (获取父节点下的所有节点)
>
> father.firstChild
>
> father.lastChild
>
> *.previousSibling/nextSibling



**更新**

这里笔记不再赘叙更新 改变即是更新



#### **删除**

首先先说明一点 该节点不能执行删除自己的属性， 只能父和兄弟节点里执行删除该节点

一般都是获取父节点，然后再父节点里删除该节点

> father.removeChild(Node)

```
var me = document.getElementById("p2");
var father = p2.parentElement;
father.removeChild(p2)

---

father.children

father.removeChild(father.child[1])
```

而且 删除是个动态的过程

还记得father.children的回报内容么

> <<HTMLcollection(3) [h1, p1, p2]



这意味着

当你删除掉任意一个节点时,child属性会被发生变化

如果有三个节点 你删除掉了[1] 再去执行删除[2]就会报错



思考:到底是什么情况会需要特地去删除节点呢？



#### **添加**

(与其说是添加 不如说是剪切?)

> father.appendChild()

前文也说过 实际上你给原本空的内容添加了内容 实际上就是了添加了节点(可能会是文字 会是元素 也可能是属性)

示例：

```html
<h1>title</h1>
<div id="father">
<p id="1">1</p>
<p id="2">2</p>
<p id="3">3</p>

</div>

<div id ="js">js</div>

<script>
var father = document.getElementById("father")
var js = document.getElementById("js")
</script>

<< father.appendChild(js)

>>  <h1>title</h1>
	<div id="father">
	<p id="1">1</p>
	<p id="2">2</p>
	<p id="3">3</p>
	<div id ="js">js</div>
	</div>
```



**创建**

****

元素节点

你还可以真正意义上创建一个新的元素节点

> document.createElement("p")

然后在这新的节点上加属性 配上计时器或者简单的for循环的话 就能批量制造某个什么单位了

比如飘雪或者下雨 或者什么流星划过特效etc..

参考rain/snow



当然 新建的标签会默认处在网页的末端，如果你要添加特定的地方

你就应该为该元素添上**ID**让父节点得以添加进去

> var p4 = document.createElement("p")
>
> p4.id = "p4"
>
> father.appendChild(p4)



当然还有

标签节点\<script>,\<style>,\<link>...etc

也是可以通过createElement("script")之类的添加进去



不过事实上 真正的内容不是它们的这个框架 而是它们要执行的内容

它们都可以通过`setAttribute(prop,val)`这种方式直接加属性与值

****

**插入**

>  Node.insertBefore(Node末,Node起)

简单来说就是在两个节点之中插入新节点 append仅支持末尾 而这个就是任意

```
var 1 = doc.get("1");
var 2 = doc.get("2");
var 3 = doc.get("3");

1
2
3

3.insertBefore(2,1);

<<
1
3
2
```







****

#### 事件监听

**addEventListener("event",function(),(capture))**

> -event 必须字符串，指定事件名。
>
> capture(可选) 指定是否在捕获阶段执行

为某个元素添加监视器,当用户对某个元素执行什么操作之后 就会触发该监视器执行内容

> document.addEventListener("click", function()
> {
>     body.innerHTML = "Hello World";
> });
>
> 像这种就是点(click)任何地方都会让#demo 替换为Hello world
>
> 估计还能替代计时器的作用
>
> 
>
> 顺带jquery的.on 原型就是这个
>
> .on("click", handler)



当然 既然有添加 那必然也有删除

removeEventListener()/off("click", handler)

****

#### **设置属性**

是的 你单拥有个标签是没有任何用的 你得给它们加上属性才会有大用

例如\<div style="">或者\<style>(InnerHtml)\</style>这样才会有用处

于是乎通过设置属性的子属性就来了 setAttribute

用法:

> *.setAttribute("Attr",value)



示例：

```javascript
ul_link_item.setAttribute("style",this.Json())
```

是的 val部分甚至可以是一个对象 如果val是字符串的话就要手动包裹

这一段说明该变量的style属性指向json函数里面的内容



或者

```javascript
var other_style = document.createElement("style");
other_style.innerHTML = "body{background-color:black;}"
var me = document.getElementsByTagName("head")[0].appendChild(other_style)
```



注:*寒冰兔说有了jQuery来实现的话 会轻松更多 建议赶紧学会以打开新世界*



### 7、操作表格

Form(表格单) 表格单作为前端给用户提交信息的的渠道 可以说是非常重要

这里简短过一遍HTML里的基础内容

form method="post/hidden" (明文/秘文) action=""提交时的行动

input包含的所有属性(name=组/value=填入值,placeholer=提示)

> input type="text" 输入框*
>
> *radio 单选 
>
> *checkbox 复选 
>
> textarea 文字输入框

*1 需要添加name属性以绑定为同一列选项(submit时也能给服务器回报正确的值),value便为真选项(传递的值)

*2 ID是为了能够锁定该标签



这里主要的是记录运用表格单的属性去获得 或者 修改值 以此传递到服务器或给用户



怎么体现？

比如最基础的value属性

```html
例如 有这么几行
<form action="post">
姓名: <input type="textarea" id="text"></input> <br>
性别: <input type="checkbox" id="check_ch1" value="me" name="choose" descripton>男</input>
	 <input type="checkbox" id="check_ch2" value="you" name="choose">女</input>

</form>

此时 你用doc锁定了ID 绑定到变量上
通过变量的子属性来获得它们的value
```



> 姓名: 哼哼 啊啊啊啊啊
> 性别: - [X] 男 - [ ] 女
>
> var text = document.getElementById("text")
> text.value
> "哼哼 啊啊啊啊啊"
>
> 
>
> 以及选择框的作答与否
>
> var choose = document.getElementById("check_ch1")
>
> choose.checked
>
> << true
>
> 或者直接定义value的值/checked的状态



但是这些实际上有什么用呢

前端嘛 就得给数据打包好 理论上来说 至少是前端以内可以处理好的东西就搞定完毕 再丢给服务器

在此之前还能使用js代码对输入数据进行验证/传输加密

****

#### 明文信息加密(MD5加密)

尽管MD5碰撞理论出现已久 但..有加密好过明文直接泄露不知多少倍

> 我可不会直接写出个js加密
>
> 所以直接调用别人的js好了(悲
>
> 
>
> 兴许你顺便能看懂它在写什么



usage:

```javascript
具体例子:

<script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
<script type="text/javascript">
function md5_encry(){
	var username = document.getElementById("username");
	var password = document.getElementById("password");
	password.value = md5(password.value);
	console.log(password.value)
}
</script>

<form action="#" method="post">
username: <input type="text" id="username" name="username"></input> <br>
password: <input type="password" id="password" name="password"></input> <br>
<button type="sumbit" onclick="md5_encry()">提交</buttom>
</form>

```



不过实话说..我想应该会有比这更好 更安全的加密方式 毕竟这里也只是基础js嘛..



总而言之 还是继续学罢(



### 8、计时器

setTimeout(exec,ms)/setInterval(exec,ms) 这两个在一般开发的时候用的最多



且你也知道setTimeout的受影响程度(根据你要执行的代码复杂程度)非常大

且setTimeout仅仅是改变了 内存中的值

如果你是靠它来实现动画的话 你还需要等下一次浏览器layout 属于是雪上加霜了



然后你也知道setInterval也不是万能的 毕竟JS只能利用单线程 延迟? 

你连切后台挂半小时的显示时间function都能给你个延迟0-1s



更别说那些网页上随着鼠标移动的一些些粒子特效了

****

那咋办？

异步ajax是一个方法,但你确实也没学到这边



部分详细内容移至css相关来看

在H5引入canvas相关里有这么个API

**requestAnimationFrame()**

请求动画帧？ 向谁要?



向你的屏幕刷新率要

> requestAnimationFrame(callback)
>
> 为什么参数是回调函数? 因为它的作用本来就是把其他要执行的函数递给**真正刷新动画帧后要执行的行为**
>
> 且其中 因为本身该函数会有一种固定值(你的屏幕刷新率) 
>
> 所以你传递给它的函数上应该有个形参给予后续调用



能保持你显示器每刷新一hz就绝对会有一hz对应的响应 那动画自然就会流畅且节流



**usage**

> window.requestAnimationFrame(console.log)
>
> << 59246.272

得出 默认返回的当前屏幕刷新的时候的 **打开网页之后的时间戳**

也就是说 思路是根据时间戳 某件事件被触发后定义一个起始变量 定住一个时间戳 

然后根据屏幕不断刷新的时间戳减去起始的时间戳

用造成数据差的**变量**以实现动画变动



```javascript
let start_timestamp;	

	function increase(timestamp){
		if (start_timestamp === undefined)   start_timestamp = timestamp;
        //定义了初始时间戳
		latency = timestamp - start_timestamp	
        //因为真实时间戳会不断更新 差距会越来越大
        
        //你可以重复这个循环至差距到某个值为止，以实现终止
		if(latency<2000){
            //1单位的时间戳=1ms
			window.requestAnimationFrame(increase);	
            //未达到条件时 重复带着当前时间戳执行increase函数
        }
        //如果你想控制动画的速率 因为你无法控制时间戳流速
        //那你就只能拉长/缩短总动画时间 
        //同时在变量上的变动上也做相对应的拉长/缩短来控制动画速率
		/*exec code write here*/
        
	}
```



疑问

既然是根据屏幕刷新率来进行刷新

那怎么避免不同刷新率下动画速率不同的问题？ 还是说函数自动规避这问题

> 75/1000 = 13.3ms
>
> 60/1000 = 16.6ms

我现在还真不知道(



### 9、 import引入资源

#### JavaScript模块

你当然可以直接在html里面直接写进一堆script标签来将你要的script全部引入

就算是要动态引入 你也可以通过jQuery

```
$("Father_node").append(<script src="blablabla")
或者自己手写内容在textarea上面 然后click提交等等
```

不过这样引入 未免太不语义化了(

这方法都是基于原生createElement"script" 然后setAttribute("src",url)的思想



不过又在**ES6**规范上

终于有了类似其他语言一样 可以直接以**模块**的形式import引入外部文件的操作

而**模块**是由要引入的js文件书写export自己说明的

`import`与`export`是相互配合的

不过 什么是模块?

> 模块(Module)或者说模组( 本意就是基于原版然后附加的外部小功能
>
> 原意也很简单 如果你要套一个模板且每个页面都要实现有丢丢不同的功能
>
> 那你是不可能将一个模板内塞入全部的功能的 这样会造成其他页面的资源浪费
>
> 
>
> 这个道理就和#include stdio.h/import Math from Math一样
>
> 且JavaScript的module可以控制外部的js哪个部分/函数 可以被调用 哪个无法调用
>
> 且ES6发展的时候 也有其他类webpack打包工具 大概原生ES6就是更好兼容他们？



注:

> 1. 无论是否声明了 `strict mode`，导入的模块都运行在严格模式下
> 2. 引入时 必须处在http等连接模式下 **file浏览**是不允许引入的 这将导致 [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) 错误
> 3. 引入时 必须script的类型是module 为什么是module 还看下文对MINE类型的解释
> 4. module类型**不能**与正常的text/javascript混用 这样做会使所有其他命令失效 建议独立script标签引入module
> 5. require chrome61+

 

外部js的基础module构造并**导出**

```javascript
var import_alert = function(){
    console.log("import it")
}

var int_cal = function(a,b){
	return ParseInt(a+b);
}
export{import_alert}	//将定义好的函数导出去

//其实这样一个基础的module就完成了
```

****



默认导出 仅导出一个变量 使得导入方可以用任意变量接收

```javascript
var acc = function(){

}

export default acc
<<
import acc2 from "/js"
```



****

模块聚合 允许你将不同的小组件结合起来 再一起导入进js里

```javascript
partA.js
const A = ...?
export {A}

partB.js
const B = ...?
export {B}

partA+B.js
export {A} from "partA.js"
export {B} from "partB.js"

<<导入

import {A,B} from "partA+B.js"
//其实功夫也没省多少 还是语义化的作用更高点 毕竟你可以在引入/导出的过程中可以改名 这样能更结构化罢
```



****

静态导入import

一是仅调用外部js的某个已导出函数

```javascript
import {import_alert} from '../js/test.js'
//但无法调用Int_cal
import {import_alert,int_cal} from '../js/test.js'
//可以调用这两个

//你也可以将模块以什么样的名字导入
import {xxApbkie as alert} from '../js/test.js'
alert = xxApbike
```

二是直接引入整个js

```javascript
import * as ??? from "../js/jsonchange"
//可以调用
```



但是还是有个问题 你作为module导入的js 你是没有办法在本module script以外的地方调用的

这确实有好处 防止用户直接在控制台里乱调用函数 也防止一些入侵攻击

但坏处也很明显 你想快捷调试的话就得又得把代码重新启用在正常的script里 一来二去还挺麻烦的



#### **JSON**



为什么我不能直接import js一样导入json?

```JavaScript
>>import pink from "./json/pink.json"
<<MIME type of "application/json". Strict MIME type checking is enforced for module scripts

//module类型的script无法检测到json应用类型
```



这就要提到MINE类型模块资源 因为`json/JavaScript`在**模块化**的时候 同属于`MINE`资源 



即无法保证json文件引入之后是否真的像json一样运作

而不会被恶意植入JavaScript有预先恶意执行脚本的风险
(最经典的莫过于劫持后 给你正常浏览的网页添加挖矿负载之类的东西)
除非引入的时候 承认该文件就是`json`(只能于`json`的方式运作解析`json`文件



否则第三方脚本实际上可以在这种情况下执行，因为第三方服务器可能会意外的返回`JavaScript／MIME`类型和恶意JavaScript负载，在导入的作用于中执行代码



原生方法

> Chrome 91+
> import pink from "./json/pink.json" assert {type:"json"}
> 这样做之后 确实能够把json打包成模块等待模块工具调用了 但是缺点也很明显 对客户端的版本号要求较高

Jesus 还是需要import assert 否则就老老实实用httprequest



这部分 建议去看看webpack篇





### 10、异步操作

原生的JavaScript是一个单线程语言 

在现在而言 单线程语言过于的低效了

因此JavaScript又引入了异步操作概念来实现类似多线程处理任务的效果





### X、 Jquery库

#### 介绍与作用

实际上 JS与Jquery并不是两个完全独立的东西

> 介绍如下
>
> jQuery是一个快速的，简洁的javaScript库
>
> jQuery是JS的框架，基于JS语言，集合Ajax技术开发出来的JS库，封装JS和Ajax的功能，提供函数接口，大大简化了Ajax，JS的操作。具有跨浏览器适配 CSS友好 轻量等特性..
>
> 
>
> 总而言之 封装(write less,do more) 就是它的特点
>
> 
>
> 一般JS调用Jquery链接:
>
> [Jquery引用]: https://code.jquery.com/jquery-3.6.0.js	" 它支持V4/V6访问(留意官网版本更新)"
>
> 要加速访问 自行选适合自己的CDN吧
>



它是怎么实现所谓的节省空间？

具体表现为:

```html
Before:
<div id="openNotepad" onclick="openNotepad()">打开</div>
<div id="openNotepad" onclick="closeNotepad()">关闭</div>

然后js里面自行配置
function openNotepad(){
var Notepad = document.getElementById("Notepad")
Notepad.style.right = "0"
.
.
.
}
function closeNotepad(){
and so do I!
}

After:
<div id="openNotepad">打开</div>
<div id="openNotepad">关闭</div>

<script>
    <script src="Jquery链接"></script>
$(function(){
	$("#openNotepad").click(function(){
		$("#Notepad").css("right","0")
	you know the rule
	})
})

	$("#closeNotepad").click(function(){
		and so do I!
	})
})
</script>
直观点来讲 我的代码从32行删减到18行 且编写内容大大减少.
```

****

值得一提的是 jQuery从没有说明自己可以相比起原生JS来说 加速代码的运作效率这样etc

毕竟本质就是对JS的代码封装然后丢给你API调用

但是ST上有个人说的好

> Computers cost much less than programmers.
>
> Let's say:
>
> Using pure js will make code run for 1ms, and programmer work 3 hours.
>
> Using jQuery will make code run for 2ms and programmer work 1 minute
>
> See *profit*?



#### `$`转义 [^$的用法]

****

**实际上是也有许多不引入库本身 但是也有一些便利的操作可以让我们简写代码**

**注:反单引号`` `包裹希望生效的区域**

`$` 它在非jquery搭配时拥有着这几个转义



`${}` 代表着字符串转义

即 包裹的内容回被译作`""` 且调用它时会直接免掉字符串与变量链接时需要调用`+`来链接

```javascript
string.push(`${array}:${style[array]}`);  
string.push(array+':'+style[array]);

即使引入jquery后 这个原生的功能也不会受影响
```



不过有一个特点就是如果你直接将`${}`指向一个对象集的话`status = ({num:01},{num:02},)` 他会直接返回[Object object]而非对象本身

这也说明你只能调用一个对象集的某个属性 `${status.num}` 而非`${status}`本身 



实现一个整体是字符串 生效字符 

****

`$()` 代表着CSS转义

默认下不加`#`/`''`便默认规定为选择ID

> ```javascript
> 要注意的是 $("#id") != document.getElementById("id");
> 
> 毕竟[0]才会相等,原本的是jquery初始化的 调用功能?
> 
> $("#nav-link-item")[0].innerText = "huh?"
> ```
>
> 以及
>
> ```javascript
> $("a").css()=a{
> 
> }
> 即它选择了所有的<a>这个标签
> 
> 但是它又和document.getElementsByTagName("a")不相同	//false
> 硬要说的话 一个是DOM原生节点 另一个是jQuery的吧?
> document.getElementsByTagName("a")[0] == $("a")[0] //true
> ```

那么 它要怎么表达CSS里的**ul li{}** 与 **ul li.nav-link-item{}** 与 **ul#menu li a{}**的效果呢？



这是jquery引入前

****

<div style="color: #119151; font-size: 23px;">你一个个来(恼)</div>

**标签**

`>` = 下层关系 且只在上位的 <u>下一位</u> 里寻找**标签**

`space` = 下属关系 在上一位的 <u>所有下位</u> 里面寻找**标签**

**属性名**

class类 直接.class就可以表示

ID类 直接#ID作表示

这点还是和CSS的表示方式**一样**



所以

**ul li{}** = `$("ul>li/ul li")` = document.getElementById("ul li");

**ul li.nav-link-item{}** = `$("ul>li.nav-link-item")`

**ul#menu li a{}** = `$("ul#menu>li>a")`

但是你不能直接用 `$("ul#menu>li>a")`.style或者var ** = $("\*") 这样直接调整CSS，需要用它的方式设置CSS



etc...

这些特点 你不引入jquery也能够实现



这是jquery引入后

****

引入之后 使用方式大大修改 具体用法是

> $("*") |([0]) .css("attr","val")	如果是标签名\<a>类[0]就成了可选 此时指代所有的\<a>标签
>
> 或
>
> ```js
> $("*").attr({'id': 'id1', 'index':1, 'value':10,'check':'checked'});
> ```
>
> goto EXP1
>
> $("a").css("text-decoration","underline")	TAG类
>
> ::EXP1
>
> 
>
> goto EXP2
>
> $('#framework').css("z-index","3") 是的 对具体的ID用jquery自带的css属性后 你已经不需要特定指定[*]了
>
> ::EXP2



不过jquery在这点上，好像不如直接js的setAttribute("style",配置引入function)的操作方便



还有一种用法`$`在引入jQuery后 本来就代表着一个选择器

> 即 $ =  $(document).ready() 的简写
>
> $.($("*").on.("click","function(){}"))



#### 选择器

那么引入了jQuery后

jQuery里普遍有这么一种定义

> $(selctor)[*].action



一般用法:

> $('#framework')
>
> <<  *jQuery.fn.init [div#framework, prevObject: jQuery.fn.init(1)]*
>
> ​	  0: div#framework
>
> 是的 这意味着你应该如此调用**$(#framework)[0]**才能等同于
>
> 不加jQuery **$(#freamwork)**的效果



即存在了选择器这个概念

除了上文提到的CSS类用法还有:

[更完整的去这里看](https://jquery.cuishifeng.cn/index.html)

| 选择器                  | 实例                       | 选取                  |
|:---------------------- |:------------------------- |:------------------- |
| [*]                     | $("*")                    | 所有元素               |
| #*id*                   | $("#lastname")            | id="lastname" 的元素   |
| .*class*                | $(".intro")               | 所有class="intro"的元素|
| *element*               | $("p")                    | 所有 <p> 元素(Tag)     |
|||类比还有img之类的标签|
| :first                  | $("p:first")              | 第一个 <p> 元素|
| :last                   | $("p:last")               | 最后一个 <p> 元素|
| :even                   | $("tr:even")              | 所有偶数 <tr> 元素|
| :odd                    | $("tr:odd")               | 所有奇数 <tr> 元素|
| eq(?)            | $("p:eq(X)")/$("p").eq(X) | 选取队列的第X个元素                        |
| :header                 | $(":header")              | 所有标题元素 <h1> - <h6>|
||||
| [:contains(*text*)]     | $(":contains('W3School')")| 包含指定字符串的所有元素 |
||||
| s1,s2,s3                | $("th,td,.intro")         | 所有带有匹配选择的元素|
|[]指定选择框|$("#ul li[name="final"]")|指定选择 li里 含有name=final标签的元素|
| [*attribute*\]          | $("[href]")               | 所有带有 href 属性的元素|
| [attribute*=*value]   | $("[href='#']")   | 所有 href 属性的值等于 "#"的元素 |
| [attribute*!=*value] | $("[href!='#']") | 所有href 属性的值不等于 "#" 的元素 |
| [attribute*$=*value] | $("[href$='.jpg']")| 所有 href 属性的值包含以 ".jpg" 结尾的元素 |
|[attribute*^=*value]|$("[href^='2021']")|所有 href 属性的值包含以 "2021" 开头的元素|
| :input                  | $(":input")                | 所有 <input> 元素  |
| :text                   | $(":text")         | 所有 type="text" 的 <input>元素|
| :... |                |                                            |
| :的都是 <br />附属元素/选项/规则 |                            |                                            |
|                      |                            |                                            |
| .prev | $("#02").prev() | 此节点的上一个 |
| .next | $("#01").next() | 此节点的下一个 |
| .children | $("#01").children() | 此节点的下一级 |
| .father | $("#001").father() | 此节点的上一级 |
| .find | $("#01").next().find("span") | 寻找div id=01标签用span包裹的元素 |
|                         |                              | 在一个标签里面有副属性的 是[x=?]           |
|                                  |                              |                                            |
|                                  |                              |                                            |
|                                  |                              |                                            |
|                                  |                              |                                            |
|  |  |  |



#### 一般css用事件

****

##### click事件

和原生的onclick作用类似



> ST搜寻结果
>
> The `.click()` only work on elements that are in the DOM when the method is called
>
> 翻译一下就是 你必须在DOM加载完成之后 去执行才会生效
>
> 
>
> 为什么click失效而又在console里生效 正是因为你在DOM未干完活前 先执行了它
>
> 建议套在ready()(window.load)内执行





Extra: 为什么更推荐用原生的evenListener(.on)代替单纯的click()事件？

ST里有一处解答

当用click的时候

1. 许多匹配的元素会创建许多相同的处理程序，从而增加内存占用(不是很懂)
2. 动态新增的项目**不会**被click响应 - 如果你的绑定对象为class类 而你想在原本的class上 再新增一个需要click响应的项目。 除非您重新绑定处理程序，否则按钮将不起作用。



而使用.on("click",...)时

1. 指定好单一的处理程序匹配的所有元素，其中包括动态创建的。
2. 既然你是用on来添加 如果你想删除的话 直接off就完事 而click却做不到如此简便的移除事件



那么说到click 必然也少不了hover了

##### Hover事件

版本1.0引入

> hover( handlerIn(eventObject), handlerOut(eventObject) ) 后者缺省时 则只有悬浮时有效



用起来就和平常的css:hover感觉没啥区别

何况这可是js导入的hover 在此之前 我好像还真没做过js导入的伪类选择器



Extra:

因为jquery的hover不是一个事件，而是jQuery封装的一个方法 所以你无法用on将hover给套进去(

虽然你可以这样曲线救国:

> ```javascript
> $("#container").on('mouseenter', '.selector', function() {
>     //do something
> });
> $("#container").on('mouseleave', '.selector', function() {
>     //do something
> });
> 
> 不过你真的需要必须要用on的情况再去吧
> 要不然这方式也怪离谱的
> ```



##### mousemove事件

> .mousemove/up/down/over/enter/leave(action())

你甚至可以强行通过on(enter/leave)来搭建hover事件



##### display快捷开关

> *.show/hide()	--display:block/none
>
> 除此之外还有个更简单的
>
> 开关的默认配置
>
> *.toggle()



#### 操作DOM用事件

同样 相比于原生JS jQuery封装给的接口也简便许多

jQuery里将赋值和得值都并在一个接口里



在所有DOM节点之前 更想说的是页面载入问题

[^DOM注意事项]: here

然后 相比起window.onload()

出了`ready()`来替代  (明显更语义化了)

另外直接一个`$`也是代表整个body.ready的效果



个人建议 如果想写在script标签内的所有代码有效

建议直接用

> $(function(){code here})



****

文本节点

基本的text 在这里直接指代为DOM的文本节点

> *.text()		 //获取值
>
> *.text("?")	//赋值
>
> 比起原生的JS里 textContent获取值 想改变值还得另外调度innerHTML要方便的多

不过值得一提的是它不止有text还有html属性 

不过不同的是html处理方式是更符合html环境(所以它不能用来处理xml文档)

text就当成普通的文本处理方式



以及直接获取value对应的val

> *.val()

****

**增减元素的DOM**

remove()/add()

这也相比起原来的appendChild/removeChild要简化

`add()`还和jQuery体系的`$()`关联 这也意味着能直接简化写入一个节点传进去

用法同样也是

```javascript
$("father").append("$(<div id="?">?</div>)")
```

****

**事件监听器**

比起add/closeEventListenr 当然是on/off更方便 用法也是一模一样



#### 与BOM互动的事件

最常用也最简单的 那肯定就是窗口缩放/拉伸

已经..不想再品鉴把窗口拉小的时候 元素挤成一团溢出窗口外的情景了(

出了写@media(max-width:??)之外  (如果你用js in css这种控制方式开销想必更大.)

jQuery毕竟还能控制js



我们浏览网页 最简单的调整BOM的操作 



无非就是放大/缩小(resize) 滚轮(scroll)..等操作



##### resize

> $(window).resize(function(){})



> `resize` 事件处理中的代码，不应该依赖于事件被调用的次数。由于不同浏览器对该事件实现的方式不同，该事件被调用的时机也不同。例如，对于 Internet Explorer 或 基于 WebKit 的浏览器（例如，Safari 和 Chrome）而言，resize 事件在窗口改变的过程中，会被连续调用。在某些浏览器，如 Opera，该事件只在调整窗口大小操作结束时被调用。



****

### Y、Vue.js

介绍

一套用于构建用户界面的**渐进式框架** 帮你从js底层与表层html的各种标签直接建立一层关系

从而**方便**你快捷将底层的js呈现在表层的html上

*渐进式*:简单来说就是要用什么给你什么 跟你调用单个函数这种感觉



为什么不接着用jQuery更新DOM？

> 我们要做的无非就是更新类似计时器 然后DOM更新
>
> 然而以后的数据在变化之后 往往难以继续快捷的追踪
>
> 而这些的成因都是 因为他们<b>没有</b>一个<b>简单</b>的提示板来告诉我当前数值的状态
>
> 而vue直接将一个标签绑定在一段APP上 则APP的数据便能在这个标签很快捷的查看/修改
>
> 以往的DOM想实现这点只能手动适配
>
>  
>
> 而且 在追求原生占用和快速构建上 后者往往收益更高 和jQuery一样的原则 write less do more.
>
> 更合理的选择是原生ES jQuery Vue 混用 哪个在当前条件下适合就用哪个



#### 创建/挂载

Vue的处理方式是将一个需要作用的片段命名为App,然后将需要作用的地方称作挂载(Mount)

```javascript
const app = Vue.createApp({
				data(){
					return {counter:0}	//已将counter绑定到app的$data上 
				}
				
			}).mount("#counter")		//与#id=counter的元素挂载

html部分

<div id="#counter">{{ counter }}</div>

已可以通过app.counter来访问 counter标签里的counter数据
>>app.counter
<<0
```

上述也被称为文本挂载 根据`{{}}`标签与挂载定位让vue来处理



**注**:这样绑定的方式不允许第二个重名的标签，为什么？大概是给下面的指令让路

利用`v-for`即可重命名标签 但需调用子属性

****



#### 指令

除了单纯的对标记执行关联

Vue内置作用于标签的多种指令以便Vue调用函数来实现各种功能



监听事件	但是不知道为什么目前的例子click都只能对按钮标签使用(

`v-on`

缩写: `@prop`

```html
<button v-on:click="reset">清零</button>	//挂载后从methods库里寻找reset函数执行

const reset = {
  data() {
    return {
    				     //注意 标注的字符 不能与method的函数名字一致! 否则会报堆栈溢出错误
        				 //所以还是第一次显示文字时不如直接在标签上重命名 
    }
  },

  methods: {
    reset() {
      display.counter = 0
    }
  }
}

Vue.createApp(reset).mount('ul li')
```

****

同原生一样 一般我们的行为都可以被监听到

不过在vue里则是以一种修饰符来细分监听的区域

用户在浏览器正常的输入 大多数的媒介也是键盘/鼠标

所以vue里也细分为 `click`,`keyup`领域





**事件处理**

一般来讲 v-on代表`addEventListener`事件 但原生的ES代码是有对其植入传入参数的

其实这里也有 且vue针对v-on还有和jQuery一样的省略符号`@`

@click = 这个事件将要执行什么 可以是直接执行@click="count++" = v-on:click("count++")



且也能代表标签对应的动作

例如 `<input>`里面的`submit`动作 只需要

```html
<form action="post">
<input @keyup.enter.prevent="submit"></input>	//即可代表在激活输入框时输入enter完成提交动作
</form>
```



**事件修饰符**

1. Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节
2. Vue.js 通过由点 `.` 表示的指令后缀来调用修饰符。(@click.*)
3. 修饰符允许单独调用不必加 `v-on`等指令 (@submit.prevent)
4. 修饰符允许串联调用



**click**的则有

> - `.once` - 只触发一次	//事件通用
> - `.left` - 左键事件
> - `.right` - 右键事件
> - `.middle` - 中键事件 (滚轮)..



**keyup**的则将部分常用的key绑定在vue的修饰符上供调用

> 常用的除F(X)的功能键
>
> 而除此以外的则遵循ASCII码转义(48→0 65→A 97→a)
>
> 例:<**input** @keyup.alt.67="clear">	*<!-- Alt + C -->*
>
> 也可以将鼠标键盘的事件组合起来
>
> *<!-- Ctrl + Click -->*
> <**div** @click.ctrl="doSomething">Do something</**div**>



通用

> **exact 修饰符**	精确的系统修饰符组合触发的事件
>
> *<!-- 有且只有 Ctrl与鼠标 被按下的时候才触发 -->*
> <**button** @click.ctrl.exact="onCtrlClick">A</**button**>
>
>  
>
> **触发**
>
> 如submit事件
>
> - `.stop` - 阻止冒泡
>   - `.prevent` - 阻止默认事件	例如submit提交时默认会重载页面
>   - 而直接<submit @.prevent>这样就可以防重载直接提交数据
> - `.capture` - 捕获事件?



从这个部分开始大概是原生ES6 `addEventListener`不包含的事件了( 

我觉得这点上我才能感受得出响应式框架的特点罢



****

**通用传参**

不过即使是原生ES6也包含传入参数 要不然监听是为了干什么(

```javascript
或传入methods里function中的参数 缺省时等于空参传入

仅传入写入参数 
v-on:click="fun(123)" = <button @click="fun(123)">烦内</button>
传入自定义参数(args)/写入参数

<button @click="reset($event,123)">烦内</button>
//兄啊 click事件要怎么传除了鼠标输入的值啊(
//input里的键盘也是这样 怎么传入除键盘动作以外的值啊(恼)
```

****



`v-model`

双向数据绑定

目前的绑定都是底层→表层

而双向就能实现表单输入和应用状态之间的双向绑定 但是我目前还真找不到这玩意从表层直接作用于底层的效果 它是从表层到底层再到表层 既然如此 

如果我仅仅只要我输入的东西 我直接input.value不也是一样的？ 

~~也许就为了看浏览器的文字渲染？~~

知识 未来可期



2.21

`v-model`更多用于表单上(`v-model` 会根据控件类型自动选取正确的方法来更新元素)

因为它会关联表单中的 toggle、checked、value、selected、picked等事件  

```html
那么既然是表格单 那肯定也有输入
无论是单选还是复选
<div id="post">
<form action="post">
  <input type="radio" v-model="picked" id="number" value="1234">1234</input>
  <input type="radio" v-model="picked" id="number2" value="5678">5678</input>
  <div id="status">{{ picked }}</div>
</div>

<input @keyup.enter="submit" placeholder="input即可以被触发为post"></input>
<input @keyup.enter.prevent="choice3" placeholder="input也可以触发app函数"></input>
</form>
</div>

```



****

`v-if`

绑定到DOM的结构 大概是通过attribute与val(true/false)来控制DOM结构？

****

`v-for`

绑定**数组**的数据来渲染一个项目列表

目前作用是文字标签的增强版 应该说更合理的版本

```javascript
<div id="list-rendering">		<!-- 这个for指令就可以做到整个标签内都是作用域 -->
  <ol>
    <li v-for="todo in todos">	<!-- 经典for循环 从todos列表里寻找 但是调用起来时却又是todo的子属性 -->
      {{ todo.text }}
      {{ todo.text2 }} 			<!-- 也允许在同一个标签内写上两个同父属性的标签 -->
      {{ todo.description}}
    </li>

  </ol>
</div>

const ListRendering = {
  data() {
    return {
      todos: [
        { text: 'JavaScript' },
        { text: 'Vue' },
        { text2: 'awesome' },
        { description:"比单独文字标签不知道高到哪里去了"}
      ]
      
    }
  },

}
Vue.createApp(ListRendering).mount('#list-rendering')
```

****

`v-bind`

缩写 `:prop`

和标签的 **属性名** 或 **属性值** 绑定 属性值绑定类似于原生的`setAttribute()`

```html
<!-- 绑定 attribute -->
<img src="1.jpg"></img>
setAttribute("src","???")
or
<img :src="???"></img>	create--> mounted --> app.src=""
<!-- 动态 attribute 名 -->
<button :[key]="value"></button>	create--> mounted --> app.key="???" << ???="value"

<!-- 但对于class属性有点特殊	因为同一个标签允许同时上多个标签
而vue允许你动态得将某些已绑定的class属性进行修改
其中包括开/关 !-->
<div :class="{red:isRed}"></div> create-->(data:{isRed:true}) mounted --> app.isRed="false"  //Red失效
<!--也支持一次性引入多个class属性 并赋予可开关属性!-->
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]"></div>

```

也和style属性直接绑定

```

```



jQuery貌似不能直接.css("style","attr") 看看vue行不行



#### 组件化

`app.component("",{})`

实际上就是将你的代码转变成模板使其可以重复在任何地方上插入

就是重复利用代码

```javascript
const component_head1 = Vue.createApp({})   //先创建app

component_head1.component('head1', {      //然后将app组件化 (标签组件名,{执行体})
    data() {
    return {
      count: 0
    }
  },
    template: 								//组件和模板对应 如果你没有重复利用的必要 那也没必要去组件化
    `<h1>自定义组件!</h1>
	<button @click="count++">
      点了 {{ count }} 次！
    </button>` 
    
    //模板内容(如果标签需要因为打属性要用到双引号时 要前置加上反引号包裹 不过加了反引号的话就不再需要双引号包裹了)
    
}).mount('#app_widget')              //但是调用组件前必须要前置挂载位创立
 
 

<div id="app_widget">
    <head1></head1> = <h1>自定义组件!</h1>	//生效
</div>

<head1></head1>	//不生效
```



不过vue还能将app的内容能单纯的用变量代替

```javascript
const button_temp = {
	template:
    `<h1>自定义组件!</h1>
	<button @click="count++">
      点了 {{ count }} 次！
    </button>` 
}

const button = Vue.createApp({
	compoenet:{button_temp}	//更语义化
}).mount('#app_widget')

<div id="app_widget">
    <head1></head1> = <h1>自定义组件!</h1>	//生效
</div>

//methods应该也是同理
```



Z、包管理

```
npm root -g	//获取当前npm全局安装包的位置
npm install -g
```



### A、 即时工具库

毕竟不是html 没法直接写好CSS里面然后直接调用 减少冗余 但是真奇怪 能翻译html 却不能用页面总体style？

**分割线**

```markdown
<div id="gap"
    style="
    border:1px solid black;
    height:1px;
    border-left: none;
    border-top: none;
    border-right: none;
                    	">
</div>

我真傻 真的 我就应该先了解这些特殊用法.. ****
```

****

正则筛选特殊符号

```javascript
function symbol_fliter(str) {
	var s = null;
	if (str) {
		s = str;
		// !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
		s = s.replace(/([\u0021-\u002F]|[\u003A-\u0040]|[\u005B-\u0060]|[\u007B-\u007E])+/g, " ");
		// ！＂＃＄％＆＇（）＊＋，－．／：；＜＝＞？＠［＼］＾＿｀｛｜｝～
		s = s.replace(/([\uFF01-\uFF20]|[\uFF3B-\uFF40]|[\uFF5B-\uFF5E])+/g, " ");
		// ·×‐‑‒–—―‖‗‘’‚‛“”„‟…‧‰、。〇〈〉《》「」『』【】〔〕〖〗〜・
		s = s.replace(/(\u00B7|\u00D7|[\u2010-\u201F]|[\u2026-\u2027]|\u2030|[\u3001-\u3002]|[\u3007-\u3011]|[\u3014-\u3017]|\u301C|\u30FB)+/g, " ");
		s = s.replace(/\s+/g, " ");
	} else {
		s = "";
	}
	return s;
}
```



实时刷新插件 Livereload

```
不仅有实时刷新能力 还可以直接建立http端口 模拟真实的访问
```



### B、 TODO

loop tasks 7.31

- [x] T1 了解null&undefined

- [x] ~~T2 了解新建new的原理~~(8.14)

- [x] T3 课程3节

  8.7 complete
  
  正在完善对象条目信息
  
  function条目架构搭建完毕
  
  ES规范了解

8.8 loop task

- [x] T3 课程3节/3个有用点

- [x] constructor.prototype.constructor.prototype.........

  bonus task

- [ ] *T 父子关系

- [x] *T Stack overflow什么的，有在访问吗？

- [x] T4 eval? 这是什么东西 22.5.9

> `eval()` 的参数是一个字符串。如果字符串表示的是表达式，`eval()` 会对表达式进行求值。如果参数表示一个或多个 JavaScript 语句，那么`eval()` 就会执行这些语句。
>
> 这意味着什么？
>
> var a = 3; var b = 4;
>
> eval(3+4) 		 <<7 这没什么大不了的对吧
>
> 然而
>
> eval(3+4+'3')	<<73 忽然感叹我之前瞎折腾toString()诸如此类的东西 人家老早就有了**极其快捷**的东西了
>
> 一般来说会 a+b+'3' << '73'
>
> parseInt(?) << 73

8.19-8.23(截止)

- [x] 正则表达式
- [x] T3 课程3节/3个有用点
- [x] json!
- [x] ~~flex布局?~~ inline-block布局!
- [x] git!
- [x] stack overflow什么的 会用吗

 狂妄 懒惰

9.10

- [x] jquery选择器应用



2.27

- [ ] 如何import json并正确调用？
- [ ] 如何理解async的意义
