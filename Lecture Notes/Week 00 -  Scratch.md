# Week 0
- **Notes:** https://cs50.harvard.edu/x/2024/notes/0/

## 1.0 Number systems
### 1.1 Unary system
- Counting with your fingers is Unary.
- 5 fingers how high can you count?
- $1 \rightarrow 2 \rightarrow 3 \rightarrow 4 \rightarrow 5$

---
- By using a more efficient way to count we can 
- By using up and down of fingers, e.g. all down = 0, thumps up = 1, pointer up = 2, etc.

- We can create a system that can count from 0 - 31
  - All fingers up $\rightarrow$ 1 + 2 + 4 + 8 + 16  
- This system is using base 2.
  - $2^0 + 2^1 + 2^2 + 2^3 + 2^4 == 1 + 2 + 4 + 8 + 16$

$\rightarrow$ This is the binary system!

### 1.2 Binary
- **Off = 0**
- **On = 1**
- Its called binary digit or bit
- Example
    ```
    2 Base system
    2^3    2^2     2^1     2^0
    16     4       2       1
    ```
    ```
    0 0 0 = 0
    0 0 1 = 1
    0 1 0 = 2
    0 1 1 = 3
    1 0 0 = 4
    1 0 1 = 5
    1 1 0 = 6
    1 1 1 = 7
    ```


### 1.3 Base 10 system Decimal
    10^2    10^1    10^0
    100     10      1  

    1       2       3    = 123

### 1.4 Base 16 system Hex

    0 1 2 3 4 5 6 7 9 A B C D E F

### 1.5 ASCII 8Bit - Letters and Numbers in Binary
- Numbers start at
  - 0 = 48 $\rightarrow$ 0 0 1 1 0 0 0 0 
  - 9 = 57 $\rightarrow$ 0 0 1 1 1 0 0 1
- Uppper-case Letters start at:
  - A = 65 $\rightarrow$ 0 1 0 0 0 0 0 1
  - Z = 90 $\rightarrow$ 0 1 0 1 1 0 1 0
- Lower-case Letters start at:
  - a = 97 $\rightarrow$ 0 1 1 0 0 0 0 1
  - z = 122 $\rightarrow$ 0 1 1 1 1 0 1 0

### 1.6 Unicode (8 / 16 / 32 bit) - Supercode of ASCII 
- Unicode uses Base 16 - Hex system
- It is used to diplay every kind of characters like letters up to  emojies etc.

### 1.7 Representation
- Context matters.
- RGB 0-255 for Red Green and Yellow can display every color
- Images a combination of pixels that are defined by a RGB value
- Sound - 3 numbers
  - Tone A B C
  - Length / Duration
  - Loudness / Volume
- Film
  - Frames per second
  - Images per second
  
## 2.0 Algorithms
- Are to solve a problem
  - As long as it works its good!
    - But, afterwards you would wnat ot optimize it.
- Example looking for a person in a Phonebook 1000 pages
  - Version 1 $O(n)$:
    - Look page for page
    - Takes a maximum of 1000 actions
  - Verion 2 $O(n/2)$:
    - Look every 2nd page, if overshoot, turn one page back
    - Takes a maximum of 500 actionis
  - Version 3 $O(log n)$:
    - Flip to the middle is the name higher or lower in the alphabet, then trow the other part away.
    - Repeat until you found it.
    - Takes a maximum of roughly 10 actions! 
    - Way faster!!!
- We ultimatly want **working** and **efficient** code!

### 2.1 Pseudocode
1. **Pick up** phone book
2. **Open to** middle pf phone book
3. **Look at** page
4. *If* ***person is on page***
   1. **Call** person
5. *Else if* ***person is erlier in book***
   1. **Open to** middle of left half of book
   2. ##Go back to line 3##
6. *Else if* ***person later in book***
   1. **Open to** middle of right half of book
   2. ##Go back to line 3##
7. *Else* 
   1. **Quit**

- **Bold** - Functions
- *Cursive* - Conditionals
- ***Bold/Cursive*** - Boolean expressions
- ##encased## - Loop

