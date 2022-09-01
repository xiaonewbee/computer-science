左值一般指长期存在的值，右值一般指**即将释放的值**(n匿名对象）或是常量

**rvalues** are values whose address cannot be obtained by dereferencing them, 

[目前看不懂](https://www.cnblogs.com/ishen/p/13771991.html)

## [左值和右值](https://blog.csdn.net/AAA123524457/article/details/104060533?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166020697616782390556102%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166020697616782390556102&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-104060533-null-null.142^v40^pc_rank_v36,185^v2^control&utm_term=c%2B%2B%20%26%26&spm=1018.2226.3001.4187)

左值的英文简写为“lvalue”，右值的英文简写为“rvalue”。很多人认为它们分别是"left value"、"right value" 的缩写，其实不然。lvalue 是“**loactor value**”的缩写，可意为存储在内存中、有明确存储地址（可寻址）的数据，而 rvalue 译为 **"read value**"，指的是那些可以提供数据值的数据（不一定可以寻址，例如存储于寄存器中的数据）。
————————————————
![img](https://img-blog.csdnimg.cn/20200121115918418.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FBQTEyMzUyNDQ1Nw==,size_16,color_FFFFFF,t_70)



![Snipaste_2022-08-11_17-21-14](D:\路径不动的文件\图片\Snipaste_2022-08-11_17-21-14.png)

![Snipaste_2022-08-11_17-23-41](D:\路径不动的文件\图片\Snipaste_2022-08-11_17-23-41.png)

#if 0

`                内容`       

 #endif

则内容会被忽视掉



可用于重载函数测试



右值用const &就行了 不用这么麻烦



> `   const char* what() const throw() {   return this->msWhat.c_str();    } `
>   前面的const表示string()返回的char*不能作为一个左值来使用。
> 例如：string() ＝ ptrChar 是不可以的,其中，ptrChar是另外一个char指针。
>
> 后面的const表示在函数调用过程中，对传入的参数不会做任何改变。一般用在对象的成员函数中，对外表明自己是一个安全的函数。







## 更新

`int &&ref = std::move(a)`和 `int a = 5`没有什么区别，等号左边就是左值，右边就是右值。

从表达式`int &&ref = std::move(a)`来看，右值引用`ref`指向的必须是右值，所以move返回的`int &&`是个右值。所以右值引用既可能是左值，又可能是右值吗？ 确实如此：**右值引用既可以是左值也可以是右值，如果有名称则为左值，否则是右值**。





LHS（Left-Hand-Side）

RHS(Right-Hand-Side)

LHS和RHS的含义是“赋值操作的左侧和右侧”，并不一定意味着“=”赋值操作符的左侧或者右侧。

LHS：赋值操作的目标

RHS：赋值操作的源头