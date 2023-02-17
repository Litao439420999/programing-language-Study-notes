# list 双向链表容器



list 容器实现了双向链表的数据结构，数据元素是通过链表指针串连成逻辑意义上的线性表，这样，对链表的任一位置的元素进行插入、删除和查找都是极快速的。

双向循环链表的结构示意图如下图所示。

![](H:\迅雷云盘\云盘缓存\2022-07-13 093658.png)

list 的每个节点有三个域∶**<u>*前驱元素指针域、数据域和后继元素指针域*</u>**。前驱元素指针域保存了前驱元素的首地址;数据域则是本节点的数据;后继元素指针域则保存

了后继元素的首地址。list 的头节点的前驱元素指针域保存的是链表中尾元素的首地址，而list 的尾节点的后继元素指针域则保存了头节点的首地址，这样，就构成

了一个双向循环链。
***由于list 对象的节点并不要求在一段连续的内存中，所以，对于迭代器，只能通过"++"或"--"的操作将迭代器移动到后继/前驱节点元素处。而不能对迭代器进行+n***

***或-n的操作，这点，是与vector等不同的地方***。

使用list 需要声明头文件包含"#include<list>"。



## 1  创建 list对象

（1）创建空链表，如∶

​				list<int> l;

（2）创建具有n个元素的链表，如∶

​				list<int> l（10）;//创建具有10个元素的链表



## 2  元素插入和遍历

有三种方法往链表里插入新元素
（1）采用push_back（）方法往尾部插入新元素，链表自动扩张。

（2）采用push_front（）方法往首部插入新元素，链表自动扩张。

（3）采用 insert（）方法往迭代器位置处插入新元素，链表自动扩张。

***注意，迭代器只能进行“++”或“--”操作，不能进行+n或-n的操作，因为元素的位置并不是物理相连的。***

采用前向迭代器 iterator 对链表进行遍历。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  //在链表末尾插入元素，链表自动扩张
    l.push_back(1);
    l.push_back(5);

    l.push_front(8); //在链表头部插入元素，链表自动扩张

    list<int>:: iterator it;
    //在任意位置插入新元素，链表自动扩张；    
    it = l.begin();
    it++;   //注意：链表的迭代器，只能通过"++"或"--"的操作将迭代器移动到后继/前驱节点元素处，不能进行+n 或-n的操作
    l.insert(it,20);

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    return 0;
}
```

运行结果：

8 20 2 1 5 



## 3  反向遍历

采用反向迭代器 reverse iterator对链表进行反向遍历。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  //在链表末尾插入元素，链表自动扩张
    l.push_back(1);
    l.push_back(5);

    l.push_front(8); //在链表头部插入元素，链表自动扩张

    list<int>:: reverse_iterator rit;
   

    for(rit = l.rbegin(); rit != l.rend(); rit++)
        cout << *rit << " ";
    cout << endl;

    return 0;
}
```

运行结果：

5 1 2 8 



## 4  元素删除

（1）可以使用 remove（）方法删除链表中一个元素，值相同的元素都会被删除。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);

    l.push_front(5); 

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    l.remove(5); //删除值等于5的所有元素

     for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;
    
    return 0;
}
```

运行结果：

5 2 1 5 

2 1



（2）使用 pop_front（）方法删除链表首元素，使用pop_back（（）方法删除链表尾元素。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);

    l.push_front(5); 

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    l.pop_back();  //删除尾部元素
    l.pop_front(); //删除头部元素

     for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;
    
    return 0;
}
```

运行结果：

5 2 1 5 



2 1 



（3）使用erase（）方法删除迭代器位置上的元素。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);

    l.push_front(5); 

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    it = l.begin();  //注意这里
    it++;
    it++;
    l.erase(it); 

     for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;
    
    return 0;
}
```

运行结果：

5 2 1 5 
5 2 5 



（4）使用clear（）方法清空链表。

```C++
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);

    l.push_front(5); 

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    l.clear(); //清空链表
    cout << l.size() << endl;
    
    return 0;
}
```

运行结果：

5 2 1 5 

0



## 5 元素查找



采用 find（））查找算法可以在链表中查找元素，如果找到该元素，返回的是该元素的迭代器位置;如果没有找到，则返回 end（）迭代器位置。

**find（）算法需要声明头文件包含语句"#include<algorithm>"。**

```c++
#include <list>
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);
     l.push_back(6);  
    l.push_back(7);
    l.push_back(9);
   

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

   it = find(l.begin(),l.end(),5);
   if(it != l.end())
        cout << "find it:" << *it << endl;
    else
       cout << " not find it!\n";

    it = find(l.begin(),l.end(), 4);
     if(it != l.end())
        cout << "find it:" << *it << endl;
    else
       cout << " not find it!\n";

    
    return 0;
}
```

运行结果：

2 1 5 6 7 9 

find it:5

not find it!



## 6  元素排序

采用sort（）方法可以对链表元素进行升序排列。



```C++
#include <list>
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(5);
     l.push_back(6);  
    l.push_back(7);
    l.push_back(9);
   

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    l.sort();
    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    
    return 0;
}
```

运行结果：

2 1 5 6 7 9 

1 2 5 6 7 9 



## 7  剔除连续重复元素

采用 unique（）方法可以剔除连续重复元素，只保留一个。

```C++
#include <list>
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    list<int> l;

    l.push_back(2);  
    l.push_back(1);
    l.push_back(1);
     l.push_back(1);  
    l.push_back(5);
    l.push_back(9);
   

    list<int>:: iterator  it;   

    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    l.unique(); //剔除连续重复元素（只保留一个）
    for(it = l.begin(); it != l.end(); it++)
        cout << *it << " ";
    cout << endl;

    
    return 0;
}
```

运行结果：

2 1 1 1 5 9 
2 1 5 9