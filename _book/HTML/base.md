# HTML基础知识



#html

### `<img>`的`title`和`alt`有什么区别

1. `title`是[global attributes](http://www.w3.org/TR/html-markup/global-attributes.html#common.attrs.core)之一，用于为元素提供附加的advisory information。通常当鼠标滑动到元素上的时候显示。
2. `alt`是`<img>`的特有属性，是图片内容的等价描述，用于图片无法加载时显示、读屏器阅读图片。可提图片高可访问性，除了纯装饰图片外都必须设置有意义的值，搜索引擎会重点分析。


### 页面重绘（repaint）和页面回流（reflow）

如果你的HTML变得很大很复杂，那么影响你javaScript性能的可能并不是javaScript代码的复杂度，而是页面的回流和重绘。

2. 重绘和回流

2.1 重绘和回流
重绘(repaint)：当render tree中的一些元素需要更新属性，单这些属性只会影响元素的外观，风格，而不会影响到元素的布局，此类的页面渲染叫作页面重绘。

回流(reflow)：当render tree中的一部分（或全部）因为元素的规模尺寸，布局，隐藏等改变而引起的页面重新渲染。

可以看出，回流必将引起重绘，而重绘不一定会引起回流。

2.2 引发回流的范例
当页面布局和几何属性改变时就需要回流。下述情况会发生浏览器回流：

DOM树发生变化——如：增加一个元素或删除一个元素（元素为可见元素）；
通过style控制元素的位置变化——典型的碰壁反弹；
元素尺寸的改变——盒模型的每种尺寸均算在其内；
内容改变引发的尺寸改变——如：文本文本改变或者图片大小改变而引起的计算值宽度和高度改变；
浏览器窗口尺寸改变——resize事件发生时。

2.3 改善由于dom操作产生的回流

减少回流、重绘其实就是需要减少对render tree的操作，并减少对一些style信息的请求，尽量利用好浏览器的优化策略。具体方法有：

（1）不要一个一个改变元素的样式属性，直接改变className，如果动态改变样式，则使用cssText。

```javascript
//不好的写法
var left = 1;
var top = 1;
el.style.left = left + "px";
el.style.right = right + "px";
//比较好的写法
el.className += "className1";
//动态改变样式，比较好的写法
el.style.cssText += ";left:" + left + "px; top:" + top + "px;";

```
（2）让要操作的元素进行“离线处理”，处理完后一起更新。这里所谓的”离线处理”即让元素不存在于render tree中，比如：

- 使用DocumentFragment进行缓存操作,引发一次回流和重绘；
    这个主要用于添加元素的时候，就是先把所有要添加到元素添加到1个div中(这个div也是新加的)，最后才把这个div append到body中。
- 使用display:none技术，只引发两次回流和重绘；
    先display:none 隐藏元素，然后对该元素进行所有的操作，最后再显示该元素。因对display:none的元素进行操作不会引起回流、重绘。所以只要操作只会有2次回流。
- 使用cloneNode(true or false) 和 replaceChild 技术，引发一次回流和重绘。

（3）不要经常访问会引起浏览器flush队列的属性，如果你确实要访问，利用缓存。

```javascript
//不好的写法
for(循环) {
     el.style.left = el.offsetLeft + 5 + "px";
     el.style.top = el.offsetTop + 5 + "px";
 }
// 比较好的写法
var left = el.offsetLeft,
	top = el.offsetTop,
	s = el.style;
for(循环) {
     left += 10;
     top += 10;
     s.left = left + "px";
     s.top = top + "px";
 }
```

4）让元素脱离动画流，减少回流的Render Tree的规模。

​ 假设block1是position: absolute的元素，block2是position: relative的元素。当使用jquery的animate()方法移动元素来展示一些动画效果时：

$("#block1").animate({left:50});

​ block1移动，会影响到它父元素下的所有子元素。因为在移动过程中，所有子元素需要判断block1的z-index是否在自己的上面，如果是在自己的上面，则需要重绘，这里不会引起回流。

$("#block2").animate({marginLeft:50});

​ block2是相对定位的元素，影响的元素与block1一样，但是因为block2非绝对定位，而且改变的是marginLeft属性，所以这里每次改变不但会重绘，还会引起父元素及其下元素的回流。

​ 所以，动画效果应用到position属性为absolute或fixed的元素上，它们不影响其他元素的布局，所它他们只会导致重新绘制，而不是一个完整回流。这样消耗会更低。

### 替换元素和非替换元素有哪些，它们的差异是什么？

####替换元素

替换元素是浏览器根据其标签的元素与属性来判断显示具体的内容。

比如：<input type="text"/> ，这是一个文本输入框，换一个其他type的时候，浏览器显示就不一样

(X)HTML中的<img>、<input>、<textarea>、<select>、<object>都是替换元素，这些元素都没有实际的内容。

####非替换元素

(X)HTML 的大多数元素是不可替换元素，他们将内容直接告诉浏览器，将其显示出来。

比如<p>merrier.wang</p>、<label>Merrier</label>

浏览器将把这段内容直接显示出来。