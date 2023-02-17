# map映照容器

map 映照容器的元素数据是由***一个键值***和***一个映照数据组成的***，**键值与映照数据之间具有一一映照的关系**。

**map 映照容器的数据结构也是采用红黑树来实现的**，**插入元素的键值不允许重复，比较函数只对元素的键值进行比较**，元素的各项数据可通过键值检索出来。由于 map 与set 采用的都是红黑树的数据结构，所以，用法基本相似。



| 键值Name | 映照数据Score |
| :------: | :-----------: |
|   Jack   |     98.5      |
|   Bomi   |     96.0      |
|   Kate   |     97.5      |

使用 map 容器需要头文件包含语句"#include <map>"。map 文件也包含了对 multimap 多重映照容器的定义。



## 1 map创建、元素插入和遍历访问



**创建 map 对象，键值与映照数据的类型由自己定义。在没有指定比较函数时，元素的插入位置是按键值由小到大插入到黑白树中去的，这点和 set 一样**。

```c++
#include <map>
#include <string>
#include <iostream>
using namespace std;

int main()
{
     map<string,float> m;   
     m["Jack"] = 98.5;
     m["Bomi"] = 96.0;
     m["Kate"] = 97.5;

     //遍历元素
     map<string,float>:: iterator it;
     for(it = m.begin(); it != m.end(); it++)
        cout << it->first << ":"  << it -> second  << endl;   //注意：first代表键，second代表值
    return 0; 
}

```

运行结果：

Bomi:96
Jack:98.5
Kate:97.5

程序编译时，会产生代号为"warning C4786"的警告，"4786"是标记符超长警告的代号。***可以在程序的头文件包含代码的前面使用“#pragma warning（disable∶4786）"宏语句，强制编译器忽略该警告。4786号警告对程序的正确性和运行并无影响***。



## 2  删除元素

与set 容器一样，**map 映照容器的 erase（）删除元素函数，可以删除某个迭代器位置上的元素、等于某个键值的元素、一个迭代器区间上的所有元素，当然，也可使用clear（）方法清空map映照容器。**



```C++
#include <map>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    map<int,char> m;  //插入元素，按键值的由小到大存入黑白树中

    m[25] = 'm';
    m[28] = 'k';
    m[10] = 'x';
    m[30] = 'a';
   
    map<int,char>:: iterator  it;
    for(it = m.begin(); it != m.end(); it++)
    {
        cout << it->first << ":" << it -> second  << endl;
    }
    cout << " 删除后数据:" << endl;
    m.erase(28);
    for(it = m.begin(); it != m.end(); it++)
    {
        cout << it->first << ":" << it -> second  << endl;
    }

    return 0;

}
```

运行结果：

10:x
25:m
28:k
30:a
 删除后数据:
10:x
25:m
30:a



## 3  元素反向遍历



可以使用反向迭代器reverse iterator反向遍历 map照映容器中的数据，它需要 rbegin（）方法和 rend（）方法指出反向遍历的起始位置和终止位置。



```c++
#include <map>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    map<int,char> m;  //插入元素，按键值的由小到大存入黑白树中

    m[25] = 'm';
    m[28] = 'k';
    m[10] = 'x';
    m[30] = 'a';
   
    map<int,char>:: reverse_iterator rit;
    for(rit = m.rbegin(); rit != m.rend(); rit++)
    {
        cout << rit->first << ":" << rit -> second  << endl;
    }
  
    return 0;

}
```

运行结果：

30:a
28:k
25:m
10:x



## 4  元素的搜索

使用 find（）方法来搜索某个键值，***如果搜索到了，则返回该键值所在的迭代器位置，否则，返回 end（）迭代器位置***。由于map 采用黑白树数据结构来实现，所以搜索速度是极快的。

```C++
#include <map>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    map<int,char> m;  //插入元素，按键值的由小到大存入黑白树中

    m[25] = 'm';
    m[28] = 'k';
    m[10] = 'x';
    m[30] = 'a';
   
   map<int,char>::iterator it;
   it = m.find(28);

    if(it != m.end())
        cout << it ->first << ":" << it->second << endl;
    else
        cout << " not find it\n";
  
    return 0;

}
```

运行结果：

28:k



## 5  自定义比较函数

将元素插入到 map 中去的时候，map 会根据设定的比较函数将该元素放到该放的节点上去。在定义 map 的时候，如果没有指定比较函数，那么采用默认的比较函数，即按键值由小到大的顺序插入元素。在很多情况下，需要自己编写比较函数。编写方法有两种。

（1）如果元素不是结构体，那么，可以编写比较函数。下面这个程序编写的比较规则是要求按键值由大到小的顺序将元素插入到map中∶

