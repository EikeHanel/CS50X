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
### 4.1 Selection Sort

- Move through the list find the lowest number and swap it with the first (index[0])
- start at index[1] and repeat