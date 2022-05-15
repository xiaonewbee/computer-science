# [C++ 11的Lambda Expressions][https://blog.csdn.net/ruibin_cao/article/details/81428435?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165240460216781818722351%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165240460216781818722351&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-81428435-null-null.142^v9^control,157^v4^control&utm_term=Lambda+expressions+in+C%2B%2B&spm=1018.2226.3001.4187]

## 1

```
#include <iostream>
using namespace std;
 
int main()
{
	int a= 5, b = 5;
	auto func = [=](int h)-> int { return b*a*h; };
	cout << func(5) << endl;
	getchar();
	return 0;
}
```

这是一段简单的代码，可以看成是求边长为5的立方体的体积，输出结果是125。代码的逻辑很简单，但是第二句代码看似理解了，但是一一看懂还是有点困难的，这就是一句Lambda Expressions。根据第三行的使用来看，Lambda Expressions可以看成是一个函数。它的语法如下：

[capture](parameters) mutable ->return-type{statement};
[capture]：捕捉列表。捕捉列表总是出现在Lambda函数的开始处。实际上，[]是Lambda引出符。编译器根据该引出符判断接下来的代码是否是Lambda函数。捕捉列表能够捕捉上下文中的变量以供Lambda函数使用;
(parameters)：参数列表。与普通函数的参数列表一致。如果不需要参数传递，则可以连同括号“()”一起省略;
mutable：mutable修饰符。默认情况下，Lambda函数总是一个const函数，mutable可以取消其常量性。在使用该修饰符时，参数列表不可省略（即使参数为空）;
->return-type：返回类型。用追踪返回类型形式声明函数的返回类型。我们可以在不需要返回值的时候也可以连同符号”->”一起省略。此外，在返回类型明确的情况下，也可以省略该部分，让编译器对返回类型进行推导;
{statement}：函数体。内容与普通函数一样，不过除了可以使用参数之外，还可以使用所有捕获的变量。
与普通函数最大的区别是，除了可以使用参数以外，Lambda函数还可以通过捕获列表访问一些上下文中的数据。具体地，捕捉列表描述了上下文中哪些数据可以被Lambda使用，以及使用方式（以值传递的方式或引用传递的方式）。语法上，在“[]”包括起来的是捕捉列表，捕捉列表由多个捕捉项组成，并以逗号分隔。
————————————————
版权声明：本文为CSDN博主「阿喵不是猫」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/ruibin_cao/article/details/81428435

## 2

捕捉列表有以下几种形式：

主要就是捕捉

- ***\*参数列表和普通函数的参数列表类似，区别如下：\****
- **参数不能有默认值。**
- **不允许变长参数列表。**
- **不允许未命名的参数。**

*----

---

- **[=]：通过值捕捉所有变量**
- **[&]：通过引用捕捉所有变量**





涿州  钢研浩普

