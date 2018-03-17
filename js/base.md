# JS基础问题

##JS

### \__proto\__和prototype和super的关系

![](https://pic1.zhimg.com/80/e83bca5f1d1e6bf359d1f75727968c11_hd.jpg)

总结：
1.对象有属性__proto__,指向该对象的构造函数的原型对象。
2.方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。

### 数据类型总结
- 六种原型：Boolean Undefined String Symbol Null Number;
- 一种object型  BUSSNON
- typeof可以识别：boolean undefined string symbol object number function 
- BUSSNOF


### $NAN
如果其中一个值是NaN,或者两个值都是NaN，则它们不相等。NaN和其他任何值都是不相等的，包括它本身。通过x !== x来判断x是否为NaN，只有在x为NaN的时候，这个表达式的值才为true。


### 变量提升

var和function都会被提升
function 是整个函数体一起提升
class 不会提升
而且函数中的变量如果没有var声明，会自动提升到全局，注意这一点
会导致子域对全局变量的改变，很坑

### 什么闭包,闭包有什么用(ali1)

MDN：闭包是函数及创建该函数的词法环境构成的，这个环境包含了这个闭包创建时所能访问的所有局部变量。在我们的例子中，myFunc 是执行 makeFunc 时创建的 displayName 函数实例的引用，而 displayName 实例仍可访问其词法作用域中的变量，即可以访问到 name 。由此，当 myFunc 被调用时，name 仍可被访问，其值 Mozilla 就被传递到alert中。


闭包是在某个作用域内定义的函数，它可以访问这个作用域内的所有变量。闭包作用域链通常包括三个部分：

1. 函数本身作用域。
2. 闭包定义时的作用域。
3. 全局作用域。

闭包常见用途：

1. 只有一个方法的对象可以用闭包来创建
2. 创建特权方法用于访问控制
3. 事件处理程序及回调



### javascript有哪几种方法定义函数(ali1)

1. 函数声明表达式
2. function操作符
3. Function 构造函数
4. ES6:arrow function

重要参考资料：MDN:Functions_and_function_scope

### javascript有哪些方法定义对象(ali1)

1. 对象字面量： var obj = {};
2. 构造函数： var obj = new Object();
3. Object.create(): var obj = Object.create(Object.prototype);



### 评价一下三种方法实现继承的优缺点,并改进

```js
function Shape() {}

function Rect() {}

// 方法1
Rect.prototype = new Shape();

// 方法2
Rect.prototype = Shape.prototype;

// 方法3
Rect.prototype = Object.create(Shape.prototype);

Rect.prototype.area = function () {
  // do something
};
```

方法1：

1. 优点：正确设置原型链实现继承
2. 优点：父类实例属性得到继承，原型链查找效率提高，也能为一些属性提供合理的默认值
3. 缺点：父类实例属性为引用类型时，不恰当地修改会导致所有子类被修改
4. 缺点：创建父类实例作为子类原型时，可能无法确定构造函数需要的合理参数，这样提供的参数继承给子类没有实际意义，当子类需要这些参数时应该在构造函数中进行初始化和设置
5. 总结：继承应该是继承方法而不是属性，为子类设置父类实例属性应该是通过在子类构造函数中调用父类构造函数进行初始化

方法2：

1. 优点：正确设置原型链实现继承
2. 缺点：父类构造函数原型与子类相同。修改子类原型添加方法会修改父类

方法3：

1. 优点：正确设置原型链且避免方法1.2中的缺点
2. 缺点：ES5方法需要注意兼容性

改进：

1. 所有三种方法应该在子类构造函数中调用父类构造函数实现实例属性初始化

```js
function Rect() {
    Shape.call(this);
}
```


2. 用新创建的对象替代子类默认原型，设置``Rect.prototype.constructor = Rect;``保证一致性
3. 第三种方法的polyfill：

```javascript
function create(obj) {
    if (Object.create) {
        return Object.create(obj);
    }

    function f() {};
    f.prototype = obj;
    return new f();
}
```
### 考察知识点最广的JS面试题目

[多看几遍](http://www.cnblogs.com/xxcanghai/p/5189353.html)

### 优先级 （）和 . 大于 new

```javascript
new Foo.getName();//2 ==== new (Foo.getName)()
new Foo().getName();//3 === (new Foo()).getName()
new new Foo().getName();// === new ((new Foo()).getName)()
```


### 构造函数返回值
语言中的构造函数本身不该有返回值，但是js中可以有

- 无返回值：返回对象
- 返回值是基本类型：忽略返回值
- 返回值是引用类型：返回引用类型

构造函数的静态属性子对象是无法访问到的。
只有构造函数的prototype中函数子对象可以访问的到



### typeof和instanceof的区别
- typeof的作用

  typeof是一元运算符，返回值为字符串，该字符串用来说明运算数的数据类型
  用来获取运算数的数据类型。返回的值有number、boolean、undefined、function、object、string
  number：数字会返回number类型
  boolean：boolean值只有true和false
  undefined：当变量未被声明时会返回undefined，这与var name;alert(name);是不一样的。后者是指变量已声明，但未被初始化。
  function：当运算数为函数时，返回function
  obeject：对象、数组、null会返回object。正因为typeof遇到数组、null都会返回object，所以我们要判断某个对象是否是数组或者某个变量是否是对象的实例时就要使用instanceof
  string：当运算数为字符串时会返回string
  (typeof null 返回object

简言之 typeof判断大方向，instanceof判断Object中的小方向

typeof的结果只有BUSSNOF七种



### addEventListener的第三个参数

先捕获再冒泡

addEventListener(event,function,useCapture)
useCapture = true 表示在事件捕获阶段调用处理函数



### 特殊作用
`n = n>>>0;`表示`n`取补码形式
判断一个数是奇数还是偶数可以使用 `& `
`n&1==0`表示偶数



### `===`运算符判断相等的流程是怎样的

1. 如果两个值不是相同类型，它们不相等
2. 如果两个值都是null或者都是undefined，它们相等
3. 如果两个值都是布尔类型true或者都是false，它们相等
4. 如果其中有一个是**NaN**，它们不相等
5. 如果都是数值型并且数值相等，他们相等， -0等于0
6. 如果他们都是字符串并且在相同位置包含相同的16位值，他它们相等；如果在长度或者内容上不等，它们不相等；两个字符串显示结果相同但是编码不同==和===都认为他们不相等
7. 如果他们指向相同对象、数组、函数，它们相等；如果指向不同对象，他们不相等

### `==`运算符判断相等的流程是怎样的

1. 如果两个值类型相同，按照===比较方法进行比较
2. 如果类型不同，使用如下规则进行比较
  1. 如果其中一个值是null，另一个是undefined，它们相等
  2. 如果一个值是**数字**另一个是**字符串**，将**字符串转换为数字**进行比较
  3. 如果有布尔类型，将**true转换为1，false转换为0**，然后用==规则继续比较
  4. 如果一个值是对象，另一个是数字或字符串，将对象转换为原始值然后用==规则继续比较
  5. **其他所有情况都认为不相等**

例子：

``` Js
1    ==  1         // true
'1'  ==  1         // true
1    == '1'        // true
0    == false      // true
0    == null       // false
var object1 = {'key': 'value'}, object2 = {'key': 'value'}; 
object1 == object2 //false
0    == undefined  // false
null == undefined  // true
[]  ==  1          //false
[]  ==  false       //true
{}  ==  false       //false
[]  ==  ''          //true
```

![==](https://pic4.zhimg.com/80/0ea77966986b068628b17c33419e4476_hd.jpg)

> 假如你打算把一个变量赋予对象类型的值，但是现在还没有赋值，那么你可以用null表示此时的状态(证据之一就是typeof null 的结果是'object')；相反，假如你打算把一个变量赋予原始类型的值，但是现在还没有赋值，那么你可以用undefined表示此时的状态。

> ToPrimitive(obj)等价于：先计算obj.valueOf()，如果结果为原始值，则返回此结果；否则，计算obj.toString()，如果结果是原始值，则返回此结果；否则，抛出异常。

引用自：[一图搞懂==](https://zhuanlan.zhihu.com/p/21650547)

总结：万物皆数

### 对象到字符串的转换步骤

1. 如果对象有toString()方法，javascript调用它。如果返回一个原始值（primitive value如：string number boolean）,将这个值转换为字符串作为结果
2. 如果对象没有toString()方法或者返回值不是原始值，javascript寻找对象的valueOf()方法，如果存在就调用它，返回结果是原始值则转为字符串作为结果
3. 否则，javascript不能从toString()或者valueOf()获得一个原始值，此时throws a TypeError



### 对象到数字的转换步骤

```Js
1. 如果对象有valueOf()方法并且返回元素值，javascript将返回值转换为数字作为结果
2. 否则，如果对象有toString()并且返回原始值，javascript将返回结果转换为数字作为结果
3. 否则，throws a TypeError
```
### <,>,<=,>=的比较规则

所有比较运算符都支持任意类型，但是**比较只支持数字和字符串**，所以需要执行必要的转换然后进行比较，转换规则如下:
1. 如果操作数是对象，转换为原始值：如果valueOf方法返回原始值，则使用这个值，否则使用toString方法的结果，如果转换失败则报错
2. 经过必要的对象到原始值的转换后，如果两个操作数都是字符串，按照字母顺序进行比较（他们的16位unicode值的大小）
3. 否则，如果有一个操作数不是字符串，**将两个操作数转换为数字**进行比较

### +运算符工作流程
1. 如果有操作数是对象，转换为原始值
2. 此时如果有**一个操作数是字符串**，其他的操作数都转换为字符串并执行连接
3. 否则：**所有操作数都转换为数字并执行加法**

### 函数内部arguments变量有哪些特性,有哪些属性,如何将它转换为数组

- arguments所有函数中都包含的一个局部变量，是一个类数组对象，对应函数调用时的实参。如果函数定义同名参数会在调用时覆盖默认对象
- arguments[index]分别对应函数调用时的实参，并且通过arguments修改实参时会同时修改实参
- arguments.length为实参的个数（Function.length表示形参长度）
- arguments.callee为当前正在执行的函数本身，使用这个属性进行递归调用时需注意this的变化
- arguments.caller为调用当前函数的函数（已被遗弃）
- 转换为数组：<code>var args = Array.prototype.slice.call(arguments, 0);</code>

### XMLHttpRequest通用属性和方法

1. `readyState`:表示请求状态的整数，取值：
  - UNSENT（0）：对象已创建
  - OPENED（1）：open()成功调用，在这个状态下，可以为xhr设置请求头，或者使用send()发送请求
  - HEADERS_RECEIVED(2)：所有重定向已经自动完成访问，并且最终响应的HTTP头已经收到
  - LOADING(3)：响应体正在接收
  - DONE(4)：数据传输完成或者传输产生错误
2. `onreadystatechange`：readyState改变时调用的函数
3. `status`：服务器返回的HTTP状态码（如，200， 404）
4. `statusText`:服务器返回的HTTP状态信息（如，OK，No Content）
5. `responseText`:作为字符串形式的来自服务器的完整响应
6. `responseXML`: Document对象，表示服务器的响应解析成的XML文档
7. `abort()`:取消异步HTTP请求
8. `getAllResponseHeaders()`: 返回一个字符串，包含响应中服务器发送的全部HTTP报头。每个报头都是一个用冒号分隔开的名/值对，并且使用一个回车/换行来分隔报头行
9. `getResponseHeader(headerName)`:返回headName对应的报头值
10. `open(method, url, asynchronous [, user, password])`:初始化准备发送到服务器上的请求。method是HTTP方法，不区分大小写；url是请求发送的相对或绝对URL；asynchronous表示请求是否异步；user和password提供身份验证
11. `setRequestHeader(name, value)`:设置HTTP报头
12. `send(body)`:对服务器请求进行初始化。参数body包含请求的主体部分，对于POST请求为键值对字符串；对于GET请求，为null

### 解释语言的特性有哪些：非独立，效率低

笔记： 
解释性语言和编译性语言的定义： 
计算机不能直接理解高级语言，只能直接理解机器语言，所以必须要把高级语言翻译成机器语言，计算机才能执行高级语言编写的程序。 
翻译的方式有两种，一个是编译，一个是解释。两种方式只是翻译的时间不同。

解释性语言的定义： 
解释性语言的程序不需要编译，在运行程序的时候才翻译，每个语句都是执行的时候才翻译。这样解释性语言每执行一次就需要逐行翻译一次，效率比较低。 
现代解释性语言通常把源程序编译成中间代码，然后用解释器把中间代码一条条翻译成目标机器代码，一条条执行。

编译性语言的定义： 
编译性语言写的程序在被执行之前，需要一个专门的编译过程，把程序编译成为机器语言的文件，比如exe文件，以后要运行的话就不用重新翻译了，直接使用编译的结果就行了（exe文件），因为翻译只做了一次，运行时不需要翻译，所以编译型语言的程序执行效率高。

对于JavaScript这种解释语言来说： 
非独立：JavaScript语言依赖执行环境，对于客户端来说是浏览器，对于服务端来说是node。 
效率低：执行前不需要编译，执行时才编译，因此效率低。



