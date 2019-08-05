# **指针运算**

您以前学过什么是指针以及如何操作指针。在本教程中，您将学习指针的算术运算。有多种算术运算可以应用于C指针：++， - ， - ，+

## **使用（++）递增指针**

就像任何变量一样，++操作会增加该变量的值。在我们的例子中，变量是一个指针，因此当我们增加它的值时，我们增加了指针所指向的内存中的地址。在我们的示例中，让我们将此操作与数组结合起来：

```
#include <stdio.h>

int main()
{
    int intarray[5] = {10,20,30,40,50};

    int i;
    for(i = 0; i < 5; i++)
        printf("intarray[%d] has value %d - and address @ %x\n", i, intarray[i], &intarray[i]);

    int *intpointer = &intarray[3]; //point to the 4th element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 4th element

    intpointer++; //now increase the pointer's address so it points to the 5th elemnt in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 5th element

    return 0;
}
```

## **用（ - ）减少指针**

就像在前面的例子中一样，我们使用++运算符将指针的指向地址增加了一个，我们可以使用减量运算符（ - ）减少指向的地址。

```
#include <stdio.h>

int main()
{
    int intarray[5] = {10,20,30,40,50};

    int i;
    for(i = 0; i < 5; i++)
        printf("intarray[%d] has value %d - and address @ %x\n", i, intarray[i], &intarray[i]);

    int *intpointer = &intarray[4]; //point to the 5th element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 5th element

    intpointer--; //now decrease the point's address so it points to the 4th element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 4th element

    return 0;
}
```

## **添加指针（+）**

我们之前将指针的指向地址增加了一个。我们也可以用整数值增加它：

```
#include <stdio.h>

int main()
{
    int intarray[5] = {10,20,30,40,50};

    int i;
    for(i = 0; i < 5; i++)
        printf("intarray[%d] has value: %d - and address @ %x\n", i, intarray[i], &intarray[i]);

    int *intpointer = &intarray[1]; //point to the 2nd element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 2nd element

    intpointer += 2; //now shift by two the point's address so it points to the 4th element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the addres of the 4th element

    return 0;
}
```

请注意输出中的地址如何在内存中移位8步。你可能想知道为什么？答案很简单：因为我们的指针是一个int指针，并且int变量的大小是4个字节，所以内存可以移位4个块。在我们的代码中，我们将2（加上+2）移动到初始地址，这样就使它们成为2 x 4字节= 8。

## **用（ - ）减去指针**

同样我们可以减去：

```
#include <stdio.h>

int main()
{
    int intarray[5] = {10,20,30,40,50};

    int i;
    for(i = 0; i < 5; i++)
        printf("intarray[%d] has value: %d - and address @ %x\n", i, intarray[i], &intarray[i]);

    int *intpointer = &intarray[4]; //point to the 5th element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 5th element

    intpointer -= 2; //now shift by two the point's address so it points to the 3rd element in the array
    printf("address: %x - has value %d\n", intpointer, *intpointer); //print the address of the 3rd element

    return 0;
}
```

再次，地址被4字节的块移位（在int的情况下）。

## **其他操作**

还有更多的操作，例如比较>，<，==。这个想法与比较变量非常相似，但在这种情况下我们正在比较内存地址。

## **练习**

将intarray的最后三个地址复制到parray中，这是一个指向int的指针数组。

```
    #include <stdio.h>
	
    int main() {
    	int intarray[5] = {10,20,30,40,50};
        //-----------------------^
        int *pointer = &intarray[2];

        // Array of 3 pointers
        int *parray[3];

        // Copy last three addresses of intarray into parray
        // Use parray and pointer
        int i;
        for (i = 0; i < 3; i++) {
            // Insert code here
        }

        // Test code
        for (i = 0; i < 3; i++) {
            if (parray[i] == &pointer[i]) {
                printf("Matched!\n");
            } else {
                printf("Fail\n");
            }
        }

        return 0;
    }
```

### **解答**

```
    #include <stdio.h>

    int main() {
        int intarray[5] = {10,20,30,40,50};
        //-----------------------^
        int *pointer = &intarray[2];

        int *parray[3];

        int i;
        for (i = 0; i < 3; i++) {
            parray[i] = pointer + i;
        }

        for (i = 0; i < 3; i++) {
            if (parray[i] == &pointer[i]) {
                printf("Matched!\n");
            } else {
                printf("Fail\n");
            }
        }

        return 0;
    }
  
  
```