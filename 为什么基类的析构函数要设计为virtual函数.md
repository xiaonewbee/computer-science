## 为什么基类的析构函数要设计为virtual函数

https://blog.csdn.net/u013517637/article/details/51829169





现在pD和pB调用的就是各自的mf了。造成这种行为的是，non-virtual函数如B::mf和D::mf都是静态绑定的。这句话的意思是，由于pB被声明为一个pointer-to-B，通过pB调用的non-virtual函数永远是B所定义的版本，即使pB指向一个类型为“B类派生的class”对象。
但是另一方面，virtual函数却是动态绑定的，所以他们不存在这个问题。如果mf是一个virtual函数，不论是通过pB还是pD调用mf。都会导致调用D::mf，因为pB和pD真正指向的都是一个类型为D的对象。



如果你正在编写class D并重新定义继承自class B的non-virtual函数mf，D对象很可能展现出精神分裂的不一致行径。更明确的说，**当mf被调用，任何一个D对象都可能表现出B或D的行为。决定因素不在对象自身，而在于 “指向该对象的指针类型”。**References也会展现和指针一样难以理解的行径。



这也就解释了，为什么基类的析构函数要设计为virtual函数！

```
// ConsoleApplication2.cpp : 定义控制台应用程序的入口点。
//
 
#include "stdafx.h"
 
 
class B
{
public:
	void mf();
};
 
class D : public B
{
public:
	void mf();
};
 
 
int main()
{
 
	D x;
 
	B* pB = &x;
	pB->mf();
 
	D* pD = &x;
	pD->mf();
 
    return 0;
}
```

