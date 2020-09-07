### 题外话

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