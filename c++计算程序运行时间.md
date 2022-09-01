# 关于C++中计算时间的一些总结

## 方法一：clock()计时函数

简单而言，就是该程序从启动到函数调用占用CPU的时间。这个函数返回从“开启这个程序进程”到“程序中调用clock()函数”时之间的CPU时钟计时单元（clock tick）数，在MSDN中称之为挂钟时间（wal-clock）；若挂钟时间不可取，则返回-1。其中clock_t是用来保存时间的数据类型。

linux 和 windows 都能用

` CLOCKS_PER_SEC` 意思是标准c的time.h头函数中宏定义的一个常数，表示一秒钟内CPU运行的时钟周期数，用于将clock()函数的结果转化为以秒为单位的量，但是这个量的具体值是与操作系统相关的。
绝大多数情况下都是1000！你电脑输出的都是毫秒数！只有少部分情况在linux下是1000000，输出出来是微秒数。
————————————————

` CLK_TCK`意思 一样

```
/* 
 * Number of clock ticks per second. A clock tick is the unit by which
 * processor time is measured and is returned by 'clock'.
 */
#define    CLOCKS_PER_SEC  ((clock_t)1000)
#define    CLK_TCK     CLOCKS_PER_SEC
```

## 方法二：GetTickCount()函数：

GetTickCount是函数。GetTickCount返回（retrieve）从操作系统启动所经过（elapsed）的毫秒数，它的返回值是DWORD。

注意事项：
GetTickcount函数：它返回从操作系统启动到当前所经过的毫秒数，常常用来判断某个方法执行的时间，其函数原型是DWORD GetTickCount(void)，返回值以32位的双字类型DWORD存储，因此可以存储的最大值是(2^32-1) ms约为49.71天，因此若系统运行时间超过49.71天时，这个数就会归0，MSDN中也明确的提到了:"Retrieves the number of milliseconds that have elapsed since the system was started, up to 49.7 days."。因此，如果是编写服务器端程序，此处一定要万分注意，避免引起意外的状况。
特别注意：这个函数并非实时发送，而是由系统每18ms发送一次，因此其最小精度为18ms。当需要有小于18ms的精度计算时，应使用StopWatch方法进行。
用clock()函数计算运行时间，表示范围一定大于GetTickCount()函数，所以，建议使用clock()函数。

————————————————
接下来是两种高精度的计时方法：**gettimeofday() 和 QueryPerformanceCounter()**

前者是windows  ，后者是linux

可以以微妙为单位计时







```c++
#include <iostream>
#include <chrono>
#include <unistd.h>
 
using namespace std;
 
// 测量 C++ 程序运行时间的主函数
// 使用 Chrono 库
int main()
{
    auto start = chrono::steady_clock::now();
 
    // 在这里做一些事情
    sleep(3);
 
    auto end = chrono::steady_clock::now();
 
    cout << "Elapsed time in nanoseconds: "
        << chrono::duration_cast<chrono::nanoseconds>(end - start).count()
        << " ns" << endl;
 
    cout << "Elapsed time in microseconds: "
        << chrono::duration_cast<chrono::microseconds>(end - start).count()
        << " µs" << endl;
 
    cout << "Elapsed time in milliseconds: "
        << chrono::duration_cast<chrono::milliseconds>(end - start).count()
        << " ms" << endl;
 
    cout << "Elapsed time in seconds: "
        << chrono::duration_cast<chrono::seconds>(end - start).count()
        << " sec";
 
    return 0;
}

```

https://www.techiedelight.com/zh/measure-elapsed-time-program-chrono-library/

从 C++11 开始，在 C++ 中测量经过时间的最佳方法是使用 [计时库](http://www.cplusplus.com/reference/chrono/)，它处理时间。

以下 C++ 程序以秒、毫秒、微秒和纳秒为单位计算简单代码所用的时间。它包括 `<chrono.h>` 标头提供对当前时间的访问 `system_clock()`.这 `system_clock` 旨在表示实时并由系统上运行的所有进程使用。

读作 可如no