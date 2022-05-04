#### 为什么需要webpack？

前端路线——打包工具


>  因为webpack将我们所有浏览器无法直接读取的文件通过依赖建立的方式与对应的文件关联（less,json）等文件与开发运行环境的工具打包 最终转化为浏览器可以读取的静态文件包(css,js,img..)

而且 你打包也意味着运行环境的隔离
也能体现的出移植性

还记得json的原生导入(assert)
得至少在91+版本的Chrome么

这显然已经不符合这一世代的泛用性了
那就只能靠webpack这种第三方引入编译了

而且而且 react也需要这种工具
*来干嘛？*



这个也不是什么新概念 之前引入ES6 module模块时已经有过这种打包的思想

****



### 0. 运行环境

node.js>npm>webpack

**文件配置**

在工作环境(项目根目录下)文件下创立`webpack.config.js`

基础内容应包括`module.export`以声明以下内容都是将作为以ES6的module总出口导出 以达成大部分浏览器平台的兼容性

`webpack.config.js`一般与将要被打包的模块平级 以方便调用

****



**运行配置**

最后在npm项目根目录下的`package.json`中的`script`引入webpack入口

```
Expression_1:
"scripts": {
    "dev": "webpack"
  },
```

再执行

> npm run dev

以执行webpack封装程序



*那么代价就是node_module 占用22MB 比你自己写的所有静态网址大小翻了有四倍多体积*

