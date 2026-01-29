---
title: C++ OOP 简介
katex: true
tag:
  - OOP
categories:
  - 计算机科学
description: 我们以 C++ 为例子介绍一下 OOP 的基本内容，虽然可能不甚详尽。
abbrlink: 59551c6a
date: 2026-01-28 10:00:00
updated: 2026-01-28 10:00:00
---

月底多更新几篇文章，一定会做到的。

## 前置知识

有些东西在算法竞赛中用的比较少，这里重写一下。

### 构造与析构

对象在被创建时会执行构造函数，被删除时会执行析构函数。

### 动态内存分配

我们可以使用 `Animal *rt = new Animal` 来新建一个

```cpp
#include <iostream>

using std::cout;

int val = 0;
class Animal {
protected:
    string brand;
public:
    Animal() {
        cout << "Object has been created " << ++val << '\n';
    }
    ~Animal() {
        cout << "Oops! Object has been deleted! Hahaha!!!\n";
    }
    void fun(void) {
        cout << "Funny!!!\n";
    }
};

int main(void) {
    Animal *rt = new Animal;
    rt->fun();
    delete rt;
    return 0;
}
```

会产生如下输出：

```sh
Object has been created 1
Funny!!!
Oops! Object has been deleted! Hahaha!!!
```

注意一个问题，`delete` 只会释放指针指向的内存，并不会将该指针赋值为 `nullptr`，此时该指针会变为悬空指针（Dangling Pointer），访问它是非常危险的。

未被初始化的指针称为野指针（Wild Pointer）。

对于数组的动态内存分配：

```cpp
int *array = new int [m];
 
delete [] array;

// 二维数组
int **array = new int *[m];
for (int i = 0; i < m; ++i) {
    array[i] = new int [n];
}
for (int i = 0; i < m; ++i) {
    delete [] array[i];
}
delete [] array;
```

### 友元函数

访问权限对友元函数没有影响，在类外定义时不需要 `friend` 关键字。

常见的用途是重在输入输出流运算符。

```cpp
#include <iostream>
using namespace std;

class Point {
private:
    int x, y;
public:
    Point(int x = 0, int y = 0) : x(x), y(y) {}
    friend istream& operator>>(istream& is, Point& p);
    friend ostream& operator<<(ostream& os, const Point& p);
};

// 实现重载 <<
ostream& operator<<(ostream& os, const Point& p) {
    os << "Point(" << p.x << ", " << p.y << ")";
    return os; // 必须返回流引用，支持链式调用
}
istream& operator>>(istream& is, Point& p) {
    is >> p.x >> p.y;
    return is;  // 必须返回流引用
}

int main(void) {
    Point p1;
    cin >> p1;
    cout << p1 << endl;

    return 0;
}
```

### 常量

首先是 `const` 与指针结合：

```cpp
int value = 10;
int other = 20;

// 1. 指向常量的指针 - 数据不可变，指针可变
const int* ptr1 = &value;
// *ptr1 = 30;        // 错误：不能修改指向的数据
ptr1 = &other;       // 正确：可以改变指针指向

// 2. 常量指针 - 指针不可变，数据可变
int* const ptr2 = &value;
*ptr2 = 30;          // 正确：可以修改指向的数据
// ptr2 = &other;    // 错误：不能改变指针指向

// 3. 指向常量的常量指针 - 都不可变
const int* const ptr3 = &value;
// *ptr3 = 30;       // 错误：不能修改数据
// ptr3 = &other;    // 错误：不能改变指针

// 记忆技巧：从右向左读
// const int* ptr   -> ptr 是指向 const int 的指针
// int* const ptr   -> ptr 是 const 指针，指向 int
```

然后是引用：

```cpp
int x = 5;

// 常量引用：不能通过引用修改原值
const int& ref = x;
// ref = 10;         // 错误
x = 10;              // 正确：原变量仍然可以修改
```

函数前加上 `const` 可以明确其返回的是一个常量。

类中函数后加上 `const` 表示不修改对象状态（除了 `mutable` 成员）。

### 静态

