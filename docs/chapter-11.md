# 数组

- 使用数组简化程序

对于相同类型的多个数据，可以使用数据代替，相同类型的多个参数，也可以使用数组代替。

例如下面计算15个学生的平均成绩

```c
#include <stdio.h>

int main(void)
{
    int score[15];
    int i;
    printf("请输入15个学生的英语成绩：\n");
    for(i=0;i<15;i++)
        scanf("%d", &score[i]);
    float sum = 0;
    float average_score = 0;
    for(i=0;i<15;i++)
        sum += score[i];
    average_score = sum/15;
    printf("他们的英语平均成绩为：%f\n", average_score);
    return 0;
}
```

- 什么是数组？
    1. 一组相同类型的数据集中在一起保存的一种方式，数组用来存储一组相同类型的数据对象；
    2. 数组元素：数组中的单个数据对象；
    3. 数组分类：字符数组、整型数组、指针数组、二维数组...；
    4. 数组的引用：使用下表`[]`或者指针，索引从0开始；

## 一维数组

- 数组的定义

```c
数组类型 数组名[数组长度];
int array[10];
```

- 定义时初始化数组

```c
int array[5] = {1, 2, 3, 4, 5};
for(int i = 0;i<5;i++)
    printf("%d",array[i]); // 引用数组时使用下表进行引用，从0开始
return 0;
```

在初始化的时候，如果定义了`10`个长度的数组，但是只在里面添加了`5`个值，那么剩下`5`个将会被默认赋值为`0`

```c
int array[10] = {1, 2, 3, 4, 5};
for(int i = 0;i<10;i++)
    printf("%d\n",array[i]);
return 0;
```

定义数组时也可以给指定索引赋值，如下代码中，定义了一个长度为`10`的数组，其中第一个元素赋值为`100`，最后一个元素赋值为`9999`

```c
int array[10] = {[0]=100, [9]=9999};
```

定义数组不指定长度，默认根据数组元素的个数来定义数组长度

```c
int array[] = {1,2,3,4,5};
```

- 动态往数组添加数据

```c
int array[5];

for(int i = 0; i<5; i++)
    array[i] = i*i;  // 数组内添加内容

for(int i = 0;i<5;i++)
    printf("%d\n",array[i]);
return 0;
```

- 数组大小

定义的数组类型不同，在初始化的时候所分配的内存大小也是不同的。

## 数组名与数组地址

- 什么是数组名
    1. 使用数组可以为同一组相同类型的变量命名同一个名称。C语言把数组名解释为指向该数组首元素的地址，数组名和指向首元素的指针等价；
    2. 当引用数组时，编译器会把数组名的值看做一个指针常量；
    3. 数组名不能用指针常量表示的情况
        - 当数组名用作`sizeof`或`&`的操作时，`sizeof`返回的是整个数组的长度
        - 取一个数值名的地址`&`产生的是一个指向数组的指针，而不是指向某个指针常量值的指针


```c
#include <stdio.h>

int main(void)
{
    int a[10];
    printf("%d %d\n",a, &a[0]);  // 两者相同
    printf("%d %d\n",a + 1, &a[1]);  // 两者相同，+1是元素的地址，默认是0
    return 0;
}
```

- 数组名作为左值和右值时的区别
    - 数组名不能作为左值：它代表的是一个指针常量，不能被修改；
    - 作为右值时：代表数组`首元素的地址`，而不是`数组的首地址`，注意，这里并没有一个地方来存储这个地址，这个是于指针不一样的地方；

- 数组名和地址的区别
    - 数组名代表的是首元素`array[0]`的地址`&array[0]`，而不是数组的首地址`&a`
    - 数组名`array+1`表示下一个数组元素的首地址`&array[0]+1`,`&array+1`指向下一个数组的首地址；


**使用数组需要注意的地方**

1. 数组的索引从0开始；
2. 数组越界问题，数组元素大于所定义长度时依旧不会报错；
3. 不指定数组大小时，编译器会根据初始化列表中元素的个数来决定；
4. 数组输入元素时，可以有更方便的写法；
5. C语言只支持一位数组；

## 二维数组

在C语言中依旧只支持一维数组，当一维数组中的每个元素都是一维数组时，就变成了二维数组；

- 初始化

定义一个三行三列的数组

```c
int array[3][3] = {
    {1, 2, 3},
    {1, 2, 3},
    {1, 2, 3}
};
```

上面的定义中，首先定义了一个长度为3的一维数组，一维数组中的每个元素又是一个长度为3的一维数组。

- 引用

```c
for(int i = 0; i<3; i++) {  // 循环每一行
    for(int j = 0; j<3; j++) {  // 循环每一列
        printf("%d ",array[i][j]);
    }
    printf("\n");
}
```

