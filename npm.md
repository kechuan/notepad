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

当前项目位置执行

> npm ls





然后 补齐就完事了

> npm install

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
 // "type":"module",
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
>
> 
>
> **type**
>
> 模块类型说明
>
> 默认为commonJS的require导入("type":"commonjs")
>
> 而当type的值设置为module的时候就为ES6的import导入



**script的执行顺序**

不过当node_modules下的.bin文件夹下存在对应命名的cmd/linux.sh/ps1/[dirname]时

script会优先处理.bin下的指向文件

1.查找规则是先从当前项目的node_modlue /bin去找,

2.找不到去全局的node_module/bin 去找

3.再找不到 去环境变量去找

****



##### CommonJS与ESM的兼容性管理

无论如何，正常情况下，一个 package 只能支持一种模块它要么是 ESM 要么是 CJS。

> type:"module/commonJS"



但是你看看别人的项目

为什么它们的build.js里面怎么就可以做到require和import一起用啊？

而且别人还有 `.cjs` `.mjs` 那又是什么？

****



先解释`.cjs`与`.mjs`

顾名思义就是专门给`commonJS`与`ES module`引入做的版本

这个道理就和一个mod的作者

它要考虑支援的版本有 旧版本玩家 以及 新版本玩家

而commonJS前文也提到过是一个古早时候没ES module标准前提出的东西

虽然一度极其盛行 但是终究还是因为有官方自带的东西 那趋势就是转向用官方的



有些作者可能还会留一个 `.cjs`给旧版本客户端专门适配

但是现在我已经发现有作者(execa,fullscreen)直接在package.json 直接声明

> "type":"module"



所以不管怎么说 自己搞项目的时候 也尽量往ESM靠拢罢

*用ejs不代表node不会支持cjs 因为有时还是需要require的特性(运行时载入)*

****



但那也是以后才能考虑的事情 现在我只是个只会调用别人库的屑

我想知道怎么在一个package里同时引入`cjs`和`mjs`



网上给出的方案是 用原生node环境去支持cjs的引入

又用npm引入的包 例如webpack/rollup来支持mjs的引入

听起来感觉蛮抽象的



不过在此之前 还是先统一用ejs构建架构罢



