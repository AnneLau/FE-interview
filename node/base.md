# node
## node面试题

[node有关面试题](https://github.com/jimuyouyou/node-interview-questions)

[node环境和浏览器的区别](http://www.cnblogs.com/webARM/p/5004595.html)

### node环境和浏览器的区别

一、全局环境下this的指向

　　在node中this指向global而在浏览器中this指向window，这就是为什么underscore中一上来就定义了一 root；

```
var root = typeof self == 'object' && self.self === self && self ||
2             typeof global == 'object' && global.global === global && global ||
3             this;
```
　而且在浏览器中的window下封装了不少的API 比如 alert 、document、location、history 等等还有很多。我门就不能在node环境中xxx();或window.xxx();了。因为这些API是浏览器级别的封装，存javascript中是没有的。当然node中也提供了不少node特有的API。

```
(function(){
    var root=this,
        isBrowserSide=false;
    if(typeof window !=="undefined" && root===window){
        isBrowserSide=true;
    }
}).call(this);
```

二、js引擎

在浏览器中不同的浏览器厂商提供了不同的浏览器内核，浏览器依赖这些内核解释折我们编写的js。但是考虑到不同内核的少量差异，我们需要对应兼容性好在有一些优秀的库帮助我们处理这个问题比如jquery、underscore等等。

　　nodejs是基于Chrome's JavaScript runtime，也就是说，实际上它是对GoogleV8引擎（应用于Google Chrome浏览器)进行了封装。V8引 擎执行Javascript的速度非常快，性能非常好。

      NodeJS并不是提供简单的封装，然后提供API调用，如果是这样的话那么它就不会有现在这么火了。Node对一些特殊用例进行了优化，提供了替代的API，使得V8在非浏览器环境下运行得更好。例如，在服务器环境中，处理二进制数据通常是必不可少的，但Javascript对此支持不足，因此，V8.Node增加了Buffer类，方便并且高效地 处理二进制数据。因此，Node不仅仅简单的使用了V8,还对其进行了优化，使其在各环境下更加给力。

　　js引擎都固定了，还对应神马兼容性。
　　
三、DOM操作

　　浏览器中的js大多数情况下是在直接或间接（一些虚拟DOM的库和框架）的操作DOM。因为浏览器中的代码主要是在表现层工作。但是node是一门服务端技术。没有一个前台页面，所以我门不会再node中操作DOM。

四、I/O读写

　　与浏览器不同，我们需要像其他服务端技术一样读写文件，nodejs提供了比较方便的组件。而浏览器（确保兼容性的）想在页面中直接打开一个本地的图片就麻烦了好多（别和我说这还不简单，相对路径。。。。。。试试就知道了要么找个库要么二进制流，要么上传上去有了网络地址在显示。不然人家为什么要搞一个js库呢），而这一切node都用一个组件搞定了。

五、模块加载

　　javascript有个特点，就是原生没提供包引用的API一次性把要加载的东西全执行一遍，这里就要看各位闭包的功力了。所用东西都在一起，没有分而治之，搞的特别没有逻辑性和复用性。如果页面简单或网站当然我们可以通过一些AMD、CMD的js库（比如requireJS 和 seaJS）搞定事实上很多大型网站都是这么干的。

　　在nodeJS中提供了CMD的模块加载的API，如果你用过seaJS，那么应该上手很快。

　　node还提供了npm 这种包管理工具，能更有效方便的管理我们饮用的库

　　当然浏览器这边ES6也有这方面的补充，相信未来会更好。。。



### 基本模块：
fs，stream，http，crypto
D5和SHA1 Hmac AES

