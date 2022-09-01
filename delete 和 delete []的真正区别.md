# delete 和 delete []的真正区别

1.我们通常从教科书上看到这样的说明：

delete 释放new分配的单个对象指针指向的内存

delete[] 释放new分配的对象数组指针指向的内存

那么，按照教科书的理解，我们看下下面的代码：

```cpp
int *a = new int[10];

delete a;        //方式1

delete [] a;     //方式2
```

肯定会有很多人说方式1肯定存在内存泄漏，是这样吗？



要分情况讨论：

(1).针对简单类型，使用new分配后的不管是数组还是非数组形式内存空间用两种方式均可 如：

```cpp
int *a = new int[10];
delete a;
delete [] a;
```

 此种情况中的释放效果相同，原因在于：分配简单类型内存时，内存大小已经确定，系 统可以记忆并且进行管理，在析构时，系统并不会调用析构函数，

它直接通过指针可以获取实际分配的内存空间，哪怕是一个数组内存空间(在分配过程中 系统会记录分配内存的大小等信息，此信息保存在结构体_CrtMemBlockHeader中.

(2).针对类Class，两种方式体现出具体差异 

 当你通过下列方式分配一个类对象数组：

```cpp
class A
   {
   private:
      char *m_cBuffer;
      int m_nLen;
   public:
      A(){ m_cBuffer = new char[m_nLen]; }
      ~A() { delete [] m_cBuffer; }
   };
   A *a = new A[10];
   delete a;    
```

delete a;    //仅释放了a指针指向的全部内存空间 但是只调用了a[0]对象的析构函数 剩下的从a[1]到a[9]这9个用户自行分配的m_cBuffer对应内存空间将不能释放 从而造成内存泄漏

   delete [] a;      //调用使用类对象的析构函数释放用户自己分配内存空间并且   释放了a指针指向的全部内存空间

   delete   ptr   代表用来释放内存，且只用来释放ptr指向的内存。 

   delete[]   rg   用来释放rg指向的内存，！！还逐一调用数组中每个对象的destructor！！

   对于像int/char/long/int*/struct等等简单数据类型，由于对象没有destructor，所以用delete 和delete [] 是一样的！但是如果是C++对象数组就不同了！







————————————————
版权声明：本文为CSDN博主「帅气滴点C」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/baidu_31437863/article/details/86558339