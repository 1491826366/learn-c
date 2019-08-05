# **条件**

## **做决定**
在生活中，我们都必须做出决定。为了做出决定，我们权衡了我们的选择，我们的计划也是如此。

以下是C中的决策结构的一般形式。

```
int target = 10;
if (target == 10) {
    printf("Target is equal to 10");
}
```
## **if条件**
if语句允许我们检查表达式是否true或false，并根据该结果执行不同的代码。

要评估两个变量是否相等，请使用==运算符，就像在第一个示例中一样。

不等式运算符也可用于计算表达式。例如：

```
int foo = 1;
int bar = 2;

if (foo < bar) {
    printf("foo is smaller than bar.");
}

if (foo > bar) {
    printf("foo is greater than bar.");
}
```

else当表达式求值时，我们可以使用关键字来表示代码false。

```
int foo = 1;
int bar = 2;

if (foo < bar) {
    printf("foo is smaller than bar.");
} else {
    printf("foo is greater than bar.");
}
```

有时我们会有两种以上的结果可供选择。在这些情况下，我们可以将多个if else语句“链接” 在一起。

```
int foo = 1;
int bar = 2;

if (foo < bar) {
    printf("foo is smaller than bar.");
} else if (foo == bar) {
    printf("foo is equal to bar.");
} else {
    printf("foo is greater than bar.");
}
```

if else如果您愿意，也可以嵌套语句。

```
int peanuts_eaten = 22;
int peanuts_in_jar = 100;
int max_peanut_limit = 50;

if (peanuts_in_jar > 80) {
    if (peanuts_eaten < max_peanut_limit) {
        printf("Take as many peanuts as you want!\n");
    }
} else {
    if (peanuts_eaten > peanuts_in_jar) {
        printf("You can't have anymore peanuts!\n");
    }
    else {
        printf("Alright, just one more peanut.\n");
    }
}
```

可以使用逻辑运算符一起评估两个或更多表达式，以检查两个表达式是否true一起评估，或者至少其中一个表达式。要检查两个表达式是否都计算true，请使用AND运算符&&。要检查表达式中是否至少有一个求值true，请使用OR运算符||。

```
int foo = 1;
int bar = 2;
int moo = 3;

if (foo < bar && moo > bar) {
    printf("foo is smaller than bar AND moo is larger than bar.");
}

if (foo < bar || moo > bar) {
    printf("foo is smaller than bar OR moo is larger than bar.");
}
```

NOT运算符!也可以同样使用：

```
int target = 9;
if (target != 10) {
    printf("Target is not equal to 10");
}
```
## **练习**
在本练习中，您必须if在guessNumber函数语句中构造一个语句，该语句检查该数字guess是否等于555.如果是这种情况，则必须使用printf“正确。您猜对了！” 打印出该函数。如果guess小于555，则必须使用printf“您的猜测太低” 打印出该功能。如果guess大于555，则必须使用printf“您的猜测太高” 打印出该功能。

```
#include <stdio.h>

int main() {
    guessNumber(500);
    guessNumber(600);
    guessNumber(555);
}

void guessNumber(int guess) {
    // TODO: write your code here
}
```
### **解答**
```
if(guess==555) printf("正确，您猜对了");
else if(guess>555) printf("您的猜测太高了");
else printf("您的猜测太低了");
```