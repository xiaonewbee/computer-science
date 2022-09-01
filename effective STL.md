contiguous memory container

node-based container

reference counting 

transactional semantics 事务语义

rope非标准

exception safe 异常安全



## 1

用 typedef 来定义容器 

` class Widget{...} `

` typedef vector<Widget> WidgeContainer `

` typedef WidgeContainer::iterator WCIterator `

当然把上两行也可以放进` private ` 里，隐藏起来





# 4.调用empty而不是检查size==0

 发表于 2018-04-06 | 分类于 [Effective STL](https://zsmj2017.tech/categories/Effective-STL/)


理论上而言，这二者等价，但是优先使用empty的理由很简单：
**对于所有标准容器，empty都是常数时间操作，而某些list的size耗费线性时间。**

list独有的splice操作导致了这种情况，举例而言：

```
list<int> list1;
list<int> list2;
...
//将list2中从第一次出现5到第二次出现10的所有节点移动到list1的末尾
list1.splice(list1.end(), list2, 
find(list2.begin(), list2.end(), 5), 
find(list2.rbegin(),list2.rend(), 10).base());
```



这段程序只有在list2中在含5的节点之后含有10的节点时才工作。
关键在于list1中有多少个元素？应该是list1之前的元素加上之后链接过来的元素.除非遍历一次，不然编译器不会知道具体个数。
list的设计者主要希望它在插入删除操作中具有较好性能，如果list的size希望有常数时间，那么splice必须遍历自身然后更新size，这样造成了splice具有线性时间。不管怎么说，list总要在size或者splice之间做出取舍。
但是，empty必然是常数时间，那我们为啥不用呢？

# 5.区间成员函数优于与之对应的单元素成员函数

对于插入，不要忘了很多函数其实做着与insert一样的事情，当你看到反复的push_back或者push_infront时，不妨提供给他们区间形式的insert版本。

# 花括号初始化

花括号初始化的另外一个值得一谈的特性是它能避免C++最令人恼火的解析。一方面，C++的规则中，所有能被解释为声明的东西肯定会被解释为声明，最令人恼火的解析常常折磨开发者，当开发者想用默认构造函数构造一个对象时，他常常会不小心声明了一个函数。问题的根本就是你想使用一个参数调用一个构造函数，你能这么做：

```scss
Widget w1(10);	//使用参数10调用Widget的构造函数
```

但是如果你使用类似的语法，尝试使用0个参数调用Widget的构造函数，你会声明一个函数，而不是一个对象：

```csharp
Widget w2();	//最令人恼火的解析！声明一个
				//名字是w2返回Widget的函数
```

函数不能使用花括号作为参数列表来声明，所以使用花括号调用默认构造函数构造一个对象不会有这样的问题：

```fsharp
Widget w3{};	//不带参数调用Widget的默认构造函数
```

因此这里对于花括号初始化有很多可以说的。这种语法能用在最宽广的范围，它能阻止隐式收缩转换（narrowing convertions），并且它能避免C++最让人恼火的解析。三个优点！但是为什么这个条款的标题不是”优先使用花括号初始化语法“呢？

# 7.在析构前记得delete容器内通过new得到的指针

上述代码改写为for_each:

```
for_each(vwp.begin(),vwp.end(),[](Widget* pw){delete pw;});
```

使用shared_ptr可以避免异常安全的问题，我们通过将原容器替换为包含智能指针的容器之后，一切都变得美好了起来。

# 8.切勿创建包含auto_ptr的容器对象

typename挺有讲究，强调了后面是一个类型

auto_ptr的值放到了一个局部临时中，随着临时对象生命周期结束，对象也被析构了，真是倒了血霉。

# emplace 与 push

  **相当于emplace直接把原料拿进家，造了一个。而push是造好了之后，再复制到自己家里，多了复制这一步。**

  **所以emplace相对于push，使用第三种方法会更节省内存。**



erase 关联容器对数时间

选择删除元素：

连续容器 ` erase remove `

 ` remove if`

