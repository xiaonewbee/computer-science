break 只跳出本层循环

c++没有直接跳出多层循环的语句，1.加判断标志，2. 使用goto

![img](https://www.runoob.com/wp-content/uploads/2014/09/c-continue-statement-works.jpg)

C++ 中的 **continue** 语句有点像 **break** 语句。但它不是强迫终止，continue 会跳过当前循环中的代码，强迫开始下一次循环。

对于 **for** 循环，**continue** 语句会导致执行条件测试和循环增量部分。对于 **while** 和 **do...while** 循环，**continue** 语句会导致程序控制回到条件测试上。