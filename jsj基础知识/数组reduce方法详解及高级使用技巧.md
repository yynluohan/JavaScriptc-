### JS数组reduce()方法使用 ###

+ 语法

  ` list.reduce(callback,[initalValue]) `  //list不能为空数组

   reduce为数组中的每一个元素依次执行回调函数，回调函数接收四个参数（初始值、当前
处理的元素值、当前元素的索引、调用reduce的数组）

 ```

    callback (执行数组中的每个元素，包含四个参数)

    1、previousValue (上一次调用函数返回的值，或者是提供的初始值initalValue)
    2、currentValue (当前数组正在处理得元素)
    3、index (当前处理的元素所在的索引)
    4、array (调用reduce的数组)

    initalValue (作为第一次调用callback函数的初始值)

 ```

 + initalValue 参数

   1、无参数时

   ```js

    var list = [1,2,3,4];
    var sum = list.reduce(function(prev,current,index) {
      console.log(prev,current,index);
      return prev + current
    })
    console.log(sum);

   ```
   打印结果：
   1 2 1    //第一次无默认值，prev是1
   3 3 2
   6 4 3
   10

   注意：这里循环了三次。

   2、有参数时

  ```js

  var list = [1,2,3,4];
  var sum = list.reduce(function(prev,current,index) {
    console.log(prev,current,index);
    return prev + current
  },0) //这里设置了初始值
  console.log(sum);

  ```

  打印结果：
  0 1 0   //第一次有默认值，prev是0
  1 2 1
  3 3 2
  6 4 3
  10

  注意：这里循环了四次。


  + reduce简单用法
