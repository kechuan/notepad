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



<div style="color:red">封装完成后会默认在项目根目录生成<b>dist</b>文件夹 以及其<b>main.js</b>文件<div>



这便是webpack打包完的产物

直接引入这个js 便可调用本次打包的所有资源



*那么代价就是node_module 占用22MB 比你自己写的所有静态网址大小翻了有四倍多体积*

*所以不要傻乎乎的连同node_module一起发布(半恼*

****


### 1.基础设置



#### 0.路径环境

用来导入node.js中专门操作路径的模块

> const path = require('path');

目前意义不是很明

****



#### 1. 入口与出口(Entry&Output)

入口起点(entry point)指示 webpack 应该使用哪个模块

疑似	loader webpack 会找出有哪些模块和库是有依赖关系的。

webpack将打包好的产物称作  Bundle
而所有被打包的东西被称作  chunk 



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

****



3. object(对象,多入口,多出口)

> entry:{ react:{index:[1.js], sub:[2.js]	} jquery:{'jquery.js'},}
对象分为键与值（其实就是属性与对应的值）
每个对象都会被生成一个bundle

`output` 属性告诉 `webpack` 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 `./dist`文件夹 

`output` 分为输出路径(path)与输出文件名(filename)这两个部分



而问题在于既然是多出口 那么每一个出口的名字就应该有独立的一个名字(默认名字都是main.js) 

否则会导致出口名字冲突导致报错

而在下游的output里有适配的输出方式规避名字冲突

则应该使用占位符(substitutions)来确保每个文件具有唯一的名称。

****



**path**
而输出在哪里 则需要依靠node.js环境给的路径了

比如最上面提到的

> const path = require('path')

这项操作使得webpack能借助node访问当前的路径并绑定在path常量里

> output:path:		path.resolve(__dirname,'dist'),

****




#### 2.输出配置

**filename**
而output文件名输出 `filename` 里提供了一组配置供我们使用
[name]	根据对象的键名来命名出口
－[hash]	追加hash值来校验*所有*对象打包的内容变与不变
--[hash:num] 生成hash的长度(默认16位)

如变动则生成新的js

－[chunkhash]只针对变动的文件发生hash变动并创立
> output:{filename:[name]-[hash:6]... }

****

**loader:**
兼容性管理
通过调用npm里的其他解码包 来生成对应处理过的可被浏览器直接读取的资源文件以达成兼容的目的

通过rules:
来引入 test,use:loader
test则为引入的文件类型
use则为对此文件类型采用对应的手段
而loader便是手段本身(一般通过npm包引入)


> module.export = {
> test: /\.css$/,
> use: [ { loader: 'style-loader' }, { loader: 'css-loader', options: { modules: true } } ] } ]
> }

****

**mode:**
module.exports = { 
mode: 'production'/mode: development 
};

webpack联动npm工作环境(线上环境与开发环境)
不过疑惑的是 命令行直接

> webpack -D/-S
就能选择了

~~为啥还要特地配置呢~~



22.4.27

现在你知道了 webpack会根据你`webpack.config.js`线上环境和开发环境的区别

执行不同的方案打包	这就是为什么要额外配置的原因



且webpack本身有这么一种处理机制

> -D操作会使得webpack快速打包 快速生成main.js
>
> -S操作则为使得webpack采用尽力压缩算法 节省空间

****
