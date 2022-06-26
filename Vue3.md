> 本md除了js的基本规则以外有其他的修订(说明)
>
> - [!]：Todo 												 Total:2
> - [?]：书写位置疑似不适合                        Total:1
>
> v1.2 贺电一下typora终于支持代码块中的多光标选择了

## Vue.js

*require vue3+*

### 0.介绍



一套用于构建用户界面的**渐进式框架** 帮你从js底层与表层html的各种标签直接建立一层关系

从而**方便**你快捷将底层的js呈现在表层的html上

*渐进式*:简单来说就是要用什么给你什么 跟你调用单个函数这种感觉



为什么不接着用jQuery更新DOM？

> 我们要做的无非就是更新类似计时器一样的数值 然后等待DOM更新
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



#### 自带Tree-Shaking

webpack上终究还是外部环境 既然是外部环境就难以断明那些内部代码里哪些是真正不用的

例如经典的

> import $ from 'jquery'

你可能仅仅只是想要其中的某一两个功能写法

结果还是得白白多几百K占用 这些占用是外部wepback无法筛掉的



`compositionApi`

复用api



[?]鸥鸽鸽之前提到过用vue代替juqery实现$的功能 或许我以后也可以试试



#### 包管理



##### monorepo

vue作为一个框架 它也有类似于包的关系

且调用思想跟其他的包管理工具差不多

可以在vue的基础环境下选择性的调用哪个包

这也是为什么它会被叫做 **渐进式框架** 的原因



其实就和npm的差不多 只不过引入的包是专门给vue的

`@vue/comiler-dom` `@vue/runtime-core` `@vue/reactivity`....



~~`monorepo`目前只有`yarn`管理工具支持~~

搓啦 现在pnpm/npm都支持monorepo了

那我当然用统一包提升管理的pnpm了



#### Typescript

> npm i typescript

你可能已经看到上面的main入口不是传统的js 而是ts

为什么必须得用ts？



道理很简单

**Vue3就是用TypeScript写的！！！**

我并不怎么接受说ts一定比js好 它只是相对于原生文本多了很多规范

然而你js写的好 那效果是完全一致的



但是先边学边试着用着罢 反正webpack里肯定也有`ts-loader`之类的东西

****



#### 打包工具

你当然可以继续用webpack来打包 但是针对于这种架构型的东西 更建议用rollup

> 和webpack相比，rollup更加的小巧简介，它更加适用于构建各种类库，比如你的项目需要代码拆分、含有图片、字体等资源。webpack比rollup更加适合。

可是我肯定终究还是要用webpack打包其他东西的

而这是下文`package.json`要写的东西



而且因为rollup 是纯import环境(完全基于ES模块引入)

这使得以前想用require进行节流的操作不再可行 也使得不能像webpack一样热替换快捷操作



试试看能不能仅用rollup打包架构

再用webpack封装静态资源罢



鉴于我自己最后还是会用webpack来封装

rollup用法我只会写在这里的Vue篇



### 1.环境搭建

*[!]此部分将会与npm(pnpm)篇一同书写*

上文也提到过**vue3**是统一用`monorepo` ,`typescript`书写,以及最好用`rollup`来搭建的



那么是怎么来搭建呢？

****

#### 子包管理

前文说到它是可以支持多个子包引入的

那它是怎么做到的？

首先monorepo要求将项目划分**工作区(workspace)**这个概念

这样在工作区这个概念里自然也就可以随意划分子包了



##### **设立工作区**

如果是npm可能会直接设在package.json

```json
{
"workspaces": [
    "packages/*",表明包的存放目录
  ],
  ...
}
```

不过我这里用的`pnpm` 理所当然的也不会额外再安装`yarn`





然后再这个目录(packages)内设立子文件夹并继续用`yarn/npm/pnpm`初始化项目

唯一不同的是其子包的`package.json`的设置会多了一层**buildOptions**节点



例如:

`package.json`

