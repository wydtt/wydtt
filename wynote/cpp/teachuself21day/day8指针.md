###### 目标

```cpp
什么是指针。

如何声明和使用指针。

什么是自由存储（堆）以及如何操作内存。
```

###### 什么是指针

==指针是保存内存地址的变量。==
不同的计算机使用不同的复杂方案来编号此内存。通常程序员不需要知道任何给定变量的具体地址，因为编译器会处理细节。但是，如果您需要此信息，则可以使用地址运算符 ( & )，

int ×page=0;

==值为0的指针是空指针,未初始化的指针是野指针。==

unsigned short int howOld = 50; // 创建变量
unsigned short int * pAge = &howOld; // 创建指向 howOld 的指针

pAge是一个指针，现在包含howOld变量的地址 。使用pAge ，您实际上可以确定howOld的值，在本例中为50 。使用指针 pAge访问howOld称为间接访问，因为您是 通过pAge间接访问howOld 的。今天晚些时候您将看到如何使用间接访问变量的值。
###### 如何声明和使用指针。
定义指针要用p开头

```cpp


#include <iostream>
using namespace std;
int main(){
  int theVariable=5;
  int * pPointer=&theVariable;
  cout<<pPointer<<endl;
  cout<<*pPointer<<endl;
  cout<<&theVariable<<endl;
  cout<<&pPointer<<endl;
}
```
0x7fff494b8ebc
5
0x7fff494b8ebc
0x7fff494b8eb0
将theVariable的地址（&theVariable） 赋值为指针pPointer


###### 什么是自由存储（堆）以及如何操作内存。

内存的五个区域

- 全局命名空间（全局变量）
    
- 空闲存储（堆，空闲存储） new 
    
- 寄存器 （跟踪堆栈顶部和指令指针）
    
- 代码空间 （代码）
    
- 栈 （局部变量和函数参数） return 后自动清理
局部变量和函数参数都位于堆栈中。当然，代码位于代码空间中，全局变量位于全局名称空间中。寄存器用于内部管理功能，例如跟踪堆栈顶部和指令指针。几乎所有剩余内存都交给空闲存储，有时也称为堆。

没有内存条指出空闲存储，栈，全局命名空间在哪，以及寄存器是哪个部位，这些概念永远是空中楼阁毫无用处
警告：每次使用new 关键字分配内存时，都必须检查以确保指针不为空。
###### new

==new 在堆中，也就是空闲存储中，==
在 C++ 中，可以使用new关键字在空闲存储区中分配内存。new 后面跟着要分配的对象的类型，以便编译器知道需要多少内存。因此，new unsigned short int在空闲存储区中分配两个字节，new long分配四个字节。

==指针是局部变量，而指针指向的new 对象是一个堆（空闲区域）变量==
==new 返回的是内存地址需要赋值给一个指针==
new的返回值是一个内存地址。它必须被赋值给一个指针。要在自由存储中创建一个无符号 短整型，你可以这样写

==无法保证创建的对象的资源是否有限，如果用完了返回空指针，所以需要判空==
如果new无法在空闲存储中创建内存（内存毕竟是有限的资源），它将返回空指针。每次请求新内存时，都必须检查指针是否为空。

警告：每次使用new 关键字分配内存时，都必须检查以确保指针不为空

###### delete

new 分配的内存（堆内存，空闲区域内存）不会自动释放，该内存就无法使用，叫做内存泄漏。

==这部分泄漏的内存是在程序结束之前是无法使用的，我们必须使用delete来释放==

```cpp
delete pPointer;
```

我们删除指针的时候，是释放这个指针地址中的内存，将指向的内存返回到堆（空闲存储区域）

```cpp
分配使用和删除指针

#include <iostream>
using namespace std;
int main(){
    int localVariable=5;
    int *pLocal=&localVariable;
    int * pHeap = new int;
    //没有足够的内存供pHeap使用
    if(pHeap==NULL){
        cout<<"Not enough memory for pHeap";
        return 0;
    }
    *pHeap=7;
    cout<<"localVariable="<<localVariable<<endl;
    cout<<"*pLocal="<<*pLocal<<endl;
    cout<<"*pHeap="<<*pHeap<<endl;
    // 释放pHeap指向的内存
    delete pHeap;
    pHeap = new int;
    // 检查是否分配成功
    if(pHeap==NULL){
        cout<<"Not enough memory for pHeap";
        return 0;
    }
    *pHeap=9;
    cout<<"*pHeap="<<*pHeap<<endl;
    delete pHeap;
    return 0;
}
```

