# C++继承体系中Is a 关系 和has a关系

[C++继承体系中Is a 关系 和has a关系](https://blog.csdn.net/My_heart_/article/details/52400419?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165554758616782246445333%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165554758616782246445333&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-52400419-null-null.142^v17^control,157^v15^new_3&utm_term=%E5%AD%90%E7%B1%BB+is+a+%E7%88%B6%E7%B1%BB&spm=1018.2226.3001.4187)

在学习继承的过程中，不管是在书中还是在网上找资料，都跟多态分不开，其中还有个很抓人眼球的问题，那就是书上总是说的is-a关系和has-a关系。 
　　很多书中讲到继承时都会说： 
　　public继承是一个接口继承，保持is-a原则，每个父类可用的成员对子类也可用，因为每个子类对象也都是一个父类对象。 （子类 is a  父类）
　　protetced/private继承是一个实现继承，基类的部分成员并非完全成为子类接口的一部分，是 has-a 的关系原则。 （子类 has a  父类）
　　那is-a，has-a原则究竟是什么呢。

is a

举例说明：

有一个Horse类可以保存关于马的所有信息，身高体重等等，那么我们就可以从Horse类中派生出白马类，白马类包含所有Horse类的成员，在白马类中可以新增关于白马的成员，这个成员通常不用于Horse类。
————————————————
