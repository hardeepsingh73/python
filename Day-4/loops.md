# Python Loops — A Comprehensive Guide

> Master Python's looping constructs: `for` loops, `while` loops, `range()`, loop control
> statements (`break`, `continue`, `pass`), nested loops, comprehensions, and common patterns —
> all with practical, executable examples.

---

## Table of Contents

1. [Why Loops?](#1-why-loops)
2. [The `for` Loop](#2-the-for-loop)
3. [The `while` Loop](#3-the-while-loop)
4. [The `range()` Function](#4-the-range-function)
5. [Loop Control Statements](#5-loop-control-statements)
6. [Nested Loops](#6-nested-loops)
7. [Looping Over Collections](#7-looping-over-collections)
8. [The `enumerate()` Function](#8-the-enumerate-function)
9. [The `zip()` Function](#9-the-zip-function)
10. [List Comprehensions](#10-list-comprehensions)
11. [Dictionary Comprehensions](#11-dictionary-comprehensions)
12. [Set Comprehensions](#12-set-comprehensions)
13. [Generator Expressions](#13-generator-expressions)
14. [The `else` Clause in Loops](#14-the-else-clause-in-loops)
15. [Common Loop Patterns](#15-common-loop-patterns)
16. [Infinite Loops](#16-infinite-loops)
17. [Performance Tips](#17-performance-tips)
18. [Common Mistakes](#18-common-mistakes)
19. [Key Takeaways](#19-key-takeaways)
20. [Practice Exercises](#20-practice-exercises)
21. [Mini Project: Number Guessing Game](#21-mini-project-number-guessing-game)

---

# 1. Why Loops?

Loops let you **repeat an action** without writing the same code over and over. Instead of:

```python
print("Hello")
print("Hello")
print("Hello")
```

write:

```python
for i in range(3):
    print("Hello")
```

**Output:**
```
Hello
Hello
Hello
```

Loops are one of the most fundamental building blocks in programming. They let you:
- Process collections of data
- Repeat tasks a specific number of times
- Search for items
- Accumulate results
- And much more

---

# 2. The `for` Loop

The `for` loop iterates over each item in a **sequence** (string, list, tuple, dictionary, set, or any iterable).

## 2.1 Basic syntax

```python
for item in iterable:
    # code to execute for each item
```

## 2.2 Iterating over a string

```python
for letter in "Python":
    print(letter)
```

**Output:**
```
P
y
t
h
o
n
```

## 2.3 Iterating over a list

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

**Output:**
```
apple
banana
cherry
```

## 2.4 Iterating over a tuple

```python
colors = ("red", "green", "blue")

for color in colors:
    print(color)
```

**Output:**
```
red
green
blue
```

## 2.5 Iterating over a set

```python
numbers = {1, 2, 3, 4, 5}

for num in numbers:
    print(num)
```

**Output:**
```
1
2
3
4
5
```

## 2.6 Iterating over a dictionary

```python
person = {"name": "Alice", "age": 25, "city": "New York"}

# Iterating over keys (default)
for key in person:
    print(key)

# Iterating over values
for value in person.values():
    print(value)

# Iterating over key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```

**Output:**
```
name
age
city
Alice
25
New York
name: Alice
age: 25
city: New York
```

## 2.7 Using a temporary variable

The variable name after `for` is up to you — use a meaningful name:

```python
students = ["Alice", "Bob", "Charlie"]

for student in students:
    print(f"Hello, {student}!")
```

**Output:**
```
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

---

# 3. The `while` Loop

The `while` loop runs **as long as** a condition is `True`.

## 3.1 Basic syntax

```python
while condition:
    # code to execute
    # IMPORTANT: something must change the condition!
```

## 3.2 Simple counter

```python
count = 0

while count < 5:
    print("Count:", count)
    count += 1
```

**Output:**
```
Count: 0
Count: 1
Count: 2
Count: 3
Count: 4
```

## 3.3 User input loop

```python
password = ""

while password != "secret":
    password = input("Enter password: ")

print("Access granted!")
```

**Output (interactive):**
```
Enter password: wrong
Enter password: try again
Enter password: secret
Access granted!
```

## 3.4 When to use `while` vs `for`

| Use `for` when... | Use `while` when... |
|---|---|
| You know how many times to iterate | You don't know when to stop |
| You're iterating over a collection | The condition depends on user input |
| You want to process each item | You need to wait for a condition |

---

# 4. The `range()` Function

`range()` generates a sequence of numbers — perfect for `for` loops.

## 4.1 `range(stop)` — starts at 0

```python
for i in range(5):
    print(i)
```

**Output:**
```
0
1
2
3
4
```

## 4.2 `range(start, stop)` — custom start

```python
for i in range(2, 7):
    print(i)
```

**Output:**
```
2
3
4
5
6
```

## 4.3 `range(start, stop, step)` — custom step

```python
for i in range(0, 10, 2):
    print(i)
```

**Output:**
```
0
2
4
6
8
```

## 4.4 Counting backwards (negative step)

```python
for i in range(10, 0, -2):
    print(i)
```

**Output:**
```
10
8
6
4
2
```

## 4.5 Converting `range` to a list

```python
print(list(range(5)))         # [0, 1, 2, 3, 4]
print(list(range(2, 7)))      # [2, 3, 4, 5, 6]
print(list(range(0, 10, 3)))  # [0, 3, 6, 9]
```

**Output:**
```
[0, 1, 2, 3, 4]
[2, 3, 4, 5, 6]
[0, 3, 6, 9]
```

## 4.6 `len()` with `range` — index-based looping

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(f"Index {i}: {fruits[i]}")
```

**Output:**
```
Index 0: apple
Index 1: banana
Index 2: cherry
```

> **Tip:** Prefer `enumerate()` over `range(len(...))` — see Section 8.

---

# 5. Loop Control Statements

## 5.1 `break` — exit the loop immediately

```python
for n in range(1, 100):
    if n == 5:
        break
    print(n)
```

**Output:**
```
1
2
3
4
```

## 5.2 `continue` — skip to the next iteration

```python
for n in range(1, 8):
    if n % 2 == 0:
        continue
    print(n)
```

**Output:**
```
1
3
5
7
```

## 5.3 `pass` — placeholder (do nothing)

```python
for n in range(5):
    pass  # TODO: implement later

def empty_function():
    pass
```

`pass` keeps the code syntactically valid while you develop.

## 5.4 Combined example

```python
for n in range(1, 11):
    if n == 3:
        continue   # skip 3
    if n == 7:
        break      # stop at 7
    print(n)
```

**Output:**
```
1
2
4
5
6
```

---

# 6. Nested Loops

A loop inside a loop. The **inner loop** runs completely for each step of the **outer loop**.

## 6.1 Basic nested loop

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i * j}")
    print("---")  # separator after each inner loop
```

**Output:**
```
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
---
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
---
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
---
```

## 6.2 Printing a pattern

```python
rows = 5

for i in range(1, rows + 1):
    for j in range(i):
        print("*", end="")
    print()
```

**Output:**
```
*
**
***
****
*****
```

## 6.3 Iterating over a 2D list (matrix)

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]

for row in matrix:
    for value in row:
        print(value, end=" ")
    print()
```

**Output:**
```
1 2 3
4 5 6
7 8 9
```

## 6.4 Nested loops with `break`

`break` only exits the **innermost** loop:

```python
for i in range(3):
    for j in range(3):
        if j == 2:
            break  # breaks inner loop only
        print(f"({i},{j})", end=" ")
    print()
```

**Output:**
```
(0,0) (0,1) 
(1,0) (1,1) 
(2,0) (2,1) 
```

---

# 7. Looping Over Collections

## 7.1 Strings

```python
for ch in "Hello":
    print(ch, end=" ")
```

**Output:**
```
H e l l o 
```

## 7.2 Lists

```python
numbers = [10, 20, 30]

for num in numbers:
    print(num * 2)
```

**Output:**
```
20
40
60
```

## 7.3 Tuples

```python
point = (3, 7)

for coord in point:
    print(f"Coordinate: {coord}")
```

**Output:**
```
Coordinate: 3
Coordinate: 7
```

## 7.4 Dictionaries

```python
student = {"name": "Alice", "grade": "A", "age": 20}

for key, value in student.items():
    print(f"{key}: {value}")
```

**Output:**
```
name: Alice
grade: A
age: 20
```

## 7.5 Sets

```python
unique = {10, 20, 30}

for item in unique:
    print(item)
```

**Output:**
```
10
20
30
```

---

# 8. The `enumerate()` Function

`enumerate()` gives you both the **index** and the **value** in each iteration.

## 8.1 Basic usage

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

**Output:**
```
0: apple
1: banana
2: cherry
```

## 8.2 Custom start index

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")
```

**Output:**
```
1. apple
2. banana
3. cherry
```

## 8.3 Why `enumerate()` is better than `range(len())`

```python
# ❌ Less readable
fruits = ["apple", "banana", "cherry"]
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# ✅ More Pythonic
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")
```

---

# 9. The `zip()` Function

`zip()` combines multiple iterables into tuples, iterating them in parallel.

## 9.1 Basic usage

```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

**Output:**
```
Alice: 85
Bob: 92
Charlie: 78
```

## 9.2 Zipping three lists

```python
names = ["Alice", "Bob"]
ages = [25, 30]
cities = ["NYC", "LA"]

for name, age, city in zip(names, ages, cities):
    print(f"{name}, {age}, {city}")
```

**Output:**
```
Alice, 25, NYC
Bob, 30, LA
```

## 9.3 Creating a dictionary from two lists

```python
keys = ["name", "age", "city"]
values = ["Alice", 25, "NYC"]

person = dict(zip(keys, values))
print(person)
```

**Output:**
```
{'name': 'Alice', 'age': 25, 'city': 'NYC'}
```

---

# 10. List Comprehensions

A compact, Pythonic way to create lists from other iterables.

## 10.1 Basic syntax

```python
# [expression for item in iterable if condition]
```

## 10.2 Squares

```python
squares = [n ** 2 for n in range(6)]
print(squares)
```

**Output:**
```
[0, 1, 4, 9, 16, 25]
```

## 10.3 With a condition (filter)

```python
evens = [n for n in range(1, 11) if n % 2 == 0]
print(evens)
```

**Output:**
```
[2, 4, 6, 8, 10]
```

## 10.4 Transforming strings

```python
words = ["hello", "world"]
upper = [word.upper() for word in words]
print(upper)
```

**Output:**
```
['HELLO', 'WORLD']
```

## 10.5 Nested comprehension (flatten a matrix)

```python
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [n for row in matrix for n in row]
print(flat)
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
```

## 10.6 List comprehension vs regular loop

```python
# Regular loop
result = []
for n in range(10):
    if n % 2 == 0:
        result.append(n ** 2)

# List comprehension (same result, one line)
result = [n ** 2 for n in range(10) if n % 2 == 0]

print(result)
```

**Output:**
```
[0, 4, 16, 36, 64]
```

---

# 11. Dictionary Comprehensions

Build dictionaries in one line.

## 11.1 Basic syntax

```python
# {key_expr: value_expr for item in iterable if condition}
```

## 11.2 Squares mapping

```python
squares = {n: n ** 2 for n in range(5)}
print(squares)
```

**Output:**
```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## 11.3 With a condition

```python
students = {"Alice": 85, "Bob": 42, "Charlie": 91, "Diana": 55}

passed = {name: score for name, score in students.items() if score >= 60}
print(passed)
```

**Output:**
```
{'Alice': 85, 'Charlie': 91}
```

## 11.4 Inverting a dictionary

```python
original = {"a": 1, "b": 2, "c": 3}
inverted = {v: k for k, v in original.items()}
print(inverted)
```

**Output:**
```
{1: 'a', 2: 'b', 3: 'c'}
```

---

# 12. Set Comprehensions

Build sets in one line — automatically removes duplicates.

## 12.1 Basic syntax

```python
# {expression for item in iterable if condition}
```

## 12.2 Example

```python
sentence = "hello world"
unique_lengths = {len(word) for word in sentence.split()}
print(unique_lengths)
```

**Output:**
```
{5}
```

## 12.3 Even numbers as a set

```python
evens = {n for n in range(10) if n % 2 == 0}
print(evens)
```

**Output:**
```
{0, 2, 4, 6, 8}
```

---

# 13. Generator Expressions

Like list comprehensions, but **lazily evaluated** — they produce items one at a time instead of building a full list in memory.

## 13.1 Basic syntax

```python
# (expression for item in iterable if condition)
```

## 13.2 Example

```python
gen = (n ** 2 for n in range(5))

print(next(gen))  # 0
print(next(gen))  # 1
print(next(gen))  # 4

# Or iterate fully
for val in (n ** 2 for n in range(5)):
    print(val, end=" ")
```

**Output:**
```
0
1
4
0 1 4 9 16 
```

## 13.3 When to use generators

- Processing large datasets
- Chaining operations
- When you only need to iterate once

```python
# Sum without creating a list in memory
total = sum(n ** 2 for n in range(1_000_000))
print(total)
```

---

# 14. The `else` Clause in Loops

Python allows an `else` clause on `for` and `while` loops. It runs **only if the loop finishes normally** (without `break`).

## 14.1 `for...else`

```python
# Search for an odd number
numbers = [2, 4, 6, 8]

for n in numbers:
    if n % 2 != 0:
        print(f"Found odd: {n}")
        break
else:
    print("No odd numbers found")
```

**Output:**
```
No odd numbers found
```

## 14.2 Useful for search loops

```python
# Prime check
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

print(is_prime(7))   # True
print(is_prime(10))  # False
```

**Output:**
```
True
False
```

---

# 15. Common Loop Patterns

## 15.1 Accumulator pattern (sum)

```python
total = 0
for n in [10, 20, 30, 40]:
    total += n
print("Sum:", total)
```

**Output:**
```
Sum: 100
```

## 15.2 Counter pattern

```python
count = 0
for ch in "hello world":
    if ch == "l":
        count += 1
print("Count of 'l':", count)
```

**Output:**
```
Count of 'l': 3
```

## 15.3 Find min/max

```python
numbers = [34, 12, 89, 45, 67]

minimum = numbers[0]
maximum = numbers[0]

for n in numbers:
    if n < minimum:
        minimum = n
    if n > maximum:
        maximum = n

print(f"Min: {minimum}, Max: {maximum}")
```

**Output:**
```
Min: 12, Max: 89
```

## 15.4 Filtering into a new list

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
evens = []

for n in numbers:
    if n % 2 == 0:
        evens.append(n)

print(evens)
```

**Output:**
```
[2, 4, 6, 8]
```

## 15.5 Building a string

```python
result = ""
for i in range(1, 6):
    result += str(i) + " "
print(result.strip())
```

**Output:**
```
1 2 3 4 5
```

## 15.6 Enumerate for indexed access

```python
students = ["Alice", "Bob", "Charlie"]

for i, student in enumerate(students, 1):
    print(f"Student {i}: {student}")
```

**Output:**
```
Student 1: Alice
Student 2: Bob
Student 3: Charlie
```

## 15.7 Nested data processing

```python
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 42},
    {"name": "Charlie", "score": 91},
]

for student in students:
    status = "PASS" if student["score"] >= 60 else "FAIL"
    print(f"{student['name']}: {student['score']} ({status})")
```

**Output:**
```
Alice: 85 (PASS)
Bob: 42 (FAIL)
Charlie: 91 (PASS)
```

---

# 16. Infinite Loops

Sometimes you intentionally want a loop that runs forever — until a `break` exits it.

## 16.1 Using `while True`

```python
while True:
    user_input = input("Enter 'quit' to exit: ")
    if user_input == "quit":
        break
    print(f"You entered: {user_input}")
```

**Output (interactive):**
```
Enter 'quit' to exit: hello
You entered: hello
Enter 'quit' to exit: quit
```

## 16.2 Server-like loop

```python
import time

print("Server started. Press Ctrl+C to stop.")

while True:
    print("Heartbeat...")
    time.sleep(2)
```

## 16.3 Menu-driven program

```python
while True:
    print("\n1. Add  2. View  3. Exit")
    choice = input("Choose: ")

    if choice == "1":
        print("Adding...")
    elif choice == "2":
        print("Viewing...")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice")
```

---

# 17. Performance Tips

## 17.1 Prefer comprehensions over manual loops

```python
# ❌ Slower
result = []
for n in range(1000):
    result.append(n ** 2)

# ✅ Faster (optimized internally)
result = [n ** 2 for n in range(1000)]
```

## 17.2 Use generators for large data

```python
# ❌ Creates a huge list in memory
squares = [n ** 2 for n in range(10_000_000)]

# ✅ Yields one at a time
squares = (n ** 2 for n in range(10_000_000))
```

## 17.3 Avoid repeated work inside loops

```python
# ❌ Recalculating length every iteration
for i in range(len(my_list)):
    pass

# ✅ Store length once
length = len(my_list)
for i in range(length):
    pass
```

## 17.4 Use `enumerate()` instead of `range(len())`

```python
# ❌ Less readable
for i in range(len(my_list)):
    print(my_list[i])

# ✅ More Pythonic
for i, item in enumerate(my_list):
    print(item)
```

---

# 18. Common Mistakes

| Mistake | Problem | Fix |
|---|---|---|
| Infinite loop | Condition never becomes `False` | Ensure something changes the condition |
| Modifying a list while iterating | Skips or duplicates items | Iterate over a copy: `for item in list[:]` |
| `break` in nested loop | Only breaks inner loop | Use a flag or function |
| Using `=` instead of `==` in `while` | Syntax error or unexpected behavior | Use `==` for comparison |
| Forgetting `range()` stop is exclusive | Off-by-one errors | `range(5)` gives 0,1,2,3,4 |
| Using mutable default in comprehension | Shared references | Create new list explicitly |

## 18.1 Infinite loop example

```python
# ❌ BUG: n never changes!
n = 0
# while n < 5:
#     print(n)

# ✅ FIX: increment n
n = 0
while n < 5:
    print(n)
    n += 1
```

## 18.2 Modifying while iterating

```python
# ❌ May skip items
numbers = [1, 2, 3, 4, 5]
# for n in numbers:
#     if n % 2 == 0:
#         numbers.remove(n)  # modifies list during iteration!

# ✅ Iterate over a copy
numbers = [1, 2, 3, 4, 5]
for n in numbers[:]:
    if n % 2 == 0:
        numbers.remove(n)
print(numbers)
```

**Output:**
```
[1, 3, 5]
```

---

# 19. Key Takeaways

- `for` loops iterate over sequences; `while` loops run until a condition is `False`. ✔
- `range(start, stop, step)` generates number sequences for `for` loops. ✔
- `break` exits the loop; `continue` skips to the next iteration; `pass` does nothing. ✔
- Nested loops run the inner loop completely for each step of the outer loop. ✔
- `enumerate()` gives index + value; `zip()` combines multiple iterables. ✔
- List comprehensions (`[expr for x in iter]`) are concise and fast. ✔
- Dictionary and set comprehensions follow the same pattern. ✔
- Generator expressions `(expr for x in iter)` are memory-efficient. ✔
- `for...else` runs the `else` block only if no `break` occurred. ✔
- Always ensure `while` loops have a way to terminate. ✔

---

# 20. Practice Exercises

### Basic

1. Print numbers 1 to 20 using a `for` loop.
2. Print all even numbers from 1 to 50 using `range()`.
3. Print the multiplication table for a user-entered number.
4. Calculate the sum of all numbers from 1 to 100 using a loop.

### Intermediate

5. Find the factorial of a number using a `while` loop.
6. Check if a number is prime.
7. Reverse a string using a loop.
8. Count the number of vowels in a string.
9. Print the Fibonacci sequence up to n terms.

### Advanced

10. Use a list comprehension to generate all Pythagorean triples where a, b, c ≤ 30.
11. Flatten a nested list of arbitrary depth.
12. Write a function that returns all prime numbers up to n using the Sieve of Eratosthenes.
13. Create a simple calculator that runs in a loop until the user chooses to quit.
14. Use `zip()` to merge two lists into a dictionary, handling unequal lengths with `itertools.zip_longest`.

---

# 21. Mini Project: Number Guessing Game

A fun project that uses loops, conditionals, and user input:

```python
import random

def play_game():
    secret = random.randint(1, 100)
    attempts = 0
    max_attempts = 7

    print("I'm thinking of a number between 1 and 100.")
    print(f"You have {max_attempts} attempts.\n")

    while attempts < max_attempts:
        guess = int(input(f"Attempt {attempts + 1}/{max_attempts} — Your guess: "))
        attempts += 1

        if guess == secret:
            print(f"Congratulations! You got it in {attempts} attempts!")
            return True
        elif guess < secret:
            print("Too low!")
        else:
            print("Too high!")

    print(f"\nGame over! The number was {secret}.")
    return False

# Main loop
while True:
    play_game()
    again = input("\nPlay again? (yes/no): ").lower()
    if again != "yes":
        print("Thanks for playing!")
        break
```

**Sample run:**
```
I'm thinking of a number between 1 and 100.
You have 7 attempts.

Attempt 1/7 — Your guess: 50
Too low!
Attempt 2/7 — Your guess: 75
Too high!
Attempt 3/7 — Your guess: 62
Too low!
Attempt 4/7 — Your guess: 68
Congratulations! You got it in 4 attempts!
```

---

*Loops are everywhere in programming. The more you practice, the more natural they become.
Try writing small programs that use loops to solve real problems — that's the best way to learn.
Happy coding!*