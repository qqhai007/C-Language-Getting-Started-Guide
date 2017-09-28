# 函数

- 函数的基本概念

把重复的功能分装到一个函数中，当每次遇到这个功能的时候可直接调用函数去完成，省去代码的重复编写。


```c
类型标识符 函数名(类型1 形参1, 类型2 形参2, 类型3 形参3.....)
{
    代码块;
    return 返回值;
}
```

如下实例：

```c
#include <stdio.h>

int jiesheng(int n)
{
    int i;
    int s = 1;
    for(i=1;i<=n;i++)
        s *= i;
    return s;
}

int main(void)
{
    int s = jiesheng(5);
    printf("%d",s);
    return 0;
}
```

- 函数是如何被执行的


`传递参数(也可以不穿)` --> `函数体运算` --> `返回值(也可以不返回)`

- 在此分析main函数
    1. 标准定义：C99
    2. 入口函数`__main`、`__start`
    3. Windows系统和嵌入式中的main

- 空函数

```c
void void_function(void)
{

}
```

- 函数的原型、声明与定义

**原型：** 原型就是一个函数声明

**函数的声明：**用来描述函数的参数类型和返回值，告诉编译器以作代码检查

**函数的定义：**实现函数的功能，函数只能定义一次，但可以多次声明

```c
// 先声明
extern int jiesheng(int n);
// 后调用
```

## 函数的参数

- 形式参数和实际参数

```c
int jiesheng(int n) // 其中的n就是形式参数，可以是个变量也可以是个常量
```

```c
int s = jiesheng(5); // 在调用时，传过来的6就是实际参数
```

- 值调用

C语言中传递的参数都是通过`值`进行调用，例如上述中把实际参数`5`进行拷贝，然后在传递给函数，拷贝后的值就是形式参数`n`；


```c
#include <stdio.h>

int print_int(int n)
{
    printf("%d\n",n);
    n+=1;
    printf("%d\n",n);
    return n;
}

int main(void)
{
    int i = 10;
    printf("%d\n",i);
    int rest = print_int(i);
    printf("%d\n",rest);
    printf("%d\n",i);
    return 0;
}
```
执行结果
```bash
10
10
11
11
10
```

- 地址调用

传递内存地址，而不是值；

```c
#include <stdio.h>

int print_int(int * n)
{
    printf("%d %x\n",*n,&n);
    *n+=1;
    printf("%d %x\n",*n,&n);
    return *n;
}

int main(void)
{
    int i = 10;
    printf("%d %x\n",i,&i);
    int rest = print_int(&i);
    printf("%d %x\n",rest,&rest);
    printf("%d %x\n",i,&i);
    return 0;
}
```
执行结果
```bash
10 2fdd9910
10 2fdd98f8
11 2fdd98f8
11 2fdd9914
11 2fdd9910
```

不管是`地址`传参还是`值`传参，都是将值拷贝一份到函数中。

## 函数的嵌套与递归函数

### 函数嵌套

- C语言中，除了`main`之外，函数之间的关系是平等的，因为`main`函数是C语言中的入口；
- 在一个函数中不能定义另外一个函数；
- 在一个函数中可以调用另外一个函数；

```c
#include <stdio.h>

int print1(int i)
{
    printf("%d\n",i);
    print2(2);
    return 0;
}

int print2(int i)
{
    printf("%d\n",i);
    print3(3);
    return 0;
}

int print3(int i)
{
    printf("%d\n",i);
    return 0;
}

int main(void)
{
    print1(1);
    return 0;
}
```

### 递归函数

- 一个函数在它的函数体定义内又调用该函数本身
    1. 直接调用：直接递归
    2. 间接调用：间接递归
- 嵌套调用的一种特殊情况
- 优点与缺点
    1. 可以帮助解决一些算法问题
    2. 运行效率较低、系统开销大
- 递归函数需要注意的一些地方
    1. 防止递归层数太多而引起栈溢出
    2. 汉诺塔、二叉树的遍历

```c
#include <stdio.h>

int story(int i)
{
    if(i < 50)
        printf("从前有座山,\n");
        for(i=0;i<60000000;i++);  //delay
        printf("山里有做庙,\n");
        for(i=0;i<60000000;i++);
        printf("庙里有个老和尚,\n");
        for(i=0;i<60000000;i++);
        printf("老和尚在给小和尚讲故事,\n");
        for(i=0;i<60000000;i++);
        printf("讲的啥？\n");
        for(i=0;i<90000000;i++);
        printf("\n\n");

        i++;
        story(i);
    return i;
}

int main(void)
{
    printf("开始讲故事啦\n\n");
    story(0);
    return 0;
}
```

## 变量的作用域

### 外部(全局)变量与局部变量

- 外部变量（全局变量）

函数外部定义的变量

- 局部变量
    1. 在函数或复合语句内部定义的变量
    2. 函数的形参也属于局部变量

```c
#include <stdio.h>

int global = 10;  // 全局变量

int main(void)
{
    int i = 1;  // 局部变量
    return 0;
}
```

- 外部变量和局比变量的作用域

变量的作用域与其定义的位置有着直接关系

```c
#include <stdio.h>

int global = 10;  // 全局变量,作用域从第三行开始

int main(void)
{
    int i = 1;  // 局部变量，作用域从第七行到12行
    {
        int j = 10;  // 代码块变量，作用域从第8行到10行
    }
    return 0;
}
```

- 一些需要注意的地方
    - 变量作用于屏蔽
    - C99标准中新的修改

### 变量的作用域

- 什么是作用于scope
    1. 变量在程序中的有效范围；
    2. 即程序在什么范围内变量可以被识别和使用；
- 分类
    1. 代码块作用域
    2. 文件作用域
    3. 函数作用域
    4. 原型作用域

## 变量的存储类型

- 变量的本质

一段连续内存空间的别名

- 声明变量的意义
    1. 建立变量符号表
    2. 变量的数据类型指示系统分配不同大小内存
    3. 变量的数据类型指示系统如何存储、运算
    4. 变量的数据类型决定变量的取值范围
- 变量名、变量的值、变量的地址
- 左值和右值

### 程序存储分布

1. 程序代码区
2. 静态存储区
    - 字符串等文字常量
    - 全局变量和静态局部变量
3. 动态存储区

### 变量的存储方式

- 自动变量：auto
- 静态变量：static
- 寄存器变量：register
- 外部变量：extern

## 关键字volatile

- 变量使用volatile修饰

告诉编译器，该变量随时会发生变化，每次使用该变量直接到内存中去取而不是采用暂存在寄存器中的值。

- 变量同时使用const和valatile修饰

状态寄存器