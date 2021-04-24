### 0.4 系统设计的响应时间列表

| 行为                                                         | 时间消耗 (单位 : 纳秒) |
| ------------------------------------------------------------ | ---------------------- |
| L1 cache reference (读取 CPU 的一级缓存)                     | 0.5 ns                 |
| Branch mispredict (分支预测)                                 | 5 ns                   |
| L2 cache reference (读取 CPU 的二级缓存)                     | 7 ns                   |
| Mutex lock/unlock (互斥锁/解锁)                              | 100 ns                 |
| Main memory reference (读取内存数据)                         | 100 ns                 |
| Compress 1K bytes with Zippy (1K 字节压缩)                   | 10,000 ns              |
| Send 2K bytes over 1 Gbps network (在 1Gbps 网络发送 2K 字节) | 20,000 ns              |
| Read 1 MB sequentially from memory (从内存顺序读取 1MB )     | 250,000 ns             |
| Round trip within same datacenter (同一个数据中心内的往返)   | 500,000 ns             |
| Disk seek (磁盘搜索)                                         | 10,000,000 ns          |
| Read 1 MB sequentially from network (从网络顺序读取 1 MB)    | 10,000,000 ns          |
| Read 1 MB sequentially from disk (从磁盘读取 1 MB)           | 30,000,000 ns          |
| Send packet CA->Netherlands->CA (一个包的一次远程访问)       | 150,000,000 ns         |

<div align = center>
    <img src = "https://github.com/sctang0/DataStructure-LeetCode/blob/main/images/00/00.007.png" alt = "img">
</div>

参考:

[1] [《“前途丛书”这就是软件工程师》](https://book.douban.com/subject/35313199/)

[2] [数据来源: 杰夫 . 迪恩](http://highscalability.com/numbers-everyone-should-know;jsessionid=CC5E05170099E7315CA1F0BF920FFB00.v5-web013)