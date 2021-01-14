### [61. 旋转链表-链表转环](https://leetcode-cn.com/problems/rotate-list/)

##### 题目描述

* 给定一个链表，旋转链表，将链表每个节点向右移动 *k* 个位置，其中 *k* 是非负数。

    * 示例:

    * ```example
        输入: 1 -> 2 -> 3 -> 4 -> 5 -> NULL, k = 2
        输出: 4 -> 5 -> 1 -> 2 -> 3 -> NULL
        解释:
        向右旋转 1 步: 5 -> 1 -> 2 -> 3 -> 4 -> NULL
        向右旋转 2 步: 4 -> 5 -> 1 -> 2 -> 3 -> NULL
        ```



##### 思路: 链表转环

<div align = center>
    <img src="https://github.com/sctang0/LeetCode/blob/master/images/01-99/chapter61.gif" alt="图片来源: 一个歪卜: 61. 旋转链表" width="70%" />
</div>

```javascript
/**
 * Definition for singly-linked list
 * function ListNode (val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function (head, k) {
    if (! head || ! head.next) {
        return head;
    }
    let curr = head;
    let len = 0;
    while (++ len && curr.next) {
        curr = curr.next;
    }
    curr.next = head;
    k %= len;
    while (++ k < len) {
        head = head.next;
    }
    let tmp = head;
    head = head.next;
    tmp.next = null;
    return head;
}
```



##### 复杂度分析

* 时间复杂度: O(n), n 为链表的长度. 平均遍历链表 1.5 遍.
* 空间复杂度: O(1)



##### 思路, 程序参考

* [一个歪卜: 61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/solution/dong-tu-suan-fa-xuan-zhuan-lian-biao-si-chong-ji-3/)

##### 图片来源

* [一个歪卜: 61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/solution/dong-tu-suan-fa-xuan-zhuan-lian-biao-si-chong-ji-3/)