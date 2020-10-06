### [58. 最后一个单词的长度-倒序遍历, 双指针](https://leetcode-cn.com/problems/length-of-last-word/)

##### 题目描述

* 给定一个仅包含大小写字母和空格 `' '` 的字符串 `s`，返回其最后一个单词的长度。如果字符串从左向右滚动显示，那么最后一个单词就是最后出现的单词。如果不存在最后一个单词，请返回 0 。

* 说明：一个单词是指仅由字母组成、不包含任何空格字符的 最大子字符串。

* 示例：

    * ```example
        输入: "Hello World"
        输出: 5
        ```



##### 思路一: 倒序遍历

* 从右往左遍历, 当遇到第一个非空的字符时, 开始计数. 此时, lastLen = 0 (注: lastLen 为记录最后一个单词长度的变量. 下同).

    * 相关语句:

        * ```javascript
            if (s[i] != ' ' && lastLen == 0) {
                lastLen = 1;
                continue;
            }
            ```

* 在遇到非空字符前, 继续遍历. 此时, lastLen != 0 .

    * 相关语句:

        * ```javascript
            if (s[i] != ' ' && lastLen != 0) {
                lastLen++;
                continue;
            }
            ```

* 再次遇到空字符时, 结束遍历, 输出 lastLen . 此时, lastLen != 0 .

    * 相关语句:

        * ```javascript
            if (s[i] == ' ' && lastLen != 0) {
                return lastLen;
            }
            ```



```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    let lastLen = 0;
    let len = s.length;
    if (len == 0) return lastLen;
    for (let i = len - 1; i >= 0; i--) {
        if (s[i] != ' ' && lastLen == 0) {
            lastLen = 1;
            continue;
        }
        if (s[i] != ' ' && lastLen != 0) {
            lastLen++;
            continue;
        }
        if (s[i] == ' ' && lastLen != 0) {
            return lastLen;
        }
    }
    return lastLen;
};
```



##### 题外话

* [continue](https://www.w3school.com.cn/js/js_break.asp): “跳过”循环中的一个迭代, 然后继续循环中的下一个迭代.
    * continue 的作用是, 防止 if() 判断正确后对 lastLen 值的更改, 影响循环中之后的 `lastLen == 0; lastLen != 0;` 的判断.
* 输入的极端情况:
    * 数组 s 为空
    * 数组 s 元素全为空格



##### 复杂度分析

* 时间复杂度: O(n), n 为最后一个单词及其右边空格长度之和. 
* 空间复杂度: O(1)



##### 思路二: 双指针

* 用变量 end 标记最后一个字符的数组下标. 用变量 start 标记最后一个单词左边第一个空格的数组下标.



```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    let end = s.length - 1;
    while (s[end] == ' ' && end >= 0) {
        end--;
    }
    if (end < 0) {
        return 0;
    }
    let start = end;
    while (s[start] != ' ' && start >= 0) {
        start--;
    }
    return end - start;
};
```



##### 题外话

* 在思路一中, for() 循环中包含三个 if() 判断语句. 当数组 s 中元素全为空格时, for() 循环中判断语句都要执行一遍, 即 3n 次. 而在双指针法中只需执行 n 次相关语句.



##### 复杂度分析

* 时间复杂度: O(n), n 为最后一个单词及其右边空格长度之和.
* 空间复杂度: O(1)



##### 思路, 程序参考

* [秦时明月: 58. 最后一个单词的长度](https://leetcode-cn.com/problems/length-of-last-word/solution/58-zui-hou-yi-ge-dan-ci-de-chang-du-by-alexer-660/)