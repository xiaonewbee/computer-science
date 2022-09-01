### 二、**ptrdiff_t**数据类型

- 这是**有符号**整数类型，**它是两个指针相减的结果**
- ptrdiff_t通常被定义为**long int**类型

**与size_t的区别：**

- 因为size_t通常用来表示数组的长度等，所以s**ize_t**必须是一个**正数**所以被设计为**unsigned类型**
- ptrdiff_t应保证足以存放同一数组中两个指针之间的差距，而距离有可能是负数，所以被设计为**signed类型**



# [size_t是什么数据类型？为什么要用size_t替代int、unsigned int、unsigned long、unsigned long long](https://blog.csdn.net/Dontla/article/details/121514064?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166057579416782391863854%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166057579416782391863854&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_v36-2-121514064-null-null.142^v40^pc_rank_v36,185^v2^control&utm_term=size_t%20%E6%98%AF%E6%95%B4%E5%9E%8B&spm=1018.2226.3001.4187)



**int小于等于数据线宽度，size_t大于等于地址线宽度。size_t存在的最大原因可能是因为：地址线宽度历史中经常都是大于数据线宽度的。**



计组： CPU的地址线数往往比存储芯片的地址线数多。

​	通常将CPU地址线的低位与存储芯片的地址线相连。

​	CPU的高位在存储芯片扩充的时候用，或片选芯片

数据线： CPU的数据线数与存储芯片的数据线数也不一定相等，**<u>必须</u>**对存储芯片扩位，使其相等

下面是自己写的代码，可以随意尝试

```

class Animal
{
public:
    Animal() : age(nullptr), male(nullptr) , male2(nullptr), male3(nullptr) {}


    Animal& operator=(const Animal &other) {
        if (this != &other) {
            cout<<"operator ="<<endl;
        }
        return *this;
    }

    Animal& operator--(){
        cout<<"operator --"<<endl;
        return *this;
    }

    Animal operator--(int){
        auto tmp = *this;
        cout<< sizeof(tmp) << endl;
        cout<< "sizeof tmp" << endl;
        --*this;
        // cout<< "tmp : " << *tmp << endl;
        printf("*p = %x\n", this);
        // cout<< "this : " << *this << endl;
        printf("*p = %x\n", *this);
        printf("*p = %x\n", tmp);
        printf("*p = %d\n", sizeof(*this));
        printf("*p = %d\n", sizeof(this)); 
        return tmp;
    }
private:
    int* age;
    int* male;
    int* male2;
    int* male3;
};

int main()
{

    // 右值引用
    int num = 10;
    // int && a = num;    // 错误，右值引用不能初始化为左值
    int &&a = 10; // 正确

    a = 100;
    // cout << a << endl; // 输出为100，右值引用可以修改值

    // Person<int> p(&&num);
    vector<Animal>v(10);
    // auto p1 = v.begin();
    // auto p2 = v+5;
    auto v1 = v[1];
    auto v2 = v[2];
    auto v3 = v[3];
    auto v4 = v[4];
    cout << "before ..." << std::endl;
    cout << &v1 << std::endl;
    cout << &v2 << std::endl;
    cout << &v[4] << std::endl;
    cout << &v[5] << std::endl;
    // printf("a%d\n", &v[5]);a38611056  4*8=32
    // printf("a%d\n", &v[4]);a38611024
    // printf("a%d\n", &v[3]);a38610992

    cout << &v[5] - &v[4] << std::endl;
    cout << endl;

    cout <<  &v1 - &v3 << std::endl;
    ptrdiff_t difp = &v1 - &v2;
    size_t difp_t = &v1 - &v2;
    cout << difp << std::endl;
    cout << difp_t << std::endl;
    cout << endl;

    std::ptrdiff_t len1=&v[2]-&v[0];
    std::ptrdiff_t len2=&v[0]-&v[3];
 
    std::cout<<"&arr[3]-&arr[0] is "<<len1<<std::endl;
    std::cout<<"&arr[0]-&arr[3] is "<<len2<<std::endl;
    // difp = p1 - p2;
    // cout << difp << std::endl;
    // Animal ani;
    // ani --;
    // std::cout << "before copy constructor..." << std::endl;
    // Foo foo1 = FooFactory();
    // std::cout << "after copy constructor..." << std::endl
    //           << std::endl;
    // // 引用右值，避免生成新对象
    // Foo &&foo2 = FooFactory();
    // std::cout << "life time ends!" << std::endl
    //           << std::endl;

    return 0;
}

```

