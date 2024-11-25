变量
![](images/变量示意图.png)
在 C++ 中，变量是存储信息的地方。变量是计算机内存中的一个位置，您可以在其中存储值，并且稍后可以从中检索该值。

计算机的内存可以看作是一系列存储格。每个存储格都是许多排成一排的存储格中的一个。每个存储格（或内存位置）都按顺序编号。这些数字称为内存地址。变量保留一个或多个存储格，您可以在其中存储值。

变量的名称（例如，myVariable）是这些小隔间的标签，这样您就可以轻松找到它，而无需知道其实际内存地址。图 3.1 是此想法的示意图。从图中可以看出， myVariable从内存地址103开始​​。根据myVariable的大小，它可以占用一个或多个内存地址。

**注意：** RAM 是随机存取存储器。运行程序时，程序会从磁盘文件加载到 RAM 中。所有变量也在 RAM 中创建。程序员提到内存时，通常指的是 RAM。

**内存分配**

当你在 C++ 中定义一个变量时，必须告诉编译器这个变量的类型：是整数、字符等。这个信息告诉编译器需要分配多少内存以及你要在变量中存储什么类型的值。

每个存储单元的大小为一字节。如果你创建的变量类型占用两个字节，那么它需要两个字节的内存，或两个存储单元。变量的类型（例如，整数）告诉编译器需要为该变量分配多少内存（多少存储单元）。

#### 整数的大小

在任何一台计算机上，每种变量类型都占用一个固定不变的空间。也就是说，一个整数在一台机器上可能是两个字节，在另一台机器上可能是四个字节，但在两台计算机上，它始终是相同的，日复一日。

char变量（用于保存字符）通常为一个字节长。在大多数计算机上，短整型为两个字节，长整型通常为四个字节，而整型（不带关键字short或long）可以是两个或四个字节。清单 3.1 应该可以帮助您确定计算机上这些类型的确切大小。
**新术语：** 字符是占用一个字节内存的单个字母、数字或符号
![](images/变量占用字节数.png)


```cpp
#include <iostream>
using namespace std;
void main()
{
	cout << "int:"<<sizeof(int)<<"\n";
	cout << "short:" << sizeof(short) << "\n";
	cout << "long:" << sizeof(long) << "\n";
	cout << "char:" << sizeof(char) << "\n";
	cout << "float:" << sizeof(float) << "\n";
	cout << "double:" << sizeof(double) << "\n";
 }
输出：
int:4
short:2
long:4
char:1
float:4
double:8
```
有符号和无符号整数
此外，所有整数类型都有两种：有符号整数和无符号整数。这里的想法是，有时您需要负数，有时您不需要。没有“无符号”一词的整数（短整数和长整数）被认为是有符号的。有符号整数要么是负数，要么是正数。无符号整数始终为正数。

由于有符号整数和无符号整数的字节数相同，因此无符号整数 中可以存储的最大数字是带符号整数中可以存储的最大正数的两倍。无符号 短整数可以处理从 0 到 65,535 的数字。有符号 短整数表示的数字中有一半是负数，因此有符号 短整数只能表示从 -32,768 到 32,767 的数字。如果这令人困惑，请务必阅读附录 A“运算符优先级”。

**Table 3.1. Variable Types.**

|                       |            |                                 |
| --------------------- | ---------- | ------------------------------- |
| **_Type_**            | **_Size_** | **_Values_**                    |
| unsigned short int    | 2 bytes    | 0 to 65,535                     |
| short int             | 2 bytes    | -32,768 to 32,767               |
| unsigned long int     | 4 bytes    | 0 to 4,294,967,295              |
| long int              | 4 bytes    | -2,147,483,648 to 2,147,483,647 |
| int (16 bit)          | 2 bytes    | -32,768 to 32,767               |
| int (32 bit)          | 4 bytes    | -2,147,483,648 to 2,147,483,647 |
| unsigned int (16 bit) | 2 bytes    | 0 to 65,535                     |
| unsigned int (32 bit) | 2 bytes    | 0 to 4,294,967,295              |
| char                  | 1 byte     | 256 character values            |
| float                 | 4 bytes    | 1.2e-38 to 3.4e38               |
| double                | 8 bytes    | 2.2e-308 to 1.8e308             |
变量命名对比
```cpp
Example 1

main()
{
     unsigned short x;
     unsigned short y;
     ULONG z;
     z = x * y;
}
Example 2

main ()
{
     unsigned short Width;
     unsigned short Length;
     unsigned short Area;
     Area = Width * Length;
}
```
变量命名规则
**注意：** 许多高级程序员使用一种通常称为匈牙利表示法的符号样式。匈牙利表示法背后的理念是在每个变量前面加上一组描述其类型的字符。整数变量可能以小写字母 i 开头，长整型变量可能以小写字母 l 开头。其他符号表示常量、全局变量、指针等等。这些符号在 C 编程中更为重要，因为 C++ 支持创建用户定义类型（参见第 6 天“基本类”），并且 C++ 是强类型的。
#### 关键词

