# Algorithms
- **Notes:** https://cs50.harvard.edu/x/2024/notes/3/

## 1. divide-and-conquer
- https://www.geeksforgeeks.org/divide-and-conquer/
---
- **Divide**: Break the given problem into smaller non-overlapping problems.
- **Conquer**: Solve Smaller Problems
- **Combine**: Use the Solutions of Smaller Problems to find the overall result.

### 1.1 Linear Search
- $O(n)$
- is basically the only way to search an unsorted list
- **Pseudocode**:
  - For i from 0 to n-1
    - If 50 is behind door[i]
      - Return true
  - Return false
    ```c
    #include <cs50.h>
    #include <stdio.h>

    int main(void)
    {
        int numbers[] = {20, 500, 10, 5, 100, 1, 50};

        int n = get_int("Number: ");
        for (int i = 0; i < 7; i++)
        {
            if (numbers[i] == n)
            {
                printf("Found\n");
                return 0;
            }
        }
        printf("Not Found\n");
        return 1;
    }       
    ```
### 1.2 Binary Search
- $O(log(n))$
- **Pseudocode**:
  - If no doors left
    - Return false
  - If 50 is behind doors[middle]
    - Return true
  - Else if 50 < doors[middle]
    - Search doors[0] through doors[middle - 1]
  - Else if 50 > door[middle]
    - Search doors[middle + 1] through doors[n - 1]

## 2. Running time
- When n is large enough constants do not matter
  - Thus, constants are removed for describing the runtime
---
- $O$ - Represents upper bound, i.e. worst case
- $O(n^2)$
- $O(nlogn)$
- $O(n)$
- $O(logn)$
- $O(1)$
  
<br>

- $\Omega$ - Represents the best case
- $\Omega(n^2)$
- $\Omega(nlogn)$
- $\Omega(n)$
- $\Omega(logn)$
- $\Omega(1)$

<br>

- $\Theta$ - Represents average case


## 3. Struct
- Creating "new" data structures
  ```c
  typedef struct
  {
    string name;
    string number
  }
  person;
  ```
- Filling this new datatype
  ```c
  person people[3];
    people[0].name = "Carter";
    people[0].number = "+1-617-495-1000";
    people[1].name = "David";
    people[1].number = "+1-617-495-1000";
    people[2].name = "John";
    people[2].number = "+1-949-468-2750";
  ```

## 4. Sorting
- Os a balance between space usage and time spend
  - low time spend -> high memory usage
  - low memory usage -> high time spend

### 4.1 Selection Sort

- Move through the list find the lowest number and swap it with the first (index[0])
- start at index[1] and repeat
- **Pseudocode**:
  - For i from 0 to n-1
    - Find smalles number between numbers[i] and numbers[n-1]
    - Swap smallest number with numbers[i]
- On the order of - $O(n^2)$ and $\Omega(n^2)$ and $\Theta(n^2)$

### 4.2 Bubble Sort
- Sorting by comparing numbers next to each other.
- bringing the biggest number to the last spot
- **Pseudocode**:
  - For i form 0 n-2
    - If numbers[i] and numbers[i+1] out of order
      - Swap them
    - If no swaps 
      - Quit
- On the order of - $O(n^2)$ and $\Omega(n)$ and $\Theta(n^2)$

### 4.3 Recursion
- A function that calls itself

- **Example crating a pyramid**:
  - Through double for loop **not recursively**
    ```c
    #include <cs50.h>
    #include <stdio.h>

    void draw(int n);
    int main(void)
    {
        int height = get_int("Height: ");
        draw(height);
    }

    void draw(int n)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < i + 1; j++)
            {
                printf("#");

            }
            printf("\n");
        }
    }
    ```
  - **Recursively**
    ```c
    #include <cs50.h>
    #include <stdio.h>

    void draw(int n);
    int main(void)
    {
        int height = get_int("Height: ");
        draw(height);
    }


    void draw(int n)
    {
        // If nothing to draw
        if (n <= 0)
        {
            return;
        }

        // Print pyramid of height n-1
        draw(n - 1);

        // Print one more row
        for (int i = 0; i < n; i++)
        {
            printf("#");
        }
        printf("\n");
    }
    ```
### 4.4 Merge Sort
- **Pseudocode**
  - If only one number Quit
    - Quit
  - Else
    - Sort left half of numbers
    - Sort right half of numbers
    - Merge sorted halves

```
                          6 | 3 | 4 | 1 | 5 | 2 | 7 | 0 

            6 | 3 | 4 | 1                               5 | 2 | 7 | 0

       6 | 3             4 | 1                    5 | 2               7 | 0

      6     3          4       1                5       2           7       0

       3 | 6             1 | 4                    2 | 5               0 | 7

            1 | 3 | 4 | 6                               0 | 2 | 5 | 7

                          0 | 1 | 2 | 3 | 4 | 5 | 6 | 7
```

- Time complexity is $O(nlogn)$ and $\Omega(nlogn)$ and $\Theta(nlogn)$