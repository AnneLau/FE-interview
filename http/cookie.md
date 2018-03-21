# cookie
[看这里：HTTP cookies 详解](https://www.kancloud.cn/kancloud/http-cookies-explained/48332)
在
```
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

### 创建cookie
```
Set-Cookie: value[; expires=date][; domain=domain][; path=path][; secure]
```
```
Set-Cookie: name=Nicholas; HttpOnly
```
表示不能使用js操作cookie

### cookie的编码

对于 cookie 的值进行编码一直都存在一些困惑。普遍认为 cookie 的值必须经过 URL 编码，但其实这是一个谬论，尽管通常都这么做。原始规范中明确指出只有三个字符必须进行编码：分号、逗号和空格，规范中还提到可以进行 URL 编码，但并不是必须，在 RFC 中没有提及任何编码。然而，几乎所有的实现都对 cookie 的值进行了一系列的 URL 编码。对于 name=value 格式，通常会对 name 和 value 分别进行编码，而不对等号 = 进行编码操作。

### 总结  cookie里面也有expires

| request | response                                                     |
| ------- | ------------------------------------------------------------ |
|         | Set-cookie:``` Set-Cookie: value[; expires=date][; domain=domain][; path=path][; secure]httponly``` |
|         |                                                              |
|         |                                                              |

### 对比cache-control

强缓存

使用cache-control和expire来共同决定

![20180320152155166235116.jpg](http://osmisz4zw.bkt.clouddn.com/20180320152155166235116.jpg)



response header中有cache-control

Expries是http1.0提出的，表示失效时间（GMT格式），只有在这个时间之前的请求才可以用强缓存。

第一次向服务器请求一个资源后，浏览器不仅会把资源保存起来，也会保存Reponse Headers，包括其中的Expires。第二次发请求时先去缓存中寻找这个资源，取到Expires，与当前的请求时间做对比，如果在Expires之前，则从缓存中取，否则重新向服务器请求，Expires在重新加载时被更新。

cache-control可以有多个值：

cache-control: max-age=111000  -->表示自第一次收到响应后的111000ms以后可以用缓存

cache-control: no-cache   -->禁止使用强缓存

cache-control: no-store  -->禁止使用缓存，每次都要去服务器重新请求

cache-control: private  -->只允许被终端用户的浏览器端缓存

cache-control: public -->可以被所有用户缓存，保存终端用户和CDN等代理服务器

由于Expries是个绝对时间，由于各个客户端之间有时差就会导致缓存不一致的问题，所以http 1.1提出了cache-control，是个相对时间，在第二次发请求时取到缓存中的max-age和第一次的请求时间计算出资源过期时间，与当前的请求时间对比决定是否使用缓存。





协商缓存



二、协商缓存 

有两组headers值：Last-Modified / If-Modified-Since 和 Etag / If-None-Match，后者优先级高于前者。

![20180320152155183299743.png](http://osmisz4zw.bkt.clouddn.com/20180320152155183299743.png)



| request         | response    |
| --------------- | ----------- |
| If-modify-since | last-modify |
| If-none-match   | E-tag       |
|                 |             |

\1. Last-Modified / If-Modified-Since

第一次请求时返回的Response Headers中用Last-Modified表示请求的资源在服务器上最新的修改时间，第二次请求时在Request Headers中用If-Modified-Since带上这个值发到服务器，服务器对比这个值和这个资源市价上的最新修改时间决定是否直接返回403还是返回资源。当返回403时，表示资源没有更新，所以浏览器缓存中的Last-Modified也就不用更新了。

但是Last-Modified的问题在于有时服务器上资源其实有变化，但是最后修改时间却没有变化，所以有了Etag / If-None-Match来管理协商缓



2. Etag / If-None-Match

Etag是服务器根据被请求资源生成的一个唯一标识字符串，只要资源发生变化，Etag就会变，跟资源的最新修改时间没有关系，能弥补Last-Modified的不足。与Last-Modified类似，第二次请求时请求头会带上If-None-Match标识的Etag值，区别是由于服务器每次会根据资源重新生成一个Etag，再拿它跟浏览器传过来的Etag对比，如果一致则返回403，所以由于每次Etag都会重新生成，所以浏览器缓存中的Etag也必须每次都更新。

一般Last-Modified和Etag是同时启用的，但是对于分布式系统多同机器间文件的Last-Modified必须一致，以免因为负载均衡到不同机器导致比对不一致，分布式系统尽量关闭Etag,因为每台机器生成的Etag也不一致。

另外当使用**F5刷新时会跳过强缓存**，当强制刷新时，强缓存和协商缓存都会跳过。其他操作行为如前进后退，地址栏回车都会按正常流程走。

浏览器默认都会缓存图片，js，css等静态文件，也可以通过待会再响应头中设置是否要启用缓存，或是通过服务器专门的配置文件统一设置Expires, Cache-control等。



session依赖于cookie

### 覆盖式发布

使用版本号


