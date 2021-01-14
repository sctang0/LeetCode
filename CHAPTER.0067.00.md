### [67. 二进制求和-逐级相加](https://leetcode-cn.com/problems/add-binary/)

##### 题目描述

* 给你两个二进制字符串，返回它们的和（用二进制表示）。

    * 输入为非空字符串且只包含数字 1 和 0 。

    * 提示：

        * 每个字符串仅由字符 '0' 或 '1' 组成。
        * `1 <= a.length, b.length <= 10 ^ 4`
        * 字符串如果不是 "0" ，就都不含前导零。

    * 示例：

        * ```example
            输入: a = "11", b = "1"
            输出: "100"
            
            输入: a = "1010", b = "1011"
            输出: "10101"
            ```

##### 思路

* 定义变量 `tmp` 保存进位的值, 定义数组 `res` 保存相加得到的和.
  
    * <div align = center>
            <img src="https://github.com/sctang0/LeetCode-Private/blob/master/images/chapter67.jpg" alt="chapter67" width="75%" /><div>
* 由上图可知, 程序的最小重复单元:
    * 保存进位值: `tmp =Math.floor( ( a[i] + b[j] + tmp) / 2 ) `
    * 保存每次相加的结果: `res[k] = ( a[i] + b[j] + tmp ) % 2`
        * 需要注意的一点是, 数组 `res` 的长度无法提前知道.
            * 解决办法是程序先从左到右保存结果, 在输出的时候使用 [`arr.reverse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) 方法将数组中元素的位置颠倒.


```javascript
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function(a, b) {
    let res = '';
    let tmp = 0;
    let i = a.length - 1;
    let j = b.length - 1;
    while (i >= 0 || j >= 0) {
        let sum = tmp;
        sum += i >= 0 ? parseInt(a[i]) : 0;
        sum += j >= 0 ? parseInt(b[j]) : 0;
        res += sum % 2;
        tmp = Math.floor(sum / 2);
        i --;
        j --;
    }
    res += tmp == 1 ? tmp : '';
    return res.split('').reverse().join('');
};
```

##### 复杂度分析

* 时间复杂度: O(n), `n = a.length >= b.length ? a.length : b.length` . 方法 [parseInt()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.1.2.2) 调用的参数数组长度为 1 , 时间复杂度为 O(1) .
* 空间复杂度: O(n), `n = a.length >= b.length ? a.length : b.length` .



##### 题外话

* [parseInt(string, redix(可选))](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt): 解析一个字符串并返回指定基数的十进制整数.
* [arr.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split): 使用指定的分隔符字符串将 `arr` 对象分割成子字符串数组.
* [arr.reverse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse): 将数组中元素的位置颠倒，并返回该数组.
* [arr.join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)：将一个数组 (或一个类数组对象) 的所有元素连接成一个字符串并返回这个字符串。



##### 思路, 程序参考

* [画手大鹏: 67. 二进制求和](https://leetcode-cn.com/problems/add-binary/solution/hua-jie-suan-fa-67-er-jin-zhi-qiu-he-by-guanpengch/)