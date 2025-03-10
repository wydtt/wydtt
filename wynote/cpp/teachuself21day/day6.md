==类扩展了 C++ 的内置功能，以帮助您表示 以及解决复杂的实际问题。今天你会学到==

- ==什么是类和对象。==
    
- ==如何定义新类并创建该类的对象。==
    
- ==什么是成员函数和成员数据。==
    
- ==什么是构造函数以及如何使用它们。==

##### 什么是类和对象。
 ```cpp
Creating New Types
这些变量的类型告诉您：

它们在内存中的大小。

他们可以保存哪些信息。

可以对他们执行哪些操作。
```
```cpp
Why Create a New Type?
编写程序通常是为了解决实际问题，例如保持跟踪 的员工记录或模拟供暖系统的运作。虽然它是 可以通过使用仅使用整数编写的程序来解决复杂问题，并且 角色，如果您可以创建 您正在讨论的对象的表示形式。换句话说，模拟 如果您可以创建表示 房间、热传感器、恒温器和锅炉。这些变量的对应度越高 实际上，编写程序就越容易。
```
```cpp
Classes and Members
您可以通过声明一个类来创建新类型。类只是变量的集合 - 通常 的 -- 与一组相关函数相结合。

将汽车视为车轮、车门、座椅、车窗、 等等。另一种方法是考虑汽车可以做什么：它可以移动、速度 Up、slow down、Stop、Park 等。类使您能够封装或捆绑、 这些不同的部分和各种函数集成到一个集合中，称为 对象。

将您所了解的有关汽车的所有信息归入一个类别具有许多优势 对于程序员来说。一切都在一个地方，这使得引用、复制、 并处理数据。同样，类的客户端（即 程序 - 可以使用您的对象，而不必担心其中的内容 或者它是如何运作的。

一个类可以由变量类型的任意组合组成，也可以由其他类组成 类型。类中的变量称为成员变量或 data 成员。Car 类可能具有表示座椅、 无线电类型、轮胎等。

New Term: 成员变量 ，也 称为 数据成员 ，是类中的变量。成员变量 是您类别的一部分，就像车轮和发动机是您汽车的一部分一样。
类中的函数通常操作成员变量。他们是 称为类的成员函数或方法。汽车的方法 类可能包括 Start（） 和 Brake（）。Cat 类可能 具有表示年龄和体重的数据成员;它的方法可能包括 Sleep（）、 Meow（） 和 ChaseMice（） 的 ChaseMice（） 进行匹配。

New Term: 成员函数 ，也 称为 methods 的函数是类中的函数。成员函数是 作为成员变量的一部分。它们确定对象 你的班级可以做到。


```
##### 如何定义新类并创建该类的对象。
```cpp
Declaring a Class
要声明类，请使用 class 关键字，后跟左大括号 ，然后列出该类的数据成员和方法。以 一个右大括号和一个分号。下面是一个名为 Cat 的类的声明：

class Cat
{
unsigned int  itsAge;
unsigned int  itsWeight;
Meow();
};
声明此类不会为 Cat.它只是在讲述 编译器 Cat 是什么，它包含什么数据（itsAge 和 itsWeight）， 以及它能做什么 （Meow（））。它还告诉编译器 Cat 有多大 是 - 即，编译器必须为每个 Cat 留出多少空间 您创建。在此示例中，如果整数是 2 个字节，则 Cat 只有 4 个 bytes big：itsAge 是 2 个字节，itsWeight 是另外 2 个字节。 Meow（） 不占用任何空间，因为没有为 member 预留存储空间 函数 （方法） 。

```
编码风格：
```cpp
编码风格：
作为程序员，您必须命名所有成员变量、成员函数和 类。正如您在第 3 天的 “变量和常量” 中学到的那样，这些应该 易于理解且有意义的名称。Cat、Rectangle 和 员工是很好的类名。 Meow（）、ChaseMice（） 和 StopEngine（） 是很好的函数名称，因为它们告诉你函数是什么 做。许多程序员使用前缀 its 命名成员变量，如 itsAge、itsWeight 和 itsSpeed。这有助于区分 来自非成员变量的成员变量。

C++ 区分大小写，所有类名都应遵循相同的模式。那 这样你就不必检查如何拼写你的类名;是 Rectangle 吗， rectangle 还是 RECTANGLE？一些程序员喜欢在每个 类名（class name）替换为特定字母（例如 cCat 或 cPerson），而 其他组织将名称全部大写或全部小写。我使用的约定 是用首字母大写命名所有类，如 Cat 和 Person。

同样，许多程序员以大写字母和所有变量开始所有函数 替换为小写。单词通常用下划线分隔（如 Chase_Mice 中）或 将每个单词大写，例如 ChaseMice 或 DrawCircle。

重要的思想是你应该选择一种风格并坚持下去 每个程序。随着时间的推移，您的风格将演变为不仅包括命名约定、 还有缩进、大括号对齐和注释样式。


NOTE: 这在开发公司中很常见 为许多风格问题制定内部标准。这可确保所有开发人员都可以 轻松阅读彼此的代码。
```

