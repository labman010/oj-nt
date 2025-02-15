***【TODO以后有需要再学习】***

**泛型编程**：

 C++泛型编程是一种编程范式，它允许程序员编写能够处理多种数据类型的通用代码，而无需针对每种数据类型编写单独的代码。泛型编程的核心思想是编写与特定数据类型无关的代码，使代码更具有通用性和复用性。(c++泛型编程由模版实现)

**泛型编程的好处**：

1. 代码复用：编写一次，应用于多种数据类型，避免了重复编码。
2. 类型安全：编译器会在编译期间验证模板实例化，确保类型正确匹配。
3. 灵活性：通过模板元编程，可以在编译期进行复杂的类型计算和逻辑推导。（元编程好像有新的标准）
4. 高效性：编译器可以针对具体类型优化生成的代码，达到与手工编写特化代码相媲美的性能。

C++的泛型编程最著名的应用就是Standard Template Library (STL)，其中包含了如容器（vector、list、set等）、迭代器和算法（sort、find等）等高度泛化的组件，它们能够在多种数据类型上无缝工作。

**模板**：

 C++实现泛型编程使用template模版特性。模板分为函数模板和类模板两种。

```c
// tips：（typename可以替换为class）
//  ======================== 函数模板 ========================
// 写法：
template <typename 类型参数1, typename 类型参数2, ...>
返回值类型  模板名(形参表)
{
    函数体
}
// 在这个例子中，swap函数可以用于交换任何类型的两个对象。使用swap时，编译器根据实参类型来实例化一个特定版本的函数。
template <typename T>
void swap(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}


//  ======================== 类模板 ========================。
// 这里，Vector类可以作为一个通用容器，容纳任何类型的数据。
template <typename T>
class Vector {
public:
    void push_back(const T& item);
    // ...其他成员函数...
private:
    std::vector<T> data;
};

```