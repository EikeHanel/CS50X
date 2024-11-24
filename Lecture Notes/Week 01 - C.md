# C
- **Notes:** https://cs50.harvard.edu/x/2024/notes/1/

## 01. Machine Code
```c
#include <stdio.h>

int main(void) 
{
    printf("Hello, World!\n");
}
```
- Source code:
  - Is the code we wirte.
- Machine code:
  - Is basically just binary
  - The source code is converted via a program to machine code.

- **Source Code** $\rightarrow$ **Compiler** $\rightarrow$ **Machine Code**

- Manual pages
  - for libraries
  - https://manual.cs50.io/

## 2. Code
- **Terminal**: 
  - **code hello.c** - to create the hello.c file
  - **make hello** - creates the machine code
  - **./hello** - runs the machine code

- **Comment**:
  - // text
```c
#include <stdio.h>
#include <cs50.h>

int main(void)
{
    string answer = get_string("What's your name? ");
    printf("hello, %s\n", answer);
}
```
### 2.1 Types
- bool - True / False
- char - Single character
- double - 64bit float
- float - Decimal number e.g. 2.2
- int - Integer
- long - 64bit integer !
- string - String of characters
- ...

### 2.2 Format codes
- %c - Single Character
- %f - Float
- %i - Integers
- %li - Long Integer
- %s - Strings

### 2.3 Conditions
- **One condition**
    ```c
    if (x < y)
    {
        printf("x is less than y\n");
    }
    ```

- **Two condition**
    ```c
    if (x < y)
    {
        printf("x is less than y\n");
    }
    else
    {
        printf("x is not less than y\n");
    }
    ```

- **Three condition**
    ```c
    if (x < y)
    {
        printf("x is less than y\n");
    }
    else if (x > y)
    {
        printf("x is greater than y\n");
    }
    else if (x == y)
    {
        printf("x is equal to y\n");
    }
    ```
    - Last else if is "useless"
        ```c
        if (x < y)
        {
            printf("x is less than y\n");
        }
        else if (x > y)
        {
            printf("x is greater than y\n");
        }
        else
        {
            printf("x is equal to y\n");
        }
        ```

### 2.4 Variables
- Variables need a type definition
    ```c
    int counter = 0;
    ```

- Incrementing the counter
    ```c
    counter = counter + 1;

    counter += 1;

    counter++;

    counter--;
    ```

### 2.5 Loops
- **while** loop, the () contain a boolean expression
    ```c
    int counter = 3;
    while (counter > 0)
    {
        printf("meow\n");
        counter = counter - 1;
    }

    int i = 3;
    while (i > 0)
    {
        printf("meow\n");
        i--;
    }
    ```
- **for** loop, **(a; b; c)** 
  - **a** defines initial variable; **b** boolean expression; **c** update variable
  ```c
  for (int i = 0; i < 3; i++)
  {
    printf("meow\n");
  }
  ```

### 2.6 Functions

```c
void meow(void)
{
    printf("meow\n");
}
```
- Using this function in a for loop:
  ```c
  int main(void)
  {
    for (int i = 0; i < 3; i++)
    {
        meow();
    }
  }
  ```
- In C the funtion need to be decleared first, but always putting the whole function at the top is also not usefull, as the main part is pushed further and further down.
  - So to avoid this use the following sytax:
    ```c
    # include <stdio.h>

    void meow(int n);

    int main(void)
    {
        meow(3); 
    }

    void meow(int n)
    {
        for (int i = 0; i < n; i++)
        {
            printf("meow\n");
        } 
    }
    ```

- Simple Calculator
  - The add function gives a return value
    ```c
    #include <stdio.h>
    #include <cs50.h>
    int add(int a, int b);
    int main(void)
    {
        int x = get_int("x: ");
        int y = get_int("y: ");

        printf("%i\n", add(x, y));
    }

    int add(int a, int b)
    {
        return (a + b);
    }
    ```

### 2.7 Terminal commands

- **cd** (Change Directory)  
  Changes the current working directory to a specified directory.  
  Example: `cd /home/user/documents`

- **cp** (Copy)  
  Copies files or directories from one location to another.  
  Example: `cp file.txt /path/to/destination/`

- **ls** (List)  
  Lists the contents of a directory.  
  Example: `ls` (lists files in the current directory)

- **mkdir** (Make Directory)  
  Creates a new directory.  
  Example: `mkdir new_folder`

- **mv** (Move)  
  Moves or renames files or directories.  
  Example: `mv oldname.txt newname.txt`

- **rm** (Remove)  
  Deletes files or directories (use with caution).  
  Example: `rm file.txt`

- **rmdir** (Remove Directory)  
  Removes an empty directory.  
  Example: `rmdir empty_folder`


### 2.8 Constants
- Syntax
    ```c
    const int n = 5;
    ```

### 2.9 integer overflow
- it happens when the memory used to store the data does not have enough bits!
  - 32Bit: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
    - 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 
      - This is 4,294,967,295 if you only want positive numbers!
      - -2,147,483,648 to 2,147,483,648
  - If you want to count higher you would need 33Bit

### 2.10 Truncation
- integer / integer = integer !
    ```c
    {
        int x = 1
        int y = 3
        float z = x / y
        printf("%f\n", z)
    }
    ```
    - Returns 0.00000

### 2.11 Type casting
- Using (float) will change the type of the integer into a float
    ```c
    {
        int x = 1
        int y = 3
        float z = (float) x / (float) y
        printf("%f\n", z)
    }
    ```

### 2.12 Special formating for printf
- 
```c
{
    int x = 1
    int y = 3
    float z = (float) x / (float) y

    printf("%.2f\n", z)

    printf("%.5f\n", z)
}
```

- **First printf** returns: 
  - 0.33
- **Second printf** returns:
  - 0.33333

Remember, the computer has limited memory, if e.g. %.20f 
is used the computer will show the most accurate rounded number with the available memory possible.
- This is called **floating-point imprecision**