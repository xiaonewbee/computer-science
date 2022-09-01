https://blog.51cto.com/u_14289397/2540190

实例：

> 

```c++
/** malloc/free用例 **/
int*ma = (int*)malloc(4)；
free(ma)；
/** new/delete用例 **/
int*ne =newint(0);
```



# [c++内存管理](https://www.361shipin.com/blog/1547763696753704960)

- 全局/静态存储区：内存在程序编译的时候已经分配好，这块内存在程序的整个运⾏期间都存在。例如全局变量，static静态全局变量。 程序结束后由系统释放。
- 常量存储区：存放常量、字符串、静态局部变量，程序结束后有系统释放。





        malloc/free是C/C++的标准库函数，new/delete是C++运算符。
    
        对于非内部类的对象而言，光用malloc/free无法满足动态对象的要求，对象在创建的同时要自动执行构造函数，对象消亡之前要自动执行析构函数，由于malloc/free是库函数，不在编译器控制权限之内，不能把构造函数和析构函数的任务强加malloc/free。
————————————————
版权声明：本文为CSDN博主「danieldingyi」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/danieldingyi/article/details/79944190

        1、new自动计算需要分配的空间，而malloc需要手工计算字节数
        2、new是类型安全的，而malloc不是，比如：
                 int* p = new float[2]; // 编译时指出错误
                 int* p = malloc(2*sizeof(float)); // 编译时无法指出错误
          new operator 由两步构成，分别是 operator new 和 construct
        3、operator new对应于malloc，但operator new可以重载，可以自定义内存分配策略，甚至不做内存分配，甚至分配到非内存设备上。而malloc无能为力
        4、new将调用constructor，而malloc不能；delete将调用destructor，而free不能。
        5、malloc/free要库文件支持，new/delete则不要。         
