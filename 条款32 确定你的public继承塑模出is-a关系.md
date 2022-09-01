# 条款32 确定你的public继承塑模出is-a关系

***\*结论：\****

***\*"\*\*public继承"意味is-a\*\*。适用于base class身上的每一件事情一定也适用与derived class身上，因为每一个derived class对象也都是一个base class对象。\****

企鹅是一种鸟，这是事实；鸟可以飞，这也是事实。但是企鹅不会飞。那么：

但是下面的例子就不适合用public继承，因为它不是Is-a关系：

```cpp
class Bird {
public:
      virtual void fly();   //鸟可以飞
};
 
class Penguin: public Bird {  //企鹅是一种鸟
      ...
};
```