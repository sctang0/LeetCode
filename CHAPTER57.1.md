### [57. 插入区间 - while() 插入数组](https://leetcode-cn.com/problems/insert-interval/)

##### 思路

* intervals 中元素是按起始端点排序的. 所以, 可以在遍历 intervals 一遍过程中, 找到 newIntervals 合适存放的位置.

    * 相关语句: 

        * ```javascript
            let j = 0;
            let i = 0;
            let tmpIntervals = [];
            let len = intervals.length;
            while(i < len) {
                if (intervals[i][0] >= newIntervals[0] && j == 0) {
                    tmpIntervals.push(newIntervals);
                    j = 1;
                }
                tmpIntervals.push(intervals[i]);
                if (i == len - 1 && j == 0) {
                    tmpIntervals.push(newIntervals);
                }
                i++;
            }
            ```

* 区间合并, 思路与[56. 区间合并](https://leetcode-cn.com/problems/merge-intervals/solution/56-he-bing-qu-jian-shun-xu-bian-li-by-shu-cheng/)相同.



```javascript
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



##### 复杂度分析

* 复杂度分析:
    * 执行用时: 击败 6.16% 用户.
    * 内存消耗: 击败 5.43% 用户.
* 使用 arr.sort() 排序的复杂度分析:
    * 执行用时: 击败 85.78% 用户.
    * 内存消耗: 击败 20.93% 用户.



##### 思路, 程序参考

* [秦时明月：56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/solution/56-he-bing-qu-jian-by-alexer-660/)