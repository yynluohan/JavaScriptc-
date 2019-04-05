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

    1、数组求和、求积。

      ```js

        var list = [1,2,3,4];
        var sum = list.reduce((x,y) => x + y);
        var mul = list.reduce((x,y) => x*y);
        console.log(sum);  //10
        console.log(mul);  //24

      ```

    + reduce的高级用法

      1、统计数组中每个元素出现的次数。

        ```js

          var list = ['a','b','c','d','a','c','a'];

          var nameNum = list.reduce(function(prev,cur) {
            if(cur in prev) {
              prev[cur] ++
            } else {
              prev[cur] = 1
            }
            return prev ;
          },{})

          console.log(nameNum);  //{a: 3, b: 1, c: 2, d: 1}

        ```

      2、数组去重。

       ```js

         var list = [1,2,3,4,4];
         var newList = list.reduce(function(prev,cur) {
           if(prev.includes(cur)) {   //使用了ES6 includes方法，可找到传入的值返回true，反之为false
             return prev
           } else {
             prev.push(cur)
           }
           return prev;
         },[])
         console.log(newList);  // [1,2,3,4]

       ```

       3、将二维数组转为一维数组。

        ```js

           var list = [1,2,[3,4],[5,6]];
           var newList = list.reduce(function(prev,cur) {
             return prev.concat(cur)
           },[])
           console.log(newList); // [1,2,3,4,5,6]

        ```

        4、将多维数组转化成一位数组。

         ```js

            var list = [[1,2],[3,4],[5,[6,7,[8,9]]]];
            const newList = function(arr){
              return arr.reduce(function(prev,cur) {
                return prev.concat(Array.isArray(cur) ? newList(cur) : cur);
              },[])
            }
            console.log(newList(list)); // [1,2,3,4,5,6,7,8,9]

         ```

         5、求数组中对象的属性和。

          ```js

            var list = [
              {
                name:"张三",
                age:16
              },
              {
                name: "李四",
                age:20
              },
              {
                name: "王五",
              }
            ]

            var sum = list.reduce(function(prev,cur) {
              return prev + (cur.age || 0)
            },0)
            console.log(sum);  // 36

          ```
