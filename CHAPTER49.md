### [49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

##### 题目描述

* 给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

* 说明：

    - 所有输入均为小写字母。
    - 不考虑答案输出的顺序。

* 示例：

    * ```example
        输入: [ "eat", "tea", "tan", "ate", "nat", "bat" ]
        输出:
        [
          [ "ate", "eat", "tea" ],
          [ "nat", "tan" ],
          [ "bat" ]
        ]
        ```



#### 思路

需解决的问题：

* 如何按照题示要求，区分不同的数组？
  * 哈希映射：字符哈希值相同的归为同一组。
  * 将每个字符串 `strs[i]` 转换为字符数 `tmpHash` ，由26个非负整数组成，表示 a, b, c 的数量。我们使用这些计数作为哈希映射的基础。
    * 这样也可以解决单个字符出现多次的情况。



#### 题外话

* `var tmpHash = new Array(26)` ：定义长度为 26 的二维数组。

* [str.charCodeAt(index)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)：指定 `index` 处字符( `str[index]` )的 UTF-16 代码单元值的一个数字；如果 `index` 超出范围，`charCodeAt()` 返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。

  * `index`：一个大于等于 `0`，小于字符串长度的整数。如果不是一个数值，则默认为 `0`。
  * 注：在历史版本中（如 JavaScript 1.2），`charCodeAt` 返回一个数字，表示给定 index 处字符的 ISO-Latin-1 编码值。ISO-Latin-1 编码集范围从 `0` 到 `255`。开头的 `0` 到 `127` 直接匹配 ASCII 字符集。
  
* [arr.join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)：将一个数组（或一个[类数组对象](https://developer.mozilla.org/zh-CN//docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)）的所有元素连接成一个字符串并返回这个字符串。

  * ```javascript
    const elements = ['Fire', 'Air', 'Water'];
    console.log(elements.join(''));
    // expected output: "FireAirWater"
    ```



 #### 思路、程序参考

* [秦时明月：49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/solution/49-zi-mu-yi-wei-ci-fen-zu-by-alexer-660/)
* [力扣(LeetCode)：49. 字符异位词分组](https://leetcode-cn.com/problems/group-anagrams/solution/zi-mu-yi-wei-ci-fen-zu-by-leetcode/)



```javascript
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
    var tmpHash = new Array(26);
    var resultHash = {};
    var out = [];
    for(var i=0;i<strs.length;i++){
        for(var k=0;k<26;k++){
            tmpHash[k] = '0';
        }
        var aCode = 'a'.charCodeAt();
        var tmpl = strs[i];
        var len = tmpl.length;
        var resultHashKey = '';
        for(var r=0;r<len;r++){
            tmpHash[tmpl[r].charCodeAt() - aCode]++;
        }
        var tmpHashKey = tmpHash.join('');
        if(resultHash[tmpHashKey] == undefined){
            resultHash[tmpHashKey] = [];
        }
        resultHash[tmpHashKey].push(tmpl);
    }
    for(var key in resultHash){
        out.push(resultHash[key])
    }
    return out;
};
```



#### 复杂度分析

* 时间复杂度：O(n*m)。`n` 为 `strs` 的长度，`m` 为 `strs` 中字符串的长度。
* 空间复杂度：O(n*m)。保存需要返回的二维数组 `out` 。