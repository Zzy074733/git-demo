1.1 什么是 C++
C++ 是在 C 语言基础上扩展的面向对象编程语言，兼容 C 语言的过程化编程特性，新增面向对象、泛型编程、异常处理等高级特性，广泛应用于游戏开发、系统编程、嵌入式开发等领域。
1.2 第一个 C++ 程序
cpp
运行
#include <iostream>
int main() {
    std::cout << "Hello, C++ World!" << std::endl;
    return 0;
}
编译与运行命令（Linux/macOS）：
bash
运行
g++ hello.cpp -o hello
./hello
编译与运行命令（Windows）：
bash
运行
g++ hello.cpp -o hello.exe
hello.exe
输出结果：
plaintext
Hello, C++ World!
1.3 C++ 与 C 语言核心差异
表格
特性	C 语言	C++
输入输出	printf/scanf	cin/cout
命名冲突解决	无	namespace
函数重载	不支持	支持
面向对象	无	class / 对象 / 继承 / 多态
数据类型	基础类型 / 指针	新增 bool/string 等
内存管理	malloc/free	new/delete
二、核心语法
2.1 命名空间（namespace）
cpp
运行
#include <iostream>
namespace MySpace {
    int num = 10;
    void printNum() {
        std::cout << "MySpace num: " << num << std::endl;
    }
}
namespace MySpace::SubSpace {
    int num = 20;
    void printNum() {
        std::cout << "SubSpace num: " << num << std::endl;
    }
}
int main() {
    std::cout << MySpace::num << std::endl;
    MySpace::printNum();
    MySpace::SubSpace::printNum();
    using MySpace::num;
    std::cout << num << std::endl;
    using namespace std;
    cout << "Hello Namespace!" << endl;
    return 0;
}
2.2 数据类型与变量
2.2.1 基础数据类型
表格
类型	大小（字节）	取值范围	示例
bool	1	true/false	bool flag = true;
char	1	-128 ~ 127	char ch = 'a';
short	2	-32768 ~ 32767	short s = 100;
int	4	-2^31 ~ 2^31-1	int num = 1000;
long	4/8	随系统而定	long l = 100000L;
long long	8	-2^63 ~ 2^63-1	long long ll = 1e18;
float	4	单精度浮点（6-7 位有效数）	float f = 3.14f;
double	8	双精度浮点（15-16 位有效）	double d = 3.1415926;
2.2.2 字符串类型（string）
cpp
运行
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str1 = "Hello";
    string str2 = " C++";
    string str3 = str1 + str2;
    cout << str3 << endl;
    cout << "长度：" << str3.size() << endl;
    cout << "截取：" << str3.substr(2, 3) << endl;
    size_t pos = str3.find("C++");
    if (pos != string::npos) {
        cout << "找到位置：" << pos << endl;
    }
    return 0;
}
2.3 函数重载
cpp
运行
#include <iostream>
using namespace std;
int add(int a, int b) {
    return a + b;
}
double add(double a, double b) {
    return a + b;
}
int add(int a, int b, int c) {
    return a + b + c;
}
int main() {
    cout << add(1, 2) << endl;
    cout << add(1.5, 2.5) << endl;
    cout << add(1, 2, 3) << endl;
    return 0;
}
2.4 内存管理（new/delete）
cpp
运行
#include <iostream>
using namespace std;
int main() {
    // 单个变量内存分配
    int* p1 = new int;
    *p1 = 10;
    cout << *p1 << endl;
    delete p1;

    // 数组内存分配
    int* p2 = new int[5];
    for (int i = 0; i < 5; i++) {
        p2[i] = i + 1;
        cout << p2[i] << " ";
    }
    delete[] p2;
    return 0;
}
2.5 面向对象编程（OOP）
2.5.1 类与对象
cpp
运行
#include <iostream>
#include <string>
using namespace std;
class Student {
private:
    string name;
    int age;
public:
    void setInfo(string n, int a) {
        name = n;
        age = a;
    }
    void showInfo() {
        cout << "姓名：" << name << "，年龄：" << age << endl;
    }
};
int main() {
    Student stu;
    stu.setInfo("小明", 18);
    stu.showInfo();
    return 0;
}
2.5.2 构造函数与析构函数
cpp
运行
#include <iostream>
#include <string>
using namespace std;
class Person {
public:
    Person() {
        cout << "无参构造函数调用" << endl;
        name = "默认名称";
        age = 0;
    }
    Person(string n, int a) {
        cout << "有参构造函数调用" << endl;
        name = n;
        age = a;
    }
    ~Person() {
        cout << "析构函数调用：" << name << endl;
    }
    void show() {
        cout << "姓名：" << name << "，年龄：" << age << endl;
    }
private:
    string name;
    int age;
};
int main() {
    Person p1;
    p1.show();
    Person p2("小红", 20);
    p2.show();
    return 0;
}
2.5.3 继承
cpp
运行
#include <iostream>
#include <string>
using namespace std;
// 基类
class Person {
protected:
    string name;
    int age;
public:
    Person(string n, int a) : name(n), age(a) {}
    void showBase() {
        cout << "姓名：" << name << "，年龄：" << age << endl;
    }
};
// 派生类
class Student : public Person {
private:
    int score;
public:
    Student(string n, int a, int s) : Person(n, a), score(s) {}
    void showAll() {
        showBase();
        cout << "成绩：" << score << endl;
    }
};
int main() {
    Student stu("小李", 19, 95);
    stu.showAll();
    return 0;
}