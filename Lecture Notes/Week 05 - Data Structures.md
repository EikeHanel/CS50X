# Data Structures
- **Notes:** https://cs50.harvard.edu/x/2024/notes/5/

## 1. Stacks and Queues
- **Queues**: 
  - **FIFO**: first in first out
  - **enqueue** (add)
  - **dequeue** (remove)

- **Stacks**:
  - **LIFO**: last in first out
  - **push**: (add)
  - **pop**: (remove)
- Queues and Stacks are abstract data types:
    ```c
    typedef struct
    {
        person people[CAPACITY];
        int size;
    } queue
    ```
    ```c
    typedef struct
    {
        person people[CAPACITY];
        int size;
    } stack
    ```
    - The CAPACITY will limit our stack or queue

## 2. Resizing Arrays
- To resize an array, your best bet in C is to create a tmp list with the needed memory and copy every datapoint into it, then add the final value.
  - Careful due to using mallic -> dont forget to free memory
- **Example Code**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>

  int main(void)
  {
      int*list = malloc(3 * sizeof(int));
      if (list == NULL)
      {
          return 1;
      }

      list[0] = 1;
      list[1] = 2;
      list[2] = 3;

      int *tmp = malloc(4 * sizeof(int));
      if (list == NULL)
      {
          free(list);
          return 1;
      }


      for (int i = 0; i < 3; i++)
      {
          tmp[i] = list[i];
      }
      tmp[4] = 4;

      free(list);
      list = tmp;

      for (int i = 0; i < 4; i++)
      {
          printf("%i\n", list[i]);
      }

      free(list);
      return 0;
  }
  ```

## 3. Linked Lists
- Variables are stored where there is space. Then the new variable in this linked list gets saved somewhere. Then they are connected via a pointer.
- Every variable stored is basically a arrary of size 2. 
  - **[0]** - Variable (e.g. 5)
  - **[1]** - Pointer (that update after a new value is added)
    - When no value is added this contains 0x0 (Zero Address)
  - Pointer is also called MetaData
- **General Syntax**: To define a Node
  ```c
  typedef struct node
  {
    int number;
    struct node *next;
  } node;
  ```

- Beginning to create a linked list:
  ```c
  node *list = NULL;
  ```
- Allocate memory
  ```c
  node *n = malloc(sizeof(node))
  ```
- Add a number:
  ```c
  n -> number = 1;
  ```
- Add the corresponding pointer: Removing Garbarge number
  ```c
  n -> next = NULL;
  ```
- Change the tmp pointer to the list
  ```c
  list = n; 
  ```
- Second number: Allocate new memory using the tmp variable (pointer)
  ```c
  node *n = malloc(sizeof(node))
  ```
- Add a number:
  ```c
  n -> number = 2;
  ```
- Add the corresponding pointer: Removing Garbarge number
  ```c
  n -> next = NULL;
  ```
- Let the new item point towards the previously created one.
  ```c
  n -> next = list;
  ```
- Update the list to tmp (n)
  ```c
  list = n
  ```

```c
list(pointer) ->  [(2, pointer)] -> [(1, pointer)]
```
- If a third node is added it will be at the front:
```c
list(pointer) -> [(3, pointer)] -> [(2, pointer)] -> [(1, pointer)]
```

### Code Example: Insertion at the front
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
} node;

int main(int argc, char *argv[])
{
    node *list = NULL;

    for (int i=0; i < argc; i++)
    {
        int number = atoi(argv[i]);

        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            // free momory
            return 1;
        }
        n->number = number;
        n->next = NULL;

        n->next = list;
        list = n;
    }

    // print whole list
    node *ptr = list;
    while (ptr != NULL)
    {
        printf("%i\n", ptr->number);
        ptr = ptr->next;
    }
}
```

- **Linked lists time complexity**:
  - Insertion at front - $O(1)$
  - Insertion at back - $O(n)$
  - Search - $O(n)$


## 4. Trees
- 2D - Linked Lists

### Binary search Tree
- A sorted tree
```
            4

      2           6

    1   3       5   7
```
- Here every left node is smaller than its root
  - 1 < 2 < 4
  - 5 < 6
- Every right node is bigger than its root
  - 3 > 2
  - 7 > 6 > 4

- The typestruct for such a tree is as follows: 
  ```c
  typestruct node
  {
    int number;
    struct node *left;
    struct node *right;
  }
  ```

#### Code Example:
- A search function for a binary tree:
  - It functions recursively (calling search() inside itself)
  ```c
  bool search(node *tree, int number)
  {
    if (tree == NULL)
    {
      return false;
    }
    else if (number < tree->number)
    {
      return search(tree->left, number)
    }
    else if (number > tree->number)
    {
      return search(tree->right, number)
    }
    else
    {
      return true
    }
  }
  ```
## 5. Dictionaries (abstract datatype)
- A datastructure that stores **keys** and **values**!

### 5.1 Hasing 
- Some number of input and map it to a finite number of outputs.
  - e.g. sorting deck of cards -> mapping to 4 outputs
    -  Heart; Spade; Diamond; Clubs


### 5.2 Hash table
- **An Array of Linked Lists**
- Is a combination of Linked Lists and Arrays
- Example: Phonebook
  - **Column** of 0 - 25 (A - Z) -> Array, works in constant time
  - **Rows**: Linked lists, containing a person. If 2 persons start with the same letter, e.g. luigi, link we combine them via pointers.

  ```c
  #include <ctype.h>

  unsigned int hash(const char *word)
  {
      return toupper(word[0]) - 'A';
  }
  ```
  - **unsigned int** - positive number
  - **const char *word** - so noone can change this 

## 6. Tries
- **A Tree of Arrays**
- Massive negative is the huge amount of space unsigned
- But the time complexity is $O(1)$ for searching and adding and deleting.