### [70. 爬楼梯-动态规划, 公式](https://leetcode-cn.com/problems/climbing-stairs/)

##### 题目描述

* 假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

* 每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

    * 注意：给定 *n* 是一个正整数。

* 示例：

    * ```example
        输入： 2
        输出： 2
        解释： 有两种方法可以爬到楼顶。
               1.  1 阶 + 1 阶
               2.  2 阶
        ```

    * ```example
        输入： 3
        输出： 3
        解释： 有三种方法可以爬到楼顶。
               1.  1 阶 + 1 阶 + 1 阶
               2.  1 阶 + 2 阶
               3.  2 阶 + 1 阶
        ```



##### 思路一: 动态规划

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    let dp = new Array(n + 1);
    dp[0] = 1;
    dp[1] = 2;
    for (let i = 2; i <= n; i ++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n - 1];
}
```

##### 复杂度分析

* 时间复杂度: O(n)
* 空间复杂度: O(1)



##### 思路, 程序参考

* [画手大鹏: 70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/solution/hua-jie-suan-fa-70-pa-lou-ti-by-guanpengchn/)



##### 思路二: 公式

* 爬楼梯对应的数列为: 1  2  3  5  8  13 21 34 55 89 ...
    * 满足 `a[n] = a[n - 1] + a[n - 2]`
    * 对应斐波拉且通项公式为
        * ![chapter70.1](https://github.com/sctang0/LeetCode-Private/blob/master/images/01-99/chapter70.1.png)
            * 注意: 该公式从 1 开始计数. 即, ![chapter70.2](https://github.com/sctang0/LeetCode-Private/blob/master/images/01-99/chapter70.2.png)

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    let sqrtFive = Math.sqrt(5);
    let p = (5 + sqrtFive) / 10;
    let q = (5 - sqrtFive) / 10;
    let fibN = p * Math.pow((1 + sqrtFive) / 2, n) + q * Math.pow((1 - sqrtFive) / 2, n);
    return Math.round(fibN);
}
```

##### 复杂度分析

* 时间复杂度: O(logn). `Math.pow()` 时间复杂度为 O(logn) .
* 空间复杂度: O(1)



##### 题外话

* [斐波拉且数列](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97): `a[1] = 0, a[2] = 1, a[n] = a[n - 1] + a[n - 2]` 形成的数列 `0  1  1  2  3  5  8  13  ...`
* [Math.pow(base, exponent)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/pow): 返回基数 (`base`) 的指数 (`exponent`) 次幂, 即 `base ^ exponent` .
* [Math.round(x)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/round): 返回 `x` 四舍五入后最接近的整数.
* [zhaozhengcc: 数列特征方程](https://blog.csdn.net/bigtiao097/article/details/77113874)
    * 推导斐波拉且通项公式的方法来源于此



##### 思路, 程序参考

* [画手大鹏: 70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/solution/hua-jie-suan-fa-70-pa-lou-ti-by-guanpengchn/)
* [力扣官方题解: 70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/solution/pa-lou-ti-by-leetcode-solution/)

##### 公式编辑器

* [Codecogs](https://www.codecogs.com/latex/eqneditor.php?lang=zh-cn)