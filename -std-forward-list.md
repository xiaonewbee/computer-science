-std-forward-list

# 元素访问 element access

同样是出于简单高效的设计目标，`forward_list`只有一个直接访问元素的接口：`c.front()`.

c.front()返回第一个元素，这个接口内部并不会检查是不是存在第一个元素。如果调用了，但是元素不存在，那么导致未定义行为。

既然只有一个接口返回第一个元素，那么怎么来遍历所有元素呢？

有两种方式：

- iterators.
- range-based for loops. (其本质依然是使用iterators)



forward _list  :: assign 

是初始化差不多的东西，得先清除之前的list里所有值，然后把另一个拷贝过来