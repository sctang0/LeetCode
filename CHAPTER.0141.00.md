### [141. 环形链表-快慢指针, 标记](https://leetcode-cn.com/problems/linked-list-cycle/)

* 给定一个链表, 判断链表中是否有环.

    * 如果链表中有某个节点, 可以通过连续跟踪 `next` 指针再次到达, 则链表中存在环. 为了表示给定链表中的环, 我们使用整数 `pos` 来表示链表尾连接到链表中的位置 ( 索引从 0 开始 ) . 如果 `pos` 是 -1 , 则在该链表中没有环.
    * 说明
        * `pos` 不作为参数进行传递, 仅仅是为了标识链表的实际情况.
        * 如果链表中存在环, 则返回 `true` . 否则, 返回 `false` .
        * 链表中节点的数目范围是 `[ 0, 104 ]`
        * `-105 <= Node.val <= 105`
        * `pos` 为 `-1` 或者链表中的一个 有效索引.

* 示例

    * 示例一

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0141.01.png)

        * ```example
            输入: head = [ 1 ], pos = - 1
            输出: false
            解释: 链表中没有环.
            ```

    * 示例二

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0141.02.png)

        * ```example
            输入: head = [ 1, 2 ], pos = 0
            输出: true
            解释: 链表中有一个环, 其尾部连接到第一个节点.
            ```

    * 示例三

        * ![img](https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0141.03.png)

        * ```example
            输入: head = [ 3, 2, 0, - 4 ], pos = 1
            输出: true
            解释: 链表中有一个环, 其尾部连接到第二个节点.
            ```




##### 思路一: 快慢指针

* 定义快指针 `fast` , 慢指针 `slow` .
    * 快指针每次走两格, 慢指针每次走一格.
* 若将两指针, 放在环中的任意位置 (环的节点数为 `n` ) .
    * 在环中, 每次 `fast` 比 `slow` 多移动一格. 即在 `fast` 移动的方向上, `fast` 与 `slow` 之间的距离减一.
    * 则至多 `n` 步后, `fast` 与 `slow` 相遇.

* 举例

<div align = center>
    <img src = "https://github.com/sctang0/LeetCode/blob/master/images/100-199/100-199.0141.04.png" alt = "img">
</div>

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
    if (! head || ! head.next) {
        return false;
    }
    let slow = head;
    let fast = head.next;
    while (fast !== null && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
        if (fast === slow) {
            return true;
        }
    }
    return false;
};
```

##### 复杂度分析

* 时间复杂度: O(n), `n` 为链表 `head` 长度.
    * 链表 `head` 中有环时.
        * 在环中, 每次 `fast` 比 `slow` 多移动一格. 即在 `fast` 移动的方向上, `fast` 与 `slow` 之间的距离减一.
        * `fast` "追赶" `slow` 最长距离为 `n` ( 此时, `head` 为首尾相连的环形链表 ). 即, 最多 `n` 步后, `fast` 与 `slow` 相遇.
* 空间复杂度: O(1)

##### 题外话

* 若 `fast.next = null` , 在执行 `fast = fast.next.next` 时, 会报错.
    * 于是, 在 `while` 运行条件中, 加入了 `fast.next` .



##### 思路二: 标记

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
    while (head && head.next) {
        if (head.flag) {
            return true
        } else {
            head.flag = 1;
            head = head.next;
        }
    }
    return false;
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

* [秦时明月: 141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/solution/141-huan-xing-lian-biao-by-alexer-660/)

##### 作图工具

- [Excalidraw](https://excalidraw.com/)