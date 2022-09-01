
size_type是**容器概念**，没有容器不能使用

* 是和string类类型和vector类类型定义相关的类型，用以保存任意string对象或vector对象的长度，标准库类型将size_type定义为unsigned类型
* string抽象意义是字符串， size（）的抽象意义是字符串的尺寸， string::size_type抽象意义是尺寸单位类型
* string::size_type可以实现在不同的机器上，动态调整长度，并非先前固定长度。但是使用了这个类型，就必须使得你的程序适合这个机器，与实际机器匹配。
* string::size_type从本质上来说，是一个整型数。关键是由于机器的环境，它的长度有可能不同。 例如：我们在使用 string::find的函数的时候，它返回的类型就是 
* string::size_type类型。而当find找不到所要找的字符的时候，它返回的是 npos的值，这个值是与size_type相关的。　　
  st.size()表示st中的字符数量，字符数量的统计是由 1 开始累计计算的，所以字符数量正好比字符串的下标索引数（由 0 开始累计计算）大 1 。
* size_type是容器概念，没有容器不能使用
  ————————————————
* 原文链接：https://blog.csdn.net/CHYabc123456hh/article/details/108984260



---

size_t不是容器概念。
size_type是容器概念，没有容器不能使用。



### 我们为什么不适用int变量来保存string的size呢？

使用int变量的问题是：有些机器上的int变量的表示范围太小，甚至无法存储实际并不长的string对象。如在有16位int型的机器上，int类型变量最大只能表示32767个字符的string对象。而能容纳一个文件内容的string对象轻易就能超过这个数字，因此，为了避免溢出，保存一个string对象的size的最安全的方法就是使用标准库类型string：：size_type().

| 32位机器 | size_t = unsigned int      | 4字节 |
| -------- | -------------------------- | ----- |
| 64位机器 | size_t = unsigned long int | 8字节 |

https://blog.csdn.net/lzx_bupt/article/details/6558566

[csdn_link](https://blog.csdn.net/weixin_44009743/article/details/90112439?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165484884216781683970477%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165484884216781683970477&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-3-90112439-null-null.142^v13^control,157^v14^new_3&utm_term=c%2B%2B+size_type&spm=1018.2226.3001.4187)