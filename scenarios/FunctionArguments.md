# **函数参数引用**

函数参数按值传递，这意味着它们被复制进出函数。但是，如果我们将指针复制到值而不是值本身呢？这将使我们能够对父函数的变量和结构进行函数控制，而不仅仅是它们的副本。

假设我们想编写一个函数，将一个数字递增1，称为addone。这不起作用：

```
void addone(int n) {
    n++;
}

int n;
printf("Before: %d\n", n);
addone(n);
printf("After: %d\n", n);
```

但是，这将有效：

```
void addone(int * n) {
    (*n)++;
}

int n;
printf("Before: %d\n", n);
addone(&n);
printf("After: %d\n", n);
```

区别在于第二个版本addone接收指向变量的指针n作为参数，然后它可以操作它，因为它知道它在内存中的位置。

请注意，在调用addone函数时，我们必须传递对变量的引用n，而不是传递本身 - 这样做是为了使函数知道变量的地址，而不仅仅是接收变量本身的副本。

## **指向结构的指针**

比方说，我们要创造出两个向前移动一个点的功能x和y方向，称为move。我们现在只能发送一个指向点结构函数的指针，而不是发送两个指针：

```
void move(point * p) {
    (*p).x++;
    (*p).y++;
}
```

但是，如果我们希望取消引用结构并访问其中一个内部成员，我们会有一个简写语法，因为此操作广泛用于数据结构中。我们可以使用以下语法重写此函数：

```
void move(point * p) {
    p->x++;
    p->y++;
}
```

## **练习**

编写一个名为的函数birthday，它将个person的age加一。
```
#include <stdio.h>

typedef struct {
  char * name;
  int age;
} person;

/* function declaration */
void birthday(person * p);

/* write your function here */

int main() {
  person john;
  john.name = "John";
  john.age = 27;

  printf("%s is %d years old.\n", john.name, john.age);
  birthday(&john);
  printf("Happy birthday! %s is now %d years old.\n", john.name, john.age);

  return 0;
}
```

### **解答**
```
void birthday(person *p)
{
p->age++;
}
```