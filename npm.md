与其说是笔记 不如说是折腾日记 



**以后抽时间再来格式化**



#### 0、环境配置

改全局包的路径\模块镜像

 当选择全局安装时，默认的安装路径为`C:\Users\xxx\AppData\Roaming\npm`，缓存路径为`C:\Users\xxx\AppData\Roaming\npm_cache`，其中`xxx`根据自己是自己系统的用户名。



可以直接在users\xxx下新建 `.npmrc`文件

其格式

```
prefix=D:\工具\node.js\npm_global
cache=D:\工具\node.js\npm_cache
registry=http://registry.npmmirror.com
```

from:[简书](https://www.jianshu.com/p/9f1b5b347bd1)



新增系统变量 可以让npm模块保留单独位置

> NODE_PATH [npm_position_here]

免得npm安装包功能被覆盖 搞得又要重装node.js



而用户变量`path`则新增存放全局安装模块位置

> [npm_global_here]

这样就可以在cmd上任意一处调用global_module里的命令



但是你还是不能将资源文件 脱离开发/产品环境上(恼)

这只能用来跑命令 项目执行的时候 一个不能少



> 那是不是global就完全莫得用了？
>
> 如果项目缺失依赖 能直接在gloal上拖下来而不是直接从仓库里下还能有点用处吧？



最后来检查所有的配置是个很好的习惯

> npm config ls



****

#### 1、模块安装使用

刚好和webpack配合一起学罢 就当作是模块管理本身和模块使用



都知道npm里面分全局/ npm执行目录所在环境 /当前**应用**(-S)/**开发(-D)**环境

它们有毛区别



本地/npm执行目录所在环境

> （1）将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
> （2）可以通过 **require()** 来引入本地安装的包。

****

全局呢

一般是丢给对应的mod扩展用的 比如sublime text里的live-server

以及各种cli环境处理



那它可不可以单独直接当生产环境用？

```css
不能使用 package.json 里列举的依赖进行全局安装
```



所以 大概是不行的罢(npm里node_module浪费体积的一大原因)



****

那么-S/-D 目的性就很明了了 只针对当前你node命令下的项目

应用 -S(`--save`) 双栈

开发环境 -D(`--save-dev`) 仅开发用



比如**性能监视窗** 它就只适合在开发用

而**jQuery**就适合一直应用



而且不同的npm模块可能会对不同的环境有着不一样的**行为**

以webpack来讲

-D操作会使得webpack快速打包 快速生成main.js

-S操作则为使得webpack采用尽力压缩算法 节省空间



#### 2、依赖环境检查

好了 现在你知道单独项目的package.json是不能用global_module的 



这下你又把node_module搞崩了.jpg

不过好在package.json不会怎么被你操作炸



那我怎么知道现在的package.json缺了什么

> 当前项目位置执行	npm ls



然后 补齐就完事了

> 当前项目位置执行	npm install

这个行为会根据`package.json`里的 **dependencies/devdependencies**的记录安装

然后从仓库源里拖缺失的组件下来到本地`node_modules`里以实现补全



所以有人说package.json是最重要的东西(指体积上的重要占比) 这倒也没错

****



#### 3、package.json的解析

在此之前 我们先引入一张普普通通的一个项目中的`package.json`

```json
{
  "name": "webpage_test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "dev": "webpack serve",
    "app": "webpack --mode prodction"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.6.0"
  },
  "devDependencies": {
    "webpack": "^5.72.0",
    "webpack-cli": "^4.9.2",
    "webpack-dev-server": "^4.8.1"
  }
}

```



这里一般有用的关键字是

> **main**
>
> 它代表着此项目中整个package.json指向的入口 一般**默认**为index.js
>
> 如果后续没有其他引入 则**默认**处理会是这个名字
>
> 
>
> **script**
>
> 允许将该项目的其他模块命令写在一个触发字段上
>
> 便于一键npm run dev触发
>
> 要注意的是 一般来说各种命令都有其分支选项 选项既可以在npm cli环境下执行 也可以直接写入json环境下等待执行调用
>
> 
>
> **dependecies/devdependecies**
>
> 依赖说明 说明这个项目将会用到什么组件 其中划分**产品环境**和**开发环境**



**Tips ^和~的区别** [From 稀土掘金](https://juejin.cn/post/7009674584211324964)

```
"dependencies": {
    "vue": "~2.5.0",
    "es6-promise": "^2.0.0"
},

~符号(上限保留)
假设Vue后面更新新的版本，已经到2.6.0或者3.2.0以上
当我们重新安装项目依赖，只会匹配到2.5.x的最新版本，不会安装到2.6.0及以上

^符号(固定版本)
假设es6-promise更新3.0.0，当我们重新安装项目依赖，es6-promise始终是2.0.0
```

****



#### X、PNPM

先写结论



##### 环境配置

虽然与npm一样共用`.npmrc` 但内部极其多设置与npm不同(基本上只有仓库的设置被继承过去了)

不过好在用户变量的Path还是共享npm配置的

这样你默认安装的时候pnpm与npm都能跑已安装的命令



pnpm大致分为 **缓存存放区域** 以及 **全局模块存放区域**

听起来大致与npm里的`cache`和 `prefix`很相似



然而官方技术文档将其分为`store-dir`,`global-dir`

分别对应cache里的`index-v5` 与 正常全局`node_module`环境





好了 那为什么实际用的时候 pnpm效率要爆杀npm呢

npm:

> 以往npm在项目安装模块的时候
>
> 你一定疑惑 我明明只装了3-4个依赖 那搞什么这个项目中的node_module里有几十个文件夹？
>
> 那是因为不同模块也需要前置依赖 但是这些又不属于模块本身的东西 
>
> 那只能放到同一等级的node_module里了
>
> 结果就是乱糟糟的



pnpm:

> pnpm因为把模块**全部**赛进 global_dir 充当本体备份 
>
> 等真正要用的时候 在`store-dir`使用**符号链接** 从本体外分割出去一个**小副本链接** 再从**小副本链接**到项目
>
> 这样做的好处就是如果该项目某个什么文件改动了 
>
> pnpm也可以做到将很多模块共通的前置先链到一起 然后下载特殊的部分重新打包成文件夹
>
> 再把该模块链过去  这样不仅看着简洁 而且利用率又高





所以npm自带的cache是来干嘛的？	*我不到啊*

22.5.3 From 鸥鸽

npm的cache缓存的只有安装包

而 pnpm 是直接把安装过的链接过去



****



但是缺陷还是有

1. 缓存设计 注定项目会优先调用缓存而非仓库源

2. 符号链路设计也注定其模块不能全放在`global_dir`里

> 这会使得你的本地项目中无法查看到`global_dir`里安装的依赖 *难不成你想pnpm ls = pnpm ls -g?*
>
> (但是如果仅仅只是本地跑跑倒是无所谓)
>
> 这也会使得别人在下载你发布的package.json的时候发现依赖缺失的问题
>
> 所以如果命令行和本地都要用的话就得装两份

3. 有的模块如果安装完之后要联网下东西的话（例如连 GitHub），缓存不一定管用



欧鸽推荐: 命令用npm -g存放	其余本地使用pnpm存放

不管你的实际模块环境怎么样

至少得确保你的`package.json`依赖需求准确 要不然兼容性白搭

****



##### 排障

好了 因为你跟npm一样在乱搞pnpm的全局模块

而且pnpm不会像npm一样仅靠`package.json`搞定一切



因其符号链接的关系 

pnpm需求***符号链接目录***的真实性存在与***被链接目录的模块*** 真实性存在才可允许进行一些改动操作

典型例子就是你把`store_dir`给嘎了 然后你连`global_dir`中该模块的使用都搞不了 

所以 尽可能的不要不要 脱离pnpm环境下自行操作模块相关的文件夹(



*虽然因其缓存的关系 重建起来的代价远小于npm的管理模式(*
