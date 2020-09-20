### [55. 跳跃游戏 - 倒序遍历](https://leetcode-cn.com/problems/jump-game/)

##### 思路





##### 题外话

* [贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)：一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法。



##### 思路、程序来源

* [秦时明月：55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/solution/55-tiao-yue-you-xi-by-alexer-660/)



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

