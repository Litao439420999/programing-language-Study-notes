# deque 双端队列容器



**deque 双端队列容器与 vector 一样，采用线性表顺序存储结构**。但与 vector 唯一不同的是，***deque 采用分块的线性存储结构来存储数据，每块的大小一般***

***为512字节，称为一个deque 块，所有的 deque 块使用一个 Map 块进行管理，每个Map 数据项记录各个 deque块的首地址***。这样一来，deque 块在头部和尾部

都可插入和删除元素，而不需移动其他元素（使用 push _back（）方法在尾部插入元素，会扩张队列;而使用push _front（）方法在首部插入元素和使用 insert

（）方法在中间插入元素，只是将原位置上的元素值覆盖，不会增加新元素）。一般来说，当考虑到容器元素的内存分配策略和操作的性能时，deque 相对于

vector 更有优势。双端队列容器结构示意图如下图所示。



![](H:\迅雷云盘\云盘缓存\2022-07-13 082332.png)



**使用 deque 需要声明头文件包含"#include <deque>"。**



## 1  创建 deque 对象

创建 deque 对象的方法通常有三种。

（1）创建没有任何元素的deque 对象，如∶

​         deque<int> d;

​         deque<float> d;

（2）创建具有n个元素的 deque 对象，如∶

​          deque<int> d（10）;//创建具有10 个整型元素为0的 deque 对象 d 

（3）创建具有n个元素的 deque 对象，并赋初值，如∶ 

​          deque<int>d（10，8.5）;//创建具有10个整型元素的 deque对象d，每个元素值为8.5



## 2   插入元素

**（1）使用push back（）方法从尾部插入元素，会不断扩张队列。**



```c++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    //以数组方式输出
    for(int i = 0; i < d.size(); i++)
        cout << d[i] << " ";
    cout << endl;
    return 0;
}

```

运行结果：

1 2 3 



**（2）从头部插入元素，不会增加新元素，只将原有的元素覆盖。**<!--这里有问题，待续-->

```c++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    d.push_front(10); //从头部开始地方插入新元素，但不增加新元素
    d.push_front(20);

    /*deque<int>:: iterator it;
    for(it = d.begin(); it != d.end(); it++)
        cout << *it << " ";*/

    //以数组方式输出
    //for(int i = 0; i < d.size(); i++)
    //    cout << d[i] << " ";
    //cout << endl;
    //cout << endl;
    cout << d[0] << " " << d[1] << " " << d[2] << endl;
   
    return 0;
}

```

运行结果：

20 10 1   （***<u>这里有问题，原有元素不是覆盖，而是向后面后移了</u>***。）



**（3）从中间插入元素，不会增加新元素，只将原有的元素覆盖。**<!--有问题-->

 

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    d.insert(d.begin()+1,8); //中间插入元素，不会增加新元素，只将原有的元素覆盖???这里有问题
    cout << d[0] << " " << d[1] << " " << d[2] << endl;

    deque<int>:: iterator it;
    for(it = d.begin(); it != d.end(); it++)
        cout << *it << " ";
    cout << endl;


    return 0;
}
```

运行结果

1 8 2
1 8 2 3

（***<u>这里有问题，原有元素不是覆盖，而是向后面后移了</u>***。）



## 3   遍历元素



**（1）以数组方式遍历。**



```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    for(int i = 0; i < d.size(); i++)
        cout << d[i] << " ";
    cout << endl;

    return 0;
}
```

运行结果：

1 2 3



**（2）以前向迭代器的方式遍历。**



```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    deque<int>:: iterator it;
    for(it = d.begin(); it != d.end(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

运行结果：

1 2 3



## 4 反向遍历



采用反向迭代器对双端队列容器进行反向遍历。

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);

    deque<int>:: reverse_iterator rit;
    for(rit = d.rbegin();rit != d.rend(); rit++)
        cout << *rit << " ";
    cout << endl;

    return 0;
}
```

运行结果：

3 2 1



## 5  删除元素

可以从双端队列容器的首部、尾部、中部删除元素，并可以清空双端队列容器。下面分别举例说明这4种删除元素的操作方法。

（1）采用 pop_front（）方法从头部删除元素。

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);
    d.push_back(4);
    d.push_back(5);
    
    //从头部删除
    d.pop_front();
    d.pop_front();
    
        
    deque<int>:: iterator it;
    for(it = d.begin();it != d.end(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

运行结果：

3 4 5 



（2）采用pop_back（）方法从尾部删除元素。

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);
    d.push_back(4);
    d.push_back(5);
    
    //从尾部部删除
    d.pop_back();
    d.pop_back();   
    
        
    deque<int>:: iterator it;
    for(it = d.begin();it != d.end(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

运行结果：

1 2 3



（3）使用erase（）方法从中间删除元素，其参数是迭代器位置。

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);
    d.push_back(4);
    d.push_back(5);
    
    d.erase(d.begin() + 2);
    
        
    deque<int>:: iterator it;
    for(it = d.begin();it != d.end(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

运行结果：

1 2 4 5

（4）使用clear（）方法清空 deque 对象。

```C++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
    deque<int> d;

    d.push_back(1);  // 从尾部连续插入三个元素
    d.push_back(2);
    d.push_back(3);
    d.push_back(4);
    d.push_back(5);

    //清空队列
    d.clear();

    cout << d.size() << endl;
    return 0;
}
```

