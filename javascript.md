## notepad for JavaScript

<svg t="1626158047738" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1648" width="18" height="18"><path d="M0 0h1024v1024H0z" fill="#FFFFFF" p-id="1649"></path><path d="M944 896H80.213333a31.189333 31.189333 0 0 1-27.306666-16.213333l-5.845334-9.813334a33.493333 33.493333 0 0 1 0-32.426666l431.36-736.426667a32.597333 32.597333 0 0 1 27.733334-15.786667h12.8a32.554667 32.554667 0 0 1 27.733333 15.786667l430.506667 736.426667a33.28 33.28 0 0 1 0 32.426666l-5.930667 9.813334a31.232 31.232 0 0 1-27.264 16.213333z m-453.205333-256a21.333333 21.333333 0 0 0-21.333334 21.333333v42.666667a21.333333 21.333333 0 0 0 21.333334 21.333333h42.666666a21.333333 21.333333 0 0 0 21.333334-21.333333v-42.666667a21.333333 21.333333 0 0 0-21.333334-21.333333z m-7.722667-256a21.333333 21.333333 0 0 0-21.333333 23.893333l17.066666 137.386667a10.666667 10.666667 0 0 0 10.581334 9.386667h45.354666a10.709333 10.709333 0 0 0 10.666667-9.386667l17.066667-137.386667a21.333333 21.333333 0 0 0-21.333334-23.893333h-58.069333z" p-id="1650"></path></svg> warning

