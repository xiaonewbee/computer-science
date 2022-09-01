然后你要对自己的tinySTL定位，除了[陈硕](https://www.zhihu.com/search?q=陈硕&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A133370355})提到的内容外，还有

- 要不要用自己的 functional（函数对象）？
- 迭代器要不要写 insert iterator？[iostream iterator](https://www.zhihu.com/search?q=iostream+iterator&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A133370355}) ？
- 算法较为复杂的除了 next_permutation ，prev_permutation 还有 rotate，inplace_merge，sort 等（不自己实现实现一遍 sort 的话就没啥意义了）？
- 算法要不要实现重载版本？
- 容器实现哪些？要不要实现 set，map（意味着你要实现 rb tree），要不要实现 unorder_set，unorder_map（意味着你要实现 hashtable）？
- 容器的接口要实现到什么程度？是实现基本插入删除，还是完善它？
- 要不要增加自己的容器（AVL tree，string等）？



作者：Alinshans
链接：https://www.zhihu.com/question/53085291/answer/133370355
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。





STL

vector

![img](http://c.biancheng.net/uploads/allimg/191212/2-191212123P2Q5.gif)

图 1 vector实现原理示意图

其中，_Myfirst 指向的是 vector 容器对象的起始字节位置；_Mylast 指向当前最后一个元素的末尾字节；_myend 指向整个 vector 容器所占用内存空间的末尾字节。

- _Myfirst 和 _Mylast 可以用来表示 vector 容器中目前已被使用的内存空间；
- _Mylast 和 _Myend 可以用来表示 vector 容器目前空闲的内存空间；
- _Myfirst 和 _Myend 可以用表示 vector 容器的容量。
- 】

##### resize  reserve 练习 

```c++
	std::vector<int> vec2{1,2,3,4};
	vec2.push_back(1);
	

	cout<< vec2.size()<<endl;
	cout<< vec2.capacity()<<endl;


	vec2.resize(100);
	// vec2.reserve(100);

	cout<< vec2.size()<<endl;
	cout<< vec2.capacity()<<endl;

	for (int a : vec2) {
		cout<< a <<' ';
	}
```

##### []和at()

[]和at()的区别在于[]不检查索引是否有效,而at()在遇到无效索引时会抛出**out_of_range**异常.

[ ](https://blog.csdn.net/yxccc_914/article/details/54846003)

访问字符串中的字符

可以使用[]或者at()方法来访问字符串中的字符,起始索引是0.最大有效索引是string.length()-1.(特别的,如果是**const string**类型的对象,那么最大有效索引是string.length(),最后一个字符是'\0’.)

[]和at()的区别在于[]不检查索引是否有效,而at()在遇到无效索引时会抛出**out_of_range**异常.

  1
  2

上面输出是0.容器初始化什么都不做,大小为0;

  std::vector<int> a;
//  std::cout<<a.size();
  a[0]=1;
  a.at(0)=1;

  1
  2
  3
  4

下标[]赋值会显示SIGSEGV段错误,越界错误.
at赋值会显示 terminate called after throwing an instance of ‘std::out_of_range’

  c++标准不要求vector::operator[]进行下标越界检查，原因是为了效率，总是强制下标越界检查会增加程序的性能开销。

所以通常使用vector两种方法:
(1)知道vector的大小,初始化时就设立大小.也就是知道下标操作肯定是没有越界的.
(2)用push_back比较安全.