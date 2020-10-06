### [52. N皇后 ii](https://leetcode-cn.com/problems/n-queens-ii/)

##### 题目描述

* n 皇后问题研究的是如何将 n 个皇后放置在 n * n 的棋盘上，并且使皇后彼此之间不能相互攻击。给定一个整数 n ，返回 n 皇后不同的解决方案的数量。

* 示例：

    * ```example
        输入: 4
        输出: 2
        解释: 4 皇后问题存在如下两个不同的解法。
        [
         [ ".Q..",  // 解法 1
           "...Q",
           "Q...",
           "..Q." ],
        
         [ "..Q.",  // 解法 2
           "Q...",
           "...Q",
           ".Q.." ]
        ]
        ```



##### 思路：递归剪枝

需要解决的问题：

* 如何穷尽所有可能的结果？

  * 皇后可以横着吃子的，所以，每一行只能由一个皇后。
  * 那么，就遍历第一行的每一个，并再次基础上遍历下一行的每一个。举例：
    * n = 2
    * 遍历第一行：[["Q."], [".Q"]]
    * 遍历第二行：[["Q.", "Q."], ["Q.", ".Q"], [".Q", "Q."], [".Q", ".Q"]]



* 如何将不符合的结果，在过程中就排除？
  
  * 每一个皇后所在的横、竖、斜（45°  135°），不能有皇后。
  
  * 在得到下一行之后，可以直接检验该行与前面的形成的数组，是否符合要求
  
    * 相关程序：
  
    * ```javascript
      for (let i=row-1; i>=0; i--) {
          if (result[i] == column) {
              return false;
          }
          if (leftColumn>=0 && result[i]==leftColumn) {
              return false;
          }
          if (rightColumn<n && result[i]==rightColumn) {
              return false;
          }
          leftColumn--;
          rightColumn++;
      }
      ```
  
    * 注：程序用数字表示皇后在每个字符串中的位置
  
      * 例如：["Q.", ".Q"] 可表示为 [01]。[["Q.", "Q."], ["Q.", ".Q"], [".Q", "Q."], [".Q", ".Q"]] 可表示为 [00011011]。
      * 当然，最后使用 format 函数，将 [00011011] 转化为了标准结果。



##### 思路、程序参考

* [秦时明月：51. N 皇后](https://leetcode-cn.com/problems/n-queens/solution/51-nhuang-hou-by-alexer-660/)
* [力扣(LeetCode)：51. N 皇后](https://leetcode-cn.com/problems/n-queens/solution/nhuang-hou-by-leetcode/)



```javascript
/**
 * @param {number} n
 * @return {number}
 */
var totalNQueens = function(n) {
    let result = new Array(n);
    let results = [];
    let dfs = (row, column) => {
        let leftColumn = column - 1;
        let rightColumn = column + 1;
        for (let i=row-1; i>=0; i--) {
            if (result[i] == column) {
                return false;
            }
            if (leftColumn>=0 && result[i]==leftColumn) {
                return false;
            }
            if (rightColumn<n && result[i]==rightColumn) {
                return false;
            }
            leftColumn--;
            rightColumn++;
        }
        return true;
    }
    let format = (result) => {
        let tmpResult = [];
        for (let i=0; i<n; i++) {
            let str = '';
            for (let j=0; j<n; j++) {
                if (result[i] == j) {
                    str += 'Q';
                } else {
                    str += '.';
                }
            }
            tmpResult.push(str);
        }
        return tmpResult;
    }
    let Nqueens = (row) => {
        if (row == n) {
            results.push(format(result));
            return;
        }
        for (let j=0; j<n; j++) {
            if (dfs(row, j)) {
                result[row] = j;
                Nqueens(row+1);
            }
        }
    }
    Nqueens(0);
    return results.length;
}
```



##### 复杂度分析

* 时间复杂度：O(n!)，n 为棋盘边的长度。n! 为该题递归遍历次数的上界。
* 空间复杂度：O(n^3)，n 为棋盘边的长度。输出的 results 不确定包含多少个数组，每个数组包含 n 个字符串，每个字符串 n 个字符。



