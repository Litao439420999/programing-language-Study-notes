# bitset位集合容器



bitset 容器是**一个 bit 位元素的序列容器，每个元素只占一个 bit 位，取值为0或1**，因而很节省内存空间。下图是一个bitset的存储示意图，它的10个元素只使用了两个字节的空间。

![](H:\迅雷云盘\云盘缓存\2022-07-15 145100.png)


使用bitset，需要声明头文件包含语句“#include <bitset>”。
bitset类提供的方法见下表。

![](H:\迅雷云盘\云盘缓存\2022-07-15 145555.png)

## 1  创建 bitset 对象

**创建bitset对象时，必须要指定容器的大小**。bitset对象的大小一经定义，就不能修改了。下面这条语句就定义了bitset对象b，它能容纳100000个元素，即100000个bit（位），此时，所有元素的值都为0。
bitset<100000>    b；



## 2  设置元素值

（1） 采用下标法

```C++
#include <bitset>
#include <iostream>
using namespace std;

int main()
{
    bitset<10> b;
    //采用下标法给元素赋值
    b[1] = 1;
    b[6] = 1;
    b[9] = 1;
    
    //用下标法输出所有元素，第0位是最低位，第9位是最高位
    int i;
    for(i = b.size() - 1; i >= 0; i--)
        cout << b[i] << " ";
    cout << endl;
    return 0;
}
```

运行结果：

1 0 0 1 0 0 0 0 1 0 



（2）用set()方法，一次性将元素设置为1

```C++
#include <bitset>
#include <iostream>
using namespace std;

int main()
{
    bitset<10> b;
   
    //采用set()方法，一次性设置为1
    b.set();

    for(int i = b.size() - 1; i >= 0; i--)
        cout << b[i] << " ";
    cout << endl;
    return 0;
}
```

运行结果：

1 1 1 1 1 1 1 1 1 1 



（3）采用set(pos)方法，将某pos位设置为1。

```C++
#include <bitset>
#include <iostream>
using namespace std;

int main()
{
    bitset<10> b;
    
    //采用set(pos)方法，将某pos位置元素设置为1
    b.set(1,1);
    b.set(6,1);
    b.set(9,1);

    for(int i = b.size()-1; i >=0 ;i--)
        cout << b[i] << " ";
    cout << endl;

    return 0;
}
```

运行结果：

1 0 0 1 0 0 0 0 1 0 



（4）采用reset(pos)，将某pos位置设置为0

```C++
#include <bitset>
#include <iostream>
using namespace std;

int main()
{
    bitset<10> b;
    b.set() ; //将所有位设置为1

    b.reset(0);
    b.reset(2);
    b.reset(3);
    b.reset(4);
    b.reset(5);
    b.reset(7);
    b.reset(8);

    for(int i = b.size()-1; i >= 0; i--)
        cout << b[i] << " ";
    cout << endl;

    return 0;
}
    
```

运行结果：

1 0 0 1 0 0 0 0 1 0 



## 3  输出元素

（1） 采用下标输出元素，见前面示例。

（2）直接向输出流输出全部元素。

```C++
#include <bitset>
#include <iostream>
using namespace std;

int main()
{
    bitset<10> b;
    b.set() ; //将所有位设置为1

    b.reset(0);
    b.reset(2);
    b.reset(3);
    b.reset(4);
    b.reset(5);
    b.reset(7);
    b.reset(8);

   cout << b  << endl;  //直接向输出流输出全部元素

    return 0;
}
    
```

运行结果：

1001000010



