# CSS基础知识

## css

### margin-collapsing
在CSS中，两个或以上的块元素（可能是兄弟，也可能不是）之间的相邻外边距可以被合并成一个单独的外边距。通过此方式合并的外边距被称为折叠，且产生的已合并的外边距被称为折叠外边距。

处于同一个块级上下文中的块元素，没有行框、没有间隙、没有内边距和边框隔开它们，这样的元素垂直边缘毗邻，则称之为相邻

什么是垂直边缘毗邻？

元素的上外边距和其属于常规流中的第一个孩子的上外边距。
元素的下外边距和其属于常规流中的下一个兄弟的上外边距。
属于常规流中的最后一个孩子的下外边距和其父亲的下外边距，如果其父亲的高度计算值为 auto。
元素的上、下外边距，如果该元素没有建立新的块级格式上下文，且 min-height 的计算值为零、height 的计算值为零或 auto、且没有属于常规流中的孩子。
说得很清楚了，我想是的。你可能需要注意的是发生 margin 折叠的元素不一定是兄弟关系，也能是父子或祖先的关系。

**如何避免margin折叠？**
我想肯定有人要问，那我不想有 margin 折叠的情况发生，该怎么办？其实从上面的规则中，我们已经可以抽出避免 margin 折叠的条件来。

margin 折叠元素只发生在块元素上；

- 浮动元素不与其他元素 margin 折叠；

- 定义了属性overflow且值不为visible（即创建了新的块级格式化上下文）的块元素，不与它的子元素发生margin 折叠；

- 绝对定位元素的 margin 不与任何 margin 发生折叠。

- 特殊：根元素的 margin 不与其它任何 margin 发生折叠；

  如果常规流中的一个块元素没有 border-top、padding-top，且其第一个浮动的块级子元素没有间隙，则该元素的上外边距会与其常规流中的第一个块级子元素的上外边距折叠。

### 外边距折叠(collapsing margins)
毗邻的两个或多个``margin``会合并成一个margin，叫做外边距折叠。规则如下：

1. 两个或多个毗邻的普通流中的块元素垂直方向上的margin会折叠
2. 浮动元素/inline-block元素/绝对定位元素的margin不会和垂直方向上的其他元素的margin折叠
3. 创建了块级格式化上下文的元素，不会和它的子元素发生margin折叠
4. 元素自身的margin-bottom和margin-top相邻时也会折叠


### 权重计算详解

我们把特殊性分为4个等级，每个等级代表一类选择器，每个等级的值为其所代表的选择器的个数乘以这一等级的权值，最后把所有等级的值相加得出选择器的特殊值。

4个等级的定义如下：

- 第一等：代表内联样式，如: style=””，权值为1000。
- 第二等：代表ID选择器，如：#content，权值为100。
- 第三等：代表类，伪类和属性选择器，如.content，权值为10。
- 第四等：代表类型选择器和伪元素选择器，如div p，权值为1。

### flex的几种属性

容器上面
```css
flex-direction: row | row-reverse | column | column-reverse;

flex-wrap:nowrap | wrap | wrap-reverse;

flex-flow:<flex-direction> || <flex-wrap>;

justify-content:flex-start | flex-end | center | space-between | space-around;

align-items:flex-start | flex-end | center | baseline | stretch;

align-content:flex-start | flex-end | center | space-between | space-around | stretch;
```

项目上面：

```css
order:<integer>;
flex-grow:<number>; /* default 0 */
flex-shrink: <number>; /* default 1 */
flex-basis:<length> | auto; /* default auto */
flex:none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
align-self:auto | flex-start | flex-end | center | baseline | stretch;
```


### z-index设为负数

