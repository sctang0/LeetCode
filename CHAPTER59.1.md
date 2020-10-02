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



##### 思路参考

* [JavaScript - cannot set property of underfined](https://stackoverflow.com/questions/7479520/javascript-cannot-set-property-of-undefined)
* [Uncaught TypeError: Cannot set property '0' of undefined](https://stackoverflow.com/questions/10673237/uncaught-typeerror-cannot-set-property-0-of-undefined)
* [Javascript cannot set property 0 of undefined](https://stackoverflow.com/questions/44540391/javascript-cannot-set-property-0-of-undefined)
