```
二、匿名函数的形式

[capture](parameters)->return-type{body} 

[捕获列表](参数列表)->返回类型-{函数主体}
```

capture：捕获列表

[]        //捕获列表为空。在函数内无法使用外部变量。
[a]      //捕获列表为按值传递形式。在函数内仅能使用传递的变量值，无法改变变量。值在匿名函数生成时便已经确定，后续修改不会影响函数内的变量值。
[&a]    //按应用传递。可改变变量。

```
#include<iostream>
using namespace std;
int main(){
    int x=1,y=2,z=0;
    auto add = [&z](auto x,auto y){z=x+y;return z;};
    auto res = add(x,y);
    cout<<res<<z<<endl;
}
```

