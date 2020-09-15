##### [backTrack(tmpPath.slice()) 为什么这里要用 arr.slice() ？](https://leetcode-cn.com/problems/permutations/solution/46-quan-xu-lie-by-shu-cheng/579219)

##### 思路

*  `res.push(tmpPath)` 与 `res.push(tmpPath.slice())` 有何区别？
    * 这里 tmpPath 是一个栈结构，最终是 [] 。前者直接将 tmpPath 直接 push 进去，最终结果中的每一个元素都指向同一个栈，所以都是 [] 。后者其实是当前 tmpPath 的一个浅拷贝，最终结果的每一个元素都指向 tmpPath 不同状态的拷贝。



##### 相关函数简谈

* [arr.slice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)：返回一个**新的数组对象**，原始数组不会被改变。
  * 在该题中，`tmpPath.slice()` 返回一个包含数组 tmpPath 所有元素新的数组对象。



##### 题外话

* [栈结构](https://juejin.im/post/6844904129605828615)：一个递归函数，在函数执行过程中，需要多次进行自我调用，在高级语言程序中，调用函数和被调用函数之间的链接与信息交换都是通过栈来进行。
  * 为了保证递归函数的正确执行，系统就要建立一层一层的的工作栈，每层工作栈保留了所有的实参，局部变量，以及上一层的返回地址，形成工作记录压入栈顶，就形成了递归工作栈。
  * 举例：
    * <img src="https://user-gold-cdn.xitu.io/2020/4/16/1718361ee0e4e060?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="递归工作栈: 程序" style="zoom:50%;" />
    * <img src="https://user-gold-cdn.xitu.io/2020/4/16/171836205787161b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="递归工作栈: 图片表示" style="zoom:50%;" />
* [浅拷贝](https://juejin.im/post/6844904197595332622)：浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。
  * 深拷贝：将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。
  * ![浅拷贝](https://user-gold-cdn.xitu.io/2020/3/1/170965259fb768fd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
  * ![深拷贝](https://user-gold-cdn.xitu.io/2020/3/1/1709652a7948d1b8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



##### 思路参考

* [null 题末回答：46. 全排列](https://leetcode-cn.com/problems/permutations/solution/jspython-hui-su-tao-lu-mo-ban-ti-46-quan-pai-lie-b/367065)
  * 注：上面思路中的逻辑、语言 90% 是照搬过来的。不过，自己并没有把原内容上下文也描述出来，所以吧，还是建议去看一下原作者内容。
* [浪里行舟：深拷贝、浅拷贝](https://juejin.im/post/6844904197595332622)

##### 图片来源

* [浪里行舟：深拷贝、浅拷贝](https://juejin.im/post/6844904197595332622)



##### 程序

* 使用控制台输出 console.log() 。看一下，不使用 arr.slice() 情况下的输出情况。



```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    let n = nums.length;
    let res = [];
    let tmpPath = [];
    let backTrack = (tmpPath) => {
        if (tmpPath.length == n) {
            res.push(tmpPath);
            console.log(res);
            return;
        }
        for (let i=0; i<n; i++) {
            if (!tmpPath.includes(nums[i])) {
                tmpPath.push(nums[i]);
                backTrack(tmpPath);
                tmpPath.pop();
            }
        }
    }
    backTrack(tmpPath);
    return res;
}
/**
 * 输入: [ 1, 2, 3 ]
 * 输出: [ [], [], [], [], [], [] ]
 * 预期结果: [ [ 1, 2, 3 ], [ 1, 3, 2 ], [ 2, 1, 3 ], [ 2, 3, 1 ], [ 3, 1, 2 ], [ 3, 2, 1 ] ]
 * stdout:
     [ [ 1, 2, 3 ] ]
     [ [ 1, 3, 2 ], [ 1, 3, 2 ] ]
     [ [ 2, 1, 3 ], [ 2, 1, 3 ], [ 2, 1, 3 ] ]
     [ [ 2, 3, 1 ], [ 2, 3, 1 ], [ 2, 3, 1 ], [ 2, 3, 1 ] ]
     [ [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ], [ 3, 1, 2 ] ]
     [
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ],
       [ 3, 2, 1 ]
     ]
 */
```