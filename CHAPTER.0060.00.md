### [60. 第 k 个排序-直达](https://leetcode-cn.com/problemset/all/)

##### 题目描述

* 给出集合 [ 1, 2, 3, … , n ] ，其所有元素共有 n ! 种排列。按大小顺序列出所有排列情况，并一一标记。

* 当 n = 3 时, 所有排列如下：
    1. "123"
    2. "132"
    3. "213"
    4. "231"
    5. "312"
    6. "321"

* 给定 n 和 k，返回第 k 个排列。注意，n 的范围是 [ 1, 9 ]，k 的范围是 [ 1,  n ! ]。

* 举例：

    * ```example
        输入: n = 3, k = 3
        输出: "213"
        ```



##### 思路

* 因为由 [ 1, 2, ... , n ] 构成的 n ! 种排序, 其由小到大的排列是可以推算出来的, 所以, 直达是可能的. 



n ! 种排序的规律:

* 若 n > 3 . 
    * 在 n ! 种排序中, 以 1 作为首字符的排序共有 n ! / n 种. 
    * 在这 ( n - 1 ) ! 种中, 以 2 作为第二个字符的排序共有 n ! / ( n * ( n - 1 ) ) 种. 
    * 在这 ( n - 2 ) ! 种中, 以 3 作为第三个字符的排序共有 n ! / ( n * ( n - 1 ) * ( n - 2 ) ) 种. 
    * ...
* 由小到大排列



```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {string}
 */
var getPermutation = function(n, k) {
    const nums = [];
    let factorial = 1;
    for (let i = 1; i <= n; i ++) {
        nums.push(i);
        factorial *= i;
    }
    k --;
    let resStr = '';
    while (nums.length > 0) {
        factorial /= nums.length;
        const index = k / factorial | 0;
        resStr += nums[index];
        nums.splice(index, 1);
        k %= factorial;
    }
    return resStr;
};
```



##### 复杂度分析

* 时间复杂度: O(n ^ 2). `while()` 循环 n 次, 而 `arr.splice()` 的时间复杂度为 O(n) .
* 空间复杂度: O(n). 



##### 题外话

* [array.splice(start, deleteCount, item1, item2, ...)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice): 通过删除, 替换, 添加来修改原数组.
    * `nums.splice(index, 1);` 为删除数组中的 `nums[index]` 元素.
* `const index = k / factorial | 0;`: `index` 为 `k / factorial` 的整数部分(不四舍五入), 保留正负号.



##### 思路, 程序参考

* [笨猪爆破组: 60. 第 k 个排序](https://leetcode-cn.com/problems/permutation-sequence/solution/shou-hua-tu-jie-jing-dian-de-dfshui-su-shu-xue-gui/)