```json
{
  "name":"@vue/reactivity",	//代表其在vue下的组件
  "version":"1.0.0",
  "main":"index.ts",
  "module":"dist/reactivity.esm-bundler.js", //代表其打包完之后生成的目录 方便给webpack用
  "license":"MIT",
  "buildOptions":{
     "name":"VueShared",
     "fromats":["cjs","esm-bundler"] //允许commonjs,esm引入
  }
}

```



现在你的项目目录大抵应该是这样的

> package.json
>
>  |—packages/
>
>  ​	|——@vue/reactivity
>
> ​					|—package.json
>
>  ​		|——@vue/shared
>
> ​					|—package.json



到这一步 实际上已经完成了`monorepo`模式的设置



在模块安装的时候

`monorepo`对对应模块安装划分为了**全局依赖**以及**局部依赖**

> npm i -w

**当设立工作区之后 常规的简略安装已经无法使用 必须带上-w/-r**

*-w就是workspace整体 合理*

*-r 你也可以安装到仓库`node_module`里*



**局部依赖**

> npm i --r -F [filename/projectname]



##### **工作区的打包输出**

**链接嵌套**

在原本的`yarn`与`npm`环境下 只需要运行一次

> npm i
>
> yarn add

就会自动将`packages`下的文件自动链接到项目里面



然而**pnpm**不一样,它针对**workspace**下有一个独特的机制



在你输入了

> pnpm i

它不会自动将你的packages链接到主项目 

而是显示**scope**以提醒你目前项目下的工作区的项目



如官网文档所说的这样做是为了避免远程仓库和本地仓库的命名重复造成不确定性

默认状态下 你有两种方法来使packages内的项目之间互相引入

一是

> pnpm i @vue/shared -r -F  @vue/reactivity
>
> 将packages下的A项目引入到B内



二是手动在`package.json`下的**dependences**引入该文件

此时因为本地仓库的优先级优于远程仓库的优先级

pnpm会自动在packages文件下寻找是否含有本地的仓库

有则直接通过链接方式引入



两种方式都会在`pnpm ls`命令下标注该包是通过链接引入的说明



[?]不过你可以在`.npmrc`文件下手动设置**link-workspace-packages**属性为**deep**



> 启用该选项，本地可用的 `packages` 将被链接到 node_modules 中而不是从配置源下载。 这在 `monorepo` 项目中使用起来将十分方便。 如果您需要本地包也链接到子依赖项，您可以使用 `deep` 设置。

 

然而引入了还不行

因为此时只是代表着项目引入了 但是实际上在node环境下还是无法具体找到该模块



> 明明执行了命令之后 `package.json` 是可以正常的添加依赖的
>
> 然而cli上却提示
>
> *No projects matched the filters*？



##### Typescript的环境设置

初始化配置文件

> npx tsc --init

默认会在当前目录下生成`ts.config.json`

****



**解析方式**

因为ts牵扯到多种方式的引入模块 不仅仅是原生的**import** 可能ts还对其他大型项目做出过特别的兼容罢



因为本md是以node环境下为前提的

所以在初始化的`ts.config.json`中 应额外配置

> "moduleResolution":"node"



自此说明在当前node环境下

假如你的入口是`index.ts`

那么当前环境下的**typescript**就会通过`index.ts`以**node**环境处理文件



**环境变量**

以及另一个因素是环境变量**path**



> 你仅仅只是在**rollup**上配置了环境变量为当前项目文件夹
>
> 而对ts本身的配置文件却没有配置 或者说**rollup**执行**tsloader**的时候压根没给其传过参
>
> 那ts本身自然也找不到 模块的位置了



配置方式就和你做过的webpack的配置一样

不过不再是path,resolve(__dirname) 这种js写法

而是针对于ts配置本身的来进行环境变量设置



在上层的rollup手动配置了`ts.config.json` 那么下层自然就不用再次配置绝对路径了

基础的设置有**baseUrl**,**paths**来组合说明ts处理器要寻找的目录以及文件夹

`ts.config.json`