[CSS postion中z-index负值的应用](http://blog.csdn.net/lihefei_coder/article/details/72869065)

当父元素设置了position属性并且设置了背景颜色，子元素设置了position:absolute和z-index:-1，子元素将会在父元素的层级背后不可见。

如果在父元素样式里加上z-index值，子元素的z-index的负数值将会失效，状态变为可见。

### CSS优先级

下面列表中，选择器类型的优先级是递增的：

类型选择器（type selectors）（例如, h1）和 伪元素（pseudo-elements）（例如, ::before）
类选择器（class selectors） (例如,.example)，属性选择器（attributes selectors）（例如, [type="radio"]），伪类（pseudo-classes）（例如, :hover）ID选择器（例如, #example）通配选择符（universal selector）(*), 关系选择符（combinators） (+, >, ~, ' ')  和 否定伪类（negation pseudo-class）(:not()) 对优先级没有影响。（但是，在 :not() 内部声明的选择器是会影响优先级）。

给元素添加的内联样式 (例如, style="font-weight:bold") 总会覆盖外部样式表的任何样式 ，因此可看作是具有最高的优先级。.

当在一个样式声明中使用一个!important 规则时，此声明将覆盖任何其他声明。虽然技术上!important与优先级无关，但它与它直接相关。

使用 !important 是一个坏习惯，应该尽量避免，因为这破坏了样式表中的固有的级联规则 使得调试找bug变得更加困难了。当两条相互冲突的带有 !important 规则的声明被应用到相同的元素上时，拥有更大优先级的声明将会被采用。



### document.querySelector的奇怪现象

[querySelector 和 querySelectorAll 方法浏览器实现无误，避免将其与 JQuery 的选择器混淆](http://w3help.org/zh-cn/casestudies/003)

> querySelectorAll : when invoked, return a NodeList containing all of the matching Element nodes within the node’s subtrees, in document order. 
> 还有一句 :Even though the method is invoked on an element, selectors are still evaluated in the context of the entire document.  


简单来说css选择器是以整个文档为基础的。

会从整个文档出发然后再判断在不在所选的结构当中。

###不同的清除浮动技巧

1. 使用带有clear属性的空元素
```css
.clearfix{
    clear:both;
}
```

2. 使用CSS的:after伪元素

给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。这是我认为目前比较完美的解决方式。

```css
.clearfix::after{
    content: "\20";
    display: block;
    height: 0;
    clear: both;
}
.clearfix{
    zoom: 1;
}
```
为了IE6和IE7浏览器，要给clearfix这个class添加一条zoom:1;触发haslayout（你可以把它写到IE6、7的CSS hacker文件里，这样不会影响W3C标准验证）。

其实Zoom属性是IE浏览器的专有属性，Firefox等浏览器不支持。它可以设置或检索对象的缩放比例。除此之外，它还有其他一些小作用，比如触发ie的hasLayout属性，清除浮动、清除margin的重叠等。 

该方法需要给每组浮动元素都添加一个容器，推荐在页面布局时使用。大量使用依旧会对代码量造成一些影响。



3. 父元素容器加一个overflow：hidden或者auto；

```css
.container{
    overflow: hidden;
}
```

4. 给父元素本身添加float

5. 给领接元素添加clear属性

[清理浮动的那些事儿——6种清理浮动的方法](http://lightcss.com/all-about-clear-float/)





### getElementsByTagName vs querySelectorAll

> 根据jsperf上速度比较结果，querySelectorAll操作每秒可执行191,649次，而getElementsByTagName操作则每秒可执行18,733,468次，是前者的97.7倍！！！

为什么差异这么大呢？其实，这两种方法的区别不仅仅是querySelectorAll接受css选择器，而getElementsByTagName只接受tagName，他们最大的区别在于返回值的不同：querySelectorAll返回静态的（static）NodeList，getElementsByTagName返回动态的(live)NodeList！


**动态NodeList**
这是文档对象模型(DOM,Document Object Model)的一个坑，NodeList对象（以及HTMLCollection对象）是一种特殊类型的对象，DOM Level 3 spec规范中对HTMLCollection对象的描述如下：

> DOM中的NodeList和NamedNodeMap对象是动态的（live），也就是说，对底层文档结果的修改会动态的反映到相关的集合NodeList和NamedNodeMap中。例如，如果先获取了某个元素的子元素的动态集合NodeList对象，然后又在其他地方顺序添加更多子元素到这个DOM父元素中，这些修改将自动反射到NodeList，不需要手动进行其他调用。同样的，对DOM树上某个Node节点的修改，也会实时影响引用了该节点的NodeList和NamedNodeMap对象。


getElementsByTagName方法返回对应标签名的元素的一个动态集合，只要document发生变化，就会自动更新对应的元素，因此，下面的代码实际上是一个死循环

```javascript
var divs = document.getElementsByTagName('div');
var i = 0;
while(i < divs.length) {
    document.body.appendChild(document.createElement('div'));
    i++;
}
```


**静态NodeList**
querySelectorAll方法返回一个静态的NodeList，这是表示的选择器API规范：

querySelectorAll返回的NodeList对象必须是静态的！后续对底层document的更改不能影响返回的这个NodeList对象，这意味着返回的对象将包含在创建列表那一刻就需要包含可匹配的所有元素节点。

使用querySelectorAll获取节点时就不会造成死循环。

**为什么动态NodeList更快呢**
动态NodeList对象在浏览器中可以更快地被创建并返回，因为他们不需要预先获取所有的信息，而静态NodeList从一开始就需要取得并封装所有相关数据。

在webkit源码中，对每种NodeList类型都有一个单独的源文件：DynamicNodeList和StaticNodeList，这两种对象类型的创建方式是完全不同的。

DynamicNodeList对象通过在cache缓存中注册他的存在并创建，从本质上讲，创建一个新的DynamicNodeList是非常轻量级的，因为不需要做任何前期工作，每次访问DynamicNodeList时，必须查询document的变化，length属性以及item()方法证明了这一点。相比之下，StaticNodeList对象实例由另一个文件创建，然后循环填充所有的数据。在document中执行静态查询的前期成本上比起DynamicNodeList要显著提高很多倍。如果真正的查看webkit的源码，你会发现他为querySelectorAll明确的创建了一个返回对象，在其中又使用一个循环来获取每一个结果，并最终返回一个NodeList。





### 形成BFC(Block Formatting Context)的几种方式

BFC全称”Block Formatting Context”, 中文为“块级格式化上下文”。BFC元素特性表现原则就是，内部子元素再怎么翻江倒海，翻云覆雨都不会影响外部的元素。


怎样形成BFC

- 根元素或其它包含它的元素

- 浮动 (元素的 float 不是 none)

- 绝对定位的元素 (元素具有 position 为 absolute 或 fixed)

- 非块级元素具有 display: inline-block，table-cell, table-caption, flex, inline-flex

- 块级元素具有overflow ，且值不是 visible

BFC用处：

1. 清除浮动
2. 布局：自适应两栏布局
3. 防止垂直margin合并


### CSS选择器有哪些

1. ***通用选择器**：选择所有元素，**不参与计算优先级**，兼容性IE6+
2. **#X id选择器**：选择id值为X的元素，兼容性：IE6+
3. **.X 类选择器**： 选择class包含X的元素，兼容性：IE6+
4. **X Y后代选择器**： 选择满足X选择器的后代节点中满足Y选择器的元素，兼容性：IE6+
5. **X 元素选择器**： 选择标所有签为X的元素，兼容性：IE6+
6. **:link，：visited，：focus，：hover，：active链接状态**： 选择特定状态的链接元素，顺序LoVe HAte，兼容性: IE4+
7. **X + Y直接兄弟选择器**：在**X之后第一个兄弟节点**中选择满足Y选择器的元素，兼容性： IE7+
8. **X > Y子选择器**： 选择X的子元素中满足Y选择器的元素，兼容性： IE7+
9. **X ~ Y兄弟**： 选择**X之后所有兄弟节点**中满足Y选择器的元素，兼容性： IE7+
10. **[attr]**：选择所有设置了attr属性的元素，兼容性IE7+
11. **[attr=value]**：选择属性值刚好为value的元素
12. **[attr~=value]**：选择属性值为空白符分隔，其中一个的值刚好是value的元素
13. **[attr|=value]**：选择属性值刚好为value或者value-开头的元素
14. **[attr^=value]**：选择属性值以value开头的元素
15. **[attr$=value]**：选择属性值以value结尾的元素
16. **[attr*=value]**：选择属性值中包含value的元素
17. **[:checked]**：选择单选框，复选框，下拉框中选中状态下的元素，兼容性：IE9+
18. **X:after, X::after**：after伪元素，选择元素虚拟子元素（元素的最后一个子元素），CSS3中::表示伪元素。兼容性:after为IE8+，::after为IE9+
19. **:hover**：鼠标移入状态的元素，兼容性a标签IE4+， 所有元素IE7+
20. **:not(selector)**：选择不符合selector的元素。**不参与计算优先级**，兼容性：IE9+
21. **::first-letter**：伪元素，选择块元素第一行的第一个字母，兼容性IE5.5+
22. **::first-line**：伪元素，选择块元素的第一行，兼容性IE5.5+
23. **:nth-child(an + b)**：伪类，选择前面有an + b - 1个兄弟节点的元素，其中n
   &gt;= 0， 兼容性IE9+
24. **:nth-last-child(an + b)**：伪类，选择后面有an + b - 1个兄弟节点的元素
   其中n &gt;= 0，兼容性IE9+
25. **X:nth-of-type(an+b)**：伪类，X为选择器，**解析得到元素标签**，选择**前面**有an + b - 1个**相同标签**兄弟节点的元素。兼容性IE9+
26. **X:nth-last-of-type(an+b)**：伪类，X为选择器，解析得到元素标签，选择**后面**有an+b-1个相同**标签**兄弟节点的元素。兼容性IE9+
27. **X:first-child**：伪类，选择满足X选择器的元素，且这个元素是其父节点的第一个子元素。兼容性IE7+
28. **X:last-child**：伪类，选择满足X选择器的元素，且这个元素是其父节点的最后一个子元素。兼容性IE9+
29. **X:only-child**：伪类，选择满足X选择器的元素，且这个元素是其父元素的唯一子元素。兼容性IE9+
30. **X:only-of-type**：伪类，选择X选择的元素，**解析得到元素标签**，如果该元素没有相同类型的兄弟节点时选中它。兼容性IE9+
31. **X:first-of-type**：伪类，选择X选择的元素，**解析得到元素标签**，如果该元素
   是此此类型元素的第一个兄弟。选中它。兼容性IE9+

### css sprite是什么,有什么优缺点

概念：将多个小图片拼接到一个图片中。通过background-position和元素尺寸调节需要显示的背景图案。

优点：

1. 减少HTTP请求数，极大地提高页面加载速度
2. 增加图片信息重复度，提高压缩比，减少图片大小
3. 更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现

缺点：

1. 图片合并麻烦
2. 维护麻烦，修改一个图片可能需要从新布局整个图片，样式


### `display: none;`与`visibility: hidden;`的区别
联系：它们都能让元素不可见

区别：

1. display:none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见
2. display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility: hidden;是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式
3. 修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
4. 读屏器不会读取display: none;元素内容；会读取visibility: hidden;元素内容

### css hack原理及常用hack

原理：利用**不同浏览器对CSS的支持和解析结果不一样**编写针对特定浏览器样式。常见的hack有1）属性hack。2）选择器hack。3）IE条件注释

- IE条件注释：适用于[IE5, IE9]常见格式如下

```
<!--[if IE 6]>
Special instructions for IE 6 here
<![endif]-->
```

- 选择器hack：不同浏览器对选择器的支持不一样

```
/***** Selector Hacks ******/

/* IE6 and below */
* html #uno  { color: red }

/* IE7 */
*:first-child+html #dos { color: red }

/* IE7, FF, Saf, Opera  */
html>body #tres { color: red }

/* IE8, FF, Saf, Opera (Everything but IE 6,7) */
html>/**/body #cuatro { color: red }

/* Opera 9.27 and below, safari 2 */
html:first-child #cinco { color: red }

/* Safari 2-3 */
html[xmlns*=""] body:last-child #seis { color: red }

/* safari 3+, chrome 1+, opera9+, ff 3.5+ */
body:nth-of-type(1) #siete { color: red }

/* safari 3+, chrome 1+, opera9+, ff 3.5+ */
body:first-of-type #ocho {  color: red }

/* saf3+, chrome1+ */
@media screen and (-webkit-min-device-pixel-ratio:0) {
 #diez  { color: red  }
}

/* iPhone / mobile webkit */
@media screen and (max-device-width: 480px) {
 #veintiseis { color: red  }
}

/* Safari 2 - 3.1 */
html[xmlns*=""]:root #trece  { color: red  }

/* Safari 2 - 3.1, Opera 9.25 */
*|html[xmlns*=""] #catorce { color: red  }

/* Everything but IE6-8 */
:root *> #quince { color: red  }

/* IE7 */
*+html #dieciocho {  color: red }

/* Firefox only. 1+ */
#veinticuatro,  x:-moz-any-link  { color: red }

/* Firefox 3.0+ */
#veinticinco,  x:-moz-any-link, x:default  { color: red  }
```

- 属性hack：不同浏览器解析bug或方法

```
/* IE6 */
#once { _color: blue }

/* IE6, IE7 */
#doce { *color: blue; /* or #color: blue */ }

/* Everything but IE6 */
#diecisiete { color/**/: blue }

/* IE6, IE7, IE8 */
#diecinueve { color: blue\9; }

/* IE7, IE8 */
#veinte { color/*\**/: blue\9; }

/* IE6, IE7 -- acts as an !important */
#veintesiete { color: blue !ie; } /* string after ! can be anything */
```

### specified value,computed value,used value计算方法

- specified value: 计算方法如下：
    1. 如果样式表设置了一个值，使用这个值
    2. 如果没有设置值，这个属性是继承属性，从父元素继承
    3. 如果没设置，并且不是继承属性，使用css规范指定的初始值

- computed value: 以specified value根据规范定义的行为进行计算，通常将相对值计算为绝对值，例如em根据font-size进行计算。一些使用百分数并且需要布局来决定最终值的属性，如width，margin。百分数就直接作为computed value。line-height的无单位值也直接作为computed value。这些值将在计算used value时得到绝对值。**computed value的主要作用是用于继承**

- used value：属性计算后的最终值，对于大多数属性可以通过window.getComputedStyle获得，尺寸值单位为像素。以下属性依赖于布局，
    - background-position
    - bottom, left, right, top
    - height, width
    - margin-bottom, margin-left, margin-right, margin-top
    - min-height, min-width
    - padding-bottom, padding-left, padding-right, padding-top
    - text-indent


    ### `link`与`@import`的区别

1. ``link``是HTML方式， ``@import``是CSS方式
2. ``link``最大限度支持并行下载，``@import``过多嵌套导致串行下载，出现[FOUC](http://www.bluerobot.com/web/css/fouc.asp/)
3. ``link``可以通过``rel="alternate stylesheet"``指定候选样式
4. 浏览器对``link``支持早于``@import``，可以使用``@import``对老浏览器隐藏样式
5. ``@import``必须在样式规则之前，可以在css文件中引用其他文件
6. 总体来说：**[link优于@import](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/)**

### ``display: block;``和``display: inline;``的区别

``block``元素特点：

1.处于常规流中时，如果``width``没有设置，会自动填充满父容器
2.可以应用``margin/padding``
3.在没有设置高度的情况下会扩展高度以包含常规流中的子元素
4.处于常规流中时布局时在前后元素位置之间（独占一个水平空间）
5.忽略``vertical-align``

``inline``元素特点

1.水平方向上根据``direction``依次布局
2.不会在元素前后进行换行
3.受``white-space``控制
4.``margin/padding``在竖直方向上无效，水平方向上有效
5.``width/height``属性对非替换行内元素无效，宽度由元素内容决定
6.非替换行内元素的行框高由``line-height``确定，替换行内元素的行框高由``height``,``margin``,``padding``,``border``决定
6.浮动或绝对定位时会转换为``block``
7.``vertical-align``属性生效



### PNG,GIF,JPG的区别及如何选
参考资料： [选择正确的图片格式](http://www.yuiblog.com/blog/2008/11/04/imageopt-2/)
**GIF**:

1. 8位像素，256色
2. 无损压缩
3. 支持简单动画
4. 支持boolean透明
5. 适合简单动画

**JPEG**：

1. 颜色限于256
2. 有损压缩
3. 可控制压缩质量
4. 不支持透明
5. 适合照片

**PNG**：

1. 有PNG8和truecolor PNG
2. PNG8类似GIF颜色上限为256，文件小，支持alpha透明度，无动画
3. 适合图标、背景、按钮

### CSS有哪些继承属性

- 关于文字排版的属性如：
  +  [font](https://developer.mozilla.org/en-US/docs/Web/CSS/font)
  +  [word-break](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break)
  +  [letter-spacing](https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing)
  +  [text-align](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align)
  +  [text-rendering](https://developer.mozilla.org/en-US/docs/Web/CSS/text-rendering)
  +  [word-spacing](https://developer.mozilla.org/en-US/docs/Web/CSS/word-spacing)
  +  [white-space](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space)
  +  [text-indent](https://developer.mozilla.org/en-US/docs/Web/CSS/text-indent)
  +  [text-transform](https://developer.mozilla.org/en-US/docs/Web/CSS/text-transform)
  +  [text-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow)
- [line-height](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height)
- [color](https://developer.mozilla.org/en-US/docs/Web/CSS/color)
- [visibility](https://developer.mozilla.org/en-US/docs/Web/CSS/visibility)
- [cursor](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor)



### IE6浏览器有哪些常见的bug,缺陷或者与标准不一致的地方,如何解决

- IE6不支持min-height，解决办法使用css hack：

```
.target {
    min-height: 100px;
    height: auto !important; 
    height: 100px;   // IE6下内容高度超过会自动扩展高度
}
```

- ``ol``内``li``的序号全为1，不递增。解决方法：为li设置样式``display: list-item;``

- 未定位父元素``overflow: auto;``，包含``position: relative;``子元素，子元素高于父元素时会溢出。解决办法：1）子元素去掉``position: relative;``; 2）不能为子元素去掉定位时，父元素``position: relative;``

```
<style type="text/css">
.outer {
    width: 215px;
    height: 100px;
    border: 1px solid red;
    overflow: auto;
    position: relative;  /* 修复bug */
}
.inner {
    width: 100px;
    height: 200px;
    background-color: purple;
    position: relative;
}
</style>

<div class="outer">
    <div class="inner"></div>
</div>
```

- IE6只支持``a``标签的``:hover``伪类，解决方法：使用js为元素监听mouseenter，mouseleave事件，添加类实现效果：

```
<style type="text/css">
.p:hover,
.hover {
    background: purple;
}
</style>

<p class="p" id="target">aaaa bbbbb<span>DDDDDDDDDDDd</span> aaaa lkjlkjdf j</p>

<script type="text/javascript">
function addClass(elem, cls) {
    if (elem.className) {
        elem.className += ' ' + cls;
    } else {
        elem.className = cls;
    }
}
function removeClass(elem, cls) {
    var className = ' ' + elem.className + ' ';
    var reg = new RegExp(' +' + cls + ' +', 'g');
    elem.className = className.replace(reg, ' ').replace(/^ +| +$/, '');
}

var target = document.getElementById('target');
if (target.attachEvent) {
    target.attachEvent('onmouseenter', function () {
        addClass(target, 'hover');
    });
    target.attachEvent('onmouseleave', function () {
        removeClass(target, 'hover');
    })
}
</script>
```

- IE5-8不支持``opacity``，解决办法：

```
.opacity {
    opacity: 0.4
    filter: alpha(opacity=60); /* for IE5-7 */
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=60)"; /* for IE 8*/
}
```

- IE6在设置``height``小于``font-size``时高度值为``font-size``，解决办法：``font-size: 0;``
- IE6不支持PNG透明背景，解决办法: **IE6下使用gif图片**
- IE6-7不支持``display: inline-block``解决办法：设置inline并触发hasLayout

```
    display: inline-block;
    *display: inline;
    *zoom: 1;
```

- IE6下浮动元素在浮动方向上与父元素边界接触元素的外边距会加倍。解决办法：
  1）使用padding控制间距。
  2）浮动元素``display: inline;``这样解决问题且无任何副作用：css标准规定浮动元素display:inline会自动调整为block
- 通过为块级元素设置宽度和左右margin为auto时，IE6不能实现水平居中，解决方法：为父元素设置``text-align: center;``

### 容器包含若干浮动元素时如何清理(包含)浮动

1. 容器元素闭合标签前添加额外元素并设置``clear: both``
2. 父元素触发块级格式化上下文(见块级可视化上下文部分)
3. 设置容器元素伪元素进行清理[推荐的清理浮动方法](http://nicolasgallagher.com/micro-clearfix-hack/)

```
/**
* 在标准浏览器下使用
* 1 content内容为空格用于修复opera下文档中出现
*   contenteditable属性时在清理浮动元素上下的空白
* 2 使用display使用table而不是block：可以防止容器和
*   子元素top-margin折叠,这样能使清理效果与BFC，IE6/7
*   zoom: 1;一致
**/

.clearfix:before,
.clearfix:after {
    content: " "; /* 1 */
    display: table; /* 2 */
}

.clearfix:after {
    clear: both;
}

/**
* IE 6/7下使用
* 通过触发hasLayout实现包含浮动
**/
.clearfix {
    *zoom: 1;
}
```

### 什么是FOUC?如何避免
Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。**解决方法**：把样式表放到文档的`head`

### 如何创建块级格式化上下文(block formatting context),BFC有什么用
创建规则：

1. 根元素
2. 浮动元素（``float``不是``none``）
3. 绝对定位元素（``position``取值为``absolute``或``fixed``）
4. ``display``取值为``inline-block``,``table-cell``, ``table-caption``,``flex``, ``inline-flex``之一的元素
5. ``overflow``不是``visible``的元素


作用：

1. 可以包含浮动元素
2. 不被浮动元素覆盖
3. 阻止父子元素的margin折叠

### display,float,position的关系

英文原文：<http://dbaron.org/css/test/sec0907>

 
影响框的生成和布局的三个属性——`display`  `position` 和  `float`——间的相互关系如下： 

- 1，如果`display`设置为`none`，用户端必须忽略掉`position`和`float`。在这种情况下，元素不产生框。 
- 2，否则，`position`设置为`absolute`或`fixed`，`display`设置为`block`且`float`设置为`none`。框的位置将由`top`，`righ`'，`bottom`和`lef`'属性和该框的包含块确定。 
- 3，否则，如果`floa`的值不是`none`，`display`设置为`block`并且该框浮动。 
- 4，否则，应用指定的其它`display`属性。 即如果`position`设置为`absolute`或`fixed`且`float`的值不为`none`，`display`的值就会被设置为`block`，所以设置`display: inline; float: left;`等同于`float:left，display:inline` 的属性并未生效。因为用户端会忽略掉对`display`的设置。`float:left`和`display:inline-block`当然是不等同的。 



**position:absolute和float会隐式的改变display类型**

​	不论之前是什么类型的元素（`display:none`除外），只要设置了`position:absolute`或`float`，都会让元素以`display:block`的方式显示，可以设置长宽，默认宽度并不占满父元素，就算是显示的设置`display:inline`或`display:block`，仍然无效。 
`float`在IE6下的双倍边距`bug`就是利用添加`display:inline`来解决的 
注意一点的是，`position:relative`并不能够隐式的改变`display`的类型 

![20180317152127510246508.png](http://osmisz4zw.bkt.clouddn.com/20180317152127510246508.png)



### 如何确定一个元素的包含块(containing block)

1. 根元素的包含块叫做初始包含块，在连续媒体中他的尺寸与viewport相同并且anchored at the canvas origin；对于paged media，它的尺寸等于page area。初始包含块的direction属性与根元素相同。
2. ``position``为``relative``或者``static``的元素，它的包含块由最近的块级（``display``为``block``,``list-item``, ``table``）祖先元素的**内容框**组成
3. 如果元素``position``为``fixed``。对于连续媒体，它的包含块为viewport；对于paged media，包含块为page area
4. 如果元素``position``为``absolute``，它的包含块由祖先元素中最近一个``position``为``relative``,``absolute``或者``fixed``的元素产生，规则如下：
    - 如果祖先元素为行内元素，the containing block is the bounding box around the **padding boxes** of the first and the last inline boxes generated for that element.
    - 其他情况下包含块由祖先节点的**padding edge**组成

    如果找不到定位的祖先元素，包含块为**初始包含块**

### stacking context,布局规则,层叠上下文
z轴上的默认层叠顺序如下（从下到上）：

1. 根元素的边界和背景
2. 常规流中的元素按照html中顺序
3. 浮动块
4. positioned元素按照html中出现顺序

如何创建stacking context：

1. 根元素
2. z-index不为auto的定位元素
3. a flex item with a z-index value other than 'auto'
4. opacity小于1的元素
5. 在移动端webkit和chrome22+，z-index为auto，position: fixed也将创建新的stacking context

### 如何水平居中一个元素
- 如果需要居中的元素为**常规流中inline元素**，为父元素设置`text-align: center;`即可实现
- 如果需要居中的元素为**常规流中block元素**，1）为元素设置宽度，2）设置左右margin为auto。3）IE6下需在父元素上设置`text-align: center;`,再给子元素恢复需要的值

```Html
<body>
    <div class="content">
    aaaaaa aaaaaa a a a a a a a a
    </div>
</body>

<style>
    body {
        background: #DDD;
        text-align: center; /* 3 */
    }
    .content {
        width: 500px;      /* 1 */
        text-align: left;  /* 3 */
        margin: 0 auto;    /* 2 */

        background: purple;
    }
</style>
```

- 如果需要居中的元素为**浮动元素**，1）为元素设置宽度，2）`position: relative;`，3）浮动方向偏移量（left或者right）设置为50%，4）浮动方向上的margin设置为元素宽度一半乘以-1

```html
<body>
    <div class="content">
    aaaaaa aaaaaa a a a a a a a a
    </div>
</body>

<style>
    body {
        background: #DDD;
    }
    .content {
        width: 500px;         /* 1 */
        float: left;

        position: relative;   /* 2 */
        left: 50%;            /* 3 */
        margin-left: -250px;  /* 4 */

        background-color: purple;
    }
</style>
```

- 如果需要居中的元素为**绝对定位元素**，1）为元素设置宽度，2）偏移量设置为50%，3）偏移方向外边距设置为元素宽度一半乘以-1

```
<body>
    <div class="content">
    aaaaaa aaaaaa a a a a a a a a
    </div>
</body>

<style>
    body {
        background: #DDD;
        position: relative;
    }
    .content {
        width: 800px;

        position: absolute;
        left: 50%;
        margin-left: -400px;

        background-color: purple;
    }
</style>
```

- 如果需要居中的元素为**绝对定位元素**，1）为元素设置宽度，2）设置左右偏移量都为0,3）设置左右外边距都为auto

```html
<body>
    <div class="content">
    aaaaaa aaaaaa a a a a a a a a
    </div>
</body>

<style>
    body {
        background: #DDD;
        position: relative;
    }
    .content {
        width: 800px;

        position: absolute;
        margin: 0 auto;
        left: 0;
        right: 0;

        background-color: purple;
    }
</style>
```

### 如何竖直居中一个元素
参考资料：[6 Methods For Vertical Centering With CSS](http://www.vanseodesign.com/css/vertical-centering/)。 [盘点8种CSS实现垂直居中](http://blog.csdn.net/freshlover/article/details/11579669)

1. position:absolute+ 负数margin（缺点是需要知道宽高）
2. absolute+transform（translate(-50%,-50%)(不用知道宽高，但是可能不兼容)
3. absolute+四个方向设置为0 （兼容性好，缺点是不灵活
4. flex布局 display:flex;justify-content:center;align-items:center



- 需要居中元素为**单行文本**，为包含文本的元素设置大于`font-size`的`line-height`：

```html
<p class="text">center text</p>

<style>
.text {
    line-height: 200px;
}
</style>
```

### px，em，rem
px相对计算机的分辨率
em是相对单位 1em = 16px
rem root em 相对root节点的相对单位（CSS3）

### box-sizing
```css
border-box: 实际width = width;
所以 contentWidth = 实际设定width - padding - border；
content-box: 实际width = border+padding+contentWidth（设定的width）;
```

### 形成BFC(Block Formatting Context)的几种方式

BFC全称”Block Formatting Context”, 中文为“块级格式化上下文”。BFC元素特性表现原则就是，内部子元素再怎么翻江倒海，翻云覆雨都不会影响外部的元素。


怎样形成BFC

- 根元素或其它包含它的元素

- 浮动 (元素的 float 不是 none)

- 绝对定位的元素 (元素具有 position 为 absolute 或 fixed)

- 非块级元素具有 display: inline-block，table-cell, table-caption, flex, inline-flex

- 块级元素具有overflow ，且值不是 visible

BFC用处：

1. 清除浮动
2. 布局：自适应两栏布局
3. 防止垂直margin合并

### 圣杯布局和双飞翼布局
都是要表示将中间的内容自适应定位。

### 深入了解CSS3新特性

新的选择器

```css
:first-child
:nth-last-child
:only-child
:enabled
:not(s)
```

```css
@font-face
word-wrap
text-overflow:clip|ellipsis
text-decoration:
```

渐变效果gradient

```css
background-image:-webkit-gradient(linear,0% 0%,100% 0%,from(#2A8BBE),to(#FE280E));
```

阴影和反射

```css
test-shadow:5px 2px 6px rgba
-webkit-box-reflect: below 10px 
-webkit-gradient(linear, left top, left bottom, from(transparent), 
     to(rgba(255, 255, 255, 0.51))); 
```

flex

动画：CSS3 的 Transitions, Transforms 和 Animation

transition：

```css
.transStart { 
   background-color: white; 
   -webkit-transition: background-color 0.3s linear; 
   -moz-transition: background-color 0.3s linear; 
   -o-transition: background-color 0.3s linear; 
   transition: background-color 0.3s linear; 
} 
```

Transform




