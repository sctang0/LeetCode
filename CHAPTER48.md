### [48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/)





##### 题外话

* [Math.floor(x) ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)：`x` 为一个数字，方法返回小于或等于 `x` 的最大整数。



##### 想法、程序参考

* [wiserui：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/you-dian-xiang-zhuan-mo-fang-by-wiserui/)
* [力扣(LeetCode)：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/xuan-zhuan-tu-xiang-by-leetcode/)

##### 图片来源

* [wiserui：48. 旋转图像](https://leetcode-cn.com/problems/rotate-image/solution/you-dian-xiang-zhuan-mo-fang-by-wiserui/)



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