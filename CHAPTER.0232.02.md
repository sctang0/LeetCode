### 232.2. 双栈实现队列程序模板-顺序, 链式

##### 顺序

```javascript
class Queue {
    constructor () {
        this._pushArr = [];
        this._popArr = [];
    }
    push (element) {
        this._pushArr.push(element);
    }
    pop () {
        if (! this._popArr.length) {
            while (this._pushArr.length) {
                this._popArr.push(this._pushArr.pop());
            }
        }
        return this._popArr.pop();
    }
    peek () {
        if (! this._popArr.length) {
            while (this._pushArr.length) {
                this._popArr.push(this._pushArr.pop());
            }
        }
        return this._popArr[this._popArr.length - 1];
    }
    isEmpty () {
        return this._pushArr.length === 0 && this._popArr.length === 0;
    }
    display () {
        let res = new Array(this._popArr.length + this._pushArr.length);
        let i = 0;
        let j = 0;
        let lenPop = this._popArr.length;
        let lenPush = this._pushArr.length;
        while (lenPop) {
            res[i] = this._popArr[lenPop - 1];
            i ++;
            lenPop --;
        }
        while (j < lenPush) {
            res[i] = this._pushArr[j];
            j ++;
            i ++;
        }
        return res;
    }
    size () {
        return this._popArr.length + this._pushArr.length;
    }
}
var useQueue = function () {
    let queue = new Queue();
    console.log(queue.isEmpty());
    queue.push('1');
    queue.push('2');
    queue.push('3');
    console.log(queue.display());
    console.log(queue.size());
    console.log(queue.pop());
    console.log(queue.isEmpty());
    console.log(queue.push('4'));
    console.log(queue.display());
    console.log(queue.size());
};
useQueue();

/**
 * console
     true
     [ '1', '2', '3' ]
     3
     1
     false
     undefined
     [ '2', '3', '4' ]
     3
 */
```



##### 链式

```javascript
class Node {
    constructor(element) {
        this._element = element;
        this.next = null
    }
}

class Queue {
    constructor() {
        this._topPushLink = null;
        this._countPushLink = 0;
        this._topPopLink = null;
        this._countPopLink = 0;
    }
    size () {
        return this._countPushLink + this._countPopLink;
    }
    push (element) {
        let node = new Node(element);
        if (this._countPushLink === 0) {
            this._topPushLink = node;
        } else {
            node.next = this._topPushLink;
            this._topPushLink = node;
        }
        this._countPushLink ++;
        return this._topPushLink;
    }
    pop () {
        if (this._countPushLink !== 0 && this._countPopLink === 0) {
            while (this._countPushLink) {
                let node = this._topPushLink;
                if (this._countPushLink === 1) {
                    this._topPushLink = null;
                } else {
                    this._topPushLink = this._topPushLink.next;
                }
                node.next = this._topPopLink;
                this._topPopLink = node;
                this._countPushLink--;
                this._countPopLink++;
            }
        }
        let node = this._topPopLink;
        if (this._countPopLink !== 0) {
            this._topPopLink = this._topPopLink.next;
            this._countPopLink -= 1;
        }
        return node._element;
    }
    isEmpty () {
        return this._countPushLink === 0 && this._countPopLink === 0;
    }
    peek () {
        if (this._countPopLink === 0) {
            let node = this._topPushLink;
            let count = this._countPushLink;
            while (count > 1) {
                node = node.next;
                count --;
            }
            return node._element;
        }
        return this._topPopLink._element;
    }
    display () {
        let res = new Array(this._countPushLink + this._countPopLink);
        let countPop = this._countPopLink;
        let countPush = this._countPushLink;
        let topPop = this._topPopLink;
        let topPush = this._topPushLink;
        let i = 0;
        while (countPop) {
            res[i] = topPop._element;
            topPop = topPop.next;
            i ++;
            countPop --;
        }
        i = this._countPushLink + this._countPopLink - 1;
        while (countPush) {
            res[i] = topPush._element;
            topPush = topPush.next;
            i--;
            countPush--;
        }
        return res;
    }
}
var useQueue = function () {
    let queue = new Queue();
    console.log(queue.isEmpty());
    queue.push('1');
    queue.push('2');
    queue.push('3');
    console.log(queue.display());
    console.log(queue.size());
    console.log(queue.pop());
    console.log(queue.isEmpty());
    console.log(queue.push('4'));
    console.log(queue.display());
    console.log(queue.size());
};
useQueue();

/**
 * console
     true
     [ '1', '2', '3' ]
     3
     1
     false
     Node { element: '4', next: null }
     [ '2', '3', '4' ]
     3
 */
```



##### 复杂度分析

* [arr.pop()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6)
    * 时间复杂度: O(1). `arr.pop()` 根据 `length` 属性来确定最后一个元素的位置.
    * 空间复杂度: O(1). `arr.pop()` 调用过程中, 并没有开辟一块 `length - 1` 大小的空间, 来存储前 `length - 1` 个元素. 而是, 直接对数组 `arr` 进行删值操作.

* [arr.push( element1, element2, ... , elementN )](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7)
    * 时间复杂度: O(n), `n = element.length` . `arr.push()` 根据 `length` 属性来确定从哪里插入给定值. `arr.push()` 内部定义数组 `items` 来从左至右储存 `element1 ~ N` 的值. 并用 `while` 循环依次加入数组 `arr` 末尾.
    * 空间复杂度: O(n), `n = element.length` . `arr.push()` 调用过程中, 定义数组 `items` 来存储 `element1 ~ N` 的值.

* [`arr.length`](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.5.2)
    * 时间复杂度: O(1). `length` 是 `Array` 的数据属性( data property ).
    * 空间复杂度: O(1)



##### 程序参考

* [王争: 队列](https://time.geekbang.org/column/article/41330)
    - 基于队列的程序实现. Github 源程序链接: [QueueBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/09_queue/QueueBasedOnLinkedList.js)
* [吕善柯-三七互娱: 232. 两个栈相互合作实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/dan-ke-xi-lie-yong-shi-8614nei-cun-10000-by-lvshan/)