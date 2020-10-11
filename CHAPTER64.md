### [64. 最小路径和-动态规划](https://leetcode-cn.com/problems/minimum-path-sum/)

##### 题目描述

* 给定一个包含非负整数的 m * n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

    * 说明：每次只能向下或者向右移动一步。

    * 示例

        * ```example
            输入:
            [
              [ 1, 3, 1 ],
              [ 1, 5, 1 ],
              [ 4, 2, 1 ]
            ]
            输出: 7
            解释: 因为路径 1 → 3 → 1 → 1 → 1 的总和最小。
            ```



##### 思路

* 从 [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/solution/62-bu-tong-lu-jing-pai-lie-zu-he-dong-tai-gui-hua-/) 知道, 起点到终点, 走的步数是固定的 (向右 m 步, 向下 n 步) . 起点到达任何一个节点的步数也是固定的, 即: 不会因为节点中的数字而改变.
* 那么, 既然路径数固定, 求出所有路径的累加结果, 再比较就好.
    * 那, 如何简化呢? 
        * 从起始点开始, 求起始节点到紧邻其的结点的数字累加最小路径, 直接选中该路径就好. 可以同理, 不断"向右, 下扩展".
            * 因为, 点与点之间的移动是向右或向下, 即: 若要到节点a, 一定会经过其左边或者上面的节点b, c.
            * 那么, 就是求到 b 和 c 的数字累加和最小的路径.
            * 同理, 也是求到 b, c 的左方和上方节点的数字累加和最小的路径.
            * ...
            * 这样不断的向左, 向上推导, 直到到达紧邻起始点的节点.

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
	let n = grid.length;
    let m = grid[0].length;
    let dp = Array.from(new Array(n), () => new Array(m));
    for (let i = 0; i < n; i ++) {
        for (let j = 0; j < m; j ++) {
            if (i != 0 && j != 0) {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            } else if (i == 0 && j != 0) {
                dp[i][j] = dp[i][j - 1] + grid[i][j];
            } else if (i != 0 && j == 0) {
                dp[i][j] = dp[i - 1][j] + grid[i][j];
            } else if (i == 0 && j == 0) {
                dp[i][j] = grid[i][j];
            }
        }
    }
    return dp[n - 1][m - 1];
};
```



##### 复杂度分析

* 时间复杂度: O(n * m), `n = grid.length; let m = grid[0].length;`.`arr.from()` 方法在该程序中的时间复杂度为 O(n * m) . 嵌套的 `for()` 循环中的语句也运行了 n * m 次.
* 空间复杂度: O(n * m), `n = grid.length; let m = grid[0].length;`. 二维数组 `dp` 包含 `n` 个一维数组, 每个一维数组中有 `m` 个元素.



##### 题外话

* [arr.from( arrayLike, mapFn(可选), thisArg(可选) )](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from): 如果 `mapFn` 指定, 新数组中每个元素都会执行该回调函数. 返回值是一个新的数组.

    * 示例:

        * ```javascript
            console.log(Array.from([1, 2, 3], x => x + x));
            // expected output: Array [ 2, 4, 6 ]
            ```



##### 思路, 程序参考

* [JoeLee2017: 动态规划-最短路径问题](https://www.cnblogs.com/lixing-nlp/p/7688549.html)
* [秦时明月: 64. 最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/solution/64-zui-xiao-lu-jing-he-by-alexer-660/)