```cpp
指针赋值之前都应该释放一下预防泄漏
1: unsigned short int * pPointer = new unsigned short int;
2: *pPointer = 72;
3: delete pPointer;
4: pPointer = new unsigned short int;
5: *pPointer = 84;
```
第三行必须要先释放指针
注意： 每次在程序中调用new时，都应该调用delete。跟踪哪个指针拥有内存区域并确保在使用完内存后将其返回到空闲存储区非常重要。

==在堆（空闲内存）中创建对象==

Cat *pCat = new Cat;
这将调用默认构造函数——不带任何参数的构造函数。每当创建对象时（在堆栈上或在自由存储中），都会调用该构造函数。

###### 删除对象

```cpp

#include <iostream>
using namespace std;
class SimpleCat{
    public:
    SimpleCat();
    ~SimpleCat();
    private:
    int itsAge;
};

SimpleCat::SimpleCat(){
    cout<<"SimpleCat 构造函数已调用...\n";
    itsAge = 1;
}

SimpleCat::~SimpleCat(){
    cout<<"SimpleCat 析构函数已调用...\n";
}
int main(){
//在自由存储中创建和删除对象
    cout<<"simplecat 活泼的猫\n";
    SimpleCat simplecat;
    cout<<"simpleCat *pRags = new SimpleCat();\n";
    SimpleCat *pRags = new SimpleCat;
    cout<<"delete pRags;\n";
    delete pRags;
    cout<<"退出，观察frisky运行\n";
    return 0;
}
simplecat 活泼的猫
SimpleCat 构造函数已调用...
simpleCat *pRags = new SimpleCat();
SimpleCat 构造函数已调用...
delete pRags;
SimpleCat 析构函数已调用...
退出，观察frisky运行
SimpleCat 析构函数已调用...

```

第一次析构函数是在delete pRags; 调用的 用来删除这个new SimpleCat
第二次析构函数 是在局部变量simplecat 超出其作用域析构函数被调用。

###### 访问数据成员

```cpp
 (*pRags).GetAge();
```
就这个意思，
	这样写很麻烦于是cpp使用

```cpp
pRags->GetAge();
```


访问堆中的对象的成员数据==使用指针==   Frisky->GetAge()
```cpp

#include <iostream>
using namespace std;
class simplecat{
public:
simplecat(){
    itsAge=2;
}
~simplecat(){}
int GetAge() const{
    return itsAge;
}
void SetAge(int age){
    itsAge=age;
}
private:
int itsAge;
};
int main(){
    simplecat *Frisky=new simplecat;
    cout<<"Frisky is "<<Frisky->GetAge()<<" years old"<<endl;
    Frisky->SetAge(5);
    cout<<"Frisky is "<<Frisky->GetAge()<<" years old"<<endl;
    delete Frisky;
    return 0;
}
```

this 指针

```cpp

#include <iostream>
using namespace std;

class Rectangle{
    public:
    Rectangle();
    ~Rectangle();
    void setLength(int length){
        this->itsLength=length;
    }
    int GetLength() const{
        return this->itsLength;
    }
    void setwidth(int width){
        this->itsWidth=width;
    }
    int GetWidth() const{
        return this->itsWidth;
    }
    private:
    int itsLength;
    int itsWidth;
};

Rectangle::Rectangle(){
    itsLength=5;
    itsWidth=10;
}

Rectangle::~Rectangle(){
    cout<<"Rectangle 析构函数已调用"<<endl;
}

int main(){
    Rectangle theRect;
    cout<<"theRect的长度为："<<theRect.GetLength()<<endl;
    cout<<"theRect的宽度为："<<theRect.GetWidth()<<endl;
    theRect.setLength(20);
    theRect.setwidth(10);
    cout<<"theRect的长度为："<<theRect.GetLength()<<endl;
    cout<<"theRect的宽度为："<<theRect.GetWidth()<<endl;
    return 0;
}
```

