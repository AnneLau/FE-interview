# 前端综合

## 前端优化

### 前端需要注意哪些SEO

1. 合理的title、description、keywords：搜索对着三项的权重逐个减小，title值强调重点即可，重要关键词出现不要超过2次，而且要靠前，不同页面title要有所不同；description把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面description有所不同；keywords列举出重要关键词即可
2. 语义化的HTML代码，符合W3C规范：语义化代码让搜索引擎容易理解网页
3. 重要内容HTML代码放在最前：搜索引擎抓取HTML顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用js输出：爬虫不会执行js获取内容
5. 少用iframe：搜索引擎不会抓取iframe中的内容
6. 非装饰性图片必须加alt
7. 提高网站速度：网站速度是搜索引擎排序的一个重要指标

### 什么是web语义化,有什么好处

web语义化是指通过HTML标记表示页面包含的信息，包含了HTML标签的语义化和css命名的语义化。
HTML标签的语义化是指：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构
css命名的语义化是指：为html标签添加有意义的class，id补充未表达的语义，如[Microformat](http://en.wikipedia.org/wiki/Microformats)通过添加符合规则的class描述信息
为什么需要语义化：

- 去掉样式后页面呈现清晰的结构
- 盲人使用读屏器更好地阅读
- 搜索引擎更好地理解页面，有利于收录
- 便团队项目的可持续运作及维护

### 如何进行网站性能优化

[雅虎Best Practices for Speeding Up Your Web Site](https://developer.yahoo.com/performance/rules.html)：

- content方面
    1. 减少HTTP请求：合并文件、CSS精灵、inline Image
    2. 减少DNS查询：DNS查询完成之前浏览器不能从这个主机下载任何任何文件。方法：DNS缓存、将资源分布到恰当数量的主机名，平衡并行下载和DNS查询
    3. 避免重定向：多余的中间访问
    4. 使Ajax可缓存
    5. 非必须组件延迟加载
    6. 未来所需组件预加载
    7. 减少DOM元素数量
    8. 将资源放到不同的域下：浏览器同时从一个域下载资源的数目有限，增加域可以提高并行下载量
    9. 减少iframe数量
    10. 不要404

- Server方面
    1. 使用CDN
    2. 添加Expires或者Cache-Control响应头
    3. 对组件使用Gzip压缩
    4. 配置ETag
    5. Flush Buffer Early
    6. Ajax使用GET进行请求
    7. 避免空src的img标签
- Cookie方面
    1. 减小cookie大小
    2. 引入资源的域名不要包含cookie
- css方面
    1. 将样式表放到页面顶部
    2. 不使用CSS表达式
    3. 使用<link>不使用@import
    4. 不使用IE的Filter
- Javascript方面
    1. 将脚本放到页面底部
    2. 将javascript和css从外部引入
    3. 压缩javascript和css
    4. 删除不需要的脚本
    5. 减少DOM访问
    6. 合理设计事件监听器
- 图片方面
    1. 优化图片：根据实际颜色需要选择色深、压缩
    2. 优化css精灵
    3. 不要在HTML中拉伸图片
    4. 保证favicon.ico小并且可缓存
- 移动方面
    1. 保证组件小于25k
    2. Pack Components into a Multipart Document

### 什么是渐进增强

渐进增强是指在web设计时强调可访问性、语义化HTML标签、外部样式表和脚本。保证所有人都能访问页面的基本内容和功能同时为高级浏览器和高带宽用户提供更好的用户体验。核心原则如下:

- 所有浏览器都必须能访问基本内容
- 所有浏览器都必须能使用基本功能
- 所有内容都包含在语义化标签中
- 通过外部CSS提供增强的布局
- 通过非侵入式、外部javascript提供增强功能
- end-user web browser preferences are respected


### 详解懒加载和预加载

以及最佳实践。


都已经到了 2018 年了，再来说 HTML5 的新特性，实在是够晚了，不过 Denis 说的好，即便再烂的文章，只要不误导，有总比没有强（不是原话，我润色了一下~）。

#### DNS 预解析缓存
众所周知，解析 DNS 是网站性能优化的比较重要的一部分，虽然加载时间不太长，但是很难压缩起来。特别是为了并发下载资源而使用多个 CDN 域名来加载资源的大型网站，更不可忽视，每加载资源之前都要先进行 CDN 域名的 DNS 解析转换。

如果采用 DNS 预加载，支持该功能的浏览器就会提前对该域名进行 DNS 解析并且缓存一下，而不会在需要请求资源再进行解析。而且这个功能应用实在是太简单：

```html
<link rel="dns-prefetch" href="http://cdn.staticfile.org/">
<link rel="dns-prefetch" href="//www.google-analytics.com">
```
具体之前草草翻译过一篇文章，有兴趣可以大体略过：使用预加载提速你的网站

#### H5 prefetch preload

资源预加载
资源预加载有很多办法，例如常见的图片预加载，有采用 CSS 的背景图片来预加载，大部分还是用 JS。目前 HTML5 提供了专门的资源预加载方法，有两个属性：prefetch（预读取）和 prerender（预渲染），分别被 Firefox 和 Chrome 浏览器支持。

prefetch 预读取
预读取就是很常见的资源预加载，当前页面加载完成之后，就会在后面偷偷的下载你指定的资源，一般是 JS 、CSS 和 图片 这类的，也可以下载页面：

```html
<link rel="prefetch" href="http://yujiangshui.com/" />
<link rel="prefetch" href="http://yujiangshui.com/wp-content/themes/jiangshui/images/avatar.jpg" />
<link rel="prefetch alternate stylesheet" href="mozspecific.css" />
```


prerender 预渲染
这个更厉害了，不仅偷偷的提前下载，而且还给你渲染出来，当用户点击链接的时候，立刻给你展现出来。
```html
<link rel="prerender" href="http://yujiangshui.com/" />
```
目前 Chrome 支持这个功能，详情请看：Web Developer’s Guide to Prerendering in Chrome。

搜素引擎其实是最需要这种预读取的功能的，因为他们非常确定用户下一步要打开的页面（搜索结果页面），所以当用户输入搜索内容的时候，就可以提前把搜索结果页面的资源提前加载，而且应用之后，效果十分明显。

目前兼容性是个缺点，貌似只有 Chrome 和 Firefox 支持，而且用的 rel 属性是不同的，如果你想同时兼容两个浏览器，可以写成下面这样：
```html
<link rel="prefetch prerender" href="http://yujiangshui.com" >
```
此外，当然为了安全没法跨域预加载资源，可能没法用 CDN 了。


以下来自[掘金](https://juejin.im/post/58e8acf10ce46300585a7a42)

像其他文章描述的那样，preload 是声明式的 fetch，可以强制浏览器请求资源，同时不阻塞文档 onload 事件。
Prefetch 提示浏览器这个资源将来可能需要，但是把决定是否和什么时间加载这个资源的决定权交给浏览器。



#### 使用js，css或者ajax等方式实现预加载

[文档参考这里](https://www.geekjc.com/post/58d94d0f16a3655650d6fafe)



使用css

```css
#preload-01 { background: url(http://qiniu.cllgeek.com/react02.png) no-repeat -9999px -9999px; }  
#preload-02 { background: url(http://qiniu.cllgeek.com/react03.png) no-repeat -9999px -9999px; }  
#preload-03 { background: url(http://qiniu.cllgeek.com/react04.png no-repeat -9999px -9999px; }

```



JS

```js
// better image preloading @ <a href="http://perishablepress.com/press/2009/12/28/3-ways-preload-images-css-javascript-ajax/">http://perishablepress.com/press/2009/12/28/3-ways-preload-images-css-javascript-ajax/</a>  
function preloader() {  
    if (document.getElementById) {  
        document.getElementById("preload-01").style.background = "url(http://qiniu.cllgeek.com/react02.png) no-repeat -9999px -9999px";  
        document.getElementById("preload-02").style.background = "url(http://qiniu.cllgeek.com/react03.png) no-repeat -9999px -9999px";  
        document.getElementById("preload-03").style.background = "url(http://qiniu.cllgeek.com/react04.png) no-repeat -9999px -9999px";  
    }  
}  
function addLoadEvent(func) {  
    var oldonload = window.onload;  
    if (typeof window.onload != 'function') {  
        window.onload = func;  
    } else {  
        window.onload = function() {  
            if (oldonload) {  
                oldonload();  
            }  
            func();  
        }  
    }  
}  
addLoadEvent(preloader);
//绑定到window.onload事件之后，这样可以避免预加载的东西阻塞了浏览器进程
```



ajax

```js
window.onload = function() {  
    setTimeout(function() {  
        // XHR to request a JS and a CSS  
        var xhr = new XMLHttpRequest();  
        xhr.open('GET', 'http://geekjc.com/preload.js');  
        xhr.send('');  
        xhr = new XMLHttpRequest();  
        xhr.open('GET', 'http://geekjc.com/preload.css');  
        xhr.send('');  
        // preload image  
        new Image().src = "http://geekjc.com/preload.png";  
    }, 1000);  
};
```



### 首屏秒开

转载自这里[移动 H5 首屏秒开优化方案探讨](http://blog.cnbang.net/tech/3477/)

firefox六个并发请求。

HTTP1.1下，chrome的并行下载数为6，同时是根据优先级来进行并行下载的。

#### 过程
为什么打开一个 H5 页面会有一长段白屏时间？因为它做了很多事情，大概是：

初始化 webview -> 请求页面 -> 下载数据 -> 解析HTML -> 请求 js/css 资源 -> dom 渲染 -> 解析 JS 执行 -> JS 请求数据 -> 解析渲染 -> 下载渲染图片

一些简单的页面可能没有 JS 请求数据 这一步，但大部分功能模块应该是有的，根据当前用户信息，JS 向后台请求相关数据再渲染，是常规开发方式。

一般页面在 dom 渲染后能显示雏形，在这之前用户看到的都是白屏，等到下载渲染图片后整个页面才完整显示，首屏秒开优化就是要减少这个过程的耗时。

#### 前端优化
上述打开一个页面的过程有很多优化点，包括前端和客户端，常规的前端和后端的性能优化在桌面时代已经有最佳实践，主要的是：

- 降低请求量：合并资源，减少 HTTP 请求数，minify / gzip 压缩，webP，lazyLoad。
- 加快请求速度：预解析DNS，减少域名数，并行加载，CDN 分发。
- 缓存：HTTP 协议缓存请求，离线缓存 manifest，离线数据缓存localStorage。
- ·渲染：JS/CSS优化，加载顺序，服务端渲染，pipeline。


其中对首屏启动速度影响最大的就是网络请求，所以优化的重点就是缓存，这里着重说一下前端对请求的缓存策略。我们再细分一下，分成 HTML 的缓存，JS/CSS/image 资源的缓存，以及 json 数据的缓存。

HTML 和 JS/CSS/image 资源都属于静态文件，HTTP 本身提供了缓存协议，浏览器实现了这些协议，可以做到静态文件的缓存，具体可以参考[这里](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=zh-cn)，总的来说，就是两种缓存：

1. 询问是否有更新：根据 If-Modified-Since / ETag 等协议向后端请求询问是否有更新，没有更新返回304，浏览器使用本地缓存。
2. 直接使用本地缓存：根据协议里的 Cache-Control / Expires 字段去确定多长时间内可以不去发请求询问更新，直接使用本地缓存。

前端能做的最大限度的缓存策略是：HTML 文件每次都向服务器询问是否有更新，JS/CSS/Image资源文件则不请求更新，直接使用本地缓存。那 JS/CSS 资源文件如何更新？常见做法是在在构建过程中给每个资源文件一个版本号或hash值，若资源文件有更新，版本号和 hash 值变化，这个资源请求的 URL 就变化了，同时对应的 HTML 页面更新，变成请求新的资源URL，资源也就更新了。

json 数据的缓存可以用 localStorage 缓存请求下来的数据，可以在首次显示时先用本地数据，再请求更新，这都由前端 JS 控制。

这些缓存策略可以实现 JS/CSS 等资源文件以及用户数据的缓存的全缓存，可以做到每次都直接使用本地缓存数据，不用等待网络请求。但 HTML 文件的缓存做不到，对于 HTML 文件，如果把 Expires / max-age 时间设长了，长时间只使用本地缓存，那更新就不及时，如果设短了，每次打开页面都要发网络请求询问是否有更新，再确定是否使用本地资源，一般前端在这里的策略是每次都请求，这在弱网情况下用户感受到的白屏时间仍然会很长。所以 HTML 文件的“缓存”和跟“更新”间存在矛盾。

#### 客户端优化

接着轮到客户端出场了，桌面时代受限于浏览器，H5 页面无法做更多的优化，现在 H5 页面是内嵌在客户端 APP 上，客户端有更多的权限，于是客户端上可以超出浏览器的范围，做更多的优化。



### HTML 缓存

先接着缓存说，在客户端有更自由的缓存策略，客户端可以拦截 H5 页面的所有请求，由自己管理缓存，针对上述 HTML 文件的“缓存”和“更新”之间的矛盾，我们可以用这样的策略解决：

1. 在客户端拦截请求，首次请求 HTML 文件后缓存数据，第二次不发请求，直接使用缓存数据。
2. 什么时候去请求更新？这个更新请求可以客户端自由控制策略，可以在使用本地缓存打开本地页面后再在后台发起请求询问更新缓存，下次打开时生效；也可以在 APP 启动时或某个时机在后台去发起请求预更新，提升用户访问最新代码的几率。

这样看起来已经比较完美了，HTML 文件在用客户端的策略缓存，其余资源和数据沿用上述前端的缓存方式，这样一个 H5 页面第二次访问从 HTML 到 JS/CSS/Image 资源，再到数据，都可以直接从本地读取，无需等待网络请求，同时又能保持尽可能的实时更新，解决了缓存问题，大大提升 H5 页面首屏启动速度。



#### 问题

上述方案似乎已完整解决缓存问题，但实际上还有很多问题：

1. **没有预加载：**第一次打开的体验很差，所有数据都要从网络请求。
2. **缓存不可控：**缓存的存取由系统 webview 控制，无法控制它的缓存逻辑，带来的问题包括： i. 清理逻辑不可控，缓存空间有限，可能缓存几张大图片后，重要的 HTML/JS/CSS 缓存就被清除了。 ii.磁盘 IO 无法控制，无法从磁盘预加载数据到内存。
3. **更新体验差：**后台 HTML/JS/CSS 更新时全量下载，数据量大，弱网下载耗时长。
4. **无法防劫持：**若 HTML 页面被运营商或其他第三方劫持，将长时间缓存劫持的页面。

这些问题在客户端上都是可以被解决的，只不过有点麻烦，简单描述下：

1. 可以配置一个预加载列表，在APP启动或某些时机时提前去请求，这个预加载列表需要包含所需 H5 模块的页面和资源，还需要考虑到一个H5模块有多个页面的情况，这个列表可能会很大，也需要工具生成和管理这个预加载列表。
2. 客户端可以接管所有请求的缓存，不走 webview 默认缓存逻辑，自行实现缓存机制，可以分缓存优先级以及缓存预加载。
3. 可以针对每个 HTML 和资源文件做增量更新，只是实现和管理起来比较麻烦。
4. 在客户端使用 httpdns + https 防劫持。

上面的解决方案实现起来十分繁琐，原因就是各个 HTML 和资源文件很多很分散，管理困难，有个较好的方案可以解决这些问题，就是离线包。

#### 离线包

既然很多问题都是文件分散管理困难引起，而我们这里的使用场景是使用 H5 开发功能模块，那很容易想到把一个个功能模块的所有相关页面和资源打包下发，这个压缩包可以称为功能模块的离线包。使用离线包的方案，可以相对较简单地解决上述几个问题：

1. 可以预先下载整个离线包，只需要按业务模块配置，不需要按文件配置，离线包包含业务模块相关的所有页面，可以一次性预加载。
2. 离线包核心文件和页面动态的图片资源文件缓存分离，可以更方便地管理缓存，离线包也可以整体提前加载进内存，减少磁盘 IO 耗时。
3. 离线包可以很方便地根据版本做增量更新。
4. 离线包以压缩包的方式下发，同时会经过加密和校验，运营商和第三方无法对其劫持篡改。

到这里，对于使用 H5 开发功能模块，离线包是一个挺不错的方案了，简单复述一下离线包的方案：

1. 后端使用构建工具把同一个业务模块相关的页面和资源打包成一个文件，同时对文件加密/签名。
2. 客户端根据配置表，在自定义时机去把离线包拉下来，做解压/解密/校验等工作。
3. 根据配置表，打开某个业务时转接到打开离线包的入口页面。
4. 拦截网络请求，对于离线包已经有的文件，直接读取离线包数据返回，否则走 HTTP 协议缓存逻辑。
5. 离线包更新时，根据版本号后台下发两个版本间的 diff 数据，客户端合并，增量更新。

#### 更多优化

离线包方案在缓存上已经做得差不多了，还可以再配上一些细节优化：

##### 公共资源包

每个包都会使用相同的 JS 框架和 CSS 全局样式，这些资源重复在每一个离线包出现太浪费，可以做一个公共资源包提供这些全局文件。

##### 预加载 webview

无论是 iOS 还是 Android，本地 webview 初始化都要不少时间，可以预先初始化好 webview。这里分两种预加载：

1. 首次预加载：在一个进程内首次初始化 webview 与第二次初始化不同，首次会比第二次慢很多。原因预计是 webview 首次初始化后，即使 webview 已经释放，但一些多 webview 共用的全局服务或资源对象仍没有释放，第二次初始化时不需要再生成这些对象从而变快。我们可以在 APP 启动时预先初始化一个 webview 然后释放，这样等用户真正走到 H5 模块去加载 webview时就变快了。
2. webview 池：可以用两个或多个 webview 重复使用，而不是每次打开 H5 都新建 webview。不过这种方式要解决页面跳转时清空上一个页面，另外若一个 H5 页面上 JS 出现内存泄漏，就影响到其他页面，在 APP 运行期间都无法释放了。

可以参考美团点评的这篇[文章](https://tech.meituan.com/WebViewPerf.html)。

##### 预加载数据

理想情况下离线包的方案第一次打开时所有 HTML/JS/CSS 都使用本地缓存，无需等待网络请求，但页面上的用户数据还是需要实时拉，这里可以做个优化，在 webview 初始化的同时并行去请求数据，webview 初始化是需要一些时间的，这段时间没有任何网络请求，在这个时机并行请求可以节省不少时间。

具体实现上，首先可以在配置表注明某个离线包需要预加载的 URL，客户端在 webview 初始化同时发起请求，请求由一个管理器管理，请求完成时缓存结果，然后 webview 在初始化完毕后开始请求刚才预加载的 URL，客户端拦截到请求，转接到刚才提到的请求管理器，若预加载已完成就直接返回内容，若未完成则等待。

##### Fallback

如果用户访问某个离线包模块时，这个离线包还没有下载，或配置表检测到已有新版本但本地是旧版本的情况如何处理？几种方案：

1. 简单的方案是如果本地离线包没有或不是最新，就同步阻塞等待下载最新离线包。这种用户打开的体验更差了，因为离线包体积相对较大。
2. 也可以是如果本地有旧包，用户本次就直接使用旧包，如果没有再同步阻塞等待，这种会导致更新不及时，无法确保用户使用最新版本。
3. 还可以对离线包做一个线上版本，离线包里的文件在服务端有一一对应的访问地址，在本地没有离线包时，直接访问对应的线上地址，跟传统打开一个在线页面一样，这种体验相对等待下载整个离线包较好，也能保证用户访问到最新。

第三种 Fallback 的方式还带来兜底的好处，在一些意外情况离线包出错的时候可以直接访问线上版本，功能不受影响，此外像公共资源包更新不及时导致版本没有对应上时也可以直接访问线上版本，是个不错的兜底方案。

上述几种方案策略也可以混着使用，看业务需求。

##### 使用客户端接口

网路和存储接口如果使用 webkit 的 ajax 和 localStorage 会有不少限制，难以优化，可以在客户端提供这些接口给 JS，客户端可以在网络请求上做像 DNS 预解析/IP直连/长连接/并行请求等更细致的优化，存储也使用客户端接口也能做读写并发/用户隔离等针对性优化。

##### 服务端渲染

早期 web 页面里，JS 只是负责交互，所有内容都是直接在 HTML 里，到现代 H5 页面，很多内容已经依赖 JS 逻辑去决定渲染什么，例如等待 JS 请求 JSON 数据，再拼接成 HTML 生成 DOM 渲染到页面上，于是页面的渲染展现就要等待这一整个过程，这里有一个耗时，减少这里的耗时也是白屏优化的范围之内。

优化方法可以是人为减少 JS 渲染逻辑，也可以是更彻底地，回归到原始，所有内容都由服务端返回的 HTML 决定，无需等待 JS 逻辑，称之为服务端渲染。是否做这种优化视业务情况而定，毕竟这种会带来开发模式变化/流量增大/服务端开销增大这些负面影响。手Q的部分页面就是使用服务端渲染的方式，称为动态直出，见[文章](https://mp.weixin.qq.com/s/evzDnTsHrAr2b9jcevwBzA)。

#### 最后

从**前端优化**，到**客户端缓存**，到**离线包**，到更多的细节优化，做到上述这些点，H5 页面在启动上差不多可以媲美原生的体验了。

总结起来，大体优化思路就是：**缓存/预加载/并行**，缓存一切网络请求，尽量在用户打开之前就加载好所有内容，能并行做的事不串行做。这里有些优化手段需要做好一整套工具和流程支持，需要跟开发效率权衡，视实际需求优化。

另外上述讨论的是针对功能模块类的 H5 页面秒开的优化方案，客户端 APP 上除了功能模块，其他一些像营销活动/外部接入的 H5 页面可能有些优化点就不适用，还需要视实际情况和需求而定。另外微信小程序就是属于功能模块的类别，差不多是这个套路。

这里讨论了 H5 页面首屏启动时间的优化，上述优化过后，基本上耗时只剩 webview 本身的启动/渲染机制问题了，这个问题跟后续的响应流畅度的问题一起属于另一个优化范围，就是类 RN / Weex 这样的方案，有机会再探讨。

#### HTTPDNS

[HttpDNS 服务详解](http://www.ttlsa.com/web/httpdns-detailed-service/)



### PC端首屏优化

[看这篇博文](https://www.cnblogs.com/jingh/p/6531105.html)

域名收敛

1. 在移动网络环境下，减少非必要 DNS 请求，将相关域名收敛成一个，可以尝到缓存的红利，进而可以减少打开页面时间
2. 移动端减少 DNS 解析时间有两种方式：
   - 减少 DNS 请求
   - 缩短 DNS 解析路径

从上面的各种网络环境下 DNS 解析时间对比，减少 DNS 请求是我们做域名收敛的主要原因。HttpDNS 的诞生不仅可以合并请求，缩短 DNS 解析路径，还有防止运营商劫持等功效。

### 雅虎35条军规

[雅虎三十五条军规](https://www.jianshu.com/p/3d77c3d3cc8f)

