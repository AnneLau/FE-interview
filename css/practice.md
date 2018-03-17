# 练习题

## css练习题

### 左边固定右边自适应

方案一：使用float+margin

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        *{
            border:0;
            padding: 0;
            margin:0;
        }
        .left{
            float: left;
            width:200px;
            height: 500px;
            background-color:red;
            /* margin-left: -200px; */
        }
        .right{
            width: 100%;
            height: 500px;
            margin-left: 200px;
            background-color: blue;
        }
    </style>
</head>
<body>
    
    <div class="left box"></div>
    <div class="right box"></div>
</body>
</html>
```

之所以能这么写是因为：
float加上负数margin会产生神奇效果


对于负的margin值，其实可以分为两组来讨论，
一组是垂直方向上的，一组是水平方向上的。
垂直方向上的：与该元素是否浮动无关，当设置负的margin-top时，元素向上移。当设置负的margin-bottom时，元素不产生移动，只是对应的参考线发生移动。
对应水平方向上的：以该元素是否浮动有关，
在非浮动下，B/R不移动，L/T向相同方向移动|margin|。
对于浮动的元素，如果margin设置的方向和float的方向相同，那么这时浮动元素发生移动。如果margin设置的方向和float的方向相反，那么这时是设计到参考线的问题，元素本身不移动。

作者：shawnXiao
链接：https://www.zhihu.com/question/20116963/answer/14036572
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

2. 使用浮动加上负边距
和float方向相反的负数margin

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            border: 0;
            padding: 0;
            margin: 0;
        }

        #left {
            background-color: green;
            float: left;
            width: 220px;
            margin-right: -100%;
        }

        #content {
            float: left;
            width: 100%;
        }

        #contentInner {
            margin-left: 220px;
            /*==等于左边栏宽值==*/
            background-color: orange;
        }
    </style>
</head>

<body>
    <div id="left">
        Left Sidebar
    </div>
    <div id="content">
        <div id="contentInner">
            Main Content
        </div>
    </div>
</body>

</html>
```


### 垂直居中

1. 设置line-height

```css
    .vertical{
        height: 100px;
        line-height: 100px;
    }
```
针对小的block，单行文本

2. 对具有固定高度的元素使用绝对定位

```css
    .vertical{
        position: absolute;
        width: 100px;
        height: 100px;
        top:50%;
        left: 50%;
        margin-top:-50px;
        margin-left:-50px;
    }
```
由于固定死元素的高度，致使没有足哆的空间，当内容超过容器的大小时，要么会消息，要么会出现滚动条（如果元素在body内，当用户缩小浏览器窗口时，body的滚动条将不会出现）。
这种方法可以实现元素的水平垂直居中，常用于页面在最中间的布局，使用这种方法一定要把握住：水平垂直居中的元素要有明确的大小（换句话说就是要有确切的宽和高度值）；给元素进行绝对定位，并设置left,top值为“50%”（此处最好使用 对定位，如果只是单单水平居中，此处可以换成相对定位）；**最后设置margin-top和margin-left的负值，而且其值分别为元素高度和宽度的一半。**

3. 使用display：table

```html
<div id="container">
    <div id="content">content</div>
</div>

#container {
    height: 300px;
    display: table;/*让元素以表格形式渲染*/
}
#content {
    display:table-cell;/*让元素以表格的单元素格形式渲染*/
    vertical-align: middle;/*使用元素的垂直对齐*/
}
```


缺点是：只适合现代浏览器。

4. 使用position:absolute;加上margin：auto

```css
    .inner{
        position: absolute;
        width: 200px;
        height: 200px;
        background-color: red;
        margin: auto;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
    }
```


