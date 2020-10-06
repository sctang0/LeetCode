### [47. 全排序 ii](https://leetcode-cn.com/problems/permutations-ii/solution/)

##### 题目描述

* 给定一个可包含重复数字的序列，返回所有不重复的全排列。

* 示例：

    * ```example
        输入: [ 1, 1, 2 ]
        输出:
        [
          [ 1, 1, 2 ],
          [ 1, 2, 1 ],
          [ 2, 1, 1 ]
        ]
        ```



##### 思路

* 一个问题是，通过怎样的方式选择 `tmpPath` 第一个或下一个元素，才能使最后得出的结果中没有重复的项？或者说，在何种情况下不选择 `nums` 的元素，作为 `tmpPath` 的元素？
  * 在递归中，该数组元素此前已经调用。
  * 在不是 `tmpPath` 开头元素（`i>1`）的情况下，元素与前一个相同（`nums[i]=nums[i-1]`），且 `nums[i-1]` 没有被调用过（`!hash[i-1]`）。
  * 具体程序：
    * `if (hash[i] || (i>0 && !hash[i-1] && nums[i]==nums[i-1])) continue;`



```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    let n =nums.length;
    nums = nums.sort((a, b) => {return a - b});
    let res = [];
    let tmpPath = [];
    let hash = {};
    let backTrack = (tmpPath) => {
        if (tmpPath.length == n) {
            res.push(tmpPath);
            return;
        }
        for (let i=0; i<n; i++) {
            if (hash[i] || (i>0 && !hash[i-1] && nums[i]==nums[i-1])) continue;
            hash[i] = true;
            tmpPath.push(nums[i]);
            backTrack(tmpPath.slice());
            hash[i] = false;
            tmpPath.pop();
        }
    }
    backTrack(tmpPath);
    return res;
};
```



##### 复杂度分析

* 时间复杂度：O(n!)。n 为数组 `nums` 的长度。`n!` 也为 `nums` 可以形成的全排序的个数。虽然重复的项不会计入结果，可也还是会有一次判断。
* 空间复杂度：最坏空间复杂度，O(n!)。最好空间复杂度，O(1)，此时 `nums` 数组元素全部相同。n 为数组 `nums` 长度。（很可能是错的，不知道如何计算，于是 LeetCode 的题解也没有写这个。）



##### 思路及程序参考

* [秦时明月：47. 全排序 ii](https://leetcode-cn.com/problems/permutations-ii/solution/47-quan-pai-lie-ii-by-alexer-660/)