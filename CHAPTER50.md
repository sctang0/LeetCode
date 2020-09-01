### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

#### 思路一：加乘

* 底数 `x` 被 0 分为两种情况，指数 `n` 被 0 分为三种情况，如下：
  * `x = 0`
    * 输出 0
  * `x != 0`
    * `n = 0` ，输出 1
    * `n > 0` ，输出 `x^n`
    * `n < 0` ，输出 `1/(x^n)`



##### 题外话

* [parseFloat(string)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)：给定值被解析成浮点数。如果给定值不能被转换成数值，则会返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。
  * 注：js 数字只有 Number 类型，双精度浮点数存储在 2 的 -53 次方到 2 的 53 次方之间。



##### 参考

* [秦时明月：50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/solution/50-powx-n-by-alexer-660/)



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

* 时间复杂度：O(n)，n 为幂函数的指数。注：此算法超出了时间限制。
* 空间复杂度：O(1)



#### 思路二：



##### 题外话

* [parseInt(string, radix)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)：从给定的字符串中解析出的一个整数。



##### 思路、程序参考

* [秦时明月：50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/solution/50-powx-n-by-alexer-660/)

