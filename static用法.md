当变量声明为static时，空间**将在程序的生命周期内分配**。即使多次调用该函数，静态变量的空间也**只分配一次**，前一次调用中的变量值通过下一次函数调用传递。这对于在C / C ++或需要存储先前函数状态的任何其他应用程序非常有用。

```
#include <iostream> 
#include <string> 
using namespace std; 

void demo() 
{ 
	// static variable 
	static int count = 0; 
	cout << count << " "; 
	
	// value is updated and 
	// will be carried to next 
	// function calls 
	count++; 
} 

int main() 
{ 
	for (int i=0; i<5; i++)	 
		demo(); 
	return 0; 
} 
```

输出：

```
0 1 2 3 4 
```

您可以在上面的程序中看到变量count被声明为static。因此，它的值通过函数调用来传递。每次调用函数时，**<u>都不会对变量计数进行初始化。</u>**

