### [54. 螺旋矩阵 - 螺旋遍历](https://leetcode-cn.com/problems/spiral-matrix/)

##### 思路

如果要按顺时针螺旋顺序遍历矩阵，会面临如下问题：

* 如何实现“转弯”？即如何从一个行进方向，转换为另外一个行进方向？
* 行走步数的变化如何调整？



1. 如何实现“转弯”？即如何从一个行进方向，转换为另一个行进方向？

   * 不难发现，前一个行进方向会固定对应着下一个行进方向。总的方向就是顺时针。

     * 具体的方向的转变就是：右 -> 下 -> 左 -> 上 -> 右 ... 。

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

     * 那么，如何设定边界？

       * 相关程序：

         * ```javascript
           let boundL = 0;                       // 向左移动的边界
           let boundR = matrix[0].length - 1;    // 向右 ...
           let boundU = 0;                       // 向上 ...
           let boundD = matrix.length - 1;       // 向下 ...
           ```

     * 为何设定的边界的值会不同？

       * 四个方向上，“坐标”变化的情况不同。
       
       * 这里的边界并不是某个坐标，而是朝某个方向移动时，“横坐标或纵坐标”变化的极限。
         
         * 举例：matrix = [ [ 0, 1, 2 ], [ 3, 4, 5 ], [ 6, 7, 8 ] ]
           * 顺时针螺旋遍历。此时向右遍历的“横坐标”移动的极限是 2 。遍历完“一圈”后，向右遍历的“横坐标”移动的极限 -1 ，变为 1 。下一次向右遍历，只能遍历到“横坐标”为 1 的位置。
         
       * 相关程序：
       
         * ```javascript
           // 注：j 可以理解为元素的“横坐标”，i 可以理解为元素的“纵坐标”。
           if (j == boundR) {
               boundU++;
               turn = 'd';
           }
           if (i == boundD) {
               boundR--;
               turn = 'k';
           }
           ```



3. 特殊情况：输入的矩阵为空

   * 所以，在运行 `let m = matrix[0].length - 1;` 之前，需要先判断矩阵不为空。

   * 相关程序：

     * ```javascript
       let n = matrix.length - 1;
       if (n < 0) return [];
       let m = matrix[0].length - 1;
       ```



##### 思路、程序参考

* [cc123nice：54. 旋转矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/luo-xuan-ju-zhen-ji-yi-li-jie-92100-by-caifeng123/)
* [力扣官方题解：54. 旋转矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/luo-xuan-ju-zhen-by-leetcode-solution/)



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