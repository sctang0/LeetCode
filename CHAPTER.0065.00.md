### [65. 有效数字-数据类型判断, 分组判断](https://leetcode-cn.com/problems/valid-number/)

##### 题目描述

* 验证给定的字符串是否可以解释为十进制数字。

    * 说明: 我们有意将问题陈述地比较模糊。在实现代码之前，你应当事先思考所有可能的情况。这里给出一份可能存在于有效十进制数字中的字符列表：

        * 数字 0-9
        * 指数 - "e"
        * 正/负号 - "+"/"-"
        * 小数点 - "."
            * 当然，在输入中，这些字符的上下文也很重要。

    * 示例：
        * ```example
            "0" => true
            " 0.1 " => true
            "abc" => false
            "1 a" => false
            "2e10" => true
            " -90e3   " => true
            " 1e" => false
            "e3" => false
            " 6e-1" => true
            " 99e2.5 " => false
            "53.5e93" => true
            " --6 " => false
            "-+3" => false
            "95a54e53" => false
            ```



##### 思路一: 数据类型判断

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isNumber = function(s) {
    return (Number(s) === 0 || !!Number(s)) && (s.trim() !== "");
};
```

##### 复杂度分析

* 时间复杂度: O(n), `n = s.length` . [`arr.trim()`](https://www.ecma-international.org/ecma-262/5.1/#sec-15.5.4.20) 的时间复杂度为 O(n) , [`Number()`](https://tc39.es/ecma262/#sec-number-objects) 的时间复杂度可能为 O(1) .
* 空间复杂度: O(n), `n = s.length` . [`arr.trim()`](https://www.ecma-international.org/ecma-262/5.1/#sec-15.5.4.20) 的空间复杂度为 O(n) , [`Number()`](https://tc39.es/ecma262/#sec-number-objects) 的空间复杂度可能为 O(n) .



##### 题外话

* [arr.trim()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/Trim): 删除字符串 `arr` 两端的空格字符.

* [Number()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number): 当作为一个函数使用时, `Number(value)` 会将 `value` 转换为数字类型. 如果值不能被转换, 就返回 `NaN` .

* `!!Number(value)` 的输出情况

    * ```javascript
        console.log(Number('string'));      // stdout: NaN
        console.log(!Number('string'));     // stdout: true
        console.log(!!Number('string'));    // stdout: false
        ```




##### 思路, 程序参考

* [raphaeltnfsh: 65. 有效数字](https://leetcode.com/problems/valid-number/discuss/23726/Share-my-200ms-one-line-solution-in-JavaScript)



##### 思路二: 分组判断

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isNumber = function(s) {
    'use strict';
    function isSimpleNumber(str, isInt) {
        let dotCount = 0;
        let digitCount = 0;
        let startIndex = (str[0] === '-' || str[0] === '+') ? 1 : 0;
        for (let i = startIndex; i < str.length; i ++) {
            if (str[i] === '.') dotCount ++;
            if (str[i] >= '0' && str[i] <= '9') digitCount ++;
            if ((str[i] < '0' || str[i] > '9') && str[i] !== '.') return false;
        }
        return digitCount > 0 && ((isInt && dotCount === 0) || (!isInt && dotCount <= 1));
    }
    s = s.trim();
    if (s.includes('e')) {
        const parts = s.split('e');
        if (parts.length !== 2 || parts[0] === '' || parts[1] === '') {
            return false;
        }
        return isSimpleNumber(parts[0]) && isSimpleNumber(parts[1], true);
    } else {
        return isSimpleNumber(s);
    }
};
```

##### 复杂度分析

* 时间复杂度: O(n), `n = s.length` . `isSimpleNumber` 函数执行过程中遍历数组 `str` 一遍.
* 空间复杂度: 
    * 若 `s` 中不包含字符 'e' , 空间复杂度为 O(1) .
    * 若 `s` 中包含字符 'e' , 空间复杂度为 O(n) , `n = s.length` . 此时, 数组 `parts` 存储 `s` 中的除 'e' 以外的字符. 



##### 题外话

* [arr.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split): 使用指定的分隔符字符串将 `arr` 对象分割成子字符串数组.



##### 思路, 程序参考

* [antipin: 65. 有效数字](https://leetcode.com/problems/valid-number/discuss/23926/Easy-clean-solution-on-JavaScript-with-explanation-of-idea)