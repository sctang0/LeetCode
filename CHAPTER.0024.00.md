### [24. 两两交换链表中的节点-迭代](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

- 给定一个链表, 两两交换其中相邻的节点, 并返回交换后的链表.

- 你不能只是单纯的改变节点内部的值, 而是需要实际的进行节点交换.

    - 示例一

        - ![img](https://github.com/sctang0/LeetCode/blob/master/images/01-99/01-99.0024.01.png)

        - ```
                输入: head = [ 1, 2, 3, 4 ]
                输出: [ 2, 1, 4, 3 ]
            ```

    - 示例二

        - ```
                输入: head = []
                输出: []
            ```

    - 示例三

        - ```
                输入: head = [ 1 ]
                输出: [ 1 ]
            ```

- 进阶

    - 不修改链表节点值的情况下解决问题 (也就是说, 仅修改节点本身.)

##### 思路: 迭代

* 定义一个哨兵节点 `zeroNode` , 并指向链表 `head`
* 两两交换 `zeroNode` 右侧节点

- 图解

<div align = center>
    <img src = "https://github.com/sctang0/LeetCode/blob/master/images/01-99/01-99.0024.02.png" alt = "img">
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
 * @return {ListNode}
 */
var swapPairs = function(head) {
    if (! head || ! head.next) {
        return head;
    }
    let res = head.next;
    let zeroNode = new ListNode(0);
    zeroNode.next = head;
    while (zeroNode.next != null && zeroNode.next.next != null) {
        let tmpNode = zeroNode.next;
        zeroNode.next = tmpNode.next;
        tmpNode.next = zeroNode.next.next;
        zeroNode.next.next = tmpNode;
        zeroNode = zeroNode.next.next;
    }
    return res;
};
```

##### 复杂度分析

- 时间复杂度: O(n), `n` 为链表 `head` 的长度. `while` 循环执行了 `n / 2` 次.
- 空间复杂度: O(1)

##### 题外话

- [迭代](https://zh.wikipedia.org/wiki/迭代): 重复反馈过程的活动, 其目的通常是为了接近并到达所需的目标或结果.
- [反馈](https://zh.wikipedia.org/wiki/反馈): (英语: feedback), 指将系统的输出返回到输入端并以某种方式改变输入.
    - ![img](https://github.com/sctang0/LeetCode/blob/master/images/01-99/01-99.0024.03.png)
- [哨兵](https://www.zhihu.com/question/27155932): 顾名思义, 是用来解决国家之间边界问题的, 不直接参与生产活动. 同样, 计算机科学中提到的哨兵, 也用来解决边界问题.



##### 思路, 程序参考

- [秦时明月: 24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/24-liang-liang-jiao-huan-lian-biao-zhong-de-jie--7/)

##### 图片思路参考

- [秦时明月: 24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/24-liang-liang-jiao-huan-lian-biao-zhong-de-jie--7/)

##### 作图工具

- [Excalidraw](https://excalidraw.com/)