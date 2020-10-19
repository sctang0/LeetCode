### [66. 加一-倒序遍历](https://leetcode-cn.com/problems/plus-one/)

##### 题目描述

* 给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

    * 最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

    * 你可以假设除了整数 0 之外，这个整数不会以零开头。

    * 示例：

        * ```javascript
            输入: [ 1, 2, 3 ]
            输出: [ 1, 2, 4 ]
            解释: 输入数组表示数字 123。
            ```




##### 思路: 倒序遍历

* 当遇到 9 时, 如何"进位"?
    * 将该位清零, 遍历中的下一位加一.
    * 若, 其下一位也为 9 , 则同样清零, 继续用同样的模式遍历. 直到遇到第一个非 9 的元素.
* 当数组 `digits` 元素全为 9 时, 如何输出?
    * 定义一个长度为 `digist.length + 1` , 首元素为 1 , 其他元素为 0 的数组. 
    * 输出该数组.

```javascript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    let i = digits.length - 1;
    while (i >= 0) {
        if (digits[i] != 9) {
            digits[i] ++;
            return digits;
        }
        if (digits[i] == 9) {
            digits[i] = 0;
        }
        i --;
    }
    digits.unshift(1);
    return digits;
};
```

##### 复杂度分析

* 时间复杂度: O(n) , `n = digits.length` .
    * 最好时间复杂度 O(1) . 此时, 数组 `digits` 的末尾元素不为 9 .
    * 最坏时间复杂度 O(n) . 此时, 数组 `digist` 的元素全为 9 . [`arr.unshift()`](https://tc39.es/ecma262/#sec-array.prototype.unshift) 方法调用的时间复杂度为 O(n) .
    * 平均时间复杂度 O(n) .
* 空间复杂度:
    * O(1) . 此时, 数组 `digits` 元素不全为 9 .
    * O(n) , `n = digits.length + 1` . 此时, 数组 `digits` 元素全为 9 . [`arr.unshift()`](https://tc39.es/ecma262/#sec-array.prototype.unshift) 方法调用的空间复杂度为 O(n) .



##### 题外话

* [arr.unshift()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift): 将一个或多个元素添加到数组的开头.

    * ```javascript
        let tmp = [ 1, 2, 3 ];
        tmp.unshift('a', 'b');
        console.log(tmp);
        
        /**
         * stdout: [ "a", "b", 1, 2, 3 ]
         */
        ```