> 1. 在JS修改CSS属性的时候，必须要去掉原本横线，改驼峰命名
>
>    否则就得使用.style['css属性名']='属性';这样修改 比驼峰麻烦
>
> 2. 本md以**`*`**代表着假定的变量名/数据类型
>
> 3. 这玩意既然能翻译html内容 却不能像真正html一样直接设一个<style>就完事 真麻烦
>
> 4. 而且HTML标签之后的MD语法通通失效(至少在预览上) 你是真的离谱
>
> 5. 总结 专事专办 祝你好用((
>
> 6. 当我写这个的时候 我开始注意到浏览器的适配情况 
>
>    旧浏览器的代表IE11 ES6 几乎只支持let与const 所以当你用到ES6的东西时
>
>    你就该祈祷不要碰上谁还在用IE打开你网页
>    
> 7. 它虽然不支持unicode直接写入 但还是支持HTML的 通过此Hyberlink查询\![unicodewiki](https://unicode-table.com/cn/blocks/control-pictures/)
>    
>    
>    

### 0、foundation

通用知识

#### 0.1、符号

`\`转义符号

无论在H/C/J里面都有广泛的通用规则 可转义ASCII码 也可反向屏蔽以来实现正确的内容

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

> `+`在reg之间有着连接作y用
>
> 而且正则遵循先来后到的形式

```javascript
/\.\d+/g 这个代表着小数点后至少一位
/\d+\./g 这则代表着至少一位数值带小数点(12. 234. 012. 0.)
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
如果不带.length的话 会直接返回一个数组对象 对象里面记录着位置以及length
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
| n*     | 匹配任何包含零个或多个 n 的字符串.          | (!=1)    |
| n?     | 匹配任何包含零个或一个 n 的字符串.          | (0,1)    |
| n{X}   | 匹配包含 X 个 n 的序列的字符串.             | (x)      |
| n{X,Y} | 匹配包含 X 至 Y 个 n 的序列的字符串.        | (x,y)    |
| n{X,}  | 匹配包含至少 X 个 n 的序列的字符串.         | (x,)     |
| ^n     | *匹配任何开头为 n 的字符串。                | n*       |
| n$     | *匹配任何结尾为 n 的字符串。(n前n后)        | *n       |
| ?=n    | 匹配n之前的字符串                           | ()n      |
| ?!n    | 匹配任何其后没有紧接指定字符串 n 的字符串。 | ()!n     |

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
3. 接下来 运用至少出现了?次的reg 根据逻辑互补 更建议用`*` (!=1)
4. 因为^[0-9]本身就代表着=1 再与 !=1 结合 即完整 
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

疑惑:这样改起css属性会比一个个getID然后"ID".style方便的多吧,那是不是可以直接这样做?

<div id="sign" style="font-size:24px; color:red">不行！</div>

 让我们看看它的后果

[^False way:modify CSS string]:  

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
    **Extra**

    你终究会遇到多个js文件挤在一起全局变量到处飞的时候(希望你做个人)

    当然当你遇到这种的时候其实已经没救了 建议重写(

    这里要做的是如何避免到那个情况

    **唯一全局变量**

    ```
    var x = {};	//定义全局变量
    x.asdasda;
    x.gretgasd;
    没错,定义了全局变量之后，你就能好像在调用属性一样调用你写的js,早日养成习惯，不要随便占用Window
    ```

    

 2. 局部变量

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
        console.log(x*y)
    	}
    	c2()
        //更别提这种离谱的变量重名时的反应(会直接让变量从内部开始向外寻找变量(要符合内向外的原则))
        //所以C2的x变量为空 即结果为NaN
        //所以你只要去掉c2函数里的'x'就能跑出结果了，因为不再重名变量，自然不需要从内部寻找变量
        //顺带 如果你直接调用c2的话，也会显示c2未定义.毕竟你不能绕过外部去访问内部的函数
    }
    ```



**Extra**

var还有一个奇怪的性质，如果你把声明变量赋值写在末尾，然后把该变量要参与的计算写在前面,它不会报错,而是返回undefined.即它已经被**定义**过了，但与其定义的值并没有被**赋值**上去.

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

 **const(常量)**

官方定义为**只读**变量,即不可被**修改**



//ES5 定义常量就是全部大写字母命名的变量就是常量(???

像极了C(#define PI 3.14



*ES6 关键字表示常量

`const`

```
const PI = '3.14';
PI = '3.1415'; //type error
console.log(PI)
//3.14
```





   但是它们有什么区别？

   首先不必多说全局最大

   但是局部的var的范围又是多大？

   **A:**

   > 用`var`定义就是作用域内变量，不用`var`就是全局变量。
   >
   > `var`的变量表示的是作用域可用
   >
   > 
   >
   > 什么是作用域？
   >
   > **变量（变量作用于又称上下文）和函数生效（能被访问）的区域**
   >
   > 
   >
   > 实际上还有一个区别，用var定义的不能用delete删除，不用var的可以用delete删除，也就是说，实际上不用var定义的变量变成了某个对象(全局window或者自定义的全局)的属性。
   >
   > 
   >
   > `let`命令范围只有在所在的代码块内有效
   >
   > 什么意思 即为function()

   

   

   

#### 1.2、访问对象(属性)



除了最基础的`.`来访问

```javascript
objectName.property  //me.age
```





#### Extra

而在此又引入了一个严格模式`use strict`,强制规定要以var/let局部变量书写否则不生效.且严格模式声明必须写在第一行.
    
```javascript
'use strict'
var i = 1;
```





### 2、 数据类型

老生常谈

> <div style="color:red;">string</div>
>
> <div style="color:red">object</div>
>
> boolean 	true/false
>
> number 	0-9
>
> <div style="color:red;">array(Map/set)</div>
>
> <div style="color:blue;">Null/undefined</div>
>
> function



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

****


#### String(字符串)

含义:包括非数字非布尔值的有效存在值即为**字符串**

被定义在变量的字符串有一个特性就是不可被赋值

​																															——“引号其实是可以’嵌套‘的”

字符串存在意义为了给我们用来编辑

##### 字符串编辑

我们固然不能直接将变量直接编辑，但它可以先通过一个转变字符串编辑的过程再进行更多操作.

具体详见

[^function-toString]:  jump!



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

   想的很好，但并不能这么写![image-20210719221827396](C:\Users\kechuan\AppData\Roaming\Typora\typora-user-images\image-20210719221827396.png)

回顾JS的对象方式 你怎么能把一个ID的style给以这种数据组覆写呢？  ~~为什么我不能~~



**The correct WAY**



> **通过 setAttribute 方法 设置元素的style属性** 	[来源于CSDN](https://cloud.tencent.com/developer/article/1435270)
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

总之我认为json比起传输这些 对于编写它们的人来说更有意义,更直观..



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

`JSON.parse(*)`

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



#### ***面向对象**

什么是面向对象？

> Javascript是一种基于对象（object-based）的语言，你遇到的所有东西几乎都是对象。但是，它又不是一种真正的面向对象编程（OOP）语言，因为它的语法中没有`class`（类）。
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

//结果是

var cat1 = {cat1.name="cat", cat1.color=color()}
var cat2 = {cat2.name="cat", cat2.color=color()}
//其实也没省多少功夫是吧
```

****

然后你在想 难道就不能在var变量的时候就直接生成好所有对应的属性的值吗？(像内置的Date()一样)

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

还记得this么 它在function里使用会指向在实参上 

以及因为this使用的方式 需要new来搭配完成this的对接

运用这种方式 就能利用this与new去指向你要的库



这就可以直接:

Patch E1.2

```javascript
function Cat(name,color){
    this.nationality="chinese";
	this.name=name;
	this.color=color;
}
var cat1 = new Cat("me","you")
以及你可以额外添加这只猫的“固定属性”
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



E2:

##### 继承对象

 `prototype`(原型)/`__proto__`(原型对象)

prototype即为某个函数的原型,是个函数都会有这个属性

> 构造函数有一个prototype属性，指向实例对象的原型对象。通过**同一个**构造函数**实例**化的多个对象具有相同的原型对象。经常使用**原型对象**来实现继承

***实例：你new的新对象便是实例对象***



什么意思？

你构造出来的函数必有原型属性(`prototype`)指向你new出来的原型(`__proto__`)



那么`__proto__`又是什么玩意？

这是每个对象(除null外)都会有的属性，叫做`__proto__`，这个属性会指向该对象的原型。



usage1:

```javascript
Cat.prototype.fur = ?;
```

而这个过程到底做了什么?

Cat函数的原型属性多了一个自己新定义的属性重新赋值

你可以理解为 cat的子属性



E2.1:

```javascript
function Cat(name,color){
    this.nationality="chinese";
	this.name=name;
	this.color=color;
	
}
Cat.prototype.fur = "white"	//Cat的原形属性fur是指向于你new出来的cat1
Cat.prototype.voice = "loud";
var cat1 = new Cat("sli","orange")
//应答:Cat {nationality: "chinese", name: "sli", color: "orange"}(fur不在这里出现)
cat1.__proto__	//应答fur:"white"
var cat2 = new Cat("sily","black")
Cat.prototype.fur = "sort"
Cat.prototype.voice = "short"
cat2.__proto__
//{fur: "sort", voice: "short", constructor: ƒ}

//注：这样写会让cat1的__proto__属性多出fur:white，而非直接显示在cat1上
```

<img src="C:\Users\kechuan\AppData\Roaming\Typora\typora-user-images\image-20210814181021686.png">&nbsp;





那么关系明了:

函数的prototype指向了调用这函数(new)的所有对象

所有上文new的函数的`__proto__`属性全部指向了该函数

一旦函数的prototype一修改，下文的new对象的`__proto__`属性全部都会被修改

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708151322530-1608157973.png)

Extra:

> 如果你追加new对象的属性是proto的重复名字属性(下文简称const `__proto__` proto)
>
> 则调用该重名属性的时候会优先于你proto属性的属性
>
> 而你想调用proto属性里面的话
>
> 就需要cat1.__proto__.fur



这种方式只适合对种类的修改,并不适合具体描述单独的个体,说白了就是记录物种的特征会有用



//**ES6**之后 引入了一个class属性

`class`是什么?

> 在ES6中，class (类)作为对象的模板被引入，可以通过 class 关键字定义类。
>
> class 的本质是 function。

而`class`的继承对象`constructor`（构造对象）则充当了原本的整个function作用

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
	
}
var cat1 = new Cat("me","black");
//or 写在class外面
Cat.prototype.fur = "white";
//应答:Cat {fur: "white", nationality: "chinese", name: "me", color: "black"}
//而且它还不会让你追加的属性跑去__proto__里 很奇怪..而是直接跑进constuctor里

```

我在浏览器里面发现一个可以不断嵌套的属性.prototype.constructor.prototype..

跟function里的`prototype`与`prototype`对象里的`__proto__`属性这样共同指向同一目标不同



它是function里的`prototype`与`prototype`对象里的`constructor`属性相互指向无限嵌套下去的

![img](https://img2018.cnblogs.com/blog/850375/201907/850375-20190708152327825-11086376.png)

更加语义化 不是吗 毕竟是直接写明了class上去

Extra

> class还引入了一个新静态属性 static 其实作用就是class作用域下的const

那么 作用呢？

毕竟class是一个更大的function

所以适合作一些运算库处理 比如你class个calculate{里面赛一堆sum sub **... static PI = Math.PI}之类的就挺语义化的



#### Array(数组/阵列)

Array可以包含任意的数据类型,同时也可变.

以`[]`来区分单纯的值

```javascript
var array = [1,2,3,4,5,6];
```



最简单的访问方式就是直接array['元素下标'] [^object_access]



以及**历遍访问**(迭代)

`for(let x in *)`

这允许你去从头顺序访问数组(一般从元素下标0开始)

```javascript
function Jsonchange(style){
        var string = [];
          for(let array in style){
              string.push(`${array}:"${style[array]}"`);
//注:json不允许使用*for of)
```



为什么在这里需要用更低作用级别的let?

因为在这里变量实际上是作为数组的下标存在，这也是为什么这个变量叫什么其实都不重要.

反正叫什么都无所谓，但也不能与上级的`var`变量冲突 所以需要使用`let`.

 

而如果采用`for(let x of *)`

则会直接访问元素的**值**本身

对于纯数组 你只能用of来访问 否则你只能得到一堆index



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
> 在调用for in历遍后它会在最终把name这个属性名也给执行一遍(如果是单纯console.log打印会把name也输出在结果上)





##### Map 和 Set(保留)

**现在的我并不清楚它们的实际意义**









#### 数据方法调用



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





##### **特殊(数组)**

****

> 
> 



###### **组型变化**

**分隔** `*.slice()` 不过其实只要一个数值就可以了	

`slice(?start,?end)`

```javascript
var ages = [32, 33, 16, 40];
ages.slice(0,4) or ages.slice(0)
//[32, 33, 16, 40]
//注:slice的?start是位置,?end是多少"个数"终止(包括起始位置本身的个数)
```

与上文的 `*.substring()`差不多，不过是针对于数组用的

~~其实我更建议统一都用slice(~~





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

多参数的处理

情景:如果你想挑出想要的参数，怎么筛选？

如果说多个参数里面 我嗯要挑倒数第二个

> ES5及以下做法 
>
> ```javascript
> var rank = function(x){
>     if (arguments.length>2){
> 		let i = arguments[arguments.length-2];//因为是数组,它是以0开始
>         console.log(i);
>     }
> }
> 
> ```
>
> 
>
> ES6新功能`...rest`
>
> [^三个点的含义]: ?
>
> ```javascript
> var rank = function(x,...rest){
>     //因为rest的介入，直接自带判断一种if是否有2个以上参数,if也就没有出现的必要
> 		let i = arguments[arguments.length-2];//因为是数组,它是以0开始
>         console.log(i);
>     /*同理，前面出现多少个就自带判断是否有X个以上的参数，且多余的参数会被归为一个数组里面
>     方便你进行后续的细分操作
>     */
>     	console.log(rest)
>     //[2,3,4]
> }
> 
> ```
>
> 





#### **错误/条件判断 异常应答**

在C的经验里处理过这些案例，本质上以debug的方式将试错方案写进去

然后以在程序中的方案去应对错误从而规避程序崩溃



如果你仅仅只是因为输入了一个错误的值就导致蓝屏或者程序FC

确实是个很蠢的应答错误(你崩坏3都会先弹出错误预警提醒你要不要关游戏或者继续游戏)



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

> 不过说实话，有直接**F12**看审查元素的效率高吗(存疑





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
> 在函数中，this 指的是全局对象.   															  //return `this.*`
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
	this.a = 1;
	this.b = 2;
    var c = 3;
    d = 4;
		console.log(this)//user{a:1,b:2}
	return {x:12};	//如果书写的是return 非对象 就会无视此return this自动绑定到对象
    return this;	//user{a:1,b:2}
    //而return this作用 更像是强调必须返回this到new的新变量上 所以我认为只是个语义化的东西..
    //因为你写个return 0也会照绑无误
    
}
var a = new user();
console.log(a);
//{x: 12};
```

> 在函数中，函数的拥有者默认绑定 this。
> 因此，在函数中，this 指的是全局对象 [object Window]。
>
> 在你new的过程中，this也会指向`a`这个新对象
>

不 没有冲突

根据顺序 this应该先绑定了对象a 然后再去执行user

结果会是什么?

1. this指向了a
2. a继承了user的属性 
3. user的属性是什么？
4. 是两个this与一个var c 和 Window.d
5. user里的this是什么?
6. 因为new是指向user函数里的全局对象 即user里的含有的`this.*` 
7. 所以结果是返回了user{a:1,b:2} c因为是局部变量不返回 d是全局变量(Window)不返回





#### **Call(调用其他var)**

它可以用来调用**所有者对象**作为参数的方法。

> Call(Object,"argument","argument"....) 
>
> //此处argument意味后续追加的字符串当然也可以空参直接Call(Object)完事



通过call()，能够使用属于另一个对象的方法。

类似this引用，也通常结合this使用

毕竟this在方法里就是意味着var里的所有属性，这也包括了又call调用来的var



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
person.fullName.call(person1);  // 将返回 "Bill Gates"

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



当return返回的是**对象**的时候 **不再返回this对象，而是返回return语句的返回值**

return {a} = "a"

return a =  a.value



**return this的含义**

this是指向当前对象的引用，return this就是把这个引用返回。可以返回对象本身这样子可以进行链形调用



#### ES6额外内容

箭头函数（Arrow Function）`=>`

不需要 function 关键字、return 关键字以及*花括号*。

<div style="color:red">但是</div>
箭头功能没有自己的 **this**。它们不适合定义对象方法。适合定义一些简简单单的东西

使用 const 比使用 var 更安全，因为函数表达式始终是常量值。

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
    
所以建议还是这么用
const flick = (x) =>  ((x/2)+45)
```

如果函数是单个语句，则能省略 `return` 关键字和`{}`



***Extra**

**IIFE()** 类似于提前订好的规则 是一个在定义时就会立即执行的"function"



```javascript
(function abc() {
    var a = 3;
})();

待添加..
```



用途 如果你需要在加载整个网页之前就要调用某个脚本的某功能的话

你就得需要这个规则 来提前部署功能 而不是等网页加载完之后(特别是油猴里的一些userscript) 再去调用 这样可能会引起js的不稳定性.



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

### 6、 操作DOM对象

DOM (Document Object Model) 译为**文档对象模型**，是 HTML 和 XML 文档的编程接口。

HTML DOM 定义了访问和操作 HTML 文档的标准方法。

DOM 以树结构表达 HTML 文档。(这个是jquery一些知识的前置)



什么意思？

事实上你一个tag或一处div id它都是一处DOM节点，没有上面的节点存在，自然也就不会有下面的分支

根据 W3C 的 HTML DOM 标准，HTML 文档中的**所有内容**都是节点：

> - 整个文档是一个文档节点
> - 每个 HTML 元素是元素节点
> - HTML 元素内的文本是文本节点
> - 每个 HTML 属性是属性节点
> - 注释是注释节点

而你要操作DOM节点 那必然要先获得DOM节点



经典*document*	对应CSS选择器

> document.getElementByTagName 对应着p1 p2 h1..
>
> document.getElementById("id") 对应着被命名的ID



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



更新

这里笔记不再赘叙更新，你连一键json都做出来了 还要写这个吗？



删除

首先先说明一点 该节点不能执行删除自己的属性， 只能父和兄弟节点里执行删除该节点

一般都是获取父节点，然后再父节点里删除该节点

> father.removeChild(Node)

```
var me = document.getElementById("p2");
var father = p2.parentElement;
father.removeChild(p2)
```

思考:到底是什么情况会需要特地去删除节点呢？





### X、 Jquery库

实际上 JS与Jquery并不是两个完全独立的东西

> jQuery是一个快速的，简洁的javaScript库
>
> jQuery是JS的框架，基于JS语言，集合Ajax技术开发出来的JS库，封装JS和Ajax的功能，提供函数接口，大大简化了Ajax，JS的操作。
>
>  
>
>  一般JS调用Jquery链接:
>
> [Jquery引用]: https://code.jquery.com/jquery-3.3.1.min.js	" 它支持V4/V6访问"



##### `$`转义 [^$的用法]

<div id="gap"
    style="
    border:1px solid black;
	height:1px;
	border-top:1px;"
    ></div>
**实际上是也有许多不引入库本身 但是也有一些便利操作可以让我们简写代码**



**注:反单引号`` `包裹希望生效的区域**



如`$`符号 在JS里面只是没有意义的符号

但它在非jquery搭配时拥有着这几个转义



`${}` 代表着字符串转义

即 包裹的内容回被译作`""` 且调用它时会直接免掉字符串与变量链接时需要调用`+`来链接

```
var a = 'sdcard'
innerHtml(`${a}`)
//sdcard
```

实现一个整体是字符串 生效字符 



`$()` 代表着CSS转义

> ```javascript
> `$("#id")`=document.getElementById("id");
> //#为特地标注ID
> ```
>
> 以及
>
> ```javascript
> `$("a")`=a{
> 
> }
> 即它选择了所有的<a>这个标签
> ```

那么 它要怎么表达CSS里的**ul li{}** 与 **ul li.nav-link-item{}** 与 **ul#menu li a{}**的效果呢？



<div style="color: #119151; font-size: 23px;">你一个个来(恼)</div>

**标签**

`>` = 下层关系 且只在上位的 <u>下一位</u> 里寻找**标签**

`space` = 下属关系 在上一位的 <u>所有下位</u> 里面寻找**标签**

**属性名**

class类

> 直接.class就可以表示

ID类

> 直接#ID作表示

这点还是和CSS的表示方式**一样**



所以



**ul li{}** = `$("ul>li")` = document.getElementById("ul li");

**ul li.nav-link-item{}** = `$("ul>li.nav-link-item")`

**ul#menu li a{}** = `$("ul#menu>li>a")`

但是你不能直接用 `$("ul#menu>li>a")`.style这样直接调整CSS，需要用它的方式设置CSS



etc...

****





### Y、 即时工具库

毕竟不是html 没法直接写好CSS里面然后直接调用 减少冗余 但是真奇怪 能翻译html 却不能用页面总体style？

**分割线**

```markdown
<div id="gap"
    style="
    border:1px solid black;
	height:1px;
	border-top:1px;">
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



### Z、changed log

**7.5?-7.23** 

我才写了那么点 就比之前写半年的index+css+js(去除废话注释)都要大了... 离谱

**7.31**

+ 数组排版整理

**+** function

**+** String细致

**+** TODO待办事项

8.1-8.18

对象完善(json基本)

BOM基本

This完善

运算符特殊用法

7.31完成

传参基本完善

GitHub开始使用

8.20

正则编写







### Ω、 TODO

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

- [ ] T4 eval? 这是什么东西

8.19-8.23(截止)

- [x] 正则表达式
- [x] T3 课程3节/3个有用点
- [ ] json!
- [x] ~~flex布局?~~ inline-block布局!
- [x] git!
- [x] stack overflow什么的 会用吗

 狂妄 懒惰

9.10

- [ ] 

