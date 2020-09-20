### [55. 跳跃游戏 - 倒序遍历](https://leetcode-cn.com/problems/jump-game/)

##### 思路

* 从右到左遍历 nums ，返回能“到达” nums[nums.length - 1] 的左边最靠近其的数。将下一个数设为该数。如果，最后能到达 nums[0] ，返回 true 否则返回 false 。
  * 举例：
    * nums = [ 2, 1, 0, 3 ]
      * 从右到左遍历。nums[2] = 0 ，到不了 nums[3] 。nums[1] = 1 ，到不了 nums[3] 。同理，nums[0] 。于是，返回 false 。
    * nums = [ 2, 3, 1, 4 ]
      * 从右到左遍历。nums[2] = 1 ，能到达 nums[3] ，将 nums[2] 设为要到达“终点”。nums[1] = 3 ，能到达 nums[2] ，将 nums[1] 设为要到达的终点。同理 nums[0] 。最终能到达 nums[0] ，返回 true 。



```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function(nums) {
    var lenPoint = nums.length - 1;
    var leftPos = lenPoint;
    for (var left = lenPoint; left >= 0; left--) {
        if (nums[left] + left >= leftPos) {
            leftPos = left;
        }
    }
    return leftPos == 0;
};
```



##### 复杂度分析

* 时间复杂度：O(n)，`n = nums.length;` 。遍历数组 nums 一遍。
* 空间复杂度：O(1)



##### 题外话

* [贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)：一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法。



##### 思路、程序来源

* [秦时明月：55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/solution/55-tiao-yue-you-xi-by-alexer-660/)



