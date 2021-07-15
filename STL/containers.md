
## 容器
分为序列式容器和关联式容器，常见的序列式容器如：vector、list、deque； 关联式如map、set等

![avatar](../pics/containers.png)

### 序列式容器
- 元素都可以有序(ordered)，但未必有序(sorted)
- c++本身内置了一个序列式容器 array, 此外STL提供了诸如`vector` `list`等序列式容器

#### vector
- 连续线性空间，可以实现随机取值，与array最大区别在于可以动态分配内存空间，不需要初始指定。
- **实现的关键元素**：
```c++
template<class T, class Alloc alloc>
class vecotr {
public:
    typedef  T value_type;
    typedef value_type* iterator; // 迭代器为普通指针
protected:
capacity();
size();
iterator start;          // 使用空间的头
iterator finish;         // 使用空间的尾
iterator end_of_storage; // 可用空间的尾
}
```

![avator](../pics/vector.png)
- 常见操作复杂度：
  - 随机访问 - 常数O(1)
  - 尾部插入/删除元素： 平均O(1)
  - 插入/移除元素与当vector结尾的距离成线性 O(N)
- 迭代器类型： Random Access Iterator
  - vector 的迭代器涵盖了指针所有的算术能力(`operator*，operator->，operator++，operator--，operator+，operator-，operator+=，operator-=`)， 同时 vector 支持随机存取，所以 vector 提供是 `Random Access Iterator`。
  - vector 维护的是一个**连续线性空间，所以不论其元素类型为何**，普通指针都可以作为 vector 的迭代器而满足所有必要条件
- 内存动态增加：
  - 动态增加大小，并不是在原空间之后接续新空间(因为无法保证原空间之后尚有可供配置的空间)，而是**以原大小的两倍另外配置一块较大空间**，然后将原内容拷贝过来， 然后才开始在原内容之后构造新元素，并释放原空间。
  - 因此，对 vector 的任何操作，一旦引起空间重新配置，**指向原 vector 的所有迭代器就都失效了**。
  - 1. 配置一块更大空间； 2.将原内容拷贝过去； 3.释放原空间