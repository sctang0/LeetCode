### [206. 反转链表-迭代, 递归](https://leetcode-cn.com/problems/reverse-linked-list/)

##### 题目描述

* 反转一个单链表

* 示例

    * ```example
        输入: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
        输出: 5 -> 4 -> 3 -> 2 -> 1 -> NULL
        ```

* 进阶

    * 你可以迭代或递归地反转链表. 你能否用两种方法解决这道题?



##### 思路一: 迭代

* 定义输出链表 `prev`
* 顺序遍历链表 `head` , 将其中的元素移入链表 `prev` .

* 图解

<div align = center>
    <img src = "https://github.com/sctang0/DataStructure-LeetCode/blob/main/images/01.array-linkList/01.001.01.png" alt = "Citizendium: Fibonacci number">
</div>

```javascript
/**
 * Definition for singly linked list
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    let prev = null;
    let curr = head;
    while (curr != null) {
        let next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

##### 复杂度分析

* 时间复杂度: O(n), `n` 为链表 `head` 的长度. 程序遍历了链表 `head` .
* 空间复杂度: O(1)

##### 题外话

* `curr` 为 `current` : "当下" 的缩写. `prev` 为 `previous` : "以前的" 的缩写.
* [迭代](https://zh.wikipedia.org/wiki/%E8%BF%AD%E4%BB%A3): 重复反馈过程的活动, 其目的通常是为了接近并到达所需的目标或结果.



##### 思路二: 递归

* 用递归算法, 实现将链表 `head` 元素移入链表 `prev` .

```javascript
/**
 * Definition for singly linked list
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    let reverse = (prev, curr) => {
        if (! curr) {
            return prev;
        }
        let next = curr.next;
        curr.next = prev;
        return reverse(curr, next);
    }
    return reverse(null, head);
}
```

##### 复杂度分析

* 时间复杂度: O(n), `n` 为链表 `head` 的长度. 程序递归了 `n` 次.
* 空间复杂度: O(1)



##### 思路, 程序参考

* [秦时明月: 206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/solution/206-fan-zhuan-lian-biao-by-alexer-660/)
    * 注: 程序 (所有) 都是照搬该位作者的
* [Nodreame: 206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/solution/js-san-chong-jie-fa-di-gui-wei-di-gui-die-dai-by-n/)
* [力扣 (LeetCode) : 206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-by-leetcode/)
* [洪水猛兽行: 函数, 变量名命名的四种方法](https://blog.csdn.net/yuhengyue/article/details/78464448)

##### 画图工具

* [Excalidraw](https://excalidraw.com/)