# set 集合容器

set 集合容器实现了红黑树（Red-Black Tree）的平衡二叉检索树的数据结构，**在插入元素时，它会自动调整二叉树的排列，把该元素放到适当的位置，以确保每个子树根节点的键值大于左子树所有节点的键值，而小于右子树所有节点的键值**;另外，还得确保**根节点左子树的高度与右子树的高度相等，**这样，二叉树的高度最小，从而检索速度最快。**要注意的是，它不会重复插入相同键值的元素，而采取忽略处理**。下图是一个典型的红黑树。

![](H:\迅雷云盘\云盘缓存\2022-07-10 140726.png)

​		**平衡二叉检索树的检索使用中序遍历算法，检索效率高于vector、deque 和 list 等容器**。另外，采用中序遍历算法可将键值由小到大遍历出来，所以，可以理解为平衡二叉检索树在插入元素时，就会自动将元素按键值由小到大的顺序排列。
​		对于 set 容器中的键值，不可直接去修改。因为如果把容器中的一个键值修改了，set 容器会根据新的键值旋转子树，以保持新的平衡，这样，修改的键值很可能就不在原先那个位置上了。**换句话来说，构造 set集合的主要目的就是为了快速检索**。
​		**multiset（多重集合容器）、map（映照容器）和 multimap（多重映照容器）的内部结构也是平衡二叉检索**树。
​		**使用 set 前，需要在程序的头文件中包含声明"#include<set>";它包含了set和 multiset 两种容器的定义。**



**1 创建 Set 集合对象**


创建 set 对象时，需要指定元素的类型，这一点与其他容器一样。下面的程序详细说明了如何创建集合对象。

```C++
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> s;

    s.insert(8); // 第一次插入8
    s.insert(1);
    s.insert(12);
    s.insert(6);
    s.insert(8); //第二次插入8,重复元素不会插入

    //中序遍历集合中的元素
    set<int>:: iterator it;  //定义前向迭代器；
    for(it = s.begin(); it != s.end(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```

运行结果：

1 6 8 12

**2 元素的反向遍历**

**使用反向迭代器 reverse iterator可以反向遍历集合**，输出的结果正好是集合元素的反向排序结果。它需要用到***rbegin（）***和 ***rend（***）两个方法，它们分别给出了反向遍历的开始位置和结束位置。

```C++
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> s;

    s.insert(8); // 第一次插入8
    s.insert(1);
    s.insert(12);
    s.insert(6);
    s.insert(8); //第二次插入8,重复元素不会插入

    //反向遍历集合中的元素
    set<int>:: reverse_iterator it;
    for(it = s.rbegin(); it != s.rend(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```



**3  元素的删除**
与插入元素的处理一样**，集合具有高效的删除处理功能，并自动重新调整内部的红黑树的平衡**。删除的对象可以是**某个迭代器位置上的元素**、等于**某键值的元素**、**一个区间上的元素和清空集**合。

```C++
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> s;

    s.insert(8); // 第一次插入8
    s.insert(1);
    s.insert(12);
    s.insert(6);
    s.insert(8); //第二次插入8,重复元素不会插入

    //删除键值为6的元素
    s.erase(6);

    //中序遍历集合中的元素
    set<int>:: reverse_iterator it;
    for(it = s.rbegin(); it != s.rend(); it++)
    {
        cout << *it << " ";
    }
    cout << endl;

    s.clear();
    cout << s.size() << endl;


    return 0;
}
```

运行结果：

12 8 1 
0



**4  元素的检索**

使用 **find（）方法对集合进行搜索，如果找到查找的键值，则返回*<u>该键值的迭代器位置，</u>*否则，返回集合最后一个元素后面的一个位置，即 end（）**。

```C++
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> s;

    s.insert(8);
    s.insert(1);
    s.insert(12);
    s.insert(6);
    s.insert(8);
    s.insert(10);

    set<int>::iterator it;
    it = s.find(6);
    if(it != s.end())
        cout << *it << endl;
    else
        cout << "not find it!" << endl;

    it = s.find(20);
    if(it != s.end())
        cout << *it << endl;
    else
        cout << "not find it!" << endl;
    
    return 0;
}
```

运行结果：

6
not find it!



**5  自定义比较函数**

**使用 insert（）将元素插入到集合中去的时候，集合会根据设定的比较函数将该元素放到该放的节点上去**。在定义集合的时候，如果没有指定比较函数，那么采用**默认的比较函数，即按键值由小到大的顺序插入元素**。在很多情况下，需要自己编写比较函数。

编写比较函数有两种方法。
（1）如果元素不是结构体，那么，可以编写比较函数。下面这个程序编写的比较规则是要求按键值由大到小的顺序将元素插入到集合中∶

```C++
#include <iostream>
#include <set>
using namespace std;

//自定义比较函数myComp，重载“（）”操作符
struct myComp
{
    bool operator()(const int &a, const int &b)
    {
        if(a != b)
            return a > b;
        else
            return a > b;
    }
};

int main()
{
    set<int,myComp> s;  //采用比较函数是myComp

    s.insert(8);
    s.insert(1);
    s.insert(12);
    s.insert(6);
    s.insert(8);
    s.insert(10);

    set<int,myComp>::iterator it;
    for(it = s.begin(); it != s.end(); it++)
    {
        cout << *it <<" ";
    }

    cout << endl;
    return 0;
}
```

运行结果

12 8 61

（2）如果元素是结构体，那么，可以直接把比较函数写在结构体内。

```C++
#include <iostream>
#include <set>
#include <string>
using namespace std;

//自定义比较函数myComp，重载“（）”操作符
struct Info
{
    string  name;
    float   score;
    bool operator < (const Info &a) const    //重载“<”操作符，自定义排序规则
    {
         return a.score < score; //按score由大到小排列。如果要由小到大排列，使用">"号即可。
    }
};

int main()
{
    set<Info> s;  //采用比较函数是myComp

    Info info;
    info.name = "jack";
    info.score = 80.5;
    s.insert(info);
    info.name = "Tomi";
    info.score = 20.5;
    s.insert(info);
     info.name = "Nacyk";
    info.score = 60.5;
    s.insert(info);
     info.name = "jimk";
    info.score = 70.5;
    s.insert(info);
    info.name = "kati";
    info.score = 82;
    s.insert(info);
    info.name = "rack";
    info.score = 74.5;
    s.insert(info);
   

    set<Info>::iterator it;
    for(it = s.begin(); it != s.end(); it++)
    {
        cout << it->name <<" " << it->score << endl;
    }

    cout << endl;
    return 0;
}
```

