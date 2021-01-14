### [59. 螺旋矩阵 II-螺旋遍历](https://leetcode-cn.com/problems/spiral-matrix-ii/)

##### 题目描述

* 给定一个正整数 n ，生成一个包含 1 到 n ^ 2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

* 示例：

    * ```example
        输入: 3
        输出:
        [
         [ 1, 2, 3 ],
         [ 8, 9, 4 ],
         [ 7, 6, 5 ]
        ]
        ```



##### 思路

* 顺时针螺旋遍历二维数组的思路与 [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/54-luo-xuan-ju-zhen-luo-xuan-bian-li-by-shu-cheng/) 的一样, 可以依葫芦画瓢.



```javascript
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let res = new Array();
    for (let i = 0; i < n; i++) {   
        res[i] = new Array();
        for (let j = 0; j < n; j++) {
            res[i][j] = 0;
        }
    }
    let i = 0;
    let j = 0;
    let boundL = 0;
    let boundR = n - 1;
    let boundU = 0;
    let boundD = n - 1;
    let turn = 'r';

    for (let a = 1; a <= n * n; a++) {
        res[i][j] = a;
        if (turn == 'r') {
            j++;
            if (j == boundR) {
                turn = 'd';
                boundU++;
            }
        } else if (turn == 'd') {
            i++;
            if (i == boundD) {
                turn = 'l';
                boundR--;
            }
        } else if (turn == 'l') {
            j--;
            if (j == boundL) {
                turn = 'u';
                boundD--;
            }
        } else if (turn == 'u') {
            i--;
            if (i == boundU) {
                turn = 'r';
                boundL++;
            }
        }
    }
    return res;
};
```



##### 复杂度分析

* 时间复杂度: O(n ^ 2). 遍历 n * n 的矩阵一遍.
* 空间复杂度: O(n ^ 2). 返回数组 res 为 n * n 的矩阵.



##### 题外话

* JavaScript 定义二维数组, 至少包括以下两种方式:

    * ```javascript
        var arr = new Array([1, 2, 3], [4, 5, 6], [7, 8, 9]);
        ```

    * ```javascript
        var arr = new Array();
        for (var i = 0; i < n; n++) {
            arr[i] = new Array();
            for (var j = 0; j < n; j++) {
                arr[i][j] = 0;
            }
        }
        ```
        



##### 思路, 程序参考

* [cc123nice: 59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/solution/luo-xuan-ju-zhen-ii-93100-by-caifeng123/)
* [书成: 54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/solution/54-luo-xuan-ju-zhen-luo-xuan-bian-li-by-shu-cheng/)
* [百度知道: JavaScript 如何定义一个二维数组](https://zhidao.baidu.com/question/7989716.html)
* [JavaScript - cannot set property of underfined](https://stackoverflow.com/questions/7479520/javascript-cannot-set-property-of-undefined)