- 存储

二维数组的存储和一维数组的存储是一样的。

- 三维数组、多维数组

三维数组实例

```c
#include <stdio.h>

int main(void)
{
    int array[3][3][3] = {  // 定义一个三行三列的数组
        {
            {1, 2, 3},
            {1, 2, 3},
            {1, 2, 3}
        },
        {
            {1, 2, 3},
            {1, 2, 3},
            {1, 2, 3}
        },
        {
            {1, 2, 3},
            {1, 2, 3},
            {1, 2, 3}
        }
    };

    for(int i = 0; i<3; i++) {
        for(int j = 0; j<3; j++) {
            for(int k = 0; k<3; k++) {
                printf("%d ",array[i][j][k]);
            }
            printf("\n");
        }
        printf("\n");
    }
    return 0;
}
```

## 字符串数组与字符串

字符数组就是数组中所有的元素都是字符类型的数据。

- 初始化

一维数组

```c
char str[20] = {'h','e','l','l','o','w','o','r','l','d'};
printf("%s\n",str);
```

二维数组

```c
char str2d[2][5] = {
    {'h','e','l','l','o'},
    {'w','o','r','l','d'}
};
for(int i = 0; i<2; i++) {
    for(int j = 0; j<5; j++) {
        printf("%c",str2d[i][j]);
    }
}
```

定义字符串数组时可以使用ASCII来进行赋值

```c
char str[10] = {104,101,108,108,111};
printf("%s\n",str);
```

- 存储

连续线性存储，和数组存储模式一样。

- 字符串

```c
char str[] = "Hello, World!";
printf("%s\n",str);
```

- 字符串的存储

字符串存储的时候会有一个转义结束标志

```c
#include <stdio.h>

int main(void)
{
    char str[] = "helloworld";
    char str1[] = {"helloworld"};
    char c[] = {'h','e','l','l','o','w','o','r','l','d'};
    printf("%d %d\n",sizeof(str),sizeof(c));  // 11 10
    printf("%d %d\n",sizeof(str),sizeof(str1));  // 11 11
    return 0;
}
```

## 字符串处理函数

- 字符串输入gets、输出函数puts

```c
#include <stdio.h>

int main(void)
{
    char str[100];
    puts("请输入字符串：");
    gets(str);
    puts(str);
    return 0;
}
```

- 字符串长度函数：strlen

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char str[100] = "Hello, World!";
    printf("%d %d\n", sizeof(str), strlen(str));
    return 0;
}
```

- 字符串连接函数：strcat

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char des[] = "hello";
    char sur[5] = {'a','s','!'};
    printf("%s\n", strncat(des, sur, 2));
    printf("%s\n", strcat(des, sur));
    return 0;
}
```

- 字符串复制函数：strncpy/strcpy

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char des[] = "Hello";
    char sur[5] = {'a', 's', '!', '!', '!'};
    // 把des拷贝到sur中
    printf("%s\n", strncpy(des,sur,2));  // 拷贝指定的字节
    printf("%s\n", strcpy(des, sur));  // 全部拷贝
    return 0;
}
```

- 字符串比较函数：strcmp

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char str1[] = "hello";
    char str2[50];
    int i = strcmp(str1, str2);
    printf("%d\n", i);

    int j = strncmp(str1, str2, 5);
    printf("%d\n", j);

    return 0;
}
```

## 数组作为函数的参数

- 数组元素作为函数的参数

```c
#include <stdio.h>

int calc_add(int a, int b){
    return a+b;
}

int main(void)
{
    int score[10] = {[0]=99, [1]=98};
    int sum;
    sum = calc_add(score[0],score[1]);
    printf("%d",sum);
    return 0;
}
```

- 数组名作为函数的参数

传递的是一个地址，或者说是常量指针，下面实例计算数组内所有值的和

```c
#include <stdio.h>

int array_add(int a[10]){
    int sum = 0;
    for(int i = 0; i<10;i++)
        sum += a[i];
    return sum;
}

int main(void)
{
    int score[10] = {[0]=99, [1]=98};
    int sum;
    sum = array_add(score);
    printf("%d",sum);
    return 0;
}
```

- 注意点

```c
int array(const int a[5]) {
    ......
    // 此时传递过来的数组a是不能够被修改的
    return 0;
}
```

1. 数组名作为函数的参数时，其实传递的是一个地址指针，形参和实参的类型必须一直；
2. 形参和实参数组的铲毒可以不相同，关于数组的长度可以通过另外一个参数传递进来；
3. 多维数组作为函数的参数时，在函数定义时对形参数组可以制定每一维的长度，但是可以省去第一维的长度。