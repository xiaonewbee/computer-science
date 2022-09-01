```
#include <iostream>
#include <typeinfo>
using namespace std;
int main()
{
	int a;
	decltype(a) b = 0;
	cout<<"a的类型是"<<typeid(a).name()<<endl;
	cout<<"b的类型是"<<typeid(b).name()<<endl;
	
	float c;

	double d;
	decltype(c + d ) e;
	cout<<"e的类型是"<<typeid(e).name()<<endl;

	return 0;
}


```

输出：

```
a的类型是i  //i代表int
b的类型是i  
e的类型是d   //d代表double

```

### 2.

[csdn_link  decltype的用法及作用意义](https://blog.csdn.net/qq_44705488/article/details/121283384?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165521113016781683983965%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165521113016781683983965&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-121283384-null-null.142^v14^control,157^v14^new_3&utm_term=c%2B%2B+print+decltype&spm=1018.2226.3001.4187)

目录
二、decltype类型推导
2.1、 decltype
decltype和auto的异同：
2.2、decltype的应用
①、decltype和typedf/using合用
②、deltype在某些场景下使用增加代码的可读性
③、使用decltype重用匿名类型
④、decltype可以适当扩大模板泛型的能力
2.3、decltype推导规则
①、表达式为普通变量或者普通表达式或者类表达式，在这种情况下，使用 decltype 推导出的类型和表达式的类型是一致的。
②、表达式是函数调用，使用 decltype 推导出的类型和函数返回值一致。
③、表达式是一个左值，或者被括号 ( ) 包围，使用 decltype 推导出的是表达式类型的引用（如果有 const、volatile 限定符不能忽略）。
2.4、cv限制符的继承与冗余的符号
①、与auto类型推导时不能“带走”cv限制符不同是：
与auto相同的是：
————————————————目录

- ---



---





### 1.【C++】C++中获得类型名称

[【C++】C++中获得类型名称](https://blog.csdn.net/wangqingchuan92/article/details/119380895?ops_request_misc=&request_id=&biz_id=102&utm_term=c++%20St6vector&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-119380895.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187)

### 文章目录

- [0x00 前言](https://blog.csdn.net/wangqingchuan92/article/details/119380895?ops_request_misc=&request_id=&biz_id=102&utm_term=c++ St6vector&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-119380895.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187#0x00__2)
- [0x02 C++中获得类型名称](https://blog.csdn.net/wangqingchuan92/article/details/119380895?ops_request_misc=&request_id=&biz_id=102&utm_term=c++ St6vector&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-119380895.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187#0x02_C_8)
- - - [1.typeid().name()](https://blog.csdn.net/wangqingchuan92/article/details/119380895?ops_request_misc=&request_id=&biz_id=102&utm_term=c++ St6vector&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-119380895.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187#1typeidname_9)
    - [2.__cxa_demangle](https://blog.csdn.net/wangqingchuan92/article/details/119380895?ops_request_misc=&request_id=&biz_id=102&utm_term=c++ St6vector&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-119380895.142^v14^control,157^v14^new_3&spm=1018.2226.3001.4187#2__cxa_demangle_107)
- 

