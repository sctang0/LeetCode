### 0.2 迭代器

* [迭代函数](https://github.com/wangzheng0822/algo/blob/master/javascript/05_array/Array.md): 通过对数组中的元素逐个应用, 来操作返回相应的值.
* 不返回新数组
    * [arr.forEach(callback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach): 按升序, 为数组中每一项执行一次函数 `callback` .
    * [arr.every(callback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every): 测试一个数组内的所有元素是否都能通过某个指定函数的测试. 它返回一个布尔值.
        * `true` . 每一项执行结果均为 `true` 或 `arr` 为空.
        * `false` . 存在元素, 执行结果为 `false` .
    * [arr.some(callback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some): 测试数组中是不是至少有 1 个元素通过了被提供的函数测试. 它返回一个布尔值.
        * `true` . 存在一项执行为 `true` , 返回 `true` .
        * `false` . 每一项执行均为 `false` 或 `arr` 为空.
    * [arr.reduce(callback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce): 对数组中的每个元素执行函数 `callback` ( 升序执行 ) 将其结果汇总为单个返回值.

```javascript
/**
 * arr.forEach(callback): 按升序, 为数组中每一项执行一次函数 callback
 */
var array = [ 'a', 'b', 'c' ];
array.forEach(element => console.log(element));
/**
 * std
      a
      b
      c
 */

function square(num) {
    console.log(num, num * num);
}
var num = [ 1, 2, 3 ];
num.forEach(square);
console.log(num);
/**
 * std
     1 1
     2 4
     3 9
 */
```



```javascript
/**
 * arr.every(callback): 测试一个数组内的所有元素是否都能通过某个指定函数的测试. 它返回一个布尔值.
 *   注: 若收到空数组, 此方法在任何情况下都会返回 true .
 */
function isEven(num){
  return num % 2 === 0;
}
var num = [ 2, 4, 6, 8, 10 ];
var even = num.every(isEven);
if(even){
  console.log("所有的数字都是偶数");
}else{
  console.log("不是所有的数字都是偶数");
}
/**
 * std
     所有的数字都是偶数
 */
```



```javascript
/**
 * arr.some(callback): 测试数组中是不是至少有 1 个元素通过了被提供的函数测试. 它返回一个布尔值.
 *   注: 若收到空数组, 此方法在任何情况下都会返回 false .
 */
function isEven(num){
  return num % 2 === 0;
}
var num = [ 1, 2, 3, 4, 5, 6, 7, 8 ];
var someEven = num.some(isEven);
if(someEven){
  console.log("有些数字是偶数");
}else{
  console.log("没有数字是偶数");
}
/**
 * std
     有些数字是偶数
 */
```



```javascript
/**
 * reduce(): 对数组中的每个元素执行函数 callback ( 升序执行 ) 将其结果汇总为单个返回值.
 */
function add(num1, num2){
  return num1 + num2;
}
var num = [ 1, 2, 3, 4 ];
var sum = num.reduce(add);
console.log(sum);

function concat(str, i) {
  return str + i;
}
var words = [ "I am ", "a ", "coder " ];
var re = words.reduce(concat);
console.log(re);
/**
 * std
     10
     I am a coder 
 */
```



* 返回新数组的
    * [arr.map(callback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map): 创建一个新数组, 其结果是该数组中的每个元素调用一次提供的函数 后的返回值.
    * [arr.filter(calllback)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter): 创建一个新数组, 其包含通过函数测试的所有元素.

```javascript
/**
 * arr.map(callback): 创建一个新数组, 其结果是该数组中的每个元素调用一次提供的函数后的返回值.
 */
function addFive(grade){
  return grade += 5;
}
var grade = [ 77, 82, 88, 95, 90 ];
var result = grade.map(addFive);
console.log(result);
/**
 * std
     [ 82, 87, 93, 100, 95 ]
 */

var array = [1, 4, 9];
var map = array.map(x => x * 2);
console.log(map);
/**
 * std
     [ 2, 8, 18 ]
 */
```



```javascript
/**
 * arr.filter(callback): 创建一个新数组, 其包含通过函数测试的所有元素.
 */
var words = [ "spray", "limit", "elite", "exuberant", "destruction", "present" ];
var result = words.filter(word => word.length > 6);
console.log(result);
/**
 * std
     [ 'exuberant', 'destruction', 'present' ]
 */

function passing(num){
    return num >= 60;
}
var grades = [];
for(var i = 0;i <= 10;i ++){
    grades[i] = Math.floor(Math.random() * 101);
}
var pass = grades.filter(passing);
console.log('随机产生的 10 个同学的分数为: ' + grades);
console.log('及格的分数有: ' + pass);
/**
 * std
     随机产生的 10 个同学的分数为: 30, 25, 77, 12, 74, 34, 41, 61, 57, 49, 92
     及格的分数有: 77, 74, 61, 92
 */
```



##### 思路, 程序参考

* [wangzheng0822: Array](https://github.com/wangzheng0822/algo/blob/master/javascript/05_array/Array.md)
* [MDN](https://developer.mozilla.org/zh-CN/)

* 注: 程序输出由 WebStorm 编译