### [55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)



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

