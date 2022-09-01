### effective c++

dangle 虚吊的

17. new 对象 与 其他语句代码分行写，省的new报错，然后出现内存泄漏

18. wrapped types 外覆类型

    DDL动态链接程序库

    raw pointer 原始指针

    ##### slicing 切割 : 

    传参的时候也是，形参 A a, 结果传了B ， 就会被切割，下面的函数方法也是按照A的类型来

    切割的意思是说，你把一个子类对象赋给父类，那么相比父类，子类对象多出的成员会被丢弃掉。比如，

    ```
    class A {
       int foo;
    };
    
    class B : public A {
       int bar;
    };
    
    B b;
    A a = b;
    ```

解决方法： 传参 传 const A&  因为引用和指针才支持动态绑定多态。

---

invariants 约束条件

underlying representation 底层表述

十字军战士    

21

```
Person P;
p a, b, c, d;

((a * b) == (c * d))
上面这个翻译
(operator==(operator*(a,b), operator*(c,d)))
```

