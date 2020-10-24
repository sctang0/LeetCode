### [48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/)

##### 题目描述

* 给定一个 n * n 的二维矩阵表示一个图像。将图像顺时针旋转 90 度。

* 说明：

    * 你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

* 示例：

    * ```example
        给定 matrix = 
        [
          [ 1, 2, 3 ],
          [ 4, 5, 6 ],
          [ 7, 8, 9 ]
        ],
        
        原地旋转输入矩阵，使其变为:
        [
          [ 7, 4, 1 ],
          [ 8, 5, 2 ],
          [ 9, 6, 3 ]
        ]
        ```



##### 思路

需解决的问题：

* 对应位置的 4 个元素，如何实现原地顺时针旋转 90° 的位置变化？

  * 如何通过一个“统一的格式”，表示这 4 个元素？

    * 例如，一个在矩阵左上角的数组元素 `matrix[i][j]` ，那么，其它对应 3 个元素如何表示？
      * 令 `len = matrix.length`
      * 那么，左下角对应元素为 `matrix[len-i][j]` 。右上角对应元素为 `matrix[i][len-j]` 。右下角对应元素为 `matrix[len-i][len-j]` 。

  * 如何实现顺时针旋转呢？

    * 定义一个临时保值变量 `temp` ，具体程序如下：

    * ```javascript
      temp = matrix[i][j];
      matrix[i][j] = matrix[len-j][i];
      matrix[len-j][i] = matrix[len-i][len-j];
      matrix[len-i][len-j] = matrix[j][len-i];
      matrix[j][len-i] = temp;
      ```

  

* 如何将矩阵分为 4 个相同的矩阵，并通过函数实现遍历？

  * 矩阵的划分，如下图：

    * <img src="https://github.com/sctang0/LeetCode/blob/master/images/48.Rotate_Image.png" alt="图片来源：wiserui：48. 旋转图像" width="70%" />

  * 那么，如何实现矩阵元素的遍历呢？

    * 实现程序：

      ```javascript
      let len = matrix.length - 1;
      for (var i=0; i<=Math.floor(len/2); i++) {
          for (var j=i; j<=len-i-1; j++) {
              matrix[i][j];
          }
      }
      ```
    



```javascript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    let len = matrix.length - 1;
    let temp;
    for (var i=0; i<=Math.floor(len/2); i++) {
        for (var j=i; j<=len-i-1; j++) {
            temp = matrix[i][j];
            matrix[i][j] = matrix[len-j][i];
            matrix[len-j][i] = matrix[len-i][len-j];
            matrix[len-i][len-j] = matrix[j][len-i];
            matrix[j][len-i] = temp;
        }
    }
    return;
};
```



##### 复杂度分析

* 时间复杂度：O(n^2)，n 为二维矩阵包含的数组元素的长度。
* 空间复杂度：O(1)，旋转操作就地完成。



##### 题外话

* [Math.floor(x) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)：`x` 为一个数字，方法返回小于或等于 `x` 的最大整数。



##### 想法、程序参考

* [wiserui：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/you-dian-xiang-zhuan-mo-fang-by-wiserui/)
* [力扣(LeetCode)：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/xuan-zhuan-tu-xiang-by-leetcode/)

##### 图片来源

* [wiserui：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/you-dian-xiang-zhuan-mo-fang-by-wiserui/)