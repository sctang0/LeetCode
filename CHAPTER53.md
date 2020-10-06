### [53. 最大子序之和](https://leetcode-cn.com/problems/maximum-subarray/)

##### 题目描述

* 给定一个整数数组  `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

* 示例：

    * ```example
        输入: [ -2, 1, -3, 4, -1, 2, 1, -5, 4 ]
        输出: 6
        解释: 连续子数组 [ 4, -1, 2, 1 ] 的和最大，为 6。
        ```



##### 思路

* 该题至少可以分解为下列问题：
  * 一段数的结果，碰到下一个数，应该如何考虑进行加、单独保留、还是对加了之后的结果与单独的两个数进行比较？
    * 注：这里的一段数也可以为数组中单独的一个元素，下同。
  * 什么情况下应该中断连续？以及如何处理中断连续之后的值得保存？



* 一段数的结果，碰到下一个数，应该如何考虑进行加、单独保留、还是对加了之后的结果与单独保留的两个数进行比较？

  * 关于数的“相遇”，可以简单分为如下两种情况，单独讨论：

    1. 负数或零  遇到  负数或零或正数
       * 直接对两数进行比较。因为，负数或零对下一个数，没有增大的可能。之后，临时保存较大的数。
         * 保存较大的数，是为了与后面的数进行相加或比较。

    2. 正数（Pos）  遇到  负数或零或正数（nums[n]）
       * 两数相加。因为，正数能对与下一个数的和起到增益的效果。之后，临时保存正数（Pos），以及两数之和。
         * 保存正数（Pos）。因为要与和进行比较，判断 nums[n] 是否有对结果有增益效果。
         * 保存两数之和。因为如果 nums[n] 为正数，相加之和就大于前一个正数。

  * 相关程序

    * ```javascript
      if (sum > 0) {
          sum += num;
      } else {
          sum = num;
      }
      res = Math.max(res, sum);
      ```



* 什么情况下应该中断连续？以及如何处理中断之后值的保存？

  * 什么情况下应该中断连续？
    
    * 前一个段数的和是负数，或者前一个段数是正数，而该数遇到了一个负数的时候。因为，此时两个数之和是不分别大于两数的。
    
  * 中断连续之后，如何处理值的保存？

    * 程序中，用 res 保存前面数组中一段元素和的最大值。用 sum 保存当前数与当前数紧邻的一段数。通过比较或求和得到的那个较大的值。

      * 通过对 res 与 sum 的比较取较大值，来兼顾总体的最大值。

    * 相关程序

      * ```javascript
        if (sum > 0) {
            sum += num;
        } else {
            sum = num;
        }
        res = Math.max(res, sum);
        ```



```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let res = nums[0];
    let sum = 0;
    for (const num of nums) {
        if (sum > 0) {
            sum += num;
        } else {
            sum = num;
        }
        res = Math.max(res, sum);
    }
    return res;
};
```



##### 复杂度分析

* 时间复杂度：O(n)，n 为数组 nums 长度。遍历数组一次的时间复杂度。
* 空间复杂度：O(1)



##### 思路、程序参考

* [画手大鹏：53. 最大子序之和](https://leetcode-cn.com/problems/maximum-subarray/solution/hua-jie-suan-fa-53-zui-da-zi-xu-he-by-guanpengchn/)
* [秦时明月：53. 最大子序之和](https://leetcode-cn.com/problems/maximum-subarray/solution/53-zui-da-zi-xu-he-by-alexer-660/)