# Memory
- **Notes**: https://cs50.harvard.edu/x/2024/notes/4/

- Pixel are bytes of information
- RGB is defined by the Hex system
  - 0x 00 00 00 = Black
  - 0x FF FF FF = White
  - 0x shows that the following numbers are in the hex system.

## 1. Memory
- `int n = 50;`
  - Creates a varaible of 4 bytes called n with the information of 50
- In C, there are some more operators to poke around the memory.
  - `&` - Adress of operator
  - `*` - De-Reference operator
    ```c
    #include <stdio.h>

    int main(void)
    {
        int n = 50;
        printf("%p\n", &n);
    }
    ```
  - %p is the Format code for displaying an address
  - &n is the address of n

### 1.1 Pointer
- A pointer is just an address, which can be stored in another variable if needed. 
  - Thus, `%p`
  - A variable which is to store a pointer is defined by:
    - `int *p = &n;`
    ```c
    #include <stdio.h>

    int main(void)
    {
        int n = 50;
        int *p = &n;
        printf("%p\n", p);
    }
    ```
- Now, what if i want to read a specified memory address? 

    ```c
    #include <stdio.h>

    int main(void)
    {
        int n = 50;
        int *p = &n;
        printf("%i\n", *p);
    }
    ```
    - Here:
      - `int *p = &n;` is used to declare a pointer that will store an address.
      - `printf("%i\n", *p);` using the * without a type (like int) it is used to go to that address, i.e. Go There
      - slightly different meanings

---

- What is a string?
  - It is a pointer towards the chars in memory
  - **Assume**:
  -  `string s = "HI!` -> get stored as:
     -  **0x 123**: H
     -  **0x 124**: I
     -  **0x 125**: !
     -  **0X 126**: \0
     - now `s` points towards 0x 123
       - While the end of the string is given by \0
    ```c
    #include <stdio.h>

    int main(void)
    {
        string s = "HI!";
        printf("%p\n", s);
    }
    ```
   - This example returned: 0x59513b91f004
- Knowing this: 
  - `string s = "HI!` is actually
  - `char *s = "HI!"`

### 1.2 Pointer Arithmetic
- Doing math on addresses!
  - like add 1, add 2 etc.
  - A simple example for pointer arithmetic
    ```c
    #include <stdio.h>

    int main(void)
    {
        char *s = "HI!";
        printf("%c", *s);
        printf("%c", *(s + 1));
        printf("%c\n", *(s + 2));
    }
    ```

## 2. String Copy
- By using the following code:
  ```c
  #include <cs50.h>
  #include <ctype.h>
  #include <stdio.h>
  #include <string.h>

  int main(void)
  {
      string s = get_string("s: ");

      string t = s;

      t[0] = toupper(t[0]);
      printf("%s\n", s);
      printf("%s\n", t);
  }
  ```
- The change for `toupper(t[0])` happens for the address which is stored in the variable.
  - Thus, both printf functions print the same word, e.g. 
  - input hello -
    - First print = Hello
    - Second print = Hello
  ```c
  int main(void)
  {
      char *s = get_string("s: ");

      char *t = s;
  }
  ```
- The `string s` is basically `char *s`
  - Strings are just addresses
  
---

- To actually copy a string into a new memory allocated position the following code is needed.
  ```c
  #include <cs50.h>
  #include <ctype.h>
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>

  int main(void)
  {
      char *s = get_string("s: ");

      char *t = malloc(strlen(s) + 1);

      for (int i = 0, n = strlen(s); i <= n;  i++)
      {
          t[i] = s[i];
      }

      if (strlen(t) > 0)
      {
          t[0] = toupper(t[0]);
      }

      printf("%s\n", s);
      printf("%s\n", t);
  }
  ```
  - Here the function **malloc** from the library **stdlib.h** is used.
  - malloc takes one argument, the number of bytes for the new variable. and returns the address to that allocated memory.
    - Then through a loop we assign the charaters of the string to the new memory address + the last character `\0` (with i <= n), which indicates that the end of the string.
- Final code to copy memory, as the loop can be replaced with a function, **strcpy**
- Additionally if you manually allocate memory via malloc, you also need to free it after usage, otherwise momory bloat/overload can happen.
  ```c
  #include <cs50.h>
  #include <ctype.h>
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>

  int main(void)
  {
      char *s = get_string("s: ");
      if (s == NULL)
      {
          return 1;
      }

      char *t = malloc(strlen(s) + 1);
      if (t == NULL)
      {
          return 1;
      }

      strcpy(t, s)

      if (strlen(t) > 0)
      {
          t[0] = toupper(t[0]);
      }

      printf("%s\n", s);
      printf("%s\n", t);

      free(t)
      return 0;
  }
  ```

## 3. Valgrind
- A tool to check usage of memory.
- Example usage:
  ```c
  #include <stdio.h>
  #include <stdlib.h>

  int main(void)
  {
      // Buggy code
      int *x = malloc(3 * sizeof(int));
      // Index starts at 1
      x[1] = 72;
      x[2] = 73;
      x[3] = 33;
      // Memory is not freed
  }
  ```

