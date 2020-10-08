### [63. 不同路径 II-动态规划](https://leetcode-cn.com/problems/unique-paths-ii/)

##### 题目描述

* 一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

* 现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

    * 说明：m 和 n 的值均不超过 100。

    * 示例：

        * ```example
            输入:
            [
              [ 0, 0, 0 ],
              [ 0, 1, 0 ],
              [ 0, 0, 0 ]
            ]
            输出: 2
            解释:
            3x3 网格的正中间有一个障碍物。
            从左上角到右下角一共有 2 条不同的路径：
            1. 向右 -> 向右 -> 向下 -> 向下
            2. 向下 -> 向下 -> 向右 -> 向右
            ```



##### 思路

* 路障对应节点的的路径数设置为 0 .
    * 节点对应的数, 表示从左上角能到达该点的路径数. 将障碍对应节点的路径数设置为 0 , 也就是从左上角到达该点的路径数为 0 , 即绕过该点. 
    * 之后, 加了这个 0 的路径都继承了一个特点, 绕过该结点(路障).

```javascript
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    let n = obstacleGrid.length;
    let m = obstacleGrid[0].length;
    let dp = new Array(n);
    for (let i = 0; i < n; i ++) {
        dp[i] = new Array(m).fill(0);
    }
    dp[0][0] = obstacleGrid[0][0] == 0 ? 1 : 0;
    if (dp[0][0] == 0) {
        return 0;
    }
    for (let i = 1; i < m; i ++) {
        if (obstacleGrid[0][i] != 1) {
            dp[0][i] = dp[0][i - 1];
        }
    }
    for (let i = 1; i < n; i ++) {
        if (obstacleGrid[i][0] != 1) {
            dp[i][0] = dp[i - 1][0];
        }
    }
    for (let i = 1; i < n; i ++) {
        for (let j = 1; j < m; j ++) {
            if (obstacleGrid[i][j] != 1) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }
    return dp[n - 1][m - 1];
};
```



##### 复杂度分析

* 时间复杂度: O(n * m). `dp[i][j] = dp[i - 1][j] + dp[i][j - 1];` 最多运行了 ( n - 1 ) * ( m - 1 ) 次.
* 空间复杂度: O(n * m). 二维数组 `dp` 包含 `n` 个一维数组, 每个一维数组里有 `m` 个元素.



##### 思路, 程序参考

* [秦时明月: 63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/solution/63-bu-tong-lu-jing-ii-by-alexer-660/)

* [狗大王: 63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/solution/jian-ji-biao-ge-jie-shi-dong-tai-gui-hua-dpsi-lu-f/)