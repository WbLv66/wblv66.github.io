# STL容器


&lt;!--more--&gt;

{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2023/03/29/02/59/woman-7884470_1280.jpg&#34;&gt;}}

# STL容器

## 1. Array

### 1.1 初始化

std::array无构造函数，只含有非静态公共成员变量，所以属于**聚合类型**，其他聚合类型还有**数组类型**。

对聚合体使用列表初始化被称为**聚合初始化**，它也是列表初始化的一种形式，聚合体初始化需要**层层嵌套**。

std::array的定义大概如下：

```cpp
template&lt;typename T, std::size_t N&gt;
class array {
public:
  T _data[N];
};
```

它的聚合初始化如下：

```cpp
/**
* 第一层是为了初始化std::array本身
* 第二层是为了初始化里面的数组
*/
std::array&lt;int, 3&gt; arr{{1,2,3}};
```
由于 C&#43;&#43; 聚合初始化时允许省略所有的内部花括号，所以可以简写做：

```cpp
std::array&lt;int, 3&gt; arr{1,2,3};
```

对于二维数组。标准形式的初始化如下：

```cpp
/**
* 最外两层是为了初始化外层array
* 内部两层是为了初始化内层array
*/
std::array&lt;std::array&lt;int, 4&gt;, 3&gt; a{{
  {{1, 2, 3, 4}},
  {{5, 6, 7, 8}},
  {{9, 10, 11, 12}}
}};
```

因为子数组内不再出现内部花括号，所以可以让子数组采用省略语法：

```cpp
/**
* 最外两层是为了初始化外层array
* 内部一层是省略后的写法
*/
std::array&lt;std::array&lt;int, 4&gt;, 3&gt; a{{
  {1, 2, 3, 4},
  {5, 6, 7, 8},
  {9, 10, 11, 12}
}};
```

## 2. Vector

### 2.1 赋值

在将其他容器的数值赋值给std::vector时，有两种方式，分别是通过构造函数或assign方法和使用std::copy算法。使用构造函数和assign会自动管理内存和大小，无需使用resize手动预留空间；使用std::copy算法需要先分配空间

```C&#43;&#43;
#include &lt;array&gt;
#include &lt;vector&gt;

int main() {
    std::array&lt;int, 5&gt; arr = {1, 2, 3, 4, 5};

    // 方法1: 通过构造函数初始化
    std::vector&lt;int&gt; vec1(arr.begin(), arr.end());

    // 方法2: 通过assign方法赋值
    std::vector&lt;int&gt; vec2;
    vec2.assign(arr.begin(), arr.end());

    return 0;
}
```

```C&#43;&#43;
#include &lt;array&gt;
#include &lt;vector&gt;
#include &lt;algorithm&gt; // 需要包含 algorithm 头文件

int main() {
    std::array&lt;int, 5&gt; arr = {1, 2, 3, 4, 5};
    std::vector&lt;int&gt; vec;

    // 确保 vector 有足够空间（可选，但建议提前预留）
    vec.resize(arr.size());

    // 使用 std::copy
    std::copy(arr.begin(), arr.end(), vec.begin());

    return 0;
}
```


---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/10a4e19/  

