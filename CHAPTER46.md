### [46. 全排序](https://leetcode-cn.com/problems/permutations/)

##### 思路

递归回溯

![图片来源：笨猪爆破组]([https://github.com/sctang0/LeetCode/blob/master/images/46.Permutations.png](https://pic.leetcode-cn.com/aa061a6233fa2bd640b4e1416c12dceceb0c4b4e6f2610240740a3cb6ea1496c-%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20200514183911.png))



##### 题外话

* [全排列]([https://baike.baidu.com/item/%E5%85%A8%E6%8E%92%E5%88%97/4022220?fr=aladdin](https://baike.baidu.com/item/全排列/4022220?fr=aladdin))：从n个不同元素中任取m（m≤n）个元素，按照一定的顺序排列起来，叫做从n个不同元素中取出m个元素的一个排列。当m=n时所有的排列情况叫全排列。

* [arr.includes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)：方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

* [arr.pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)：`**pop()**`方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
  * 此方法更改数组 `arr` ，变为不包含数组最后一个元素的数组（若 `arr.length>=1`）。

* [arr.slice(begin, end)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`）。原始数组不会被改变。
  * 如果省略 `begin`，则 `slice` 从索引 `0` 开始。如果 `begin` 大于原数组的长度，则会返回空数组。
  * 如果 `end` 被省略，则 `slice` 会一直提取到原数组末尾。如果 `end` 大于数组的长度，`slice` 也会一直提取到原数组末尾。
  * 程序 `tmpPath.slice()` 加入 `.slice()`  ，是考虑 `res.push(tmpPath)` 。若使用 `backTrack(tmpPath)` ，那最后加入数组 res 的就是数组 tmpPath 的头指针，而不是 tmpPath 数组元素组成的数组。



##### 思路及代码来源

* [秦时明月：46. 全排序](https://leetcode-cn.com/problems/permutations/solution/46-quan-pai-lie-by-alexer-660/)

##### 图片来源

* [笨猪爆破组：46. 全排序](https://leetcode-cn.com/problems/permutations/solution/chou-xiang-cheng-jue-ce-shu-yi-ge-pai-lie-jiu-xian/)



```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    let n = nums.length;
    let res = [];
    let tmpPath = [];
    let backTrack = (tmpPath) => {
        if (tmpPath.length == n) {
            res.push(tmpPath);
            return;
        }
        for (let i=0; i<n; i++) {
            if (!tmpPath.includes(nums[i])) {
                tmpPath.push(nums[i]);
                backTrack(tmpPath.slice());
                tmpPath.pop();
            }
        }
    }
    backTrack(tmpPath);
    return res;
}
```



##### 复杂度分析

* 时间复杂度：O(n!)，n 为数组 `nums` 的长度。`n!` 也为 `nums` 可以形成的全排序的个数。
* 空间复杂度：O(n!)。**`tmpPath.pop()`** 在递归的结尾处，将存有 **`temPath`** 的数组值全部删除。二维数组 **`res`** 需要储存全排列，而一共可以形成 **`n!`** 个对应一维数组。 