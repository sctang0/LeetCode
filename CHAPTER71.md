### [71. 简化路径-顺序栈, 链式栈](https://leetcode-cn.com/problems/simplify-path/)

##### 题目描述

* 以 Unix 风格给出一个文件的绝对路径, 你需要简化它. 或者换句话说, 将其转换为规范路径.

    * 在 Unix 风格的文件系统中. 一个点 (.) 表示当前目录本身; 此外, 两个点  (..) 表示将目录切换到上一级 (指向父目录) ; 两者都可以是复杂相对路径的组成部分. 更多信息请参阅: [Linux / Unix中的绝对路径 vs 相对路径](https://blog.csdn.net/u011327334/article/details/50355600)

    * 请注意, 返回的规范路径必须始终以斜杠 / 开头, 并且两个目录名之间必须只有一个斜杠 / . 最后一个目录名 (如果存在) 不能以 / 结尾. 此外, 规范路径必须是表示绝对路径的最短字符串.

    * 示例

        * ```example
            输入: "/home/"
            输出: "/home"
            解释: 注意, 最后一个目录名后面没有斜杠.
            ```

        * ```example
            输入: "/../"
            输出: "/"
            解释: 从根目录向上一级是不可行的, 因为根是你可以到达的最高级.
            ```

        * ```example
            输入: "/home//foo/"
            输出: "/home/foo"
            解释: 在规范路径中, 多个连续斜杠需要用一个斜杠替换.
            ```

        * ```example
            输入: "/a/./b/../../c/"
            输出: "/c"
            ```

        * ```example
            输入: "/a/../../b/../c//.//"
            输出: "/c"
            ```

        * ```example
            输入: "/a//b////c/d//././/.."
            输出: "/a/b/c"
            ```

##### 思路: 顺序栈

* Unix 风格
    * 一个点 (`.`) , 表示当前目录.
    * 两个点 (`..`) , 表示上一级目录.
    * 可以出现连续斜杠 (`/`)
* 规范路径
    * 以 `/` 开头
    * 两个目录之间, 只有一个斜杠.
    * 最后一个目录名(如果存在), 不以 `/` 结尾.
    * 为 Unix 风格最短字符串 ()

思路

* 使用 [`arr.split()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法, 以斜杠 (`/`) 为分隔符, 将 Unix 路径 `path` 拆分为若干字符串组成的数组.
* 将字符串顺序压入栈中
    * 不包含元素, 一个点 (`.`) 时, 跳过.
    * 两个点 (`..`) 时, 将当前栈顶元素移出栈.

```javascript
/**
 * @param {string} path
 * @return {string}
 */
class Stack {
    constructor() {
        this._top = 0;
        this._data = [];
    }
    push(element) {
        this._top ++;
        return this._data.push(element);
    }
    pop() {
        this._top --;
        return this._data.pop();
    }
    join(symbol) {
        this._top = 1;
        return this._data.join(symbol);
    }
}
var simplifyPath = function(path) {
    let stack = new Stack();
    let pathArr = path.split('/');
    for (let eachStr of pathArr) {
        if (eachStr == '' || eachStr == '.') {
            continue;
        } else if (eachStr == '..') {
            stack.pop();
        } else {
            stack.push(eachStr);
        }
    }
    return '/' + stack.join('/');
}
```

##### 复杂度分析

* 时间复杂度: O(n), `n = path.split('/').length` .
    * `for` 循环遍历数组 `path.split('/')` .
    * 在该题中, 方法 [arr.push()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7) [arr.pop()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6) 的时间复杂度为 O(1) , [arr.join()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.5) [string.split()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.5.4.14) 的时间复杂度为 O(n) .
* 空间复杂度: O(n), `n = path.split('/').length` .
    * 数组 `pathArr` 长度为 `n = path.split('/').length` .
    * 在该题中, 方法 [arr.push()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.7) [arr.pop()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.6) 的空间复杂度为 O(1) , [arr.join()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.4.4.5) [string.split()](https://www.ecma-international.org/ecma-262/5.1/#sec-15.5.4.14) 的空间复杂度为 O(n) .



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

##### 程序, 思路参考

* [huxiaocheng: 71. 简化路径](https://leetcode-cn.com/problems/simplify-path/solution/tu-jie-miao-dong-by-huxiaocheng-2/)
* [raymond-yan: 71. 简化路径](https://leetcode-cn.com/problems/simplify-path/solution/71-simplify-path-ti-jie-javascript-by-raymond-yan/)
* [101刘辰: JavaScript 数组中长度最大是多少? 能设置吗?](https://zhidao.baidu.com/question/499788673)



##### 思路: 链式栈

```javascript
/**
 * @param {string} path
 * @return {string}
 */
class Node {
    constructor (element) {
        this.element = element
        this.next = null
    }
}
class Stack {
    constructor() {
        this._top = null;
    }
    push(element) {
        let node = new Node(element);
        if (this._top == null) {
            this._top = node;
        } else {
            node.next = this._top;
            this._top = node;
        }
    }
    pop() {
        if (this._top == null) {
            return -1;
        }
        let element = this._top.element;
        this._top = this._top.next;
        element = null;
    }
    display() {
        let res = '';
        if (this._top != null) {
            let tmp = this._top;
            res = tmp.element;
            tmp = tmp.next;
            while (tmp != null) {
                res = tmp.element + '/' + res;
                tmp = tmp.next;
            }
        }
        return '/' + res;
    }
}
var simplifyPath = function(path) {
    let stack = new Stack();
    let pathArr = path.split('/');
    for (let eachStr of pathArr) {
        if (eachStr == '' || eachStr == '.') {
            continue;
        } else if (eachStr == '..') {
            stack.pop();
        } else {
            stack.push(eachStr);
        }
    }
    return stack.display();
}
```



##### 题外话

* [JavaScript 链式栈优点](https://blog.csdn.net/zhangxiangDavaid/article/details/28679027)
    * 一般, 链式栈与顺序栈相比, 优点是可以动态扩容.
        * 不过, JavaScript 数组长度是无限的, 只要内存允许. 即使设置了数组长度, 如果需要的话, 随后该长度也可以自动增长. 无需担心溢出.
            * 所以, 在 JavaScript 中, 链式栈的优点
                * 插入, 删除灵活
                * 物理地址不必相连

##### 程序参考

* [sctang0: 栈-程序模板](https://github.com/sctang0/LeetCode-Private/blob/master/CHAPTER71.1.md)
* [101刘辰: JavaScript 数组中长度最大是多少? 能设置吗?](https://zhidao.baidu.com/question/499788673)
* [苏叔叔: 栈的实现: 链式栈](https://blog.csdn.net/zhangxiangDavaid/article/details/28679027)
* [王争: StackBasedOnLinkedList.js](https://github.com/wangzheng0822/algo/blob/master/javascript/08_stack/StackBasedOnLinkedList.js)