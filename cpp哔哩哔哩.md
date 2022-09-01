| Ctrl shift U                                                 |      |      |
| ------------------------------------------------------------ | ---- | ---- |
| #pragma once                                                 |      |      |
| #ifndef                                                      |      |      |
| #define                                                      |      |      |
| #endif                                                       |      |      |
| a.cpp在编译的时候，发现一个函数调用，在当前                  |      |      |
| 文件找不到，函数位置生成符号（让链接器去找函数定义声明的地方。） |      |      |
| 二次编译，模板编译了，调用的时候生成具体函数。               |      |      |
| 函数模板先进行一次编译，根据使用生成具体的函数               |      |      |
| 声明不编译                                                   |      |      |
| hpp文件 ，头文件和模板的合体                                 |      |      |
| 让别人一目了然，声明和实现都在一个文件，类模板都写到hpp文件里 |      |      |
|                                                              |      |      |
|                                                              |      |      |
|                                                              |      |      |
|                                                              |      |      |

## 类模板碰到static成员

类模板碰到static成员， 每个static成员属于自己的实例类里，每个实例类自己有各自的static成员，不互通，不共享。

但是` typename <class T> `

```
比如说Person<int>p1, p2, p3;
and  Person<char>pp1, pp2, pp3;

result:p1 = p2 = p3 ;
		pp1 = pp2 = pp3;
		p1 != pp1;

sumary: 这里我试了，是同一类模板共享一个static成员，不同的肯定不共享啦
```



## 类模板去派生类模板

` 自动类型推导适用于函数模板，不适于类模板`，类模板得显示指示类型。

派生的时候，得显示指定类型（普通的类去**派生**（类内调用类模板）类模板的时候）（如果类不确定，编译器不知道分配多少内存，类去定义对象的时候，

```
1. 普通的类去派生类模板 -->得显示指定类型
class SubPerson:public Person<int>{};

2. 类模板去派生类模板 -->不用显示指定类型
template<class T>
class Cat : public Animal<T>{};
```

== 二次编译 ==

## 函数模板的实现

1. 编译
2. [bilibili链接][https://www.bilibili.com/video/BV1PW411t7Xg?p=16&spm_id_from=pageDriver&vd_source=74774e96c765e0483877879b1a4b186e]

### 类模板类外实现

类模板实现在类的外部的话，如果用友元的话，就会出现一些问题。` friend void PrintPerson<T>(Person<T>&p);`

### 友元不要使用，不同编译器处理方式不同。

### 类模板h与cpp分离编写

，报错原因的是因为二次编译







```cpp
using namespace std;
template <class T>
class MyArray{
	//
	// 
public:
	MyArray(int capacity)
	{
		this->mCapacity = capacity;
		this->mSize = 0;
		// 申请内存
		this->pAddr = new T[this->mCapacity]；
	};
	
	// copy constructor
	MyArray(const MyArray<T>& arr){
		for(int i = 0;i< this->mSize;i++){
			this->pAddr[i] = arr[i];
		}
	};
	
	T& operator[](int index){
		return this->pAddr[index];
	};
	// overloading
	MyArray<T> operator=(const MyArray<T>& arr){
		if (this->)
		return *this;
		// return this 返回的是地址
		// return *this 返回的是对象
		// return *this 可以采用链式编程  a = b = c
	}
	void PushBack(T& data){
		// 
		if(this->mSize >= this->mCapacity){
			return;
		}
		
		this -> pAddr[this->mSize] = data;
		this -> mSize++;
		
	}
public:
	int mCapacity;
	int mSize;
	//save first address
	T* pAddr;
}










```


值拷贝问题都会引发深浅拷贝的问题：
1. 属性创建在堆区，会产生堆区数据重复释放， 浅拷贝问题，需要深拷贝去解决