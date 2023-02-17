# C语言——有关指针





### 1.指针常量（常指针）

**指针常量**意指 "类型为指针的常量"，**初始化后不能被修改，固定指向某个内存地址**。我们***⽆法修改指针⾃⾝的值，但可以修改指针所指目标的内容***。

举例：

```c
#include <stdio.h>

int main()
{
    int x[] = {1, 2, 3, 4, 5};
    int *const p = x; //常指针

    for(int i = 0; i < 5; i++)
    {
        int v = *(p + i);
        *(p + i) = ++v;

        printf("%d\n",v);

        // p++; 编译出错，为什么？
    }

    return 0;

}
```

本例中的指针 p 始终指向数组 x 的第⼀个元素，是个常指针，和数组名 x 作⽤相同。由于指针本⾝是常量，⾃然⽆法执⾏ p++、++p 之类的操作，否则会导致编译错误。



### 2. 常量指针

**常量指针**是说 "指向常量数据的指针"，***指针目标被当做常量处理 (尽管原目标不⼀定是常量)，不能⽤通过指针做赋值处理。指针⾃⾝并⾮常量，可以指向其他位置，但依然不能做赋值操作。***

举例：

```c
#include <stdio.h>

int main(void)
{
    int x = 1, y = 2;

    const int *p = &x; //定义常量指针
    //*p = 100; 编译出错

    p = &y;
    printf("%d\n",*p);
    // *p = 100; 
    
    return 0;
}
```

⼏种特殊情况：

- 下⾯的代码据说在 VC 下⽆法编译，但 GCC 是可以的。

  ```C
  const int x = 1;
  int* p = &x; 
  printf("%d\n", *p);
  *p = 1234; 
  printf("%d\n", *p);
  ```

- const int* p 指向 const int ⾃然没有问题，但肯定也不能通过指针做出修改。

  ```C 
  const int x = 1;
  const int* p = &x;
  printf("%d\n", *p);
  *p = 1234;  // Compile Error!
  ```

- 声明指向常量的指针常量，这很罕⻅，但也好理解。

  ```C
  int x = 10;
  const int* const p = &i;
  p++;  // Compile Error!
  *p = 20; // Compile Error!
  ```

区别指针常量和常量指针⽅法很简单：**看 const 修饰的是谁，也就是 * 在 const 的左边还是右边。**

-  int* const p: const 修饰指针变量 p，指针是常量。

-  int const *p: const 修饰指针所指向的内容 *p，是常量的指针。或写成 const int *p。*

- const int* const p: 指向常量的指针常量。右 const 修饰 p 常量，左 const 表明 *p 为常量。

  

### 3. 指针的指针

指针本⾝也是内存区的⼀个数据变量，⾃然也可以⽤其他的指针来指向它。

举例：

```C 
#include <stdio.h>

int main(void)
{
    int x = 10;
    int *p = &x;
    int **p2 = &p;

    printf("p = %p, *p =%d\n",p,*p);
    printf("p2 = %p, *p2 = %x\n",p2,*p2);
    printf("x = %d,%d\n",*p,**p2);

    return 0;
}
```

结果为：

```
p = 000000000061FE14, *p =10
p2 = 000000000061FE08, *p2 = 61fe14
x = 10,10
```

可以发现 p2 存储的是指针 p 的地址。因此才有了指针的指针⼀说。



### 4. 数组指针

默认情况下，***数组名为指向该数组第⼀个元素的指针常量***。

```C
int x[] = { 1, 2, 3, 4 };
int* p = x;
for (int i = 0; i < 4; i++)
{
 	printf("%d, %d, %d\n", x[i], *(x + i), , *p++); 
}
```

尽管我们可以⽤* (x + 1) 访问数组元素，但不能执⾏ x++ / ++x 操作。但 **"数组的指针" 和数组名并不是⼀个类型，数组指针将整个数组当做⼀个对象，⽽不是其中的成员(元素)。**

```C
int x[] = { 1, 2, 3, 4 }; 
int* p = x;
int (*p2)[] = &x; // 数组指针
for(int i = 0; i < 4; i++)
{
 	printf("%d, %d\n", *p++, (*p2)[i]);
}
```

详情参考《数组指针》。

### 5. 指针数组

**元素类型为指针的数组称之为指针数组。**

```C
int x[] = { 1, 2, 3, 4 };
int* ps[] = { x, x + 1, x + 2, x + 3 };
for(int i = 0; i < 4; i++)
{
 	printf("%d\n", *(ps[i])); 
}
```

**x 默认就是指向第⼀个元素的指针，那么 x + n ⾃然获取后续元素的指针。**

指针数组通常⽤来处理交错数组 (Jagged Array，⼜称数组的数组，不是⼆维数组)，最常⻅的就是字符串数组了。

举例说明：

```C
#include <stdio.h>

void test(const char **x, int len)
{
    for(int i = 0; i < len; i++)
    {
        printf("test:%d = %s\n",i, *(x + i));
    }
}

int main(void)
{
    char a[] = "aaa",b[] = "bbb"; //这里要注意
   
    const char* ss[] = {a,b};

    for(int i= 0; i < 2; i++)
    {
        printf("%d = %s\n",i,ss[i]);
    }

    test(ss,2); //这里要注意传参的类型

    return 0;
}
```

详情参考后续《指针数组》。

### 6. 函数指针

**默认情况下，函数名就是指向该函数的指针常量。**

举例：

```c
#include <stdio.h>

void inc(int *x)
{
    *x += 1;
}

int main(void)
{
    void (*f)(int *) = inc;
    int i = 100;

    f(&i);
    printf("%d\n",i);

    return 0;

}
```

如果嫌函数指针的声明不好看，可以定义⼀个函数指针类型。

举例：

```C
#include <stdio.h>

void inc(int *x)
{
    *x += 1;
}

typedef void (*inc_t)(int*); // 定义一个函数指针类型

int main(void)
{
    inc_t f= inc; 
    int i = 100;

    f(&i);
    printf("%d\n",i);

    return 0;

}
```

**注意:**

```C 
#include <stdio.h>

void test()
{
    printf("test!\n");
}

typedef void (func_t)(); //定义函数类型
typedef void (*func_ptr_t)(); //定义函数指针类型

int main(void)
{
    func_t* f = test;
    func_ptr_t p = test;

    f();
    p();

    return 0;
}
```

