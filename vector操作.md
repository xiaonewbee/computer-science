```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
    vector<int> v;
    //Insert values 1 to 10
    v.push_back(20);
    v.push_back(10);
    v.push_back(30);
    v.push_back(20);
    v.push_back(40);
    v.push_back(20);
    v.push_back(10);

    vector<int>::iterator new_end;
    new_end = remove(v.begin(), v.end(), 20);

    for(int i=0;i<v.size(); i++){
        cout << v[i] << " ";
    }
    //Prints [10 30 40 10]
    return 0;
}

```

https://iq.opengenus.org/ways-to-remove-elements-from-vector-cpp/

```
1.在c++中，vector是一个十分有用的容器，下面对这个容器做一下总结。

(1)头文件#include<vector>.

(2)创建vector对象，vector<int> vec;

(3)初始化vector对象，vector<T> v1;  类型为T的默认初始化

                                   vector<T> v2(n,val); v2中包含了n个类型为T值为val的元素

                                   vector<T> v3{  a, b, c ...  }; 列表初始化 

 注：vector<int> v1{10,1}; v1有两个 元素 0和1

        vector<int> v2(10,1); v2有十个元素，每个都是1

(4)尾部插入元素：vec.push_back(a);

(5)插入元素：    vec.insert(vec.begin()+i,a);在第i+1个元素前面插入a;
(6)使用下标访问元素，cout<<vec[0]<<endl;但是不能直接赋值，vec[0]=1//!!严重错误。

(7)删除元素：    vec.erase(vec.begin()+2);删除第3个元素

                         vec.erase(vec.begin()+i,vec.end()+j);删除区间[i,j-1];区间从0开始

(8)向量大小:      vec.size();

(9)清空:             vec.clear();
(10)使用sort排序：需要头文件#include<algorithm>，

      sort(vec.begin(),vec.end());(默认是按升序排列,即从小到大).

      可以通过重写排序比较函数按照降序比较，如下：

      bool Comp(const int &a,const int &b)
   {
    return a>b;
   }
    调用时:sort(vec.begin(),vec.end(),Comp)，这样就降序排序。


```