```json
"baseUrl":"./", //根目录查找 相当于path
    "paths":{
      "@vue/*":[      //对于@vue下的子包软链 会去寻找真正的源
        "packages/*/src"
      ]
    }
```

****



#### 打包

子项目全部完成了之后那自然就要靠打包输出了

前文提到过vue最好使用`rollup`来打包



在node环境下装好了rollup之后

> npm i rollup -w

 

需要和wepback一样在项目根目录创立对应的配置文件

在这里叫做 `rollup.config.js`

配置其实和webpack大同小异



但是因为一般在上线环境上rollup需要寻找子包集合下的所有文件夹对应的index入口

在路径定义上会比较精细点

```js
import path from 'path'

const packagesDir = path.resolve(__dirname,'packages'); 
//当前目录下寻找packages(子包集合)文件夹

const packageDir = path.resolve(packagesDir,process.env.TARGET); 
// process.env node的进程环境变量 顺便判别你是线上还是开发环境 
//packages文件夹下的子包 真正的子包基准目录

const resolve = (p)=>path.resolve(packageDir,p) 
//一层层嵌套下来 简略定义解析地址 

const pkg = require(resolve('package.json'))
const name = path.basename(packageDir) 	//取文件名
```



以及打包上的具体差异

```diff
- module.export:{
- entry: {
-		javascript:{import:path.join(__dirname,'/src/js/javascript.js'),dependOn: 
- 'shared'},
-		sidebar_css:{import:path.join(__dirname,'/src/sidebar/css.js')},
-		shared: ['jquery']	//共享合集
-	},
-	output: {
-		path: path.resolve(__dirname,'dist'),
-		filename: 'js/[name].js'
-	},
- ...

+ function createConfig(format,output){
+ 	return{
+ 		input:resolve(`src/index.ts`),
+ 		output,
+ 		plugins:[
+ 			json(), //json无需额外配置
+ 			ts({
+ 				tsconfig:path.resolve(__dirname,'tsconfig.json')	
+ //ts插件 必须需求常规+ tsconfig.json
+ 			}),
+ 			resolvePlugin()
+ 			
+ 		]
+ 	}
+ }
+ export default options.formats.map(	//将对应的键值对映射出来并最终输出
+ format=>createConfig(format,outputConfig[format])
+ )
```

可以看到 相对于webpack的精细分离所有出入口**一并**处理 

`rollup`是更注重于单项目下的输入输出 

所以实际上并没有`webpack`那种 错一发动全身的感觉



记住最后不管怎么样 你都是要让它们变成静态的js让webpack引入的





****



### 2.创建/挂载

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



### 指令

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



jQuery貌似不能直接.css("style","attr") 看看vue行不行



### 组件化

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

****



### API

Vue本体对开发环境提供了4个API

> - reactive
> - shallowReactive
> - readonly
> - shallowReadonly



reactive代表着proxy响应式

shallow代表着浅层

意味着被带上shallow关键字的属性是会对表层(即为数组/对象直接接触的属性)生效



****

*为什么说因为`reactive`调用了**Proxy**就会被叫做响应式？*



因为Proxy的运行原理(特别是**set**)就是响应式的,所以在封装了Proxy处理方式的`reactive`也是响应式的

例如选用Vue3的第一个API `reactive`

`index.html`

```html
<script src="vue.global.js"></script>
<script>
	let {reactive} = Vue <!--使该对象绑定Vue上的API 类似于激活罢-->
    
	console.log(reactive({name:3}))  
</script>


<<Proxy {name: 3}
```

它会在控制台上直接输出Proxy，证明其本身就是通过Proxy响应式的设计

比如**Proxy**中的子方法set 其可以在进行值更新之后允许插入额外的function操作



那么问题来了(

我为什么不直接用Proxy呢？

reactive本身到底额外封装了什么内容 对比单纯的Proxy多了什么功能？



简单来说 是Vue对内置的各个子方法内额外封装了一大堆的**handler**

从而在调用Vue下的reactive的时候，用引入的内置的方法就比自己额外写Proxy要好的多(



****





