## hashtable 的数据结构

hashtable 的模板参数比较多，包括：

Value：节点的实值型别
Key：节点的键值型别
HashFcn：hash function 的函数型别
ExtractKey：从节点中取出键值的方法（函数或仿函数）
EqualKey：判断键值相同与否的方法
Alloc：空间配置器



rehash 会从hash素数表中找临近大于

### 查找

可以看到，这是典型的 hash 操作的写法

1. 先对 key 算出 hash code
2. 找到这个 hash code 对应的桶
3. 在这个桶里面，遍历去找这个 key 对应的节点
4. 把节点返回



- 结论2：undered_map与undered_multimap采用的迭代器是iterator，而undered_set与undered_multiset采用的迭代器是const_iterator。

- 结论3：undered_map与undered_multimap的key是key，value是key+value；而undered_set与undered_multiset的key是Value，Value也是Key。

https://cloud.tencent.com/developer/article/1530885



![img](https://img2018.cnblogs.com/blog/1183871/201811/1183871-20181120153735807-1531529767.jpg)