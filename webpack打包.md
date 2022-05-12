#### 为什么需要webpack？

前端路线——打包工具


>  因为webpack将我们所有浏览器无法直接读取的文件通过依赖建立的方式与对应的文件关联（less,json）等文件与开发运行环境的工具打包 最终转化为浏览器可以读取的静态文件包(css,js,img..)

而且 你打包也意味着运行环境的隔离
也能体现的出移植性

还记得json的原生导入(assert)
得至少在91+版本的Chrome么

这显然已经不符合这一世代的泛用性了
那就只能靠webpack这种引入第三方工具编译了

而且而且 react也需要这种工具
*来干嘛？*



这个也不是什么新概念 之前引入ES6 module模块时已经有过这种打包的思想

****



### 0. 运行环境

node.js>npm>webpack

**文件配置**

在工作环境(项目根目录下)文件下创立`webpack.config.js`

基础内容应包括`module.export`以声明以下内容都是将作为以**ES6**的**module**总出口导出 以达成大部分浏览器平台的兼容性

`webpack.config.js`一般与将要被打包的模块平级 以方便调用

****



**运行配置**

最后在**npm**项目根目录下的`package.json`中的`script`引入webpack入口

```
Expression_1:
"scripts": {
    "dev": "webpack"
  },
```

再执行

> npm run dev

以执行**webpack**封装程序



*那么代价就是`node_module` 占用22MB 比你自己写的所有静态网址大小翻了有四倍多体积*

