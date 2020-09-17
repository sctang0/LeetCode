### [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

##### 思路

如果要按顺时针螺旋顺序遍历矩阵，会面临如下问题：

* 如何实现“转弯”？即如何从一个行进方向，转换为另外一个行进方向？
* 行走步数的变化如何调整？
* 如何在最后一步停下？



特殊情况：输入的矩阵为空

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

* 时间复杂度：O(n * m)，n 为二维数组 matrix 的包含一维数组的个数，m 为 matrix 中一维数组中所包含的元素的个数。遍历数组 matrix 一次的时间复杂度。
* 空间复杂度：O(n * m)，与事件复杂度中对应变量表达相同含义。res 包含 matrix 中所有元素。