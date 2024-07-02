**typedef关键字(C)**

<https://c.biancheng.net/view/298.html>

用途：定义自己习惯的数据类型名称，来替代系统默认的基本类型名称、数组类型名称、指针类型名称与用户自定义的结构型名称、共用型名称、枚举型名称等。

```c
// 用法一：为基本数据类型定义新的类型名
// typedef + 原名称 + 新名称
typedef unsigned int size_t;
typedef long double REAL;

// 为数组定义简洁的类型名称
typedef int INT_ARRAY_100[100];
INT_ARRAY_100 arr;

// 用法二：为自定义数据类型定义简洁的的类型名
struct tagPoint
{
    double x;
    int y;
};
struct tagPoint p1; // 标准定义法。C语言定义必须保留struct,C++不必。
typedef struct tagPoint Point; // 所以为了便捷，我们为这个结构体起个别名，于是就能Point p1;直接定义了。

// 以上这2步，等于下面直接起别名。(大部分c语言项目链表的用法)
typedef struct tagPoint
{
    double x;
    int y;
    struct tagPoint *next; //不能用Point,因为此时Point还未定义
} Point;
Point p2; // 可直接使用

// 另一种用法：
struct tagNode
{
    char *pItem;
    struct tagNode *pNext;
};
typedef struct tagNode* pNode;  // 这里定义一个名称pNode，表示tagNode类型的指针变量。
pNode mypoint;   // mypoint是一个tagNode指针。


// 用法三：复杂变量声明。
int *(*a[5])(int,char*); // 分析：首先这是定义了一个有5个元素的数组，数组元素都是指向函数的指针，函数接受一个int类型和一个char类型指针参数，函数的返回值是一个int类型的指针。

// 对于上面这个变量，可以对一个函数指针其别名，然后定义函数指针数组：
typedef int *(*PFun)(int,char*);
PFun a[5];

// 使用例：
int ADD(callback p, int a, int b){
    return  p(a,b);
}
typedef void (*Fun)();  //定义一个函数指针类型变量类型 Fun  

```

**转义字符**

转义字符

意义

ASCII码值（十进制）

\\a

响铃(BEL)

007

\\b

退格(BS) ，将当前位置移到前一列

008

\\f

换页(FF)，将当前位置移到下页开头

012

\\n

换行(LF) ，将当前位置移到下一行开头

010

\\r

回车(CR) ，将当前位置移到本行开头

013

\\t

水平制表(HT) （跳到下一个TAB位置）

009

\\v

垂直制表(VT)

011

\\\\

代表一个反斜线字符''\\'

092

\\'

代表一个单引号（撇号）字符

039

\\"

代表一个双引号字符

034

\\?代表一个问号063

\\0

空字符(NUL)

000

\\ddd

1到3位八进制数所代表的任意字符

三位八进制

\\xhh

1到2位十六进制所代表的任意字符

二位十六进制

注意：区分，斜杠："/" 与 反斜杠："\\"

**volatile关键字**

TODO

<https://bbs.huaweicloud.com/blogs/292866>

<https://blog.csdn.net/tigerjibo/article/details/7427366>

**C语言可变参数**

<https://www.cnblogs.com/zhaobinyouth/p/8781915.html>

va\_list va\_start() va\_end

带可变参数的函数由来...

当函数中的参数个数不确定时，这时候就需要带可变参数的函数！

```c
// 如printf
int   printf(   const   char*   format,   ...);
它除了有一个参数format固定以外,后面跟的参数的个数和类型是可变的。例如我们可以有以下不同的调用方法：

printf( "%d ",i);   
printf( "%s ",s);   
printf( "the   number   is   %d   ,string   is:%s ",   i,   s);   

```