### 题外话

* [Math.floor(x) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)：`x` 为一个数字，方法返回小于或等于 `x` 的最大整数。

* [arr.includes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)：方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

* [arr.pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)：`**pop()**`方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
  * 此方法更改数组 `arr` ，变为不包含数组最后一个元素的数组（若 `arr.length>=1`）。

* [arr.slice(begin, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`）。原始数组不会被改变。
  * 如果省略 `begin`，则 `slice` 从索引 `0` 开始。如果 `begin` 大于原数组的长度，则会返回空数组。
  * 如果 `end` 被省略，则 `slice` 会一直提取到原数组末尾。如果 `end` 大于数组的长度，`slice` 也会一直提取到原数组末尾。