[ESM/CJS共存](https://www.jianshu.com/p/0ad1e1a8c518)

****



##### **版本号**

npm仓库里允许作者提供类似测试版-开发版等源

一般找不到你想指定要的版本仓库就会返回给你**各种版本**的最新版



例如:

> Other releases are:
>   * bridge: 7.0.0-bridge.0
>   * lerna-temp: 6.26.3
>   * next: 7.0.0-beta.3
>   * old: 5.8.38



而调用则为

> npm i -D babel-core@next

则为使用next源的7.0.0-beta.3版本



如要查看所有版本则为

> npm view [module_name] versions

但我建议你还是直接去[npm.js](https://www.npmjs.com)上看 可比这个命令管用



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



#### 4、node环境变量指令运用

除开熟悉的path变量(这个也是属于在node环境下的)



##### **读取/打开文件的用法**

在静态的网页端就已经有`require`/`import`了

那为什么还需要更上一级(node)环境的读取文件？



那可不废话吗

在网页端上都已经是编译成静态资源了

怎么和node环境下的动态库外加一堆插件来比啊(恼

除非**electron**那种node和浏览器绑定的



所以node环境里有自带的文件打开方式

###### fs

> const fs = require('fs');	commonJS引入
>
> import Fs from 'fs'



fs里自带方法`readFile()`



`fs.readFile(url,[codec],function(err,data){}`



> **err**代表读取不到文件执行的回调函数
>
> **data**则为读取成功执行的回调函数
>
> **codec**代表以什么编码方式打开文件 如果缺省则默认为Buffer HEX码
>
> 想保持hex码打开又要以文本显示就需要手动.toString()



fs提供了**同步读取**以及**异步读取**的方式

> 默认readFile()就是异步读取
>
> 同步读取:readFileSync()



以一个简单示例

```js
import fs from 'fs' //ES6

fs.readFile('1.txt','utf8',function(err,data){console.log(data)})
fs.readFile('2.txt','utf8',function(err,data){console.log(data)})
fs.readFile('3.txt','utf8',function(err,data){console.log(data)})

const data1 = fs.readFileSync('1.txt','utf8');
console.log("同步读取: " + data1);
const data2 = fs.readFileSync('2.txt','utf8');
console.log("同步读取: " + data2);
const data3 = fs.readFileSync('3.txt','utf8');
console.log("同步读取: " + data3);


<<同步读取: 1
<<同步读取: 2
<<同步读取: 3
<<1
<<3
<<2
```



****

以及相似语法的`open()`

打开文件

`fs.open([url],flags,callback(err,fd))`



flags是什么？

还C语言只学文件指针皮毛的债

> r/w 通俗易懂
>
> \+ 意味着扩展补全
>
> x 路径冲突检测
>
> a 追加(光标直接在文件尾)模式



```js
const fs = require("fs");	//commonJS
fs.open('artical.txt',"r+",function(err,fd){
   if (err) {
       return console.error(err);
   }

   if(fd){
      console.log(fd)
   }
})
```



前端总得需要读入图片/文字然后加以处理 最后返回

文字还好 如果不是太长直接切成**字符串**+**队列**的形式存储并处理

然而**图片**这种东西你不可能var一个变量给别人填进textarea然后再返回的 

何况真的仅仅是文字/图片的话 前端的FileReader就完全足够了(



*[!]待补充 open的具体真实意义*

****



###### then-fs

那么既然已经有看起来完善的**fs** 为什么会需要**then-fs**?

因为上面说了那么多东西 它都是仅属于**node**环境里的东西

而**then-fs**却有专门有面向静态网页的`Promise`方式



还有一点

上文有提到过node默认的fs方式 在**异步情况**下会出现读入文件乱序的问题

这个现象的本质原因是多种线程的指派问题	(狗抢狗粮.jpg)

所以你应该需要指定一个线程后锁定只在该线程执行



而如果你用`readFileSync`同步方式明显就会阻塞主线程运行



于是乎 then-fs带着**.then()**方法来力



****

usage:

> npm i then-fs



> import thenFs from 'then-fs'



它在使用与fs不同的地方是

它把原本附带的回调函数集成进以原生js里的`.then()`里而非fs一样一次性写完

原本的data变成**自定义变量**

`thenfs.readFile(url,[codec]).then(r1 => {sucss_here},err => {err_here})`



Buffer(HEX数据)

不过thenfs就不会帮你把读取的数据默认导出为字符串出去

而是需要手动`.toString()`



否则会显示

> <Buffer XX XX XX>



不过`thenFs`和**promise**有什么鬼关系

实际上then方法就是等于返回了一个新的promise实例对象(



于是乎 你可以使用以前写过的**链式调用**来解决回调地狱/非顺序读取的问题

```js
thenFs.readFile('1.txt','utf8')
    .then(r1 => {
       console.log(r1)
       return thenFs.readFile('2.txt','utf8')
    })

	.then(r2 => {
       console.log(r2)
       return thenFs.readFile('3.txt','utf8')
    })

	.then(r3 => {
       console.log(r3)
    })
```

这样就能在异步(其他线程)上进行相对于其本身的同步操作而不会指派给其他线程执行了



其中**then**充当了原本return的返回*主页面作用*以及链接代码的作用

说实话 比原本原生js 链式调用更格式化一点(



希望能在以后的vue学习上用得到(



你说try&catch？

直接console.log()+保存刷新可比手动套一层试错快得多的多



process.env





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

这两个都需要在`.npmrc`定义了路径才能实现完全的搬移



****

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



##### **工作空间**

特别指代`monorepo`这一类对于需求工作空间的东西

pnpm给出设立`pnpm-workspace.yaml`配置文件来控制工作区

```json
packages:
  # all packages in subdirs of packages/ and components/
  - 'packages/**'
  - 'components/**'
  # exclude packages that are inside test directories
  - '!**/test/**'
```

*似乎大家都把子包叫做 packages*



上面就简单的把这个项目根目录文件下的`packages`与`components`文件夹设为子包

但是仅仅设立了工作空间还不够

对于其子包的模块关系还没有被声明建立

而工作空间里pnpm分为了**全局依赖**以及**局部依赖**



**全局**简单易懂 就是所有子包都能够享受

> pnpm i typescript -w/-r

*`-w`就是把依赖安装到根目录的`node_modules` 其实就是等于整个项目里的-g*

当然也可以把它安装在所有 packages 中，使用 `-r` 代替 `-w`



而**局部依赖**当然就是针对单个子包安装对应的依赖

你可以直接cd进对应的子目录直接

> pnpm i typescript



不过pnpm提供了`filter`在安装时给你挑选

[pnpm教程-工作空间](https://pnpm.io/zh/workspaces) [工作空间](https://www.kancloud.cn/chandler/web_technology/2625185#workspace_24)

例如把`packages`下的`@test/utils`装入`packages/web`下 `package.json`的`name`为 `@test/web`包中。需要执行：

```
pnpm i [package] -F [projectname]/[filename]
```

使用 `--filter/-F` 后面接子 package 的 name 表示只把安装的新包装入这个`package`中。



注:

> 当你把项目设置成有工作空间的时候 无法再通过简单的 pnpm i ??? 安装 
>
> 必须指向-w(根目录) 以及局部的项目



而在总项目上的脚本 你可以这样设置

```json
"scripts": {
    "dev:app1": "pnpm start --filter @vue/reactivity",
    "dev:app2": "pnpm start --filter @test/shared"
},
```



****

##### **节流**

这在npm上是完全不敢想的

除了用符号链接重复使用之外

pnpm还有移除掉在内缓存完全在符号链接上没有**被引用**的包

*未引用的包是系统上的任何项目中都未使用的包*

> pnpm store prune



##### 项目移除

> pnpm uni rm -r *

移除项目所有的包

> pnpm unlink -r *

解除项目所有文件的联系

> pnpm prune

最后更新本地的仓库链接状况 以实现完全删除



切记！与包一样 不要自己手动删除！



****

##### 排障

好了 因为你跟npm一样在乱搞pnpm的全局模块 把环境给搞炸了

而且pnpm不会像npm一样仅靠`package.json`搞定一切



因其符号链接的关系 

pnpm需求***符号链接目录***的真实性存在与***被链接目录的模块*** 真实性存在才可允许进行一些改动操作

典型例子就是你把`store_dir`给嘎了 然后你连`global_dir`中该模块的使用都搞不了 

所以 尽可能的不要不要 脱离pnpm环境下自行操作模块相关的文件夹(



*虽然因其缓存的关系 重建起来的代价远小于npm的管理模式(*



#### Y、Vite

可以理解为npm环境下内置的且似乎是专门面向**Vue**的包管理入口(`.sh`)

介绍:

- 一个开发服务器，它基于 [原生 ES 模块](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) 提供了 [丰富的内建功能](https://vitejs.cn/guide/features.html)，如速度快到惊人的 [模块热更新（HMR）](https://vitejs.cn/guide/features.html#hot-module-replacement)。
- 一套构建指令，它同样使用 [Rollup](https://rollupjs.org/) 打包你的代码，并且它是预配置的，可输出用于生产环境的高度优化过的静态资源。

npm:

> npm init vite

pnpm:

> pnpm create vite



> 在初始化vite完毕之后
>
> 打开`node_modules`的.vite发现已经内置好typescript,vue/vue-tsc等
>
> vue环境下基本的组件了。



##### Vite目录

在初始化后的根目录下的src里存放着

assets层级静态资源

component组件

以及入口main.ts和基础的`App.Vue`



index.html则单独存放至根目录下作为总入口



配置

`vite.config.ts`

当前默认生成的配置文件是这样的:

```tsx
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()]
})

```

*[!]*Vue文件刷新时无法触发HMR



实际上没有经过任何的配置(

我还蛮奇怪官方是怎么说有HMR特点的 结果初始化的配置文件连个入口都不给人看

光甩个config链接 而且这点和webpack的中文文档一样**中 文 翻 译 又 是 打 不 开**

> 两个域名都不一致 
>
> https://www.vitejs.net/ | https://cn.vitejs.dev/



#### Z、模块推荐

webpack那边有模块推荐

那么这里应该也要有!

这里都是教程里面基本没有的东西

算是个扩展吧 逛别人项目大部分应该能看到这些新玩意



ultra-run
