# cc++中sizeof()、strlen()、length()、size()详解和区别

https://blog.csdn.net/z_qifa/article/details/77744482

sizeof(...)是运算符，其值在编译时即计算好了，参数可以是数组、指针、类型、对象、函数等。它的功能是：获得保证能容纳实现所建立的最大对象的字节大小。由于在编译时计算，因此sizeof不能用来**返回动态分配的内存空间**的大小。

strlen(...)是函数，该函数实际完成的功能是从代表该字符串的第一个地址开始遍历，直到遇到**结束符'\0**'。返回的长度大小不包括'\0'。



# 字符数组：

C语言允许用字符串的方式对数组作初始化赋值。例如：
  char c[]={'c', ' ','p','r','o','g','r','a','m'};
可写为：
  char c[]={"C program"};
或去掉{}写为：
  char c[]="C program";

用字符串方式赋值比用字符逐个赋值要多占一个字节， 用于存放字符串结束标志'\0'。上面的数组c在内存中的实际存放情况为：
![img](http://c.biancheng.net/cpp/uploads/allimg/120129/sfdsgfsge.gif)
‘\0'是由C编译系统自动加上的。由于采用了‘\0'标志，所以在用字符串赋初值时一般无须指定数组的长度， 而由系统自行处理。

# C 库函数 - strcpy()

[![C 标准库 - ](https://www.runoob.com/images/up.gif) C 标准库 - ](https://www.runoob.com/cprogramming/c-standard-library-string-h.html)

## 描述

C 库函数 **char \*strcpy(char \*dest, const char \*src)** 把 **src** 所指向的字符串复制到 **dest**。

需要注意的是如果目标数组 dest 不够大，而源字符串的长度又太长，可能会造成缓冲溢出的情况。

## 声明

下面是 strcpy() 函数的声明。

```
char *strcpy(char *dest, const char *src)
```

## 参数

- **dest** -- 指向用于存储复制内容的目标数组。
- **src** -- 要复制的字符串。

## 返回值

该函数返回一个指向最终的目标字符串 dest 的指针。

https://www.runoob.com/cprogramming/c-function-strcpy.html

# assert

assert是当括号里的内容为假时程序报错。

# 简洁的C语言字符串复制函数：

```
char *strcpy(char *strDest, const char *strSrc);
{
assert((strDest!=NULL) && (strSrc !=NULL));
char *address = strDest;
while( (*strDest++ = * strSrc++) != ‘\0’ )
NULL ;
return address ;
}
```

> assert是当括号里的内容为假时程序报错。
> 先*,后++,然后赋值,然后while里面的循环判断比较。
> 将*strSrc赋值给*strDest，然后判断是不是已经到达\0（即字符串结尾），同时，执行完赋值后strSrc和strDest指针均后移一位。总的结果即是：将strSrc指向的内容复制到strDest,直到strSrc指向\0.
> \0代表字符串的结束符。





# 代码阅读

```cpp
#include<iostream>
#include<cstring>


using namespace std;
class Person{
public:
    typedef enum {
        BOY = 0, 
        GIRL 
    }SexType;
    Person(char *n, int a,SexType s){
        name=new char[strlen(n)+1];
        strcpy(name,n);
        age=a;
        sex=s;
    }
    int get_age() const{
    
        return this->age; 
    }
    Person& add_age(int a){
        age+=a;
        return *this; 
    }
    ~Person(){
        delete [] name;
    }
private:
    char * name;
    int age;
    SexType sex;
};


int main(){
    Person p("zhangsan",20,Person::BOY); 
    cout<<p.get_age()<<endl;
	cout<<p.add_age(10).get_age()<<endl;
    return 0;
}
```

main函数里的` cout<<p.add_age(10).get_age()<<endl;`

能串一串，是因为add_age return 的是指针指向对象，