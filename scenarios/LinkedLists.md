# **链表**

## **介绍**

链接列表是使用指针实现的动态数据结构的最佳和最简单的示例。但是，了解指针对于理解链接列表的工作方式至关重要，因此如果您跳过指针教程，则应该返回并重做它。您还必须熟悉动态内存分配和结构。

从本质上讲，链接列表可以作为一个数组，可以根据需要从数组中的任何点进行增长和缩小。

链接列表比数组有一些优点：

  * 1.可以从列表中间添加或删除项目
  * 2.无需定义初始大小
但是，链表也有一些缺点：

  * 1.没有“随机”访问 - 如果没有首先迭代所有项目直到该项目，就不可能到达数组中的第n个项目。这意味着我们必须从列表的开头开始，计算我们在列表中前进的次数，直到我们到达所需的项目。
  * 2.需要动态内存分配和指针，这会使代码复杂化并增加内存泄漏和段错误的风险。
  * 3.链表比数组有更大的开销，因为链表项是动态分配的（内存使用效率较低），列表中的每个项也必须存储一个额外的指针。

## **什么是链表？**

链表是一组动态分配的节点，以这样的方式排列，即每个节点包含一个值和一个指针。指针始终指向列表的下一个成员。如果指针为NULL，则它是列表中的最后一个节点。

使用指向列表的第一项的本地指针变量来保持链接列表。如果该指针也为NULL，则该列表被视为空。

```
---------------         ---------------
|      |      |         |      |      |
| DATA | NEXT |-------->| DATA | NEXT |
|      |      |         |      |      |
---------------         ---------------
```
让我们定义一个链表节点：

```
typedef struct node {
    int val;
    struct node * next;
} node_t;
```

请注意，我们以递归方式定义结构，这在C中是可能的。让我们命名我们的节点类型node_t。

现在我们可以使用节点了。让我们创建一个局部变量，指向列表的第一项（称为head）。

```
node_t * head = NULL;
head = malloc(sizeof(node_t));
if (head == NULL) {
    return 1;
}

head->val = 1;
head->next = NULL;
```

我们刚刚在列表中创建了第一个变量。如果我们想完成填充列表，我们必须设置值，并将下一个项设置为空。请注意，我们应该始终检查malloc是否返回NULL值。

要将变量添加到列表的末尾，我们可以继续前进到下一个指针：

```
node_t * head = NULL;
head = malloc(sizeof(node_t));
head->val = 1;
head->next = malloc(sizeof(node_t));
head->next->val = 2;
head->next->next = NULL;
```

这可以继续，但我们应该做的是前进到列表的最后一项，直到next变量为止NULL。

## **迭代列表**

让我们构建一个打印出列表中所有项目的函数。为此，我们需要使用一个current指针来跟踪我们当前正在打印的节点。在打印节点的值之后，我们将current 指针设置为下一个节点，然后再次打印，直到我们到达列表的末尾（下一个节点为NULL）。

```
void print_list(node_t * head) {
    node_t * current = head;

    while (current != NULL) {
        printf("%d\n", current->val);
        current = current->next;
    }
}
```

## **将项添加到列表的末尾**

为了迭代链表的所有成员，我们使用一个名为的指针current。我们将其设置为从头部开始，然后在每个步骤中，我们将指针前进到列表中的下一个项目，直到我们到达最后一个项目。

void push(node_t * head, int val) {
    node_t * current = head;
    while (current->next != NULL) {
        current = current->next;
    }

    /* now we can add a new variable */
    current->next = malloc(sizeof(node_t));
    current->next->val = val;
    current->next->next = NULL;
}

链表的最佳用例是堆栈和队列，我们​​现在将实现它们：

## **将项添加到列表的开头（推送到列表）**

要添加到列表的开头，我们需要执行以下操作：

  * 1.创建一个新项目并设置其值
  * 2.链接新项目以指向列表的头部
  * 3.将列表的头部设置为我们的新项目
这将有效地创建一个带有新值的列表的新头，并保持列表的其余部分链接到它。

由于我们使用函数来执行此操作，因此我们希望能够修改head变量。要做到这一点，我们必须传递一个指向指针变量（双指针）的指针，这样我们就可以修改指针本身。

```
void push(node_t ** head, int val) {
    node_t * new_node;
    new_node = malloc(sizeof(node_t));

    new_node->val = val;
    new_node->next = *head;
    *head = new_node;
}
```
## **删除第一个项目（从列表中弹出）**

要弹出变量，我们需要撤消此操作：

  * 1.取下头指向的下一个项目并保存
  * 2.释放头项目
  * 3.将头部设置为我们存储在侧面的下一个项目
这是代码：

