#  js判断对象是否为空的几种方法 #

## 目录 ##

1. [将对象转化成json字符串](#href1)
2. [使用ES6的Object.keys()方法](#href2)
3. [Object.getOwnPropertyNames()方法](#href3)
4. [使用for in循环判断](#href4)

### <a href="href1">将对象转成json字符串</a> ###
转成json字符串之后在判断是否为空

```js
var obj = {};
console.log(JSON.stringify(obj) == '{}'); //true

```

### <a href='href2'>使用ES6的Object.keys()方法</a> ###
此方法是获取对象的属性名，存到数组中，返回数组对象，可以通过判断数组的length属性来判断
对象是否为空。

```js
var obj = {};
var arr =  Object.keys(obj);
console.log(arr.length,Array.isArray(arr)); // 0 true   注意：arr为数组。


var obj1 = {a:1,b:2};
var arr1 = Object.keys(obj1);
console.log(arr1.length);  //2
```

### <a href='href3'>Object.getOwnPropertyNames()方法</a> ###
此方法与上面的类似。

```js
var obj = {};
var arr = Object.getOwnPropertyNames(obj);
console.log(arr.length,Array.isArray(arr));  // 0 true

```

### <a href='href4'>使用for in循环判断</a> ###

```js
var isObj = function (x) {
  let y = false;
  for (var key in x) {
    y = true
  }
  return y
}
console.log(isObj({}));   //false

var isObj1 = function (x) {
  let y = false;
  for (var key in x) {
    y = true
  }
  return y
}
console.log(isObj1({a:1,b:2}));   //true
```
