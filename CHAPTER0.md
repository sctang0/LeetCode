### 题外话

##### 方法

* [str.charCodeAt(index)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)：指定 `index` 处字符( `str[index]` )的 UTF-16 代码单元值的一个数字；如果 `index` 超出范围，`charCodeAt()` 返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。
  * `index`：一个大于等于 `0`，小于字符串长度的整数。如果不是一个数值，则默认为 `0`。
  * 注：在历史版本中（如 JavaScript 1.2），`charCodeAt` 返回一个数字，表示给定 index 处字符的 ISO-Latin-1 编码值。ISO-Latin-1 编码集范围从 `0` 到 `255`。开头的 `0` 到 `127` 直接匹配 ASCII 字符集。



* [parseFloat(string)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)：给定值被解析成浮点数。如果给定值不能被转换成数值，则会返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。
  * 注：js 数字只有 Number 类型，双精度浮点数存储在 2 的 -53 次方到 2 的 53 次方之间。



* [parseInt(string, radix)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)：从给定的字符串中解析出的一个整数。



* [Math.floor(x) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)：`x` 为一个数字，方法返回小于或等于 `x` 的最大整数。



* [arr.includes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)：方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。



* [arr.join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)：将一个数组（或一个[类数组对象](https://developer.mozilla.org/zh-CN//docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)）的所有元素连接成一个字符串并返回这个字符串。

  * ```javascript
    const elements = ['Fire', 'Air', 'Water'];
    console.log(elements.join(''));
    // expected output: "FireAirWater"
    ```



* [arr.pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)：`**pop()**`方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
  * 此方法更改数组 `arr` ，变为不包含数组最后一个元素的数组（若 `arr.length>=1`）。



* [arr.push(element1, ..., elementN)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)：将一个或多个元素添加到数组的末尾，并返回该数组的新长度。
  * elementN：被添加到数组末尾的元素
  * 返回值：当调用该方法时，新的 length 属性值将被返回。



* [arr.slice(begin, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`）。原始数组不会被改变。
  * 如果省略 `begin`，则 `slice` 从索引 `0` 开始。如果 `begin` 大于原数组的长度，则会返回空数组。
  * 如果 `end` 被省略，则 `slice` 会一直提取到原数组末尾。如果 `end` 大于数组的长度，`slice` 也会一直提取到原数组末尾。



##### 概念

* [浅拷贝](https://juejin.im/post/6844904197595332622)：浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。
  * 深拷贝：将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。
  * <img src="https://user-gold-cdn.xitu.io/2020/3/1/170965259fb768fd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="浅拷贝" width="569" />
  * <img src="https://user-gold-cdn.xitu.io/2020/3/1/1709652a7948d1b8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="深拷贝" width="569" />



* [贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)：一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法。



* [栈结构](https://juejin.im/post/6844904129605828615)：一个递归函数，在函数执行过程中，需要多次进行自我调用，在高级语言程序中，调用函数和被调用函数之间的链接与信息交换都是通过栈来进行。
  * 为了保证递归函数的正确执行，系统就要建立一层一层的的工作栈，每层工作栈保留了所有的实参，局部变量，以及上一层的返回地址，形成工作记录压入栈顶，就形成了递归工作栈。
  * 举例：
    * <img src="https://user-gold-cdn.xitu.io/2020/4/16/1718361ee0e4e060?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="递归工作栈: 程序" width="300" />
    * <img src="https://user-gold-cdn.xitu.io/2020/4/16/171836205787161b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="递归工作栈: 图片表示" width="375" />
