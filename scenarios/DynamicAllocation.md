# **动态分配**

动态分配内存是C中非常重要的主题。它允许构建复杂的数据结构，例如链表。动态分配内存有助于我们在编写程序时最初不知道数据大小的情况下存储数据。

要动态分配一块内存，我们必须准备一个指针来存储新分配的内存的位置。我们可以使用相同的指针访问分配给我们的内存，一旦我们完成使用它，我们就可以使用该指针再次释放内存。

假设我们想要动态分配人员结构。这个人定义如下：

```
typedef struct {
    char * name;
    int age;
} person;
```

要在myperson参数中分配新人，我们使用以下语法：

```
person * myperson = malloc(sizeof(person));
```

这告诉编译器我们想要动态分配足以在内存中保存person结构，然后返回指向新分配数据的指针。

请注意，这sizeof不是一个实际的函数，因为编译器会解释它并将其转换为person结构的实际内存大小。

要访问此人的成员，我们可以使用以下->符号：

```
myperson->name = "John";
myperson->age = 27;
```

完成使用动态分配的结构后，我们可以使用free以下命令释放它：

```
free(myperson);
```

请注意，free不会删除myperson变量本身，它只是释放它指向的数据。该myperson变量仍然指向内存的某个地方-但打完电话后myperson，我们不允许再访问该地区。在我们使用它分配新数据之前，我们不能再使用该指针。

## **练习**

使用malloc动态分配的点结构。

```
#include <stdio.h>
#include <stdlib.h>

typedef struct {
  int x;
  int y;
} point;

int main() {
  point * mypoint;

  /* Dynamically allocate a new point
     struct which mypoint points to here */

  mypoint->x = 10;
  mypoint->y =5 ;
  printf("mypoint coordinates: %d, %d\n", mypoint->x, mypoint->y);

  free(mypoint);
  return 0;
}
```

### **解答**
```
mypoint = malloc(sizeof(point));
```