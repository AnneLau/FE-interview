# ES6相关问题

### Symbol

> Symbol() funtion 返回一个symbol类型的值

！！！不能使用 new Symbol()
引用官方翻译，符号是一种特殊的、不可变的数据类型，它可以作为对象属性的标识符使用。符号对象是一个对的符号原始数据类型的隐式对象包装器。

Symbol的应用场景。

- symbol是最终的解决方案
- symbol是程序创建并且可以用作属性键的值，并且它能避免命名冲突的风险。
```js
   var mySymbol = Symbol();
```
symbol设计的初衷是为了避免冲突



### fetch和ajax的区别
[fetch](https://github.com/camsong/blog/issues/2)
fetch
window的一个方法 主要特点是
1、第一个参数是URL
2、第二个参数可选参数 可以控制不同的init对象
3、使用了js 中的promise对象

```js
fetch(url).then(function (response) {
    return response.json()   //执行成功第一步
}).then(function (returnedValue) {
    //执行成功的第二步
}).catch(function (err) {
    //中途的任何地方出错  都会在这里被捕获到
})
```
注意：
fetch 的第二参数中
1、默认的请求为get请求 可以使用method:post 来进行配置 
2、第一步中的 response有许多方法 json() text() formData()
3、Fetch跨域的时候默认不会带cookie 需要手动的指定 credentials:'include'

使用fetch之后得到的是一个promise对象 在这个promise对象里边再定义执行成功的时候是什么。下面是正确的fetch的使用方法

```js
 var promise=fetch('http://localhost:3000/news', {
        method: 'get'
    }).then(function(response) {
             return  response.json()
    }).catch(function(err) {
        // Error :(
    });
    promise.then(function (data) {
          console.log(data)
    }).catch(function (error) {
        console.log(error)
    })
```
fetch和ajax 的主要区别
1、fetch()返回的promise将不会拒绝http的错误状态，即使响应是一个HTTP 404或者500 
2、在默认情况下 fetch不会接受或者发送cookies

使用fetch开发项目的时候的问题
1、所有的IE浏览器都不会支持 fetch()方法
2、服务器端返回 状态码 400 500的时候 不会reject


Fetch 请求默认是不带 cookie 的，需要设置 fetch(url, {credentials: 'include'})
服务器返回 400，500 错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject。
竟然没有提到 IE，这实在太不科学了，现在来详细说下 IE

