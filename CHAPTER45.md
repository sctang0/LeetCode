### [45. 跳跃游戏 ii](https://github.com/sctang0/LeetCode/blob/master/CHAPTER45.md)

##### 思路：

* 需要保证两点：
  1. 跳到最远的位置
  2. 使用最少跳跃次数
* 跳到最远的位置
  * 例如：[2, 3, 1, 1, 4]。如果，第一次直接跳两格，则会“错过”直接跳到结尾的"3"。
  * 而解决方案是，遍历中间，维护一个能跳到的最大距离的值。下方程序中的相应变量为 canJumpMax。
* 使用最少的跳跃次数
  * 如果，选择 nums[i]~nums[i+nums[i]]，之间的数组元素值作为跳跃的步数。那，跳跃的次数如何考虑和处理呢？
  * 在遍历中间后，还要遍历末尾的 nums[i+nums[i]] 。这样保证了所有下一步数组值，跳跃次数的一致。
  * 例如：nums = [2, 3, 3, 1, 1, 1]。
    * nums[0] = 2，能最远跳到 nums[2]。
    * 遍历 nums[1], nums[2] ，能跳的最远的距离均为 3 ，在加上本身的下标 1，2。比较之后，选取跳到 nums[2]



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