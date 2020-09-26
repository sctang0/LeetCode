### [57. 插入区间 - 顺序遍历](https://leetcode-cn.com/problems/insert-interval/)

##### 思路

* 将数组 newIntervals 添加到 intervals 末尾. 并对添加后的 intervals 数组进行排序.

    * 相关程序:

        * ```javascript
            intervals.push(newInterval);
            intervals.sort((a, b) => a[0] - b[0]);
            ```

* 区间合并, 思路与[56. 区间合并](https://leetcode-cn.com/problems/merge-intervals/solution/56-he-bing-qu-jian-shun-xu-bian-li-by-shu-cheng/)相同.



```javascript
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    let i = 0;
    let result = [];
    let len = intervals.length;
    if (len == 0) {
        intervals.push(newInterval);
        return intervals;
    }
    intervals.push(newInterval);
    intervals.sort((a, b) => a[0] - b[0]);
    len += 1;
    while (i < len) {
        let currLeft = intervals[i][0];
        let currRight = intervals[i][1];
        while (i < len - 1 && intervals[i+1][0] <= currRight) {
            i++;
            currRight = Math.max(intervals[i][1], currRight);
        }
        result.push([currLeft, currRight]);
        i++;
    }
    return result;
};
```



##### 复杂度分析

* 时间复杂度: O(nlog(n)), n = intervals.length +1. arr.sort() 使用快速排序的平均时间复杂度为 O(nlogn) .
* 空间复杂度: O(n), n = intervals.length + 1. result 的数组长度为 intervals.length + 1.



##### 题外话

* [尝试改进失败](https://github.com/sctang0/LeetCode/blob/master/CHAPTER57.1.md): 二维数组 intervals 是按照区间起始端点排序. 那么, 可以遍历 intervals[i] [0] , 找到newIntervals 合适存放的位置.

    * 相关语句:

        * ```javascript
            /**
             * @param {number[][]} intervals
             * @param {number[]} newInterval
             * @return {number[][]}
             */
            var insert = function(intervals, newInterval) {
                let j = 0;
                let i = 0;
                let result = [];
                let tmpIntervals = [];
                let len = intervals.length;
                if (len == 0) {
                    intervals.push(newInterval);
                    return intervals;
                }
                while(i < len) {
                if (intervals[i][0] >= newInterval[0] && j == 0) {
                        tmpIntervals.push(newInterval);
                    j = 1;
                    }
                    tmpIntervals.push(intervals[i]);
                if (i == len - 1 && j == 0) {
                        tmpIntervals.push(newInterval);
                }
                    i++;
                }
                console.log(tmpIntervals);
                i = 0;
                len = tmpIntervals.length;
                while (i < len) {
                    let currLeft = tmpIntervals[i][0];
                    let currRight = tmpIntervals[i][1];
                    while (i < len - 1 && tmpIntervals[i+1][0] <= currRight) {
                        i++;
                        currRight = Math.max(tmpIntervals[i][1], currRight);
                    }
                    result.push([currLeft, currRight]);
                    i++;
                }
                return result;
            };
            ```
    
    * 复杂度分析:
    
        * 执行用时: 击败 6.16% 用户.
        * 内存消耗: 击败 5.43% 用户.
    
    * 使用 arr.sort() 排序的复杂度分析:
    
        * 执行用时: 击败 85.78% 用户.
        * 内存消耗: 击败 20.93% 用户.



##### 思路, 程序参考

* [秦时明月：56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/solution/56-he-bing-qu-jian-by-alexer-660/)