- explicit 修饰构造函数时，可以防止隐式转换和复制初始化
- explicit 修饰转换函数时，可以防止隐式转换，但按语境转换除外

*explicit 只对构造函数起作用，用来抑制隐式转换*

https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-mean?rq=1

![Snipaste_2022-07-02_10-55-12](D:\路径不动的文件\图片\侯捷\Snipaste_2022-07-02_10-55-12.png)

```cpp
class String {
public:
    String(int n); // allocate n bytes to the String object
    String(const char *p); // initializes object with char *p
};
```

Now, if you try:

```cpp
String mystring = 'x';
```

The character `'x'` will be implicitly converted to `int` and then the `String(int)` constructor will be called. But, this is not what the user might have intended. So, to prevent such conditions, we shall define the constructor as `explicit`:

```cpp
class String {
public:
    explicit String (int n); //allocate n bytes
    String(const char *p); // initialize sobject with string p
};
```