### [54. 螺旋矩阵-螺旋遍历](https://leetcode-cn.com/problems/spiral-matrix/)

##### 题目描述

* 给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

* 示例：

    * ```example
        输入:
        [
         [ 1, 2, 3 ],
         [ 4, 5, 6 ],
         [ 7, 8, 9 ]
        ]
        输出: [ 1, 2, 3, 6, 9, 8, 7, 4, 5 ]
        ```



##### 思路

顺时针螺旋遍历矩阵，可分解为如下问题：

* 如何实现“转弯”？
* 行走步数的变化如何调整？



1. 如何实现“转弯”？

   * 不难发现，方向变化是固定的。

     * 即：右 -> 下 -> 左 -> 上 -> 右 ... 。

     * 相关程序：

       * ```javascript
         if (turn == 'r') {
             if (j == boundR) {
                 turn = 'd';
             }
         } else if (turn == 'd') {
             if (i == boundD) {
                 turn = 'l';
             }
         }
         ```



2. 行走步数的变化如何调整？

   * “定义 4 个方向边界。当触及边界时即按固定方向转向，且其对应的边界值向内收缩 1 。若没触及边界，即按自身方向继续行走，改变坐标值直到触边界或数字全部遍历过。”

     * 相关语句：

       * ```javascript
         let boundL = 0;                       // 向左移动的边界
         let boundR = matrix[0].length - 1;    // 向右 ...
         let boundU = 0;                       // 向上 ...
         let boundD = matrix.length - 1;       // 向下 ...
         ```

     * 举例：matrix = [ [ 0, 1, 2 ], [ 3, 4, 5 ], [ 6, 7, 8 ] ]
       
       * 顺时针遍历。第一次向右遍历的边界为 2 。一横行遍历完之后，自然，向上遍历的边界收缩 1 ，即 `boundU++` 。同理, 其它方向的遍历。
       
     * 相关语句：

       * ```javascript
         if (turn == 'r') {
             j++;
             if (j == boundR) {
                 boundU++;
                 turn = 'd';
             }
         }
         ```




```javascript
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    let res = [];
    let i = 0;
    let j = 0;
    let n = matrix.length - 1;
    if (n < 0) return [];
    let m = matrix[0].length - 1;
    let turn = (m == 0) ? 'd' : 'r';
    let boundL = 0;
    let boundR = m;
    let boundU = 0;
    let boundD = n;
    
    for (let a = 0; a < (m + 1) * (n + 1); a++) {
        res.push(matrix[i][j]);
        if (turn == 'r') {
            j++;
            if (j == boundR) {
                boundU++;
                turn = 'd';
            }
        } else if (turn == 'd') {
            i++;
            if (i == boundD) {
                boundR--;
                turn = 'l';
            }
        } else if (turn == 'l') {
            j--;
            if (j == boundL) {
                boundD--;
                turn = 'u';
            }
        } else if (turn == 'u') {
            i--;
            if (i == boundU) {
                boundL++;
                turn = 'r';
            }
        }
    }
    return res;
};
```



##### 复杂度分析

* 时间复杂度：O(n * m)，`n = matrix.length - 1; m = matrix[0].length - 1;` 。遍历数组 matrix 一次的时间复杂度。
* 空间复杂度：O(n * m)，`n = matrix.length - 1; m = matrix[0].length - 1;` 。res 包含数组 matrix 所有元素。



##### 思路、程序参考

* [cc123nice：54. 旋转矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/luo-xuan-ju-zhen-ji-yi-li-jie-92100-by-caifeng123/)
* [力扣官方题解：54. 旋转矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/luo-xuan-ju-zhen-by-leetcode-solution/)