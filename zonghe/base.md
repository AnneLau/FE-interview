# 前端综合

## 综合

### web开发中会话跟踪的方法有哪些

1. cookie
2. session
3. url重写
4. 隐藏input
5. ip地址



### 哪些操作会造成内存泄漏？
使用 `process.memoryUsage`

ES6 考虑到了这一点，推出了两种新的数据结构：WeakSet 和 WeakMap。它们对于值的引用都是不计入垃圾回收机制的，所以名字里面才会有一个"Weak"，表示这是弱引用。

```js
const wm = new WeakMap();
const element = document.getElementById('example');
wm.set(element, 'some information');
wm.get(element) // "some information"
```
JavaScript 内存管理

JavaScript 是一种垃圾回收语言。垃圾回收语言通过周期性地检查先前分配的内存是否可达，帮助开发者管理内存。换言之，垃圾回收语言减轻了“内存仍可用”及“内存仍可达”的问题。两者的区别是微妙而重要的：仅有开发者了解哪些内存在将来仍会使用，而不可达内存通过算法确定和标记，适时被操作系统回收。

1：意外的全局变量
JavaScript 处理未定义变量的方式比较宽松：未定义的变量会在全局对象创建一个新变量。在浏览器中，全局对象是 window 。
```
function foo(arg) {
    bar = "this is a hidden global variable";
}
```

2. 被遗忘的计时器或回调函数

```javascript
var someResource = getData();
setInterval(function() {
    var node = document.getElementById('Node');
    if(node) {
        // 处理 node 和 someResource
        node.innerHTML = JSON.stringify(someResource));
    }
}, 1000);
```

3. 脱离 DOM 的引用

有时，保存 DOM 节点内部数据结构很有用。假如你想快速更新表格的几行内容，把每一行 DOM 存成字典（JSON 键值对）或者数组很有意义。此时，同样的 DOM 元素存在两个引用：一个在 DOM 树中，另一个在字典中。将来你决定删除这些行时，需要把两个引用都清除。

```js
var elements = {
    button: document.getElementById('button'),
    image: document.getElementById('image'),
    text: document.getElementById('text')
};
function doStuff() {
    image.src = 'http://some.url/image';
    button.click();
    console.log(text.innerHTML);
    // 更多逻辑
}
function removeButton() {
    // 按钮是 body 的后代元素
    document.body.removeChild(document.getElementById('button'));
    // 此时，仍旧存在一个全局的 #button 的引用
    // elements 字典。button 元素仍旧在内存中，不能被 GC 回收。
}
```

4. 闭包

保存父级作用域的变量


### javascript跨域

