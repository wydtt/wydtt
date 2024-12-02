一个goto例子

很久之前的书都不推荐goto
喜欢 任何工具，只要小心使用并在合适的人手中，Goto 都可以是一个有用的结构， ANSI 委员会决定将其保留在该语言中，因为它有其合法的 使用。
```cpp
// 包含iostream头文件
#include <iostream>

// 使用标准命名空间
using namespace std;

// 主函数
int main() {
    // 初始化计数器
    int counter = 0;

    // 开始循环
    loop:
    // 计数器加1
    counter++;
    // 输出计数器的值
    cout << "counter: " << counter << "\n";
    // 如果计数器小于5，跳转到loop标签处
    if (counter < 5)
        goto loop;
    // 输出循环结束后的计数器值
    cout << "Complete. Counter: " << counter << ".\n";
    // 返回0，表示程序正常结束
    return 0;
}
```

wihle循环
```cpp
// 包含iostream头文件
#include <iostream>

// 使用标准命名空间
using namespace std;

// 主函数
int main() {
    // 初始化计数器
    int counter = 0;

    // 开始循环
    while (counter < 5) {
        // 计数器加1
        counter++;
        // 输出计数器的值
        cout << "counter: " << counter << "\n";
    }

    // 输出循环结束后的计数器值
    cout << "Complete. Counter: " << counter << ".\n";
    // 返回0，表示程序正常结束
    return 0;
}
```

```cpp
// FILEPATH: /cloudide/workspace/learncpp21days/main.cpp
// 引入 iostream 库
#include <iostream>
using namespace std;
// 定义枚举类型 BOOL，包含 FALSE 和 TRUE 两个值
enum BOOL { FALSE, TRUE };
// 定义无符号短整型的别名 USHORT
typedef unsigned short int USHORT;

// 函数声明
USHORT menu();
void DoTaskOne();
void DoTaskMany(USHORT);

int main()
{
    // 初始化 exit 变量为 FALSE
    BOOL exit = FALSE;
    // 开始一个无限循环
    for (;;)
    {
        // 调用 menu 函数，获取用户的选择
        USHORT choice = menu();
        // 根据用户的选择执行不同的操作
        switch(choice)
        {
            // 如果用户选择 1，执行 DoTaskOne 函数
            case (1):
                DoTaskOne();
                break;
            // 如果用户选择 2，执行 DoTaskMany 函数，参数为 2
            case (2):
                DoTaskMany(2);
                break;
            // 如果用户选择 3，执行 DoTaskMany 函数，参数为 3
            case (3):
                DoTaskMany(3);
                break;
            // 如果用户选择 4，跳过当前循环，重新开始
            case (4):
                continue;  // 冗余！
                break;
            // 如果用户选择 5，设置 exit 变量为 TRUE，表示退出程序
            case (5):
                exit=TRUE;
                break;
            // 如果用户输入的不是 1-5，提示用户重新选择
            default:
                cout << "Please select again!\n";
                break;
        }          // end switch

        // 如果 exit 变量为 TRUE，跳出无限循环
        if (exit)
            break;
    }                // end forever

    // 程序结束，返回 0
    return 0;
}                    // end main()

// 定义 menu 函数，用于显示菜单并获取用户的选择
USHORT menu()
{
    USHORT choice;

    cout << " **** Menu ****\n\n";
    cout << "(1) Choice one.\n";
    cout << "(2) Choice two.\n";
    cout << "(3) Choice three.\n";
    cout << "(4) Redisplay menu.\n";
    cout << "(5) Quit.\n\n";
    cout << ": ";
    cin >> choice;
    return choice;
}

// 定义 DoTaskOne 函数，用于执行任务一
void DoTaskOne()
{
    cout << "Task One!\n";
}

// 定义 DoTaskMany 函数，根据传入的参数执行不同的任务
void DoTaskMany(USHORT which)
{
    if (which == 2)
        cout << "Task Two!\n";
    else
        cout << "Task Three!\n";
}
```

循环测试，循环豆的四种写法
```cpp

#include <iostream>
using namespace std;

int main() {
    int a=100;
	do{
		cout<<a<<endl;
		a+=2;
	}while(a<=200);
}

#include <iostream>
using namespace std;

int main() {
    int a=100;
	do{
		a+=2;
		cout<<a<<endl;
	}while(a<=200);
}


#include <iostream>
using namespace std;

int main() {
    int a=100;
	while (a<=200) {
			cout<<a<<endl;
	a+=2;

	}
}

#include <iostream>
using namespace std;

int main() {
    for(int i=100;i<200;i+=2){
		cout<<i<<endl;
	}
}
```