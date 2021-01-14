### [Time Complexity for Javascript Methods in V8](https://stackoverflow.com/questions/15622248/time-complexity-for-javascript-methods-in-v8)

* Ask by: [*Chris Redford*](https://stackoverflow.com/users/130427/chris-redford)

I know that the Javascript standard does not specify required time complexities for methods like array `unshift` but is there a reference for time complexities in a specific Javascript engine like V8?



* Answer by: [*Gsamaras*](https://stackoverflow.com/users/2411320/gsamaras)

> is there a reference for time complexities in a specific Javascript engine like V8?

*No*.

The ECMA specification does not specify a bounding complexity, as you already might know, and nor does that engine. Every JavaScript engine is free to implement its own functionality, as long as it is compatible with the Standard.

V8, for example, does not provide Time Complexities for its methods.

You could of course look at the source code, construct the algorithm used under the hood in our mind, understand it, analyse it and then come up with a bound for its Time Complexity.



* 提问: [*Chris Redford*](https://stackoverflow.com/users/130427/chris-redford)

我知道 Javascript 标准并未为数组 `unshift` 之类的方法指定所需的时间复杂性. 但是, 在诸如 V8 之类的特定 Javascript 引擎中, 是否有时间复杂性的参考？



* 回答: [*Gsamaras*](https://stackoverflow.com/users/2411320/gsamaras)

> V8 这样的特定 Javascript 引擎中, 是否有时间复杂性参考？

*没有*.

您可能已经知道, ECMA 规范并未指定边界复杂性, 该引擎也未指定. 只要与标准兼容, 每个 JavaScript 引擎都可以自由实现其自身的功能.

例如, V8 不为其方法提供时间复杂性.

您当然可以查看源代码, 构造我们脑海中使用的算法, 了解它, 对其进行分析, 然后为其时间复杂度提出一个界限.



##### 思想, 翻译来源

* [Stack Overflow: Time Complexity for Javascript Methods in V8](https://stackoverflow.com/questions/15622248/time-complexity-for-javascript-methods-in-v8)
* [Google 翻译](https://translate.google.com/?sl=auto&tl=zh-CN&op=translate)