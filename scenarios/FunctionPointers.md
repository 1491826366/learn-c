# **函数指针**

记得指针？我们使用它们指向一个字符数组，然后从中生成一个字符串。当我们学会如何控制这些指针时，事情变得更有趣。现在是时候用指针做一些更有趣的事情，使用它们来指向和调用函数。

## **为什么指向一个函数？**

您可能会想到的第一个问题是，当我们只需通过名称调用函数时，为什么我们会使用指针来调用函数：- 这是一个很好的问题！现在想象一下您需要对数组进行排序的函数。有时您希望按升序或降序排序数组元素。你会如何选择？函数指针！

## **函数指针语法**

```
void (*pf)(int);
```

我同意你的看法。这绝对是非常复杂的，或者你可能会想到。让我们重新阅读该代码并尝试逐点理解它。从里到外阅读。*pf是指向函数的指针。void是该函数的返回类型，最后int是该函数的参数类型。得到它了？好。

让我们在函数指针中插入指针并尝试再次读取它：

```
char* (*pf)(int*)
```

再说一遍：1。*pf是函数指针。2. char*是该函数的返回类型。3. int*是参数的类型。

理论上还不错。让我们用一些真正的代码弄脏手。看这个例子：

```
#include <stdio.h>
void someFunction(int arg)
{
    printf("This is someFunction being called and arg is: %d\n", arg);
    printf("Whoops leaving the function now!\n");
}

main()
{
    void (*pf)(int);
    pf = &someFunction;
    printf("We're about to call someFunction() using a pointer!\n");
    (pf)(5);
    printf("Wow that was cool. Back to main now!\n\n");
}
```

还记得我们之前谈过的吗？我们也可以这样做。我们可以使用我们自己的比较函数sort()执行相反的操作，而不是按升序排序集合，如下所示：

```
#include <stdio.h>
#include <stdlib.h> //for qsort()

int compare(const void* left, const void* right)
{
    return (*(int*)right - *(int*)left);
    // go back to ref if this seems complicated: http://www.cplusplus.com/reference/cstdlib/qsort/
}
main()
{
    int (*cmp) (const void* , const void*);
    cmp = &compare;

    int iarray[] = {1,2,3,4,5,6,7,8,9};
    qsort(iarray, sizeof(iarray)/sizeof(*iarray), sizeof(*iarray), cmp);

    int c = 0;
    while (c < sizeof(iarray)/sizeof(*iarray))
    {
        printf("%d \t", iarray[c]);
        c++;
    }
}
```

让我们再次记住。为什么我们使用函数指针？1.允许程序员使用库来实现不同的用法 - >“灵活性”

## **练习**

```
    #include <stdio.h>

    void f1(int var)
    {
            printf("this is f1 and var is: %d\n", var);
    }

    void f2(int var)
    {
            printf("this is f2 and var is: %d\n", var);
    }

    void f3(int var)
    {
            printf("this is f3 and var is: %d\n", var);
    }

    int main()
    {
                /* define an array full of function pointers 
                to the above functions, that take an `int` as 
                their only argument */


		int c = 0;
		while(c < 3)
		{
                        /* call the functions using the function pointers
                        of the array at index `c` with `c` as an argument */

			++c;
		}

	  return 0;
    }
```

### **解答**

```
    #include <stdio.h>

    void f1(int var)
    {
            printf("this is f1 and var is: %d\n", var);
    }

    void f2(int var)
    {
            printf("this is f2 and var is: %d\n", var);
    }

    void f3(int var)
    {
            printf("this is f3 and var is: %d\n", var);
    }

    int main()
    {
		void (*pf[])(int) = {f1, f2, f3};

		int c = 0;
		while(c < 3)
		{
			pf[c](c);
			++c;
		}

		return 0;
    }
```