# **共同体**

C Unions与C Structures基本相同，不同之处在于Union不允许包含多个变量，每个变量都有自己的内存，而Union允许同一个变量使用多个名称。这些名称可以将内存视为不同的类型（并且联合的大小将是最大类型的大小，+编译器可能决定给它的任何填充）

因此，如果您希望能够以不同的方式读取变量的内存，例如一次读取整数一个字节，您可以使用以下内容：

```
union intParts {
  int theInt;
  char bytes[sizeof(int)];
};
```

允许您单独查看每个字节而不使用指针并使用指针算法：

```
union intParts parts;
parts.theInt = 5968145; // arbitrary number > 255 (1 byte)

printf("The int is %i\nThe bytes are [%i, %i, %i, %i]\n",
parts.theInt, parts.bytes[0], parts.bytes[1], parts.bytes[2], parts.bytes[3]);

// vs

int theInt = parts.theInt;
printf("The int is %i\nThe bytes are [%i, %i, %i, %i]\n",
theInt, *((char*)&theInt+0), *((char*)&theInt+1), *((char*)&theInt+2), *((char*)&theInt+3));

// or with array syntax which can be a tiny bit nicer sometimes

printf("The int is %i\nThe bytes are [%i, %i, %i, %i]\n",
    theInt, ((char*)&theInt)[0], ((char*)&theInt)[1], ((char*)&theInt)[2], ((char*)&theInt)[3]);
```

将其与结构相结合，您可以创建一个“标记”联合，可以用于存储多个不同类型，一次一个。

例如，您可能有一个“数字”结构，但您不想使用这样的东西：

```
struct operator {
    int intNum;
    float floatNum;
    int type;
    double doubleNum;
};
```

因为你的程序有很多，并且所有变量都需要太多的内存，所以你可以使用它：

```
struct operator {
    int type;
    union {
      int intNum;
      float floatNum;
      double doubleNum;
    } types;
};
```

像这样，struct的大小只是int type的大小+ union中最大类型的大小（double）。不是一个巨大的收益，只有8或16个字节，但这个概念可以应用于类似的结构。

使用：

```
operator op;
op.type = 0; // int, probably better as an enum or macro constant
op.types.intNum = 352;
```

此外，如果您没有给联盟一个名称，那么它的成员可以直接从结构中访问：

```
struct operator {
    int type;
    union {
        int intNum;
        float floatNum;
        double doubleNum;
    }; // no name!
};

operator op;
op.type = 0; // int
// intNum is part of the union, but since it's not named you access it directly off the struct itself
op.intNum = 352;
```

在那个例子中，你可以看到有一个结构包含美国的四个（普通）硬币。

由于union使变量共享相同的内存，因此coins数组与struct中的每个int匹配（按顺序）：

```
union Coins change;
for(int i = 0; i < sizeof(change) / sizeof(int); ++i)
{
    scanf("%i", change.coins + i); // BAD code! input is always suspect!
}
printf("There are %i quarters, %i dimes, %i nickels, and %i pennies\n",
    change.quarter, change.dime, change.nickel, change.penny);
```

## **练习**

创建一个存储21个字符和6个整数的数组的联合（6个自21/4 == 5，但5 * 4 == 20，因此本练习需要1个以上），您将整数设置为6给定值，然后将字符数组打印为一系列字符和字符串。

```
    #include <stdio.h>
  
    /* define the union here */
  
    int main() {
    
        // initializer lists like this are assigned to the first member of the union/struct!
        // There are 6 ints here so...
        <union declaration> intCharacters = {{1853169737, 1936876900, 1684955508, 1768838432, 561213039, 0}};
      
        /* testing code */
        printf("[");
        // only go to 18 because 1 byte is for the terminating 0 and we don't print the last in the loop
        for(int i = 0; i < 19; ++i)
            printf("%c, ", intCharacters.chars[i]);
        printf("%c]\n", intCharacters.chars[19]);
    
        printf("%s\n", intCharacters.chars);
    }
```

### **解答**

```
    #include <stdio.h>
  
    union hiddenMessage {
        int  ints[6];
        char chars[21];
    };
  
    int main() {
        union hiddenMessage intCharacters = {{1853169737, 1936876900, 1684955508, 1768838432, 561213039, 0}};
    
        printf("[");
        // only go to 18 because 1 byte is for the terminating 0 and we don't print the last in the loop
        for(int i = 0; i < 19; ++i)
            printf("%c, ", intCharacters.chars[i]);
        printf("%c]\n", intCharacters.chars[19]);
        printf("%s\n", intCharacters.chars);
    }
```