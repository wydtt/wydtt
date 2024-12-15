```java
有哪些参考资料。

引用与指针的区别。

如何创建引用并使用它们。

参考文献的局限性是什么。

如何通过引用将值和对象传入和传出函数。

```

###### 什么是引用

引用是一个别名；创建引用时，会用另一个对象（即目标）的名称对其进行初始化。从那一刻起，引用就充当了目标的替代名称，对引用执行的任何操作实际上都是对目标执行的。

创建引用的方法是，先写出目标对象的类型，然后是引用运算符 ( & )，最后是引用的名称。引用可以使用任何合法的变量名，但在本书中，我们将在所有引用名前加上“r”。因此，如果您有一个名为someInt 的整数变量，则可以通过以下方式引用该变量：
```cpp
int &rSomeRef = someInt;
```

演示引用的使用
```cpp
#include <iostream>
using namespace std;

//演示引用的使用
int main(){
    int intOne;
    int &rSomeRef = intOne;
    intOne = 5;
    cout<<"intOne:"<<intOne<<endl;
    cout<<"rSomeRef:"<<rSomeRef<<endl;

    rSomeRef=7;
    cout<<"intOne:"<<intOne<<endl;
    cout<<"rSomeRef:"<<rSomeRef<<endl;
    return 0;
}

intOne:5
rSomeRef:5
intOne:7
rSomeRef:7
```


获取引用的地址
```cpp
#include <iostream>
using namespace std;

//获取引用的地址
int main(){
    int intOne=5;
    int &rSomeRef=intOne;

    intOne=5;
    cout<<"intOne: "<<intOne<<endl;
    cout<<"rSomeRef: "<<rSomeRef<<endl;

    cout<<"&intOne:"<<&intOne<<endl;
    cout<<"&rSomeRef:"<<&rSomeRef<<endl;
    
    return 0;
}
intOne: 5
rSomeRef: 5
&intOne:0x7ffd984aa074
&rSomeRef:0x7ffd984aa074

```


重新分配引用
```cpp
#include <iostream>
using namespace std;

//重新分配引用
int main(){
    int intOne;
    int &rSomeRef=intOne;

    intOne = 5;
    cout<<"intOne:"<<intOne<<endl;
    cout<<"rSomeRef:"<<rSomeRef<<endl;
    cout<<"&intOne:"<<&intOne<<endl;
    cout<<"&rSomeRef:"<<&rSomeRef<<endl;

    int intTwo=8;
    //将inttwo的值赋值给rsomeref 同时也赋值给intone
    rSomeRef=intTwo;
    cout<<"intOne:"<<intOne<<endl;
    cout<<"intTwo:"<<intTwo<<endl;
    cout<<"rSomeRef:"<<rSomeRef<<endl;
    cout<<"&intOne:"<<&intOne<<endl;
    cout<<"&intTwo:"<<&intTwo<<endl;
    cout<<"&rSomeRef:"<<&rSomeRef<<endl;
    return 0;
}

intOne:5
rSomeRef:5
&intOne:0x7ffd16148c94
&rSomeRef:0x7ffd16148c94
intOne:8
intTwo:8
rSomeRef:8
&intOne:0x7ffd16148c94
&intTwo:0x7ffd16148c90
&rSomeRef:0x7ffd16148c94
```

请使用引用来创建对象的别名。请初始化所有引用。
不要尝试重新分配引用。不要混淆地址运算符和引用运算符。

###### 对对象的引用
```cpp
#include <iostream>
using namespace std;

//对对象的引用

class SimpleCat{
    public:
    SimpleCat(int age,int weight);
    ~SimpleCat(){}
    int GetAge() const {return itsAge;}
    int GetWeight() const {return itsWeight;}
    private:
    int itsAge;
    int itsWeight;
};

SimpleCat::SimpleCat(int age,int weight){
    itsAge = age;
    itsWeight = weight;
}
int main(){
    SimpleCat Frisky(5,8);
    //对对象的引用
    SimpleCat &rCat = Frisky;

    cout<<"Frisky is ";
    cout<<rCat.GetAge()<<" years old and ";
    cout<<rCat.GetWeight()<<" pounds weight"<<endl;
    return 0;
}

```

