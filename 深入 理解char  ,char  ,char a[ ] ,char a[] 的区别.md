# 深入 理解char * ,char ** ,char a[ ] ,char *a[] 的区别

C语言中**字符串常量**的本质表示其实是一个地址，这是许多初学者比较难理解的问题。。。



### **一、char \*a与char a[]的区别**

char *a = "hello" 中的a是指向第一个字符‘h'的一个指针；

char a[20] = "hello" 中数组名a也是执行数组第一个字符‘h’的指针。

> 但二者并**不相同，**看如下把两个字符串相加（strcat函数见附录）的实例：
>
> 把字符串加到指针所指的字串上去，出现段错误，本质原因：*d="0123456789"存放在常量区，是无法修改的。而数组是存放在栈中，是可以修改的。两者区别如下：

difference:

> 
>
> 1、读写能力
>
> char *a = "abcd"; //"abcd"存放在常量存储区，通过指针只可以访问字符串常量，而不可以改变它
>
> char a[20] = "abcd"; //"abcd"存放在栈，可以通过指针去访问和修改数组内容
>
> 2、赋值时刻
>
> char *a = "abcd"; //在编译时就确定了（因为是常量）
>
> char a[20] = "abcd"; //在运行时确定
>
> 3、存取效率
>
> char *a = "abcd"; //存于常量存储区，在栈上的数组比指针所指向字符串快，因此慢
>
> char a[20] = "abcd"; //存于栈上，因此快
>
> 4、另外注意：
>
> 1）char a[] = "01234",虽然没有指明字符串的长度，但是此时系统已经开辟好了，就是大小为6（'0' '1' '2' '3' '4' '5' '\0'）。
>
> 2）另外注意strlen(a)是不计‘\0’。
> ————————————————

[csdn_link](https://blog.csdn.net/liht_1634/article/details/124717461?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165511531316781435469941%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165511531316781435469941&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-124717461-null-null.142^v14^control,157^v14^new_3&utm_term=++char+a%5B%5D&spm=1018.2226.3001.4187)

​     **char \*s ;**

​     **s = "China";**

​     **为什么可以把一个字符串赋给一个指针变量。。**



​    **字符数组：**

​    **char str[10] = "hello"；**

​    **前面已经说了，str = &str[0] ， 也等于 "hello"的首地址。。**

​    **所以printf("%s",str); 本质也是 printf("%s", 地址");**



​    C语言中操作字符串是通过它在内存中的存储单元的首地址进行的，这是字符串的终极本质。。。

### 1. **char \* 与 char a[ ] 

​    **char \* 与 char a[ ] 的本质区别：**

​    **当定义 char a[10 ] 时，编译器会给数组分配十个单元，每个单元的数据类型为字符。。**

​    **而定义 char \*s 时， 这是个指针变量，只占四个字节，32位，用来保存一个地址。。**



---



**指针变量存放**的是右边每一个字符串常量的内存**首地址**，是指示器。右边则只是**字符串常量即字面上**“how r u ?"这些。**指针即地址**和**常量**有本质性的区别。

[csdn_link](https://blog.csdn.net/sober0314/article/details/104477425?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165511625116782391847928%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165511625116782391847928&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-104477425-null-null.142^v14^control,157^v14^new_3&utm_term=ISO+C%2B%2B+forbids+converting+a+string+constant+to+char*&spm=1018.2226.3001.4187)