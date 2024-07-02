C语言和C++的区别

===========

**

<https://blog.csdn.net/czc1997/article/details/81254971>

**

#### memset函数
在C中 <string.h>
在C++中貌似不需要其他头文件，或 cstring ？

原型：void *memset(void *s,int c,size_t n)

总的作用：将已开辟内存空间s的首n个字节的值设为值c。（void指针可以指向任意类型的数据，就是说可以用任意类型的指针对void*这个指针赋值）
如：
```
char *s="Golden Global View";
memset(s,'G',6);

char str[100];
memset(str,0,100);//常用于内存空间初始化
```
//赋值：int*可以赋给void*，反之不行
**技巧：memset可以方便的清空一个结构类型的变量或数组。**
如：
```
struct sample_struct
{
    char csName[16];
    int iSeq;
    int iType;
};
struct sample_strcut stTest;
memset(&stTest,0,sizeof(struct sample_struct));
```

  
###  malloc/free  new/delete
  * malloc/free只是动态分配内存空间/释放空间。而new/delete除了分配空间还会调用构造函数和析构函数进行初始化与清理（清理成员）
  * 它们都是动态管理内存的入口。
  * malloc/free是C/C++标准库的函数，new/delete是C++操作符。
  * malloc/free需要手动计算类型大小且返回值w为void*，new/delete可自动计算类型的大小，返回对应类型的指针。
  * malloc/free管理内存失败会返回0，new/delete等的方式管理内存失败会抛出异常。

#### malloc函数（动态内存分配）
原型：void *malloc(size_t size)
```
int *p;
p = (int*)malloc(sizeof(int) * 128);
//分配128个（可根据实际需要替换该数值）整型存储单元。在堆上分配了100个字节内存，返回这块内存的首地址，把地址强制转换成int *类型后赋给int *类型的指针变量p。
``` 
#### free函数
free函数：斩断指针变量与这块内存的关系。
程序中malloc的使用次数一定要和free相等。

free函数之后指针变量p本身保存的地址并没有改变，那我们就需要重新把p的值变为NULL，否则是野指针.

#### new[]和delete[]xx配套，new和delete

int* ptr = new int(10);
int* arr = new int[5];
int* arr = new int[5]{1, 2, 3, 4, 5};
delete[] arr;

#### snprintf()函数
原型：
```
int snprintf(char* dest_str,size_t size,const char* format,...);
```
函数功能：先将可变参数“…”按照format的格式格式化为字符串，然后再将其拷贝至dest_str中。  

注意事项：如果格式化后的字符串长度小于size，则将字符串全部拷贝至dest_str中，并在字符串结尾处加上‘\0’； 
如果格式化后的字符串长度大于或等于size，则将字符串的(size-1)拷贝至dest_str中，然后在字符串结尾处加上’\0’. 
函数返回值是 格式化字符串的长度。
如1：
snprintf(str.data,str.len,"hello");
如2：
```
int main(void){  
    char dest_str[1024];  
    memset(dest_str,0,sizeof(dest_str));  

    char *s1 = "Linux C程序设计";  
    int size = strlen(s1);  
    int year = 2017;  
    int month = 9;  
    int day = 8;  

    snprintf(dest_str,sizeof(dest_str),"字符串:%s\n长度是:%d\n今天是:%d年%d月%d日\n",s1,size,year,month,day);  

    printf("%s",dest_str);  

}  
结果：
字符串:Linux C程序设计
长度是:15
今天是:2017年9月8日
```


#### sizeof和strlen等函数注意点
sizeof是操作符，输入参数可以是数据类型，也可以是变量，编译器编译时就计算出sizeof结果，计算出占用内存大小。
strlen是库函数，只能统计字符串，且以'\0'结尾，在程序运行时才计算。

#### strcpy等函数注意点

```c
%d 有符号10进制整数
%i 有符号10进制整数
%o 无符号8进制整数
%u 无符号10进制整数
%x 无符号的16进制数字，并以小写abcdef表示
%X 无符号的16进制数字，并以大写ABCDEF表示
%F/f 浮点数
%E/e 用科学表示格式的浮点数
%g 使用%f和%e表示中的总的位数表示最短的来表示浮点数 G 同g格式，但表示为指数
%c 单个字符
%s 字符串


```

####C/C++结构体的区别

1.C的结构体内不允许有函数存在，C++允许有内部成员函数，且允许该函数是虚函数。所以C的结构体是没有构造函数、析构函数、和this指针的。
2.C的结构体对内部成员变量的访问权限只能是public，而C++允许public,protected,private三种。
3.C语言的结构体是不可以继承的，C++的结构体是可以从其他的结构体或者类继承过来的。
4.在C中定义一个结构体类型要用typedef，如下：
typedef struct Complex{
　　int read;
　　int image;
}Complex;
于是才能这样定义：
Complex complex;
否则若就只能：
struct Complex complex;



## 杂
可以用转义序列
printf("\"");输出"
printf("\'");输出'
printf("\\");输出\

* c语言没有bool类型和true与false
* c语言

### c与c++的代码风格
  c的命名习惯是蛇形，下划线形
  c++是驼峰型

**高级区别内容**

**函数符号名称**

C++使用了名称修饰（Name Mangling）来处理函数重载和方法重载(C不支持)。这意味着C++编译器会在编译时为函数和方法生成唯一的名称，以区分它们。

这也意味着C++编译后的符号名称可能会包含参数类型信息等，与C语言的函数名称不同。

**extern "C" **

如果你要在C++中调用C语言编写的函数，需要使用 extern "C" 声明来告诉C++编译器使用C语言的名称修饰规则。

这可以确保C++编译器不会对C语言函数的名称进行修饰。

```c

```