空指针和空引用
```

当指针未初始化或被删除时，应将其赋值为null ( 0 )。但引用则不然。事实上，引用不能为 null，引用 null 对象的程序被视为无效程序。当程序无效时，几乎任何事情都可能发生。它可能看似正常运行，也可能删除磁盘上的所有文件。这两种情况都是无效程序的可能结果。

大多数编译器都会毫无怨言地支持空对象，只有当您尝试以某种方式使用该对象时才会崩溃。然而，利用这一点仍然不是一个好主意。当您将程序移至另一台机器或编译器时，如果您有空对象，可能会出现神秘的错误。
```

有单最好绝不要使用空引用。


###### 引用的作用

我们在编程中常常遇到 需要返回多个值的情况。

通过引用传递函数可以克服 这两个限制，参数传递以及返回多个值
###### 通过指针传递函数参数


根据上一章所学的内容，函数参数是通过栈传递的
```cpp
内存的五个区域（复习）

- 全局命名空间（全局变量）
    
- 空闲存储（堆，空闲存储） new 
    
- 寄存器 （跟踪堆栈顶部和指令指针）
    
- 代码空间 （代码）
    
- 栈 （局部变量和函数参数） return 后自动清理
```


###### 普通的按值传递

```cpp
#include <iostream>
using namespace std;

void swap(int x, int y);
void swap(int x, int y){
    int temp;
    cout<<"swap.交换前，x="<<x<<",y="<<y<<endl;
    temp=x;
    x=y;
    y=temp;
    cout<<"swap.交换后，x="<<x<<",y="<<y<<endl;
}
int main(){
    int x=5,y=10;
    cout<<"Main.交换前，x="<<x<<",y="<<y<<endl;
    swap(x,y);
    cout<<"Main.交换后，x="<<x<<",y="<<y<<endl;
    return 0;
}
Main.交换前，x=5,y=10//不影响值的改变
swap.交换前，x=5,y=10
swap.交换后，x=10,y=5
Main.交换后，x=5,y=10//不影响值的改变

```

用指针改写上述代码

```cpp
#include <iostream>
using namespace std;


void swap(int *x, int *y);
void swap(int *px, int *py){
    int temp;
    cout<<"swap.交换前，*px="<<*px<<",*py="<<*py<<endl;
    temp=*px;
    *px=*py;
    *py=temp;
    cout<<"swap.交换后，*px="<<*px<<",*py="<<*py<<endl;
}
int main(){
    int x=5,y=10;
    cout<<"Main.交换前，x="<<x<<",y="<<y<<endl;
    swap(&x,&y);
    cout<<"Main.交换后，x="<<x<<",y="<<y<<endl;
    return 0;
}

Main.交换前，x=5,y=10
swap.交换前，*px=5,*py=10
swap.交换后，*px=10,*py=5
Main.交换后，x=10,y=5//传入的是x，y的地址，通过解引用交换了，最后这个值会被影响到
```

用引用改写
```cpp
#include <iostream>
using namespace std;


void swap(int &x, int &y);
void swap(int &rx, int &ry){
    int temp;
    cout<<"swap.交换前，rx="<<rx<<",ry="<<ry<<endl;
    temp=rx;
    rx=ry;
    ry=temp;
    cout<<"swap.交换后，rx="<<rx<<",ry="<<ry<<endl;
}
int main(){
    int x=5,y=10;
    cout<<"Main.交换前，x="<<x<<",y="<<y<<endl;
    swap(x,y);
    cout<<"Main.交换后，x="<<x<<",y="<<y<<endl;
    return 0;
}
Main.交换前，x=5,y=10
swap.交换前，rx=5,ry=10
swap.交换后，rx=10,ry=5
Main.交换后，x=10,y=5

```

###### 了解函数头和原型
```cpp
在 C++ 中，类和函数的客户端依靠头文件来告知所需的一切；它充当类或函数的接口。实际实现对客户端是隐藏的。这允许程序员专注于手头的问题并使用类或函数而不必担心它是如何工作的。
当约翰·罗布林上校设计布鲁克林大桥时，他非常关注混凝土的浇筑方式和桥梁钢丝的制造方式。他密切参与了制造材料所需的机械和化学过程。然而，今天，工程师们通过使用众所周知的建筑材料来更有效地利用时间，而不管制造商是如何生产这些材料的。
C++ 的目标是让程序员可以依赖易于理解的类和函数，而无需考虑它们的内部工作原理。这些“组件”可以组装起来生成程序，就像组装电线、管道、夹具和其他部件以生成建筑物和桥梁一样。

就像工程师检查管道的规格表以确定其承载能力、体积、配件尺寸等一样，C++ 程序员读取函数或类的接口来确定它提供哪些服务、采用哪些参数以及返回哪些值。
```

