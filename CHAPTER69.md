### [69. x 的平方根-二分查找, 牛顿法](https://leetcode-cn.com/problems/sqrtx/)

##### 题目描述

* 实现 int sqrt(int x) 函数。

    * 计算并返回 x 的平方根，其中 x 是非负整数。
    * 由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

* 示例:

    * ```example
        输入: 4
        输出: 2
        ```

    * ```example
        输入: 8
        输出: 2
        说明: 8 的平方根是 2.82842..., 
             由于返回类型是整数，小数部分将被舍去。
        ```



##### 思路一: 二分查找

* 设定查找的边界, 根据查找范围中间值的平方相较于 `x` 的大小, 将边界不断收缩到原来的 1 / 2 .

* 定义 `left` `right` 为结果的左右边界, 初值为 1, `x` . `mid = Math.floor((left + right) / 2)` .
    * 若 `mid * mid > x`
        * 平方根在 `mid` 右侧
        * 缩小范围 `left = mid; mid = Math.floor((left + right) / 2);`
    * 若 `mid * mid <= x`
        * 平方根在 `mid` 左侧, 或等于 `mid` .
        * 缩小范围 `right = mid; mid = Math.floor((left + right) / 2);`
            * 没有单独列出一种情况 `mid * mid == x` . 是因为, 出现 `mid * mid == x` 为 `true` 的概率不大. 若为此在循环中, 多加入一行判断语句, 会有点得不偿失.
    * 若 `x` 没有平方根. 即, 当 `right - left <= 1` 时, 输出 `left` .

* 递归的程序实现

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    if (x == 0 || x == 1) {
        return 0;
    }
    var find = function (level, left, right, x) {
        if (right - left <= 1) {
            return left;
        }
        mid = Math.floor((left + right) / 2);
        if (mid * mid > x) {
            right = mid;
        } else {
            left = mid;
        }
        return find(level + 1, left, right, x);
    }
    return find(0, 1, x, x);
};
```

* while 循环的程序实现

```javascript
/**
 * @param {number} x
 * @return {return}
 */
var mySqrt = function (x) {
    if (x == 0 || x == 1) {
        return x;
    }
    let left = 1;
    let right = x;
    while (right - left > 1) {
        let mid = Math.floor((right + left) / 2);
        if (mid * mid > x) {
            right = mid;
        } else {
            left = mid;
        }
    }
    return left;
}
```

##### 复杂度分析:

* 时间复杂度: O(logn), `n = x`. 查找过程中, 查找范围不断减半.
* 空间复杂度: O(1)

 

##### 方法二: 牛顿法

* 下面这张动图是等式 <img src = "https://github.com/sctang0/LeetCode/blob/master/images/chapter69.1.svg" width = "10%"> 的收敛图. 可以看到牛顿法的收敛过程.

<div align = center>
    <img src = "https://github.com/sctang0/LeetCode/blob/master/images/chapter69.2.gif" alt = "author: Ralf Pfeifer href: https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95#/media/File:NewtonIteration_Ani.gif" width = "70%">
</div>




```javascript
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function (x) {
    if (x == 0 || x == 1) {
        return x;
    }
    var mid = x;
    var sqrt = function (x) {
        var sqrtX = (x + mid / x) / 2;
        if (sqrtX == x) {
            return parseInt(x);
        } else {
            return sqrt(sqrtX);
        }
    }
    return sqrt(x);
}
```

##### 复杂度分析

* 时间复杂度: O(F(n)logn), `F(n) = f(n) / f'(n) = mid / x` . [牛顿法](https://en.citizendium.org/wiki/Newton's_method#Computational_complexity)每次迭代后的精度都为前一次的两倍.
* 空间复杂度: O(1)



##### 题外话

* [牛顿法](https://en.citizendium.org/wiki/Newton's_method#Computational_complexity): 一个解决函数值为零的方法, 换一句话说解决方程 ![img](https://github.com/sctang0/LeetCode/blob/master/images/chapter69.3.png) .



##### 程序, 思路参考

* [秦时明月: 69. x 的平方根](https://leetcode-cn.com/problems/sqrtx/solution/69-x-de-ping-fang-gen-by-alexer-660/)
* [牛顿法复杂度分析](https://en.citizendium.org/wiki/Newton's_method#Computational_complexity)

##### 图片来源

* 第一个公式: [维基百科: 牛顿法](https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95)

* 动图来源: [Ralf Pfeifer](https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95#/media/File:NewtonIteration_Ani.gif)
* 第二个公式: [Citizendium: Newton's Method](https://en.citizendium.org/wiki/Newton's_method#Computational_complexity)

