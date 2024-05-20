---
layout: page
permalink: /teach/index.html
title: Teach
---

# Python note for myself

# Matlab note for myself

# Cpp note for myself

## vector

```c++
// 1. 创建空vector; 常数复杂度
vector<int> v0;
// 1+. 这句代码可以使得向vector中插入前3个元素时，保证常数时间复杂度
v0.reserve(3);
// 2. 创建一个初始空间为3的vector，其元素的默认值是0; 线性复杂度
vector<int> v1(3);
// 3. 创建一个初始空间为3的vector，其元素的默认值是2; 线性复杂度
vector<int> v2(3, 2);
// 4. 创建一个初始空间为3的vector，其元素的默认值是1，
// 并且使用v2的空间配置器; 线性复杂度
vector<int> v3(3, 1, v2.get_allocator());
// 5. 创建一个v2的拷贝vector v4， 其内容元素和v2一样; 线性复杂度
vector<int> v4(v2);
// 6. 创建一个v4的拷贝vector v5，其内容是{v4[1], v4[2]}; 线性复杂度
vector<int> v5(v4.begin() + 1, v4.begin() + 3);
// 7. 移动v2到新创建的vector v6，不发生拷贝; 常数复杂度; 需要 C++11
vector<int> v6(std::move(v2));  // 或者 v6 = std::move(v2);
```

1.  `begin()/cbegin()`

    返回指向首元素的迭代器，其中 `*begin = front`。

2.  `end()/cend()`

    返回指向数组尾端占位符的迭代器，注意是没有元素的。

3.  `rbegin()/crbegin()`

    返回指向逆向数组的首元素的逆向迭代器，可以理解为正向容器的末元素。

4.  `rend()/crend()`

    返回指向逆向数组末元素后一位置的迭代器，对应容器首的前一个位置，没有元素。

-   `empty()` 返回一个 `bool` 值，即 `v.begin() == v.end()`，`true` 为空，`false` 为非空。

-   `size()` 返回容器长度（元素数量），即 `std::distance(v.begin(), v.end())`。

-   `resize()` 改变 `vector` 的长度，多退少补。补充元素可以由参数指定。

-   `max_size()` 返回容器的最大可能长度。

-   `reserve()` 使得 `vector` 预留一定的内存空间，避免不必要的内存拷贝。

-   `capacity()` 返回容器的容量，即不发生拷贝的情况下容器的长度上限。

-   `shrink_to_fit()` 使得 `vector` 的容量与长度一致，多退但不会少。

-   `clear()` 清除所有元素

-   `insert()` 支持在某个迭代器位置插入元素、可以插入多个。**复杂度与 `pos` 距离末尾长度成线性而非常数的**

-   `erase()` 删除某个迭代器或者区间的元素，返回最后被删除的迭代器。复杂度与 `insert` 一致。

-   `push_back()` 在末尾插入一个元素，均摊复杂度为 **常数**，最坏为线性复杂度。

-   `pop_back()` 删除末尾元素，常数复杂度。

-   `swap()` 与另一个容器进行交换，此操作是 **常数复杂度** 而非线性的。

    

## stack

```c++
std::stack<TypeName> s;  // 使用默认底层容器 deque，数据类型为 TypeName
std::stack<TypeName, Container> s;  // 使用 Container 作为底层容器
std::stack<TypeName> s2(s1);        // 将 s1 复制一份用于构造 s2
```

-   `top()` 访问栈顶元素（如果栈为空，此处会出错）
-   `push(x)` 向栈中插入元素 x
-   `pop()` 删除栈顶元素
-   `size()` 查询容器中的元素数量
-   `empty()` 询问容器是否为空

## set

`set` 中不会出现值相同的元素。如果需要有相同元素的集合，需要使用 `multiset`。`multiset` 的使用方法与 `set` 的使用方法基本相同。`insert(x)` 当容器中没有等价元素的时候，将元素 x 插入到 `set` 中。



-   `insert(x)` 当容器中没有等价元素的时候，将元素 x 插入到 `set` 中。

insert 函数的返回值类型为 `pair<iterator, bool>`，其中 iterator 是一个指向所插入元素（或者是指向等于所插入值的原本就在容器中的元素）的迭代器，而 bool 则代表元素是否插入成功

