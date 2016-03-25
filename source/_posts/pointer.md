---
title: 指针
date: 2016-03-10 23:00:19
tags:
---
<h2 align = "center">1.指针</h2>

`指针类型`（pointer type）可由函数类型、对象类型或不完全的类型派生，派生指针类型的类型称为引用类型。指针类型描述一个对象，该类对象的值提供对该引用类型实体的引用。由引用类型 T 派生的指针类型有时称为“（指向）T 的指针”。从引用类型构造指针类型的过程称为“指针类型的派生”。这些构造派生类型的方法可以递归地应用。
### 1.1 ###
`[ ]`比`*`优先级高.

`int *p[10];`先看`p[10]`，所以`p`是数组,数组的每一个元素都是指针变量,int型的指针变量.
`int (*q)[10];`同上，`q`是指针,指向数组,int [10]的数组.

```c
# include"stdio.h"

int main(void)
{

    int *p[10];
    int (*q)[10];
    printf( "*p[10]:%d\n ", sizeof(p));
    printf( "(*q)[10]:%d\n ", sizeof(q));

    return 0;

}
```

输出:

```
*p[10]:40
(*q)[10]:4
```

###1.2 指针的值

```c
#include <stdio.h>

int main(void)
{
    int     hoge = 5;
    int     piyo = 10;
    int     *hoge_p;

    /*输出每个变量的地址*/
    printf("&hoge..%p\n", &hoge);
    printf("&piyo..%p\n", &piyo);
    printf("&hoge_p..%p\n", &hoge_p);

    /*将hoge 的地址赋予hoge_p*/
    hoge_p = &hoge;
    printf("hoge_p..%p\n", hoge_p);

    /*通过hoge_p 输出hoge 的内容*/
    printf("*hoge_p..%d\n", *hoge_p);

    /*通过hoge_p 修改hoge 的内容*/
    *hoge_p = 10;
    printf("hoge..%d\n", hoge);

    return 0;
}
```

输出:
```
&hoge..0028FEBC
&piyo..0028FEB8
&hoge_p..0028FEB4
hoge_p..0028FEBC
*hoge_p..5
hoge..10
```
### 1.3 空指针
```c
#include <stdio.h>

int main(void)
{
    int hoge = 5;
    void *hoge_p;

    hoge_p = &hoge;    // ←这里不报错
    printf("%d\n", *(int*)hoge_p); //打印输出hoge_p 指向的变量的值

    return 0;
}
```
输出

```
5
```

### 1.4 指针的加减运算

```c
#include <stdio.h>

int main(void)
{
    int hoge;
    int *hoge_p;
    /*将指向hoge 的指针赋予hoge_p */
    hoge_p = &hoge;
    /*输出hoge_p 的值*/
    printf("hoge_p..%p\n", hoge_p);
    /*给hoge_p 加1*/
    hoge_p++;
    /*输出hoge_p 的值*/
    printf("hoge_p..%p\n", hoge_p);
    /*输出hoge_p 加3 后的值*/
    printf("hoge_p..%p\n", hoge_p + 3);

    return 0;
}
```

输出:

```
hoge_p..0028FEB8
hoge_p..0028FEBC    
hoge_p..0028FEC8
```
### 1.5 数组的地址
```c
#include <stdio.h>

int main (void)
{
    int array[5];
    int i;

    for (i = 0; i < 5; i++)
        array[i] = i;

    for (i = 0; i < 5; i++)
        printf ("%d\n", array[i]);

    for (i = 0; i < 5; i++ )
        printf ("&array[%d]... %p\n", i, &array[i]);
}
```

输出:

```
0
1
2
3
4
&array[0]... 0028FEA8
&array[1]... 0028FEAC
&array[2]... 0028FEB0
&array[3]... 0028FEB4
&array[4]... 0028FEB8
```
可以改成:

```
#include <stdio.h>

int main (void)
{
    int array[5];
    int *p;
    p = array;
    int i;

    for (i = 0; i < 5; i++)
        array[i] = i;

    for (i = 0; i < 5; i++)
        printf ("%d\n", array[i]);

    for (i = 0; i < 5; i++ )
        printf ("&array[%d]... %p\n", i, &i[array]);
}
```

因为`*(p+i)`等于`array[i]`等于`p[i]`,`p+i`等于`i+p`,
所以`*(p+i)`等于`*(i+p)`等于`i[p]`等于`i[array]`.
总结:
`*array[i]`是`*(array+i)`的简单写法.是为了人类容易理解而引入的功能,俗称语法糖(syntax sugar).
数组的传递不同写法.

```
int func(int *a);	//写法1
int func(int a[]);   //写法2
int func(int a[10]); //写法3
```
