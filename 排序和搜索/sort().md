### 自定义排序

参考http://c.biancheng.net/view/7457.html

#### C++ sort()排序函数

C++ STL 标准库中的 sort() 函数，本质就是一个**模板函数**。该函数专门用来对容器或普通数组中指定范围内的元素进行排序，排序规则**默认以元素值的大小做升序排序**，除此之外我们也可以选择标准库提供的其它排序规则（比如`std::greater<T>`降序排序规则），甚至还可以**自定义排序规则**。

#### 使用条件

sort() 函数受到底层实现方式的限制，它仅适用于普通**数组**和**部分类型的容器**

- 容器支持的迭代器类型必须为随机访问迭代器。这意味着，sort() 只对 array、vector、deque 这 3 个容器提供支持
- 如果对容器中指定区域的元素做默认升序排序，则元素类型必须支持`<`小于运算符；同样，如果选用标准库提供的其它排序规则，元素类型也必须支持该规则底层实现所用的比较运算符；
- sort() 函数在实现排序时，需要交换容器中元素的存储位置。这种情况下，如果容器中存储的是自定义的类对象，则该类的内部必须提供移动构造函数和移动赋值运算符。

#### 使用方式

sort() 函数位于`<algorithm>`头文件中，因此在使用该函数前，程序中应包含如下语句：

```c++
#include <algorithm>
```

sort() 函数有 2 种用法，其语法格式分别为：

```c++
//对 [first, last) 区域内的元素做默认的升序排序
void sort (RandomAccessIterator first, RandomAccessIterator last);
//按照指定的 comp 排序规则，对 [first, last) 区域内的元素进行排序
void sort (RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

其中，first 和 last 都为随机访问迭代器，它们的组合 [first, last) 用来指定要排序的目标区域；另外在第 2 种格式中，comp 可以是 C++ STL 标准库提供的排序规则（比如 std::greater<T>），也可以是自定义的排序规则。

关于如何自定义一个排序规则，除了《[C++ STL关联式容器自定义排序规则](http://c.biancheng.net/view/7213.html)》一节介绍的 2 种方式外，还可以直接定义一个具有 2 个参数并返回 bool 类型值的函数作为排序规则。

例如

```c++
#include <iostream>     // std::cout
#include <algorithm>    // std::sort
#include <vector>       // std::vector
//以普通函数的方式实现自定义排序规则
bool mycomp(int i, int j) {
    return (i < j);
}
//以函数对象的方式实现自定义排序规则
class mycomp2 {
public:
    bool operator() (int i, int j) {
        return (i < j);
    }
};
int main() {
    std::vector<int> myvector{ 32, 71, 12, 45, 26, 80, 53, 33 };
    //调用第一种语法格式，对 32、71、12、45 进行排序
    std::sort(myvector.begin(), myvector.begin() + 4); //(12 32 45 71) 26 80 53 33
    //调用第二种语法格式，利用STL标准库提供的其它比较规则（比如 greater<T>）进行排序
    std::sort(myvector.begin(), myvector.begin() + 4, std::greater<int>()); //(71 45 32 12) 26 80 53 33
   
    //调用第二种语法格式，通过自定义比较规则进行排序
    std::sort(myvector.begin(), myvector.end(), mycomp2());//12 26 32 33 45 53 71 80
    //输出 myvector 容器中的元素
    for (std::vector<int>::iterator it = myvector.begin(); it != myvector.end(); ++it) {
        std::cout << *it << ' ';
    }
    return 0;
}
```

程序执行结果为：

```c++
12 26 32 33 45 53 71 80
```

可以看到，程序中分别以函数和函数对象的方式自定义了具有相同功能的 mycomp 和 mycomp2 升序排序规则。需要注意的是，和为关联式容器设定排序规则不同，给 sort() 函数指定排序规则时，需要为其传入一个函数名（例如 mycomp ）或者函数对象（例如 std::greater<int>() 或者 mycomp2()）。