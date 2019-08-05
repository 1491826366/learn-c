# **数组和指针**

在之前的Pointers教程中，您了解到指向给定数据类型的指针可以存储该特定数据类型的任何变量的地址。例如，在以下代码中，指针变量pc存储字符变量的地址c。

```
char c = 'A';
char *pc = &c;
```

这c是一个只能存储单个值的标量变量。但是，您已经熟悉可以在连续分配的内存块中保存相同数据类型的多个值的数组。所以，您可能想知道，我们是否也可以指向数组？的确，我们可以。

让我们从示例代码开始，看看它的输出。我们将在后面讨论它的行为。

```
char vowels[] = {'A', 'E', 'I', 'O', 'U'};
char *pvowels = &vowels;
int i;

// Print the addresses
for (i = 0; i < 5; i++) {
    printf("&vowels[%d]: %u, pvowels + %d: %u, vowels + %d: %u\n", i, &vowels[i], i, pvowels + i, i, vowels + i);
}

// Print the values
for (i = 0; i < 5; i++) {
    printf("vowels[%d]: %c, *(pvowels + %d): %c, *(vowels + %d): %c\n", i, vowels[i], i, *(pvowels + i), i, *(vowels + i));
}
```

以上代码的典型输出如下所示。

＆元音[0]：4287605531，pvowels + 0：4287605531，元音+ 0：4287605531

＆元音[1]：4287605532，pvowels + 1：4287605532，元音+ 1：4287605532

＆元音[2]：4287605533，pvowels + 2：4287605533，元音+ 2：4287605533

＆元音[3]：4287605534，pvowels + 3：4287605534，元音+ 3：4287605534

＆元音[4]：4287605535，pvowels + 4：4287605535，元音+4：4287605535

元音[0]：A，*（pvowels + 0）：A，*（元音+ 0）：A

元音[1]：E，*（pvowels + 1）：E，*（元音+ 1）：E

元音[2]：我，*（pvowels + 2）：我，*（元音+ 2）：我

元音[3]：O，*（pvowels + 3）：O，*（元音+3）：O

元音[4]：U，*（pvowels + 4）：U，*（元音+4）：U

正如你猜对了，给出了数组第i个元素的内存位置。此外，由于这是一个字符数组，每个元素占用一个字节，因此连续的存储器地址被一个字节分开。我们还创建了一个指针，并为其分配了数组的地址。是一个有效的操作; 虽然总的来说，这可能并不总是有意义的（在Pointer Arithmetics中进一步探讨）。特别是，上面显示的输出表示并且是等效的。随意更改数组和指针变量的数据类型以测试它。&vowels[i]vowelspvowelsvowelspvowels + i&vowels[i]pvowels + i

如果你仔细看看前面的代码，你会注意到我们还使用了另一个明显令人惊讶的符号：。此外，和返回相同的事情-的地址我个数组的元素。在另一方面，并且都返回我阵列的第i个元素。为什么会这样？vowels + ipvowels + ivowels + ivowels*(pvowels + i)*(vowels + i)vowels

这是因为数组本身的名称是指向数组第一个元素的（常量）指针。换句话说，符号vowels，并且都指向相同的位置。&vowels[0]vowels + 0

您可以通过指针和数组进一步详细讨论该主题。

## **数组的动态内存分配**

到目前为止，我们知道我们可以使用指针遍历数组。此外，我们还知道我们可以使用块指针动态分配（连续）内存。可以组合这两个方面来动态地为阵列分配内存。这在以下代码中说明。

```
// Allocate memory to store five characters
int n = 5;
char *pvowels = (char *) malloc(n * sizeof(char));
int i;

pvowels[0] = 'A';
pvowels[1] = 'E';
*(pvowels + 2) = 'I';
pvowels[3] = 'O';
*(pvowels + 4) = 'U';

for (i = 0; i < n; i++) {
    printf("%c ", pvowels[i]);
}

printf("\n");

free(pvowels);
```

在上面的代码中，我们分配了五个连续的内存字节来存储五个字符。随后，我们使用数组符号来遍历内存块，就好像pvowels是一个数组一样。但是，请记住，pvowels实际上它是一个指针，并且如指针和数组中所指出的，指针和数组通常不是一回事。

