#  H5
##  H5 

### `img`的`title`和`alt`有什么区别

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

`$("#block1").animate({left:50});`

​ block1移动，会影响到它父元素下的所有子元素。因为在移动过程中，所有子元素需要判断block1的z-index是否在自己的上面，如果是在自己的上面，则需要重绘，这里不会引起回流。

`$("#block2").animate({marginLeft:50});`

​ block2是相对定位的元素，影响的元素与block1一样，但是因为block2非绝对定位，而且改变的是marginLeft属性，所以这里每次改变不但会重绘，还会引起父元素及其下元素的回流。

​ 所以，动画效果应用到position属性为absolute或fixed的元素上，它们不影响其他元素的布局，所它他们只会导致重新绘制，而不是一个完整回流。这样消耗会更低。

### 替换元素和非替换元素有哪些，它们的差异是什么？

#### 替换元素

替换元素是浏览器根据其标签的元素与属性来判断显示具体的内容。

比如：`<input type="text"/> `，这是一个文本输入框，换一个其他type的时候，浏览器显示就不一样

(X)HTML中的`<img>、<input>、<textarea>、<select>、<object>`都是替换元素，这些元素都没有实际的内容。

#### 非替换元素

`(X)HTML `的大多数元素是不可替换元素，他们将内容直接告诉浏览器，将其显示出来。

比如`<p>merrier.wang</p>、<label>Merrier</label>`

浏览器将把这段内容直接显示出来。



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

​ 假设block1是position: absolute的元素，block2是position: relative的元素。当使用`jquery`的animate()方法移动元素来展示一些动画效果时：

`$("#block1").animate({left:50});`

​ block1移动，会影响到它父元素下的所有子元素。因为在移动过程中，所有子元素需要判断block1的z-index是否在自己的上面，如果是在自己的上面，则需要重绘，这里不会引起回流。

`$("#block2").animate({marginLeft:50});`

​ `block2`是相对定位的元素，影响的元素与block1一样，但是因为block2非绝对定位，而且改变的是marginLeft属性，所以这里每次改变不但会重绘，还会引起父元素及其下元素的回流。

​ 所以，动画效果应用到position属性为absolute或fixed的元素上，它们不影响其他元素的布局，所它他们只会导致重新绘制，而不是一个完整回流。这样消耗会更低。

### 可替换元素和非可替换元素（头条）

[可替换元素和非可替换元素](https://segmentfault.com/a/1190000006835284)

### 层叠上下文
[层叠上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)

- 给一个 HTML 元素定位和 z-index 赋值创建一个层叠上下文，（opacity 值不为 1 的也是相同）。
- 层叠上下文可以包含在其他层叠上下文中，并且一起创建一个有层级的层叠上下文。
- 每个层叠上下文完全独立于它的兄弟元素：当处理层叠时只考虑子元素。
- 每个层叠上下文是自包含的：当元素的内容发生层叠后，整个该元素将会 在父层叠上下文中 按顺序进行层叠。

### doctype是什么,举例常见doctype及特点

1. `<!doctype>`声明必须处于HTML文档的头部，在`<html>`标签之前，HTML5中不区分大小写
2. `<!doctype>`声明不是一个HTML标签，是一个用于告诉浏览器当前HTMl版本的指令
3. 现代浏览器的html布局引擎通过检查doctype决定使用兼容模式还是标准模式对文档进行渲染，一些浏览器有一个接近标准模型。
3. 在HTML4.01中`<!doctype>`声明指向一个DTD，由于HTML4.01基于SGML，所以DTD指定了标记规则以保证浏览器正确渲染内容
4. HTML5不基于SGML，所以不用指定DTD

常见dotype：

1. **HTML4.01 strict**：不允许使用表现性、废弃元素（如font）以及frameset。声明：`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`
2. **HTML4.01 Transitional**:允许使用表现性、废弃元素（如font），不允许使用frameset。声明：`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">`
3. **HTML4.01 Frameset**:允许表现性元素，废气元素以及frameset。声明：`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">`
4. **XHTML1.0 Strict**:不使用允许表现性、废弃元素以及frameset。文档必须是结构良好的XML文档。声明：``<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">``
5. **XHTML1.0 Transitional**:允许使用表现性、废弃元素，不允许frameset，文档必须是结构良好的XMl文档。声明： ``<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">``
6. **XHTML 1.0 Frameset**:允许使用表现性、废弃元素以及frameset，文档必须是结构良好的XML文档。声明：``<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">``
7. **HTML 5**: `<!doctype html>`


### HTML全局属性(global attribute)有哪些

参考资料：[MDN: html global attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)或者[W3C HTML global-attributes](http://www.w3.org/TR/html-markup/global-attributes.html#common.attrs.core)

- `accesskey`:设置快捷键，提供快速访问元素如<a href="#" accesskey="a">aaa</a>在windows下的firefox中按``alt + shift + a``可激活元素
- `class`:为元素设置类标识，多个类名用空格分开，CSS和javascript可通过class属性获取元素
- `contenteditable`: 指定元素内容是否可编辑
- `contextmenu`: 自定义鼠标右键弹出菜单内容
- `data-*`: 为元素增加自定义属性
- `dir`: 设置元素文本方向
- `draggable`: 设置元素是否可拖拽
- `dropzone`: 设置元素拖放类型： copy, move, link
- `hidden`: 表示一个元素是否与文档。样式上会导致元素不显示，但是不能用这个属性实现样式效果
- `id`: 元素id，文档内唯一
- `lang`: 元素内容的的语言
- `spellcheck`: 是否启动拼写和语法检查
- `style`: 行内css样式
- `tabindex`: 设置元素可以获得焦点，通过tab可以导航
- `title`: 元素相关的建议信息
- `translate`: 元素和子孙节点内容是否需要本地化

