# **递归**

当函数在其中包含对自身的调用时发生递归。递归可以产生非常简洁，优雅的代码，可以直观地遵循。如果递归过深，它还可能导致使用非常大量的内存。

使用递归的常见示例：

  * 行走递归数据结构，如链表，二叉树等。
  * 探索国际象棋等游戏中的可能场景

递归总是由两个主要部分组成。一个终止案例，指示递归何时完成以及对自身的调用必须在终止案例中取得进展。

例如，此函数将通过递归添加执行乘法：

```
#include <stdio.h>

unsigned int multiply(unsigned int x, unsigned int y)
{
    if (x == 1)
    {
        /* Terminating case */
        return y;
    }
    else if (x > 1)
    {
        /* Recursive step */
        return y + multiply(x-1, y);
    }

    /* Catch scenario when x is zero */
    return 0;
}

int main() {
    printf("3 times 5 is %d", multiply(3, 5));
    return 0;
}
```
## **练习**
定义一个名为的新函数factorial()，它将通过递归乘法计算阶乘（5！= 5 x 4 x 3 x 2 x 1）。

```
#include <stdio.h>

int main() {
    /* testing code */
    printf("1! = %i\n", factorial(1));
    printf("3! = %i\n", factorial(3));
    printf("5! = %i\n", factorial(5));
}

/* define your function here (don't forget to declare it) */
```

### **解答**
```
#include <stdio.h>

int factorial(int number);

int main() {
    /* testing code */
    printf("1! = %i\n", factorial(1));
    printf("3! = %i\n", factorial(3));
    printf("5! = %i\n", factorial(5));
}

int factorial(int number){
    int f = number;
    if(number > 1){
        f *= factorial(number-1);
    }
return f;
}
```