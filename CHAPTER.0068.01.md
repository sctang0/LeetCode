### 递归算法模板

##### JavaScript

```javascript
var recursion = function (level, param1, param2, ...) {    // 一般会有一个层级, 表示递归到了第几层
    if (level > Max_Level) {
        return result;
    }
    // recursion terminator. 递归的终止条件(放在最前面, 清晰一点)


    process_data(level, param1, param2, ...);
    // process logic in current level. 数据处理 (程序逻辑, 业务逻辑)


    recursion(level + 1, param1, param2, ...)
    // drill down. 到下一层去, 你可能还有其它的业务要在下一层完成


    reverse_statel(level)
    // reverse the current level status if needed. 进行下一层操作之后, 会回到这里. 一些收尾的工作, 例如内存释放.
}
```



##### Python

```python
def recursion(level, param1, param2, ...):    # 一般会有一个层级, 表示递归到了第几层
    if level > Max_LEVEL:
      print_result
      result
    # recursion terminator. 递归的终止条件(放在最前面, 清晰一点)


    process_data(level, param1, param2, ...)
    # process logic in current level. 数据处理 (程序逻辑, 业务逻辑)


    self.recursion(level + 1, param1, param2, ...)
    # drill down. 到下一层去, 你可能还有其它的业务要在下一层完成


    reverse_statel(level)
    # reverse the current level status if needed. 进行下一层操作之后, 会回到这里. 可以做一些收尾的工作, 例如内存释放.
```



思路, 程序参考:

* [覃超: 递归 & 分治](https://time.geekbang.org/course/detail/100019701-42710)