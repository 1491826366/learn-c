# **多维数组**

在之前的Arrays教程中，我们介绍了数组及其工作原理。我们看到的数组都是一维的，但C可以创建和使用多维数组。以下是多维数组声明的一般形式：

```
type name[size1][size2]...[sizeN]；
```

例如，这是一个基本的供您查看

```
int foo[1][2][3];
```

或者这个

```
char vowels[1][5]={
   {'a', 'e', 'i', 'o', 'u'}
};
```

## **二维数组**
最简单的多维数组形式是二维数组。二维数组几乎是一维数组的列表。要声明一个大小为[x][y]的二维整数数组，你会写这样的东西-
```
type arrayName [x][y];
```
其中type可以是任何C数据类型（int,char,long,long long,double等），arrayName将是有效的C标识符或变量。二维数组可以被认为是具有[x]行数和[y]列数的表。可以显示一个包含三行四列的二维数组a,并考虑如下-

     |Column 0|Column 1|Column 2|Column 3|
:---:|:------:|:------:|:------:|:------:|
Row 0|a[0][0] |a[0][1] |a[0][2] |a[0][3] |
Row 1|a[1][0] |a[1][1] |a[1][2] |a[1][3] |
Row 2|a[2][0] |a[2][1] |a[2][2] |a[2][3] |

从这个意义上来说，数组a中的每个元素都由a[i][j]形式的元素名称标识，其中'a'是数组的名称，'i'和'j'是索引唯一标识或显示'a'中的每个元素。

说实话，你不必真的输入[x]值，因为如果你做了这样的事情-
```
char vowels[][5]={
    {'A','E','I','O','U'},
    {'a','e','i','o','u'}
};
```
你可以说编译器将知道有两个“维度”，但是，你必须需要a[y]值，编译器虽然很聪明，但它不知道你在维度中使用了多少个整数，字符，浮点数。要记住这点。

## **初始化二维数组**
可以通过为每行指定括号[]值来使用多维数组。下面是一个包含3行的数组，每行有4列。为了使它更容易，你可以忘记3并保持空包，它仍然可以工作。

```
int a[3][4] = {  
   {0, 1, 2, 3} ,   /*  initializers for row indexed by 0 */
   {4, 5, 6, 7} ,   /*  initializers for row indexed by 1 */
   {8, 9, 10, 11}   /*  initializers for row indexed by 2 */
};
```
指示所需的内括号是可选的。以下初始化与前一个示例相同-

```
int a[3][4] = {0,1,2,3,4,5,6,7,8,9,10,11};
```

## **访问二维数组元素**
通过使用下标（即，数组的行索引和列索引）来访问二维数组中的元素。例如-
```
int val=a[2][3];
```
上面的语句将从数组的第3行获取第4个元素。

## **练习**
让我们试着找出两个学科，即数学和物理学的五个学生的平均分数。为此，我们使用一个名为的二维数组grades。与数学相对应的标记将存储在第一行（）中，而与物理相对应的标记将存储在第二行（）中。完成以下步骤，以便您可以执行此程序。grades[0]grades[1]

 * 将成绩声明为整数的二维数组
 * 通过指定终止条件来完成for循环
 * 计算每个科目获得的平均分数

```
	#include <stdio.h>

	int main() {
		/* TODO: declare the 2D array grades here */
		float average;
		int i;
		int j;

		grades[0][0] = 80;
		grades[0][1] = 70;
		grades[0][2] = 65;
		grades[0][3] = 89;
		grades[0][4] = 90;

		grades[1][0] = 85;
		grades[1][1] = 80;
		grades[1][2] = 80;
		grades[1][3] = 82;
		grades[1][4] = 87;

		/* TODO: complete the for loop with appropriate terminating conditions */
		for (i = 0; i < ; i++) {
			average = 0;
			for (j = 0; j < ; j++) {
				average += grades[i][j];
			}

			/* TODO: compute the average marks for subject i */
			printf("The average marks obtained in subject %d is: %.2f\n", i, average);
		}

		return 0;
	}
```

### **解答**
```
int grades[1][4];
for (i=0; i<2; i++)
for (j=0; j<5; j++)
average=average/10;
```