###### 返回多个值

==我要返回两个值怎么办？==

***我们可以在栈中创建一个局部变量，这个函数不需要返回多个值，只需要将操作的我们想要的结果放到这几个局部变量中，我们用指针，引用，等方法取出来即可***

###### 下面演示用指针的方法“返回”多个值
```cpp
#include <iostream>
using namespace std;

//从函数返回多个值,使用指针
typedef unsigned short USHORT;

short Factor(USHORT,USHORT*,USHORT*);

short Factor(USHORT n,USHORT *pSquared,USHORT *pCubed){
    short Value=0;
    if(n>20){
        Value=1;//错误状态
    }else {
        *pSquared=n*n;
        *pCubed=n*n*n;
        Value=0;//成功状态
    }
    return Value;
}
int main(){

    USHORT number,squared,cubed;
    short error;//0为成功，1为错误

    cout<<"请输入一个数字（0-20）";
    cin>>number;
    
    error=Factor(number,&squared,&cubed);// 传递变量的地址（指针
    if(!error){
        cout<<"number="<<number<<endl;
        cout<<"squared="<<squared<<endl;
        cout<<"cubed="<<cubed<<endl;
    }else{
        cout<<"error="<<error<<endl;
    }

    return 0;
}
请输入一个数字（0-20）3
number=3
squared=9
cubed=27

```

还可以继续改进成枚举类型
```cpp
enum ERROR_VALUE { SUCCESS, FAILURE};
```
###### 第二种通过引用返回并且使用枚举优化

```cpp
#include <iostream>
using namespace std;

//从函数返回多个值,使用引用
typedef unsigned short USHORT;
enum ERR_CODE{SUCCESS,ERROR};
//用枚举优化代替value 设置0,1 ，更易阅读
ERR_CODE Factor(USHORT,USHORT&,USHORT&);

ERR_CODE Factor(USHORT n,USHORT &rSquared,USHORT &rCubed){
    if(n>20){
        return ERROR;
    }else {
        rSquared=n*n;
        rCubed=n*n*n;
        return SUCCESS;
    }
}
int main(){
    //栈局部变量
    USHORT number,squared,cubed;
    ERR_CODE result;

    cout<<"请输入一个数字（0-20）";
    cin>>number;
    
    result=Factor(number,squared,cubed);
    if(result==SUCCESS){
        cout<<"number="<<number<<endl;
        cout<<"squared="<<squared<<endl;
        cout<<"cubed="<<cubed<<endl;
    }else{
       cout<<"输入错误！"<<endl;
    }
    return 0;
}
```

###### 通过引用传递以提高效率

通过值传递对象给函数
通过值从函数返回对象 都会生成副本，产生了额外的内存，和时间。
每次将对象的临时副本放入堆栈时都会调用复制构造函数。

###### 通过引用传递对象

```cpp
#include <iostream>
using namespace std;
//通过引用传递对象

class SimpleCat{
    public:
        SimpleCat();
        SimpleCat(SimpleCat&);
        ~SimpleCat();
};
SimpleCat::SimpleCat(){
    cout<<"Simple Cat 构造函数...\n";
}
SimpleCat::SimpleCat(SimpleCat&){
    cout<<"Simple Cat 拷贝构造函数...\n";
}
SimpleCat::~SimpleCat(){
    cout<<"Simple Cat 析构函数...\n";
}
SimpleCat FunctionOne(SimpleCat theCat);
SimpleCat* FunctionTwo(SimpleCat* theCat);
SimpleCat FunctionOne(SimpleCat theCat){
    cout<<"FunctionOne() 返回\n";
    return theCat;
}
SimpleCat* FunctionTwo(SimpleCat* theCat){
    cout<<"FunctionTwo() 返回\n";
    return theCat;
}
int main() {
    cout<<"making a cat...\n";
    SimpleCat Frisky;
    cout<<"调用 FunctionOne...\n";
    FunctionOne(Frisky);
    cout<<"调用 FunctionTwo...\n";
    FunctionTwo(&Frisky);
    return 0;
}

//首先输出making a cat...
//创建SimpleCat Frisky; SimpleCat(); 输出Simple Cat 构造函数... 
//然后输出调用 FunctionOne...
//然后执行FunctionOne(Frisky); 将创建好的对象Frisky拷贝给theCat; SimpleCat(SimpleCat&); 输出Simple Cat 拷贝构造函数...
//FunctionOne()内部输出 FunctionOne() 返回
//然后执行return theCat; 并以值形式返回SimpleCat 对象。这会创建该对象的另一个副本，调用复制构造函数
//FunctionOne()的返回值未分配给任何对象，因此为返回而创建的临时对象被丢弃，调用析构函数
//由于FunctionOne()已结束，其本地副本超出范围并被销毁，调用析构函数并产生输出。
//然后输出调用FunctionTwo...
//但参数是通过引用传递的。没有生成副本，因此没有输出。
//然后再次通过引用返回SimpleCat对象，因此再次不产生对构造函数或析构函数的调用。
//最后，程序结束，Frisky超出范围，导致最后一次调用析构函数并打印输出
```

