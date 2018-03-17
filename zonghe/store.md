# 有关存储

### sessionStorage,localStorage,cookie区别

1. 都会在浏览器端保存，有大小限制，同源限制
2. cookie会在请求时发送到服务器，作为会话标识，服务器可修改cookie；web storage不会发送到服务器
3. cookie有path概念，子路径可以访问父路径cookie，父路径不能访问子路径cookie
4. 有效期：cookie在设置的有效期内有效，默认为浏览器关闭；sessionStorage在窗口关闭前有效，localStorage长期有效，直到用户删除
5. 共享：sessionStorage不能共享，localStorage在同源文档之间共享，cookie在同源且符合path规则的文档之间共享
6. localStorage的修改会促发其他文档窗口的update事件
7. cookie有secure属性要求HTTPS传输
8. 浏览器不能保存超过300个cookie，单个服务器不能超过20个，每个cookie不能超过4k。web storage大小支持能达到5M it

### 离线缓存
1. localstorage: key-value,每个5mb
2. 本地存储 sessionStorage：关闭页面后会被清空，而localStorage会一直保留
3. 离线缓存：application-cache:提升页面载入速度，降低服务器压力

```
1. 浏览器对缓存数据的容量限制可能不太一样（某些浏览器设置的限制是每个站点 5MB）
2. 如果manifest文件，或者内部列举的某一个文件不能正常下载，整个更新过程将视为失败，浏览器继续全部使用老的缓存
3. 引用manifest的html必须与manifest文件同源，在同一个域下
4. 浏览器会自动缓存引用manifest文件的HTML文件，这就导致如果改了HTML内容，也需要更新版本才能做到更新。
5. manifest文件中CACHE则与NETWORK，FALLBACK的位置顺序没有关系，如果是隐式声明需要在最前面
6. FALLBACK中的资源必须和manifest文件同源
7. 更新完版本后，必须刷新一次才会启动新版本（会出现重刷一次页面的情况），需要添加监听版本事件。
8. 站点中的其他页面即使没有设置manifest属性，请求的资源如果在缓存中也从缓存中访问
9. 当manifest文件发生改变时，资源请求本身也会触发更新
```
离线缓存与传统浏览器缓存区别：

1. 离线缓存是针对整个应用，浏览器缓存是单个文件

2. 离线缓存断网了还是可以打开页面，浏览器缓存不行

3. 离线缓存可以主动通知浏览器更新资源


