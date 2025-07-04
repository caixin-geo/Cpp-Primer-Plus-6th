# 第三章 处理数据

**面向对象编程（OOP）的本质是设计并扩展自己的数据类型。设计自己的数据类型就是让类型与数据匹配。**

内置的C++类型分两组：基本类型和复合类型。本章将介绍基本类型，即整数和浮点数。似乎只有两种类型，但C++知道，没有任何一种整型和浮点型能够满足所有的编程要求，因此对于这两种数据，它提供 了多种变体。

## 3.1 简单变量

把信息存储在计算机中，程序必须记录3个基本属性：

* 信息将存储在哪里； 
* 要存储什么值； 
* 存储何种类型的信息。

实际上，程序将找到一块能够存储整数的内存，将该内存单元标记为braincount，并将5复制到该内存单元中；然 后，您可在程序中使用braincount来访问该内存单元。

> 可以使用&运算符来检索braincount的内存地址。

### 3.1.1 变量名

C++ 提倡使用有一定含义的变量名，并遵循几 种简单的 C++ 命名规则：

* 在名称中只能使用字母字符、数字和下划线 ( _ )；
* 名称的第一个字符不能是数字；
* 区分大写字符与小写字符；
* 不能将C++关键字用作名称；
* 以*两个下划线* 或 *下划线+大写字母* 打头的名称被保留给实现（编译器及其使用的资源）使用；
* 以 *一个下划线* 开头的名称被保留给实现，用作全局标识符；

C++对于名称的长度没有限制，名称中所有的字符都有意义，但有些平台有长度限制。

> 倒数第二点与前面几点有些不同，因为使用像 __time_stop 或 _Donut 这样的名称不会导致编译器错误，而会导致行为的不确定性。换句话说，不知道结果将是什么。不出现编译器错误的原因是，这样的名称不 是非法的，但要留给实现使用。

