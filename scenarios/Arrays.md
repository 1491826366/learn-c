# **数组**

数组是特殊变量，可以在同一个变量名下保存多个值，并使用索引进行组织。使用非常简单的语法定义数组：

```
/* defines an array of 10 integers */
int numbers[10];
```

使用相同的语法从数组中访问数字。请注意，C中的数组是从零开始的，这意味着如果我们定义了一个大小为10的数组，则定义了数组单元格0到9(包括）。不是实际值。numbers[10]

```
int numbers[10];

/* populate the array */
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
numbers[3] = 40;
numbers[4] = 50;
numbers[5] = 60;
numbers[6] = 70;

/* print the 7th number from the array, which has an index of 6 */
printf("The 7th number in the array is %d",number[6]);
```

数组只能有一种类型的变量，因为它们是作为计算机内存中的一系列值实现的。因此，访问特定的阵列单元非常有效。

## **行使**
  * 下面的代码无法编译，因为grades缺少变量。
  * 缺少其中一个成绩。你能定义它，使得平均成绩是85吗？

### **练习**
```
#inlcude<studio.h>

int main(){
  /*TODO:在这里定义成绩变量*/
  int average;
  
  grades[0]=80;
  /* TODO:定义缺失的成绩
     这样平均值将达到85*/
  grades[2]=90;
  
  average=(grades[0]+grades[1]+grades[2])/3;
  printf("The average of the 3 grades is: %d",average);
  return 0;
}
```
### **解答**
```
grades[1]=85;
```