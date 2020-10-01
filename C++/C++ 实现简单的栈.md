
# C++ 实现简单的栈

栈是学习计算机必不可少的一种数据结构。

经过一段时间的学习，我自己写了一个简单的栈(<del>大佬勿喷</del>)



## 实现

#### 一、StackSource.h

**为了避免与C++ STL中的stack重名，所以取了这个名字。**

首先，我们要先用*typedef*来定义一个类型叫Item.

```c++
            typedef std::string Item;		// 这里的std::string可以改为任何你想改成的类型（甚至是自定义的类）
```

当然，要引用*iostream*库

```c++
            #include <iostream>
```

注：*iostream*库间接包含*std::string*，所以引用*iostream*就无需引用*string*库了。

然后，我们定义一个宏名叫*maxN*

```c++
            #define maxN 1010		// maxN用于类的构造函数，这里先不赘述
```

接下来，我们就要明确*mystack*类需要满足哪些要求：

* push()
* pop()
* gettop()  获取栈的大小
* getval()  获取栈顶元素
* print() 打印这个栈的信息
* isempty()和isfull()  判断栈空或栈满

于是，我们可以写一个*mystack*类：

```c++
// stack类
class mystack
{
private:
	unsigned top;
	Item* st;	// 定义一个指针用于使用动态数组

public:
	mystack(const Item *);		// 用一个值来初始化
	mystack();					// 默认构造函数
	~mystack();					// delete掉已分配的内存空间

	void push(Item &);
	void pop();
	unsigned gettop();
	Item getval(int);

	void print();

	bool isempty();
	bool isfull();
};
```

------

#### 二、StackSource.cpp

**类函数的实现文件**。

首先，我们要实现构造函数和析构函数：

```c++
// 含参数构造函数
mystack::mystack(const Item* Init) {
	st = new std::string[maxN];		// 分配内存空间
	top = 0;

	Item InitValue = *Init;
	push(InitValue);
}

// 无参数构造函数
mystack::mystack() {
	st = new std::string[maxN];
	top = 0;
}

// 析构函数
mystack::~mystack() { delete[] st; }
```

然后实现主要功能：

```c++
// 主要功能：1. push()
void mystack::push(Item & pushNum) {
	if (!isfull()) {
		std::cout << "Overflow!" << std::endl;
		return;
	}

	st[++top] = pushNum;
}

// 主要功能：2. pop()
void mystack::pop() {
	if (!isempty()) {
		std::cout << "Overflow!" << std::endl;
		return;
	}

	top--;
}

// 主要功能：3. gettop()		返回top的值
unsigned mystack::gettop() { return top; }

// 主要功能：4. topval()		返回栈中第n个元素的值
Item mystack::getval(int subScript) {
	if (subScript < 0 || subScript >= maxN) {
		std::cout << "Value not found!" << std::endl;
		return;
	}

	return st[subScript];
}


// 次要功能：1. print()		打印栈中每个元素的值。
void mystack::print() {
	if (!isempty() || !isfull()) {
		std::cout << "Overflow!" << std::endl;
		return;
	}

	std::cout << "Stack top:\t" << top << std::endl;
	for (int i = 1; i <= top; i++)
		std::cout << i << ".\t" << st[i] << std::endl;
}

// 次要功能：2. isempty()		判断栈是否为空
bool mystack::isempty() { return top; }

// 次要功能：3. isfull()		判断栈是否为满
bool mystack::isfull() { return (top == maxN); }
```

至此，*mystack*类的实现就结束了。


## 开源
**若要查看源码，请访问以下网站：**

* github地址：https://github.com/CristimeCai/MyStack

* 国内用户请使用gitee（github网速不稳定）: https://gitee.com/cristime/MyStack

**欢迎Star或Fork，使用上有问题可以提Issue，我会不定期的查看（本人中学党QAQ）**

感谢Microsoft Visual Studio     <del>宇宙第一IDE果然名不虚传</del>
