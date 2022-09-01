类类型，

不完全类型

定义指向不完全类型的指针。

友元 先声明 再指明友元 再定义

在类外定义成员函数时必须现在类内写出成员函数的原型声明，然后再在类外定义；

```
class Robot
{
public:
    void clean(){}
    void turnRight();
    void turnLeft();
    bool move();
    pos move(); // 错误，不能提前使用pos，得先typedef才能用
private:
    pos height = 0;
    typedef std::string::size_type pos;// 需要放到第9行前面，编译出错
};
```

```
typedef std::string Type;
class Robot
{
private:
    typedef std::string::size_type pos;
    typedef double Type;
    pos height = 0;
public:
    Type setValue(Type);形参类型是double，返回值类型是double
};

Type Robot::setValue(Type name){};
形参类型是double，返回值类型是string
需要修改 加作用域运算符强制指定函数的返回值类型
Robot::Type Robot::setValue(Type name){};


```
#### 构造函数初始值列表一些问题

```
class myClass{
public: // 叫做访问说明符
  int i;
  const int ci;
  int& ri;
};
myClass mc; 不对
```

https://blog.csdn.net/hou09tian/article/details/109594572

3.1 不能在构造函数的函数体来初始化常量或引用成员变量

```
myClass()
{
  i = 1;
  ci = 2;
  ri = i;
}
不对
```

3.2 在类的构造函数初始值列表来初始化常量或引用成员变量

```css
myClass():i(1),ci(2),ri(i)
{
}
对
```

如果一个构造函数为所有参数都提供了默认实参，则它实际上也定义了默认构造函数。

https://www.cnblogs.com/Braveliu/p/12232915.html

委托构造函数 环

确实有环， primer第五版 练习7.41 给出的代码 中就有三条链路

委托构造函数执行  受委托构造函数体中的所有代码。（先初始值列表，后函数体）

委托构造函数 再 执行   自己函数体中的所有代码。

**1.默认的继承访问权。class默认的是private,strcut默认的是public。**

stack，queue都是基于deque来实现的，priority-queue基于heap来实现，从技术上来说它们属于容器适配器（adapter）

java 字段 c++ 成员变量

方法  成员函数

forward_list

有 emplace_after

insert_after

erase_after

before_begin

begin

无序关联式容器，又称哈希容器。和关联式容器一样，此类容器存储的也是键值对元素；不同之处在于，关联式容器默认情况下会对存储的元素做升序排序，而无序关联式容器不会。

```
void test_whether_(){
    vector<int>v(10,1);
    vector<int> *old = &v; 这个后续pushback 不会变成野指针
    auto m = old->begin(); 这个后续pushback 会变成野指针了
    for (int i = 0; i<1;i++) {
        v.push_back(i);
    }
    cout<<(*(m));
    // cout<<((old->begin()));
    // cout<<*old;
}

```



### 5、类中的成员函数与inline

**定义**在类中的**成员函数**默认都是**内联的**，如果在类定义时就在类内给出函数定义，那当然最好。如果在类中未给出成员函数定义，而又想内联该函数的话，那在类外要加上 **inline**，否则就认为不是内联的。

C++要求对一般的内置函数要用关键字inline声明，但对类内定义的成员函数，可以省略inline，因为这些成员函数已经被隐含地指定为内置函数了。

##### new

**小结**

对于
const char * a=”string1”
char b[]=”string2”;

1.a是const char *类型， b是char* const类型
（ 或者理解为 (const char)*xx 和 char* (const xx) ）

2.a是一个指针变量，a的值（指向）是可以改变的，但a只能指向（字符串）常量，指向的区域的内容不可改变；

3.b是一个指针常量，b的值（指向）不能变；但b指向的目标（数组b在内存中的区域）的内容是可变的

4.作为函数的声明的参数的时候，char []是被当做char *来处理的！两种形参声明写法完全等效！





```
vector<int>ans;

ans.reserve(nums1.size());

ans.push_back(-1);
```

and --->       

​      

```
vector<int>ans(nums1.size());

否则前面都是0
不能用，得用下标了，否则[0,0,0,0,0,0,-1,-1,-1]
ans.push_back(-1);
```