==不必担心创建或删除this指针。编译器会处理这些事情。==

##### 流浪指针或悬空指针

```cpp
简而言之，在调用delete后，请小心不要使用指针 。指针仍指向旧的内存区域，但编译器可以随意将其他数据放在那里；使用指针可能会导致程序崩溃。更糟糕的是，您的程序可能会顺利运行，几分钟后就会崩溃。这被称为定时炸弹，一点也不好玩。为了安全起见，删除指针后，将其设置为null ( 0 )。这会解除指针的武装。
```

注：流浪指针被称为野指针

故意创建一个流浪指针
```cpp
#include <iostream>
typedef unsigned short int USHORT; 
int main(){
    USHORT * pInt = new USHORT;
    *pInt = 10;
    std::cout<<"*pInt ="<<*pInt<<std::endl;
    delete pInt;
    pInt = 0;
    long * pLong = new long;
    *pLong = 90000;
   std::cout<<"*pLong ="<<*pLong<<std::endl;
    *pInt=20;//这个已经被删除了
    std::cout<<"*pInt ="<<*pInt<<std::endl;
    std::cout<<"*pLong ="<<*pLong<<std::endl;
    delete pLong;
    pLong = 0;
    return 0;
}

*pInt =10
*pLong =90000
Segmentation fault (core dumped)
```

注：请使用new在自由存储中创建对象。请使用delete 在自由存储中销毁对象并返回其内存。不要忘记用delete语句平衡所有new语句。不要忘记为调用delete 的所有指针 分配null ( 0 ) 。请检查new返回的值。

###### const指针

```cpp

const int * pOne;
int * const pTwo;
const int * const pThree;
pOne是指向常量整数的指针。指向的值不可改变。

pTwo是指向整数的常量指针。整数可以改变，但pTwo不能指向其他任何值。

pThree是指向常量整数的常量指针。指向的值不可更改，并且pThree不可更改为指向其他任何值。

保持这种状态的诀窍是查看关键字const的右侧 ，找出被声明为常量的内容。如果类型位于关键字的右侧，则该值是常量。如果变量位于关键字 const的右侧，则指针变量本身是常量。

const int * p1; // 指向的 int 是常量
int * const p2; // p2 是常量，它不能指向其他任何东西
```

使用指向const对象的指针
```cpp
#include <iostream>
using namespace std;
class Rectangle{
    public:
    Rectangle();
    ~Rectangle();
    void setLength(int length){
        itsLength=length;
    }
    int GetLength() const{
        return itsLength;
    }
    void setWidth(int width){
        itsWidth=width;
    }
    int GetWidth() const{
        return itsWidth;
    }
    private:
    int itsLength;
    int itsWidth;
};

Rectangle::Rectangle():itsWidth(5),itsLength(10){}

Rectangle::~Rectangle(){
    cout<<"Rectangle 析构函数已调用"<<endl;
}

int main(){
    Rectangle *pRect=new Rectangle;
    const Rectangle *pConstRect=new Rectangle;
    Rectangle * const pConstPtr=new Rectangle;
    cout<<"pRect的宽度为："<<pRect->GetWidth()<<endl;
    cout<<"pConstRect的宽度为："<<pConstRect->GetWidth()<<endl;
    cout<<"pConstPtr的宽度为："<<pConstPtr->GetWidth()<<endl;
    pRect->setWidth(10);
    pConstPtr->setWidth(10);
    cout<<"pRect的宽度为："<<pRect->GetWidth()<<endl;
    cout<<"pConstRect的宽度为："<<pConstRect->GetWidth()<<endl;
    cout<<"pConstPtr的宽度为："<<pConstPtr->GetWidth()<<endl;
    return 0;
}

pRect的宽度为：5
pConstRect的宽度为：5
pConstPtr的宽度为：5
pRect的宽度为：10
pConstRect的宽度为：5
pConstPtr的宽度为：10
```

