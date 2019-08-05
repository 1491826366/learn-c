# **函数**

C函数很简单，但由于C的工作方式，函数的功能有点受限。

  * 函数接收固定或可变数量的参数。
  * 函数只能返回一个值，或者不返回任何值。
在C中，参数通过值复制到函数，这意味着我们不能更改参数以在函数之外影响它们的值。要做到这一点，我们必须使用指针，这将在后面讲授。

使用以下语法定义函数：

```
int foo(int bar) {
    /* do something */
    return bar * 2;
}

int main() {
    foo(1);
}
```

我们定义的foo函数接收一个参数，即bar。函数接收一个整数，将其乘以2，然后返回结果。

要foo以1作为参数执行函数bar，我们使用以下语法：

```
foo(1);
```

在C中，必须首先定义函数，然后才能在代码中使用它们。它们可以先声明，然后使用头文件或在C文件的开头实现，也可以按照它们使用的顺序实现（不太可取）。

使用函数的正确方法如下：

```
/* function declaration */
int foo(int bar);

int main() {
    /* calling foo from main */
    printf("The value of foo is %d", foo(1));
}

int foo(int bar) {
    return bar + 1;
}
```

我们还可以使用关键字创建不返回值的函数void：

```
void moo() {
    /* do something and don't return a value */
}

int main() {
    moo();
}
```

## **练习**

编写一个函数print_big，该函数接收一个参数（一个整数），x is big如果给函数的参数是一个大于10的数字，则打印该行。
  * **重要提示**：不要忘记\n在printf字符串的末尾添加换行符。

```
#include <stdio.h>

/* function declaration */
void print_big(int number);

int main() {
  int array[] = { 1, 11, 2, 22, 3, 33 };
  int i;
  for (i = 0; i < 6; i++) {
    print_big(array[i]);
  }
  return 0;
}

/* write your function here *
```

###  **解答**

```
void print_big(int x)
{
if(x>10) printf("%d\n",x);
}
```