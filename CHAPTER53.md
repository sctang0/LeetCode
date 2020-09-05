### [53. 最大子序之和](https://leetcode-cn.com/problems/maximum-subarray/)

##### 思路





##### 思路、程序来源

* [画手大鹏：53. 最大子序之和](https://leetcode-cn.com/problems/maximum-subarray/solution/hua-jie-suan-fa-53-zui-da-zi-xu-he-by-guanpengchn/)



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