### [56. 合并区间 - 顺序遍历](https://leetcode-cn.com/problems/merge-intervals/)

##### 思路

该题可以分解为如下问题：

* 什么情况下可以合并？怎么合并？
* 有无特殊情况需要考虑？



1. 什么情况下可以合并？怎么合并？
   * 当上一个数组的“右包围”，大于下一个数组的“左包围”时，就可以合并。即 `intervals[i][1] >= intervals[i+1][0]` 。
   * 合并时将 `intervals[i][0]` 与 `Math.max(intervals[i][1], intervals[i + 1][1])` ，分别作为合并后数组的“左右包围”，组成一个数组。
     * 例如：intervals = [ [ 1, 4 ], [ 4, 5 ] ]
       * 4 = 4，可以进行合并
       * Math.max(4, 5) = 5 ，将 5 作为合并后数组的右包围
       * res.push([1, 5]) 
   * 在做 `intervals[i][1] >= intervals[i+1][0]` 判断时，可以扩充一下。`intervals[i][1] >= intervals[i + n][0] (n >= 1)` 。向右遍历，直到出现第一次判断为否。
   * 合并的时候，“左包围”还是 `intervals[i][0]` ，“右包围”是 `Math.max(intervals[i][1], ... , intervals[i + n][1])(n >= 1)` 。
     * 例如：intervals = [ [ 1, 3 ], [ 2, 6 ], [ 8, 10 ], [ 15, 18 ] ]
       * 3 > 2 ，可以进行合并
       * Math.max(3, 6) = 6，将 6 作为合并后数组的右包围
       * 6 < 8 ，中断向右的遍历
       * res.push([1, 6])
       * 10 < 15 ，不能进行合并，直接加到 res 末尾
       * res.push([8, 10])
       * res.push([15, 18])，只剩下一个元素，直接加到 res 末尾



2. 特殊情况

   * intervals 为空

     * 在 intervals 为空时，调用其值会报错，要事先中回避这种情况。

     * 相关语句：

       * ```javascript
         let len = intervals.length;
         if (len == 0) return [];
         ```



```javascript
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {
    let i = 0;
    let res = [];
    let len = intervals.length;
    if (len == 0) return [];
    intervals.sort((a, b) => a[0] - b[0]);
    while (i < len) {
        let currLeft = intervals[i][0];
        let currRight = intervals[i][1];
        while (i < len - 1 && currRight >= intervals[i + 1][0]) {
            i++;
            currRight = Math.max(currRight, intervals[i][1]);
        }
        res.push([currLeft, currRight]);
        i++;
    }
    return res;
};
```



##### 复杂度分析

* 时间复杂度：O(nlogn)，n = intervals.length 。arr.sort() 使用快速排序的平均时间复杂度为 O(nlogn) 。
* 空间复杂度：O(n) ，n = intervals.length 。输出数组 res ，极端情况下包含数组 intervals 中所有的元素。



##### 题外话

* [arr.sort([compareFunction])](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)：上方程序中的是根据二维数组 intervals 元素“左包围”的值，对 intervals 中的数组元素进行排序。
  * 注：“右包围”的数值大小在排序过程中没有考虑。
  * 相关语句：`intervals.sort((a, b) => a[0] - b[0]);` 




##### 思路、程序参考

* [秦时明月：56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/solution/56-he-bing-qu-jian-by-alexer-660/)
* [小袁大圣：深入浅出 JavaScript 的 Array.prototype.sort 排序算法](https://segmentfault.com/a/1190000010648740)