[详解前端跨域](https://github.com/wengjq/Blog/issues/2)

1. 同源策略

协议、端口和主机相同，才叫同源。
可以在同一主机下访问不同文件夹

2. 主域的跨域

document.domain的场景只适用于不同子域的框架间的交互，及主域必须相同的不同源。

页面可能会更改其自己的来源，但有一些限制。脚本可以将 document.domain的值设置为其当前域或其当前域的超级域。如果将其设置为其当前域的超级域，则较短的域将用于后续原始检查。例如，假设文档中的一个脚本在 http://store.company.com/dir/other.html 执行以下语句：

```js
document.domain = "company.com";
```
这条语句执行之后，页面将会成功地通过对 http://company.com/dir/page.html 的同源检测。

> 注：浏览器单独保存端口号。任何的赋值操作，包括document.domain = document.domain都会以null值覆盖掉原来的端口号。因此，company.com:8080页面的脚本不能仅通过设置document.domain = "company.com"就能与company.com通信。赋值时必须带上端口号，以确保端口号不会为null。

```js
(1) 在www.a.com/a.html中：
document.domain = 'a.com';
var ifr = document.createElement('iframe');
ifr.src =  'http://www.script.a.com/b.html';  
ifr.display = none;
document.body.appendChild(ifr);
ifr.onload = function(){ 
    var doc = ifr.contentDocument || ifr.contentWindow.document;                                                          
    ifr.onload = null;
};

(2) 在www.script.a.com/b.html中：
document.domain = 'a.com';//注意：使用document.domain允许子域安全访问其父域时，您需要设置document域在父域和子域中具有相同的值。这是必要的，即使这样做只是将父域设置回其原始值。否则可能会导致权限错误。这里都是a.com。
```

#### 3. 完全不同源的跨域（两个页面之间的通信）

3.1 通过 `location.hash` 跨域

假设域名a.com下的文件cs1.html要和jianshu.com域名下的cs2.html传递信息。

1. cs1.html首先创建自动创建一个隐藏的iframe，iframe的src指向jianshu.com域名下的cs2.html页面。
2. cs2.html响应请求后再将通过修改cs1.html的hash值来传递数据。
3. 同时在cs1.html上加一个定时器，隔一段时间来判断location.hash的值有没有变化，一旦有变化则获取获取hash值。

3.2 通过 `Window.name` 跨域

window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的。window.name属性的神奇之处在于name 值在不同的页面（甚至不同域名）加载后依旧存在（如果没修改则值不会变化），并且可以支持非常长的 name 值（2MB）。

3.3 通过`window.postMessage`跨域

```js
var popup = window.open('http://bbb.com', 'title');//父窗口http://aaa.com向子窗口http://bbb.com发消息，调用postMessage方法。
popup.postMessage('Hello World!', 'http://bbb.com');
```
postMessage方法的第一个参数是具体的信息内容，第二个参数是接收消息的窗口的源（origin），即"协议 + 域名 + 端口"。也可以设为*，表示不限制域名，向所有窗口发送。


#### 4. AJAX请求不同源的跨域

4.1 通过`JSONP`跨域

```js
function todo(data){
  console.log('The author is: '+ data.name);
}
var script = document.createElement('script');
script.src = 'http://www.jianshu.com/author?callback=todo';//向服务器www.jianshu.com发出请求。注意，该请求的查询字符串有一个callback参数，用来指定回调函数的名字。
document.body.appendChild(script);
//服务器收到这个请求以后，会将数据放在回调函数的参数位置返回。
todo({"name": "fewjq"});
//由于<script>元素请求的脚本，直接作为代码运行。这时，只要浏览器定义了todo函数，该函数就会立即调用。作为参数的JSON数据被视为JavaScript对象。
```
优点：简单适用，老式浏览器全部支持，服务器改造小。不需要XMLHttpRequest或ActiveX的支持。
缺点：只支持GET请求。

4.2 通过WebSocket跨域

WebSocket是一种通信协议，使用ws://（非加密）和wss://（加密）作为协议前缀。该协议不实行同源政策，只要服务器支持，就可以通过它进行跨源通信。

4.3、通过CORS跨域

隶属于 W3C 的 Web 应用工作组推荐了一种新的机制，即跨源资源共享（Cross-Origin Resource Sharing ) CORS。这种机制让Web应用服务器能支持跨站访问控制，从而使得安全地进行跨站数据传输成为可能。需要特别注意的是，这个规范是针对API容器的（比如说XMLHttpReques 或者 Fetch），以减轻跨域HTTP请求的风险。


跨源资源共享标准( cross-origin sharing standard) 使得以下场景可以使用跨站 HTTP 请求：

1、使用 XMLHttpRequest 或 Fetch发起跨站 HTTP 请求。
2、Web 字体 (CSS 中通过 @font-face 使用跨站字体资源)，因此，网站就可以发布 TrueType 字体资源，并只允许已授权网站进行跨站调用。
3、WebGL 贴图
4、使用drawImage绘制
5、Images/video 画面到canvas.
6、样式表（使用 CSSOM）
7、Scripts (for unmuted exceptions)

```js
//比如说，假如站点 http://foo.example 的网页应用想要访问 http://bar.other 的资源。以下的 JavaScript 代 
//码应该会在 foo.example 上执行：    
var invocation = new XMLHttpRequest();
var url = 'http://bar.other/resources/public-data/';
function callOtherDomain() {
  if(invocation) {    
    invocation.open('GET', url, true);
    invocation.onreadystatechange = handler;
    invocation.send(); 
  }
}
```

CORS的优点：CORS支持所有类型的HTTP请求，是跨域HTTP请求的根本解决方案。


### 详解CORS

- Cross-Origin Resource Sharing实现的最重要的一点就是对参数” Access-Control-Allow-Origin”的配置，即通过 次参数检查该跨域请求是否可以被通过。
- 如：Access-Control-Allow-Origin:http://a.com表示允许a.com下的域名跨域访问；
- Access-Control-Allow-Origin:*表示允许所有的域名跨域访问。


如果需要读取读取cookie：
需要配置参数：`Access-Control-Allow-Credentials:true`
同时在`xhr`发起请求的时候设置参数`withCredentials`为`true`：
```javascript
var xhr = new XMLHttpRequest();
xhr.open();
xhr.withCredentials = true; //这个放在xhr.open后面执行，否则有些浏览器部分版本会异常，导致设置无效。
```
php代码
```php
header('Access-Control-Allow-Origin:http: //a.com');
header('Access-Control-Allow-Methods:POST,GET');
header('Access-Control-Allow-Credentials:true'); 
echo 'Cross-domain Ajax';
```


JS:
```
var xhr = new XMLHttpRequest(); ; 
xhr.open('GET', 'http: //b.com/cros/ajax.php', true);
xhr.withCredentials = true;
xhr.onload = function () {          
  alert(xhr.response);//reposHTML;
};  
xhr.onerror = function () {
 alert('error making the request.');
};
xhr.send();
```


