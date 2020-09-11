##### [backTrack(tmpPath.slice()) 为什么这里要用 arr.slice() ？](https://leetcode-cn.com/problems/permutations/solution/46-quan-xu-lie-by-shu-cheng/579219)

##### 思路

*  `res.push(tmpPath)` 与 `res.push(tmpPath.slice())` 有何区别？
    * 这里 tmpPath 是一个栈结构，最终是 [] 。前者直接将 tmpPath 直接 push 进去，最终结果中的每一个元素都指向同一个栈，所以都是 [] 。后者其实是当前 tmpPath 的一个浅拷贝，最终结果的每一个元素都指向 tmpPath 不同状态的拷贝。



##### 相关函数简谈

* [arr.slice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：返回一个**新的数组对象**，原始数组不会被改变。
  * 在该题中，`tmpPath.slice()` 返回一个包含数组 tmpPath 所有元素新的数组对象。



##### 思路参考

* [null 题末回答：46. 全排列](https://leetcode-cn.com/problems/permutations/solution/jspython-hui-su-tao-lu-mo-ban-ti-46-quan-pai-lie-b/367065)
  * 注：上面思路中的逻辑、语言 90% 是照搬过来的。不过，自己并没有把原内容上下文也描述出来，所以吧，还是建议去看一下原作者内容。



##### 程序

* 使用控制台输出 console.log() 。看一下，不使用 arr.slice() 情况下的输出情况。



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
            console.log(res);
            return;
        }
        for (let i=0; i<n; i++) {
            if (!tmpPath.includes(nums[i])) {
                tmpPath.push(nums[i]);
                backTrack(tmpPath);
                tmpPath.pop();
            }
        }
    }
    backTrack(tmpPath);
    return res;
}
/**
 * 输入: [ 1, 2, 3 ]
 * 输出: [ [], [], [], [], [], [] ]
 * 预期结果: [ [ 1, 2, 3 ], [ 1, 3, 2 ], [ 2, 1, 3 ], [ 2, 3, 1 ], [ 3, 1, 2 ], [ 3, 2, 1 ] ]
 * stdout:
     [ [ 1, 2, 3 ] ]
     [ [ 1, 3, 2 ], [ 1, 3, 2 ] ]
     [ [ 2, 1, 3 ], [ 2, 1, 3 ], [ 2, 1, 3 ] ]
     [ [ 2, 3, 1 ], [ 2, 3, 1 ], [ 2, 3, 1 ], [ 2, 3, 1 ] ]
     [ [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ] ]
     [
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ]
     ]
 */
```