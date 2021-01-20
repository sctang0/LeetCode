### [142. 环形链表II-标记](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

* 给定一个链表, 返回链表开始入环的第一个节点. 如果链表无环, 则返回 `null` .

    * 为了表示给定链表中的环, 我们使用整数 `pos` 来表示链表尾连接到链表中的位置 ( 索引从 0 开始 ) . 如果 `pos` 是 -1 , 则在该链表中没有环. 注意, `pos` 仅仅是用于标识环的情况, 并不会作为参数传递到函数中.
    * 说明
        * 不允许修改给定的链表
        * 链表中节点的数目范围在范围 `[0, 104]` 内
        * `-105 <= Node.val <= 105`
        * `pos` 的值为 `-1` 或者链表中的一个有效索引

* 示例

    * 示例一

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0142.01.png)

        * ```example
            输入: head = [ 1 ], pos = -1
            输出: 返回 null
            解释: 链表中没有环
            ```

    * 示例二

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0142.02.png)

        * ```example
            输入: head = [ 1, 2 ], pos = 0
            输出: 返回索引为 0 的链表节点
            解释: 链表中有一个环, 其尾部连接到第一个节点.
            ```

    * 示例三

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0142.03.png)

        * ```example
            输入: head = [ 3, 2, 0, -4 ], pos = 1
            输出: 返回索引为 1 的链表节点
            解释: 链表中有一个环, 其尾部连接到第二个节点.
            ```



##### 思路: 标记

```javascript
/**
 * Definition for singly-linked list.
 * function ListNOde(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function(head) {
    while (head && head.next) {
        if (head.flag) {
            return head;
        } else {
            head.flag = 1;
            head = head.next
        }
    }
    return null;
}
```

##### 复杂度分析

* 时间复杂度: O(n), `n` 为链表 `head` 的长度.
* 空间复杂度: O(1)

##### 题外话

* [listNode.flag](https://stackoverflow.com/questions/17402125/what-is-a-flag-variable): 未定义时, 为 `undefined` .

    * ```javascript
        class Node {
            constructor (element) {
                this.element = element;
                this.next = null;
            }
        }
        let i = new Node(1);
        console.log(i.flag);
        i.flag = 2;
        console.log(i.flag);
        i.flag = false;
        console.log(i.flag);
        
        /**
         * std:
         *   undefined
         *   2
         *   false
         *
         * 注: 由 WebStorm 编译
         */
        ```



##### 思路, 程序参考

* [秦时明月: 142. 环形链表II](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/142-huan-xing-lian-biao-ii-by-alexer-660/)