-   `erase(x)` 删除值为 x 的 **所有** 元素，返回删除元素的个数。
-   `erase(pos)` 删除迭代器为 pos 的元素，要求迭代器必须合法。
-   `erase(first,last)` 删除迭代器在 ![[first,last)](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 范围内的所有元素。
-   `clear()` 清空 `set`。

1.  `begin()/cbegin()`
    返回指向首元素的迭代器，其中 `*begin = front`。
2.  `end()/cend()`
    返回指向数组尾端占位符的迭代器，注意是没有元素的。
3.  `rbegin()/crbegin()`
    返回指向逆向数组的首元素的逆向迭代器，可以理解为正向容器的末元素。
4.  `rend()/crend()`
    返回指向逆向数组末元素后一位置的迭代器，对应容器首的前一个位置，没有元素。



-   `count(x)` 返回 `set` 内键为 x 的元素数量。

-   `find(x)` 在 `set` 内存在键为 x 的元素时会返回该元素的迭代器，否则返回 `end()`。

-   `lower_bound(x)` 返回指向首个不小于给定键的元素的迭代器。如果不存在这样的元素，返回 `end()`。

-   `upper_bound(x)` 返回指向首个大于给定键的元素的迭代器。如果不存在这样的元素，返回 `end()`。

-   `empty()` 返回容器是否为空。

-   `size()` 返回容器内元素个数。

    ```c++
    struct cmp {
      bool operator()(int a, int b) { return a > b; }
    };
    
    set<int, cmp> s;
    ```


## pqueue

```c++
std::priority_queue<TypeName> q;             // 数据类型为 TypeName
std::priority_queue<TypeName, Container> q;  // 使用 Container 作为底层容器
std::priority_queue<TypeName, Container, Compare> q;
// 使用 Container 作为底层容器，使用 Compare 作为比较类型

// 默认使用底层容器 vector
// 比较类型 less<TypeName>（此时为它的 top() 返回为最大值）
// 若希望 top() 返回最小值，可令比较类型为 greater<TypeName>
// 注意：不可跳过 Container 直接传入 Compare

// 从 C++11 开始，如果使用 lambda 函数自定义 Compare
// 则需要将其作为构造函数的参数代入，如：
auto cmp = [](const std::pair<int, int> &l, const std::pair<int, int> &r) {
  return l.second < r.second;
};
std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int> >,
                    decltype(cmp)>
    pq(cmp);
```

**以下所有函数均为常数复杂度**

-   `top()` 访问堆顶元素（此时优先队列不能为空）
-   `empty()` 询问容器是否为空
-   `size()` 查询容器中的元素数量

**以下所有函数均为对数复杂度**

-   `push(x)` 插入元素，并对底层容器排序
-   `pop()` 删除堆顶元素（此时优先队列不能为空）

```c++
std::priority_queue<int> q1;
std::priority_queue<int, std::vector<int> > q2;
// C++11 后空格可省略
std::priority_queue<int, std::deque<int>, std::greater<int> > q3;
// q3 为小根堆
for (int i = 1; i <= 5; i++) q1.push(i);
// q1 中元素 :  [1, 2, 3, 4, 5]
std::cout << q1.top() << std::endl;
// 输出结果 : 5
q1.pop();
// 堆中元素 : [1, 2, 3, 4]
std::cout << q1.size() << std::endl;
// 输出结果 ：4
for (int i = 1; i <= 5; i++) q3.push(i);
// q3 中元素 :  [1, 2, 3, 4, 5]
std::cout << q3.top() << std::endl;
// 输出结果 : 1
```

## map

-   可以直接通过下标访问来进行查询或插入操作。例如 `mp["Alan"]=100`。
-   通过向 `map` 中插入一个类型为 `pair<Key, T>` 的值可以达到插入元素的目的，例如 `mp.insert(pair<string,int>("Alan",100));`；
-   `erase(key)` 函数会删除键为 `key` 的 **所有** 元素。返回值为删除元素的数量。
-   `erase(pos)`: 删除迭代器为 pos 的元素，要求迭代器必须合法。
-   `erase(first,last)`: 删除迭代器在 ![[first,last)](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7) 范围内的所有元素。
-   `clear()` 函数会清空整个容器

-   `count(x)`: 返回容器内键为 x 的元素数量。复杂度为 ![O(data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)（关于容器大小对数复杂度，加上匹配个数）。
-   `find(x)`: 若容器内存在键为 x 的元素，会返回该元素的迭代器；否则返回 `end()`。
-   `lower_bound(x)`: 返回指向首个不小于给定键的元素的迭代器。
-   `upper_bound(x)`: 返回指向首个大于给定键的元素的迭代器。若容器内所有元素均小于或等于给定键，返回 `end()`。
-   `empty()`: 返回容器是否为空。
-   `size()`: 返回容器内元素个数。



```c++
maps.insert(pair<int, student>(i, students[i]));
```

## deque

```c++
// 1. 定义一个int类型的空双端队列 v0
deque<int> v0;
// 2. 定义一个int类型的双端队列 v1，并设置初始大小为10; 线性复杂度
deque<int> v1(10);
// 3. 定义一个int类型的双端队列 v2，并初始化为10个1; 线性复杂度
deque<int> v2(10, 1);
// 4. 复制已有的双端队列 v1; 线性复杂度
deque<int> v3(v1);
// 5. 创建一个v2的拷贝deque v4，其内容是v4[0]至v4[2]; 线性复杂度
deque<int> v4(v2.begin(), v2.begin() + 3);
// 6. 移动v2到新创建的deque v5，不发生拷贝; 常数复杂度; 需要 C++11
deque<int> v5(std::move(v2));
```

-   `at()` 返回容器中指定位置元素的引用，执行越界检查，**常数复杂度**。
-   `operator[]` 返回容器中指定位置元素的引用。不执行越界检查，**常数复杂度**。
-   `front()` 返回首元素的引用。
-   `back()` 返回末尾元素的引用。
    -   `clear()` 清除所有元素
    -   `insert()` 支持在某个迭代器位置插入元素、可以插入多个。**复杂度与 `pos` 与两端距离较小者成线性**。
    -   `erase()` 删除某个迭代器或者区间的元素，返回最后被删除的迭代器。复杂度与 `insert` 一致。
    -   `push_front()` 在头部插入一个元素，**常数复杂度**。
    -   `pop_front()` 删除头部元素，**常数复杂度**。
    -   `push_back()` 在末尾插入一个元素，**常数复杂度**。
    -   `pop_back()` 删除末尾元素，**常数复杂度**。
    -   `swap()` 与另一个容器进行交换，此操作是 **常数复杂度** 而非线性的

`std::list` 是 STL 提供的 [双向链表](https://oi-wiki.org/ds/linked-list/) 数据结构。能够提供线性复杂度的随机访问，以及常数复杂度的插入和删除。

-   `front()` 返回首元素的引用。
-   `back()` 返回末尾元素的引用。
-   `splice()`、`remove()`、`sort()`、`unique()`、`merge()` 等。
