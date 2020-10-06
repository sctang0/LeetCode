### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

##### 题目描述

* 实现 pow(x, *n*)，即计算 x 的 n 次幂函数。

* 说明：

    - -100.0 < x < 100.0
    - n 是 32 位有符号整数，其数值范围是 [ (−2) ^ 31, 2 ^ 31 − 1 ] 。

* 示例：

    * ```example
        输入: 2.10000, 3
        输出: 9.26100
        ```



#### 思路一：加乘

* 底数 `x` 被 0 分为两种情况，指数 `n` 被 0 分为三种情况，如下：
  * `x = 0`
    * 输出 0
  * `x != 0`
    * `n = 0` ，输出 1
    * `n > 0` ，输出 `x^n`
    * `n < 0` ，输出 `1/(x^n)`



```javascript
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
var myPow = function(x, n) {
    let nSign = 1;
    let sum = parseFloat(1);
    x = parseFloat(x);
    if (x == 0) return 0;
    if (n == 0) return 1;
    if (n < 0) nSign = -1;
    for (let i=0; i<n*nSign; i++) {
        sum *= x;
    }
    if (nSign == -1) {
        return 1 / sum;
    }
    if (nSign == 1) {
        return sum;
    }
};
```



##### 复杂度分析

* 时间复杂度：O(n)，n 为幂函数中的指数。注：此算法超出了时间限制。
* 空间复杂度：O(1)



##### 题外话

* [parseFloat(string)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)：给定值被解析成浮点数。如果给定值不能被转换成数值，则会返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。
    * 注：js 数字只有 Number 类型，双精度浮点数存储在 2 的 -53 次方到 2 的 53 次方之间。



##### 参考

* [秦时明月：50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/solution/50-powx-n-by-alexer-660/)



#### 思路二：迭代

* 相较于思路一，将乘的过程优化了。如下：
  * `xTmp = x`
  * `x = x^2` ，底数不断二次方，同时 `n = parseInt(n/2)` 指数不断除 2 。
  * 直到 `n = 1` ，`return x * xTmp` 。
  * 举例：Pow(x, n) (x=2, n=5)
    * `xTmp = 2`
    * `x = x^2 = 2^2; n = parseInt(n/2) = parseInt(5/2);` ...
    *  当 `n = 1` 时，`x = 16`
    * `return x * xTmp;` ，即 `return 16 * 2`



```javascript
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
var myPow = function(x, n) {
    if (n == 0) {
        return 1;
    }
    x = parseFloat(x);
    if (n < 0) {
        x = parseFloat(1 / x);
        n = -n;
    }
    var subResult = x;
    var result = 1;
    for (var i=n; i>0; i=parseInt(i/2)) {
        if (i&1 == 1) {
            result *= subResult;
        }
        subResult *= subResult;
    }
    return result;
};
```



##### 复杂度分析

* 时间复杂度：O(logn)，n 为幂函数中的指数。
* 空间复杂度：O(1)



##### 题外话

* [parseInt(string, radix)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)：从给定的字符串中解析出的一个整数。



##### 思路、程序参考

* [秦时明月：50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/solution/50-powx-n-by-alexer-660/)