定义对象
```cpp
定义新类型的对象就像定义整数变量一样：

unsigned int GrossWeight;         // define an unsigned integer
Cat Frisky;                       // define a Cat
此代码定义了一个名为 Gross Weight 的变量，其类型为 unsigned 整数。它还定义了 Frisky，这是一个对象，其类（或类型） 是 Cat。
```
类和对象
```cpp
你从不抚摸猫的定义；你抚摸的是单个的猫。你区分了猫的概念和现在正在客厅里掉毛的那只猫。同样，C++ 区分了 Cat 类（猫的概念）和每个单独的Cat对象。因此，Frisky 是Cat类型的对象，就像GrossWeight是 unsigned int类型的变量一样。

新术语：对象是类的单独实例。
```
访问类成员
```cpp
定义实际的Cat对象（例如 Frisky）后，可以使用点运算符 ( . ) 访问该对象的成员。因此，要将 50 分配给 Frisky 的Weight成员变量，您可以这样写

Frisky.体重 = 50;
同样，要调用Meow()函数，你可以这样写

Frisky.Meow();
使用类方法时，可以调用该方法。在此示例中，您正在 Frisky 上 调用Meow() 。
```
定义类
```cpp
class Cat
{
public:
unsigned int Age;
unsigned int Weight;
void Meow();
};

Cat  Frisky;
Frisky.Age = 8;
Frisky.Weight = 18;
Frisky.Meow();

```

实现类
```cpp

#include<iostream>
using namespace std;

class Cat {
public:
	int getAge();
	void setAge(int age);
	void Meow();
private:
	int itsAge;
};

int Cat::getAge() {
	return itsAge;
}
void Cat::setAge(int age) {
	itsAge = age;
}
void Cat::Meow() {
	cout << "meow\n";
}

int main() {
	Cat j;
	j.setAge(5);
	j.Meow();
	cout << j.getAge();
	return 0;
}
```
##### 什么是成员函数和成员数据。
void SomeFunction（）const；
如果将类方法声明为 const，则表示您承诺该方法不会更改类的任何成员的值。
SetAge()不能是const ，因为它会更改成员变量 itsAge。另一方面，GetAge()可以且应该是const， 因为它根本不会更改类。GetAge ()仅返回成员变量itsAge的当前值。因此，这些函数的声明应如下所示：
void SetAge(int anAge); 
int GetAge() const;
##### 什么是构造函数以及如何使用它们。

一定要将类声明放在 HPP 文件中，将成员函数放在 CPP 文件中。一定要尽可能使用const 。一定要在继续之前了解类。

今天，你学习了如何创建新的数据类型（称为类）。你学习了如何定义这些新类型的变量（称为对象）。

类有数据成员，即各种类型的变量，包括其他类。类还包括成员函数（也称为方法）。您可以使用这些成员函数来操作成员数据并执行其他服务。

类成员（包括数据和函数）可以是公共的或私有的。公共成员可供程序的任何部分访问。私有成员仅可供类的成员函数访问。

将类的接口或声明隔离在头文件中是一种很好的编程习惯。您通常在扩展名为.HPP 的文件中执行此操作。类方法的实现写在扩展名为.CPP的文件中 。

类构造函数初始化对象。类析构函数销毁对象，通常用于释放类方法分配的内存。


看过之后感觉cpp太麻烦了，还要定义函数原型，或者函数接口到头文件，这个cpp的作者脑子里有泡
以及const问题，

测验
2. 哪个会留出内存——声明还是定义？

变量定义会留出内存。类的声明不会留出内存。
3. 类的声明是它的接口还是它的实现？

类的声明是它的接口；它告诉类的客户端如何与类交互。类的实现是存储的成员函数集——通常存储在相关的 CPP 文件中。

学迷糊了