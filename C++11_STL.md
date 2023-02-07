## C++11_STL
### 目录
- [array](#array)
- [vecyor](#vecyor)
- [deque](#deque)
- [list](#list)
- [forword_list](#forword_list)
- [map](#map)
- [multimap](#multimap)
- [set](#set)
- [multiset](#multiset)
- [unordered_map](#unordered_map)
- [unordered_multimap](#unordered_multimap)
- [unordered_set](#unordered_set)
- [unordered_multiset](#unordered_multiset)

### array
- 和其它容器不同，array 容器的大小是固定的，无法动态的扩展或收缩，这也就意味着，在使用该容器的过程无法借由增加或移除元素而改变其大小，它只允许访问或者替换存储的元素。
|成员函数	|功能
|-|-|
|begin()	|返回指向容器中第一个元素的随机访问迭代器。
|end()	    |返回指向容器最后一个元素之后一个位置的随机访问迭代器，通常和 begin() 结合使用。
|rbegin()	|返回指向最后一个元素的随机访问迭代器。
|rend()	    |返回指向第一个元素之前一个位置的随机访问迭代器。
|cbegin()	|和 begin() 功能相同，只不过在其基础上增加了 const 属性，不能用于修改元素。
|cend()	    |和 end() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crbegin()	|和 rbegin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crend()	|和 rend() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|size()	    |返回容器中当前元素的数量，其值始终等于初始化 array 类的第二个模板参数 N。
|max_size()	|返回容器可容纳元素的最大数量，其值始终等于初始化 array 类的第二个模板参数 N。
|empty()	|判断容器是否为空，和通过 size()==0 的判断条件功能相同，但其效率可能更快。
|at(n)	    |返回容器中 n 位置处元素的引用，该函数自动检查 n 是否在有效的范围内，如果不是则抛出 |out_of_range| 异常。
|front()	|返回容器中第一个元素的直接引用，该函数不适用于空的 array 容器。
|back()	    |返回容器中最后一个元素的直接应用，该函数同样不适用于空的 array 容器。
|data()	    |返回一个指向容器首个元素的指针。利用该指针，可实现复制容器中所有元素等类似功能。
|fill(val)	|将 val 这个值赋值给容器中的每个元素。
|array1.swap(array2)	|交换 array1 和 array2 容器中的所有元素，但前提是它们具有相同的长度和类型。
### vector
- vector 常被称为向量容器，因为该容器擅长在尾部插入或删除元素，在常量时间内就可以完成，时间复杂度为O(1)；而对于在容器头部或者中部插入或删除元素，则花费时间要长一些（移动元素需要耗费时间），时间复杂度为线性阶O(n)。
- vector创建
```C++
#include <vector>
using namespace std

std::vector<double> values;
values.reserve(20);
std::vector<int> primes {2,3,5,7,11,13,17,19}
std::vector<double> value(20);
std::vector<double> values(20, 1.0);
int num = 20;
double value = 1.0;
std::vector<double> values(num, value);
std::vector<char> value1(5, "c");
std::vector<char> value2(value1);

int array[] = {1,2,3};
std::vector<int> value(array, array+2);
std::vector<int> value1{1,2,3,4,5};
std::vector<int> value2(std::begin(value1),std::begin(value1)+3)
```
|函数成员|函数功能|
|-|-|
|begin()	|返回指向容器中第一个元素的迭代器。
|end()	    |返回指向容器最后一个元素所在位置后一个位置的迭代器，通常和 |begin() 结合使用。
|rbegin()	|返回指向最后一个元素的迭代器。
|rend()	    |返回指向第一个元素所在位置前一个位置的迭代器。
|cbegin()	|和 begin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|cend()	    |和 end() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crbegin()	|和 rbegin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crend()	|和 rend() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|size()	    |返回实际元素个数。
|max_size()	|返回元素个数的最大值。这通常是一个很大的值，一般是 232-1，所以我们很少会用到这个函数。
|resize()	|改变实际元素的个数。
|capacity()	|返回当前容量。
|empty()	|判断容器中是否有元素，若无元素，则返回 true；反之，返回 false。
|reserve()	|增加容器的容量。
|shrink _to_fit()|	将内存减少到等于当前元素实际所使用的大小。
|operator[ ]|	重载了 [ ] 运算符，可以向访问数组中元素那样，通过下标即可访问甚至修改 vector 容器中的元素。
|at()	    |使用经过边界检查的索引访问元素。
|front()	|返回第一个元素的引用。
|back()	    |返回最后一个元素的引用。
|data()	    |返回指向容器中第一个元素的指针。
|assign()	|用新元素替换原有内容。
|push_back()|	在序列的尾部添加一个元素。
|pop_back()	|移出序列尾部的元素。
|insert()	|在指定的位置插入一个或多个元素。
|erase()	|移出一个元素或一段元素。
|clear()	|移出所有的元素，容器大小变为 0。
|swap()	    |交换两个容器的所有元素。
|emplace()	|在指定的位置直接生成一个元素。
|emplace_back()|	在序列尾部生成一个元素。
- emplace_back/emplace 与 push_back/insert
    如果要将一个结构体类型的实例，放入容器中，一般有2个步骤：

    构造这个实例
    copy这个实例到容器中
    注意，这个copy的动作有2种方法：
    1> 通过普通的拷贝构造函数完成
    2> 自C++11起可以通过移动构造函数来完成的

    那么，push_back 和 insert 就是按照这2个步骤来做的；
    但是 emplace_back/emplace 并不是，它是在指定位置构造出实例。 这就是区别。
    因此， emplace_back/emplace 的参数也是很有特点，它并不是容器元素类型，而是容器元素的构造函数所需要的类型。

## deque
- deque 容器也擅长在序列尾部添加或删除元素（时间复杂度为O(1)），而不擅长在序列中间添加或删除元素。
- deque 容器也可以根据需要修改自身的容量和大小。
- 和 vector 不同的是，deque 还擅长在序列头部添加或删除元素，所耗费的时间复杂度也为常数阶O(1)。并且更重要的一点是，deque 容器中存储元素并不能保证所有元素都存储到连续的内存空间中。
- 当需要向序列两端频繁的添加或删除元素时，应首选 deque 容器。
- deque创建
```C++
#include <deque>
using namespace std;
std::deque<int> d;
std::deque<int> d(10);
std::deque<int> d(10, 5);
std::deque<int> d1(5);
std::deque<int> d2(d1);
//拷贝普通数组，创建deque容器
int a[] = { 1,2,3,4,5 };
std::deque<int>d(a, a + 5);
//适用于所有类型的容器
std::array<int, 5>arr{ 11,12,13,14,15 };
std::deque<int>d(arr.begin()+2, arr.end());//拷贝arr容器中的{13,14,15}
```
|函数成员	|函数功能
|-|-|
|begin()	|返回指向容器中第一个元素的迭代器。
|end()	    |返回指向容器最后一个元素所在位置后一个位置的迭代器，通常和 begin() 结合使用。
|rbegin()	|返回指向最后一个元素的迭代器。
|rend()	    |返回指向第一个元素所在位置前一个位置的迭代器。
|cbegin()	|和 begin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|cend()	    |和 end() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crbegin()	|和 rbegin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crend()	|和 rend() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|size()	    |返回实际元素个数。
|max_size()	|返回容器所能容纳元素个数的最大值。这通常是一个很大的值，一般是 232-1，我们很少会用到这个函数。
|resize()	|改变实际元素的个数。
|empty()	|判断容器中是否有元素，若无元素，则返回 true；反之，返回 false。
|shrink _to_fit()|	将内存减少到等于当前元素实际所使用的大小。
|at()	    |使用经过边界检查的索引访问元素。
|front()	|返回第一个元素的引用。
|back()	    |返回最后一个元素的引用。
|assign()	|用新元素替换原有内容。
|push_back()|	在序列的尾部添加一个元素。
|push_front()|	在序列的头部添加一个元素。
|pop_back()	|移除容器尾部的元素。
|pop_front()|	移除容器头部的元素。
|insert()	|在指定的位置插入一个或多个元素。
|erase()	|移除一个元素或一段元素。
|clear()	|移出所有的元素，容器大小变为 0。
|swap()	    |交换两个容器的所有元素。
|emplace()	|在指定的位置直接生成一个元素。
|emplace_front()|	在容器头部生成一个元素。和 push_front() 的区别是，该函数直接在容器头部构造元素，省去了复制移动元素的过程。
|emplace_back()|	在容器尾部生成一个元素。和 push_back() 的区别是，该函数直接在容器尾部构造元素，省去了复制移动元素的过程。


## list
- 容器的底层是以双向链表的形式实现的。这意味着，list 容器中的元素可以分散存储在内存空间里，而不是必须存储在一整块连续的内存空间中
- 它可以在序列已知的任何位置快速插入或删除元素（时间复杂度为O(1)）。并且在 list 容器中移动元素，也比其它容器的效率高。
- 使用 list 容器的缺点是，它不能像 array 和 vector 那样，通过位置直接访问元素。举个例子，如果要访问 list 容器中的第 6 个元素，它不支持容器对象名[6]这种语法格式，正确的做法是从容器中第一个元素或最后一个元素开始遍历容器，直到找到该位置。
```C++
std::list<int> values;
std::list<int> values(10);
std::list<int> values(10, 5);
std::list<int> value1(10);
std::list<int> value2(value1);
//拷贝普通数组，创建list容器
int a[] = { 1,2,3,4,5 };
std::list<int> values(a, a+5);
//拷贝其它类型的容器，创建 list 容器
std::array<int, 5>arr{ 11,12,13,14,15 };
std::list<int>values(arr.begin()+2, arr.end());//拷贝arr容器中的{13,14,15}
```
|成员函数	|功能
|-|-|
|begin()	|返回指向容器中第一个元素的双向迭代器。
|end()	    |返回指向容器中最后一个元素所在位置的下一个位置的双向迭代器。
|rbegin()	|返回指向最后一个元素的反向双向迭代器。
|rend()	    |返回指向第一个元素所在位置前一个位置的反向双向迭代器。
|cbegin()	|和 begin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|cend()	    |和 end() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crbegin() 	|和 rbegin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|crend()	|和 rend() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改元素。
|empty()	|判断容器中是否有元素，若无元素，则返回 true；反之，返回 false。
|size()	    |返回当前容器实际包含的元素个数。
|max_size()	|返回容器所能包含元素个数的最大值。这通常是一个很大的值，一般是 232-1，所以我们很少会用到这个函数。
|front()	|返回第一个元素的引用。
|back()	    |返回最后一个元素的引用。
|assign()	|用新元素替换容器中原有内容。
|emplace_front()|	在容器头部生成一个元素。该函数和 push_front() 的功能相同，但效率更高。
|push_front()|	在容器头部插入一个元素。
|pop_front()|	删除容器头部的一个元素。
|emplace_back()|	在容器尾部直接生成一个元素。该函数和 push_back() 的功能相同，但效率更高。
|push_back()|	在容器尾部插入一个元素。
|pop_back()	|删除容器尾部的一个元素。
|emplace()	|在容器中的指定位置插入元素。该函数和 insert() 功能相同，但效率更高。
|insert() 	|在容器中的指定位置插入元素。
|erase()	|删除容器中一个或某区域内的元素。
|swap()	    |交换两个容器中的元素，必须保证这两个容器中存储的元素类型是相同的。
|resize()	|调整容器的大小。
|clear()	|删除容器存储的所有元素。
|splice()	|将一个 list 容器中的元素插入到另一个容器的指定位置。
|remove(val)|	删除容器中所有等于 val 的元素。
|remove_if()|	删除容器中满足条件的元素。
|unique()	|删除容器中相邻的重复元素，只保留一个。
|merge()	|合并两个事先已排好序的 list 容器，并且合并之后的 list 容器依然是有序的。
|sort()	    |通过更改容器中元素的位置，将它们进行排序。
|reverse()	|反转容器中元素的顺序。
## list、vector和deque的区别
- 如果你需要高效的随即存取，而不在乎插入和删除的效率，使用vector
- 如果你需要大量的插入和删除，而不关心随机存取，则应使用list
- 如果你需要随机存取，而且关心两端数据的插入和删除，则应使用deque

## forword_list
- forward_list 容器具有和 list 容器相同的特性，即擅长在序列的任何位置进行插入元素或删除元素的操作，但对于访问存储的元素，没有其它容器（如 array、vector）的效率高。

- 另外，由于单链表没有双向链表那样灵活，因此相比 list 容器，forward_list 容器的功能受到了很多限制。比如，由于单链表只能从前向后遍历，而不支持反向遍历，因此 forward_list 容器只提供前向迭代器，而不是双向迭代器。这意味着，forward_list 容器不具有 rbegin()、rend() 之类的成员函数。

## pair
```C++
#include <iostream>
#include <utility>      // pair
#include <string>       // string
using namespace std;
int main() {
    // 调用构造函数 1，也就是默认构造函数
    pair <string, double> pair1;
    // 调用第 2 种构造函数
    pair <string, string> pair2("STL教程","http://c.biancheng.net/stl/");  
    // 调用拷贝构造函数
    pair <string, string> pair3(pair2);
    //调用移动构造函数
    pair <string, string> pair4(make_pair("C++教程", "http://c.biancheng.net/cplus/"));
    // 调用第 5 种构造函数
    pair <string, string> pair5(string("Python教程"), string("http://c.biancheng.net/python/"));  
   
    cout << "pair1: " << pair1.first << " " << pair1.second << endl;
    cout << "pair2: "<< pair2.first << " " << pair2.second << endl;
    cout << "pair3: " << pair3.first << " " << pair3.second << endl;
    cout << "pair4: " << pair4.first << " " << pair4.second << endl;
    cout << "pair5: " << pair5.first << " " << pair5.second << endl;
    return 0;
}
```

## map
- 与此同时，在使用 map 容器存储多个键值对时，该容器会自动根据各键值对的键的大小，按照既定的规则进行排序。默认情况下，map 容器选用std::less<T>排序规则（其中 T 表示键的数据类型），其会根据键的大小对所有键值对做升序排序。当然，根据实际情况的需要，我们可以手动指定 map 容器的排序规则，既可以选用 STL 标准库中提供的其它排序规则（比如std::greater<T>），也可以自定义排序规则。
- 另外需要注意的是，使用 map 容器存储的各个键值对，键的值既不能重复也不能被修改。换句话说，map 容器中存储的各个键值对不仅键的值独一无二，键的类型也会用 const 修饰，这意味着只要键值对被存储到 map 容器中，其键的值将不能再做任何修改。
```C++
#include <map>
using namespace std;
template < class Key,                                     // 指定键（key）的类型
           class T,                                       // 指定值（value）的类型
           class Compare = less<Key>,                     // 指定排序规则
           class Alloc = allocator<pair<const Key,T> >    // 指定分配器对象的类型
           > class map;
std::map<std::string, int>myMap;
std::map<std::string, int>myMap{ {"C语言教程",10},{"STL教程",20} };
std::map<std::string, int>myMap{std::make_pair("C语言教程",10),std::make_pair("STL教程",20)};
std::map<std::string, int>newMap(myMap);
#创建一个会返回临时 map 对象的函数
std::map<std::string,int> disMap() {
    std::map<std::string, int>tempMap{ {"C语言教程",10},{"STL教程",20} };
    return tempMap;
}
//调用 map 类模板的移动构造函数创建 newMap 容器
std::map<std::string, int>newMap(disMap());
std::map<std::string, int>myMap{ {"C语言教程",10},{"STL教程",20} };
std::map<std::string, int>newMap(++myMap.begin(), myMap.end());
std::map<std::string, int>myMap{ {"C语言教程",10},{"STL教程",20} };
std::map<std::string, int, std::less<std::string> >myMap{ {"C语言教程",10},{"STL教程",20} };
\\<"C语言教程", 10>
\\<"STL教程", 20>
std::map<std::string, int, std::greater<std::string> >myMap{ {"C语言教程",10},{"STL教程",20} };
\\<"STL教程", 20>
\\<"C语言教程", 10>
```
|成员方法|	功能|
|-|-|
|begin()	|返回指向容器中第一个（注意，是已排好序的第一个）键值对的双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。
|end()	    |返回指向容器最后一个元素（注意，是已排好序的最后一个）所在位置后一个位置的双向迭代器，通常和 begin() 结合使用。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。
|rbegin()	|返回指向最后一个（注意，是已排好序的最后一个）元素的反向双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。
|rend()	    |返回指向第一个（注意，是已排好序的第一个）元素所在位置前一个位置的反向双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。
|cbegin()	|和 begin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改容器内存储的键值对。
|cend()	    |和 end() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改容器内存储的键值对。
|crbegin()	|和 rbegin() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改容器内存储的键值对。
|crend()	|和 rend() 功能相同，只不过在其基础上，增加了 const 属性，不能用于修改容器内存储的键值对。
|find(key)	|在 map 容器中查找键为 key 的键值对，如果成功找到，则返回指向该键值对的双向迭代器；反之，则返回和 end() 方法一样的迭代器。另外，如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。
|lower_bound(key)|	返回一个指向当前 map 容器中第一个大于或等于 key 的键值对的双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。
|upper_bound(key)|	返回一个指向当前 map 容器中第一个大于 key 的键值对的迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。
|equal_range(key)|	该方法返回一个 pair 对象（包含 2 个双向迭代器），其中 pair.first 和 lower_bound() 方法的返回值等价，pair.second 和 upper_bound() 方法的返回值等价。也就是说，该方法将返回一个范围，该范围中包含的键为 key 的键值对（map 容器键值对唯一，因此该范围最多包含一个键值对）。
|empty() 	|若容器为空，则返回 true；否则 false。
|size()	    |返回当前 map 容器中存有键值对的个数。
|max_size()	|返回 map 容器所能容纳键值对的最大个数，不同的操作系统，其返回值亦不相同。
|operator[]	|map容器重载了 [] 运算符，只要知道 map 容器中某个键值对的键的值，就可以向获取数组中元素那样，通过键直接获取对应的值。
|at(key)	|找到 map 容器中 key 键对应的值，如果找不到，该函数会引发 out_of_range 异常。
|insert()	|向 map 容器中插入键值对。
|erase()	|删除 map 容器指定位置、指定键（key）值或者指定区域内的键值对。后续章节还会对该方法做重点讲解。
|swap()	    |交换 2 个 map 容器中存储的键值对，这意味着，操作的 2 个键值对的类型必须相同。
|clear()	|清空 map 容器中所有的键值对，即使 map 容器的 size() 为 0。
|emplace()	|在当前 map 容器中的指定位置处构造新键值对。其效果和插入键值对一样，但效率更高。
|emplace_hint()|	在本质上和 emplace() 在 map 容器中构造新键值对的方式是一样的，不同之处在于，使用者必须为该方法提供一个指示键值对生成位置的迭代器，并作为该方法的第一个参数。
|count(key)	|在当前 map 容器中，查找键为 key 的键值对的个数并返回。注意，由于 map 容器中各键值对的键的值是唯一的，因此该函数的返回值最大为 1。
```C++
#include <iostream>
#include <map>      // map
#include <string>       // string
using namespace std;
int main() {
    //创建空 map 容器，默认根据个键值对中键的值，对键值对做降序排序
    std::map<std::string, std::string, std::greater<std::string>>myMap;
    //调用 emplace() 方法，直接向 myMap 容器中指定位置构造新键值对
    myMap.emplace("C语言教程","http://c.biancheng.net/c/");
    myMap.emplace("Python教程", "http://c.biancheng.net/python/");
    myMap.emplace("STL教程", "http://c.biancheng.net/stl/");
    //输出当前 myMap 容器存储键值对的个数
    cout << "myMap size==" << myMap.size() << endl;
    //判断当前 myMap 容器是否为空
    if (!myMap.empty()) {
        //借助 myMap 容器迭代器，将该容器的键值对逐个输出
        for (auto i = myMap.begin(); i != myMap.end(); ++i) {
            cout << i->first << " " << i->second << endl;
        }
    }  
    return 0;
}
```

## multimap 
- multimap 容器具有和 map 相同的特性，即 multimap 容器也用于存储 pair<const K, T> 类型的键值对（其中 K 表示键的类型，T 表示值的类型），其中各个键值对的键的值不能做修改；并且，该容器也会自行根据键的大小对存储的所有键值对做排序操作。和 map 容器的区别在于，multimap 容器中可以同时存储多（≥2）个键相同的键值对。
```C++
#include <iostream>
#include <map>  //map
using namespace std;   
int main()
{
    //创建并初始化 multimap 容器
    multimap<char, int>mymultimap{ {'a',10},{'b',20},{'b',15}, {'c',30} };
    //输出 mymultimap 容器存储键值对的数量
    cout << mymultimap.size() << endl;
    //输出 mymultimap 容器中存储键为 'b' 的键值对的数量
    cout << mymultimap.count('b') << endl;
    for (auto iter = mymultimap.begin(); iter != mymultimap.end(); ++iter) {
        cout << iter->first << " " << iter->second << endl;
    }
    return 0;
}
```
## set
## multiset
## unordered_map
## unordered_multimap
## unordered_set
## unordered_set