```
int pop(node_t ** head) {
    int retval = -1;
    node_t * next_node = NULL;

    if (*head == NULL) {
        return -1;
    }

    next_node = (*head)->next;
    retval = (*head)->val;
    free(*head);
    *head = next_node;

    return retval;
}
```
## **删除列表的最后一项**

从列表中删除最后一项非常类似于将其添加到列表的末尾，但有一个很大的例外 - 因为我们必须在最后一项之前更改一个项目，所以我们实际上必须先查看两个项目并查看是否下一项是列表中的最后一项：

```
int remove_last(node_t * head) {
    int retval = 0;
    /* if there is only one item in the list, remove it */
    if (head->next == NULL) {
        retval = head->val;
        free(head);
        return retval;
    }

    /* get to the second to last node in the list */
    node_t * current = head;
    while (current->next->next != NULL) {
        current = current->next;
    }

    /* now current points to the second to last item of the list, so let's remove current->next */
    retval = current->next->val;
    free(current->next);
    current->next = NULL;
    return retval;

}
```

## **删除特定项目**

要从列表中删除特定项目，无论是通过列表开头的索引还是通过其值，我们都需要检查所有项目，不断向前看，看看我们是否已经到达项目之前的节点我们希望删除。这是因为我们需要将位置更改为上一个节点指向的位置。

这是算法：

  * 1.在我们要删除的节点之前迭代到节点
  * 2.将我们要删除的节点保存在临时指针中
  * 3.将上一个节点的下一个指针设置为指向我们要删除的节点之后的节点
  * 4.使用临时指针删除节点
我们需要处理一些边缘情况，因此请确保您理解代码。

```
int remove_by_index(node_t ** head, int n) {
    int i = 0;
    int retval = -1;
    node_t * current = *head;
    node_t * temp_node = NULL;

    if (n == 0) {
        return pop(head);
    }

    for (i = 0; i < n-1; i++) {
        if (current->next == NULL) {
            return -1;
        }
        current = current->next;
    }

    temp_node = current->next;
    retval = temp_node->val;
    current->next = temp_node->next;
    free(temp_node);

    return retval;

}
```

## **练习**

您必须实现remove_by_value接收到头部的双指针的函数，并删除列表中具有该值的第一个项目val。

```
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int val;
    struct node * next;
} node_t;

void print_list(node_t * head) {
    node_t * current = head;

    while (current != NULL) {
        printf("%d\n", current->val);
        current = current->next;
    }
}

int pop(node_t ** head) {
    int retval = -1;
    node_t * next_node = NULL;

    if (*head == NULL) {
        return -1;
    }

    next_node = (*head)->next;
    retval = (*head)->val;
    free(*head);
    *head = next_node;

    return retval;
}

int remove_by_value(node_t ** head, int val) {
    /* TODO: fill in your code here */
}

int main() {

    node_t * test_list = malloc(sizeof(node_t));
    test_list->val = 1;
    test_list->next = malloc(sizeof(node_t));
    test_list->next->val = 2;
    test_list->next->next = malloc(sizeof(node_t));
    test_list->next->next->val = 3;
    test_list->next->next->next = malloc(sizeof(node_t));
    test_list->next->next->next->val = 4;
    test_list->next->next->next->next = NULL;

    remove_by_value(&test_list, 3);

    print_list(test_list);
}
```

### **解答**

```
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int val;
    struct node * next;
} node_t;

void print_list(node_t * head) {
    node_t * current = head;

    while (current != NULL) {
        printf("%d\n", current->val);
        current = current->next;
    }
}

int pop(node_t ** head) {
    int retval = -1;
    node_t * next_node = NULL;

    if (*head == NULL) {
        return -1;
    }

    next_node = (*head)->next;
    retval = (*head)->val;
    free(*head);
    *head = next_node;

    return retval;
}

int remove_by_value(node_t ** head, int val) {
    node_t *previous, *current;

    if (*head == NULL) {
        return -1;
    }

    if ((*head)->val == val) {
        return pop(head);
    }

    previous = current = (*head)->next;
    while (current) {
        if (current->val == val) {
            previous->next = current->next;
            free(current);
            return val;
        }

        previous = current;
        current  = current->next;
    }
    return -1;
}

void delete_list(node_t *head) {
    node_t  *current = head, 
            *next = head;

    while (current) {
        next = current->next;
        free(current);
        current = next;
    }
}

int main(void) {
    node_t * test_list = malloc(sizeof(node_t));

    test_list->val = 1;
    test_list->next = malloc(sizeof(node_t));
    test_list->next->val = 2;
    test_list->next->next = malloc(sizeof(node_t));
    test_list->next->next->val = 3;
    test_list->next->next->next = malloc(sizeof(node_t));
    test_list->next->next->next->val = 4;
    test_list->next->next->next->next = NULL;

    remove_by_value(&test_list, 3);

    print_list(test_list);
    delete_list(test_list);

    return EXIT_SUCCESS;
}
```
