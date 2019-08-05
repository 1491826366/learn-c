# **静态**

static是C编程语言中的关键字。它可以与变量和函数一起使用。

## **什么是静态变量？**

默认情况下，变量是定义它们的作用域的本地变量。变量可以声明为static，以将其范围增加到包含它们的文件。因此，可以在文件内的任何位置访问这些变量。

考虑以下情况 - 我们想要计算参加比赛的参赛者：

```
#include<stdio.h>
int runner() {
    int count = 0;
    count++;
    return count;
}

int main()
{
    printf("%d ", runner());
    printf("%d ", runner());
    return 0;
}
```
我们将看到它count没有更新，因为它在函数完成后立即从内存中删除。static但是，如果使用：

```
#include<stdio.h>
int runner()
{
    static int count = 0;
    count++;
    return count;
}

int main()
{
    printf("%d ", runner());
    printf("%d ", runner());
    return 0;
}
```
## **什么是静态功能？**

默认情况下，函数在C中是全局的。如果我们声明一个函数static，该函数的范围将减少到包含它的文件。

语法如下所示：

```
static void fun(void) {
   printf("I am a static function.");
}
```

## **静态与全局？**

虽然静态变量在包含它们的文件上具有范围，使得它们只能在给定文件内访问，但全局变量也可以在文件外部访问。

## **练习**

在本练习中，尝试使用static关键字查找某些数字的总和。不要将表示运行总计的任何变量传递给函数sum().

```
   #include <stdio.h>
   int sum (int num) {
       /**
       * find sum to n numbers
       */
   }

   int main() {
       printf("%d ",sum(55));
       printf("%d ",sum(45));
       printf("%d ",sum(50));
       return 0;
   }
```

### **解答**

```
int sum(int num)
{
  static int count=0;
  count+=num;
  return count;
}
```
