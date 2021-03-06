# Hello World!

几乎所有的的编程语言教学中，第一个小程序就是输出其`Hello Word!`，当然我也不想例外，所以就让我们来看一段输出`Hello Word!`的代码吧。

```c
#include <stdio.h>

int main(void)
{
    printf("Hello world!\n");
    return 0;
}
```

以上是一段标准的`C`语言程序，其输出就是`Hello world!`。

## 代码结构

- 头文件

```c
#include <stdio.h>
```

以`#`开头的语句称为预处理器指令，`include`是预定义的标识符，这是编译器所指定的而不是`c`语言预定义的。

`#include`语句不是必须的，但是如果一旦程序中有该语句，就必须将它放在程序的开始处；

以`.h`为后缀的文件我们称为头文件，可以是C标准库中的头文件，也可以是自定义的库文件；

- 函数

```c
int main(void)
{
    ......
    return 0;
}
```

`int`是`c语言`中的关键字，定义了一个`main`函数，其要求返回类型为整型，`main`函数是`c语言`定义的一个入口；

- 代码块

```c
{
    ......
}
```

放在`花括号`中的代码被称为代码块也成为函数体。

- 语句

```c
...
    printf("Hello world!\n");
    return 0;
...
```

代码块中的每一行代码代表一条`语句`，每条语句由`分隔符`表示结束。

- 输入与输出实例

以下程序将会提示你输入你个`数字`，然后打印出来

```c
#include <stdio.h>

int main(void)
{
    int i;  // 定义一个整型变量i
    printf("请输入一个整数：");  // 输出
    scanf("%d",&i);  // 接受用户输入的数字，并赋值给变量i
    printf("你输入的整数是：%d\n",i);  // 通过字符串格式化输出输入的数字
    return 0;
}
```

## 注释

程序中注释的作用其实就是让阅读源代码的程序员更快速的理解，C程序在编译时会忽略注释中的内容。

- 单行注释

```c
// 我是单行注释
```

- 多行注释

```c
/*
我是块(多行)注释
*/
```