###### 传递const指针
```cpp

#include <iostream>
using namespace std;

class SimpleCat{
    public:
        SimpleCat();
        SimpleCat(SimpleCat&);
        ~SimpleCat();
        int GetAge() const {return itsAge;}
        void SetAge(int age) {itsAge = age;}
    private:
        int itsAge;
};
SimpleCat::SimpleCat(){
    cout<<"Simple Cat 构造函数...\n";
    itsAge = 1;
}
SimpleCat::SimpleCat(SimpleCat&){
    cout<<"Simple Cat 拷贝构造函数...\n";
}
SimpleCat::~SimpleCat(){
    cout<<"Simple Cat 析构函数...\n";
}
const SimpleCat* const FunctionTwo(const SimpleCat* const theCat);

const SimpleCat* const FunctionTwo(const SimpleCat* const theCat){
    cout<<"FunctionTwo() 返回\n";
    cout<<"Frisky 现在"<<theCat->GetAge()<<"岁\n";
    return theCat;
}
int main() {
    cout<<"making a cat...\n";
    SimpleCat Frisky;
    cout<<"调用 FunctionOne...\n";
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    int age=5;
    Frisky.SetAge(age);
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    cout<<"调用 FunctionTwo...\n";
    FunctionTwo(&Frisky);
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    return 0;
}
making a cat...
Simple Cat 构造函数...
调用 FunctionOne...
Frisky 现在1岁
Frisky 现在5岁
调用 FunctionTwo...
FunctionTwo() 返回
Frisky 现在5岁
Frisky 现在5岁
Simple Cat 析构函数...
```

解决了进行额外复制的问题，从而省去了对复制构造函数和析构函数的调用。它使用指向常量对象的常量指针，从而解决了函数更改对象的问题。然而，它仍然有些麻烦，因为传递给函数的对象是指针。

因为你知道对象永远不会为空，所以如果传入的是引用而不是指针，那么在函数中操作起来会更容易。

###### 传递对象引用
```cpp
#include <iostream>
using namespace std;
//传递对象的引用

class SimpleCat{
    public:
        SimpleCat();
        SimpleCat(SimpleCat&);
        ~SimpleCat();
        int GetAge() const {return itsAge;}
        void SetAge(int age) {itsAge = age;}
    private:
        int itsAge;
};
SimpleCat::SimpleCat(){
    cout<<"Simple Cat 构造函数...\n";
    itsAge = 1;
}
SimpleCat::SimpleCat(SimpleCat&){
    cout<<"Simple Cat 拷贝构造函数...\n";
}
SimpleCat::~SimpleCat(){
    cout<<"Simple Cat 析构函数...\n";
}
const SimpleCat& FunctionTwo(const SimpleCat& theCat);

const SimpleCat& FunctionTwo(const SimpleCat& theCat){
    cout<<"FunctionTwo() 返回\n";
    cout<<"Frisky 现在"<<theCat.GetAge()<<"岁\n";
    return theCat;
}
int main() {
    cout<<"making a cat...\n";
    SimpleCat Frisky;
    cout<<"调用 FunctionOne...\n";
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    int age=5;
    Frisky.SetAge(age);
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    cout<<"调用 FunctionTwo...\n";
    FunctionTwo(Frisky);
    cout<<"Frisky 现在"<<Frisky.GetAge()<<"岁\n";
    return 0;
}

```

