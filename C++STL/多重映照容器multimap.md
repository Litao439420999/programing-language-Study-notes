# 多重映照容器multimap

​		

​		multimap与map 基本相同，唯独不同的是，***multimap 允许插入重复键值的元素。由于允许重复键值存在***，所以，multimap 的元素插入、删除、查找都与 

map 不相同。要使用multimap，则需要头文件包含语句"***#include<map>***"。



## 1  multimap 对象创建、元素插入



可以重复插入元素，插入元素需要使用 insert（）方法。



```c++
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main()
{
    multimap<string,double> m;
    m.insert(pair<string,double>("Jack",300.5));
    m.insert(pair<string,double>("Kity",200));
    m.insert(pair<string,double>("Memi",500));

    //重复插入键值"Jack"
    m.insert(pair<string,double>("Jack",306));

    multimap<string,double>:: iterator it;
    for(it = m.begin(); it !=m.end(); it++)
        cout << it->first << ":" << it->second << endl;
    return 0;
}
```

运行结果：

Jack:300.5

Jack:306

Kity:200

Memi:500





## 2  元素的删除

删除操作采用erase（）方法，可删除某个迭代器位置上的元素、等于某个键值的所有重复元素、一个迭代器区间上的元素。使用 clear（）方法可将multimap 容



器中的元素清空。**因为有重复的键值，所以，删除操作会将要删除的键值一次性从 multimap 中删除**。



```C++
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main()
{
    multimap<string,double> m;
    m.insert(pair<string,double>("Jack",300.5));   //注意这里
    m.insert(pair<string,double>("Kity",200));
    m.insert(pair<string,double>("Memi",500));

    //重复插入键值"Jack"
    m.insert(pair<string,double>("Jack",306));

    multimap<string,double>:: iterator it;
    for(it = m.begin(); it !=m.end(); it++)
        cout << it->first << ":" << it->second << endl;


    m.erase("Jack"); //删除键值为“Jack”元素
    cout << "the elements after deleted: " << endl;
    for(it = m.begin(); it !=m.end(); it++)
        cout << it->first << ":" << it->second << endl;


    return 0;
}
```

运行结果：

Jack:300.5

Jack:306

Kity:200

Memi:500

the elements after deleted:

Kity:200

Memi:500



## 3  元素的查找

由于 multimap 存在重复的键值，所以 ***find（）方法只返回重复键值中的第一个元素的迭代器位置，如果没有找到该键值，则返回 end（）迭代器位置***。



```C++
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main()
{
    multimap<string,double> m;
    m.insert(pair<string,double>("Jack",300.5));   //注意这里
    m.insert(pair<string,double>("Kity",200));
    m.insert(pair<string,double>("Memi",500));

    //重复插入键值"Jack"
    m.insert(pair<string,double>("Jack",306));

    multimap<string,double>:: iterator it;
    for(it = m.begin(); it !=m.end(); it++)
        cout << it->first << ":" << it->second << endl;
    
    cout << "the search result:" << endl;
    it = m.find("Jack");

    if(it != m.end())
        cout << it ->first << ":" << it ->second << endl;
    else
        cout << "not find it!\n";
    
    it = m.find("Nacy");
    if(it != m.end())
        cout << it ->first << ":" << it ->second << endl;
    else
        cout << "not find it!\n";
    
    return 0;
}
```

运行结果：

Jack:300.5

Jack:306

Kity:200

Memi:500

the search result:

Jack:300.5

not find it!