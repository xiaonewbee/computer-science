# 访问容器元素时下标操作与at函数的区别（C++）

对于C++的STL内的顺序容器，可以使用下标或at函数对容器内的元素进行访问，如：

```
//假设存在一个容器vector<int> v，现在要访问其第i个成员，下面两种方式是等价的
v[i]
v.at(i)

```

二者的区别在于，如果下标越界（[编译器](https://so.csdn.net/so/search?q=编译器&spm=1001.2101.3001.7020)并不检查这种错误），**在运行时at函数会抛出一个out_of_range的异常，而下标操作不进行任何输出或直接运行奔溃：**

```
void test1()
{
    vector<int> v; //定义一个空容器
    cout << v[0] << endl; //运行错误，容器内无任何元素，无法访问
}

```

```
void test2()
{
    vector<int> v; //定义一个空容器
    cout << v.at(0) << endl; //无法访问，抛出异常
}

//这段代码的运行结果：
terminate called after throwing an instance of 'std::out_of_range'
  what():  vector::_M_range_check: __n (which is 0) >= this->size() (which is 0)

```

[csdn_link](https://blog.csdn.net/Ivan_47/article/details/116233905?ops_request_misc=&request_id=&biz_id=102&utm_term=c++%20%E4%B8%8B%E6%A0%87%E8%AE%BF%E9%97%AE%EF%BC%8C%E4%B8%8Eat&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-116233905.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187)