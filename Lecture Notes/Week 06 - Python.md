# Python
- **Notes:** https://cs50.harvard.edu/x/2024/notes/6/

- Python does not compile the code, it runs an **Interpreter** that runs the code from top left to bottom right

## 1. functions

```python
# from cs50 import get_string

# answer = get_string("What's your name? ")
answer = input("What's your name? ")
print("hello, " + answer)
print("hello,", answer)
print(f"hello, {answer}")
```
- All these give the same result.

## 2. variables
- Creating a variable
    ```python
    counter = 1
    counter = counter + 1
    counter += 1
    ```

## 3. types
- bool
- int
- float
- str
- range
- list
- tuple
- dict
- set

### Code example:
- Converting str into int
    ```py
    x = int(input("x: "))
    y = int(input("y: "))
    print(x + y)
    ```

## 4. conditionals

```py
if x < y:
    print("x is less than y") 
elif:
    print("x greater than y")
else:
    print("x is equal to y") 
```

```py
s = input("s: ")
t = input("t: ")

if s == t:
    print("same")
else:
    print("different")
```

```py
s = input("do you agree? ").lower()

if s in ["y", "yes"]:
    print("agreed")
elif s in ["n", "no"]:
    print("not agreed")
```

## 5. named parameters
- print()
  - end="\n" - default
    ```py
    before = input("before: ")
    print("after: ", end="")
    for c in before:
        print(c.upper(), end="")
    ```

## 6. def main()
```py
def main():
    meow(3)


def meow(n):
    for _ in range(n):
        print("meow")


main()
```

## 7. truncation
```py
x = 1
y = 3
z = y / x
print(z)
```

### 7.1 floating-point imprecision
```py
x = 1
y = 3
z = y / x
print(f"{z:.50f}")
```
- **f"{z:.50f}"** - this f string formats the number to have 50 numbers after the comma
- And the imprecision still exists!

### 7.2 integer overflow
- This does not exist in python

## 8. exceptions
```py
def get_int(prompt):
    while True:
        try:
            return int(input(promt))
        except ValueError:
            print("Not an integer")


def main():
    x = get_int("x: ")
    y = get_int("y: ")
    print(x + y)
```

## 9. Lists

```py
from cs50 import get_int

scores = []
for i in range(3):
    score = get_int("Score: ")
    scores.append(score)

average = sum(scores) / len(scores)
```

### 9.1 Lists for loop
- A for loop can have a else statement!
    ```py
    names = ["Carter", "David", "John"]
    name = input("name: ")

    for n in names:
        if name == n:
            print("Found")
            break
    else:
        print("Not Found")
    ```
- This code does not need a for loop!
    ```py
    names = ["Carter", "David", "John"]
    name = input("name: ")

    if name in names:
        print("Found")
    else:
        print("Not Found")
    ```

## 10. dict
```py
people = [
    {"name": "Carter", "number": "11111"},
    {"name": "David", "number": "22222"},
    {"name": "John", "number": "33333"},
]

name = input("Name: ")

for person in people:
    if person["name"] == name:
        number = person["number"]
        print(f"Found {number}")
        break
else:
    print("Not Found")
```

```py
people = {
    "Carter": "11111",
    "David": "22222",
    "John": "33333",
}
name = input("Name: ")

if name in people:
    print(f"Found {people[name]}")
else:
    print("Not Found")
```


## 11. sys - library
- Terminal Code: python greet.py
  - Returns `hello, world`
- Terminal Code: python greet.py Eike
  - Returns `hello, Eike`
    ```py
    from sys import argv

    if len(argv) == 2:
        print(f"hello, {argv[1]}")
    else:
        print("hello, world")
    ```
- Exit code:
    ```py
    import sys

    if len(sys.argv) != 2:
        print("Missing command-line argument")
        sys.exit()

    print(f"Hello, {sys.argv[1]}")
    sys.exit(0)
    ```