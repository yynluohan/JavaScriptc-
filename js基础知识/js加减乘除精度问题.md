# js四则运算精度问题 #

## 目录 ##

1. [加法运算](#href1)
   1. [方法一](#href1-1)
   2. [方法二](#href1-2)
   2. [方法三](#href1-3)
2. [减法运算](#href2)
2. [乘法运算](#href3)

javascript进行加减乘除运算时，如果操作数出现小数时，会出现精度问题，从而导致计算的结果
不准确。

## <a name='href1'>加法运算</a> ##

### <a name='href1-1'>方法一</a> ###

使用Math.pow()方法

```js
function addSum(){
  let sum = 0;
  if(arguments.length > 0) {
    for(let i = 0; i < arguments.length; i++) {
      //第一个数的小数点后面的长度
      const firstNumber = sum.toString().split('.').length > 1 ? sum.toString().split('.')[1].length : 0;
      //取加法后一位的小数点后的长度
      const lastNumber = arguments[i].toString().split('.').length > 1 ? arguments[i].toString().split('.')[1].length : 0;
      //比较长度
      const lengthNumber = firstNumber > lastNumber ? firstNumber : firstNumber == lastNumber ? 0 : lastNumber;
      const multiple = Math.pow(10,lengthNumber);
      sum = (sum*multiple + arguments[i]*multiple)/multiple
    }
  }
  return sum
}
```

### <a name='href1-2'>方法二</a> ###

使用数组join()方法

```js
function addSum(){
  let sum = 0;
  if(arguments.length > 0) {
    for(let i = 0; i < arguments.length; i++) {
      //第一个数的小数点后面的长度
      const firstNumber = sum.toString().split('.').length > 1 ? sum.toString().split('.')[1].length : 0;
      //取加法后一位的小数点后的长度
      const lastNumber = arguments[i].toString().split('.').length > 1 ? arguments[i].toString().split('.')[1].length : 0;
      //比较长度
      const lengthNumber = firstNumber > lastNumber ? firstNumber : firstNumber == lastNumber ? 0 : lastNumber;
      let list = [];
      list.length = lengthNumber + 1;
      const multiple = Number(1 + list.join('0'));
      sum = (sum*multiple + arguments[i]*multiple)/multiple
    }
  }
  return sum
}
```

### <a name='href1-3'>方法三</a> ###

使用粗暴的for循环

```js
function addSum(){
  let sum = 0;
  if(arguments.length > 0) {
    for(let i = 0; i < arguments.length; i++) {
      //第一个数的小数点后面的长度
      const firstNumber = sum.toString().split('.').length > 1 ? sum.toString().split('.')[1].length : 0;
      //取加法后一位的小数点后的长度
      const lastNumber = arguments[i].toString().split('.').length > 1 ? arguments[i].toString().split('.')[1].length : 0;
      //比较长度
      const lengthNumber = firstNumber > lastNumber ? firstNumber : firstNumber == lastNumber ? 0 : lastNumber;
      let multiple = 1;
      if(lengthNumber > 0) {
        for(let j = 0; j < lengthNumber; j++){
          multiple += '0'
        }
      }
      multiple = Number(multiple)
      sum = (sum*multiple + arguments[i]*multiple)/multiple
    }
  }
  return sum
}
```

```js
测试结果：
const sum = addSum(1.123,2,3.2131,1.032,10.25);
console.log('sum = ',sum)  //sum = 17.6181
```


## <a name='href2'>减法运算</a> ##

```js
function onSub( a, b ) {
  //将传进来的参数转换成数值型
  var firstNumber = a != undefined ? Number(a) : 0;
  var lastNumber = b != undefined ? Number(b) : 0;
  //获取小数点后面的位数
  var firstDec = firstNumber.toString().split('.').length > 1 ? firstNumber.toString().split('.')[1].length : 1;
  var lastDes = lastNumber.toString().split('.').length > 1 ? lastNumber.toString().split('.')[1].length : 1;
  //比较小数点最大的位数
  var adec = firstDec > lastDes ? firstDec : firstDec == lastDes ? firstDec : lastDes;
  adec = Math.pow(10,adec)
  return (firstNumber*adec - lastNumber*adec)/adec
}
```

```js
测试结果：
const sub = onSub(5.6666,2.333);
console.log('sub = ',sub)  //sub = 3.3336
```

## <a name='href3'>乘法运算</a> ##

```js
function onMul (a,b) {
  //转为字符串，判断两个数总共有多少小数点。
  var seg1 = a != undefined ? a.toString() : '';  
  var seg2 = b != undefined ? b.toString() : '';
  var m = 0;
  var result = 0;
  m += seg1.split('.').length > 1 ? seg1.split('.')[1].length : 0;
  m += seg2.split('.').length > 1 ? seg2.split('.')[1].length : 0;
  //替换掉小数点，确保都是整数相乘。
  result = Number(seg1.replace(".",""))*Number(seg2.replace(".",""))/Math.pow(10,m);
  return result
}
```

```js
测试结果：
console.log(onMul(1.12,2.21))  // 2.4752
```