![image-20210719213322578](https://static.fungenomics.com/images/2021/07/image-20210719213322578.png)

如果想用两个或更多的单词组成一个名称，通常的做法是用下划线字符将单词分开，如 my_onions (**用这类**)；或者从第二个单词开始将每个单词的第一个字母大写，如 myEyeTooth。

**在 C++ 所有主观的风格中，一致性和精度是最重要的**。请根据自己的需要、喜好和个人风格来使用变量名（或必要时，根据雇主的需要、喜好和个人风格来选择变量名）。

### 3.1.2 整型

不同C++整型使用不同的内存量来存储整数。使用的内存量越大，可以表示的整数值范围也越大。

C++的基本整型（按宽度递增的顺序排列）分别是char、short、int、long和C++11新增的long long，其中每种类型都有符号版本和无符号版本，因此总共有10种类型可供选择。

### 3.1.3 整型short、int、long和long long

C++ 的short、int、long和long long类型通过使用不同数目的位来存储值，最多能够表示4种不同的整数宽度：

* short至少16位；
* int至少与short一样长；
* long 至少32位，且至少与int一样长；
* long long至少64位，且至少与long一样长。

> 这意味着可以把16位单元设置成65 536个不同的值，把 32位单元设置成4 294 672 296个不同的值，把64位单元设置为18 446 744 073 709 551 616个不同的值。作为比较，unsigned long存储不了地球上当前的人数和银河系的星星数，而long long 能够。

当前很多系统都使用最小长度，即short为16位，long为32位。这仍然为int提供了多种选择，其宽度可以是16位、24位或32位，同时又符合标准；甚至可以是64位，因为long和long long至少长64位。

> 类型的宽度随实现而异，这可能在将C++程序从一种环境移到另一种环境（包括在同一个系统中使用不同编译器）时引发问题。

首先，sizeof运算符返回类型或变量的长度；其次，头文件climits（在老式实现中为limits.h）中包含了关于整型限制的信息。具体地说，它定义了表示各种限制的符号名称。例如，INT_MAX为int的最大取值，CHAR_BIT为字节的位数。

在我的 Macbook Air 64位 OS 上，数据类型是这样的: 

```bash
int is 4 bytes.
short is 2 bytes.
long is 8 bytes.
long long is 8 bytes.

Maximum values:
int: 2147483647
short: 32767
long: 9223372036854775807
long long: 9223372036854775807

Minimum int value = -2147483648
Bits per byte = 8
```

![image-20210719215348315](https://static.fungenomics.com/images/2021/07/image-20210719215348315.png)
![image-20210719215405073](https://static.fungenomics.com/images/2021/07/image-20210719215405073.png)

**赋值与声明合并在一起叫做初始化。**如果知道变量的初始值应该是什么，则应对它进行初始化。

如果不对函数内部定义的变量进行初始化，该变量的值将是不确定的。这意味着该变量的值 将是它被创建之前，相应内存单元保存的值。

![image-20210719215954131](https://static.fungenomics.com/images/2021/07/image-20210719215954131.png)


### 3.1.4 无符号类型

要创建 无符(正负)号版本 的基本整型，只需使用关键字 unsigned 来修改声明即可。注意，unsigned本身是unsigned int的缩写。
-无符号类型的表示范围（绝对值）是对应的有符号类型的1/2

### 3.1.5 选择整型类型

通常，int被设置为对 目标计算机而言最为“自然”的长度。自然长度（natural size）指的是计 算机处理起来效率最高的长度。如果没有非常有说服力的理由来选择其 他类型，则应使用int。

如果知道变量可能表示的整数值大于16位整数的最大可能值，则使用long。即使系统上int为32位，也应这样做。这样，将程序移植到16位系统时，就不会突然无法正常工作（参见图3.2）。如果要存储的值超过20亿，可使用long long。

> 所以对于基因组数据上的位置信息，最好是 long 类型咯，即便 unsigned int 类型已经足够。（不过我可能还是希望用 unsigned int ）

![image-20210719220858422](https://static.fungenomics.com/images/2021/07/image-20210719220858422.png)

如果short比int小，则使用short可以节省内存。通常，仅当有大型整 型数组时，才有必要使用short。如果只需要一个字节，可使用char。

### 3.1.6 整型字面值

整型字面值（常量）是显式地书写的常量，如212或1776。

> 诸如cout<<hex;等代码不会在屏幕上显示任何内容，而只是修改 cout显示整数的方式。因此，控制符hex实际上是一条消息，告诉cout采 取何种行为。另外，由于标识符hex位于名称空间std中，而程序使用了 该名称空间，因此不能将hex用作变量名。然而，如果省略编译指令 using，而使用std::cout、std::endl、std::hex和std::oct，则可以将hex用作 变量名。

### 3.1.7 C++如何确定常量的类型

![image-20210719221757664](https://static.fungenomics.com/images/2021/07/image-20210719221757664.png)

### 3.1.8 char类型：字符和小整数

char类型是专为存 储字符（如字母和数字）而设计的。

char类型是另一种整型。实际上，很多系统支持的字符都不超过128个，因此用一个字节就可以表示所有的符号。因此，虽然char最常被用来处理字符，但也可以 将它用做比short更小的整型。

C++对字符用单引号，对字符串使用双引号。 cout对象能够处理这两种情况，但正如第4章将讨论的，这两者有天壤之别）。

与int不同的是，char在默认情况下既不是没有符号，也不是有符号。是否有符号由C++实现决定，这样编译器开发人员可以最大限度地将这种类型与硬件属性匹配起来。如果char有某种特定的行为对您来说 非常重要，则可以显式地将类型设置为signed char 或unsigned char。

如果将char用作数值类型，则unsigned char和signed char之间的差异将非常重要。unsigned char类型的表示范围通常为0～255，而signed char 的表示范围为−128到127。

> 例如，假设要使用一个char变量来存储像200这样大的值，则在某些系统上可以，而在另一些系统上可能不可以。但 使用unsigned char可以在任何系统上达到这种目的。

如果大型字符 集是实现的基本字符集(如中文日文系统)，则编译器厂商可以将char定义为一个16位的字节或更长的字节。其次，一种实现可以同时支持一个小型基本字符集和 一个较大的扩展字符集。8位char可以表示基本字符集，另一种类型 wchar_t（宽字符类型）可以表示扩展字符集。wchar_t类型是一种整数类型，它有足够的空间，可以表示系统使用的最大扩展字符集。这种类 型与另一种整型（底层（underlying）类型）的长度和符号属性相同。对底层类型的选择取决于实现，因此在一个系统中，它可能是unsigned short，而在另一个系统中，则可能是int。



## 3.2 const 限定符

C++有一种比 `#define` 更好的处理符号常量的方法，这种方法就是使用 const 关键字来修改变量声明和初始化。

```Cpp
const int Months = 12;
```
常量（如Months）被初始化后，其值就被固定 了，编译器将不允许再修改该常量的值。如果您这样做，g++将指出程 序试图给一个只读变量赋值。关键字const叫做限定符，因为它限定了声 明的含义。

> #define 定义符号常量的方式应抛弃。

一种常见的做法是将名称的首字母大写，以提醒您Months是个常量。这决不是一种通用约定，但在阅读程序时有助于区分常量和变量。另一种约定是将整个名称大写，使用#define创建常量时通常使用这种约定。

**注意：** 如果在声明常量时没有提供值，则该常量的值将是不确定的，且无 法修改。

## 3.3 浮点数

使用浮点类型可以表示诸如2.5、3.14159和122442.32这样的数字，即带小数部分的数字。计算机将这样的值分成两部分存储。一部分表示值，另一部分用于对值进行放大或缩小。下面打个比方。对于数字34.1245和34124.5，它们除了小数点的位置不同外，其他都是相同的。 可以把第一个数表示为0.341245（基准值）和100（缩放因子），而将第二个数表示为0.341245（基准值相同）和10000（缩放因子更大）。缩放因子的作用是移动小数点的位置，术语浮点因此而得名。C++内部表示浮点数的方法与此相同，只不过它基于的是二进制数，因此缩放因 子是2的幂，不是10的幂。

### 3.3.1 书写浮点数

C++有两种书写浮点数的方式：
* 第一种是使用常用的标准小数点表示法；
* 第二种表示浮点值的方法叫做E表示法，其外观是像这样的： 3.45E6，这指的是3.45与1000000相乘的结果；E6指的是10的6次方，即 1后面6个0。因此，3.45E6表示的是3450000，6被称为指数，3.45被称为 尾数。

![image-20210719225234354](https://static.fungenomics.com/images/2021/07/image-20210719225234354.png)

E表示法确保数字以浮点格式存储，即使没有小数点。注意，既可 以使用E也可以使用e，指数可以是正数也可以是负数，不要有空格。

![image-20210719224852195](https://static.fungenomics.com/images/2021/07/image-20210719224852195.png)

> 电子的质量是 9.11e-31 kg 表示 0.000000000000000000000000000000911 kg， 而美国报警电话 911 竟然很巧合地与此相同。

### 3.3.2 浮点类型

C++也有3种浮点类型：float、double 和 long double。

事实上，C和C++对于有效位数的要求是，float至少32位，double至少48位，且不少于float，long double至少和double一样多。这三种类型的有效位数可以一样多。然而，通常，float为32位，double为64位， long double为80、96或128位。另外，这3种类型的指数范围至少是−37到37。可以从头文件cfloat或float.h中找到系统的限制。

### 3.3.3 浮点常量

在默认情况下，像8.24和2.4E8这样的浮点常量都属于double类型。如果希望常量为float类型，请使用f或F后缀。对于long double类型，可使用l或L后缀（由于l看起来像数字1，因此L是更好的选择）。

### 3.3.4 浮点数的优缺点

与整数相比，浮点数有两大优点。首先，可以表示整数之间的 值。其次，由于有缩放因子，它们可以表示的范围大得多。另一方面， **浮点运算的速度通常比整数运算慢，且精度将降低**。

如: 2.34E+22是一个小数点左边有23位的数字。加上1，就 是在第23位加1。但float类型只能表示数字中的前6位或前7位，因此修改第23位对这个值不会有任何影响。

## 3.4 C++算术运算符

![image-20210719230134697](https://static.fungenomics.com/images/2021/07/image-20210719230134697.png)

`11.17 + 50.25` 应等于61.42，但是输出的却是61.419998。这不是运算问题，而是由于float类型表示有效位数的能力有限。记住，对于float，C++只保证6位有效位。如果将 61.419998四舍五入成6位，将得到61.4200，这是在保证精度下的正确值，如果用double 则精度足够，所以直接可以获得 61.42 的值。

> 通常来说 double 都比 float 更精准，应尽量使用 double。

### 3.4.1 运算符优先级和结合性

算术运算符遵 循通常的代数优先级，先乘除，后加减。

### 3.4.2 除法分支

除法运算符（/）的行为取决于操作数的类型。如果两个操作数都 是整数，则C++将执行整数除法。这意味着结果的小数部分将被丢弃， 使得最后的结果是一个整数。**如果其中有一个（或两个）操作数是浮点 值，则小数部分将保留，结果为浮点数**。

![image-20210719230953958](https://static.fungenomics.com/images/2021/07/image-20210719230953958.png)

**浮点常量在默认情况下为 double类型。**

### 3.4.3 求模运算符

求模运算符返回整数除法的余数。它与整数除 法相结合，尤其适用于解决要求将一个量分成不同的整数单元的问题。

### 3.4.4 类型转换

由于有11种整型和3种浮点类型，因此计算机需 要处理大量不同的情况，C++自动执行很多类型转换：

* 将一种算术类型的值赋给另一种算术类型的变量时，C++将对值进 行转换； 
* 表达式中包含不同的类型时，C++将对值进行转换；
* 将参数传递给函数时，C++将对值进行转换。

C++允许将一种类型的值赋给另一种类型的变量。这样做时，值将 被转换为接收变量的类型。例如，假设so_long的类型为long，thirty的类 型为short。

将一个值赋给值取值范围更大的类型通常不会导致什么问题。如，将short值赋给long变量并不会改变这个值，只是占用的字节更多而 已。然而，将一个很大的long值（如2111222333）赋给float变量将降低 精度。因为float只有6位有效数字，因此这个值将被四舍五入为 2.11122E9。因此，有些转换是安全的，有些则会带来麻烦。

![image-20210719232005071](https://static.fungenomics.com/images/2021/07/image-20210719232005071.png)

如下的报错是一个可能:

![image-20210719232233106](https://static.fungenomics.com/images/2021/07/image-20210719232233106.png)

将0赋给bool变量时，将被转换为false；而非零值将被转换为true。

当同一个表达式中包含两种不同的算术类型时，将出现什么情况 呢？在这种情况下，C++将执行两种自动转换：首先，一些类型在出现 时便会自动转换；其次，有些类型在与其他类型同时出现在表达式中时 将被转换。

* 在计算表达式时，C++将bool、char、unsigned char、signed char和short值转换为int。具体地说，true被转换为1，false 被转换为0。这些转换被称为整型提升（integral promotion）。

![image-20210719232513015](https://static.fungenomics.com/images/2021/07/image-20210719232513015.png)

> int 是一种最自然的类型，运算速度也最快，要主用。

* 同样，wchar_t被提升成为下列类型中第一个宽度足够存储wchar_t 取值范围的类型：int、unsigned int、long或unsigned long。

* 将不同类型进行算术运算时，也会进行一些转换，例如将int和float 相加时。**当运算涉及两种类型时，较小的类型将被转换为较大的类型。**

![image-20210719232833549](https://static.fungenomics.com/images/2021/07/image-20210719232833549.png)

* 传递参数时的类型转换通常由C++函数原型控制。
* C++还允许通过强制类型转换机制显式地进行类型转换。强制类型转换 的格式有两种。如下：

![image-20210719233243273](https://static.fungenomics.com/images/2021/07/image-20210719233243273.png)

![image-20210719233319788](https://static.fungenomics.com/images/2021/07/image-20210719233319788.png)

**新格式的想法 是，要让强制类型转换就像是函数调用。这样对内置类型的强制类型转换就像是为用户定义的类设计的类型转换。**

更安全的转换方式是使用 `static_cast<typeName> (value)` 函数。

Stroustrup认为，C语言式的强制类型转换由于有过多的可能性而极 其危险，这将在第15章更深入地讨论。运算符 `static_cast<>` 比传统强制 类型转换更严格。

### 3.4.5 C++11中的auto声明

在初始化声明中，如果 使用关键字auto，而不指定变量的类型，编译器将把变量的类型设置成 与初始值相同。

![image-20210719234008239](https://static.fungenomics.com/images/2021/07/image-20210719234008239.png)

![image-20210719234059088](https://static.fungenomics.com/images/2021/07/image-20210719234059088.png)

## 3.5 总结

C++的基本类型分为两组：一组由存储为整数的值组成，另一组由存储为浮点格式的值组成。整型之间通过存储值时使用的内存量及有无符号来区分。整型从最小到最大依次是：bool、char、signed char、 unsigned char、short、unsigned short、int、unsigned int、long、unsigned long以及C++11新增的long long和unsigned long long。还有一种wchar_t 类型，它在这个序列中的位置取决于实现。C++11新增了类型char16_t 和char32_t，它们的宽度足以分别存储16和32位的字符编码。C++确保了char足够大，能够存储系统基本字符集中的任何成员，而wchar_t则可以存储系统扩展字符集中的任意成员，short至少为16位，而int至少与short一样长，long至少为32位，且至少和int一样长。确切的长度取决于 实现。

浮点类型可以表示小数值以及比整型能够表示的值大得多的值。3种浮点类型分别是float、double和long double。C++确保float不比double 长，而double不比long double长。通常，float使用32位内存，double使用 64位，long double使用80到128位。

对变量赋值、在运算中使用不同类型、使用强制类型转换时，C++将把值从一种类型转换为另一种类型。
