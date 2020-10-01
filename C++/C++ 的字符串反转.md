# C++ 的字符串反转

### 方法一：

使用 algorithm 中的 reverse 函数：

```c++
// reverse 函数的定义（在 std 名称空间中）
template<class BidirIt>
void reverse(BidirIt first, BidirIt last)
{
    while ((first != last) && (first != --last)) {
        std::iter_swap(first++, last);
    }
}
```



由此我们可以得知，reverse  函数有两个参数，一个是字符串的开始，一个是字符串的结尾。

下面是一个使用 reverse 函数的一个小例子：

```c++
// 使用 reverse 函数
#include <algorithm>
#include <string>
int main() {
    std::string str = "Hello World";
    std::reverse(str.begin(), str.end());
    std::cout << str << std::endl;
    return 0;
}
```

输出：

![aHEuef.png](https://s1.ax1x.com/2020/08/10/aHEuef.png)

### 方法二：

有些人可能会认为 STL 不靠谱，于是诞生第二种方法：自己写函数！

下面是我自己写的一个字符串反转函数：

```c++
// 反转字符串
void ReverseStr(std::string & str) {
    int len = str.length()-1;
    for (int i = 0; i < len / 2; i++)
        swap(str[i], str[len-i]);
}
```

接下来是一个小例子：

```c++
#include <iostream>
#include <string>
#include <algorithm>

void ReverseStr(std::string &);

int main() {
    std::string str = "Hell0xo F";
    ReverseStr(str);
    std::cout << str << std::endl;
    return 0;
}

// 反转字符串
void ReverseStr(std::string & str) {
    int len = str.length()-1;
    for (int i = 0; i < len / 2; i++)
        std::swap(str[i], str[len-i]);
}
```

输出：

![aHEKw8.png](https://s1.ax1x.com/2020/08/10/aHEKw8.png)

#### End