# C++STL概述

​		在 ACM竞赛中，需要用到数组、字符串、队列、堆栈、链表、平衡二叉检索树等数据结构和排序、搜索等算法，以提高程序的时间、空间运行效率。这些数据结构，如果都需要手工来编写，那是相当麻烦的事情。
​	幸运的是，ANSI C++中包含了一个C++ STL（Standard Template Library），即**C++标准模板库**，又称**C++泛型库**，*<u>它在 std 命名空间中定义了常用的数据结构和算法</u>*，使用起来十分方便。

## C++STL组件

​		STL提供三种类型的组件∶**容器、迭代器和算法**，它们都支持泛型程序设计标准。容器主要有两类∶**顺序容器和关联容器**。<u>*顺序容器（vector、list、deque 和 string 等）是一系列元素的有序集合。关联容器（set、multiset、map和multimap）包含查找元素的键值*</u>。
**迭代器的作用是遍历容器。**

​		STL 算法库包含四类算法∶**排序算法、不可变序算法、变序性算法和数值算法**。

举例：

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
using namespace std;

int main()
{
    vector<int> v;
    int i;

    //赋值
    for(i = 0; i < 10; i++)
    {
        v.push_back(i);  // 尾部元素扩张方式赋值
    }

    //使用迭代器遍历所有元素
    vector<int>::iterator  it ;
    for(it = v.begin(); it != v.end(); it++)
        cout << *it << "\t" ;
    
    cout << endl;

    cout << accumulate(v.begin(),v.end(),0) << endl;  //accumulate函数定义numeric头文件

    return 0;

}
```



## vector向量容器

**vector 向量容器不但能像数组一样对元素进行随机访问，还能在尾部插入元素，是一种简单、高效的容器，完全可以代替数组。**

值得注意的是，***<u>vector 具有内存自动管理的功能，对于元素的插入和删除，可动态调整所占的内存空间</u>***。

**vector容器的下标是从0开始计数的，也就是说，如果vector容器的大小是n，那么，元素的下标是0～n-1**。对于vector容器的容量定义，可以事先定义一个固定大小，事后，可以随时调整其大小；**也可以事先不定义，随时使用push_back（）方法从尾部扩张元素，也可以使用insert（）在某个元素位置前插入新元素**。
vector容器有两个重要的方法，**begin（）和end（）**。begin（）返回的是首元素位置的迭代器；end（）返回的是最后一个元素的下一元素位置的迭代器。

**1 创建 vector 对象**
创建 vector 对象常用的有三种形式。
（1）不指定容器的元素个数，如定义一个用来存储整型的容器∶vector<int> v;

（2）创建时，指定容器的大小，如定义一个用来存储 10个double类型元素的向量容器∶vector<double> v (10);
**注意，元素的下标为0～9;另外，每个元素的值被初始化为0.0。**

（3）创建一个具有n个元素的向量容器对象，每个元素具有指定的初始值∶vector<double> v(10,8.6);
上述语句定义了v 向量容器，共有10个元素，每个元素的值是8.6。



**2  尾部元素扩张**
通常使用 push_back（）对 vector 容器在尾部追加新元素。尾部追加元素，vector 容器会自动分配新内存空间。可对空的 vector 对象扩张，也可对已有元素的 vector 对象扩张。

举例：

```C++ 
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> v;
    v.push_back(2);
    v.push_back(7);
    v.push_back(9);

    for(int i = 0; i < v.size(); i++)
        cout << v[i] << " ";
    
    cout << endl;

    return 0;
}
```

上面的代码将 2，7，9三个元素从尾部添加到v 容器中，这样，v 容器中就有三个元素，其值依次是2，7，9。

访问或遍历 vector 对象是常要做的事情。对于vector对象，可以采用下标方式随意访问它的某个元素，当然，也可以以下标方式对某元素重新赋值，这点类似于数组的访问方式。

```C++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> v(3);
    v[0] = 2;
    v[1] = 7;
    v[2] = 9;

    for(int i = 0; i < v.size(); i++)
        cout << v[i] << " ";
    
    cout << endl;

    return 0;
}
```



**3  用迭代器访问 vector 元素** 
常使用迭代器配合循环语句来对vector 对象进行遍历访问，迭代器的类型一定要与它要遍历的 vector 对象的元素类型一致。

```c++
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    vector<int> v(3);
    v[0] = 2;
    v[1] = 7;
    v[2] = 9;

    vector<int>:: iterator it;
    for(it = v.begin(); it != v.end(); it++)
    {
        cout << *it << " ";
    }

    cout << endl;
    return 0;

}
```



**4 元素的插入**
insert（）方法可以**在 vector 对象的任意位置前插入一个新的元素**，同时，vector 自动扩张一个元素空间，**插入位置后的所有元素依次向后挪动一个位置**。
**要注意的是，insert（）方法要求插入的位置，是*<u>元素的迭代器位置</u>*，而不是元素的下标。**



```C++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector <int> v(3);
    v[0] = 2;
    v[1] = 7;
    v[2] = 9;

    v.insert(v.begin(),8);  // 在最前面插入新元素，元素值为8;
    v.insert(v.begin() + 2, 1); //在第二个元素前插入新元素1;
    v.insert(v.end(), 3); //在向量末尾追加新元素3;

    //定义迭代器变量
    vector<int> :: iterator  it;
    for(it = v.begin(); it != v.end(); it++)
        cout << *it << " ";
    
    cout << endl;
    return 0;

}
```

最后输出结果为：

8 2 1 7 9 3 



**5  元素的删除**

**erase（）方法可以删除vector中迭代器所指的一个元素或一段区间中的所有元素。clear（）方法则一次性删除 vector 中的所有元素。**

```c++
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    vector<int> v(10);

    for(int i = 0; i < 10; i++) //前提是有确切的长度
        v[i] = i;
    
    v.erase(v.begin() + 2); //删除第2个元素，从0开始计数；

    vector<int>:: iterator it;
    for(it = v.begin(); it != v.end(); it++)
        cout << *it << " ";
    cout << endl;

    v.erase(v.begin()+1, v.begin()+5);//删除迭代器第2个元素到第5个区间的所有元素；
     for(it = v.begin(); it != v.end(); it++)
        cout << *it << " ";
    
    cout << endl;
    return 0;
}   


