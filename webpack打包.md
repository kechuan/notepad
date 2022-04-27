前端路线——打包工具

为什么我们需要webpack这类打包工具？
>  因为webpack将我们所有浏览器无法直接读取的文件通过依赖建立的方式与对应的文件关联（less,json）等文件与开发运行环境的工具打包 最终转化为浏览器可以读取的静态文件包(css,js,img..)

而且 你打包也意味着运行环境的隔离
也能体现的出移植性

还记得json的原生导入(assert)
得至少在91+版本的Chrome么

这显然已经不符合这一世代的泛用性了
那就只能靠webpack这种第三方引入编译了

而且而且 react也需要这种工具
*来干嘛？*



这个也不是什么新概念
之前引入ES6 module模块时已经有过这种打包的思想



### 0. 运行环境
node.js>npm>webpack

文件配置
在工作环境文件下
创立webpack.config.js
内容包括

0.node.js操作路径环境
1. module.export
2.包选取的模块(入口)
3. 出口的命名
3.1.loader javascript兼容性处理 
4.npm模式选择


> 基础路径结构:const path = require('path');

且之后所有出入口相关的打包 兼容性处理应被
`module.exports{}`包裹

> module.exports{
> output:,
> loader,
> }

亦或是

> const config = {entry:,output:,loader:,...}
> module.exports = config;


以声明以下内容都是将作为es6的module导出

webpack.config.js一般与将要被打包的模块平级 以方便调用

****
#### 0.路径环境
const path = require('path');

#### 1. 入口与出口(Entry&Output)
入口起点(entry point)指示 webpack 应该使用哪个模块

疑似loader webpack 会找出有哪些模块和库是有依赖关系的。

webpack将打包好的产物称作  Bundle
而所有被打包的东西被称作  chunk

单入口与多入口
entry:

1. string --> './js/json2css.js'
	字符串方式(单入口)
	此时chunk们都有一个默认的名称为 "main"

>	entry:'./js/json2css.js'

既然会有默认名称 说明这个方式引入多个chunk将会发生命名重复的问题 也说明这个会被叫作单入口的原因


2.array --> ['./js/json2css.js','pink.json']
	数组方式（多入口）

> entry:['./js/json2css.js','pink.json']

3. object(对象,多入口,多出口)

> entry:{ react:{index:[1.js], sub:[2.js]	} jquery:{'jquery.js'},}
对象分为键与值（其实就是属性与对应的值）
每个对象都会被生成一个bundle

`output` 属性告诉 `webpack` 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 `./dist` 

`output` 分为输出路径(path)与输出文件名(filename)这两个部分

**path**
而在哪里 则需要依靠node.js环境给的路径了
> const path = require('path')
这项操作使得webpack能借助node访问当前的路径并绑定在path常量里

> output:path:		path.resolve(__dirname,'dist'),

****
而问题在于既然是多出口 那么每一个出口的名字就应该有独立的一个名字(默认名字都是main.js) 否则会导致出口名字冲突导致报错

而在下游的output里有适配的输出方式规避名字冲突

则应该使用占位符(substitutions)来确保每个文件具有唯一的名称。

**filename**
而output文件名输出 `filename` 里提供了一组配置供我们使用
[name]	根据对象的键名来命名出口
－[hash]	追加hash值来校验*所有*对象打包的内容变与不变
--[hash:num] 生成hash的长度(默认16位)

如变动则生成新的js

－[chunkhash]只针对变动的文件发生hash变动并创立
> output:{filename:[name]-[hash:6]... }

loader:
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



mode:
module.exports = { 
mode: 'production'/mode: development 
};

webpack联动npm工作环境(线上环境与开发环境)
不过疑惑的是 命令行直接
> webpack -D/-S
就能选择了

为啥还要特地配置呢

