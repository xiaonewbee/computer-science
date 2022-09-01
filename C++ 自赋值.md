# C++ 自赋值

https://harttle.land/2015/07/30/effective-cpp-11.html，这个讲的很不错！

自赋值一般存在：自赋值安全和异常安全，两个问题，例如:

**自赋值安全**：

当是自赋值的时候，p**b已经先被删除了**，那么后面的new就会为空，这是未知的计算。

new 拷贝构造后面 跟的 **空的**

```
Widget& Widget::operator=(const Widget& rhs){
    delete pb;                   // stop using current bitmap
    pb = new Bitmap(*rhs.pb);    // start using a copy of rhs's bitmap
    return *this;                // see Item 10
}
```

**异常安全**：

这个自赋值安全，但是没有异常安全，如果**new处出现了异常**，那么pb仍旧指向空。

**new异常**，在分配内存的时候如果失败我们可以使用bad_alloc类来完成他在new头文件中，

通过**调整语句顺序**：

```
Widget& Widget::operator=(const Widget& rhs){
    Bitmap *pOrig = pb;               // remember original pb
    pb = new Bitmap(*rhs.pb);         // make pb point to a copy of *pb
    delete pOrig;                     // delete the original pb
    return *this;
}
```

通过一个中间变量来实现，而没有使用if的判断，因为可能会影响效率。

**这样一来自赋值的判断也不需要了，当然如果你关心效率，也可以添加自赋值判断。** 



**总结一下**，赋值运算符的重载要注意自赋值安全和异常安全。有三种方法：

1. 判断两个地址是否相同
2. 仔细地排列语句顺序
3. Copy and Swap

