## C++11
http://c.biancheng.net/view/7151.html
### 目录
- [auto](#auto)
- [decltype](#decltype)
- [C++11模板实例化中连续右尖括号>>的改进](C++11模板实例化中连续右尖括号>>的改进)
- [使用using定义别名](#使用using定义别名)
- [支持函数模板的默认模板参数](#支持函数模板的默认模板参数)
- [列表初始化](#列表初始化)
- [lamba匿名函数](#lamba匿名函数)
- [非受限联合体](#非受限联合体)
- [for循环](#for循环)
- [constexpr](#constexpr)
- [const和constexpr的区别](#const和constexpr的区别)
- [longlong超长整形](#longlong超长整形)
- [引用限定符](#引用限定符)
- [完美转发](#完美转发)
- [shared_ptr](#shared_ptr)
- [unique_ptr](#unique_ptr)
- [weak_ptr](#weak_ptr)
### auto
- auto 仅仅是一个占位符，在编译器期间它会被真正的类型所替代。或者说，C++ 中的变量必须是有明确类型的，只是这个类型是由编译器自己推导出来的
- 限制
    - 不能在函数参数中使用
    - 不能作用于类的非静态成员变量
    - 不能定义数组
    - 不能作用于函数模板
- 应用
    - 定义迭代器
        ``` C++
        vector< vector<int> > v;
        vector< vector<int> >::iterator i = v.begin();
        auto i = v.begin();
        ```
    - 用于泛型编程
        ``` C++
        #include <iostream>
        using namespace std;
        class A{
        public:
            static int get(void){
                return 100;
            }
        };
        class B{
        public:
            static const char* get(void){
                return "http://c.biancheng.net/cplus/";
            }
        };
        template <typename T>
        void func(void){
            auto val = T::get();
            cout << val << endl;
        }
        int main(void){
            func<A>();
            func<B>();
            return 0;
        }
        ```
## decltype
- 如果 exp 是一个不被括号( )包围的表达式，或者是一个类成员访问表达式，或者是一个单独的变量，那么 decltype(exp) 的类型就和 exp 一致，这是最普遍最常见的情况。
- 如果 exp 是函数调用，那么 decltype(exp) 的类型就和函数返回值的类型一致。
- 如果 exp 是一个左值，或者被括号( )包围，那么 decltype(exp) 的类型就是 exp 的引用；假设 exp 的类型为 T，那么 decltype(exp) 的类型就是 T&。
``` C++
#include <vector>
using namespace std;
template <typename T>
class Base {
public:
    void func(T& container) {
        m_it = container.begin();
    }
private:
    typename T::iterator m_it;  //注意这里
};
int main()
{
    const vector<int> v;
    Base<const vector<int>> obj;
    obj.func(v);
    return 0;
}
template <typename T>
class Base {
public:
    void func(T& container) {
        m_it = container.begin();
    }
private:
    decltype(T().begin()) m_it;  //注意这里
};
```

## 返回类型后置
```c++
int& foo(int& i);
float foo(float& f);
template <typename T>
auto func(T& val) -> decltype(foo(val))
{
    return foo(val);
}
```

## C++11模板实例化中连续右尖括号>>的改进

## 使用using定义别名
- typedef无法重定义一个模板
- c++98
    ```C++
    template <typename Val>
    struct str_map
    {
        typedef std::map<std::string, Val> type;
    };
    // ...
    str_map<int>::type map1;
    // ...
    ```
- C++11
    ```
    template <typename Val>
    using str_map_t = std::map<std::string, Val>;
    // ...
    str_map_t<int> map1;
    ```
## 支持函数模板的默认模板参数
``` C++
template <typename T = int>  // error in C++98/03: default template arguments
void func()
{
    // ...
}
int main(void)
{
    func();   //T = int
    return 0;
}
```
- 此时模板参数 T 的类型就为默认值 int。从上面的例子中可以看出，当所有模板参数都有默认参数时，函数模板的调用如同一个普通函数。但对于类模板而言，哪怕所有参数都有默认参数，在使用时也必须在模板名后跟随<>来实例化。
- 当默认模  板参数和编译器自行推导出模板参数类型的能力一起结合使用时，代码的书写将变得异常灵活。我们可以指定函数中的一部分模板参数采用默认参数，而另一部分使用自动推导，比如下面的例子：
```C++
template <typename R = int, typename U>
R func(U val)
{
    return val;
}
int main()
{
    func(97);               // R=int, U=int
    func<char>(97);         // R=char, U=int
    func<double, int>(97);  // R=double, U=int
    return 0;
}
```

## tuple
- tuple 本质是一个以可变模板参数定义的类模板
- 实例化 tuple 模板类对象常用的方法有两种，一种是借助该类的构造函数，另一种是借助 make_tuple() 函数

## 列表初始化
- 在上面我们已经看到了，对于普通数组和 POD 类型，C++98/03 可以使用初始化列表（initializer list）进行    初始化
- 在 C++11 中，初始化列表的适用性被大大增加了。它现在可以用于任何类型对象的初始化，堆上动态分配的数组终于也可以使用初始化列表进行初始化了
``` C++
class Foo
{
public:
    Foo(int) {}
private:
    Foo(const Foo &);
};
int main(void)
{
    Foo a1(123);
    Foo a2 = 123;  //error: 'Foo::Foo(const Foo &)' is private
    Foo a3 = { 123 };
    Foo a4 { 123 };
    int a5 = { 3 };
    int a6 { 3 };
    return 0;
}
```
- 在上例中，a3、a4 使用了新的初始化方式来初始化对象，效果如同 a1 的直接初始化。

  a5、a6 则是基本数据类型的列表初始化方式。可以看到，它们的形式都是统一的。

  这里需要注意的是，a3 虽然使用了等于号，但它仍然是列表初始化，因此，私有的拷贝构造并不会影响到它。

  a4 和 a6 的写法，是 C++98/03 所不具备的。在 C++11 中，可以直接在变量名后面跟上初始化列表，来进行对象的初始化。


## lamba匿名函数
```C++
[外部变量访问方式说明符] (参数) mutable noexcept/throw() -> 返回值类型
{
   函数体;
};
```
- []
    
    方括号用于向编译器表明当前是一个 lambda 表达式，其不能被省略。在方括号内部，可以注明当前 lambda 函数的函数体中可以使用哪些“外部变量”
- (参数)

    和普通函数的定义一样，lambda 匿名函数也可以接收外部传递的多个参数。和普通函数不同的是，如果不需要传递参数，可以连同 () 小括号一起省略；
- mutable
    有点像static
    此关键字可以省略，如果使用则之前的 () 小括号将不能省略（参数个数可以为 0）。默认情况下，对于以值传递方式引入的外部变量，不允许在 lambda 表达式内部修改它们的值（可以理解为这部分变量都是 const 常量）。而如果想修改它们，就必须使用 mutable 关键字。
- noexcept/throw()

    可以省略，如果使用，在之前的 () 小括号将不能省略（参数个数可以为 0）。默认情况下，lambda 函数的函数体中可以抛出任何类型的异常。而标注 noexcept 关键字，则表示函数体内不会抛出任何异常；使用 throw() 可以指定 lambda 函数内部可以抛出的异常类型。
-  返回值类型

    指明 lambda 匿名函数的返回值类型。值得一提的是，如果 lambda 函数体内只有一个 return 语句，或者该函数返回 void，则编译器可以自行推断出返回值类型，此情况下可以直接省略-> 返回值类型。
- lambda匿名函数中的[外部变量]

    []	空方括号表示当前 lambda 匿名函数中不导入任何外部变量。

    [=]	只有一个 = 等号，表示以值传递的方式导入所有外部变量；


    [&]	只有一个 & 符号，表示以引用传递的方式导入所有外部变量；

    [val1,val2,...]	表示以值传递的方式导入 val1、val2 等指定的外部变量，同时多个变量之间没有先后次序；

    [&val1,&val2,...]	表示以引用传递的方式导入 val1、val2等指定的外部变量，多个变量之间没有前后次序；

    [val,&val2,...]	以上 2 种方式还可以混合使用，变量之间没有前后次序。

    [=,&val1,...]	表示除 val1 以引用传递的方式导入外，其它外部变量都以值传递的方式导入。

    [this]	表示以值传递的方式导入当前的 this 指针。

## 非受限联合体
- 非受限联合体的赋值注意事项
    - C++11 规定，如果非受限联合体内有一个非 POD 的成员，而该成员拥有自定义的构造函数，那么这个非受限联合体的默认构造函数将被编译器删除；其他的特殊成员函数，例如默认拷贝构造函数、拷贝赋值操作符以及析构函数等，也将被删除。
    ``` C++
    #include <string>
    using namespace std;
    union U {
        string s;
        int n;
    };
    int main() {
        U u;   // 构造失败，因为 U 的构造函数被删除
        return 0;
    }
    ```
- placement new
    ``` C++
    #include <string>
    using namespace std;
    union U {
        string s;
        int n;
    public:
        U() { new(&s) string; }
        ~U() { s.~string(); }
    };
    int main() {
        U u;
        return 0;
    }
    ```

    new(address) ClassConstruct(...)

## for循环

- 在使用新语法格式的 for 循环遍历某个序列时，如果需要遍历的同时修改序列中元素的值，实现方案是在 declaration 参数处定义引用形式的变量    

```c++
#include <iostream>
#include <vector>
using namespace std;
int main() {
    char arc[] = "abcde";
    vector<char>myvector(arc, arc + 5);
    //for循环遍历并修改容器中各个字符的值
    for (auto &ch : myvector) {
        ch++;
    }
    //for循环遍历输出容器中各个字符
    for (auto ch : myvector) {
        cout << ch;
    }
    return 0;
}
```

## constexpr
- constexpr 关键字的功能是使指定的常量表达式获得在程序编译阶段计算出结果的能力，而不必等到程序运行阶段。C++ 11 标准中，constexpr 可用于修饰普通变量、函数（包括模板函数）以及类的构造函数。
- constexpr修饰普通变量
    ``` c++
    #include <iostream>
    using namespace std;
    int main()
    {
        constexpr int num = 1 + 2 + 3;
        int url[num] = {1,2,3,4,5,6};
        couts<< url[1] << endl;
        return 0;
    }
    ```
- constexpr修饰函数
    ```c++
    constexpr int display(int x) {
    //可以添加 using 执行、typedef 语句以及 static_assert 断言
    return 1 + 2 + x;
    }
    ```
- constexpr修饰类的构造函数
    - 对于 C++ 内置类型的数据，可以直接用 constexpr 修饰
    - 当我们想自定义一个可产生常量的类型时，正确的做法是在该类型的内部添加一个常量构造函数
    ``` c++
    #include <iostream>
    using namespace std;
    //自定义类型的定义
    struct myType {
        constexpr myType(char *name,int age):name(name),age(age){};
        const char* name;
        int age;
        //其它结构体成员
    };
    int main()
    {
        constexpr struct myType mt { "zhangsan", 10 };
        cout << mt.name << " " << mt.age << endl;
        return 0;
    }
    ```
- constexpr修饰模板函数

    C++11 语法中，constexpr 可以修饰模板函数，但由于模板中类型的不确定性，因此模板函数实例化后的函数是否符合常量表达式函数的要求也是不确定的。

    针对这种情况下，C++11 标准规定，如果 constexpr 修饰的模板函数实例化结果不满足常量表达式函数的要求，则 constexpr 会被自动忽略，即该函数就等同于一个普通函数
## const和constexpr的区别
- constexpr在编译器得到结果，const在运行期
- const只读，constexpr常量
- const经过一些指针操作会变的可修改

## longlong超长整形
- C++11 标准规定，每种整数类型必须同时具备有符号（signed）和无符号（unsigned）两种类型，且每种具体的有符号整形和无符号整形所占用的存储空间（也就是位数）必须相同。注意，C++11 标准中只限定了每种类型最少占用多少存储空间，不同的平台可以占用不同的存储空间

## 引用限定符
- 默认情况下，对于类中用 public 修饰的成员函数，既可以被左值对象调用，也可以被右值对象调用
    ```c++
    #include <iostream>
    using namespace std;
    class demo {
    public:
        demo(int num):num(num){}
        int get_num(){
            return this->num;
        }
    private:
        int num;
    };
    int main() {
        demo a(10);
        cout << a.get_num() << endl;
        cout << move(a).get_num() << endl;
        return 0;
    }
    ```
- 某些场景中，我们可能需要限制调用成员函数的对象的类型（左值还是右值），为此 C++11 新添加了引用限定符。所谓引用限定符，就是在成员函数的后面添加 "&" 或者 "&&"，从而限制调用者的类型（左值还是右值）。
    ```C++
    #include <iostream>
    using namespace std;
    class demo {
    public:
        demo(int num):num(num){}
        int get_num()&{
            return this->num;
        }
    private:
        int num;
    };
    int main() {
        demo a(10);
        cout << a.get_num() << endl;          // 正确
        //cout << move(a).get_num() << endl;  // 错误
        return 0;
    }
    ```
## 完美转发
- std::forword
- 左值还是左值右值还是右值

## nullptr
- nullptr 是 nullptr_t 类型的右值常量

## shared_ptr
- C++ 智能指针底层是采用引用计数的方式实现的。简单的理解，智能指针在申请堆内存空间的同时，会为其配备一个整形值（初始值为 1），每当有新对象使用此堆内存时，该整形值 +1；反之，每当使用此堆内存的对象被释放时，该整形值减 1。当堆空间对应的整形值为 0 时，即表明不再有对象使用它，该堆空间就会被释放掉。
- 多个 shared_ptr 智能指针可以共同使用同一块堆内存。并且，由于该类型智能指针在实现上采用的是引用计数机制，即便有一个 shared_ptr 指针放弃了堆内存的“使用权”（引用计数减 1），也不会影响其他指向同一堆内存的 shared_ptr 指针（只有引用计数为 0 时，堆内存才会被自动释放）。
- 自定义所指堆内存的释放规则
```c++
    std::shared_ptr<int> p6(new int[10], std::default_delete<int[]>());
    //自定义释放规则
    void deleteInt(int*p) {
        delete []p;
    }
    //初始化智能指针，并自定义释放规则
    std::shared_ptr<int> p7(new int[10], deleteInt);
    std::shared_ptr<int> p7(new int[10], [](int* p) {delete[]p; });
```
operator=()	重载赋值号，使得同一类型的 shared_ptr 智能指针可以相互赋值。

operator*()	重载 * 号，获取当前 shared_ptr 智能指针对象指向的数据。

operator->()	重载 -> 号，当智能指针指向的数据类型为自定义的结构体时，通过 -> 运算符可以获取其内部的指定成员。

swap()	交换 2 个相同类型 shared_ptr 智能指针的内容。

reset()	当函数没有实参时，该函数会使当前 shared_ptr 所指堆内存的引用计数减 1，同时将当前对象重置为一个空指针；当为函数传递一个新申请的堆内存时，则调用该函数的 shared_ptr 对象会获得该存储空间的所有权，并且引用计数的初始值为 1。

get()	获得 shared_ptr 对象内部包含的普通指针。

use_count()	返回同当前 shared_ptr 对象（包括它）指向相同的所有 shared_ptr 对象的数量。

unique()	判断当前 shared_ptr 对象指向的堆内存，是否不再有其它 shared_ptr 对象再指向它。

operator bool()	判断当前 shared_ptr 对象是否为空智能指针，如果是空指针，返回 false；反之，返回 true。
## unique_ptr
作为智能指针的一种，unique_ptr 指针自然也具备“在适当时机自动释放堆内存空间”的能力。和 shared_ptr 指针最大的不同之处在于，unique_ptr 指针指向的堆内存无法同其它 unique_ptr 共享，也就是说，每个 unique_ptr 指针都独自拥有对其所指堆内存空间的所有权。
## weak_ptr
- 和share_ptr配合使用，weak_ptr 指针并不会使所指堆内存的引用计数加 1；同样，当 weak_ptr 指针被释放时，之前所指堆内存的引用计数也不会因此而减 1。也就是说，weak_ptr 类型指针并不会影响所指堆内存空间的引用计数
- 除此之外，weak_ptr<T> 模板类中没有重载 * 和 -> 运算符，这也就意味着，weak_ptr 类型指针只能访问所指的堆内存，而无法修改它
