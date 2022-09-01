### 条款39：明智而审慎地使用private继承

**这个有点难**

**暂时不理解**

当需要复合时，尽可能的使用复合,必要时才使用private: 当protected成员或virtual函数牵扯进来的时候 当空间方面的利害关系，需要尺寸最小化



**private继承意味着implemented-in-terms-of**(根据某物实现出)

private继承绝不是is-a的关系。



https://blog.csdn.net/zhizhengguan/article/details/116675552

[链接2](https://blog.csdn.net/qq_36333986/article/details/109660644?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-109660644-blog-116675552.t5_layer_eslanding_D_4&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-109660644-blog-116675552.t5_layer_eslanding_D_4&utm_relevant_index=2)

[stackoverflow 1](https://stackoverflow.com/questions/7209019/private-inheritance-vs-composition-when-to-use-which)

> "Only inheritance gives access to protected members, and only inheritance allows for virtual functions to be redefined. Because virtual functions and protected members exist, private inheritance is sometimes the only practical way to express an is-implemented-in-terms-of relationship between classes."



降低编译时的依赖程度

c++ 189页

例子