### [45. 跳跃游戏 ii](https://github.com/sctang0/LeetCode/blob/master/CHAPTER45.md)

##### 思路：



##### 思路及程序来源：

* [秦时明月：45. 跳跃游戏ii](https://leetcode-cn.com/problems/jump-game-ii/solution/45-tiao-yue-you-xi-ii-by-alexer-660/)

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
    var steps = 0;
    var canJumpMax = 0;
    var last_canJumpMax = 0;
    var len = nums.length;
    for (var i=0; i<len-1; i++) {
        canJumpMax = Math.max(canJumpMax, i+nums[i]);
        if (last_canJumpMax == i) {
            last_canJumpMax = canJumpMax;
            steps++;
        }
        if (last_canJumpMax >= len-1) {
            break;
        }
    }
    return steps;
}
```



##### 复杂度分析：

* 时间复杂度：O(n)，n 为数组 nums 的长度。
* 空间复杂度：O(1)