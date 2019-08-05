# **for循环**

C中的for循环很简单。它们提供了创建循环的能力 - 一个运行多次的代码块。For循环需要一个迭代器变量，通常标记为i。

for循环提供一下功能：
  * 使用初始值初始化迭代器变量
  * 检查迭代器是否已达到其最终值
  * 增加迭代器
例如，如果我们希望迭代一个块10次，我们写道：

```
int i;
for (i = 0; i < 10; i++) {
    printf("%d\n", i);
}
```

该块将打印数字0到9（总共10个数字）。

For循环可以迭代数组值。例如，如果我们想要对数组的所有值求和，我们将使用迭代器i作为数组索引：

```
int array[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
int sum = 0;
int i;

for (i = 0; i < 10; i++) {
    sum += array[i];
}

/* sum now contains a[0] + a[1] + ... + a[9] */
printf("Sum of the array is %d\n", sum);
```

## **练习**
计算阶乘（所有项目的乘法来，含），可变的。array[0]array[9]array

```
#include <stdio.h>

int main() {
  int array[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
  int factorial = 1;
  int i;

  /* calculate the factorial using a for loop  here*/

  printf("10! is %d.\n", factorial);
}
```

### **解答**
```
for(i=0;i<10;i++)
  factorial*=array[i];
```