这个代码只要看懂一点pConstRect的宽度为：5 没有被修改，不能被修改，是因为const Rectangle *pConstRect=new Rectangle; 对象Rectangle 左边是const 

###### 总结

```cpp
指针提供了一种强大的间接访问数据的方法。每个变量都有一个地址，可以使用地址运算符 ( & )获取。该地址可以存储在指针中。

指针的声明方式是先写出指向对象的类型，然后是间接运算符 ( * ) 和指针的名称。应将指针初始化为指向某个对象或指向null ( 0 )。

您可以使用间接运算符 ( * )访问存储在指针中的地址处的值。您可以声明const指针（不能重新分配以指向其他对象）和指向const对象的指针（不能用于更改其指向的对象）。

要在空闲存储区创建新对象，请使用new关键字并将返回的地址分配给指针。通过调用指针上的delete关键字释放该内存。delete会释放内存，但不会销毁指针。因此，必须在释放内存后重新分配指针。

```

概括代码
```cpp
#include <iostream>
using namespace std;

int main() {
    int value = 42;
    int* ptr = &value; // 声明一个指向 int 类型的指针，并初始化为 value 的地址

    cout << "Value: " << value << endl;
    cout << "Address of value: " << &value << endl;
    cout << "Value pointed by ptr: " << *ptr << endl;

    *ptr = 100; // 通过指针修改 value 的值

    cout << "New value: " << value << endl;

    delete ptr; // 释放指针所指向的内存
    ptr = nullptr; // 将指针设置为 nullptr，以避免悬挂指针

    return 0;
}
```


```cpp
1. 用于确定变量地址的运算符是`&`，称为地址运算符或取地址运算符。它返回变量的内存地址。例如，`&variable`将给出变量`variable`的内存地址。

2. 用于查找指针中保存的地址处存储的值的运算符是`*`，称为解引用运算符或间接运算符。它允许你访问指针所指向的内存地址中的值。例如，`*pointer`将给出指针`pointer`所指向的内存地址中的值。

3. 指针是一个变量，它存储了另一个变量的内存地址。指针可以指向任何数据类型，包括基本数据类型（如整数、字符等）和用户自定义的数据类型（如结构体、类等）。通过指针，可以间接访问和操作它所指向的变量。

4. 指针中存储的地址是一个内存位置的标识符，它指向某个变量或对象在内存中的位置。而该地址处的值是存储在该内存位置的数据。指针本身只是一个地址，而不是数据本身。通过解引用指针，可以访问和修改存储在该地址处的值。

5. 间接运算符`*`和解引用运算符`&`的区别在于它们的作用和使用场景：
   - `*`（解引用运算符）：用于访问指针所指向的内存地址中的值。它是一个一元运算符，放在指针变量的前面，表示获取指针所指向的内存地址中的值。
   - `&`（地址运算符）：用于获取变量的内存地址。它是一个一元运算符，放在变量的前面，表示获取变量的内存地址。

6. `const int * ptrOne`和`int * const ptrTwo`的区别在于它们对指针和指针所指向的内容的限制：
   - `const int * ptrOne`：这是一个指向`const int`类型的指针，即指针指向的是一个常量整数。`ptrOne`本身可以指向不同的`const int`变量，但不能通过`ptrOne`来修改它所指向的整数的值。
   - `int * const ptrTwo`：这是一个指向`int`类型的常量指针，即指针本身是一个常量，不能指向其他的内存地址。但是，可以通过`ptrTwo`来修改它所指向的整数的值。

总结来说，`const int *`限制了指针所指向的内容不能被修改，而`int * const`限制了指针本身不能被重新赋值指向其他地址。
```

练习
如果您有一个名为yourAge的无符号短整型变量，您将如何声明一个指针来操作yourAge？

```cpp
unsigned short int *pyourAge=&yourAge;
```

编写一个小程序，声明一个整数和一个指向整数的指针。将整数的地址赋给指针。使用指针在整数变量中设置一个值。
```cpp
#include <iostream>
int main(){
	int theInteger;
	int *pInteger = &theInteger;
	*pInteger = 5;
}
```

