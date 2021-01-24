* ### [0.3 数组的浅复制与深复制](https://github.com/wangzheng0822/algo/blob/master/javascript/05_array/Array.md)

    * 浅复制: 把数组赋给另外一个数组, 然后改变其中一个数组的值, 另一数组也会随之改变.
    * 深复制: 不改变原来的数组而去创建一个新的数组.

    ```javascript
    /**
     * 浅复制
     */
    var num = [ 1, 2, 3 ];
    var newNum = num;
    num[0] = 10;
    console.log(newNum[0]);
    /**
     * std
         10
     */
    
    /**
     * 深复制
     */
    function copy(arr, newArr) {
      for(let i = 0; i < arr.length; ++ i){
        newArr[i] = arr[i];
      }
    }
    var num = [ 1, 2, 3 ];
    var newNum = [];
    copy(num, newNum);
    num[0] = 10;
    console.log(newNum[0]);
    /**
     * std
         1
     */
    ```

    

    ##### 思路, 程序参考

    * [wangzheng0822: Array](https://github.com/wangzheng0822/algo/blob/master/javascript/05_array/Array.md)

    * 注: 程序输出由 WebStorm 编译