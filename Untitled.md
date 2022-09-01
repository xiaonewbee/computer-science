```c++
   // 服务窗口的总数
    int window_num;
    
    // 总的营业时间
    int total_service_time;
    
    // 顾客的逗留总时间
    int total_customer_stay_time;
    
    // 总顾客数
    int total_customer_num;
    
    ServiceWindow*  windows;
    Queue<Customer> customer_list;
    Queue<Event>       event_list;
    Event*          current_event;
    
    double avg_customers;
    double avg_stay_time;
```

**对于一个银行而言，对外界来说只需要提供两个参数：**

1. **总共的服务时间**
2. **服务窗口的数量**

**对于顾客而言，有两个属性是能够被抽象出来的：**

1. **到达银行的时间；**
2. **需要服务的时间。**

**总结一下，现在我们需要实现的东西有：**

1. **服务窗口类(会被创建 w 个)**
2. **顾客队列类(只会被创建一个)**
3. **顾客结构(包含两个随机属性: 到达时间, 服务时间)**

每个顾客说需要的服务时间是随机的，但是到达时间并不应该由顾客自身确定

顾客也会成为等待队列中的一员。所以，Customer 也可以被称之为队列的一个 Node

整个系统还处于静止状态。当顾客位于等待队列时，窗口什么时候服务下一个顾客，如何处理这里面的逻辑，到目前为止，我们都没有思考过。

