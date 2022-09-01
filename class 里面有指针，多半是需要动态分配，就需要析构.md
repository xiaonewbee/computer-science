class 里面有指针，多半是需要动态分配，就需要析构



```
class Person{
	Person(){};
	~Person();
};

int main{
	Person * p = new Person();
    delete p;
}
```



两个指针指向同一块数据内存区域，叫浅拷贝



	String (const  String& str){
		mstring = new char(strlen(str)+1);
		strcpy(mstriing, str);
	}
	
	String& operator = (const String &str){
		delete[] this->m_data;
		this = new char
		strcpy
		return *this;
	}
	
	delete + 类名
	delete + 类名.数据
	~Person();
	
	Answer:
		析构函数和delete的关系
			delete用于释放new在堆中动态生成的对象空间。 释放时会自动调用类的析构函数，在析构函数中用于释放类内部动态分配的得到的资源。
当然，由于内置类型没有析构函数，所以delete内置类型指针时，什么也不需要做。


	return *this;
	这个涵义
	拿着Person&接受


成员函数都有隐藏的this指针

调制指针 debug 前32 后4