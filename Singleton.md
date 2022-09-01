如果new一个对象在堆上

实例的析构函数什么时候执行？



我们想程序一开始执行这个实例就存在，



放到全局区，static

系统会接管全局区的分配与释放



多进程 多线程 CPU大后先问题



**懒汉式单例模式：**

优点：延迟加载

缺点：不加同步的懒汉式是线程不安全的，加了synchronized之后就变成线程安全的了

   饱汉模式多线程时不安全，需要使用饿汉模式，在程序跑起来前就生成单例对象

**饿汉式**  优点：线程安全. *缺点*：浪费内存空间

[ *lazy* vs eager initialisation?](https://stackoverflow.com/questions/34506466/singleton-with-or-without-holder-lazy-vs-eager-initialisation)

如一个类允许最多五个实例。设计出来



拷贝构造函数也要设置为private



类CGarbo被定义为CSingleton的私有内嵌类，以防该类被在其他地方滥用。

程序运行结束时，系统会调用CSingleton的**静态成员**Garbo的析构函数，该析构函数会删除单例的唯一实例。

利用程序在结束时析构全局变量的特性，选择最终的释放时机；