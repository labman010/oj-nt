总：<https://www.cnblogs.com/smiler/p/4457622.html>

**STL概述**：

**std::string**

**std::vector 向量，相当于一个数组**

**std::deque 双端队列**

**std::list 双向链表，非连续空间**

**std::forward\_list 单向链表**

**std::array 固定大小的数组**

**std::map (或unordered\_\*)**

**std::set (或unordered\_\*)**

**std::pair (可使用std::make\_pair()函数)**

---

vector、list、deque使用区别：

1 如果你需要高效的随即存取，而不在乎插入和删除的效率，使用vector 

2 如果你需要大量的插入和删除，而不关心随即存取，则应使用list 

3 如果你需要随即存取，而且关心两端数据的插入和删除，则应使用deque

vector与list的区别：

list封装了链表,vector封装了数组,list和vector得最主要的区别在于vector使用连续内存存储的，他支持[]运算符随机访问，而list是以链表形式实现的，不支持[]。

set和vector的区别在于set不包含重复的数据

```c

```

**map**

**unordered\_map**

优点

有序性，这是map结构最大的优点。

因为内部实现了哈希表，因此其查找速度非常的快。

缺点

空间占用率高，因为map内部实现了红黑树，虽然提高了运行效率，但是因为每一个节点都需要额外保存父节点，孩子节点以及红/黑性质，使得每一个节点都占用大量的空间。

哈希表的建立比较耗费时间。

适用处

对于那些有顺序要求的问题，用map会更高效一些。

对于查找问题，unordered\_map会更加高效一些，因此遇到查找问题，常会考虑一下用unordered\_map

---

**map/unordered\_map/set/unordered\_set底层实现**

 ** unordered\_map/unordered\_set:**

 首先无序容器如 unordered\_map/unordered\_set 是用hash表存储结构的，且使用拉链法解决冲突。

 当使用无序容器存储键值对时，会先申请一整块连续的存储空间，但此空间并不用来直接存储键值对，而是存储各个链表的头指针，各键值对真正的存储位置是各个链表的节点。

 STL中把拉链的各个链表叫做桶（bucket）。

 负载因子 = 容器存储的总键值对 / 桶数 

 默认情况下，无序容器的最大负载因子为 1.0。如果操作无序容器过程中，使得最大复杂因子超过了默认值，则容器会自动增加桶数，并重新进行哈希，以此来减小负载因子的值。需要注意的是，此过程会导致容器迭代器失效，但指向单个键值对的引用或者指针仍然有效。

 (这也就解释了，为什么我们在操作无序容器过程中，键值对的存储顺序有时会“莫名”的发生变动。)

 **map/set:**

 封装了红黑树，树中的每一个节点保存key、value、父节点、子节点等信息。

 貌似构建树排序的话，是直接按key来排序(set按值排序)?

```c

```

**STL通用 (迭代器等)**

**C++ 迭代器**

1) 正向迭代器，定义如：

 vector\<int\>::iterator itr; // 容器类名::iterator 迭代器名;

2) 常量正向迭代器：

  vector\<int\>::const\_iterator itr;

3) 反向迭代器：

  vector\<int\>::reverse\_iterator itr;

4) 常量反向迭代器:

  vector\<int\>::const\_reverse\_iterator itr;

通过迭代器可以读取它指向的元素，\*迭代器名 就表示迭代器指向的元素。

通过非常量迭代器能**修改**其指向的元素，常量迭代器则不行。

迭代器都可以进行++操作。反向迭代器和正向迭代器的区别在于：

 对正向迭代器进行++操作时，迭代器会指向容器中的后一个元素；

 而对反向迭代器进行++操作时，迭代器会指向容器中的前一个元素。

```c
// 与迭代器相关函数：

    // distance返回整数，表示两个迭代器之间的距离，即迭代器 p 经过多少次 + + 操作后和迭代器 q 相等。如果调用时 p 已经指向 q 的后面，则这个函数会陷入死循环。
    std::distance(p, q);

    // next和advance函数都用于得到当前迭代器的下n个迭代器
    auto newit = std::next(itr, number); // next不修改而是返回新迭代器
    std::advance(itr, number);      // advance不返回直接修改旧迭代器



// erase函数的返回值是一个指向被删除元素之后元素的迭代器，如果删除的是最后一个元素，则返回 end() 迭代器。
iterator erase(const_iterator position);
iterator erase(const_iterator first, const_iterator last);



// min_element 比较算法函数，支持普通数据和容器。
    // 定义：
    template< class ForwardIt >
    ForwardIt min_element( ForwardIt first, ForwardIt last );
    // 使用例子：
        int arr[] = { 100, 200, -100, 300, 400 };
        //finding smallest element
        int result = *min_element(arr + 0, arr + 5);
    或
        vector<int> v1{ 10, 20, 30, 40, 50 };
        int result = *min_element(v1.begin(), v1.end());
        
    
```

