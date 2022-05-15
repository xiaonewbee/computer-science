# const 用法　

　（5） 可以节省空间，避免不必要的内存分配。 例如： 
　　#define PI 3.14159 //常量宏 
　　const double Pi=3.14159; //此时并未将Pi放入RAM中 ...... 
　　double i=Pi; //此时为Pi分配内存，以后不再分配！ 
　　double I=PI; //编译期间进行宏替换，分配内存 
　　double j=Pi; //没有内存分配 
　　double J=PI; //再进行宏替换，又一次分配内存！ 
　　const定义常量从汇编的角度来看，只是给出了对应的内存地址，而不是象#define一样给出的是立即数，所以，const定义的常量在程序运行过程中只有一份拷贝，而#define定义的常量在内存中有若干个拷贝。 
————————————————

## 4.定义常量

```cpp
const int b = 10;
b = 0; // error: assignment of read-only variable ‘b’
const string s = "helloworld";
const int i,j=0 // error: uninitialized const ‘i’
```

上述有两个错误：

- b 为常量，不可更改！
- i 为常量，必须进行初始化！(因为常量在定义后就不能被修改，所以定义时必须初始化。)



---------

## C++ 类构造函数初始化列表

**注意点：**

初始化列表的成员初始化顺序:

C++ 初始化类成员时，是按照声明的顺序初始化的，而不是按照出现在初始化列表中的顺序。

```cpp
class CMyClass {
    CMyClass(int x, int y);
    int m_x;
    int m_y;
};

CMyClass::CMyClass(int x, int y) : m_y(y), m_x(m_y)
{
};
```

你可能以为上面的代码将会首先做 m_y=I，然后做 m_x=m_y，最后它们有相同的值。但是编译器先初始化 m_x，然后是 m_y,，因为它们是按这样的顺序声明的。**结果是 m_x 将有一个不可预测的值。**有两种方法避免它，一个是总是按照你希望它们被初始化的顺序声明成员，第二个是，如果你决定使用初始化列表，总是按照它们声明的顺序罗列这些成员。这将有助于消除混淆。

https://www.runoob.com/w3cnote/cpp-construct-function-initial-list.html

```cpp
class CExample {
public:
    int a;
    float b;
    //构造函数初始化列表
    CExample(): a(0),b(8.8)
    {}
    //构造函数内部赋值
    CExample()
    {
        a=0;
        b=8.8;
    }
};
```

对于类中的const成员变量必须通过初始化列表进行初始化，如下所示：

```cpp
class Apple{
private:
    int people[100];
public:
    Apple(int i); 
    const int apple_number;
};

Apple::Apple(int i):apple_number(i)
{

}
```

### 例子一个：

const对象只能访问const成员函数,而非const对象可以访问任意的成员函数,包括const成员函数.

例如：

```cpp
//apple.cpp
class Apple
{
private:
    int people[100];
public:
    Apple(int i); 
    const int apple_number;
    void take(int num) const;
    int add();
    int add(int num) const;
    int getCount() const;

};
//main.cpp
#include<iostream>
#include"apple.cpp"
using namespace std;

Apple::Apple(int i):apple_number(i)
{

}
int Apple::add(){
    take(1);
    return 0;
}
int Apple::add(int num) const{
    take(num);
    return num;
}
void Apple::take(int num) const
{
    cout<<"take func "<<num<<endl;
}
int Apple::getCount() const
{
    take(1);
    add();  // error
    return apple_number;
}
int main(){
    Apple a(2);
    cout<<a.getCount()<<endl;
    a.add(10);
    return 0;
}
```

> 编译： g++ -o main main.cpp apple.cpp

此时报错，上面getCount()方法中调用了一个add方法，而add方法并非const修饰，所以运行报错。也就是说const成员函数只能访问const成员函数。

```
const Apple b(3);
b.add(); // error
```

https://github.com/Light-City/CPlusPlusThings/tree/master/basic_content/const