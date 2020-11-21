### 71.1 栈-程序模板

##### 基于数组

```javascript
class StackBasedArray {
    constructor () {
        this._count = 0;
        this._items = [];
    }
    /**
     * numberPlace 从 1 开始计数, 而不是 0
     * 例如: _items = [ 0, 1, 2, 3 ], numberInsert = 1, element = 4
     * 返回: _items = [ 4, 0, 1, 2, 3]
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
    push (element) {
        this._items[this._count] = element;
        this._count ++;
    }
    pop () {
        if (this._count >= 1) {
            this._items[this._count] = null;
            this._count --;
        } else {
            return null;
        }
    }
    peek () {
        return this._items[this._count - 1];
    }
    isEmpty () {
        return this._count === 0;
    }
    size () {
        return this._count;
    }
    clear () {
        this._count = 0;
        this._items = [];
    }
    join (symbol) {
        this._count = 1;
        return this._items.join(symbol);
    }
    display () {
        return this._items;
    }
}
var useStack = function () {
    let stack = new StackBasedArray();
    console.log(stack.isEmpty());
    stack.push("1");
    stack.push("2");
    console.log(stack.display());
    console.log(stack.isEmpty());
    stack.insert(1, '0');
    console.log(stack.display());
    console.log(stack.size());
    stack.clear();
    console.log(stack.display());

    return;
};
useStack();

/**
 * console:
     true
     [ '1', '2' ]
     false
     [ '0', '1', '2' ]
     3
     []
 */
```



##### 基于链表

```javascript
class Node {
    constructor (element) {
        this.element = element;
        this.next = null;
    }
}
class StackBasedLinkedList {
    constructor () {
        this._top = null;
        this._count = 0;
    }
    /**
     * numberPlace 从 1 开始计数, 而不是 0
     * 例如: _items = 0 <- 1 <- 2 <- 3 , numberInsert = 1, element = 4
     * 返回: _items = 4 <- 0 <- 1 <- 2 <- 3
     */
    insert (numberPlace, element) {
        let node = new Node(element);
        if (this._top === null) {
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
    push (element) {
        this._count ++;
        let node = new Node(element);
        if (this._top === null) {
            this._top = node;
        } else {
            node.next = this._top;
            this._top = node;
        }
    }
    pop () {
        if (this._top === null) {
            return false;
        }
        let element = this._top.element;
        this._top = this._top.next;
        element = null;
        this._count --;
    }
    clear () {
        this._top = null;
        this._count = 0;
    }
    size () {
        return this._count;
    }
    isEmpty () {
        return this._count === 0;
    }
    search (element) {
        if (this._top === null) {
            return false;
        }
        let tmpTop = this._top;
        while (tmpTop !== null) {
            if (element !== tmpTop.element) {
                tmpTop = tmpTop.next;
            } else {
                return true;
            }
        }
        return false;
    }
    display () {
        if (this._top !== null) {
            let tmp = this._top;
            let resStr = tmp.element;
            tmp = tmp.next;
            while (tmp !== null) {
                resStr = resStr + '->' + tmp.element;
                tmp = tmp.next;
            }
            return resStr;
        }
        return this._top;
    }
}
var useStack = function () {
    let stack = new StackBasedLinkedList();
    stack.push('1');
    stack.push('2');
    stack.insert(1, 0);
    console.log(stack.search('1'));
    console.log(stack.display());
    console.log(stack.isEmpty());
    stack.clear();
    console.log(stack.display());

    return;
};
useStack();

/**
 * console:
     true
     2->1->0
     false
     null
 */
```



##### 复杂度分析

* [arr.join()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.5)
    * 时间复杂度: O(n), `n = arr.length` . 用 `while` 循环, 依次将数组 `arr` 中元素, 存放到返回字符串 `R` 末尾.
    * 空间复杂度: O(n * m), `n = arr.length; m = arr[n].length` . 定义返回字符串 `R`,  储存数组 `arr` 中所有元素.

##### 题外话

* [数组长度](https://zhidao.baidu.com/question/499788673)

    * JavaScript 数组的长度可以是无限的, 只要内存允许的话. 数组的初始长度可以设置, 如果需要, 随后该长度可以自动增长. 使用数字串当作数组的索引, 等价于直接使用数字索引.

    * JavaScript 数组实际上是个 Key-Value 对. Key 不仅可以使数字, 还可以是其它对象.

        * ```javascript
            var arr = new Array(2);
            arr[0] = 1;
            arr['second'] = 2;
            arr['third'] = 3;
            console.log(arr['0'] + ' ' + arr['second'] + [' '] + arr['third']);
            console.log(arr.length);
            /**
             * console:
                 1 2 3
                 2
             */
            ```


* [JavaScript 链式栈优点](https://blog.csdn.net/zhangxiangDavaid/article/details/28679027)
    * 一般, 链式栈与顺序栈相比, 优点是可以动态扩容.
        * 不过, JavaScript 数组长度是无限的, 只要内存允许. 即使设置了数组长度, 如果需要的话, 随后该长度也可以自动增长. 无需担心溢出.
            * 所以, 在 JavaScript 中, 链式栈的优点
                * 插入, 删除灵活
                * 物理地址不必相连

##### 思路, 程序参考

* [<学习 JavaScript 数据结构与算法(第三版)>](https://www.dedao.cn/eBook/N5lDqb9b47pXZxGn1kBzPlMyQArYv0qyee0qe85E2aVKdo9jNgOLRmDJ6nXLm16K)
    * 基于数组的程序实现
* [王争: 栈](https://time.geekbang.org/column/article/41222)
    * 基于链表的程序实现. Github 源程序链接: [StackBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/08_stack/StackBasedOnLinkedList.js)
* [101刘辰: JavaScript 数组中长度最大是多少? 能设置吗?](https://zhidao.baidu.com/question/499788673)
* [苏叔叔: 栈的实现: 链式栈](https://blog.csdn.net/zhangxiangDavaid/article/details/28679027)
* [JavaScript 数组释放内存](https://segmentfault.com/q/1010000018717541)