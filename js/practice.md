# 一些常见的套路和练习题


### JavaScript each函数的实现
几个关键点：
typeof instanceOf callback.call

```javascript
function each(obj,callback){
    if(typeof(obj)!=="object") return false;
    // var newobj = obj instanceof Array? []: {};
    for(let key in obj){
        if(callback.call(obj[key],key,obj[key])===false){
            break;
        }
        // console.log(key);
        // console.log(obj[key]);
        // callback.call(obj[key],key,obj[key]);
    }
    return obj;
}

function log(key,value){
    console.log('key: '+key+' value: '+value);
    console.log(this.name);
}

//test
var person = [
    {name: 'kevin'},
    {name: 'daisy'}
]
var john = {
    "name":"john",
    "age":18,
    "sex":true,
}
each(john,log);
```

### for in 和for of的区别



### 有关for循环血的教训~~~
在for循环中。如果使用了arr.length,永远都不要在for循环中使用pop，push这种东西！！！！！


