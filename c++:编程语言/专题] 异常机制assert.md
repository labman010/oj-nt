<https://blog.51cto.com/ticktick/191881>

**什么是assert**

assert 宏通常用于调试和测试阶段，它允许程序员在代码中插入检查点，以确保程序的某些条件是满足的。如果断言失败（条件不满足），程序将中止执行，通常会输出有关失败的信息，如文件名、行号和错误消息。

```c
#include <cassert>
int main() {
    int x = 5;
    int y = 10;
    assert(x < y); // 检查 x 是否小于 y
    // 如果 x < y，则程序会继续执行
    // 如果 x >= y，则程序将终止执行，并输出错误消息
    return 0;
}
错误时终端输出：
Assertion failed: (x > y), function main, file test.cpp, line 5.


```

**什么是异常**

C++运行错误常见的有文件打开失败、数组下标溢出、系统内存不足等等。比如针对文件打开失败的情况，保护的方法有很多种，最简单的就是return，告诉上层调用者函数执行失败；另外一种处理策略就是利用c++的异常机制，抛出异常。

**和if判断对比：**

 异常处理机制通常能够提高代码的可读性和维护性。它允许将错误处理代码集中在一个或多个 catch 块中，使代码更清晰，因为正常的执行路径不会被错误处理代码混淆。使用 if 条件判断和 return 的错误处理可能会导致错误处理代码分散在函数的多个地方，降低了代码的可读性。

 异常处理机制允许异常在函数调用堆栈中传播，直到找到适当的 catch 块处理异常。这意味着你可以在高层函数中捕获异常，而不必在每个函数中都进行错误检查和处理。使用 if 条件判断和 return 的错误处理需要在每个可能引发错误的地方进行检查和处理，增加了代码的复杂性。

三个关键字： try、 throw 、 catch 。

异常抛出（Throwing Exceptions）： 当程序遇到错误或异常情况时，可以使用 throw 关键字来抛出异常。异常通常是一个对象，可以是任何类型，但通常是异常类的实例。

```c
throw MyException("Something went wrong");
throw std::runtime_error("Division by zero");

```

异常捕获（Catching Exceptions）： 在代码中，你可以使用 try 和 catch 块来捕获异常。try 块包含可能引发异常的代码块，而 catch 块用于处理特定类型的异常。

* 一个try后可以多个catch捕获不同异常。*

*
*

异常类（Exception Classes）： 异常通常是类的实例，它们派生自标准库的 std::exception 类或其子类。开发人员可以创建自定义的异常类（见文档末尾），以表示不同的异常情况，并添加适当的信息和方法。

标准异常类（Standard Exception Classes）： C++标准库提供了一些标准异常类，如 std::runtime\_error、std::logic\_error 等，用于表示常见的异常情况。

```c
// 各类异常！！！
try {
    // 可能引发异常的代码
} catch (const std::runtime_error& e) {
    // 处理运行时错误
    std::cerr << "Runtime error: " << e.what() << std::endl;
} catch (const std::logic_error& e) {
    // 处理逻辑错误
    std::cerr << "Logic error: " << e.what() << std::endl;
} catch (const MyException& e) {
    // 处理自定义的 MyException 类型的异常
} catch (const std::exception& e) {
    // 捕获所有其他异常
} catch (...) {
    // 捕获未知类型的异常
    std::cerr << "An unknown exception occurred." << std::endl;
}
```

异常传播（Propagation of Exceptions）： 异常可以在函数之间传播。如果一个函数内部引发异常但没有捕获它，异常将传播到调用函数，依此类推，直到某个 catch 块捕获它。

**底层原理：**

异常抛出的新对象并非创建在函数栈上，而是创建在专用的异常栈上，因此它才可以跨接多个函数而传递到上层，否则在栈清空的过程中就会被销毁。***所有从try到throw语句之间构造起来的对象的析构函数将被自动调用。***但如果一直上溯到main函数后还没有找到匹配的catch块，那么系统调用terminate()终止整个程序，这种情况下不能保证所有局部对象会被正确地销毁。

```c
注意问题：
1. 如果抛出的异常一直没有函数捕获(catch)，则会一直上传到c++运行系统那里，导致整个程序的终止。
2. 一般在异常抛出后资源可以正常被释放，但注意如果在类的构造函数中抛出异常，系统是不会调用它的析构函数的，处理方法是：如果在构造函数中要抛出异常，则在抛出前要记得删除申请的资源。
3. 异常处理仅仅通过类型而不是通过值来匹配的，所以catch块的参数可以没有参数名称，只需要参数类型。
4. 应该在throw语句后写上异常对象时，throw先通过Copy构造函数构造一个新对象，再把该新对象传递给 catch.
5. catch块的参数推荐采用地址传递而不是值传递，不仅可以提高效率，还可以利用对象的多态性。另外，派生类的异常扑获要放到父类异常扑获的前面，否则，派生类的异常无法被扑获。

```

```c
// chatgpt一个自定义异常的例子
#include <iostream>
#include <exception>

// 自定义异常类 MyException，继承自 std::exception
class MyException : public std::exception {
public:
    MyException(const char* message) : msg(message) {}

    // 重写 std::exception 的虚拟函数 what()，返回异常信息
    const char* what() const noexcept override {
        return msg.c_str();
    }

private:
    std::string msg;
};

int main() {
    try {
        // 模拟引发自定义异常
        throw MyException("This is a custom exception");
    } catch (const MyException& e) {
        // 捕获并处理自定义异常
        std::cerr << "Custom exception caught: " << e.what() << std::endl;
    }

    return 0;
}
```

```c
// 一个常用例子
double func(double x, double y) {
    // 除法函数
    if(y == 0) {
        throw y;
    }
    return x/y;
}

int main() {
    double res;
    try {
        res = fun(2, 3);
        cout << res;
    } catch (double) { // 看！这里只写类型就行.
        //而且普通类型也没错误，但是不好/不推荐。
        cerr << "some error";
        exit(1);
    }
}
```