## STL主要板块

1. STL概论与实现版本简介
2. 空间配置器 allocator
3. 迭代器 iterators 与 traits 编程技法
4. 序列式容器 sequence container
5. 关联式容器 associated containers
6. 算法 algorithms
7. 仿函数或函数对象 functors or function objects
8. 配接器 adapter



在C语言里面，数组之后的一个地址是固定的，但不允许被使用

STL vector 适合 push_back pop_back ,但都建议单口容器加，删，哦1 复杂度。

---

#### sizeof vector

指针就是迭代器（说反了

` vector <int> v1(arr, arr + sizeof(arr)/sizeof(int))`

`   vector<int>v1(arr, arr+sizeof(arr));`

上面两个不一样 second 8x4=32

`   int arr[] = {0, 1, 2, 3, 4, 55, 6, 7};`

` sizeof()`

---



[csdn_linkc++中vector＜int＞ a[] sizeof无效的问题](https://blog.csdn.net/K2939631189/article/details/124323047?spm=1035.2023.3001.6557&utm_medium=distribute.pc_relevant_bbs_down_v2.none-task-blog-2~default~OPENSEARCH~Rate-1-124323047-bbs-392278309.pc_relevant_bbs_down_v2_opensearchbbsnew&depth_1-utm_source=distribute.pc_relevant_bbs_down_v2.none-task-blog-2~default~OPENSEARCH~Rate-1-124323047-bbs-392278309.pc_relevant_bbs_down_v2_opensearchbbsnew)

 我们可以看到随着a中元素的增多，nums长度改变，sizeof(nums)不变以及sizeof(nums)/sizeof(nums[0])不变。



---

#### vector 

[vector all operator](https://blog.csdn.net/qq_63211065/article/details/123607844?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165526376016780366592553%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165526376016780366592553&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-123607844-null-null.142^v16^control,157^v14^new_3&utm_term=c%2B%2B%2B%E5%88%9B%E5%BB%BA%E5%8C%BF%E5%90%8Dvector%2B%E5%AF%B9%E8%B1%A1&spm=1018.2226.3001.4187)



---

### list	

list 不支持随机访问，所以算法的 sort 不适用于 list。 



---

### deque

号称连续存储



### 泛型编程

generic programing

` using namespace std      using std::cout ` 

这两个写法，前者适合小项目，后者适用于一般工程

predicate : 解释为 这是一个判断式，传回真或假。



### set

set中 key = value

multiset 不要求独一无二，可以重复

红黑树实现



unordered

hashtable

sparate chaining 

允许哈希碰撞，但是不能碰撞太多次，因为碰撞多了，一个bucket挂了太多链，查找速度会变得特别慢，所以会打散链。



标准库容器之间，尽量避免继承，估计用命名空间



**PDF X-Change Editor shortcus**

|        Name         | Shortcuts |
| :-----------------: | :-------: |
|      Oval Tool      |  alt + o  |
|      line tool      |  alt + l  |
|   highlight text    |  alt + h  |
|     pencil tool     |  alt + p  |
|   Rectangle Tool    |  alt + r  |
| Underline Text Tool |  alt + u  |
|   Typewriter Tool   |  alt + t  |

#### 容器的分类

序列式容器都是可序，不一定有序。


|   序列式容器   |  关联式容器   |
| :------------: | :-----------: |
|     array      |      set      |
|     vector     |      map      |
|      heap      |   multiset    |
| priority_queue |   multimap    |
|      list      |   hashtable   |
|     deque      | unordered_set |
| queue(配接器)  | unordered_map |
| stack(配接器)  |               |
|                |               |



#### 迭代器分类

根据移动特性和实行操作，迭代器可以分为5类

 

1. Input iterator:不允许外界改变。只读(read only) ,只能单步向前迭代
2. Output iterator:不允许读，只写(write only)，只能单步向前迭代
3. Forward iterator: 可读可写，允许在该迭代器所指区间上进行读取和写入操作，单步向前迭代operator++
4. Bidirectional Iterator：可双向移动，允许在该迭代器所指区间上进行读取和写入操作operator++，operator--
5. Random Access Iterator：可读可写，同时支持像指针一样的操作，包括 p+n,p-n等

---

cd

迭代器就像一个指针，故迭代器最重要实现工作的就是要对 [operator](https://so.csdn.net/so/search?q=operator&spm=1001.2101.3001.7020)* 和 operator-> 重载。
