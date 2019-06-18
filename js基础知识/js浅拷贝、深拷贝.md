# js浅拷贝、深拷贝 #

## 目录 ##

1. [基本数据类型-键值存储在栈内存中](#href1)
2. [引用数据类型-键存在栈内存中，值存在堆内存中](#href2)
3. [实现深拷贝的几种方法](#href3)
   1. [使用JSON对象的parse、stringify](#href3-1)
   2. [递归实现深拷贝](#href3-2)

js数据类型可以划分为基本数据类型和引用数据类型。
基本数据类型：number,string,null,undefined,boolean
引用类型：对象{a:1}、数组[1,2,3]、函数(方法)


### <a name='href1'>基本数据类型-键值存储在栈内存中</a> ###

```js
例如： var a = 1;

        栈内存
  name          value
   a              1
```

当b = a时，栈内存会开辟一个新的内存。

```js
var b = a;
       栈内存
  name        value
   a            1
   b            1
```

因此，当a的值改变时，b的值是不会改变的。


### <a name='href2'>引用数据类型-键存在栈内存中，值存在堆内存中</a> ###

对于引用数据类型，名存在栈内存中，值存在于堆内存中，但是栈内存会提供一个引用的地址指向堆内存中的值。

```js
var arr = [1,2,3];

       栈内存                  堆内存
  name      value              value
  arr       堆地址1  ----->    [1,2,3]    //值是存在堆内存里面

```

当将arr的值复制给arr1时。

```js
var arr1 = arr;
       栈内存                  堆内存
  name      value              value
  arr       堆地址1  
                     ----->    [1,2,3]    //两者都是指向同一个内存
  arr1      堆地址2
```
因此，当将arr复制给arr1时，其实是复制了arr的引用地址，而不是单纯的值。


```js
arr[0] = 0;
       栈内存                  堆内存
  name      value              value
  arr       堆地址1  
                     ----->    [0,2,3]    //两者都是指向同一个内存
  arr1      堆地址2
```
当改变arr的某一项时，由于arr和arr1指向的地址是一样的，所以arr1也会受到影响。这就是浅拷贝。



### <a name='href3'>实现深拷贝的几种方法</a> ###

如果在堆内存中也开辟一个新的内存专门为arr1存放值，就像基本类型那样，就可以实现深拷贝。

#### <a name='href3-1'>使用JSON对象的parse、stringify</a> ####

```js
var arr = [1,2,3];
var arr1 = JSON.parse(JSON.stringify(arr));
arr[0] = 0;
console.log(arr,arr1);  // [0,2,3] [1,2,3]
```

#### <a name='href3-2'>递归实现深拷贝</a> ####

```js
function deepClone (obj){
    let objClone = Array.isArray(obj) ? [] : {};
    if (obj && typeof obj === "object") {
      // for...in 会把继承的属性一起遍历
      for (let key in obj) {
        // 判断是不是自有属性，而不是继承属性
        if (obj.hasOwnProperty(key)) {
          //判断ojb子元素是否为对象或数组，如果是，递归复制
          if (obj[key] && typeof obj[key] === "object") {
            objClone[key] = this.deepClone(obj[key]);
          } else {
            //如果不是，简单复制
            objClone[key] = obj[key];
          }
        }
      }
    }
    return objClone;
}
var arr = [1,2,3];
var arr1 = deepClone(arr);
arr[0] = 0;
console.log(arr,arr1);  //[0,2,3] [1,2,3]
```
递归实现深拷贝时会有一个缺陷：当遇到两个互相引用的对象，会出现死循环的情况，
为了避免相互引用的对象导致死循环的情况，则应该在遍历的时候判断是否相互引用对象，
如果是则退出循环。

#### <a name='href3-3'>其他方法</a> ####

1.热门的函数库lodash，也有提供_.cloneDeep用来做深拷贝

```js
var _ = require('lodash');
var obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
var obj2 = _.cloneDeep(obj1);
```

2.jquery实现深拷贝
jquery 提供一个$.extend可以用来做深拷贝

```js
var $ = require('jquery');
var obj1 = {
   a: 1,
   b: {
     f: {
       g: 1
     }
   },
   c: [1, 2, 3]
};
var obj2 = $.extend(true, {}, obj1);
```

注意：slice()和concat()并非深拷贝方法。
