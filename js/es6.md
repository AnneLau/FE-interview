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



