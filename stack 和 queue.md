 **stack 不提供走访功能，也不提供迭代器**。

除了deque之外，list也是双向开口的[数据结构](https://so.csdn.net/so/search?q=数据结构&spm=1001.2101.3001.7020)。上面 stack 源码中使用的底层容器的函数 empty，size，back，push_back等，list也都具备。**所以 list 也可以作为 stack 的底层容器**。

