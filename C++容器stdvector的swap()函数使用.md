[C++容器std::vector的swap()函数使用](https://blog.csdn.net/feikudai8460/article/details/104902914?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165526165516781667826865%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165526165516781667826865&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-2-104902914-null-null.142^v16^control,157^v14^new_3&utm_term=c%2B%2B+vector+swap&spm=1018.2226.3001.4187)

std::vector中的常用函数：
  .clear();清空数据

  .size();当前vector容器内存储的元素的个数

  .capacity();当前vector容器重新分配内存之前所能容纳的元素数量

  .swap();函数交换

  .reserve();向系统预订一段足够的连续的空间


.swap用于释放内存：
  首先，vector与deque不同，其内存占用空间只会增长，不会减小。比如你首先分配了10,000个字节，然后erase掉后面9,999个，则虽然有效元素只有一个，但是内存占用仍为10,000个。所有空间在vector析构时回收。
  在用vector时，输入完一组数据处理完后，调用clear()进行清理，如果此时打印vector[0]，会发现仍然输出之前vector所存的内容，但是如果调用.empty()函数又会返回1，告诉我们这个容器现在是空的，什么原因？ 这是因为使用.clear()清空内容，但是没有释放内存的原因。