###### const 引用
```cpp
C++ 程序员通常不区分“对SimpleCat对象的常量引用”和“对常量SimpleCat 对象的引用”。引用本身永远不能重新分配以引用另一个对象，因此始终是常量。
如果将关键字const应用于引用，则会使所引用的对象成为常量。

引用的常量性
引用本身：引用在 C++ 中本质上是一个别名。一旦引用被初始化，它就永远不能被改变去引用另一个对象。因此，引用本身是常量的。

当我们在 C++ 中使用 const 引用时，主要是为了防止通过引用修改原对象的值。const 可以应用于引用来使所引用的对象成为常量。
void Function(const SimpleCat& cat);
这种形式声明了一个对 SimpleCat 对象的常量引用，表示我们不能通过这个引用来修改 cat 对象的值。在函数内部，尝试修改 cat 的任何值都会导致编译错误。

const 引用参数
当函数参数是对象时，使用 const 引用可以避免不必要的拷贝，同时保证参数不会被修改：
void PrintCat(const SimpleCat& cat) {
    // 不能修改 cat 的任何属性
    cat.Display();  // 假设 SimpleCat 类有一个 Display 方法
}
返回 const 引用
函数也可以返回 const 引用，避免复制大对象，并保证返回的对象不会被修改：

const SimpleCat& GetCat() {
    static SimpleCat cat;  // 静态对象，保证其生命周期
    return cat;
}
引用本身是常量：一旦引用初始化，就不能改变它指向的对象。
const 引用：通过 const 引用，可以防止通过引用修改原对象的值。
```

###### 何时使用引用何时使用指针

C++ 程序员非常喜欢引用而不是指针。引用更简洁、更易于使用，而且它们可以更好地隐藏信息，正如我们在上例中看到的那样。

但是，引用不能重新赋值。如果您需要先指向一个对象，然后再指向另一个对象，则必须使用指针。引用不能为空，因此如果所讨论的对象有可能为空，则不能使用引用。您必须使用指针。
```cpp

后一种问题的一个示例是运算符new。 如果new 无法在空闲存储中分配内存，它将返回一个空指针。 由于引用不能为空，因此在检查它不为空之前，不得初始化对此内存的引用。 以下示例显示了如何处理此问题：
int *pInt = new int;
if (pInt != NULL)
int &rInt = *pInt;//将pint 指向的值赋值给引用rint的值
在此示例中，声明了一个指向 int 的指针pInt ，并使用运算符new返回的内存对其进行初始化。测试pInt中的地址，如果它不为空，则取消引用pInt 。取消引用int变量的结果是一个int对象，并且rInt被初始化为引用该对象。因此，rInt成为 运算符new返回的int的别名
```
*尽可能通过引用传递参数。尽可能通过引用返回。如果引用可行，请勿使用指针。尽可能使用const 来保护引用和指针。不要返回对本地对象的引用。*

###### 不要返回不在范围内的对象的引用
```cpp
一旦 C++ 程序员学会了通过引用传递，他们就会变得疯狂起来。但是，他们也有可能过度使用。请记住，引用始终是某个其他对象的别名。如果将引用传入或传出函数，请务必问自己：“我所别名的对象是什么？每次使用它时它是否仍然存在？”
```

```cpp
#include <iostream>
using namespace std;
//返回对不存在对象的引用

class SimpleCat{
    public:
        SimpleCat(int age,int weight);
        ~SimpleCat();
        int GetAge() {return itsAge;}
        int GetWeight() {return itsWeight;}
    private:
        int itsAge;
        int itsWeight;
};
SimpleCat::SimpleCat(int age,int weight):itsAge(age),itsWeight(weight){
    
}
SimpleCat &TheFunction();
SimpleCat &TheFunction() {
    SimpleCat Frisky(5,9);
    return Frisky;
}
int main() {
    SimpleCat &rCat = TheFunction();
    int age = rCat.GetAge();
    cout << "rCat is " << age << " years old" << endl;
    return 0;
}

Output: Compile error: Attempting to return a reference to a local object!
```

###### 返回对堆上的对象的引用

###### 内存泄漏了怎么办

