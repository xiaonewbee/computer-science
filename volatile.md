易变性：volatile告诉编译器，某个变量是易变的，当编译器遇到这个变量的时候，只能从变量的内存地址中读取这个变量，不可以从缓存、寄存器、或者其它   任何地方读取。
顺序性：两个包含volatile变量的指令，编译后不可以乱序。注意是编译后不乱序，但是在执行的过程中还是可能会乱序的，这点需要由其它机制来保证，例如memory- barriers。
不可优化性：volatile告诉编译器，不要对这个变量进行各种激进的优化，甚至将变量直接消除，保证代码中的指令一定会被执行。

# [volatile(防止编译器对代码进行优化,常用于多线程环境中)](https://www.cnblogs.com/Stephen-Qin/p/11388620.html)

一.单词解释

- adj.易变的；无定性的；无常性的；可能急剧波动的

**精确地说就是，优化器在用到这个变量时必须每次都小心地重新读取这个变量的值，而不是使用保存在寄存器里的备份。**


**\1. 编译器的优化**

在本次线程内, 当读取一个变量时，为提高存取速度，编译器优化时有时会先把变量**读取到一个寄存器**中；以后，再取变量值时，**就直接从寄存器中取值；**

当变量值在本线程里改变时，**会同时把变量的新值copy到该寄存器中，**以便保持一致

当变量在因别的线程等而改变了值，该寄存器的值不会相应改变，从而造成应用程序读取的值和实际的变量值不一致

当该寄存器在因别的线程等而改变了值，原变量的值不会改变，从而造成应用程序读取的值和实际的变量值不一致 

volatile关键字是一种类型修饰符