*所以不要傻乎乎的连同node_module一起发布(半恼*

****


### 1.基础设置



#### 0.路径环境(建议)

用来导入node.js中专门操作路径的模块

> const path = require('path');

引入当前路径的变量	不管兼容性还是易用性都比敲纯路径要有效的多



****



#### 1. 入口与出口(Entry&Output)

入口起点(entry point)指示 webpack 应该调用哪些东西打包成模块

并将下文的loader一起联合 处理引入的模块



**webpack**将所有被打包的东西被称作 `chunk` 

**webpack**将打包好的产物称作  `Bundle`



<div style="color:red">默认的打包入口文件会在<b>src</b>文件夹里的<b>index.js</b>



*注:无论是默认入口还是默认出口的**文件指向路径**与**名称** 均可以被`webpack.config.js`相关配置修改*

****

**entry:**

单入口与多入口

1. string --> './js/json2css.js'
	字符串方式(单入口)
	
	不写名称直接引入路径
	
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

在某个**html**上直接引入这个**js** 便可调用本次打包内含的所有资源

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

> path:path.resolve(__dirname,'???')

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



### 2.Asset层级资源

*require(webpack5+)*

webpack5中因为原生兼容了通常资源的载入(图片/url/..etc)

即使你不用去特地的去**引入**也能够自动处理



其中划分为:

1. asset/inline => file-loader(include svg!)
2. asset/resource => url-loader
3. asset/source => raw-loader



在webpack5中 对常规资源打包如下

例如官方演示代码中的`.png`图片

> ```diff
> module: {
> +   rules: [
> +     {
> +       test: /\.png/,
> +       type: 'asset/resource'
> +     }
> +   ]
> + },
> ```

注:实际上如果只是普通的html网页src引入的话 甚至都**不需要**专门去配置

会默认直接以**[hash:16]**的形式丢在你打包完的文件夹里



好 那我要怎么给每个图片以及其他资源设立独立的文件夹与文件名？

这就得开始需要用一些额外设置了



它可以通过下文的generator节点设置来独立设置



### 3.其他配置

****

##### **mode**

> module.exports = { 
> mode: 'production'/mode: development 
> };



webpack联动npm工作环境(线上环境与开发环境)
不过疑惑的是 命令行直接

> webpack -D/-S
> 就能选择了

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



##### plugins

一般会和你引入的第三方包环境联动

例如

> const Htmlplugin = require('html-webpack-plugin')
>
> const webpage = new Htmlplugin({	//因为其是一个实例函数 所以你需要new一个来调用 并指定其参数
> 	template: './src/index.html',
> 	filename: './index.html'
> })
>
> 则在moudle.exports的plugins节点中
>
> plugins:[webpage],

感觉本质上就是全局作用型的**module.rules**



##### resolve

字如其名 负责解析部分 

不过是负责设置模块**如何**被解析(options)



****

**alias**



**@的用处**

基于webpack中**resolve.alias**节点特性

在webpack打包时，会把路径引用中的@符号，转换为相对应的路径

**usage**:

> ```js
> module.exports = {
>   resolve: {
>     alias:{	//alias(别名的意思)
>       'vue$': 'vue/dist/vue.common.js',
>       '@': path.resolve(__dirname, './src'),　　// 通过这里的配置，@符号等同于src 
>     }
>   }
> }
> ```

简单易懂 实际上就是名称上define/const

目的也很简单 为了在js引入模块上做到简化与语义化

通过此操作后

其实就类似于模块环境里的

> import @ from './src' => import $ from 'jquery'



****

##### loader/generator

兼容性管理
通过调用环境里的其他解码包 来生成对应处理过的可被浏览器直接读取的资源文件以达成兼容的目的



webpack本身打包只能处理以.js模块 非js的模块webpack并不能处理

所以需要loader引入第三方加载器协助打包

> css-loader:	*.css
>
> less-loader:	*.less
>
> 
>
> ...



通过**module**节点中**rules**数组里:
来引入**test**与**use** 来处理webpack本身无法处理的模块

test则为匹配的文件类型(类似**try**):可以用正则来匹配
use则为对此文件类型采用对应的手段(类似**catch**)

```js
module: 
{
rules: [{
  	  test: /\.css$/,						//test代表对何种文件生效(try)
      use: [{loader: 'style-loader'},		//use代表采取什么loader(catch)	
            {loader: 'css-loader',
             options: {modules: true}		//options中的选项会因各个引入的loader不同
            }]		
      	}]
}
```

关于loader的调用**顺序** 是从后往前调用(老出入栈思想了)



`module.rules`允许你在 webpack上配置中指定多个 loader



其余第三方loader(此处不看作额外**功能性**插件):

[为什么解析css内容需要两个loader?(简书)](https://www.jianshu.com/p/d2470f719fee)

1. style-loader	再将其套入style标签封装(css-in-js)
   1. css-loader      先将css解析出来(将css的每一行内容单独字符串解析出来，合为一个总数组)





****

*require(webpack 5.12.0+)*

**module.generator**

这个节点来**确定如何处理项目中不同类型的模块**



在使用webpack5时 默认配置的 三个loader皆会与asset处理冲突

> When using the old assets loaders (i.e. `file-loader`/`url-loader`/`raw-loader`) along with Asset Module in webpack 5, you might want to stop Asset Module from processing your assets again as that would result in asset **duplication**. This can be done by setting asset's module type to `'javascript/auto'`.

冲突是因为两个进程造成的资源打包重复

你可以在**rule**节点下添加**type**节点:

> type:javascript/auto

以规避冲突



而且文档还提到过

> `asset` automatically chooses between exporting a data URI and emitting a separate file. Previously achievable by using `url-loader` with asset size **limit**.
>
> 等效于
>
> use['url-loader'],options:{limit:???}

已经可以自己自动选择合适的limit大小了



那既然原生都自带处理程序了 且你项目没怎么开始构建 那自然就转用官方的asset试试看

不过管理方式的节点就不是单纯的**test**/**use**

而是统一用**generator**这个节点管理



实例**usage**:

```js
{
test: /(\.jpg|jpeg|png|bmp|ico|gif)$/,
type:'asset/resource',	//因为原生的关系 措词关系不再是引入 而是直接指示资源的类型让webpack处理
    generator: {		// Generator options for asset modules(实际上就是options for asset)
        filename: 'images/[name]_[hash:8][ext]'	 //通用的filename,outputPath,etc...
	}

 }
```



**注意**

*webpack5+*

在以往的webpack版本中	像url/图片之类的资源 要靠第三方loader去解析

而在webpack5里已经可以 直接载入这类资源 而不用再去自己手动适配了！！！



这原本应该是好事 然而又是经典前端更新后端不更 webpack本体改是改了

然后file-loader,url-loader全特么没改 

经典白忙活一天 

经典官方**中文**文档对这类改动的**兼容性**问题不谈

[From CSDN](https://blog.csdn.net/Coralpapy/article/details/119419137)



22.5.7

英文文档里有 也确实谈了这个问题

但是中文文档的https证书不更新 根本进不去



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





****





### 4.节流/优化

文件大小分割/base64转换





代码内联

所谓内联就是打包的时候将代码直接写在该html内 这样在请求的时候可以减少服务端HTTP请求次数

代价当然就是用户端一次性接收的文件大小变大



****



### 5.打包后排障处理

为什么需要这样做？

webpack是多么方便 直接合并各种loader(less,vue,jquery)堆成一个js让你去慢慢开发

所以很有可能你以后就干脆一直用webpack了(反正有devserver帮你实现类似live-server的效果)

好了 问题来了

因为代码是直接被你**打包**过的 如果某个环节报错了 你可能难以定位到错误信息



我写的东西里 暂时找一个不太好说明的例子

local:

> << http://127.0.0.1:8666/images/mediabox/carousel_04.png 404 (Not Found)



webpack打包

> <<carousel_.*\.png$:14 Uncaught Error: Cannot find module './carousel_04.png'
>     at webpackContextResolve (VM1159 carousel_.*\.png$:14)
>     at webpackContext (VM1159 carousel_.*\.png$:9)
>     at Object.change (VM972 carousel.js:61)
>     at Object.next (VM972 carousel.js:25)
>     at HTMLDivElement.eval (VM954 javascript.js:54)



同样是报错信息

本地**live-server**下 可以说是言简意骸 关系链仅仅只有找不到04.png

**webpack**上则扯出来一堆的错误链 jquery.next()调用>JavaScript.js(import carousel)>carousel

最后给你说找不到04.png这个模块

而且实际上**最后**还没有指出到底是说04打包失败(命令行里看)/还是说根本没有04图片



那么 我需要 至少能让在打包环境下还原出本地live-server的环境的**报错信息**



#### sourceMap

这就是 `Source Map` 想要解决的问题。

sourceMap不是单独的一个软件 似乎是一种集成手段 类似live-server一样的动态服务器

甚至webpack本身就有sourceMap的设置

![](https://pic3.zhimg.com/80/v2-a1b36828a0e36d46b5e9325de2a97e02_720w.jpg)

说实话 我没感觉给的报错代码有哪里不一样 好像默认的就够了？？



建议刚写代码需要频繁调试的时候 把值切到 `eval-source-map`

建议调试完后 默认不用动



而在生产环境下 建议是把值切到 `nosources-source-map` 可以避免源码泄露 而写过的人也能看到

代价就是图所示 速度最慢



笑死 我什么时候才会用到这种功能



先这样了罢(



****





### X.占位符

##### **path**

而输出在哪里 则需要依靠node.js环境给的路径了

比如最上面提到的

> const path = require('path')

这项操作使得webpack能借助node访问当前的路径并绑定在path常量里

> entry:path.join(__dirname,'./js/javascript')
>
> output:{
>
> ​	path:path.resolve(__dirname,'dist')
>
> ​	...
>
> }



****

`path.join()`与`path.resolve()`的区别？



`path.join`	链接路径

> path.join()方法可以连接任意多个路径字符串
>
> ```js
> >>path.join('/foo', 'bar', 'baz/asdf', 'quux', '..')
> //等效于
> <<path.join('/foo/bar/baz/asdf)
> ```



`path.resolve` 路径解析

> path.resolve()方法可以将多个路径解析为一个规范化的绝对路径
>
> 类似于对这些路径逐一进行cd操作，与cd操作不同的是，这引起路径可以是文件
>
> ```js
> >>path.resolve('/foo/bar', './baz') 
> //等效于
> <<path.resolve('/foo/bar/baz')
> 
> path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif') 
> // 当前的工作路径是 /home/itbilu/node，则输出结果为 
> '/home/itbilu/node/wwwroot/static_files/gif/image.gif'
> 
> ```



实际上就是路径处理的不同方式

只不过output上更贴近于实际的文件夹环境(类似 cd操作)里



****



##### **__dirname**

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



### Y.额外插件引入

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
> 4.0.0beta.0 提供了比较完善的错误提示，当设置了错误属性时能够给出详细提示信息。

****





#### html-webpack-plugin

用来自定义你的`index.html`内容 



官方文档介绍:

> [`HtmlWebpackPlugin`](https://github.com/jantimon/html-webpack-plugin)简化了HTML文件的创建，以便为你的webpack包提供服务。这对于在文件名中包含每次会随着编译而发生变化哈希的 webpack bundle 尤其有用。



不过一般而言

我们都是先写好自己的`index.html` 再去写对应的js的

直接纯**js**模式生成**html**至少对于我自己而言还是少见(



所以用此插件**意义**就是为了给自己本地静态的`index.html`与打包的各种js资源关联起来



**usage:**

> npm i html-webpack-plugin



在`webpack.config.js`上如此配置

```js
//引入 htmlplugin 环境
const Htmlplugin = require('html-webpack-plugin')

//根据其实例创建新的对象
const webpage = new Htmlplugin({
	template: './src/index.html',	//入口
	filename: './index.html'
})

module.exports = {
plugins: [webpage],	//最后通过打包的插件节点引入
...
}
```

****



**多页面构建**

`html-webpack-plugin`的一个**实例**生成一个html文件，如果单页应用中需要多个页面入口，或者多页应用时配置多个html时，那么就需要实例化该插件多次；

即有几个页面就需要在webpack的plugins数组中配置几个该插件实例：

```javascript
    ...
    plugins: [
        new HtmlWebpackPlugin({
             template: 'src/html/index.html',
             
        }),
        new HtmlWebpackPlugin({
            filename: 'list.html',
            template: 'src/html/list.html',
            
        }), 
        new HtmlWebpackPlugin({
          filename: 'detail.html',
          template: 'src/html/detail.html',
           
        })
    ]
    ...
```

如上例应用中配置了三个入口页面：index.html、list.html、detail.html；并且每个页面注入的thunk不尽相同；类似如果多页面应用，就需要为每个页面配置一个；



这对iframe页面来说是否有点..



**额外设置**

```json
{
	plugins: [
		new CleanWebpackPlugin(), //删除上次打包文件，默认目录'./dist'
		new HtmlWebpackPlugin({ // 打包输出HTML
		  title: '测试htmlWebpackPlugin',
		  minify: { // 压缩HTML文件
			removeAttributeQuotes: true, // 移除属性的引号
			removeComments: true, // 移除HTML中的注释
			collapseWhitespace: true, // 删除空白符与换行符
			minifyCSS: true// 压缩内联css
		  },
		  (多页面构建非常注意！！！)inject: true, // 默认值为true 会自动将输出的js自动绑定在新构建的html上,false关闭
		  hash: true, // 引入 js 文件后面紧跟一个独特的 hash 值
		  // filename: 'huangbiao.html', // 文件名
		  filename:'huangbiao-[hash].html', // 带hash 值的文件名
		  template: './src/template/index.html' // 模板地址
		})
	  ],
}
```



另一个大问题

这个插件**不会**去处理**内联**的css!

又因为`webpack`环境上只能对**import**的模块做处理 如果你不把内联的`css`单独提取出一个模块让`webpack`处理

简单来说就是那段**内联**`css`直接失效



可惜的是 这个插件没有内置的选项去实现这个东西 你得找另外一个插件去实现它

****



#### ExtractTextWebpackPlugin

你这上下段还是连着的啊

你的**css样式**将不再内嵌到 JS bundle 中，而是会放到一个单独的 `CSS` 文件（即 `styles.css`）当中。





****



#### clean-webpack-plugin

帮你清除打包之后的输出目录 避免文件冲突(说实话这个功能迟早应该被官方吸收)

**简单配置**

光速吟唱安装过程

> npm i clean-webpack-plugin

它是**实例函数**

> const cleanPlugin = new CleanWebpackPlugin()

然后直接插件节点中引入即可

> module.exports = {
>
> ...
>
> plugins:[cleanPlugin],
>
> ...
>
> }



plugin:[From(npm.js)](https://www.npmjs.com/package/clean-webpack-plugin)

