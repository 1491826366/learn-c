# **结构**

C结构是特殊的大变量，里面包含几个命名变量。结构是C中对象和类的基础。结构用于：
  * 数据序列化
  * 通过单个参数将多个参数传入和传出函数
  * 数据结构，如链表，二叉树等
结构的最基本的例子是点，它是包含两个变量的单个实体 - x和y。让我们定义一个观点：

```
struct point {
    int x;
    int y;
};
```

现在，让我们定义一个新点，然后使用它。假设函数draw接收一个点并在屏幕上绘制它。如果没有结构，使用它将需要两个参数 - 每个参数对应于每个坐标：

```
/* draws a point at 10, 5 */
int x = 10;
int y = 5;
draw(x, y);
```

使用结构，我们可以传递一个点参数：

```
/* draws a point at 10, 5 */
struct point p;
p.x = 10;
p.y = 5;
draw(p);

```
要访问点的变量，我们使用点.运算符。

## **类型定义**

Typedef允许我们定义具有不同名称的类型 - 在处理结构和指针时可以派上用场。在这种情况下，我们想要摆脱点结构的长定义。我们可以使用以下语法struct从每次要定义新点时删除关键字：

```
typedef struct {
    int x;
    int y;
} point;
```

这将允许我们定义一个像这样的新点：

```
point p;
```

结构也可以保存指针 - 这允许它们保持字符串，或指向其他结构的指针 - 这是它们的真正力量。例如，我们可以通过以下方式定义车辆结构：

```
typedef struct {
    char * brand;
    int model;
} vehicle;
```

由于品牌是char指针，因此车辆类型可以包含字符串（在这种情况下，表示车辆的品牌）。

```
vehicle mycar;
mycar.brand = "Ford";
mycar.model = 2007;
```

## **练习**

定义一个名为“person”的新数据结构，其中包含一个调用的字符串（指向char的指针）name和一个名为的整数age。

```
#include <stdio.h>

/* define the person struct here using the typedef syntax */

int main() {
    person john;

    /* testing code */
    john.name = "John";
    john.age = 27;
    printf("%s is %d years old.", john.name, john.age);
}
```

### **解答**
```
typedef struct{
  char *name;
  int age;
}person;
```