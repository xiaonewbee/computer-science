[临时对象不能被绑定到非const引用参数上====》扩展到临时对象问题](https://blog.csdn.net/liuxialong/article/details/6539717?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165526197616780357242486%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165526197616780357242486&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-6539717-null-null.142^v16^control,157^v14^new_3&utm_term=%E4%B8%B4%E6%97%B6%E5%AF%B9%E8%B1%A1%E4%B8%8D%E8%83%BD%E7%BB%91%E5%AE%9A%E5%88%B0%E9%9D%9Econst%E5%BC%95%E7%94%A8%E4%B8%8A&spm=1018.2226.3001.4187)

概括一下：

不能把临时对象作为实参传给非const引用。

例如：

 

void conv(string &str){}

 

int main()

{

    conv("dasd");//这里错了，编译器自动生成一个string(“dasd”)临时对象，不能将该临时对象传给非const引用

}

 

 

因此，需要将其改为

void conv(string str){} //值传递

或者

void conv(const string &str){}//const引用，因为标准规定临时对象是不能更改的，所以要加上const修饰

 

 

那么这里涉及到一个问题，什么时候会出现临时对象呢？？？？

临时对象的定义：

来看一个例子，在c++里，这个tmp是局部对象（变量），而不是临时对象

template <T>

void swap(T &obj1, T&obj2)

{

 obj tmp=obj1;//这里的tmp不能被称为临时对象，它只是局部对象

 obj1=obj2;

 obj2=tmp;

}

在C++中真正的临时对象是看不见的，它们不出现在你的源代码中。

建立一个没有命名的非堆（non-heap）对象会产生临时对象。

这种未命名的对象通常在两种条件下产生：为了使函数成功调用而进行隐式类型转换和函数返回对象时。

理解如何和为什么建立这些临时对象是很重要的，因为构造和释放它们的开销对于程序的性能来说有不可忽视的影响。

 

1、首先考虑为使函数成功调用而建立临时对象这种情况。

当传送给函数的对象类型与参数类型不匹配时会产生这种情况。

例如文章开头的那个例子，conv函数的参数是string，可是传入的实参却是“dasd”，因此，编译器会自动进行隐式转换，生成一个string（“dasd”）的临时对象，再把这个对象传入，这个没有命名的临时对象当然不能修改了，因此必须加上const修饰。

这就是文章一开头的那个问题产生的原因。

 

2、建立临时对象的第二种环境是函数返回对象时。

例如operator+必须返回一个对象，以表示它的两个操作数的和（参见Effective C++ 条款23）。

给定一个类型Number，这种类型的operator+被这样声明：

const Number operator+(const Number& lhs,

                       const Number& rhs);

这个函数的返回值是临时的，因为它没有被命名；它只是函数的返回值。

你必须为每次调用operator+构造和释放这个对象而付出代价。

 

关于临时对象的总结：

临时对象是有开销的，所以你应该尽可能地去除它们，然而更重要的是训练自己寻找可能建立临时对象的地方。

1、在任何时候只要见到常量引用（reference-to-const）参数，就存在建立临时对象而绑定在参数上的可能性。====》就是文章一开头的那个问题

2、在任何时候只要见到函数返回对象，就会有一个临时对象被建立（以后被释放）。

学会寻找这些对象构造，你就能显著地增强透过编译器表面动作而看到其背后开销的能力。

————————————————
版权声明：本文为CSDN博主「liuxialong」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/liuxialong/article/details/6539717