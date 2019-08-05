# **指针**

指针也是变量，在C编程语言中起着非常重要的作用。使用它们有几个原因，例如：

  * 字符串
  * 动态内存分配
  * 通过引用发送函数参数
  * 构建复杂的数据结构
  * 指向功能
  * 构建特殊的数据结构（即Tree，Tries等......）
还有很多。

## **什么是指针？**

指针本质上是一个简单的整数变量，它保存一个指向值的内存地址，而不是保存实际值本身。

计算机的内存是数据的顺序存储，指针指向内存的特定部分。我们的程序可以使用指针，指针指向大量内存 - 取决于我们决定从该点读取多少。

## **字符串作为指针**

我们已经讨论了字符串，但是现在我们可以更深入地了解一下C中的字符串是什么（当与C ++混合时，它们被称为C-Strings以区别于其他字符串）

以下行：

```
char *name="john";
```

做三件事：
 * 1、它分配一个名为的本地（堆栈）变量name，该变量是指向单个字符的指针。
 * 2、它导致字符串“John”出现在程序存储器中的某个位置（当然，在编译和执行之后）。
 * 3、它初始化name参数以指向J角色所在的位置（后面是内存中其余字符串）。

如果我们尝试将name变量作为数组访问，它将起作用，并将返回字符的序数值J，因为name变量实际上指向字符串的开头。

由于我们知道内存是顺序的，我们可以假设如果我们在内存中向前移动到下一个字符，我们将收到字符串中的下一个字母，直到我们到达字符串的末尾，标记为空终止符（序数值为0的字符，标记为\0）。

## **取消引用**

解除引用是指向指针指向的位置而不是内存地址的行为。我们已经在数组中使用解引用 - 但我们还不知道它。括号运算符 - 例如，访问数组的第一项。由于数组实际上是指针，因此访问数组中的第一项与取消引用指针相同。使用星号运算符取消引用指针。[0]*

如果我们想要创建一个指向堆栈中不同变量的数组，我们可以编写以下代码：

```
/* define a local variable a */
int a = 1;

/* define a pointer variable, and point it to a using the & operator */
int * pointer_to_a = &a;

printf("The value a is %d\n", a);
printf("The value of a is also %d\n", *pointer_to_a);
```

请注意，我们使用&运算符指向a我们刚刚创建的变量。

然后我们使用解除引用运算符来引用它。我们还可以更改解除引用变量的内容：

```
int a = 1;
int * pointer_to_a = &a;

/* let's change the variable a */
a += 1;

/* we just changed the variable again! */
*pointer_to_a += 1;

/* will print out 3 */
printf("The value of a is now %d\n", a);
```

## **练习**

创建一个指向所n调用的局部变量的指针pointer_to_n，并使用它将n的值增加1。

```
#include <stdio.h>

int main() {
  int n = 10;

  /* your code goes here */

  /* testing code */
  if (pointer_to_n != &n) return 1;
  if (*pointer_to_n != 11) return 1;

  printf("Done!\n");
  return 0;
}
```

### **解答**
```
int *pointer_to_n=&n;
*pointer_to_n++;
```