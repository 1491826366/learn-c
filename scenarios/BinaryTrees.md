# **二叉树**

## **介绍**

二叉树是一种数据结构，其中每个节点最多有两个子节点（左子节点和右子节点）。二叉树用于实现二叉搜索树和二进制堆，并用于高效搜索和排序。二叉树是K-ary树的特例，其中k是2.二叉树的常见操作包括插入，删除和遍历。如果树是平衡的，并且节点是叶节点还是分支节点，则执行这些操作的难度会有所不同。对于平衡树，每个节点的左右子树的深度相差1或更小。这允许可预测的深度，也称为高度。这是从根到叶的节点的度量，其中root为0，后续节点为（1,2..n）。这可以用log 2（n）的整数部分表示，其中n是树中节点的数量。

```
     g            s              9
    / \          / \            / \
   b   m        f   u          5   13
  / \              / \            / \
 c   d            t   y          11  15
```

在树上执行的操作需要以两种主要方式之一进行搜索：深度优先搜索和广度优先搜索。深度优先搜索（DFS）是用于遍历或搜索树或图数据结构的算法。一个从根开始，并在回溯之前尽可能沿着每个分支进行探索。深度优先搜索遍历有三种类型：预订访问，左，右，有序左，访问，右，后订单左，右，访问。广度优先搜索（BFS）是用于遍历或搜索树或图结构的算法。在级别顺序中，我们访问级别上的每个节点，然后再转到较低级别。

## **练习**

下面是具有插入和打印功能的二叉树的实现。这棵树是有序但不平衡的。此示例在插入时保持其排序。

将打印例程更改为先序深度优先搜索。

```
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
  int val;
  struct node * left;
  struct node * right;
} node_t;

void insert(node_t * tree,int val);
void print_tree(node_t * current);
void printDFS(node_t * current);

int main()
{
  node_t * test_list = malloc(sizeof(node_t));
  /* set values explicitly, alternative would be calloc() */
  test_list->val = 0;
  test_list->left = NULL;
  test_list->right = NULL;

  insert(test_list,5);
  insert(test_list,8);
  insert(test_list,4);
  insert(test_list,3);

  printDFS(test_list);
  printf("\n");
}

void insert(node_t * tree, int val)
{
  if (tree->val == 0)
  {
    /* insert on current (empty) position */
    tree->val=val;
  }
  else
  {
    if (val < tree->val)
    {
      /* insert left */
      if (tree->left != NULL)
      {
        insert(tree->left, val);
      }
      else
      {
        tree->left = malloc(sizeof(node_t));
        /* set values explicitly, alternative would be calloc() */
        tree->left->val = val;
        tree->left->left = NULL;
        tree->left->right = NULL;
      }
    }
    else
    {
      if (val >= tree->val)
      {
        /* insert right */
        if (tree->right != NULL)
        {
          insert(tree->right,val);
        }
        else
        {
          tree->right=malloc(sizeof(node_t));
          /* set values explicitly, alternative would be calloc() */
          tree->right->val=val;
          tree->right->left = NULL;
          tree->right->right = NULL;
        }
      }
    }
  }
}

/* depth-first search */
void printDFS(node_t * current)
{
  /* change the code here */
  if (current == NULL)         return;   /* security measure */
  if (current->left != NULL)   printDFS(current->left);
  if (current != NULL)         printf("%d ", current->val);
  if (current->right != NULL)  printDFS(current->right);
}
```

### **解答**

```
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
  int val;
  struct node * left;
  struct node * right;
} node_t;

void insert(node_t * tree,int val);
void print_tree(node_t * current);
void printDFS(node_t * current);

int main()
{
  node_t * test_list = malloc(sizeof(node_t));
  /* set values explicitly, alternative would be calloc() */
  test_list->val = 0;
  test_list->left = NULL;
  test_list->right = NULL;

  insert(test_list,5);
  insert(test_list,8);
  insert(test_list,4);
  insert(test_list,3);

  printDFS(test_list);
  printf("\n");
}

void insert(node_t * tree, int val)
{
  if (tree->val == 0)
  {
    /* insert on current (empty) position */
    tree->val=val;
  }
  else
  {
    if (val < tree->val)
    {
      /* insert left */
      if (tree->left != NULL)
      {
        insert(tree->left, val);
      }
      else
      {
        tree->left = malloc(sizeof(node_t));
        /* set values explicitly, alternative would be calloc() */
        tree->left->val = val;
        tree->left->left = NULL;
        tree->left->right = NULL;
      }
    }
    else
    {
      if (val >= tree->val)
      {
        /* insert right */
        if (tree->right != NULL)
        {
          insert(tree->right,val);
        }
        else
        {
          tree->right=malloc(sizeof(node_t));
          /* set values explicitly, alternative would be calloc() */
          tree->right->val=val;
          tree->right->left = NULL;
          tree->right->right = NULL;
        }
      }
    }
  }
}

/* depth-first search */
void printDFS(node_t * current)
{
  /* change the code here */
  if (current == NULL)         return;   /* security measure */
  if (current != NULL)         printf("%d ", current->val);
  if (current->left != NULL)   printDFS(current->left);
  if (current->right != NULL)  printDFS(current->right);
}
```