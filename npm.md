与其说是笔记 不如说是折腾日记 



**以后抽时间再来格式化**



##### 0、环境配置

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



##### 1、模块安装使用

刚好和webpack配合一起学罢 就当作是模块管理本身和模块使用



都知道npm里面分全局/ npm执行目录所在环境 /当前**应用**(-S)/**开发(-D)**环境

它们有毛区别



本地/npm执行目录所在环境

> （1）将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
> （2）可以通过 **require()** 来引入本地安装的包。

****

全局呢

一般是丢给对应的mod扩展用的 比如sublime text里的live-server



那它可不可以单独直接当生产环境用？

```css
不能使用 package.json 里列举的依赖进行全局安装
```



所以 大概是不行的罢(node_module浪费体积的一大原因)



****

那么-S/-D 目的性就很明了了 只针对当前你node命令下的项目

应用 -S(`--save`) 双栈

开发环境 -D(`--save-dev`) 仅开发用



比如性能监视窗 它就只适合在开发用

而jQuery就适合一直应用