```

输出结果为：

0 1 3 4 5 6 7 8 9 
0 6 7 8 9



```c++
 v.clear() ; //清空向量
 cout << v.size() << endl;
```



**6 使用reverse反向排列算法**
reverse 反向排列算法，**需要定义头文件"#include <algorithm>"**，reverse 算法可将向量中某段迭代器区间元素反向排列。

```C++
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> v(10);
    for(int i = 0; i < 10; i++)
    {
        v[i] = i;
    }

    reverse(v.begin(), v.end()); // 反向排列向量的从首到尾间的元素
    vector<int>:: iterator it;

    for(it = v.begin(); it != v.end(); it++)
        cout << *it << " ";
    
    cout << endl;

    reverse(v.begin()+3, v.end()-2);
     for(it = v.begin(); it != v.end(); it++)
        cout << *it << " ";

    cout << endl;
    return 0;


}
```

运行结果：

9 8 7 6 5 4 3 2 1 0 
9 8 7 2 3 4 5 6 1 0



**7.使用 sort 算法对向量元素排序**

使用 sort算法，需要声明头文件**"#include <algorithm>"。**
sort 算法要求使用随机访问迭代器进行排序，**在默认的情况下，对向量元素进行升序排列**。

```C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> v;

    int i;

    for(i = 0; i < 10; i++)
        v.push_back(9 - i);
     
    for(i = 0; i < 10; i++ )
        cout << v[i] << " ";
    cout << endl;

    sort(v.begin(),v.end()); // 默认为升序排列
     for(i = 0; i < 10; i++ )
        cout << v[i] << " ";
    cout << endl;

    return 0;
}
```

运行结果：

9 8 7 6 5 4 3 2 1 0 
0 1 2 3 4 5 6 7 8 9



还可以**自己设计排序比较函数**，然后，把这个函数指定给 sort 算法，那么，sort 就根据这个比较函数指定的排序规则进行排序。下面的程序自己设计了一个排序比较函数Comp，要求对元素的值由大到小排序∶

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool Comp(const int &a, const int &b)
{
    if(a!=b)return a>b;
    else return a>b;
}

int main()
{
    vector<int> v;
    int i;

    for(i = 0;i < 10; i++)
        v.push_back(i);
    
    for(i = 0; i < 10; i++)
        cout << v[i] << " ";
    cout << endl;

    sort(v.begin(),v.end(),Comp);
    for(i = 0; i < 10; i++)
        cout << v[i] << " ";
    cout << endl;

    return 0;

}
```

运行结果：

0 1 2 3 4 5 6 7 8 9 
9 8 7 6 5 4 3 2 1 0



**8  向量的大小**
使用size（（）方法可以返回向量的大小，即元素的个数。使用 empty（）方法返回向量是否为空。

```C++ 
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> v;

    int i;

    for(i = 0; i < 10; i++)
        v.push_back(9 - i);
     
    cout << v.size() << endl; //输出向量的大小，即包含了多少个元素
    cout << v.empty() << endl;
    v.clear(); //清空向量
     cout << v.empty() << endl;
    return 0;
}
```

运行结果：

10
0
1

向量的使用方法还有很多，这里举出的只是常用的方法，如果需要更为详实的资料，请大家参考C++STL 相关材料。
另外，向量的元素类型可以是 int，double，char 等简单类型，也可以是结构体或string 基本字符序列容器，使用起来非常灵活。