**std::pair**

```c
std::pair和std::make_pair()

// make_pair无需写出型别， 就可以生成一个pair对象
// 例：
std::make_pair(42, '@');
// 而不必费力写成：
std::pair<int, char>(42, '@')

// 当有必要对一个接受pair参数的函数传递两个值时， make_pair()尤其显得方便，
void f(std::pair<int, const char*>);
void foo {
    f(std::make_pair(42, '@')); //pass two values as pair
}

```

**std::string**

```c
// 在<string>头文件中的函数
int stoi(const std::string& str, std::size_t* pos = nullptr, int base = 10 ); 
std::string to_string(int value); //或double等


// string转字符串的方法
c_str() // 如：const char* p = s.c_str();

// 字符转string
char c = 'x';
string s = string(1,c);

// string对象的成员函数。
substr(num);//返回从num脚标开始的所有字符，包括num角标对应的字符
substr(a,b);//返回从a角标开始的b个字符，b是长度。范围即：[a, a+b-1]

```

**std::set**

std::set**
**

**std::list**

双向链表的实现。

**std::vector的初始化和赋值**

```c
// 1 不带参数的构造函数初始化
vector<int> abc;

// 2 带参数的构造函数初始化
vector<int> abc(10);    //初始化了10个默认值为0的元素
vector<int> cde(10，1);    //初始化了10个值为1的元素

// 3 通过数组地址初始化
int a[5] = {1,2,3,4,5};
通过数组a的地址初始化，注意地址是从0到5（左闭右开区间）
vector<int> b(a, a+5);

// 4 同类型vector初始化
vector<int> a(5,1);
vector<int> b(a);

// 5 通过insert初始化
// insert初始化方式将同类型的迭代器对应的始末区间（左闭右开区间）内的值插入到vector中
vector<int> a(6,6);
vecot<int> b;
//将a[0]~a[2]插入到b中，b.size()由0变为3
b.insert(b.begin(), a.begin(), a.begin() + 3);
// insert也可通过数组地址区间实现插入
int a[6] = {1,2,3,4,5,6};
vector<int> b;
b.insert(b.begin(), a, a+7);

// 6 通过copy函数赋值,同理insert
vector<int> a(5,1);
int a1[5] = {2,2,2,2,2};
vector<int> b(10);
copy(a.begin(), a.end(), b.begin());
copy(a1, a1+5, b.begin() + 5);


// #############################
// 二维vector初始化方法,指定长宽，初始化为0
vector<vector<bool>> block(m, vector<bool>(n, 0));

```

**hash类容器的常用方法**

```c
// 创建，删除，插入，修改，遍历，查询

// 创建
map<char, int> TmpMap;
map<char, int>::iterator Itr;  // 创建同类迭代器

// 删除
TmpMap.erase(key);
TmpMap.erase(Itr);// 可以用迭代器

// 插入/修改
    mymap[key] = value; // 直接插入或者更新一项。
    mymap.insert(pair<int, string>(222 ,"zhang liu"));
    (Insert方法不能覆盖，如果键已经存在，则无事发生！)
    (数组方法可以直接插入，如果键已经存在，则将会直接更新键对应的值。)

// 查询
int getvalue = mymap[key];
Itr = TmpMap.find('a');
Itr->second = 123; // value可修改，但key不能。


// find()
// map等的find函数返回迭代器。
// string的find函数返回uint型下标位置。
unordered_map<int, int> mymap;      
mymap.insert({1,2});      
auto it = mymap.find(1); // 返回值为迭代器      
if (it != mymap.end()) {} // 不存在返回尾迭代器mymap.end() 

string s("abcd");      
std::size_t pos = s.find("ab"); // 返回值为下标位置
if (pos != std::string::npos){} // 不存在返回string::npos,即-1.


```

**其他常见用法**

返回空的容器、对象、结构体： return {}



