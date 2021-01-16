### 0.1 测试程序执行时长

```javascript
console.time('one');
let i = '1';
console.log(i);
console.timeEnd('one');

console.time('two');
let j = '2';
console.log(j);
console.timeEnd('two');

console.time('three');
let k = '3';
console.log(k);
console.timeEnd('three');

/**
 * std:
 *   1
 *   one: 15.477ms
 *   2
 *   two: 0.12ms
 *   3
 *   three: 0.105ms
 *   
 * 注: 由 WebStrom 编译
 */
```



##### 语法

* [console.time(timerName)](https://developer.mozilla.org/zh-CN/docs/Web/API/Console/time)
    * `timerName`: 新计时器的名字, 用来标记这个计时器.
* [console.timeEnd(laber)](https://developer.mozilla.org/zh-CN/docs/Web/API/Console/timeEnd)
    * `laber`: 需要停止的计时器名字.
    * 注: 该特性是非标准的, 请尽量不要在生产环境中使用它.



##### 参考

* [« JavaScript 语法简明手册»](https://www.dedao.cn/eBook/lxaVvndNG6D4kgLJ2OKxqVMmE1zXPwV9Pd3AdjyQeYR75vbaBnr9ol8pZERLg1my)
* [时代的眼泪a: 测试程序执行时长: console.time() 和 console.timeEnd()](https://blog.csdn.net/weixin_45844049/article/details/104511166)