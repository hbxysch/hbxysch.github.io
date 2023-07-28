# C++ basic knowledge for interview
## const
1. const int a; 常对象成员，初始化列表+类内初始化，常量需要声明即初始化。
2. const A a；常对象，只能调用常成员函数
3. const A *p；指针变量，指向常对象
4. const A &p = a; 指向常对象的引用
5. char greeting[] = "Hello"; const char* p = greeting；指针变量，指向字符数组常量
6. char* const p = greeting; 常量指针，指向字符数组变量
7. const int* function1(); 返回指向常量的指针变量
8. int* const function2(); 返回指向int变量的常量指针

## 宏定义#define和const
#define相当于字符替换，无类型安全检查，不分配内存，存储在代码段，可以通过#undef取消；const是常量声明，有类型安全检查，分配内存，存储在数据段，不可取消

## static作用
1. 修饰普通变量：存储在静态区，在main函数之前即分配好内存空间
2. 修饰普通函数：仅在定义该函数的文件中才能使用，防止命名冲突
3. 修饰成员变量：使所有对象只保存一个该变量，而且不用创建对象即可访问
4. 修饰成员函数：只能访问静态成员，不用创建对象即可以访问该函数

## this指针
this指针是隐藏在每个非静态成员函数中的指针，指向调用该成员函数的那个变量

## inline内联函数
省去了调用函数的成本，也就是不进入函数直接执行函数体；编译器不会内联包括循环递归等复杂操作的函数；类内定义函数除了虚函数都会隐式内联，类外定义函数需要显式内联；虚函数表现为多态的时候不能内联。   
inline函数可以提高运行效率，但是以代码膨胀（复制）为代价。

## volatile
volatile表示变量可能会被编译器不知道的因素（操作系统，硬件或者其他线程）修改，因此每次使用必须从内存中取值，而不是由于CPU的优化从寄存器中取值。

## sizeof()
sizeof（）对数组会得到整个数组的长度，对指针会得到指针占用内存大小

## extern
在一个文件中定义了变量和函数，在其他文件中要使用，有以下两种方式：
1. 添加头文件
2. 在其他文件中使用extern关键字声明

extern可以使得变量和函数在全作用域可见。

## struct和typedef struct
C language
```
typedef struct Student {
    int age;
} S;
```
等价于
```
struct Student {
    int age;
};
typedef struct Student S;
```
这里S相当于struct Student的别名
C++中使用struct定义之后可以直接使用Student创建结构体，但是如果有同名函数，Student（）代表函数，需要用struct Student me；这样来创建结构体。   
C++中结构体可以用来存储数据，特别是当所有成员都是public的时候，建议不用class而用struct

## explicit关键字

## using