那么什么时候有用呢？请记住，在声明数组时，必须事先知道它包含的元素数。因此，在某些情况下，可能会发生为阵列分配的空间要小于所需空间或太多的空间。但是，通过使用动态内存分配，可以分配程序所需的内存。此外，通过调用该free()函数，就可以释放未使用的内存。在不利的情况下，通过动态内存分配，必须负责任地调用free()。否则，将发生内存泄漏。

我们通过查看二维数组的动态内存分配来结束本教程。这可以以类似的方式推广到n维。与我们使用指针的一维数组不同，在这种情况下，我们需要一个指向指针的指针，如下所示。

```
int nrows = 2;
int ncols = 5;
int i, j;

// Allocate memory for nrows pointers
char **pvowels = (char **) malloc(nrows * sizeof(char *));

// For each row, allocate memory for ncols elements
pvowels[0] = (char *) malloc(ncols * sizeof(char));
pvowels[1] = (char *) malloc(ncols * sizeof(char));

pvowels[0][0] = 'A';
pvowels[0][1] = 'E';
pvowels[0][2] = 'I';
pvowels[0][3] = 'O';
pvowels[0][4] = 'U';

pvowels[1][0] = 'a';
pvowels[1][1] = 'e';
pvowels[1][2] = 'i';
pvowels[1][3] = 'o';
pvowels[1][4] = 'u';

for (i = 0; i < nrows; i++) {
    for(j = 0; j < ncols; j++) {
        printf("%c ", pvowels[i][j]);
    }

    printf("\n");
}

// Free individual rows
free(pvowels[0]);
free(pvowels[1]);

// Free the top-level pointer
free(pvowels);
```

## **练习**

帕斯卡三角形的前七行如下所示。请注意，第i行包含i个元素。因此，要存储前三行中的数字，需要1 + 2 + 3 = 6个内存插槽。

1

1 1

1 2 1

1 3 3 1

1 4 6 4 1

1 5 10 10 5 1

1 6 15 20 15 6 1

完成下面给出的框架代码，使用动态内存分配将Pascal三角形的前三行中的数字存储在二维“数组”中。请注意，您必须准确分配六个内存插槽来存储这六个数字。不应分配额外的内存。在程序结束时，释放此程序中使用的所有内存块。

```
#include <stdio.h>
#include <stdlib.h>

int main() {
    int i, j;
    /* TODO: define the 2D pointer variable here */

    /* TODO: complete the following line to allocate memory for holding three rows */
    pnumbers = (int **) malloc();

    /* TODO: allocate memory for storing the individual elements in a row */
    pnumbers[0] = (int *) malloc(1 * sizeof(int));

    pnumbers[0][0] = 1;
    pnumbers[1][0] = 1;
    pnumbers[1][1] = 1;
    pnumbers[2][0] = 1;
    pnumbers[2][1] = 2;
    pnumbers[2][2] = 1;

    for (i = 0; i < 3; i++) {
        for (j = 0; j <= i; j++) {
            printf("%d", pnumbers[i][j]);
        }
        printf("\n");
    }

    for (i = 0; i < 3; i++) {
        /* TODO: free memory allocated for each row */
    }

    /* TODO: free the top-level pointer */

  return 0;
}
```

### **解答**

```
#include <stdio.h>
#include <stdlib.h>

int main() {
    int i, j;
    /* TODO: define the 2D pointer variable here */
    int **pnumbers;

    /* TODO: Complete the following line to allocate memory for holding three rows */
    pnumbers = (int **) malloc(3  *sizeof(int *));

    /* TODO: Allocate memory for storing the individual elements in a row */
    pnumbers[0] = (int *) malloc(1 * sizeof(int));
    pnumbers[1] = (int *) malloc(2 * sizeof(int));
    pnumbers[2] = (int *) malloc(3 * sizeof(int));

    pnumbers[0][0] = 1;
    pnumbers[1][0] = 1;
    pnumbers[1][1] = 1;
    pnumbers[2][0] = 1;
    pnumbers[2][1] = 2;
    pnumbers[2][2] = 1;

    for (i = 0; i < 3; i++) {
        for (j = 0; j <= i; j++) {
            printf("%d", pnumbers[i][j]);
        }
        printf("\n");
    }

    for (i = 0; i < 3; i++) {
        free(pnumbers[i]);
    }

    free(pnumbers);

  return 0;
}
```