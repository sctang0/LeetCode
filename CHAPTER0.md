### 题外话

##### 方法

* [str.charCodeAt(index)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)：指定 `index` 处字符( `str[index]` )的 UTF-16 代码单元值的一个数字；如果 `index` 超出范围，`charCodeAt()` 返回 `NaN` 。
  * `index`：一个大于等于 `0`，小于字符串长度的整数。如果不是一个数值，则默认为 `0`。
  * 注：在历史版本中（如 JavaScript 1.2），`charCodeAt` 返回一个数字，表示给定 index 处字符的 ISO-Latin-1 编码值。ISO-Latin-1 编码集范围从 `0` 到 `255`。开头的 `0` 到 `127` 直接匹配 ASCII 字符集。



* [continue](https://www.w3school.com.cn/js/js_break.asp): “跳过”循环中的一个迭代, 然后继续循环中的下一个迭代.



* [arr.fill()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill): 用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。

    * ```javascript
        let tmp = [ 1, 2, 3 ];
        tmp = tmp.fill(0);
        console.log(tmp);
        /**
         * stdout: [ 0, 0, 0 ]
         */
        ```



* [Math.floor(x) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)：`x` 为一个数字，方法返回小于或等于 `x` 的最大整数。



* [arr.includes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)：方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 `true` ，否则返回 `false` 。



* [arr.join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)：将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。

  * ```javascript
    const elements = ['Fire', 'Air', 'Water'];
    console.log(elements.join(''));
    // expected output: "FireAirWater"
    ```

  * [复杂度分析](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.5)

    * 时间复杂度: O(n), `n = arr.length` . 用 `while` 循环, 依次将数组 `arr` 中元素, 存放到返回字符串 `R` 末尾.
    * 空间复杂度: O(n * m), `n = arr.length; m = arr[n].length` . 定义返回字符串 `R`,  储存数组 `arr` 中所有元素.



* [Number()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number): 当作为一个函数使用时, `Number(value)` 会将 `value` 转换为数字类型. 如果值不能被转换, 就返回 `NaN` .



* [parseFloat(string)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)：给定值被解析成浮点数。如果给定值不能被转换成数值，则会返回 `NaN` 。
    * 注：js 数字只有 Number 类型，双精度浮点数存储在 2 的 -53 次方到 2 的 53 次方之间。



* [parseInt(string, redix(可选))](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt): 解析一个字符串并返回指定基数的十进制整数.



* [arr.pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop): `pop()` 方法从数组中删除最后一个元素, 并返回该元素的值. 此方法更改数组的长度.
  * 此方法更改数组 `arr` , 变为不包含数组最后一个元素的数组 (若 `arr.length >= 1`) .
  * [复杂度分析](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6)
      * 时间复杂度: O(1). `arr.pop()` 根据 `length` 属性来确定最后一个元素的位置.
      * 空间复杂度: O(1). `arr.pop()` 调用过程中, 并没有开辟一块 `length - 1` 大小的空间, 来存储前 `length - 1` 个元素. 而是, 直接对数组 `arr` 进行删值操作.



* [arr.push(element1, ..., elementN)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push): 将一个或多个元素添加到数组的末尾, 并返回该数组的新长度.
  * elementN: 被添加到数组末尾的元素
  * 返回值: 当调用该方法时, 新的 length 属性值将被返回.
  * [复杂度分析](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7)
      * 时间复杂度: O(n), `n = element.length` . `arr.push()` 根据 `length` 属性来确定从哪里插入给定值. `arr.push()` 内部定义数组 `items` 来从左至右储存 `element1 ~ N` 的值. 并用 `while` 循环依次加入数组 `arr` 末尾.
      * 空间复杂度: O(n), `n = element.length` . `arr.push()` 调用过程中, 定义数组 `items` 来存储 `element1 ~ N` 的值.



* [arr.reverse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse): 将数组中元素的位置颠倒，并返回该数组.

    * ```javascript
        let tmp = [ "one", "two", "three" ];
        console.log(tmp.reverse());
        /**
         * stdout: [ "three", "two", "one" ]
         */
        ```



* [arr.shift()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)：从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。从数组中删除的元素; 如果数组为空则返回 undefined 。



* [arr.slice(begin, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的浅拷贝（包括 `begin`，不包括`end`）。原始数组不会被改变。
  * 如果省略 `begin`，则 `slice` 从索引 `0` 开始。如果 `begin` 大于原数组的长度，则会返回空数组。
  * 如果 `end` 被省略，则 `slice` 会一直提取到原数组末尾。如果 `end` 大于数组的长度，`slice` 也会一直提取到原数组末尾。



* [arr.sort([compareFunction])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)：用[原地算法](https://juejin.im/entry/6844903507439419399#comment)对数组的元素进行排序，并返回数组。上方程序中的是以一维数组中的第一个元素为参考，来进行升序排序。
  * `compareFunction`（可选）：用来指定按某种顺序进行排列的函数。
  * 返回值：排序后的数组。请注意，数组已原地排序，并且不进行复制。
  * 注：由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。



* [string.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split): 使用指定的分隔符字符串将 `arr` 对象分割成子字符串数组.
    * [复杂度分析](https://www.ecma-international.org/ecma-262/5.1/#sec-15.5.4.14)
        * 时间复杂度: O(n), `n = string.length` . 在 `string` 元素, 传入返回数组 `arr` 过程中, 遍历了字符串 `string` .
        * 空间复杂度: O(n), `n = string.length` . 定义返回数组 `arr` . 特殊情况, `string` 字符全为分隔字符, `arr` 长度为 `string.length` , 元素都为 `''` . 平均情况, `arr` 包含 `string.length / 2` 个字符.



* [array.splice(start, deleteCount, item1, item2, ...)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice): 通过删除, 替换, 添加来修改原数组.

    * `start` : 修改开始的位置(从0计数).

    * `deleteCount(可选)` : 整数, 表示要移除的数组元素的个数.

    * `item1, item2, ... (可选)` : 要添加进数组的元素, 从 `start` 位置开始. 如果不指定, 则 `splice()` 将只删除数组元素.

    * 返回值 : 由被删除元素组成的一个数组.

    * ```javascript
        const months = ['Jan', 'March', 'April', 'June'];
        months.splice(1, 0, 'Feb');
        console.log(months);
        // expected output: Array ["Jan", "Feb", "March", "April", "June"]
        
        months.splice(4, 1, 'May');
        console.log(months);
        // expected output: Array ["Jan", "Feb", "March", "April", "May"]
        
        ```



* [Math.sqrt(number)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/sqrt): 返回数 `number` 的平方根.
    * [Math.sqrt()](https://github.com/v8/v8/blob/master/test/mjsunit/math-sqrt.js) Chrome v8 程序链接



* [arr.trim()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/Trim): 删除字符串 `arr` 两端的空格字符.



* [arr.unshift()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift): 将一个或多个元素添加到数组的开头.

    * ```javascript
        let tmp = [ 1, 2, 3 ];
        tmp.unshift('a', 'b');
        console.log(tmp);
        
        /**
         * stdout: [ "a", "b", 1, 2, 3 ]
         */
        ```



##### 概念

* [动态规划](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92): 为避免多次解决重复的子问题, 结果会被都逐渐计算并保存.



* [JavaScript 链式栈优点](https://blog.csdn.net/zhangxiangDavaid/article/details/28679027)
    * 一般, 链式栈与顺序栈相比, 优点是可以动态扩容.
        * 不过, JavaScript 数组长度是无限的, 只要内存允许. 即使设置了数组长度, 如果需要的话, 随后该长度也可以自动增长. 无需担心溢出.
            * 所以, 在 JavaScript 中, 链式栈的优点
                * 插入, 删除灵活
                * 物理地址不必相连



* [牛顿法](https://en.citizendium.org/wiki/Newton's_method#Computational_complexity): 一个解决函数值为零的方法, 换一句话说解决方程 ![img](https://en.citizendium.org/images/math/f/d/0/fd05d8d90456c441c8f10641bd8576bc.png) .
    * a method for finding where a function obtains the value zero, or in other words, solving the equation ![img](https://github.com/sctang0/LeetCode/blob/master/images/chapter69.3.png).



* [浅拷贝](https://juejin.im/post/6844904197595332622)：浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。
  * 深拷贝：将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。
  * <img src="https://github.com/sctang0/LeetCode/blob/master/images/chapter46.1.3" alt="浅拷贝 来源: https://juejin.im/post/6844904197595332622" width="569" />
  * <img src="https://github.com/sctang0/LeetCode/blob/master/images/chapter46.1.4" alt="深拷贝 来源: https://juejin.im/post/6844904197595332622" width="569" />



* [数组长度](https://zhidao.baidu.com/question/499788673)

    * JavaScript 数组的长度可以是无限的, 只要内存允许的话. 数组的初始长度可以设置, 如果需要, 随后该长度可以自动增长. 使用数字串当作数组的索引, 等价于直接使用数字索引.

    * JavaScript 数组实际上是个 Key-Value 对. Key 不仅可以使数字, 还可以是其它对象.

        * ```javascript
            var arr = new Array(2);
            arr[0] = 1;
            arr['second'] = 2;
            arr['third'] = 3;
            console.log(arr['0'] + ' ' + arr['second'] + [' '] + arr['third']);
            console.log(arr.length);
            /**
             * console:
                 1 2 3
                 2
             */
            ```



* [贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)：一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法。



* [栈结构](https://juejin.im/post/6844904129605828615)：一个递归函数，在函数执行过程中，需要多次进行自我调用，在高级语言程序中，调用函数和被调用函数之间的链接与信息交换都是通过栈来进行。
  * 为了保证递归函数的正确执行，系统就要建立一层一层的的工作栈，每层工作栈保留了所有的实参，局部变量，以及上一层的返回地址，形成工作记录压入栈顶，就形成了递归工作栈。
  * 举例：
    * <img src="https://github.com/sctang0/LeetCode/blob/master/images/chapter46.1.1" alt="递归工作栈: 程序 来源: https://juejin.im/post/6844904129605828615" width="300" />
    * <img src="https://github.com/sctang0/LeetCode/blob/master/images/chapter46.1.2" alt="递归工作栈: 图片表示 来源: https://juejin.im/post/6844904129605828615" width="375" />



* [运算符优先级](https://baike.baidu.com/item/%E8%BF%90%E7%AE%97%E7%AC%A6%E4%BC%98%E5%85%88%E7%BA%A7)