```c++
#include <map>
#include <string>
#include <iostream>
using namespace std;

struct myComp
{
    bool operator()(const int &a, const int &b)
    {
        if(a != b) return a > b;
        else
            return  a > b;
    }
};

int main()
{
    map<int,char,myComp> m;  //由大到小
    m[25]  = 'm';
    m[28]  = 'k';
    m[10]  = 'x';
    m[30]  = 'a';

    map<int,char,myComp>:: iterator it;   
    for(it = m.begin(); it != m.end(); it++)
    {
        cout << it ->first << ":" << it -> second << endl;
    }

    return 0;
}
```

运行结果：

30:a
28:k
25:m
10:x

（2）如果元素是结构体，那么，可以直接把比较函数写在结构体内。下面的程序详细说明了如何操作∶

```C++
#include <string>
#include <iostream>
#include <map>
using namespace std;

struct Info
{
    string name;
    float  score;

    bool operator < (const Info &a)const
    {
        return a.score < score;
    }

};

int main()
{
    map<Info,int> m;
    Info info;
    info.name = "Jack";
    info.score = 60;
    m[info] = 25;
   
    info.name = "Bomi";
    info.score = 80;
    m[info] = 10;
    
    info.name = "Peti";
    info.score = 66.5;
    m[info] = 30;

    map<Info,int>:: iterator it;
    for(it = m.begin(); it != m.end(); it++)
    {
        cout << it -> second << ":";
        cout << it ->first.name  << " " << it -> first.score << endl;
    }

    return 0;
}
```

运行结果：

10:Bomi 80
30:Peti 66.5
25:Jack 60



## 6 用 map 实现数字分离



对数字的各位进行分离，采用取余等数学方法操作是很耗时的。而把数字当成字符串，使用 map 的映照功能，很方便地实现了数字分离。下面这个程序将一个字符串中的字符当成数字，并将各位的数值相加，最后输出各位的和。

```C++
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main()
{
    map<char,int> m;
    
    for(int j = 0; j < 10; j++)
        m['0' + j] = j;
    string sa,sb;
    sa = "6234";
    int i;
    int sum = 0;

    for(i = 0; i < sa.length(); i++)
        sum += m[sa[i]];
    cout << " sum =" << sum << endl;

    return 0;

}
```

运行结果：

 sum =15

第二种方式：

```C++
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main()
{
    map<char,int> m;
    m['0'] = 0;
    m['1'] = 1;
    m['2'] = 2;
    m['3'] = 3;
    m['4'] = 4;
    m['5'] = 5;
    m['6'] = 6;
    m['7'] = 7;
    m['8'] = 8;
    m['9'] = 9;

    string sa,sb;
    sa = "6234";
    int i;
    int sum = 0;

    for(i = 0; i < sa.length(); i++)
        sum += m[sa[i]];
    cout << " sum =" << sum << endl;

    return 0;

}
```



## 7 数字映照字符的map 写法



在很多情况下，需要实现将数字映射为相应的字符，看看下面这个程序∶

```c++
#include <map>
#include <string>
#include <iostream>
using namespace std;

int main()
{
    map<int,char> m;

    for(int j = 0; j < 10 ; j++)
        m[j] = '0' + j;
    
    int n = 7;
    string s = "The number is ";
    cout << s + m[n]  << endl;

    return 0;
}
```

运行结果：

The number is 7



题目一：

153是一个非常特殊的数，它等于它的每位数字的立方和，即153=1*1*1+5*5*5+3*3*3。编程求所有满足这种条件的三位十进制数。使用map相关方法。

```c++
#include <iostream>
#include <cstdlib>
#include <string>
#include <cstring>
#include <map>
using namespace std;

int main()
{
    map<char,int> m;
    int num,sum;

    for(int j = 0; j < 10; j++)
        m['0' + j] = j;
    
    for(num = 100; num < 1000; num++)
    {   
        sum = 0;
       char  sn[10] ;
       itoa(num,sn,10);
        for(int i = 0; i < strlen(sn); i++)
          sum +=  m[sn[i]] * m[sn[i]] * m[sn[i]];
        
        if(sum == num)
            cout << num  << endl;
    }

    return 0;
}

```

运行结果：

153
370
371
407



题目二：十六进制转十进制

问题描述
　　从键盘输入一个不超过8位的正的十六进制数字符串，将它转换为正的十进制数后输出。注：十六进制数中的10~15分别用大写的英文字母A、B、C、D、E、F表示。

```C++
#include <iostream>
#include <map>
#include <string>
#include <cmath>
using namespace std;

int main()
{
    map<char,int> m;
    string s;

    for(int i = 0; i < 10; i++)
        m['0' + i] = i;
    
    for(int i = 0; i < 6;i++)
        m['A'+ i] = 10 + i;

   
    
    cin >> s;
    int j,k,sum = 0;
    j = 0; k = s.size()-1;
    
    for(j,k;j < s.size();j++,k--)
    {
       sum += m[s[j]] * pow(16.0,k);
    }
    
    cout << int(sum) << endl;
    return 0;

}


```

运行结果：

输入：FFFF
输出：65535



输入：218
输出：536
