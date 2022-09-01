





## STL主要板块

1. STL概论与实现版本简介
2. 空间配置器 allocator
3. 迭代器 iterators 与 traits 编程技法
4. 序列式容器 sequence container
5. 关联式容器 associated containers
6. 算法 algorithms
7. 仿函数或函数对象 functors or function objects
8. 配接器 adapter



operator new()  and malloc
operator delete() and free

1. allocator
2. deallocate



VC6 STL 

vector list deque keyword= class_A = allocator

what is the most important of the allocator : two: 1. allocator 2.deallocate

1. allocator 2.deallocate made by ::operator new and ::operator delete

overhead things proportion too big if malloc too small memory.

temporary/ anonymous object :::---> allocator <int> () 

VC6 allocator need remember how much space you request, because need deallocate the same space you request ,precise to figures, not just deallocate the pointer , but also the precise figures allocated.

overhead : extra cost

![Snipaste_2022-06-15_15-36-13](D:\路径不动的文件\图片\Snipaste_2022-06-15_15-36-13.png)![Snipaste_2022-06-15_15-35-59](D:\路径不动的文件\图片\Snipaste_2022-06-15_15-35-59.png)

malloc always bring with extra cost , which is cookie in the head and tail to record the whole memory of this time allocate, 
the key is to reduce the number of malloc times





### vector

![Snipaste_2022-06-15_17-01-09](D:\路径不动的文件\图片\Snipaste_2022-06-15_17-01-09.png)

![Snipaste_2022-06-15_17-01-27](D:\路径不动的文件\图片\Snipaste_2022-06-15_17-01-27.png)

这三个指针一个指针32位电脑 4个字节，所以sizeof（vector) 12 字节占用内存

我的电脑64位，` sizeof(int *) 占用8字节大小`   

所以一个 ` vector占用24位字节大小，three pointers 1. start, 2. finish , 3. end_of_storage`

上图： finish指针指向第7个块的地址，容器是前闭后开，





#### 类别推导

在处理指针与常量指针的时候，利用模板偏特化来执行特化的版本。从而达到类别推导的效果

#### count，find，sort算法

对于set map 有自己自身的count，find不用标准库提供的count，比较慢

但是没有sort，他们不支持sort，或者本身带有sort



如果他作为父类，有人继承他了，那他的大小就是0



是一个对象，但像一个函数

适配器：做桥梁，中间层

实现：做幕后	



binder 修饰容器表现为容器

修饰函数，表现为函数



创建对象 还是函数调用，小括号



### istream

```cpp
std::istream_iterator<double> eos; 				// 标志迭代器,通过与该迭代其比较以判断输入流是否终止
std::istream_iterator<double> iit(std::cin); 	// 封装std::cin的输入流迭代器

double value;
if (iit != eos) 
    value = *iit;		// 从输入流读取数据到变量value中,相当于: std::cin >> cvalue


```

istream_iterator重载了运算符=,*和++,其源码如下:

```cpp
template<class T, class charT=char, class traits=char_traits<charT>, class Distance=ptrdiff_t>
class istream_iterator :
        public iterator<input_iterator_tag, T, Distance, const T *, const T &> {
    basic_istream<charT, traits> *in_stream;	// 输入流
    T value;									// 上一次读入的值
public:
    typedef charT char_type;
    typedef traits traits_type;
    typedef basic_istream<charT, traits> istream_type;

    istream_iterator() : in_stream(0) {}							// 空迭代器,表示输入流终止
    istream_iterator(istream_type &s) : in_stream(&s) { ++*this; }	//**** 创建好迭代器后马上读入一个值 *****
    istream iterator(const istream_iterator<T, charT, traits, Distance> &x)
            : in_stream(x.in_stream), value(x.value) {}

    // 重载运算符++
    istream_iterator<T, charT, traits, Distance> &operator++() {
    //等待输入
        if (in_stream && !(*in_stream >> value)) 
            in_stream = 0;
        return *this;
    }
	istream_iterator<T, charT, traits, Distance> operator++(int) {
        istream_iterator<T, charT, traits, Distance> tmp = *this;
        ++*this;
        return tmp;
    }
    
	// 重载运算符*和->
    const T &operator*() const { return value; }
    const T *operator->() const { return &value; }
};


```

```
//当你创建一个对象iit时，已经在读了
istream_iterator<int> iit(cin), eos;//eos作为标定：
copy(iit, eos, inserter(c, c.begin()));

```



---

## difference_type

[difference_type使用来表示两个[迭代器](https://so.csdn.net/so/search?q=迭代器&spm=1001.2101.3001.7020)之间的距离的。]

[csdn link](https://blog.csdn.net/qq_27396861/article/details/92665849?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165672346716782246443749%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165672346716782246443749&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-92665849-null-null.142^v30^control,185^v2^control&utm_term=difference_type&spm=1018.2226.3001.4187)



random_access_iterator：
1.std::array 由于数组是连续空间，可以根据头指针偏移量来直接寻址
2.std::vector 动态数组容器由于是连续空间，类似数组，所以也可以根据头指针偏移量来直接寻址
3.std::deque 双向队列的内部实现其实是通过多个连续空间拼接而成的，所以也可以直接寻址
————————————————

**bidirectional_iterator**
1.**std::list** 列表的内部实现是双向链表，不是连续空间，因此只能使用指针逐一迭代间接寻址
2.**std::set/std::multiset** 集合的内部实现是红黑树，红黑树是低度平衡二叉搜索树，红黑树的节点结构如下

```
struct __rb_tree_node_base
{
	typedef __rb_tree_color_type color_type;
	typedef __rb_tree_node_base* base_ptr;
	color_type color;
	base_ptr parent;
	base_ptr left;
	base_ptr right;
}

```

每个节点保存了父节点和左右子节点的指针，所以可以通过指针逐一间接寻址
3.**std::map//std::multimap** 表的内部实现也是红黑树，理由同上



forward_iterator
1.std::unordered_set/std::unordered_multiset 无序集合（哈希集合）的内部实现是hashtable，hashtable是通过连续空间下的buckets（**通常用vector实现**）来散列存储元素，虽然是连续空间，但是实际上**unordered容器的实**现，每个bucket（node）的结构是这样的

```
template <class Value>
struct __hashtable_node
{
	__hashtable_node* next;
	Value val;
}
```

val是bucket中的元素，next用于指向下一个node。这样设计的原因是解决hash冲突，这样**冲突的元素会放在这样的一条单向链表中**，所以实际上每一个bucket中的元素只能从前往后迭代，无法向前迭代
2.std::unordered_map/std::unordered_multimap 无序表（哈希表）的内部实现也是hashtable，同理
3.std::forward_list 单向列表的内部实现为单向链表，只支持单向迭代

` std:: vector<int>str1 :: iterator it`

` it.clear() `

不用的迭代器要clear掉，防止迭代器时效



导致vector容器迭代器失效的原因

1。 push_back insert

2. erase , pop_back, clear 
3. resize 变大的话，全部失效，变小的话被切掉的迭代器失效
4. deque失效：中间删除，全部失效，首尾删除，首尾失效
5. ![img](https://img-blog.csdn.net/20140514212336515?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXVzaGl5YW9nZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

deque 唯一一个迭代器失效但是指针和引用不一定失效的容器
