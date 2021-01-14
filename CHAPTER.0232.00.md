### [232. 两个栈相互合作实现队列-顺序队列, 链式队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

##### 题目描述

* 请你仅使用两个栈实现先入先出队列. 队列应当支持一般队列的支持的所有操作 ( `push`, `pop`, `peek`, `empty` )

    * 实现 `MyQueue` 类

        * `void push(int x)`: 将元素 `x` 推到队列的末尾
        * `int pop()`: 从队列的开头移除并返回元素
        * `int peek()`: 返回队列开头的元素
        * `boolean empty()`: 如果队列为空, 返回 `true` ; 否则, 返回 `false`

    * 说明

        * 你只能使用标准的栈操作 -- 也就是只有 `push to top` , `peek/pop from top` , `size` , 和 `is empty` 操作是合法的.
        * 你所使用的语言也许不支持栈. 你可以使用 `list` 或者 `deque` (双端队列) 来模拟一个栈, 只要是标准的栈操作即可.

    * 进阶

        * 你能否实现每个操作均摊时间复杂度为 `O(1)` 的队列? 换句话说, 执行 `n` 个操作的总时间复杂度为 `O(n)` , 即使其中一个操作可能花费较长时间.

    * 提示

        * `1 <= x <= 9`
        * 最多调用 100 次 `push` , `pop` , `peek ` 和 `empty`
        * 假设所有操作都是有效的 (例如, 一个空的队列不会调用 `pop` 或者 `peek` 操作)

    * 示例

        * ```example
            输入：
                [ "MyQueue", "push", "push", "peek", "pop", "empty" ]
                [ [], [ 1 ], [ 2 ], [], [], [] ]
            输出：
                [ null, null, null, 1, 1, false ]
            
            解释：
                MyQueue myQueue = new MyQueue();
                myQueue.push(1); // queue is: [ 1 ]
                myQueue.push(2); // queue is: [ 1, 2 ] (leftmost is front of the queue)
                myQueue.peek();  // return 1
                myQueue.pop();   // return 1, queue is [ 2 ]
                myQueue.empty(); // return false
            ```



##### 思路: 顺序队列

* 定义栈 `pushStack` , `popStack` . (注: 演示中使用的是顺序栈, 且只描述 `pop()` , `push()` 的运行思路)
    * 加入队列末尾的值, 传入 `pushStack` .
    * 移出队列值时
        * 若, `popStack` 为空
            * 将 `pushStack` 中元素全部移入 `popStack` (移入后, `pushStack` 为空)
            * 移出 `popStack` 中一个元素
        * 若, `popStack` 不为空
            * 移出 `popStack` 中一个元素
    * 示例
        * [ 'push', 'push', 'push', 'pop', 'pop' ] , [ 1, 2, 3, [], [] ]
            1. `pushStack = [ 1 ] popStack = []`
            2. `pushStack = [ 1, 2 ] popStack = []`
            3. `pushStack = [ 1, 2, 3 ] popStack = []`
            4. 分两步
                1. `pushStack = [] popStack = [ 3, 2, 1 ]`
                2. `pushStack = [] popStack = [ 3, 2 ]`
            5. `pushStack = [] popStack = [ 3 ]`
        * [ 'push', 'pop', 'push', 'push', 'pop' ] , [ 1, [], 3, 4, [] ]
            1. `pushStack = [ 1 ] popStack = []`
            2. 分两步
                1. `pushStack = [] popStack = [ 1 ]`
                2. `pushStack = [] popStack = []`
            3. `pushStack = [ 3 ] popStack = []`
            4. `pushStack = [ 3, 4 ] popStack = []`
            5. 分两步
                1. `pushStack = [] popStack = [ 4, 3 ]`
                2. `pushStack = [] popStack = [ 4 ]`

```javascript
class MyQueue {
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
    empty () {
        return ! this._pushArr.length && ! this._popArr.length;
    }
}
```

##### 复杂度分析

* 时间复杂度: 在该题中, 方法 [arr.push()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7) [arr.pop()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6) 的时间复杂度为 O(1) .
* 空间复杂度:在该题中, 方法 [arr.push()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7) [arr.pop()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6) 的空间复杂度为 O(1) .



##### 思路, 程序参考

* [吕善柯-三七互娱: 232. 两个栈相互合作实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/dan-ke-xi-lie-yong-shi-8614nei-cun-10000-by-lvshan/)
* [liweiwei: 232. 两个栈相互合作实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/shi-yong-liang-ge-zhan-yi-ge-zhuan-men-ru-dui-yi-g/)
* [王争: 队列](https://time.geekbang.org/column/article/41330)
    * 基于队列的程序实现. Github 源程序链接: [QueueBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/09_queue/QueueBasedOnLinkedList.js)



##### 思路: 链式队列

```javascript
class Node {
    constructor(element) {
        this._element = element;
        this.next = null
    }
}

class MyQueue {
    constructor() {
        this._topPushLink = null;
        this._countPushLink = 0;
        this._topPopLink = null;
        this._countPopLink = 0;
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
                this._countPushLink --;
                this._countPopLink ++;
            }
        }
        let node = this._topPopLink;
        if (this._countPopLink !== 0) {
            this._topPopLink = this._topPopLink.next;
            this._countPopLink -= 1;
        }
        return node._element;
    }
    empty () {
        return ! this._countPushLink && ! this._countPopLink;
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
}
```



##### 程序参考

* [吕善柯-三七互娱: 232. 两个栈相互合作实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/dan-ke-xi-lie-yong-shi-8614nei-cun-10000-by-lvshan/)

* [王争: 队列](https://time.geekbang.org/column/article/41330)
    * 基于队列的程序实现. Github 源程序链接: [QueueBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/09_queue/QueueBasedOnLinkedList.js)