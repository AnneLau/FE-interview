# 模块
## 模块化

### AMD CMD CommonJS


#### 1. CommonJS

CommonJS是一种思想，它的终极目标是使应用程序开发者根据CommonJS API编写的JavaScript应用可以在不同的JavaScript解析器和HOST环境上运行。目前，有四大平台支持CommonJS API：Rhino、Spidermonkey、v8、JavaScriptCore。

在兼容CommonJS的系统中，你可以使用JavaScript开发以下程序：
(1).服务器端JavaScript应用程序
(2).命令行工具
(3).图形界面应用程序
(4).混合应用程序（如，Titanium或Adobe AIR）

2009年，美国程序员Ryan Dahl创造了node.js项目，将javascript语言用于服务器端编程。这标志"Javascript模块化编程"正式诞生。因为老实说，在浏览器环境下，没有模块也不是特别大的问题，毕竟网页程序的复杂性有限；但是在服务器端，一定要有模块，与操作系统和其他应用程序互动，否则根本没法编程。NodeJS是CommonJS规范的实现，webpack 也是以CommonJS的形式来书写。

#### 1.1 原理

浏览器不兼容CommonJS的根本原因，在于缺少四个Node.js环境的变量。

module
exports
require
global
只要能够提供这四个变量，浏览器就能加载 CommonJS 模块。

下面是一个简单的示例。



#### 1.2 Browserify的实现

知道了原理，就能做出工具了。Browserify 是目前最常用的 CommonJS 格式转换的工具。
请看一个例子，main.js 模块加载 foo.js 模块。

#### 2. AMD
由于require是同步的，会导致js的解析会等到网络加载完模块以后再进行，会导致浏览器假死。

AMD是"Asynchronous Module Definition"的缩写，就是异步模块定义。采用回调的模式来完成异步操作。

MD比较适合浏览器环境。目前，主要有两个Javascript库实现了AMD规范：require.js和curl.js。

RequireJS就是实现了AMD规范的呢。

#### 3. CMD
大名远扬的玉伯写了seajs，就是遵循他提出的CMD规范，与AMD蛮相近的，不过用起来感觉更加方便些，最重要的是中文版，应有尽有：seajs官方doc

虽然CMD(通用模块定义)与AMD(异步模块定义)蛮像的，但区别还是挺明显的，官方非官方都有阐述和理解，我觉得吧，说的都挺好：

总结：

```js
/* AMD是RequireJS对模块化的定义
 * CMD是seaJS对模块化的定义
 * CommonJS是Node对模块化的规范
 **/
/* AMD 依赖关系前置 */
define(['./a', './b'], function (a, b) {
    a.something();
    b.something();
})
/* CMD 按需加载，依赖就近 */
define(function (require, exports, module) {
    var a = require('./a');
    a.something();
    var b = require('./b');
    b.something();
})
```



