总归，对于protected函数，只能造子类内部和本类内部调用，[private](https://so.csdn.net/so/search?q=private&spm=1001.2101.3001.7020)函数，只能在本类内部中调用。这些都是c++最基础的知识，这里只是顺带提一下。

那么将构造函数/析构函数声明为protected或者private?可以通过以下使用场景来看：
1) 作为类设计者的你，不希望你定义的类(cla)可以生成对象，而是要让调用者定子类subCla来继承cla后，子类可以生成对象。那么就要将cla的构造/析构函数声明为protected，子类subCla的构造/析构函数为public：
————————————————
版权声明：本文为CSDN博主「mybright_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_29344757/article/details/74757441

**整型（bool、char、int、short、long等**

static constexpr数据成员必须在类内声明和初始化。在类内声明和初始化时，static constexpr数据成员是真正的const。

只读   常量区

至于为什么char型数据成员也可以，我想着应该与char的实现机制有关，char型可以转换成int型，毕竟我们知道字符可以以int型输出其ASSIC码值。

static const int a=1;

;并不分配内存，编译时直接将a换成1，放到常量表中

![Snipaste_2022-08-13_11-15-48](D:\路径不动的文件\图片\Snipaste_2022-08-13_11-15-48.png)