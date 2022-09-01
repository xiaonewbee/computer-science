# priority_queue用法总结

priority_queue 允许用户以任何次序将任何元素推入容器中，但取出时一定按从优先权最高的元素开始取。

heap 并不归属于 STL 容器组件，它是个幕后英雄，扮演 priority queue（优先队列）的助手。

priority_queue 完全以底部容器（一般为vector为底层容器）作为根据，再加上 heap 处理规则，所以其实现非常简单。缺省情况下是以 vector 为底部容器。.

https://blog.51cto.com/u_14301180/5354189

### 1、[头文件](https://so.csdn.net/so/search?q=头文件&spm=1001.2101.3001.7020)

```cpp
#include<queue>
1
```

### 2、定义

```cpp
priority_queue<int> p;
1
```

### 3、优先输出[大数据](https://so.csdn.net/so/search?q=大数据&spm=1001.2101.3001.7020)

```cpp
priority_queue<Type, Container, Functional>
1
```

Type为数据类型， [Container](https://so.csdn.net/so/search?q=Container&spm=1001.2101.3001.7020)为保存数据的容器，Functional为元素比较方式。

如果不写后两个参数，那么容器默认用的是[vector](https://so.csdn.net/so/search?q=vector&spm=1001.2101.3001.7020)，比较方式默认用operator<，也就是优先队列是大顶堆，队头元素最大。

​	

[csdn_link](https://blog.csdn.net/qwq1503/article/details/107343937?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165492829416782184661456%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165492829416782184661456&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-107343937-null-null.142^v13^control,157^v14^new_3&utm_term=priority_queue&spm=1018.2226.3001.4187)

假设有如下一个[struct](https://so.csdn.net/so/search?q=struct&spm=1001.2101.3001.7020)：

```

```

```c++
struct Node {
    int value;
    int idx;
    Node (int v, int i): value(v), idx(i) {}
    friend bool operator < (const struct Node &n1, const struct Node &n2) ; 
};

inline bool operator < (const struct Node &n1, const struct Node &n2) {
    return n1.value < n2.value;
}

priority_queue<Node> pq; // 此时pq为最大堆
```



---





### lc mergeKLists

```cpp



class Solution {
public:
    struct comp {
        bool operator()(ListNode* a, ListNode* b) {
            return a->val > b->val;
        }
    };

    priority_queue<ListNode*, vector<ListNode*>, comp> q;

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        for (auto node: lists) {
            if (node) q.push(node);
        }
        ListNode* head = new ListNode();
        ListNode* tail = head;
        while (!q.empty()) {
            ListNode* node = q.top();
            q.pop();
            tail->next = node; 
            tail = tail->next;
            if (node->next) q.push(node->next);
        }
        return head->next;
    }
};
```

` priority_queue<Type, Container, Functional>`