在函数内部声明的 `static` 变量只初始化一次，保持值不变，存储在静态存储区。

静态全局变量表明只有在该文件内可见。

类的静态成员变量属于类本身而不是某个对象。变量必须在类外定义。

```cpp
class Employee {
private:
    std::string name;
    static int totalEmployees;

    // 或者使用
    // inline static int totalEmployees = 0;
    
public:
    Employee(const std::string& n) : name(n) {
        totalEmployees++;
    }
    
    ~Employee() {
        totalEmployees--;
    }
};

int Employee::totalEmployees = 0;
```

同理，静态成员函数没有 `this` 指针，不能访问非静态成员。

## 继承与多态

继承可以基于已有的类创建新类。`private` 只能在基类中访问，`protected` 可以在派生的子类中访问。

继承分为三种，常用的是 `public` 继承。

- 公有继承（public）：当一个类派生自公有基类时，基类的公有成员也是派生类的公有成员，基类的保护成员也是派生类的保护成员，基类的私有成员不能直接被派生类访问，但是可以通过调用基类的公有和保护成员来访问。
- 保护继承（protected）： 当一个类派生自保护基类时，基类的公有和保护成员将成为派生类的保护成员。
- 私有继承（private）：当一个类派生自私有基类时，基类的公有和保护成员将成为派生类的私有成员。

构造析构函数、重载运算符、友元函数不会被继承。

支持多继承，长这样：

```cpp
class <派生类名>:<继承方式1><基类名1>,<继承方式2><基类名2>, {
    <派生类类体>
};
```

继承时会先调用基类的构造函数，然后是派生类的构造函数。删除时先调用派生类的析构函数，再调用基类的析构函数。

```cpp
#include <iostream>
using namespace std;

class Animal {
    protected:
        int width, height;
    public:
        Animal(int x, int y) {
            this->width = x, this->height = y;
            cout << "Designing Animal!!\n";
        }
        ~Animal() {
            cout << "Sorry, Animal has been removed\n";
        }
};

class Dog : public Animal {
    public:
        Dog(int x, int y) : Animal(x, y) {
            cout << "I have made a dog!\n";
        }
        ~Dog() {
            cout << "Oh no! My dog has gone:(\n";
        }
        int fat(void) { return width * height; }
};

int main(void) {
    Dog* p; p = new Dog(2, 3);
    cout << p->fat() << '\n';
    delete p;
    return 0;
}
```

```sh 输出
Designing Animal!!
I have made a dog!
6
Oh no! My dog has gone:(
Sorry, Animal has been removed
```

`static` 变量会被继承，是共用的。

### 虚函数

基类中可以声明一个函数为虚函数，这样派生类就可以重写这个虚函数。

使用 `= 0` 将其定义为纯虚函数。

```cpp
#include <iostream>
#include <queue>
using namespace std;

priority_queue<int> q;

class Animal {
    public:
        virtual void sound(void) {
            cout << "Animal make a sound.\n";
        }
        void sound(int x) {
            cout << x << '\n';
        }
};

class Dog : public Animal {
    public:
        void sound(void) override {
            cout << "Dog barks\n";
        }
};

int main(void) {
    Animal* ptr;
    ptr = new Dog;
    ptr->sound(5);
    ptr->sound();
    ptr = new Animal;
    ptr->sound();
    return 0;
}
```

```sh 输出
5
Dog barks
Animal make a sound.
```

此时如果要写析构函数，基类的析构函数应该是虚函数，否则 Animal 指针 delete 的时候会调用 Animal 的析构函数而不是 Dog 的。使用虚析构函数就可以正常先调用派生类的析构函数再调用基类的析构函数。

拥有纯虚函数的类称为**抽象类**。

这里可以看出，多态的“多种形态”指的是基类派生出的多种子类。

### 数据抽象

数据抽象是指，只向外界提供关键信息，并隐藏其后台的实现细节，即只表现必要的信息而不呈现细节。比如 `sort` 函数。

### 数据封装

数据封装是关于保护数据，防止直接访问，通过公共方法提供受控的访问。通过 `private` 等实现。

## 总结

嗯，感觉我什么也没写。