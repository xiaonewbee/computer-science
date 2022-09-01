   1、首先需要从const谈起。我们知道由**const修饰的变量**其对应的数值保持恒定不变。类的成员变量，如果由const 修饰，**能且只能**在构造函数的初始化列表中完成初始化。例：

const **必须**在初始化列表里完成初始化，不能在后面的构造函数体内完成赋值操作

```cpp
class A
{
	public:	
		A():a(1){}
	private:
		const int a;
};
```

若static const数据成员不是整型（bool、char、int、short、long等），则不能在类内初始化。

 原因在于const成员变量，它属于类生成的对象，在每一个对象中都包含了一个相应的const成员变量。在建立对象的过程中完成const成员变量的初始化。而必须在初始化列表中完成初始化则是由于当const成员变量出现**在构造函数体内时默认完成的是<u>赋值操作</u>**。这**与const成员变量必须保持相应的值不变相矛盾。**



其实，const还有一个含义，就是在函数的参数列表的“)”之后，函数体的“{”之前。这种用法说明函数不会修改目标对象的值。





关键就是加了一个该死的const。因为常变量是无法在初始化操作之外变更的。

所以你在声明的时候不初始化，之后就无法在编译期对它进行赋值了，只能读：）