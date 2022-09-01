`字面值类型`：算术类型、引用和指针都属于字面值类型，自定义类、IO库，string类型则不属于字面值类型，不能被定义成constexpr；

const和constexpr区别
对于修饰对象来说，const并未区分出编译期常量和运行期常量，constexpr限定在了编译期常量
在constexpr声明中如果定义了一个指针，限定符constexpr仅对指针有效，与指针所指的对象无关。

```
const int*p1=nullptr;  			//p1是一个指向常量的指针
constexpr int*p2=nullptr;		//p2是一个指向整数的常量指针
constexpr const int*p3=nullptr; //p3是一个指向常量的常量指针
```





若static const数据成员不是整型（bool、char、int、short、long等），则**不能在类内初始化。**

static const int a=1;并不分配内存，编译时直接将a换成1，放到常量表中，当然，若对a取地址，则在只读的常量区分配内存。所以，这和类声明不分配内存并不矛盾。至于为什么char型数据成员也可以，我想着应该与char的实现机制有关，char型可以转换成int型，毕竟我们知道字符可以以int型输出其ASSIC码值






## constexpr函数的形参可以是非常量，但是实参必须是常量

```cpp
总结：
```

static constexpr数据成员必须在**类内声明和初始化**。在类内声明和初始化时，static constexpr数据成员是真正的const。
若编译时static constexpr数据成员可用它的值替代（如表示数组个数等），它可以不需要定义。若不能替代（如作为参数等），必须含有一条定义语句。建议不管是否可替代都在类外定义一次。
若static constexpr数据成员**即使不是整型，也可进行类内初始化时。**

//整型的静态成员
static constexpr bool b2 = false;
static constexpr char c2 = 'b';
static constexpr int i2 = 2;
//浮点型的数据成员
static constexpr float f2 = 3.5;
static constexpr double d2 = 4.5;

// char m1[i1]; // 错误：i1的常量还未初始化
char m2[i2];
