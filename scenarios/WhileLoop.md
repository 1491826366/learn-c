# **While循环**

while循环类似于for循环，但功能较少。只要while中的条件保持为真，while循环就会继续执行while块。例如，以下代码将执行十次：

```
int n = 0;
while (n < 10) {
    n++;
}
```

如果给出的条件始终计算为true（非零），则循环也可以无限执行：

```
while (1) {
   /* do something */
}
```

## **循环指令**

有两个重要的循环指令与C中的所有循环类型一起使用 - break和continue指令。

该break指令在十个循环后停止一个循环，即使while循环永远不会完成：

```
int n = 0;
while (1) {
    n++;
    if (n == 10) {
        break;
    }
}
```
在以下代码中，该continue指令导致printf跳过命令，因此只打印出偶数数字：


```
int n = 0;
while (n < 10) {
    n++;

    /* check that n is odd */
    if (n % 2 == 1) {
        /* go back to the start of the while block */
        continue;
    }

    /* we reach this code only if n is even */
    printf("The number %d is even.\n", n);
}
```

## **练习**
该array变量由10个数字序列。在while循环中，您必须编写两个if条件，以下列方式更改循环流（不更改printf命令）：

  * 如果即将打印的当前编号小于5，请勿打印。
  * 如果即将打印的当前数字大于10，请不要打印它并停止循环。

请注意，如果不提前使用迭代器变量i并使用continue导数，则会陷入无限循环。

```
#include <stdio.h>

int main() {
    int array[] = {1, 7, 4, 5, 9, 3, 5, 11, 6, 3, 4};
    int i = 0;

    while (i < 10) {
        /* your code goes here */

        printf("%d\n", array[i]);
        i++;
    }

    return 0;
}
```

### **解答**
```
if(i<5) continue;
if(i>10) break;
```