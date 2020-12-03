### 232.1. 队列程序模板-顺序队列, 链式队列

##### 细节

|                                 | 顺序队列                                                     |                                                     链式队列 |
| :-----------------------------: | ------------------------------------------------------------ | -----------------------------------------------------------: |
| `insert (numberPlace, element)` | `numberPlace >= 1`  若 `numberPlace > this._count` 则中间空出来的元素为 `undefined` | `this._count >= numberPlace >= 1 ` 若 `numberPlace > this._count` , 返回 `false` . |
|            `size ()`            | 返回 `this._count`                                           |                                                         同左 |
|        `push (element)`         | 无返回值                                                     |                            返回 `element` 对应的 `this._top` |
|            `pop ()`             | 返回删除的值                                                 |                                                         同左 |
|           `clear ()`            | `this._items = []` 数组清空, 无返回值                        |                           所有的节点转化为 `null` , 无返回值 |
|            `isEmpty`            | `return this._count === 0;`                                  |                                                         同左 |
|          `display ()`           | 直接输出数组 `this._items`                                   |                                             用数组保存, 输出 |
|            `peek ()`            | `return this._items[this._count - 1]`                        |                                   遍历到链表末尾, 返回对应值 |



##### 顺序队列

```javascript
class QueueBasedOnArray {
    constructor () {
        this._items = [];
        this._count = 0;
    }
    /**
     * numberPlace 从 1 开始计数, 而不是从 0
     * 例如: _items = [ 0, 1, 2, 3 ], numberInsert = 1, element = 4
     * 返回: _items = [ 4, 0, 1, 2, 3 ]
     */
    insert (numberPlace, element) {
        let i = this._count;
        while (i >= numberPlace) {
            this._items[i] = this._items[i - 1];
            i --;
        }
        this._items[numberPlace - 1] = element;
        this._count ++;
    }
    size () {
        return this._count;
    }
    push (element) {
        this._items[this._count] = element;
        this._count ++;
    }
    pop () {
        if (this._count === 0) {
            return undefined;
        }
        let i = 0;
        let tmpItems = this._items[0];
        while (i < this._count - 1) {
            this._items[i] = this._items[i + 1];
            i ++;
        }
        this._items[this._count - 1] = null;
        this._count --;
        return tmpItems;
    }
    isEmpty () {
        return this._count === 0;
    }
    peek () {
        return this._items[this._count - 1];
    }
    display () {
        return this._items;
    }
    clear () {
        this._count = 0;
        this._items = [];
    }
}
var useQueue = function () {
    let queue = new QueueBasedOnArray();
    console.log(queue.isEmpty());
    queue.push(1);
    queue.push(2);
    queue.push(3);
    console.log(queue.isEmpty());
    queue.insert(1, 0);
    console.log(queue.display());
    queue.pop();
    console.log(queue.display());
    console.log(queue.size());
    queue.push(4);
    console.log(queue.display());
    console.log(queue.peek());
    queue.insert(10, 10);
    console.log(queue.display());
    queue.clear();
    console.log(queue.display());
};
useQueue();

/**
 * console
     true
     false
     [ 0, 1, 2, 3 ]
     [ 1, 2, 3, null ]
     3
     [ 1, 2, 3, 4 ]
     4
     [ 1, 2, 3, 4, <5 empty items>, 10 ]
     []
 */
```



##### [链式队列](https://github.com/wangzheng0822/algo/blob/master/javascript/09_queue/QueueBasedOnLinkedList.js)

```javascript
class Node {
    constructor(element) {
        this._element = element;
        this.next = null
    }
}

class QueueBasedOnLinkedList {
    constructor() {
        this._top = null;
        this._count = 0;
    }
    /**
     * numberPlace 从 1 开始计数, 而不是从 0 开始
     * 例如: _items = 0 <- 1 <- 2 <- 3 , numberInsert = 1, element = 4
     * 返回: _items = 4 <- 0 <- 1 <- 2 <- 3
     */
    insert (numberPlace, element) {
        let node = new Node(element);
        if (this._top === null || numberPlace > this._count) {
            return false;
        }
        let nodeRight = this._top;
        let i = this._count - numberPlace;
        while (i > 0) {
            nodeRight = nodeRight.next;
            i --;
        }
        if (nodeRight.next !== null) {
            let nodeLeft = nodeRight.next;
            node.next = nodeLeft;
            nodeRight.next = node;
        } else {
            nodeRight.next = node;
        }
        this._count ++;
    }
    size () {
        return this._count;
    }
    push (element) {
        let node = new Node(element);
        if (this._count === 0) {
            this._top = node;
        } else {
            node.next = this._top;
            this._top = node;
        }
        this._count ++;
        return this._top;
    }
    pop () {
        if (this._count === 0) {
            return false;
        }
        let count = this._count;
        let top = this._top;
        while (count > 1) {
            top = top.next;
            count --;
        }
        let topRes = top._element;
        top = null;
        this._count --;
        return topRes;
    }
    clear () {
        if (this._count <= 1) {
            this._top = null;
            this._count = 0;
        } else {
            let tmpTop = this._top;
            let tmpTopNext = this._top.next;
            while (tmpTopNext != null) {
                tmpTop = null;
                tmpTop = tmpTopNext;
                tmpTopNext = tmpTopNext.next;
            }
            tmpTopNext = null;
            this._count = 0;
        }
    }
    isEmpty () {
        return this._count === 0;
    }
    peek () {
        if (this._count === 0) {
            return null;
        } else {
            let tmpCount = this._count;
            let tmpTop = this._top;
            while (tmpCount > 1) {
                tmpTop = tmpTop.next;
                tmpCount --;
            }
            return tmpTop._element;
        }
    }
    display () {
        if (this._count === 0) {
            return null;
        }
        let top = this._top;
        let res = top._element;
        top = top.next;
        let i = 1;
        while (i < this._count) {
            res = top._element + ' <- ' + res;
            top = top.next;
            i ++;
        }
        return res;
    }
}
var useQueue = function () {
    let queue = new QueueBasedOnLinkedList();
    console.log(queue.isEmpty());
    queue.push(1);
    queue.push(2);
    queue.push(3);
    console.log(queue.isEmpty());
    queue.insert(1, 0);
    console.log(queue.display());
    queue.pop();
    console.log(queue.display());
    console.log(queue.size());
    queue.push(4);
    console.log(queue.display());
    queue.insert(1, 11);
    console.log(queue.peek());
    queue.insert(2, 10);
    console.log(queue.display());
    queue.clear();
    console.log(queue.display());
};
useQueue();

/**
 * console
     true
     false
     0 <- 1 <- 2 <- 3
     1 <- 2 <- 3
     3
     1 <- 2 <- 3 <- 4
     11
     11 <- 10 <- 1 <- 2 <- 3 <- 4
     null
 */
```



##### 程序参考

* [吕善柯-三七互娱: 232. 两个栈相互合作实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/dan-ke-xi-lie-yong-shi-8614nei-cun-10000-by-lvshan/)

* [王争: 队列](https://time.geekbang.org/column/article/41330)
    - 基于队列的程序实现. Github 源程序链接: [QueueBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/09_queue/QueueBasedOnLinkedList.js)
- [hahahaf: 删除整个链表](https://www.cnblogs.com/fanhaha/p/7118162.html)

