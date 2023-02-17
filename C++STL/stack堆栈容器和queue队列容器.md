# stack堆栈容器和queue队列容器



## 1 stack堆栈容器

stack堆栈是一个后进先出（LastIn First Out，LIFO）的线性表，插入和删除元素都只能在表的一端进行。插入元素的一端称为栈顶（StackTop），而另一端则称为栈底（Stack Bottom）。插入元素叫入栈（Push），元素的删除则称为出栈（Pop）。下图是堆栈示意图。



![](H:\迅雷云盘\云盘缓存\2022-07-15 153234.png)



要使用stack，必须声明头文件包含语句"#include<stack>"。


堆栈的使用方法
堆栈只提供入栈、出栈、栈顶元素访问和判断是否为空等几种方法。
采用push（）方法将元素入栈；采用pop（）方法出栈；采用top（）方法访问栈顶元素；采用empty（）方法判断堆栈是否为空，如果是空的，则返回逻辑真，否则返回逻辑假。当然，可以采用size（）方法返回当前堆栈中有几个元素。

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

tack top:4

stack size:4

stack empty:0

4 3 2 1 



## 2 queue队列容器

queue 队列容器是一个先进先出（First In First Out，FIFO）的线性存储表，元素的插入只能在队尾，元素的删除只能在队首。下图是queue 队列容器数据结构示意图。

![](H:\迅雷云盘\云盘缓存\2022-07-15 155507.png)

使用queue需要声明头文件包含语句“#include <queue>”。
queue 队列的使用方法
queue 队列具有入队 push（）（即插入元素）、出队 pop（）（即删除元素）、读取队首元素 front（）、读取队尾元素 back（）、判断队列是否为空 empty（）和队列当前元素的数目 size（）这几种方法。



```C++
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<int> q;
    
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(9);

    cout << q.size() << endl;
    cout << q.empty() << endl;

    cout << q.front() << endl ; //取队首元素
    cout << q.back() << endl;   //取队尾元素

    while(q.empty()!= true)
    {
        cout << q.front() << " ";
        q.pop();
    }

    cout << endl;
    return 0;
}
```

运行结果：

4

0

1

9

1 2 3 9 

