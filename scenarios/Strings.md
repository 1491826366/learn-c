# **字符串**

## **定义字符串**
C中的字符串实际上是字符数组。尽管在C中使用指针是一个高级主题，稍后将对此进行详细说明，但我们将使用指向字符数组的指针来定义简单字符串，方法如下：

```
char * name = "John Smith";
```

此方法创建一个我们只能用于阅读的字符串。如果我们希望定义一个可以操作的字符串，我们需要将其定义为本地字符数组：

```
char name[] = "John Smith";
```

这种表示法是不同的，因为它分配了一个数组变量，所以我们可以操纵它。空括号表示法告诉编译器自动计算数组的大小。这实际上与显式分配它相同，在字符串的长度上添加一个：[]

```
char name[] = "John Smith";
/* is the same as */
char name[11] = "John Smith";
```

我们需要添加一个的原因，虽然字符串John Smith长度正好是10个字符，但是用于字符串终止：一个特殊字符（等于0），表示字符串的结尾。标记字符串的末尾是因为程序不知道字符串的长度 - 只有编译器根据代码知道它。

## **使用printf进行字符串格式化**
我们可以使用该printf命令将字符串与其他字符串一起格式化，方式如下：

```
char * name = "John Smith";
int age = 27;

/* prints out 'John Smith is 27 years old.' */
printf("%s is %d years old.\n", name, age);
```

请注意，在打印字符串时，我们必须添加换行符（\n）字符，以便我们的下一个printf语句将以新行打印。

## **字符串长度**
函数'strlen'返回必须作为参数传递的字符串的长度：

```
char * name = "Nikhil";
printf("%d\n",strlen(name));
```

## **字符串比较**
该函数strncmp在两个字符串之间进行比较，如果它们相等则返回数字0，如果它们不同则返回不同的数字。参数是要比较的两个字符串，以及最大比较长度。此函数还有一个不安全的版本strcmp，但不建议使用它。例如：

```
char * name = "John";

if (strncmp(name, "John", 4) == 0) {
    printf("Hello, John!\n");
} else {
    printf("You are not John. Go away.\n");
}
```

## **字符串连接**
函数'strncat'将src字符串字符串的前n个字符追加到目标字符串，其中n是min（n，length（src））; 传递的参数是目标字符串，源字符串和n - 要追加的最大字符数。例如：

```
char dest[20]="Hello";
char src[20]="World";
strncat(dest,src,3);
printf("%s\n",dest);
strncat(dest,src,20);
printf("%s\n",dest);
```

## **练习**
定义字符串first_name与值John使用指示器符号，并定义字符串last_name与值Doe 使用本地数组符号。

```
#include <stdio.h>
#include <string.h>
int main() {
  /* define first_name */
  /* define last_name */
  char name[100];

  last_name[0] = 'B';
  sprintf(name, "%s %s", first_name, last_name);
  if (strncmp(name, "John Boe", 100) == 0) {
      printf("Done!\n");
  }
  name[0]='\0';
  strncat(name,first_name,4);
  strncat(name,last_name,20);
  printf("%s\n",name);
  return 0;
}
```

### **解答**
```
char first_name[50];
char last_name[50];
```