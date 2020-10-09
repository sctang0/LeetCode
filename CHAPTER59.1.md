### 59.1 else 移除后为何会报错呢?



```javascript
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let res = new Array();
    for (let i = 0; i < n; i++) {   
        res[i] = new Array();
        for (let j = 0; j < n; j++) {
            res[i][j] = 0;
        }
    }
    let i = 0;
    let j = 0;
    let boundL = 0;
    let boundR = n - 1;
    let boundU = 0;
    let boundD = n - 1;
    let turn = 'r';

    for (let a = 1; a <= n * n; a++) {
        res[i][j] = a;
        if (turn == 'r') {
            j++;
            if (j == boundR) {
                turn = 'd';
                boundU++;
            }
        }
        if (turn == 'd') {
            i++;
            if (i == boundD) {
                turn = 'l';
                boundR--;
            }
        }
        if (turn == 'l') {
            j--;
            if (j == boundL) {
                turn = 'u';
                boundD--;
            }
        }
        if (turn == 'u') {
            i--;
            if (i == boundU) {
                turn = 'r';
                boundL++;
            }
        }
    }
    return res;
};

/**
 * 报错信息(LeetCode 控制台):
    Line 22 in solution.js
            res[i][j] = a;
                      ^
    TypeError: Cannot set property '1' of undefined
        Line 22: Char 19 in solution.js (generateMatrix)
        Line 81: Char 19 in solution.js (Object.<anonymous>)
        Line 16: Char 8 in runner.js (Object.runner)
        Line 72: Char 26 in solution.js (Object.<anonymous>)
        Line 1251: Char 30 in loader.js (Module._compile)
        Line 1272: Char 10 in loader.js (Object.Module._extensions..js)
        Line 1100: Char 32 in loader.js (Module.load)
        Line 962: Char 14 in loader.js (Function.Module._load)
        at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:72:12)
        Line 17: Char 47 in run_main_module.js   
 */
```



##### 原因: `if ... else ...` 的判断执行

* ```javascript
    if (判断 A) {
        B;
    } else {
        C;
    }
    ```

    * 判断 A 成立时, B 执行, C 不执行.

* ```javascript
    if (判断 A) {
        B;
    }
    if (判断 D) {
        C;
    }
    ```

    * 判断 A 成立时, B 执行, 且 B 的执行, 可能会影响判断 D .

    * 具体

        * ```javascript
            for (let a = 1; a <= n * n; a++) {
                res[i][j] = a;
                if (turn == 'r') {    // 判断(1)
                    j++;
                    if (j == boundR) {
                        turn = 'd';
                        boundU++;
                    }
                }
                if (turn == 'd') {    // 判断(2)
                    i++;
                    if (i == boundD) {
                        turn = 'l';
                        boundR--;
                    }
                }
            }
            ```

            * 当 `j == boundR` 判断正确时, `turn = 'd'` . 
            * 此时, 顺序执行判断(2). 判断(2)正确, 执行其包含语句.
            * 于是 `i`, `j` 多加 / 减了几次, 并在执行 `res[i][j] = a;` 时, 超出了数组 `res` 的定义范围.
            * 报错.



##### 修正

```javascript
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let res = new Array();
    for (let i = 0; i < n; i++) {   
        res[i] = new Array();
        for (let j = 0; j < n; j++) {
            res[i][j] = 0;
        }
    }
    let i = 0;
    let j = 0;
    let boundL = 0;
    let boundR = n - 1;
    let boundU = 0;
    let boundD = n - 1;
    let turn = 'r';

    for (let a = 1; a <= n * n; a++) {
        res[i][j] = a;
        if (turn == 'r') {
            j++;
            if (j == boundR) {
                turn = 'd';
                boundU++;
                continue;
            }
        }
        if (turn == 'd') {
            i++;
            if (i == boundD) {
                turn = 'l';
                boundR--;
                continue;
            }
        }
        if (turn == 'l') {
            j--;
            if (j == boundL) {
                turn = 'u';
                boundD--;
                continue;
            }
        }
        if (turn == 'u') {
            i--;
            if (i == boundU) {
                turn = 'r';
                boundL++;
                continue;
            }
        }
    }
    return res;
};
/**
 * 输入: 3
 * 输出: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]
 * 预期结果: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]
 * 提交: 成功
 */
```

##### 题外话

* [continue](https://www.w3school.com.cn/js/js_break.asp): “跳过”循环中的一个迭代, 然后继续循环中的下一个迭代.
    * `continue` 的作用是, 防止 if() 判断正确后对 `turn` 值的更改, 影响循环中之后的 `turn == 'd'; turn == 'l'; turn == 'u';` 的判断.