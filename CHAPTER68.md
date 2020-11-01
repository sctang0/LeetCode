### [68. 文本左右对齐-逐层递归](https://leetcode-cn.com/problems/text-justification/)

##### 题目描述

* 给定一个单词数组和一个长度 `maxWidth` ，重新排版单词，使其成为每行恰好有 `maxWidth` 个字符，且左右两端对齐的文本。
    * 你应该使用“贪心算法”来放置给定的单词；也就是说，尽可能多地往每行中放置单词。必要时可用空格 `' '` 填充，使得每行恰好有 `maxWidth` 个字符。
    * 要求尽可能均匀分配单词间的空格数量。如果某一行单词间的空格不能均匀分配，则左侧放置的空格数要多于右侧的空格数。
    * 文本的最后一行应为左对齐，且单词之间不插入额外的空格。

* 说明:

    * 单词是指由非空格字符组成的字符序列。
    * 每个单词的长度大于 0 ，小于等于 `maxWidth` 。
    * 输入单词数组 `words` 至少包含一个单词。

* 示例：

    * ```example
        Input:
        words = [ "This", "is", "an", "example", "of", "text", "justification." ]
        maxWidth = 16
        
        Output:
        [
           "This    is    an",
           "example  of text",
           "justification.  "
        ]
        ```
        
    * ```example
        Input:
        words = [ "What", "must", "be", "acknowledgment", "shall", "be" ]
        maxWidth = 16
        
        Output:
        [
          "What   must   be",
          "acknowledgment  ",
          "shall be        "
        ]
        
        解释: 注意最后一行的格式应为 "shall be    " 而不是 "shall     be",
              因为最后一行应为左对齐，而不是左右两端对齐。       
              第二行同样为左对齐，这是因为这行只包含一个单词。
        ```

    * ```example
        Input:
        words = [ 
                  "Science", "is", "what", "we", "understand", "well",
                  "enough", "to", "explain", "to", "a", "computer.",
                  "Art", "is", "everything", "else", "we", "do" 
                ]
        maxWidth = 20
        
        Output:
        [
          "Science  is  what we",
          "understand      well",
          "enough to explain to",
          "a  computer.  Art is",
          "everything  else  we",
          "do                  "
        ]
        ```

##### 思路

* 对齐规则:
    * 最后一行
        * 单词左对齐
        * 单词间空格数为一
    * 非最后一行
        * 单词左右对齐
        * 单词间空格均匀分布
        * 无法均匀分布时, 左侧空格数多于右侧空格数.



* 递归的最小重复单元(形成输出数组 `res` 的一个字符串)

    * Recursion terminatior (递归终止)
        * 递归遍历到数组 `words` 的末尾
    * Process logic in current level (当前层的过程逻辑)
        * 非最后一行
            * 确定 `words` 中能加入该行字符串的个数, 并将字符串保存到数组 `rowArr` .
            * 对数组 `rowArr` 进行"处理", 形成符合非最后一行规则的字符串, 保存到数组 `res` .
        * 最后一行
            * 确定 `words` 中能加入该行字符串的个数, 并将字符串保存到数组 `rowArr` .
            * 对数组 `rowArr` 进行"处理", 形成符合最后一行规则的字符串, 保存到数组 `res` .
    * Drill down (去下一层)
        * `return appendLine(words, maxWidth, res, i)`
            * `i`: 对应下一次递归, 加入数组 `rowArr` 的首个字符串, 在数组 `words` 中的下标.
            * `res`: 要输出的数组

    * Reverse the current level status if needed (进行下一层的操作之后, 会回到这里. 可以在这里做一些收尾的工作.)
        * `res.pop()`
            * 删去数组数组 `res` 最后一个数组. 这样在递归结束时, 数组 `res` 可以清空.

```javascript
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string []}
 */
var fullJustify = function(words, maxWidth) {
    const appendLine = (level, words, maxWidth, res, start) => {
        // Recursion terminatior (递归终止)
        if (start >= words.length) {
            return res;
        }
        
        // Process logic in current level (当前层的过程逻辑)
        let rowArr = [words[start]];
        let count = words[start].length;
        let i = start + 1;
        while (i < words.length && count + words[i].length < maxWidth) {
            count += words[i].length + 1;
            rowArr.push(words[i]);
            i ++;
        }
        let rowStr = '';
        if (i < words.length) {
            let space = maxWidth - count + rowArr.length - 1;
            let eachSpace = parseInt(space / (rowArr.length - 1));
            let extSpace = space % (rowArr.length - 1);
            for (let j = 0; j < rowArr.length; j ++) {
                rowStr += rowArr[j];
                if (j !== rowArr.length - 1) {
                    let space = eachSpace;
                    if (extSpace > 0) {
                        space += 1;
                        extSpace --;;
                    }
                    while (space -- > 0) {
                        rowStr += ' ';
                    }
                }
            }
        } else {
            for (let j = 0; j < rowArr.length; j ++) {
                if (j < rowArr.length - 1) {
                    rowStr += rowArr[j] + ' ';
                } else {
                    rowStr += rowArr[j];
                }
            }
        }
        while (rowStr.length < maxWidth) {
            rowStr += ' ';
        }
        res.push(rowStr);
        
        // Drill down (去下一层)
        return appendLine(level + 1, words, maxWidth, res, i);
        
        // Reverse the current level status if needed (进行下一层的操作之后, 会回到这里. 可以在这里做一些收尾的工作.)
        res.pop();
    }
    return appendLine(0, words, maxWidth, [], 0);
};
```

##### 复杂度分析

* 时间复杂度: O(m * r), `m = maxWidth r = res.length` . m * r, 为最后输出的数组 `res` 包含的字符总数. 
* 空间复杂度: 
    * 最坏空间复杂度, O(n * m), `n = words.length m = maxWidth` . 此时, 数组 `words` 每一个字符串的长度, 都大于等于 `maxWidth / 2` .
    * 最好空间复杂度, O(m), `m = maxWidth` . 此时, 形成的结果数组的长度为 1 .



##### 题外话

* [arr.pop()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)：`pop()` 方法从数组中删除最后一个元素，并返回该元素的值。
    * 此方法更改数组 `arr` ，变为不包含数组最后一个元素的数组（若 `arr.length >= 1`）。



##### 思路, 程序参考

* [raymond-yan: 68. 文本左右对齐](https://leetcode-cn.com/problems/text-justification/solution/wen-ben-zuo-you-dui-qi-javascript-ti-jiao-zhong-ji/)
* [覃超: 递归 & 分治](https://time.geekbang.org/course/detail/100019701-42710)