- Using valgrind ./memory.C returns:
  ```
  Week-04/ $ valgrind ./memory
  ==18639== Memcheck, a memory error detector
  ==18639== Copyright (C) 2002-2022, and GNU GPL'd, by Julian Seward et al.
  ==18639== Using Valgrind-3.22.0 and LibVEX; rerun with -h for copyright info
  ==18639== Command: ./memory
  ==18639== 
  ==18639== Invalid write of size 4
  ==18639==    at 0x109170: main (memory.c:11)
  ==18639==  Address 0x4b9f04c is 0 bytes after a block of size 12 alloc'd
  ==18639==    at 0x4846828: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
  ==18639==    by 0x109151: main (memory.c:7)
  ==18639== 
  ==18639== 
  ==18639== HEAP SUMMARY:
  ==18639==     in use at exit: 12 bytes in 1 blocks
  ==18639==   total heap usage: 1 allocs, 0 frees, 12 bytes allocated
  ==18639== 
  ==18639== 12 bytes in 1 blocks are definitely lost in loss record 1 of 1
  ==18639==    at 0x4846828: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
  ==18639==    by 0x109151: main (memory.c:7)
  ==18639== 
  ==18639== LEAK SUMMARY:
  ==18639==    definitely lost: 12 bytes in 1 blocks
  ==18639==    indirectly lost: 0 bytes in 0 blocks
  ==18639==      possibly lost: 0 bytes in 0 blocks
  ==18639==    still reachable: 0 bytes in 0 blocks
  ==18639==         suppressed: 0 bytes in 0 blocks
  ==18639== 
  ==18639== For lists of detected and suppressed errors, rerun with: -s
  ==18639== ERROR SUMMARY: 2 errors from 2 contexts (suppressed: 0 from 0)
  ```
- **Important messages:**
  ```
  ==18639== Invalid write of size 4
  ==18639==    at 0x109170: main (memory.c:11)
  ```
    - Shows that at line 11 there is a invalid write of size 4 (4bytes = most likely an int)
      - Looking at the code 
        ```c
        x[1] = 72;
        x[2] = 73;
        x[3] = 33;
        ```
      - We can see that the indicies are false.
  ```
  ==18639== 12 bytes in 1 blocks are definitely lost in loss record 1 of 1
  ==18639==    at 0x4846828: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
  ==18639==    by 0x109151: main (memory.c:7)
  ```
  - This shows that there is a **Memory Leak** in line 7
    - `int *x = malloc(3 * sizeof(int));`
    - So it shows the line where we called malloc, and as this leads to a memory leak, it must not have been freed.
  ```
  ==18639== LEAK SUMMARY:
  ==18639==    definitely lost: 12 bytes in 1 blocks
  ==18639==    indirectly lost: 0 bytes in 0 blocks
  ==18639==      possibly lost: 0 bytes in 0 blocks
  ==18639==    still reachable: 0 bytes in 0 blocks
  ==18639==         suppressed: 0 bytes in 0 blocks
  ```
  - Memory leak summary, i.e. what was lost

- **Fixed Code**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>

  int main(void)
  {
      int *x = malloc(3 * sizeof(int));
      x[0] = 72;
      x[1] = 73;
      x[2] = 33;
      free(x);
  }
  ```
- New valgrind ./memory.c
  ```
  Week-04/ $ valgrind ./memory
  ==24085== Memcheck, a memory error detector
  ==24085== Copyright (C) 2002-2022, and GNU GPL'd, by Julian Seward et al.
  ==24085== Using Valgrind-3.22.0 and LibVEX; rerun with -h for copyright info
  ==24085== Command: ./memory
  ==24085== 
  ==24085== 
  ==24085== HEAP SUMMARY:
  ==24085==     in use at exit: 0 bytes in 0 blocks
  ==24085==   total heap usage: 1 allocs, 1 frees, 12 bytes allocated
  ==24085== 
  ==24085== All heap blocks were freed -- no leaks are possible
  ==24085== 
  ==24085== For lists of detected and suppressed errors, rerun with: -s
  ==24085== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
  ```
  - Shows no leaks are possible - Code is ok regarding the memory!

## 4. Garbage values
- Values of variables that you did not proactively set yourself.
- **Example**:
  ```c
  # include <stdio.h>

  int main(void)
  {
      int scores[1024];
      for (int i = 0; i < 1024; i++)
      {
          printf("%i\n", scores[i]);
      }
  }

  ```
- Some of the return values:
  ```
  0
  1596434048
  28985
  -1092832672
  32765
  0
  28985
  1596431024
  28985
  -1092832680
  32765
  -1092832432
  32765
  ```
- We clearly didnt set these values so be careful of what you trust.

## 5. Swap
- When swapping two int in a function, the address and pointers are needed due to scope.
- Example code:
  ```c
  #include <stdio.h>

  void swap(int *a, int *b);

  int main(void)
  {
      int x = 1;
      int y = 2;

      printf("x is %i, y is %i\n", x, y);
      // Calling swap with the addresses
      swap(&x, &y);
      printf("x is %i, y is %i\n", x, y);
  }

  void swap(int *a, int *b)
  {
      // swapping the pointers
      int tmp = *a;
      *a = *b;
      *b = tmp;
  }
  ```

## 6. File I/O
- **Example**: open file -> write to it and save.
  - can be repeated!
  ```c
  #include <cs50.h>
  #include <stdio.h>
  #include <string.h>

  int main(void)
  {
      FILE *file = fopen("phonebook.csv", "a");
      if (file == NULL)
      {
          return 1;
      }

      char *name = get_string("Name: ");
      char *number = get_string("Number: ");

      fprintf(file, "%s,%s\n", name, number);

      fclose(file);
  }
  ```
- `FILE *file = fopen("phonebook.csv", "a");` 
  - opens the file("phonebook.csv") in append mode ("a")!
- `fprintf(file, "%s,%s\n", name, number);`
  - writes to the file
- `fclose(file);`
  - closes the file

- **Example**: Copy a file
  ```c
  #include <stdio.h>
  #include <stdint.h>

  typedef uint8_t BYTE;

  int main(int argc, char *argv[])
  {
      FILE *src = fopen(argv[1], "rb");
      FILE *dst = fopen(argv[2], "wb");

      BYTE b;

      while (fread(&b, sizeof(b), 1, src) != 0)
      {
          fwrite(&b, sizeof(b), 1, dst);
      }
  }
  ```