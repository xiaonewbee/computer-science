

3、既然已经有了const、static成员变量，那么static const 成员变量的产生也就顺理成章了。static const成员变量可以认为是该文件一个专属的成员变量，它属于类本身，并为所有对象、友元函数所共享。

 static const成员变量初始化方式，与static成员变量相同，例：

```c++
class C
{
	public:
		C(){}
	private:
		static const string s;
};
const string C::s="hello world";//在类体外初始化，同样省略掉static
```



> static const int NumTurns=5;*//常量声明式*
>
> 通过static const修饰的整型变量由于未定义，在编译的过程中直接被初始化的值所替代，这样可以简化内存。