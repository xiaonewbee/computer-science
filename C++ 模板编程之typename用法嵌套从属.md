```
template<typename C>
void printAll(const C& container)
{
	//如果const_iterator为嵌套从属名称，需要添加typename关键字
	//C::const_iterator iter(container.begin());
	typename C::const_iterator iter(container.begin());
	for (; iter != container.end(); ++iter)
	{
		cout << *iter << " ";
	}
	cout << endl;
}
```

加不加typename有什么差别呢？

先来解释几个概念：

从属名称：template内出现的名称如果相依于某个template参数，称之为从属名称。

嵌套从属名称：嵌套从属名称是从属名称的子集，如果从属名称在class内呈嵌套状，我们称它为嵌套从属名称。还是有点绕口,在代码示例中，如果C是一个STL的容器类，那C::const_iterator既是从属名称，又是一个嵌套从属名称。实际上它是嵌套从属类型名称。

如上面所说，如果类型C是一个STL的容器类，那C::const_iterator无疑就是我们的迭代器类，但对于编译器来说，这是有歧义的，如果有某个自定义类恰巧也有一个叫做const_iterator的静态成员呢？我们写下这样的代码”C::const_iterator* x;“，是有歧义的，如果C::const_iterator是迭代器类，则" * "代表指针；但如果C::const_iterator是静态成员变量，" * "代表乘法。很有可能在编译器中不报错，为了消除歧义，编译器优先将C::const_iterator解释为一个静态成员变量，如果C::const_iterator是一个嵌套从属类型名称，我们就要在语句前面加上typename关键词以示区分。

在模板类中，如果继承的基类是某个依赖template参数的类的嵌套从属类型，在继承语法和构造函数列表中不必添加typename关键词，但在类中其他地方，包括构造函数函数体内就需要typename关键词，代码如下：

```
template<typename T>
class Derived:public Base<T>::Nested{//Base<T>::Nested前不要加typename
public:
    explicit Derived(int x):Base<T>::Nested(x)//Base<T>::Nested前不要加typename
    {
        typename Base<T>::Nested temp;//Base<T>::Nested要加typename
        ...
    }
}
```

[csdn_link](https://blog.csdn.net/qq_38755753/article/details/103284546?ops_request_misc=&request_id=&biz_id=102&utm_term=c++%E6%A8%A1%E6%9D%BF%E7%BB%A7%E6%89%BF%20typename&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-103284546.142^v20^rank_v33,157^v15^new_3&spm=1018.2226.3001.4187)

太难了





侯捷：

 