*所以不要傻乎乎的连同node_module一起发布(半恼*

****


### 1.基础设置



#### 0.路径环境

用来导入node.js中专门操作路径的模块

> const path = require('path');

引入当前路径的变量	不管兼容性还是易用性都比敲纯路径要有效的多



****



#### 1. 入口与出口(Entry&Output)

入口起点(entry point)指示 webpack 应该调用哪些东西打包成模块

并将下文的loader一起联合 处理引入的模块



`webpack`而所有被打包的东西被称作 `chunk` 

`webpack`将打包好的产物称作  `Bundle`



<div style="color:red">默认的打包入口文件会在<b>src</b>文件夹里的<b>index.js</b>

*注:无论是默认入口还是默认出口 均可以被`webpack.config.js`相关配置修改*

****



单入口与多入口

**entry:**

1. string --> './js/json2css.js'
	字符串方式(单入口)
	此时chunk们都有一个默认的名称为 "main"

>	entry:'./js/json2css.js'

既然会有默认名称 说明这个方式引入多个chunk将会发生命名重复的问题 这也是会被叫作单入口的原因

****



2. array --> ['./js/json2css.js','pink.json']
   	数组方式（多入口）

> entry:['./js/json2css.js','pink.json']

(意义不是非常的大 一般这样做也等效于在一个index.js上import一大堆额外的东西)

****



3. object(对象,多入口,多出口)

> entry:{ react:{index:[1.js], sub:[2.js]}, jquery:{'jquery.js'}}
对象分为键与值（其实就是属性与对应的值）
每个对象都会被生成一个bundle

(这个主要是用来明确的区分环境 或者为不同的版本产出)

****



**output**:

`output` 属性告诉 `webpack` 在哪里输出它所创建的 bundles，以及如何命名这些文件



<div style="color:red">封装完成后会默认在项目根目录生成<b>dist</b>文件夹 以及其<b>main.js</b>文件<div>
这便是`webpack`打包完的产物

在某个html上直接引入这个js 便可调用本次打包的所有资源

****



`output` 分为输出路径(path)与输出文件名(filename)这两个属性

```javascript
output:{
	path:,
    filename:
}
```



`output`本身是支持**多出口**的

而问题在于既然是**多出口** 那么每一个出口的名字就应该有独立的一个名字(默认名字都是main.js) 

否则会导致出口名字冲突导致报错



这就是为什么`output`里不会像`entry`一样 一个配置写满`path`与`filename`

毕竟`entry`上 文件名是已经确定的

而`output`在多文件上则是属于未确定的文件名 会有概率重复



**path**:

此处`path`基本会与`entry`的规则配置一致 只是输出不再是具体到文件 而是文件夹

因为文件名会交给`filename`处理





**filename**:
而output文件名输出 `filename` 里提供了一组配置供我们使用
[name]	根据对象的键名来命名出口
-[hash]	追加hash值来校验*所有*对象打包的内容变与不变
--[hash:num] 生成hash的长度(默认16位)

如变动则生成新的js

-[chunkhash]只针对变动的文件发生hash变动并创立

> output:{filename:[name]-[hash:6]... }

则应该使用**占位符**(substitutions)来确保每个文件具有唯一的名称。

****



#### 2.占位符



**path**
而输出在哪里 则需要依靠node.js环境给的路径了

比如最上面提到的

> const path = require('path')

这项操作使得webpack能借助node访问当前的路径并绑定在path常量里

> output:path:		path.resolve(__dirname,'dist'),

****



**__dirname**

文件名变量	*一般代表该文件所存在的目录*

> entry:	path.join(__dirname,'./src/index.js')	
>
> //入口处配置 路径环境配置 加入 当前文件名路径中的 './src/index.js'

这样就能简单的指定打包的入口



output同理

> output:{
>
> path: path.join(__dirname,'src'),
> filename: 'bundle.js'
>
> }

****



#### 3.其他配置

****

##### **loader**

兼容性管理
通过调用npm里的其他解码包 来生成对应处理过的可被浏览器直接读取的资源文件以达成兼容的目的



webpack本身打包只能处理以.js模块 非js的模块webpack并不能处理

所以需要loader引入第三方加载器协助打包

> css-loader:	*.css
>
> less-loader:	*.less
>
> 
>
> ...



`module.rules`允许你在 webpack上配置中指定多个 loader

一般来说loader都有这样的子选项

> ```js
> module: 
> {
>  rules: [{
>      test: /\.css$/,						//test代表对何种文件生效(try)
>      use: [
> 			{loader: 'style-loader'},		//use代表采取什么loader(catch)	
>          	{loader: 'css-loader',options: {modules: true}}
>          	//wepack5+ 而loader本身有会有子选项options 这因loader本体而不同
>           ] 	 	
> 		}]
> }
> ```





第三方loader:

[为什么解析css内容需要两个loader?(简书)](https://www.jianshu.com/p/d2470f719fee)

1. style-loader	再将其套入style标签封装(css-in-js)
   1. css-loader      先将css解析出来(将css的每一行内容单独字符串解析出来，合为一个总数组)





**注意**

*webpack5+*

在以往的webpack版本中	像url/图片之类的资源 要靠第三方loader去解析

而在webpack5里已经可以 直接载入这类资源 而不用再去自己手动适配了！！！



这原本应该是好事 然而又是经典前端更新后端不更 webpack本体改是改了

然后file-loader,url-loader全特么没改 

经典白忙活一天 

经典官方文档对这类改动的**兼容性**问题不谈

[From CSDN](https://blog.csdn.net/Coralpapy/article/details/119419137)



****



通过**module**节点中**rules**数组里:
来引入**test**与**use** 来处理webpack本身无法处理的模块

test则为匹配的文件类型(类似**try**):可以用正则来匹配
use则为对此文件类型采用对应的手段(类似**catch**)


> module.export = {
>
> module: {
> 		rules:[
> 			{test: /\.css$/, use:['style-loader','css-loader']}	//匹配css后缀 对其使用两个loader 
> 		]
> 	}
>
> }



关于loader的调用**顺序** 是从后往前调用(老出入栈思想了)







****

##### **mode**

> module.exports = { 
> mode: 'production'/mode: development 
> };



webpack联动npm工作环境(线上环境与开发环境)
不过疑惑的是 命令行直接

> webpack -D/-S
就能选择了

~~为啥还要特地配置呢~~



****

22.4.27

现在你知道了 webpack会根据你`webpack.config.js`线上环境和开发环境的区别

执行不同的方案打包	这就是为什么要额外配置的原因



且webpack本身有这么一种处理机制

> -D操作会使得webpack快速打包 快速生成main.js
>
> -S操作则为使得webpack采用尽力压缩算法 节省空间

****



##### **devServer**

该节点负责的内容也很简单明了 跟live-server类似

负责输出内容的服务器各项调整

> devServer:{
> 		static: './src',	//webpack5+ 暂且未知定位信息
> 		open: true,	//弹出浏览器 live-server里则是nobroswer
> 		host: 'localhost',
> 		port: 8888
> 	}



不过实际上你也可以直接在`package.json`中的scripts上操作也是可以的 这也等同于npm环境上的操作

> "scripts": {
>     "dev": "webpack serve --port=8888"
>
> }



****



### 2.额外插件引入

[webpack](https://www.webpackjs.com/plugins)官方提供了很多插件以及说明文档

<div style="color:red">额外插件所有的设置 一般都应该在webpack.config.js中配置</div>

这里调一些一般都会用得上的来讲

 



#### **webpack-dev-server**

实现类似live-server的效果	但是是作为一个实时打包器



##### 配置

****

**usage:**

模块安装后

在`package.json`的`script`节点中引入`serve`

默认端口值为8080

每次webpack打包的时候就会自动连携该插件



这个时候你就得问 那我为什么不直接用live-server监控所有文件?

****

好 那我们先直接用live-server(



live-server

> pnpm i live-server -g

用法简单粗暴 直接在**全局模块**上安装 然后直接npm环境执行live-server就行

同你在sublime-text上的设置一样

```json
{
  "port": 8888,
  "cors": true,
  "browser": "default",
  "nobrowser": false,
  "wait": 100
}

```

当然NODE_PATH一类的东西是已经调好了的 一般用得上的就是port之类的杂项

运行的时候附带参数就行

> live-server --port=8888 --nobroswer=false



或者是在上文一样在config上单独设立 再用json方式调整



然而这样的话每次打包变更都得

> [editor] --save
>
> npm run dev
>
> ………………

****



然而webpack-dev-server

仅仅只需要在编辑器上执行保存的动作 就能一键连携

且devServer会将打包的文件放入内存作为缓存 要调用的时候直接从内存中读取

无论是从性能上还是损耗性都会是这个好



##### **注意**

但是正因如此 启用了**serve**后 它也不会在磁盘上生成文件 而是一直只读内存上的缓存文件

> 在网站上会读取到 xxx:8888/js.js

所以在**production**环境下不应该启用它 改该用正常的live-server了(



我感觉可以说是叠加了打包功能的live-server

实际上在控制台上也确实是这样子(

> (2) [webpack-dev-server] Live Reloading enabled.	VM1946 index.js:551 

不过用的是livereload

****





##### 排障

22.4.30	经典前端改动后端不改

****

webpack-dev-server返回404返回页面

> 应该还是版本问题，最后在官网文档上找到
>
> ```json
> devServer: {
> 	static:'./src'	//默认本应为当前工作目录
> }
> ```

From: [CNblogs](https://www.cnblogs.com/tangtangtang1/p/15459368.html)



而默认属性是项目根目录/public	

> <i> [webpack-dev-server] Content not from webpack is served from 'C:\Users\lenovo\Desktop\website\Lab(HTML测试)\webpack\0.color_interaction\public' directory

好家伙 你webpack打包出来的默认文件夹充其量默认是dist 好端端哪来的public啊？？？



正常旧版本至少还会提示

> webpack output is served from /???

新版本居然什么都没提示



推荐选择版本

> webpack 5.42.1
>
> webpack-dev-server@4.0.0beta.0 
>
>  4.0.0beta.0 提供了比较完善的错误提示，当设置了错误属性时能够给出详细提示信息。

****





#### html-webpack-plugin

用来自定义index.html内容 我现在确实不知道有个什么用

先空着

****
