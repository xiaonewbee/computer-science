## 1.两者与map及set的关系

`map和set`底层是红黑树，近似平衡搜索树。C++98支持。

`unordered_map`和`unordered_set`底层是哈希，哈希表/散列表。C++11支持。

前者有正向和反向迭代器。后者没有反向迭代器。





find first of 

find

前者只调用一次，找到所有第一次

```c++
  int needle1[] = {40,50,60,70};
```