有些字是 C++ 的保留字，您不能将它们用作变量名。这些是编译器用来控制程序的关键字。关键字包括if、 while、for和main。您的编译器手册应该会提供完整列表，但通常，任何合理的变量名称几乎肯定不是关键字。

> ---
> 
> **定义变量时，请先**写类型，然后再写变量名。**请** 使用有意义的变量名。请记住，C++ 区分大小写。**请勿** 使用 C++ 关键字作为变量名。请了解每种变量类型在内存中占用的字节数，以及该类型的变量中可以存储什么值。 **请勿**对负数 使用无符号变量。

给变量定义别名

```cpp
typedef unsigned short int USHORT
```

```cpp
   // *****************
   // Demonstrates typedef keyword
   #include <iostream.h>

   typedef unsigned short int USHORT;       //typedef defined

   void main()
   {
     USHORT  Width = 5;
    USHORT Length;
    Length = 10;
    USHORT Area  = Width * Length;
    cout << "Width:" << Width << "\n";
    cout << "Length: "  << Length << endl;
    cout << "Area: " << Area <<endl;
 }
Output: Width:5
Length: 10
Area: 50
```

这些变量是环形的

```cpp
#include <iostream>
using namespace std;
void main()
{
	unsigned short int smallNumber;
	smallNumber = 65535;
	cout << "smallNumber:" << smallNumber << "\n";
	smallNumber++;
	cout << "smallNumber:" << smallNumber << "\n";
	smallNumber++;
	cout << "smallNumber:"<< smallNumber <<"\n";
 }
smallNumber:65535
smallNumber:0
smallNumber:1
```
根据数字打印字符ascii

```cpp
#include <iostream>
using namespace std;
int main()
{
	for (int i = 32; i < 128; i++)
	{
		cout << (char)i;
	}
	return 0;
 }
输出：
!"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
```

转意字符
\n新行
\t标签
\b退格键
\”双引号
\'单引号
\？问号
\\反斜杠

### 常量

与变量一样，常量是数据存储位置。与变量不同，顾名思义，常量不会改变。创建常量时必须初始化它，并且以后不能为其赋新值。

#### 文字常量

C++ 有两种类型的常量：文字和符号。

文字常量是直接在程序中需要的地方输入的值。例如

int 我的年龄 = 39;

myAge是int类型的变量；39是文字常量。您无法为39赋值，并且其值无法更改。
#### 符号常量

符号常量是用名称表示的常量，就像变量一样。但与变量不同的是，常量在初始化后，其值不能更改。

如果你的程序有一个名为students 的整型变量和另一个名为 classes 的整型变量，那么在已知班级数量的情况下，如果你知道每个班级有 15 名学生，你就可以计算出有多少名学生：

学生数=班级数*15；
在 C++ 中，有两种方法可以声明符号常量。旧的、传统的、现在已经过时的方法是使用预处理器指令#define。使用 #define 定义常量要以传统方式定义常量，
```cpp
#define studentsPerClass 15
```
因为预处理器在编译器之前运行，所以编译器永远看不到你的常量；它看到的是数字15。用 const 定义常量虽然 #define有效，但在 C++ 中还有一种新的、更好的定义常量的方法：
```cpp
const unsigned short int studentsPerClass = 15;
```

### 枚举常量

枚举常量使您可以创建新类型，然后定义这些类型的变量，这些变量的值被限制为一组可能的值。例如，您可以将COLOR声明为枚举，并且可以定义COLOR有五个值：RED、BLUE、GREEN、 WHITE和BLACK。

枚举常量的语法是先写关键字enum，然后是类型名称、一个左括号、用逗号分隔的每个合法值，最后是右括号和分号。以下是示例：
```cpp
enum COLOR { RED, BLUE, GREEN, WHITE, BLACK };
```

此语句执行两项任务：

1.将COLOR设为枚举的名称，即一种新类型。
2.将RED设为值为0的符号常量，将 BLUE 设为值为1 的符号常量，将 GREEN设为值为2 的符号常量，等等。

也可以初始化
```cpp
enum Color { RED=100, BLUE, GREEN=500, WHITE, BLACK=700 };
```

**枚举常量的演示**
```cpp
#include <iostream>
using namespace std;
int main()
{
	enum Days 
	{
		星期一,
		星期二,
		星期三,
		星期四,
		星期五,
		星期六,
		星期七
	};

	Days 星期假;
	int x;
	cout << "你想哪天休息（0-6）？\n";
	cin >> x;
	星期假 = Days(x);
	if (星期假 == 星期六 || 星期假 == 星期七) {
		cout << "你已经休息过了\n";
	}
	else
	{
		cout << "你必须去上班\n";
	}
 }
```