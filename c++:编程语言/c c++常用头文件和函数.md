```c
C/C++头文件一览
================================================
=====================  c  =====================
================================================
#include <stdio.h>　　　　 //定义输入／输出函数
#include <stdlib.h>　　　　//定义杂项函数及内存分配函数
#include <string.h>　　　　//字符串处理
#include <errno.h>　　　　 //定义错误码
#include <time.h>　　　　　//定义关于时间的函数
#include <unistd.h>        //进程控制,sleep
// unistd.h是unix std的意思，是POSIX标准定义的unix类系统定义符号常量的头文件，包含了许多UNIX系统服务的函数原型，例如read函数、write函数和getpid函数。
#include <pthread.h>

#include <assert.h>　　　　//设定插入点
#include <ctype.h>　　　　 //字符处理
#include <float.h>　　　　 //浮点数处理
#include <iso646.h>        //对应各种运算符的宏
#include <limits.h>　　　　//定义各种数据类型最值的常量
#include <locale.h>　　　　//定义本地化C函数
#include <math.h>　　　　　//定义数学函数
#include <setjmp.h>        //异常处理支持
#include <signal.h>        //信号机制支持
#include <stdarg.h>        //不定参数列表支持
#include <stddef.h>        //常用常量
#include <wchar.h>　　　　 //宽字符处理及输入／输出
#include <wctype.h>　　　　//宽字符分类


================================================
===================== c++ =====================
================================================
#include <iostream>        //输入输出流
#include <fsteram>         //C++ STL中对文件操作的合集
#include <algorithm>       //基于迭代器的非成员模版函数。
    max()
    min()
    swap()
    reverse()
    sort()
#include <thread>          //C++11

```

\<stdio.h\>

int ferror(FILE \*stream);

ferror，函数名，在调用各种输入输出函数（如 putc.getc.fread.fwrite等）时，如果出现错误，除了函数[返回值](https://baike.baidu.com/item/%E8%BF%94%E5%9B%9E%E5%80%BC/9629649)有所反映外，还可以用ferror函数检查。 它的一般调用形式为 ferror(fp)；如果ferror返回值为0（假），表示未出错。如果返回一个非零值，表示出错。应该注意，对同一个文件 每一次调用输入输出函数，均产生一个新的ferror函 数值，因此，应当在调用一个输入输出函数后立即检 查ferror函数的值，否则信息会丢失。在执行[fopen](https://baike.baidu.com/item/fopen/10942321)函数时，ferror函数的初始值自动置为0。

fread结束的问题 <https://blog.csdn.net/sunshineyy85/article/details/7901356>

popen

```c
int atoi(const char *str)
```

\#include \<algorithm\> // c++

```c
// reverse()
vector<int> v = {5,4,3,2,1};
reverse(v.begin(),v.end());//v的值为1,2,3,4,5

string str="www.mathor.top";
reverse(str.begin(),str.end());//str结果为pot.rohtam.wwww


// sort()
sort(v.begin(),v.end())
sort(v.begin(),v.end(), cmpfunction);
```