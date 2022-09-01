

```
	printf("maxdepth=%d\n", *maxDepth);
指针型变量也可以用%d
```



2. string.push_back() 函数来在一个 string 对象后面附加一个字符 

   

   ```
   string str("hello");
   char ch = 'a';
   str.push_back(ch);
   
   ```

   使用 string.substr() 函数来获取子串

   ```
   string str("hello");
   string str2 = str.substr(3,2)
   
   ```

3. short ≤ int ≤ long ≤ long long

# 11. 理解复合类型的声明

`int* p;` 中，int 是基本数据类型，* 是类型修饰符，修饰 p 而不是 int
因此 `int* p1, p2;` 中，p1 是 int 类型的指针，p2 是 int，因为 * 只修饰了 p1



# 13. const 限定符

默认状态下，const 对象仅在文件内有效
想在多个文件之间共享 const 对象，必须在变量的定义之前添加 extern 关键字

# 16. 指向常量的XX 常量XX

```
const <T> &var //指向常量的引用 不能被用作修改他所绑定的对象
const <T> *var //指向常量的指针 不能被用作修改他所指向的对象
<T> *const var //常量指针 指针本身是常量

```

```
const <T> &var //指向常量的引用 不能被用作修改他所绑定的对象 底层 const
const <T> *var //指向常量的指针 不能被用作修改他所指向的对象 底层 const
<T> *const var //常量指针 指针本身是常量 顶层 const

```

# 22. 头文件不应包含 using 声明

![在这里插入图片描述](https://img-blog.csdnimg.cn/4ce21d9a8a744342b32f3ecdeb1df0d4.png#pic_center)

# 赋值操作的右结合性

与下标和解引用 操作符一样，赋值操作也返回左值。

赋值操作符的优先级低于不等操作符（！=）
