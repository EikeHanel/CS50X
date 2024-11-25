# Arrays
- **Notes:** https://cs50.harvard.edu/x/2024/notes/2/

## 1. Compiling
**make vs clang**
- make hello
  - is runnig an acual compiler in the background to change your code into machine code
- clang is a different command to compile your code.
  - the default output is a.out
  - to change the output name:
    - clang -o hello hello.c
  - But if a unknown library is used (like cs50.h) an additional command need to be added
    - clang -o hello hello.c -lcs50
- Thus, make is quite popular as it makes the command propmt simple and fast to write!

---

Overall compiling is a process with four steps:
- Preprocessing
  - Find and replace the `#include <...>` libraries with the code indside the libraries.
- Compiling
  - Changes the code into Assembly.
- Assembling
  - Takes the Assembly code and converts it into Machine Code.
- Linking
  - All the needed files are combined/linked, as Machine Code.
    - For the hello.c there are 3 files:
      - hello.c 
      - cs50.c      
      - stdio.c

### 1.1 Decompiling
- Reverse engineering is easier said than done!
  - As there are multiple ways to solve the same problem.
  - Also, you lose the variable names, function names etc.

## 2. Debugging
- Example of buggy code (i <= 3 should be i < 3)
    ```c
    #include <stdio.h>

    int main(void)
    {
        for (int i = 0; i <= 3; i++)
        {
            // printf("i is %i\n", i);
            printf("#\n");
        }
    }
    ```
    ```c
    #include <cs50.h>
    #include <stdio.h>

    void print_column(int height);
    int main(void)
    {
        int h = get_int("Height: ");
        print_column(h)
    }

    void print_column(int height)
    {
        for (int i = 0; i <= 3; i++)
        {
            printf("#\n");
        }
    }
    ```
- Tools to find bugs:
  - printf
    - to many are can be confusing!
  - Debugger
    - make buggy
    - debug50 ./buggy
      - Add breakpoints (click the row number -> Red circle)
      - Control buttons on the top!
  - Rubber Duck Debugging
    - Explaining the code to an inanimate object, verbally.


## 3. Memory
- **bool** - 1 byte <=> 2 bit
- **int** - 4 bytes <=> 32 bit
- **long** - 8 bytes <=> 64 bit
- **float** - 4 bytes
- **double** - 8 bytes
- **char** - 1 byte
- **string** - ? bytes
- ...

- Think of bit having an Address/Indicies
  - Where is it saved
  - Basically a Canvas, Pixels of bit positions


# 4. Array
- Is a chunck of memory
- Defining an array: Type name[max_number_of_items]
    ```c
    int scores[3];
    ```
- Adding items to the array:
    ```c
    int scores[3];
    scores[0] = 72;
    scores[1] = 73;
    scores[2] = 33;
    ```
---

- We alread now aray's you just didn't know.
  - A String = Array of Chars
  ```c
  #include <stdio.h>

  int main(void)
  {
      char c1 = 'H';
      char c2 = 'I';
      char c3 = '!';

      printf("%i %i %i\n", c1, c2, c3);
  }
  ```

  ```c
  #include <cs50.h>
  #include <stdio.h>

  int main(void)
  {
      string s = "HI!";

      printf("%s\n", s);
  }
  ```

  ```c
  #include <cs50.h>
  #include <stdio.h>

  int main(void)
  {
      string s = "HI!";

      printf("%i %i %i\n", s[0], s[1], s[2]);
  }
  ```
  - They are the same!
- How does the computer know when a sting ends - Memory wise!
  - The end is defined by a special character = 0 0 0 0 0 0 0 0 0 (8 Bit all 0)
  - Every String is n+1 byte, n = length + 1 due to the special character 
  - This special char is wirtten like `\0`
  
---
- There are nested lists.
  ```c
  #include <cs50.h>
  #include <stdio.h>

  int main(void)
  {
      string words[2];

      words[0] = "HI!";
      words[1] = "BYE!";

      printf("%s\n", words[0]);
      printf("%s\n", words[1]);
  }
  ```
  - To acces the individual charaters you can use: `words[0][0]`
    - First char of the first word.

---

- By knowing that a sting ends with `\0` you can create a function to calculate the length of a string.
  ```c
  #include <cs50.h>
  #include <stdio.h>

  int string_length(string s);
  int main(void)
  {
      string name = get_string("Name: ");
      int length = string_length(name);
      printf("%i\n", length);
  }

  int string_length(string s)
  {
      int n = 0;
      while (s[n] != '\0')
      {
          n++;
      }
      return n;
  }
  ```

- But by using string.h library you can make it easier by just calling `strlen()`
  ```c
  #include <cs50.h>
  #include <stdio.h>
  #include <string.h>

  int main(void)
  {
      string name = get_string("Name: ");
      int length = strlen(name);
      printf("%i\n", length);
  }
  ```

---

- Transform String to Uppercase
- Using Asci "indexes" 
  ```c
  #include <cs50.h>
  #include <stdio.h>
  #include <string.h>

  int main(void)
  {
      string s = get_string("Before: ");
      printf("After:  ");
      for (int i = 0; n = strlen(s); i < n; i++)
      {
        // If lowercase
        if (s[i] >= 'a' && s[i] <= 'z')
        {
          printf("%c", s[i] - 32);
        }
        else
        {
          printf("%c", s[i]);
        }
        printf("\n");
      }
  }
  ```
- ctype.h library makes this also easier.
  - Function name: `toupper()`

