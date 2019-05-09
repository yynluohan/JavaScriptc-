# ES6 let与const用法 #

## 目录 ##

1. [let命令](#href1)
   1. [基本用法](#href1-1)
   2. [let声明的变量不存在变量提升](#href1-2)
   3. [暂时性死区](#href1-3)
   4. [不允许重复声明](#href1-4)
2. [块级作用域](#href2)

## <a name='href1'>let命令</a> ##

### <a name='href1-1'>基本用法</a> ###

let和var类似，都是用来声明变量，但是let申明的变量只能在所在的代码块生效。

```js
{
  let a = 123;
  var b = 345;
  console.log(a); //123
}
console.log(a); //a is not defined
console.log(b); //345
```

例子：
（1）当使用var定义时，下面代码块输出的是10

```js
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function() {
    console.log(i);
  }
}
a[6]()  // 10
```
注释：变量i是用var定义的，在全局都是有效的，所以每一次循环，新的i都会覆盖旧的值，导致
输出的是最后一轮的i的值

（2）当使用let定义时，下面代码块输出的是6

```js
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function() {
    console.log(i);
  }
}
a[6]()  // 6
```
注释：变量i是用let声明的，仅在块级作用域内有效，当前的i只在本轮循环有效，所以每一次循环
的i其实都是一个新的变量，所以最后输出的是6。


### <a name='href1-2'>let声明的变量不存在变量提升</a> ###
var定义的变量存在变量提升，但是let声明的变量不存在变量提升。

```js
console.log(a);  //报错 （let声明变量，必须先声明，后使用）
console.log(b);  //undefined

let a = '123';
var b = '123';
```
注释：上面代码中，当脚本运行到第一行时，虽然下面已经定义了变量a，但是let声明的变量不会
提升，所以此时的a暂未声明，所以会抛出错误。但是当脚本运行到第二行时，此时变量b已经声明
了，只是暂未赋值，所以会输出undefined。

### <a name='href1-3'>暂时性死区</a> ###

（1）只要块级作用域内存在let命令，它所声明的变量就“绑定”这个区域，不在受外部的影响。

```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // 报错
  let tmp;
}
```

上面代码中，存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。

ES6明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称TDZ）。

```js
if (true) {
  // TDZ开始
  tmp = 'abc'; // 报错
  console.log(tmp); // 报错

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```
（2）暂时性死区也意味着typeof不再是一个百分之百安全的操作。

```js
typeof x; // 报错
let x;
```

（3）如果一个变量根本没有被声明，使用typeof反而不会报错

```js
typeof x   //undefined
```
上面的x是一个不存在的变量名，结果返回“undefined”。所以，在没有let之前，typeof运算符是
百分之百安全的，永远不会报错。

（4）有些“死区”比较隐蔽，不太容易发现
```js
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错
```
上面代码中，调用bar函数之所以报错（某些实现可能不报错），是因为参数x默认值等于
另一个参数y，而此时y还没有声明，属于”死区“。如果y的默认值是x，就不会报错，因为
此时x已经声明了。

```js
function bar(x = 2, y = x) {
  return [x, y];
}
bar(); // [2, 2]
```

ES6规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量
声明前就使用这个变量，从而导致意料之外的行为。这样的错误在ES5是很常见的，现在有了这种
规定，避免此类错误就很容易了。

总之，暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可
获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。


### <a name='href1-4'>不允许重复声明</a> ###
let不允许在**相同作用域内**，重复声明一个变量。

```js
//报错
function () {
  let a = 123;
  var a = 456;
}


//报错
function () {
  let a = 1;
  let a = 2;
}
```
注意：let定义变量不能再同一个作用域内重复定义。

```js
function func(arg) {
  let arg;  //报错
}

function func(arg) {
  {
    let arg; //不报错
  }
}
```


## <a name='#href2'>块级作用域</a> ##

### <a name='herf2-1'>为什么需要块级作用域</a> ###
ES5只有**全局作用域**和**函数作用域**，这带来了很多不合理的场景。

（1）场景1：内层变量可能会覆盖外层。

```js
var arr = 123;

function fun() {
  console.log(arr);  // 123
}
fun()

///
var arr = 123;

function fun() {
  console.log(arr); //undefined
  var arr = 456
}
```
上面代码输出的值不同，第二处的arr变量由于变量提升，导致内层的arr变量覆盖了外层的arr变量。

（2）场景2：用来计数的循环变量泄露为全局变量。

```js
var s = 'hello';
for (var i = 0; i < s.length; i++){
  console.log(s[i]);
}
console.log(i); //5
```
上面的代码中，变量i只是用来控制循环，但是循环结束后，这个变量i并没有消失，泄露成了全局变量。
