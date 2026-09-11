# Python Part 1 — A Beginner's Guide to Python

> Learn Python from scratch: variables, data types, strings, conditionals, collections, loops,
> functions, recursion, file I/O, and Object-Oriented Programming — all with practical,
> executable examples.

---

## Table of Contents

1. [Variables and Data Types](#1-variables-and-data-types)
2. [Strings and Conditional Statements](#2-strings-and-conditional-statements)
3. [Lists and Tuples](#3-lists-and-tuples)
4. [Dictionaries and Sets](#4-dictionaries-and-sets)
5. [Loops](#5-loops)
6. [Functions and Recursion](#6-functions-and-recursion)
7. [File I/O](#7-file-io)
8. [OOPs / Object-Oriented Programming](#8-oops--object-oriented-programming)
9. [Python Part-1 Cheat Sheet](#9-python-part-1-cheat-sheet)
10. [Mixed Practice Questions](#10-mixed-practice-questions)
11. [Beginner Project: Student Database Manager](#11-beginner-project-student-database-manager)

---

# 1. Variables and Data Types

## 1.1 What are variables?

A **variable** is a name you give to a value stored in your computer's memory. Think of it
as a labelled box: the *label* is the variable name, and the *content* of the box is the value.

```python
age = 25          # the variable "age" now holds the value 25
name = "Alice"    # the variable "name" now holds the text "Alice"
print(age)
print(name)
```

**Output:**
```
25
Alice
```

## 1.2 Variable naming rules and conventions

**Rules (Python will give an error if you break these):**
- Names must start with a letter or underscore (`_`), **not** a number.
- The rest of the name can contain letters, digits, and underscores.
- Names are case-sensitive: `Age`, `age`, and `AGE` are three different variables.
- You cannot use Python *keywords* (reserved words) as names, such as `if`, `for`, `while`, `class`, `def`, `import`.

**Conventions (best practices):**
- Use `snake_case` for variable and function names: `first_name`, `total_price`.
- Use `UPPER_SNAKE_CASE` for constants: `PI = 3.14159`.
- Use meaningful names: `total_cost` is better than `t` or `x1`.

```python
# valid names
student_name = "Bob"
_score = 90
variable2 = "ok"

# invalid names (each would raise an error if uncommented)
# 2nd_var = 10      # starts with a digit
# my-name = "x"     # hyphen is not allowed
# if = 5            # "if" is a keyword

print(student_name, _score, variable2)
```

**Output:**
```
Bob 90 ok
```

## 1.3 Variable assignment

Assignment uses the single equals sign `=` — meaning *"store the value on the right into the
name on the left"*.

```python
x = 10
y = x + 5          # the value of x (10) is read, then 5 is added
print(x, y)

x = 99             # reassign: the box "x" now holds a new value
print(x, y)        # y is unchanged because it was computed earlier
```

**Output:**
```
10 15
99 15
```

## 1.4 Multiple variable assignment

You can assign several variables on one line:

```python
a, b, c = 1, 2, 3        # assigns in order
print(a, b, c)

x = y = z = 0            # all three get the same value
print(x, y, z)
```

**Output:**
```
1 2 3
0 0 0
```

## 1.5 Constants and conventions in Python

Python has **no built-in constant keyword** like `const`. Instead, programmers follow the
convention of naming constants in `UPPER_CASE`. Everything is still changeable — the naming
is a signal to other developers that the value shouldn't be changed.

```python
PI = 3.14159
GRAVITY = 9.8
MAX_ATTEMPTS = 5

print(PI, GRAVITY, MAX_ATTEMPTS)
```

**Output:**
```
3.14159 9.8 5
```

## 1.6 Dynamic typing

Python is **dynamically typed** — a variable can hold one type of value and later be
reassigned to a completely different type. The type belongs to the value, not the variable.

```python
thing = "hello"      # string
print(thing, type(thing))

thing = 7            # now the same variable holds an integer
print(thing, type(thing))
```

**Output:**
```
hello <class 'str'>
7 <class 'int'>
```

## 1.7 Basic data types

| Type      | Example        | Description                              |
|-----------|----------------|------------------------------------------|
| `int`     | `42`, `-7`     | Whole numbers                            |
| `float`   | `3.14`, `2.0`  | Decimal (floating point) numbers         |
| `complex` | `2 + 3j`       | Numbers with a real and imaginary part   |
| `bool`    | `True`, `False`| Logical true/false                       |
| `str`     | `"hi"`, `'ok'` | Text (a sequence of characters)          |
| `None`    | `None`         | Represents "no value" (absence of value) |

```python
price = 9.99                 # float
count = 3                    # int
z = 2 + 5j                   # complex
is_active = True             # bool
name = "Python"              # str
nothing = None               # NoneType

print(price, count, z, is_active, name, nothing)
```

**Output:**
```
9.99 3 (2+5j) True Python None
```

## 1.8 The `type()` function

`type()` returns the type of any value or variable.

```python
print(type(42))
print(type(3.14))
print(type("text"))
print(type(True))
print(type(None))
```

**Output:**
```
<class 'int'>
<class 'float'>
<class 'str'>
<class 'bool'>
<class 'NoneType'>
```

## 1.9 Type conversion / type casting

You can convert a value from one type to another using the type names as functions.

```python
# string -> number
num = int("42")
print(num, type(num))

# number -> string
text = str(3.5)
print(text, type(text))

# float -> int (truncates/rounds toward zero, no rounding!)
print(int(7.9))      # -> 7  (decimal part is dropped)

# int -> float
print(float(10))     # -> 10.0

# anything -> bool
print(bool(0), bool(1), bool(-5))
print(bool(""), bool("hi"))
```

**Output:**
```
42 <class 'int'>
3.5 <class 'str'>
7
10.0
False True True
False True
```

**Common mistake:** converting text that isn't a valid number raises an error.

```python
# int("abc")   # ValueError: invalid literal for int() with base 10: 'abc'
# int("4.5")   # ValueError too: "Text is not iVal word"  -> actually: invalid literal
```

## 1.10 `isinstance()`

`isinstance(value, type_name)` returns `True` if a value is of the given type (or a subclass).

```python
print(isinstance(5, int))          # True
print(isinstance(5, float))        # False
print(isinstance("hi", str))       # True
print(isinstance(5, (int, float))) # True — checks against a tuple of types
```

**Output:**
```
True
False
True
True
```

## 1.11 Mutable vs immutable objects

- **Immutable**: the value cannot be changed after creation. When you "modify" it, Python
  actually creates a new object in the background. (`int`, `float`, `str`, `bool`, `tuple`)
- **Mutable**: the value *can* be changed in place. (`list`, `dict`, `set`)

```python
# Immutable example
s = "hello"
# s[0] = "H"      # ERROR: strings are immutable, cannot change a character

# Mutable example
lst = [1, 2, 3]
lst[0] = 99       # OK: lists can be modified in place
print(lst)
```

**Output:**
```
[99, 2, 3]
```

Python **ignores** this rule — this is real world data and even years of age data or you must
display boolean for impossible. **Always realign your answer to the ACTUAL PYTHON output.**

---

## 1.12 Common beginner mistakes

1. **Using `=` instead of `==`** — `=` assigns, `==` compares.
2. **Using a variable before assigning it** → `NameError`.
3. **Mixing types in operations** — `"5" + 5` raises `TypeError`. Convert first.
4. **Thinking division is clean** — `5 / 2` is `2.5`; use `//` for floor division, `%` for remainder.
5. **Forgetting that `=` reads right-to-left** — `a = b` copies the *value* of `b` into `a`.

```python
# Fixing mistake 3:
a = 5
b = "5"
print(a + int(b))        # converts string to int first
```

**Output:**
```
10
```

## 1.13 Key Takeaways

- Variables are named labels for values; Python names them with `snake_case`. ✔
- Python is dynamically typed — the *value* has a type, not the variable. ✔
- To change a type, cast with `int()`, `float()`, `str()`, `bool()`. ✔
- `int`, `float`, `str`, `bool`, `tuple` are immutable; `list`, `dict`, `set` are mutable. ✔
- Use `type()` to inspect and `isinstance()` to test types safely. ✔

## 1.14 Practice Exercises

1. Assign `10`, `3.5`, `"Python"`, and `False` to four variables and print each one with its `type()`.
2. Convert `"3.14"` to a float, then to an int. What value do you get and why?
3. Swap the values of two variables (`a` and `b`) using a third temporary variable. Then swap using `a, b = b, a`.
4. Create a constant-looking name for `GRAVITY = 9.8` and print it.
5. What is the output of `bool(" " )` (a string with one space)? Test it.

---

# 2. Strings and Conditional Statements

## 2.1 Creating strings

Strings store text. Use single, double, or triple quotes — all three work.

```python
single = 'Single quotes'
double = "Double quotes"
triple = """Triple
quotes allow
multiple lines"""

print(single)
print(double)
print(triple)
```

**Output:**
```
Single quotes
Double quotes
Triple
quotes allow
multiple lines
```

## 2.2 Single, double, and triple quotes

- Single and double quotes are interchangeable — pick one and stay consistent.
- Triple quotes are for multi-line text and for writing docstrings inside functions/classes.
- A string opened with one quote type can safely contain the other quote type.

```python
quote = 'He said, "Hello!"'
print(quote)

# triple quotes can also be used for a big block of text
paragraph = """This is line one.
This is line two."""
print(paragraph)
```

**Output:**
```
He said, "Hello!"
This is line one.
This is line two.
```

## 2.3 String indexing

Each character has an index. The first character is index `0`; negative indices count from
the end, starting at `-1`.

```python
word = "Python"
# indexes:  P y t h o n
#           0 1 2 3 4 5
#         -6-5-4-3-2-1

print(word[0])    # P
print(word[2])    # t
print(word[-1])   # n  (last character)
print(word[-2])   # o
```

**Output:**
```
P
t
n
o
```

## 2.4 String slicing

`string[start:stop:step]` — gets characters from `start` up to but **not including** `stop`.

```python
word = "Python"

print(word[0:2])      # Py   (indexes 0,1)
print(word[2:])       # thon (index 2 to end)
print(word[:2])       # Py   (from start to index 1)
print(word[:])        # copy of the whole string
print(word[::2])      # Pto  (every second character)
print(word[::-1])     # nohtyP (reversed string!)
```

**Output:**
```
Py
thon
Py
Python
Pto
nohtyP
```

## 2.5 String concatenation (`+`)

Joining strings with `+`.

```python
first = "Sponge"
second = "Bob"
full = first + " " + second
print(full)
```

**Output:**
```
Sponge Bob
```

## 2.6 String repetition (`*`)

Repeating a string with `*`.

```python
print("ha" * 3)
print("-" * 10)
```

**Output:**
```
hahaha
----------
```

## 2.7 Escape characters

A backslash `\` escapes a character so it does something special.

| Escape | Meaning                 |
|--------|-------------------------|
| `\n`   | Newline                 |
| `\t`   | Tab                     |
| `\'`   | Single quote            |
| `\"`   | Double quote            |
| `\\`   | Literal backslash       |

```python
print("Line1\nLine2")
print("Column1\tColumn2")
print("It\'s ok")
print('She said \"hi\"')
```

**Output:**
```
Line1
Line2
Column1 Column2
It's ok
She said "hi"
```

## 2.8 Common string methods

Methods are called with `string.method()`. They **return** new strings — they never modify
the original (strings are immutable).

```python
text = "  Python Programming  "

print(text.upper())               # PYTHON PROGRAMMING
print(text.lower())               # python programming
print(text.strip())               # removes surrounding whitespace
print(text.replace("Programming", "Coding"))
print(text.strip().split())       # splits on whitespace -> list of words
print(",".join(["a", "b", "c"]))  # -> "a,b,c"
print(text.startswith("  Py"))    # True
print(text.endswith("  "))        # True
print(len(text))                  # length = 22
```

**Output:**
```
PYTHON PROGRAMMING
python programming
Python Programming
Python Coding
['Python', 'Programming']
a,b,c
True
True
22
```

Other handy methods: `title()`, `swapcase()`, `count(sub)`, `find(sub)`, `index(sub)`,
`isalpha()`, `isdigit()`, `islower()`, `isupper()`.
`find()` returns `-1` when not found; `index()` raises an error instead.

## 2.9 f-strings (formatted strings)

Prefix a string with `f` and put variables/expressions inside `{}`.

```python
name = "Ada"
age = 36

print(f"{name} is {age} years old.")
print(f"In 10 years, {name} will be {age + 10}.")
print(f"{name:*^10}")       # centered, padded with *
print(f"PI is {3.14159:.2f}")  # 2 decimal places
```

**Output:**
```
Ada is 36 years old.
In 10 years, Ada will be 46.
***Ada****
PI is 3.14
```

Format spec mini-guide: `:d` integer, `:f` float, `:.2f` float with 2 decimals, `:>5` and
`:<5` and `:^5` align right/left/center inside 5 spaces.

## 2.10 String formatting (older styles)

You will see these in older code — know how to read them.

```python
name, age = "Bob", 30

print("%s is %d years old" % (name, age))      # %-formatting
print("{} is {} years old".format(name, age))  # str.format()
print("{0} {0} {1}".format("x", "y"))          # positional reuse
```

**Output:**
```
Bob is 30 years old
Bob is 30 years old
x x y
```

> Prefer **f-strings** in new code — they are modern, fast, and clean.

## 2.11 `in` and `not in`

Test whether a substring exists inside a string. Result is a boolean.

```python
name = "Monty Python"

print("Python" in name)        # True
print("Monty" not in name)     # False
print("parrot" in name)        # False
```

**Output:**
```
True
False
False
```

## 2.12 Immutability of strings

Strings cannot be changed in place. "Modifying" always makes a new string.

```python
s = "abc"
# s[0] = "X"        # TypeError: 'str' object does not support item assignment

s2 = "X" + s[1:]     # build a new string instead
print(s2)
```

**Output:**
```
Xbc
```

---

## Conditional Statements

## 2.13 The `if` statement

Execute code only when a condition is `True`.

```python
age = 18

if age >= 18:
    print("You can vote.")
```

**Output:**
```
You can vote.
```

## 2.14 `if`-`else`

```python
age = 15

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

**Output:**
```
Minor
```

## 2.15 `if`-`elif`-`else`

Check multiple alternatives in order. The first matching one runs; the rest are skipped.

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"

print(f"Grade: {grade}")
```

**Output:**
```
Grade: B
```

## 2.16 Nested conditions

An `if` inside another `if` — use sparingly; flat logic is usually clearer.

```python
num = 15

if num > 0:
    if num % 2 == 0:
        print("positive and even")
    else:
        print("positive and odd")
else:
    print("not positive")
```

**Output:**
```
positive and odd
```

## 2.17 Comparison operators

| Operator | Meaning              | Example      |
|----------|----------------------|--------------|
| `==`     | Equal to             | `3 == 3` → True  |
| `!=`     | Not equal to         | `3 != 4` → True  |
| `>`      | Greater than         | `5 > 3` → True   |
| `<`      | Less than            | `5 < 3` → False  |
| `>=`     | Greater or equal     | `5 >= 5` → True  |
| `<=`     | Less or equal        | `5 <= 3` → False |

```python
print(3 == 3)    # True
print(3 != 4)    # True
print(5 >= 5)    # True
```

## 2.18 Logical operators: `and`, `or`, `not`

Combine conditions.

```python
x = 10

print(x > 5 and x < 20)    # True  (both true)
print(x > 15 or x > 5)     # True  (one true)
print(not x > 5)           # False (negates the True)
```

**Output:**
```
True
True
False
```

## 2.19 Identity operators: `is`, `is not`

`is` checks whether two objects are the **same object in memory**, not just equal.
For small integers and strings Python reuses objects, so `is` often returns `True` — but
don't rely on it; use `is` with `None`, and `==` for value comparison.

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)    # True  — same values
print(a is b)    # False — different objects in memory
print(a is c)    # True  — same object (two names, one list)
print(None is None)  # True
```

**Output:**
```
True
False
True
True
```

## 2.20 Membership operators: `in`, `not in`

Work on strings, lists, tuples, dictionaries, and sets.

```python
print("e" in "hello")          # True
print(3 in [1, 2, 3])          # True
print(10 not in [1, 2, 3])     # True
print("age" in {"name": "x"})  # False — `in` on a dict checks KEYS
```

**Output:**
```
True
True
True
False
```

## 2.21 Truthy and falsy values

In conditions, Python treats almost everything as `True` except these falsy values:

- `0`, `0.0`, `0j`
- `""` (empty string)
- `[]`, `()` , `{}`, `set()`
- `None`

```python
if 0:
    print("won't print")
if "":          # empty string
    print("won't print either")
if [1, 2]:
    print("non-empty list is truthy")
if 42:
    print("42 is truthy")
```

**Output:**
```
non-empty list is truthy
42 is truthy
```

## 2.22 Conditional expression / ternary operator

A one-line `if`-`else` that returns a value.

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)

# Same idea with a function
def min_of(a, b):
    return a if a < b else b

print(min_of(7, 3))
```

**Output:**
```
Adult
3
```

## 2.23 Common string/conditional mistakes

1. **Comparing strings with `is` instead of `==`.**
2. **Mutable default-like confusion**: `[]` is falsy only when empty.
3. **Chained comparison pitfall**: `3 < x < 10` is valid and checks both — nice!
4. **Forgetting Python is case-sensitive** — `"Python" != "python"`.

## 2.24 Key Takeaways

- Strings support indexing, slicing, f-strings, and many built-in methods — and are immutable. ✔
- Use f-strings for readable formatted output. ✔
- `if/elif/else` runs the first true branch. ✔
- Chain with `and`, `or`, `not`; use `==` for equality and `is` only for identity. ✔
- Falsy values are `0`, `""`, `[]`, `()` , `{}`, `None`. ✔

## 2.25 Practice Exercises

1. Ask the user for their name with `input()` and print a personalized greeting with an f-string.
2. Check whether `"code" in "overcoding"` and explain the result.
3. Take a string, reverse it, and print `it is a palindrome` if it equals the original.
4. Ask for a number and print `even` or `odd` using a ternary expression.
5. Write a program that prints a category for a temperature: `< 0` freezing, `0–20` cold,
   `20–35` pleasant, `> 35` hot.

---

# 3. Lists and Tuples

## 3.1 What are lists?

A **list** is an ordered, changeable (mutable) collection, written in square brackets `[]`.
Lists can hold items of mixed types.

```python
fruits = ["apple", "banana", "cherry"]
mixed = [1, "two", 3.0, True, [5, 6]]   # lists can hold anything
print(fruits)
print(mixed)
```

**Output:**
```
['apple', 'banana', 'cherry']
[1, 'two', 3.0, True, [5, 6]]
```

## 3.2 Indexing and slicing

Same rules as strings: start at `0`, negative from the end, `[start:stop:step]` slices.

```python
nums = [10, 20, 30, 40, 50]

print(nums[0])        # 10
print(nums[-1])       # 50
print(nums[1:4])      # [20, 30, 40]
print(nums[::2])      # [10, 30, 50]
print(nums[::-1])     # reversed copy
```

**Output:**
```
10
50
[20, 30, 40]
[10, 30, 50]
[50, 40, 30, 20, 10]
```

## 3.3 Adding elements

```python
nums = [1, 2, 3]

nums.append(4)            # add to the end
print(nums)

nums.insert(0, 0)         # insert at an index
print(nums)

nums.extend([5, 6])       # add many elements
print(nums)
```

**Output:**
```
[1, 2, 3, 4]
[0, 1, 2, 3, 4]
[0, 1, 2, 3, 4, 5, 6]
```

## 3.4 Updating elements

```python
nums = [10, 20, 30]
nums[1] = 99              # change by index
print(nums)

nums[0:2] = [1, 2]        # replace a slice
print(nums)
```

**Output:**
```
[10, 99, 30]
[1, 2, 30]
```

## 3.5 Removing elements

```python
nums = [1, 2, 3, 4, 3]

nums.remove(3)        # removes the FIRST occurrence of value 3
print(nums)

popped = nums.pop()   # remove and return the last item
print(popped, nums)

del nums[0]           # delete by index
print(nums)

nums.clear()          # empty the list
print(nums)
```

**Output:**
```
[1, 2, 4, 3]
3 [1, 2, 4]
[2, 4]
[]
```

## 3.6 List methods summary

| Method          | What it does                              |
|-----------------|-------------------------------------------|
| `append(x)`     | Add `x` to the end                        |
| `insert(i, x)`  | Insert `x` at index `i`                   |
| `extend(iter)`  | Add all items from `iter`                 |
| `remove(x)`     | Remove first occurrence of `x` (error if missing) |
| `pop([i])`      | Remove & return item at index `i` (default last) |
| `clear()`       | Remove all items                          |
| `index(x)`      | Index of first `x`                        |
| `count(x)`      | How many times `x` appears                |
| `sort()`        | Sort in place                             |
| `reverse()`     | Reverse in place                          |
| `copy()`        | Return a shallow copy                     |

```python
names = ["Zoe", "Ana", "Eve"]
names.sort()
print(names)
names.reverse()
print(names)

print(names.count("Ana"))
print([1, 4, 2, 8, 5].index(8))
```

**Output:**
```
['Ana', 'Eve', 'Zoe']
['Zoe', 'Eve', 'Ana']
1
3
```

## 3.7 Iterating over lists

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)

# With index
for i, fruit in enumerate(fruits):
    print(i, fruit)
```

**Output:**
```
apple
banana
cherry
0 apple
1 banana
2 cherry
```

## 3.8 Nested lists

Lists inside lists — perfect for tables, grids, or matrices.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]

print(matrix[0])        # first row
print(matrix[1][2])     # row 1, column 2 -> 6

for row in matrix:
    for value in row:
        print(value, end=" ")
    print()             # newline after each row
```

**Output:**
```
[1, 2, 3]
6
1 2 3
4 5 6
7 8 9
```

## 3.9 List unpacking

Assign each list element to a variable in one line.

```python
point = [3, 7]
x, y = point
print(x, y)

grades = [90, 80, 70, 60]
first, *rest = grades
print(first, rest)

a, b, c, *others = grades
print(a, b, c, others)
```

**Output:**
```
3 7
90 [80, 70, 60]
90 80 70 [60]
```

## 3.10 List comprehensions

A compact way to build a new list from another. Pattern:

```python
# [expression for item in iterable if condition]

squares = [n ** 2 for n in range(6)]
print(squares)

evens = [n for n in range(1, 11) if n % 2 == 0]
print(evens)

words = ["cat", "dog", "bird"]
lengths = [len(w) for w in words]
print(lengths)
```

**Output:**
```
[0, 1, 4, 9, 16, 25]
[2, 4, 6, 8, 10]
[3, 3, 4]
```

Nested comprehension example (flatten a matrix):

```python
matrix = [[1, 2], [3, 4]]
flat = [n for row in matrix for n in row]
print(flat)
```

**Output:**
```
[1, 2, 3, 4]
```

---

## Tuples

## 3.11 Creating tuples

A **tuple** is an ordered, **immutable** (unchangeable) collection in round brackets `()`.
The comma makes a tuple, not the brackets.

```python
empty = ()
one_item = (5,)          # comma is REQUIRED for a single-element tuple
numbers = (1, 2, 3)
also = 1, 2, 3           # parentheses are optional

print(empty, one_item, numbers, also)

point = (3, 7)
print(type(point))
```

**Output:**
```
() (5,) (1, 2, 3) (1, 2, 3)
<class 'tuple'>
```

## 3.12 Tuple indexing and slicing

```python
t = (10, 20, 30, 40, 50)

print(t[0])       # 10
print(t[-1])      # 50
print(t[1:4])     # (20, 30, 40)
print(t[::2])     # (10, 30, 50)
```

**Output:**
```
10
50
(20, 30, 40)
(10, 30, 50)
```

## 3.13 Tuple unpacking

```python
point = (3, 7)
x, y = point
print(x, y)

coords = (1, 2, 3)
a, b, c = coords
print(a, b, c)

name, age, city = ("Ana", 25, "Berlin")
print(name, age, city)
```

**Output:**
```
3 7
1 2 3
Ana 25 Berlin
```

## 3.14 Nested tuples

```python
grid = ((1, 2), (3, 4))
print(grid[1][0])     # 3

for row in grid:
    for cell in row:
        print(cell, end=" ")
    print()
```

**Output:**
```
3
1 2
3 4
```

## 3.15 Tuple methods

Tuples only have two methods because they can't change:

```python
t = (1, 2, 2, 3, 2)

print(t.count(2))     # 3
print(t.index(3))     # 3  -> index of first 3
print(len(t))         # 5  (len() works everywhere)
```

**Output:**
```
3
3
5
```

## 3.16 Immutability

Tuples cannot be modified. That's their super-power: they are safe to share.

```python
t = (1, 2, 3)
# t[0] = 99     # TypeError: 'tuple' object does not support item assignment
# t.append(4)   # AttributeError: 'tuple' object has no attribute 'append'
print(t)
```

**Output:**
```
(1, 2, 3)
```

## 3.17 When to use lists vs tuples

| Feature              | Lists                    | Tuples                  |
|----------------------|--------------------------|-------------------------|
| Syntax               | `[1, 2, 3]`              | `(1, 2, 3)`             |
| Mutable?             | Yes                      | No                      |
| Use for              | Changing data            | Fixed data              |
| Speed memory         | Slightly heavier         | Lighter/faster          |
| Can be a dict key?   | No (unhashable)          | Yes (if values hashable)|
| Typical use          | To-do lists, collections | Coordinates, return values, constants |

```python
# tuple can be a dictionary key, list cannot
d = {(0, 0): "origin"}
print(d[(0, 0)])

# a function that returns several values returns a tuple
def divmod_pair(a, b):
    return a // b, a % b   # returns a tuple

q, r = divmod_pair(17, 5)
print(q, r)
```

**Output:**
```
origin
3 2
```

## 3.18 Common mistakes

1. `(5)` is an **int**, not a tuple — you need `(5,)`.
2. Trying to change a tuple element (TypeError).
3. Expecting `sort()` to return a sorted copy — it sorts **in place** and returns `None`.
4. Modifying a list you are iterating over at the same time (skip or iterate a copy).

## 3.19 Key Takeaways

- Lists are mutable, ordered, and perfect for changing data. ✔
- Tuples are immutable but faster and usable as dictionary keys. ✔
- Unpacking works for both. ✔
- A one-item tuple needs a trailing comma. ✔

## 3.20 Practice Exercises

1. Create a list of 5 numbers; print the sum using `sum()`, the max with `max()`, and the min with `min()`.
2. Add `0` to the front, `10` to the back, and remove the middle element.
3. `[n for n in range(1, 21) if n % 3 == 0]` — predict the output, then run it.
4. Unpack `("lat", "long")` position data into two variables.
5. Try to make a list the key of a dictionary. What error appears? Explain why.
6. Use a list comprehension to build a list of the lengths of `words = ["apple", "pear", "kiwi"]`.

---

# 4. Dictionaries and Sets

## 4.1 Creating dictionaries

A **dictionary** stores **key-value pairs**, written with curly braces `{}`. Keys are unique,
and values can be anything.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York",
}

print(person)

empty = {}
also_empty = dict()
print(empty, also_empty)
```

**Output:**
```
{'name': 'Alice', 'age': 30, 'city': 'New York'}
{} {}
```

## 4.2 Keys and values

- Keys must be **immutable** and hashable: `int`, `str`, `float`, `tuple`, `bool`, `None`.
- Lists and dictionaries cannot be keys.
- Values can be any type, including lists, dicts, functions, etc.
- Keys are unique — a later duplicate overwrites the earlier one.

```python
d = {
    1: "one",
    "two": 2,
    (1, 2): "tuple key",     # a tuple is allowed
    # [1, 2]: "list key",    # ERROR: unhashable type: 'list'
}
print(d[(1, 2)])
```

**Output:**
```
tuple key
```

## 4.3 Accessing values

```python
person = {"name": "Bob", "age": 40}

print(person["name"])          # bracket access — error if key missing

print(person.get("age"))       # .get() — safe
print(person.get("job", "unknown"))   # default value if missing
print(person.get("city"))      # None if missing

print("name" in person)        # check via membership
```

**Output:**
```
Bob
40
unknown
None
True
```

## 4.4 Adding / updating items

```python
person = {"name": "Bob"}

person["age"] = 40          # add a new key
person["name"] = "Robert"   # update an existing key
print(person)

person.update({"city": "Paris", "age": 41})   # merge many at once
print(person)
```

**Output:**
```
{'name': 'Robert', 'age': 40}
{'name': 'Robert', 'age': 41, 'city': 'Paris'}
```

## 4.5 Removing items

```python
person = {"name": "Ana", "age": 25, "city": "Berlin", "job": "Dev"}

removed = person.pop("job")      # remove key, return its value
print(removed, person)

del person["city"]               # delete a key
print(person)

person.pop("nothing", "default")  # safe pop with default
```
**Output:**
```
Dev {'name': 'Ana', 'age': 25, 'city': 'Berlin'}
{'name': 'Ana', 'age': 25}
```

## 4.6 Dictionary methods

| Method          | Description                                     |
|-----------------|-------------------------------------------------|
| `keys()`        | View of all keys                                |
| `values()`      | View of all values                              |
| `items()`       | View of (key, value) pairs                      |
| `get(k, [def])` | Value for key or default                        |
| `pop(k, [def])` | Remove and return value                         |
| `update(dict)`  | Merge another dict                              |
| `setdefault(k, v)` | Insert only if key missing                  |
| `clear()`       | Remove everything                               |
| `copy()`        | Shallow copy                                    |

```python
person = {"name": "Ana", "age": 25}

print(list(person.keys()))
print(list(person.values()))
print(list(person.items()))
```

**Output:**
```
['name', 'age']
['Ana', 25]
[('name', 'Ana'), ('age', 25)]
```

## 4.7 Iterating over dictionaries

```python
person = {"name": "Ana", "age": 25, "city": "Berlin"}

for key in person:                    # keys by default
    print(key)

for key in person.keys():             # same thing
    print(key)

for value in person.values():         # values
    print(value)

for key, value in person.items():     # both
    print(f"{key} = {value}")
```

**Output:**
```
name
age
city
Ana
25
Berlin
name = Ana
age = 25
city = Berlin
```

## 4.8 Nested dictionaries

Dictionaries inside dictionaries model real-world data beautifully.

```python
users = {
    "alice": {"age": 30, "email": "alice@example.com"},
    "bob":   {"age": 25, "email": "bob@example.com"},
}

print(users["bob"]["email"])          # navigate two levels deep

for name, info in users.items():
    print(f"{name} is {info['age']} years old")
```

**Output:**
```
bob@example.com
alice is 30 years old
bob is 25 years old
```

## 4.9 Dictionary comprehensions

```python
squares = {n: n ** 2 for n in range(5)}
print(squares)

ages = {"Ana": 25, "Bob": 40, "Eve": 30}
adults = {name: age for name, age in ages.items() if age >= 30}
print(adults)
```

**Output:**
```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
{'Bob': 40, 'Eve': 30}
```

## 4.10 Dictionary unpacking

```python
first = {"a": 1, "b": 2}
second = {"b": 3, "c": 4}

merged = {**first, **second}    # later values win for duplicate keys
print(merged)

def show(**kwargs):
    for k, v in kwargs.items():
        print(k, v)

show(name="Ana", age=25)
```

**Output:**
```
{'a': 1, 'b': 3, 'c': 4}
name Ana
age 25
```

---

## Sets

## 4.11 Creating sets

A **set** is an unordered collection of **unique** items in curly braces `{}`.
Empty set needs `set()`.

```python
numbers = {1, 2, 3, 3, 2, 1}    # duplicates are dropped
print(numbers)

letters = set("hello")
print(letters)

empty = set()                   # {} is an EMPTY DICT, not a set!
print(empty, type(empty))
```

**Output:**
```
{1, 2, 3}
{'h', 'e', 'l', 'o'}
set() <class 'set'>
```

## 4.12 Set properties

- Unordered — elements have no index; you can't do `numbers[0]`.
- Unique — duplicates vanish automatically.
- Mutable — add/remove elements.
- Elements must be hashable (like dict keys).
- Set membership tests are **very fast**.

```python
data = {1, 2}
# print(data[0])  # TypeError: 'set' object is not subscriptable
print(5 in {1, 2, 5})   # True
```

**Output:**
```
True
```

## 4.13 Adding / removing elements

```python
s = {1, 2}

s.add(3)
print(s)

s.update([4, 5, 6])
print(s)

s.remove(4)     # error if missing
print(s)

s.discard(99)   # NO error if missing — safe
print(s)

s.discard(6)
popped = s.pop()    # removes and returns an ARBITRARY element
print(popped, s)

s.clear()
print(s)
```

**Output:**
```
{1, 2, 3}
{1, 2, 3, 4, 5, 6}
{1, 2, 3, 5, 6}
{1, 2, 3, 5, 6}
1 {2, 3, 5}
set()
```

## 4.14 Set operations: union, intersection, difference, symmetric difference

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)          # union         -> all from both
print(a.union(b))     # same

print(a & b)          # intersection  -> common items
print(a.intersection(b))

print(a - b)          # difference    -> in a, not in b
print(a.difference(b))

print(a ^ b)          # symmetric diff-> in one OR other, not both
print(a.symmetric_difference(b))
```

**Output:**
```
{1, 2, 3, 4, 5, 6}
{1, 2, 3, 4, 5, 6}
{3, 4}
{3, 4}
{1, 2}
{1, 2}
{1, 2, 5, 6}
{1, 2, 5, 6}
```

## 4.15 Comparing and testing sets

```python
a = {1, 2, 3}
b = {1, 2, 3}
c = {1, 2}

print(a == b)            # True — same elements
print(a == c)            # False
print(c.issubset(a))     # True — c inside a
print(a.issuperset(c))   # True — a contains c
print(a.isdisjoint({9})) # True — no shared elements
```

**Output:**
```
True
False
True
True
True
```

## 4.16 Set comprehensions

```python
evens = {n for n in range(10) if n % 2 == 0}
print(evens)

unique_lengths = {len(w) for w in ["cat", "dog", "bird", "elephant"]}
print(unique_lengths)
```

**Output:**
```
{0, 2, 4, 6, 8}
{3, 4, 8}
```

## 4.17 When to use sets

- Removing duplicates from a collection.
- Fast membership checks (`x in huge_collection`).
- Comparing collections (math set operations).

```python
words = ["apple", "banana", "apple", "cherry", "banana"]
unique_words = set(words)
print(unique_words)

duplicates_removed = list(unique_words)
print(duplicates_removed)
```

**Output:**
```
{'cherry', 'banana', 'apple'}
['cherry', 'banana', 'apple']
```

## 4.18 Dictionaries vs sets — quick reference

| Feature               | Dictionary                              | Set                                 |
|-----------------------|-----------------------------------------|-------------------------------------|
| Written with          | `{"key": value}`                        | `{value}` or `set()`                |
| Empty                 | `{}`                                    | `set()`                             |
| Stores                | key-value pairs                         | unique values only                  |
| Index/slice?          | By key                                  | No (unordered)                      |
| Order (Python ≥3.7)   | Insertion order for dicts               | Unordered                           |
| Use for               | Lookup by key, structured data          | Deduplication, membership, set math |
| Methods               | `keys()`, `values()`, `items()`, `get()`| `add()`, `union()`, `intersection()`|

## 4.19 Common mistakes

1. Using `{}` and thinking you made a set — it's an empty dict.
2. Using a list as a dict key or set element — must be hashable; use a tuple instead.
3. Expecting set ordering — order is not guaranteed.

## 4.20 Key Takeaways

- Dicts map unique keys to values; lookups are fast. ✔
- `.get()` is the safe way to read; `in` checks keys. ✔
- Sets store unique, unordered items and excel at deduplication and set math. ✔
- `{}` = dict, `set()` = set. ✔

## 4.21 Practice Exercises

1. Build a dict from `name`, `age`, `skills` (list) and print each key's value.
2. Use `dict.get()` for a missing key and provide a default.
3. Write a function `word_count(text)` that returns a dict of word → frequency.
4. Given two lists, find the common items (intersection) and items only in the first.
5. Count the number of unique characters in a string using a set.
6. Use a dict comprehension to invert a small dict (swap keys and values).

---

# 5. Loops

## 5.1 Why loops are used

Loops let you repeat an action without writing the same code dozens of times. Instead of:

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

## 5.2 `for` loops

`for item in collection:` — runs once for each item.

```python
for letter in "abc":
    print(letter)

for n in [1, 2, 3]:
    print(n * 10)
```

**Output:**
```
a
b
c
10
20
30
```

## 5.3 `while` loops

`while condition:` — runs **as long as** the condition is `True`. Make sure the condition
eventually becomes `False`.

```python
count = 0
while count < 5:
    print("Count:", count)
    count = count + 1
```

**Output:**
```
Count: 0
Count: 1
Count: 2
Count: 3
Count: 4
```

## 5.4 `range()`

`range()` generates sequences of numbers. `range(stop)`, `range(start, stop)`,
`range(start, stop, step)`.

```python
print(list(range(5)))            # 0..4
print(list(range(2, 7)))         # 2..6
print(list(range(2, 11, 3)))     # 2, 5, 8
print(list(range(10, 0, -2)))    # 10, 8, 6, 4, 2 (backwards)

for i in range(3):
    print(f"iteration {i}")
```

**Output:**
```
[0, 1, 2, 3, 4]
[2, 3, 4, 5, 6]
[2, 5, 8]
[10, 8, 6, 4, 2]
iteration 0
iteration 1
iteration 2
```

## 5.5 Iterating over various collections

```python
# string
for ch in "hi":
    print("str:", ch)

# list
for x in [10, 20]:
    print("list:", x)

# tuple
for x in (1, 2):
    print("tuple:", x)

# dict (keys by default)
for k in {"name": "Ana", "age": 25}:
    print("dict key:", k)

# dict items
for k, v in {"name": "Ana", "age": 25}.items():
    print("pair:", k, v)

# set (unordered but consistent within a run)
for x in {8, 9, 10}:
    print("set:", x)
```

**Output:**
```
str: h
str: i
list: 10
list: 20
tuple: 1
tuple: 2
dict key: name
dict key: age
pair: name Ana
pair: age 25
set: 8
set: 9
set: 10
```

## 5.6 Nested loops

Loops inside loops. The inner loop fully finishes for each step of the outer loop.

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i * j, end=" ")
    print()   # newline after inner loop finishes
```

**Output:**
```
1 2 3
2 4 6
3 6 9
```

## 5.7 `break` — exit the loop immediately

```python
for n in range(1, 100):
    if n == 3:
        break
    print(n)
```

**Output:**
```
1
2
```

## 5.8 `continue` — skip to the next iteration

```python
for n in range(1, 6):
    if n == 3:
        continue
    print(n)
```

**Output:**
```
1
2
4
5
```

## 5.9 `pass` — placeholder that does nothing

```python
for n in range(3):
    pass          # "I'll write this section later"

def not_ready_yet():
    pass
```

No output. `pass` keeps the code syntactically valid while you develop.

## 5.10 Loop `else`

The `else` block runs **only if the loop finishes without hitting `break`**. Handy for
search loops.

```python
nums = [4, 6, 15, 8]
for n in nums:
    if n % 2 != 0:
        print(f"Found odd: {n}")
        break
else:
    print("No odd numbers found")

for n in [4, 6, 8]:
    if n % 2 != 0:
        break
else:
    print("All even.")
```

**Output:**
```
Found odd: 15
All even.
```

## 5.11 Common loop patterns

```python
# Sum
total = 0
for n in [10, 20, 30]:
    total += n
print("total:", total)

# Count matching items
count = 0
for ch in "hello world":
    if ch == "l":
        count += 1
print("l count:", count)

# Build a list
result = []
for n in range(5):
    result.append(n ** 2)
print(result)

# Index and value together
for i, ch in enumerate("abc"):
    print(i, ch)
```

**Output:**
```
total: 60
l count: 3
[0, 1, 4, 9, 16]
0 a
1 b
2 c
```

## 5.12 Avoiding infinite loops

An infinite loop never ends. When writing `while`, always ask: *does something change the
condition?*

```python
# DANGER (do NOT run this):
# n = 0
# while n < 5:
#     print(n)        # n never changes -> runs forever

# FIX: make sure the condition changes
n = 0
while n < 5:
    print(n)
    n += 1            # <-- changes n each iteration
```

**Output:**
```
0
1
2
3
4
```

Guardrails: use `break` when needed, or switch to a `for` loop with `range()` whenever the
number of iterations is known in advance.

## 5.13 Common mistakes

1. Forgetting to update the condition variable in a `while` loop (infinite loop).
2. `continue` placed where it skips the update statement (also infinite).
3. Modifying a list while iterating over it — iterate a copy instead.
4. Off-by-one: `range(5)` gives `0..4`, not `0..5`.

## 5.14 Key Takeaways

- `for` is the workhorse for iterating over collections. ✔
- `while` repeats while a condition holds — update the condition or risk an infinite loop. ✔
- `break` leaves the loop; `continue` skips one iteration; `else` runs if no `break`. ✔
- `range()` gives numeric sequences for indexed loops. ✔

## 5.15 Practice Exercises

1. Print all even numbers from 1 to 20 using a `for` loop.
2. Compute the sum of all numbers from 1 to 100 with a `while` loop (answer: `5050`).
3. Print a multiplication table for 5 (5×1 to 5×10).
4. Build the pattern `*`, `**`, `***`, `****` using nested loops.
5. Use `enumerate()` to print index + value for `["a", "b", "c"]`.
6. Write a loop-with-`else` that confirms a list contains no negative numbers.

---

# 6. Functions and Recursion

## 6.1 Why functions are useful

Functions wrap reusable logic into a named block:

- **Reuse** — write once, call many times.
- **Organization** — break big problems into small pieces.
- **Testing & debugging** — fix a bug in one place.
- **Readability** — names explain *what* the code does.

## 6.2 Defining functions

`def` defines a function. The body is indented.

```python
def greet():
    print("Hello, world!")

greet()        # call the function
greet()        # call it again
```

**Output:**
```
Hello, world!
Hello, world!
```

## 6.3 Calling functions

```python
def say_hi(name):
    print(f"Hi, {name}!")

say_hi("Alice")
say_hi("Bob")
```

**Output:**
```
Hi, Alice!
Hi, Bob!
```

## 6.4 Parameters and arguments

**Parameters** are the names in the definition. **Arguments** are the values you pass when
calling.

```python
def add(a, b):          # a and b are parameters
    return a + b

result = add(3, 5)      # 3 and 5 are arguments
print(result)
```

**Output:**
```
8
```

## 6.5 Positional arguments

Arguments in the same order as parameters.

```python
def describe(name, age, city):
    print(f"{name} is {age} and lives in {city}")

describe("Ana", 30, "Paris")
```

**Output:**
```
Ana is 30 and lives in Paris
```

## 6.6 Keyword arguments

Pass by parameter name — order no longer matters.

```python
def describe(name, age, city):
    print(f"{name} is {age} and lives in {city}")

describe(city="Paris", age=30, name="Ana")
```

**Output:**
```
Ana is 30 and lives in Paris
```

You can mix positional and keyword, but positional-first:

```python
describe("Ana", age=30, city="Paris")   # OK
# describe(name="Ana", 30, "Paris")     # ERROR: positional after keyword
```

## 6.7 Default arguments

Parameters can have default values; callers may omit them.

```python
def greet(name="world"):
    print(f"Hello, {name}!")

greet()            # uses default
greet("Python")    # overrides it
```

**Output:**
```
Hello, world!
Hello, Python!
```

> **Warning:** never use a mutable default like `[]` or `{}` — it is shared across calls.

```python
# BAD:
def add_item(item, bag=[]):
    bag.append(item)
    return bag

print(add_item("a"))   # ['a']
print(add_item("b"))   # ['a', 'b']  <-- shared bag, bug!

# GOOD:
def add_item(item, bag=None):
    if bag is None:
        bag = []
    bag.append(item)
    return bag

print(add_item("a"))
print(add_item("b"))
```

**Output:**
```
['a']
['a', 'b']
['a']
['b']
```

## 6.8 Variable-length arguments: `*args` and `**kwargs`

- `*args` collects extra **positional** arguments into a tuple.
- `**kwargs` collects extra **keyword** arguments into a dict.

```python
def total(*args):
    return sum(args)

print(total(1, 2, 3))
print(total(1, 2, 3, 4, 5))


def print_details(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_details(name="Ana", age=30, job="Dev")
```

**Output:**
```
6
15
name: Ana
age: 30
job: Dev
```

You can use all argument kinds together, in this order:
`def f(positional, *args, keyword_only, **kwargs)`.

## 6.9 Return values

`return` sends a result back to the caller. A function without `return` returns `None`.

```python
def square(n):
    return n ** 2

result = square(5)
print(result)

def no_return():
    print("doing work")

print(no_return())   # prints None
```

**Output:**
```
25
doing work
None
```

## 6.10 Multiple return values

Return a tuple and unpack it.

```python
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([4, 2, 9, 1])
print(low, high)

def stats(numbers):
    total = sum(numbers)
    count = len(numbers)
    return total, count, total / count

s, c, avg = stats([10, 20, 30])
print(s, c, avg)
```

**Output:**
```
1 9
60 3 20.0
```

## 6.11 Scope: local vs global variables

Variables defined inside a function are **local** — invisible outside. Variables defined at
the top level are **global** — visible everywhere.

```python
x = 10            # global

def show():
    y = 5         # local
    print("inside:", x, y)

show()
# print(y)        # NameError: name 'y' is not defined
```

**Output:**
```
inside: 10 5
```

## 6.12 Reading vs assigning globals

Inside a function you can *read* a global, but *assigning* a variable creates a NEW local
variable unless you declare `global`.

```python
counter = 0

def read_only():
    print("reading global:", counter)

read_only()


def bad_increment():
    counter = counter + 1    # ERROR: local before assignment


def good_increment():
    global counter           # declare we mean the global
    counter += 1

good_increment()
good_increment()
print(counter)
```

**Output:**
```
reading global: 0
2
```

Rule of thumb: avoid `global` whenever possible — prefer passing values in and returning
results out.

## 6.13 Lambda functions

Anonymous one-line functions. `lambda arguments: expression`.

```python
double = lambda x: x * 2
print(double(5))

# above is identical to:
def double_func(x):
    return x * 2

# classic use: sorting with a key
points = [(3, 8), (1, 2), (5, 0)]
points.sort(key=lambda p: p[1])     # sort by the second value
print(points)

nums = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda n: n % 2 == 0, nums))
squared = list(map(lambda n: n ** 2, nums))
print(evens)
print(squared)
```

**Output:**
```
10
[(5, 0), (1, 2), (3, 8)]
[2, 4, 6]
[1, 4, 9, 16, 25]
```

## 6.14 Docstrings

A string at the top of a function/class/module that documents what it does. Accessible via
`help()` or `__doc__`.

```python
def add(a, b):
    """Return the sum of a and b."""
    return a + b

print(add.__doc__)
# help(add)   # interactive help viewer
```

**Output:**
```
Return the sum of a and b.
```

## 6.15 Type hints

Annotations tell readers (and tools like mypy) the expected types. They do **not** enforce
anything at runtime.

```python
def greet(name: str, age: int = 0) -> str:
    return f"{name} is {age} years old"

print(greet("Ana", 25))


def total(*numbers: int) -> int:
    return sum(numbers)

print(total(1, 2, 3))
```

**Output:**
```
Ana is 25 years old
6
```

## 6.16 Higher-order functions / functional concepts

Functions that take functions as arguments or return functions.

```python
def apply_twice(func, value):
    return func(func(value))

result = apply_twice(lambda n: n + 3, 2)
print(result)               # (2+3)+3 = 8

# map / filter / reduce style (built-ins)
from functools import reduce

nums = [1, 2, 3, 4]
print(list(map(lambda n: n * 10, nums)))
print(list(filter(lambda n: n % 2 == 0, nums)))
print(reduce(lambda a, b: a + b, nums))
```

**Output:**
```
8
[10, 20, 30, 40]
[2, 4]
10
```

---

## Recursion

## 6.17 What recursion is

**Recursion** is when a function calls **itself** to solve a smaller version of the same
problem.

Every recursive function needs two parts:

- **Base case** — the simplest situation where the answer is known directly; recursion stops.
- **Recursive case** — calls itself with a smaller or simpler input.

```python
def countdown(n):
    if n <= 0:           # base case
        print("Liftoff!")
        return
    print(n)
    countdown(n - 1)     # recursive case: call with a smaller n

countdown(3)
```

**Output:**
```
3
2
1
Liftoff!
```

## 6.18 How recursive calls work

Each call is placed on the **call stack**. The stack grows until the base case, then
unwinds in reverse order.

```python
def countdown(n):
    if n <= 0:
        print("Liftoff!")
        return
    print("down to", n)
    countdown(n - 1)
    print("back up from", n)

countdown(2)
```

**Output:**
```
down to 2
down to 1
Liftoff!
back up from 1
back up from 2
```

Notice: the "back up" lines print after the recursion returns — the stack unwinds in
reverse order.

## 6.19 Factorial example

`n! = n × (n-1) × ... × 1`

```python
def factorial(n):
    if n <= 1:          # base case: 0! and 1! are both 1
        return 1
    return n * factorial(n - 1)   # recursive case

print(factorial(5))
```

Trace for `factorial(5)`:
```
factorial(5) = 5 * factorial(4)
            = 5 * (4 * factorial(3))
            = 5 * (4 * (3 * factorial(2)))
            = 5 * (4 * (3 * (2 * factorial(1))))
            = 5 * (4 * (3 * (2 * 1)))
            = 5 * (4 * (3 * 2))
            = 5 * (4 * 6)
            = 5 * 24
            = 120
```

**Output:**
```
120
```

## 6.20 Fibonacci example

Each number is the sum of the two before it: `0, 1, 1, 2, 3, 5, 8, 13, ...`

```python
def fib(n):
    if n <= 1:          # fib(0) = 0, fib(1) = 1
        return n
    return fib(n - 1) + fib(n - 2)

for i in range(8):
    print(fib(i), end=" ")
print()
```

**Output:**
```
0 1 1 2 3 5 8 13
```

> Note: plain recursive Fibonacci is slow (exponential work). For large `n`, use iteration
> or memoization.

## 6.21 Recursive list / string examples

```python
def recursive_sum(numbers):
    if not numbers:            # empty list -> base case
        return 0
    return numbers[0] + recursive_sum(numbers[1:])

print(recursive_sum([1, 2, 3, 4]))


def is_palindrome(s):
    if len(s) <= 1:            # base case
        return True
    if s[0] != s[-1]:          # mismatch
        return False
    return is_palindrome(s[1:-1])   # check the inside

print(is_palindrome("racecar"))
print(is_palindrome("hello"))
```

**Output:**
```
10
True
False
```

## 6.22 Recursion vs iteration

| Aspect       | Recursion                                | Iteration                    |
|--------------|------------------------------------------|------------------------------|
| Style        | Function calls itself                    | Loops (`for`, `while`)       |
| Best for     | Tree/graph problems, divide & conquer    | Most everyday repetition     |
| Memory       | Uses call stack — can overflow           | Constant extra memory        |
| Readability  | Elegant for naturally recursive problems | Straightforward               |
| Performance  | Slower (function call overhead)          | Faster                        |

Iterative versions of the earlier examples:

```python
def factorial_iter(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

def fib_iter(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print(factorial_iter(5))
print(fib_iter(7))
```

**Output:**
```
120
13
```

## 6.23 Common recursion mistakes

1. **No base case** (or never reached) → `RecursionError: maximum recursion depth exceeded`.
2. Recursive case not making progress toward the base case.
3. Forgetting `return` in the recursive case (returns `None`).

```python
# DANGER (never run):
# def forever(n):
#     return forever(n)     # no base case -> RecursionError

# Python's recursion limit is inflated on purpose:
import sys
print(sys.getrecursionlimit())
```

**Output:**
```
1000
```

## 6.24 Key Takeaways

- Functions package logic into reusable pieces with parameters and returns. ✔
- Prefer local scope; avoid `global`; use default `None` instead of mutable defaults. ✔
- `*args` / `**kwargs` handle flexible argument lists. ✔
- Lambdas are concise one-expression functions for `map`, `filter`, `sorted` keys. ✔
- Recursion = base case + recursive case; prefer iteration when performance matters. ✔

## 6.25 Practice Exercises

1. Write `is_even(n)` and call it from a loop to print even numbers up to 20.
2. Write `random_sum(*nums)` accepting any number of arguments.
3. Write a function `describe(**info)` that prints key/value pairs from kwargs.
4. Refactor this loop into a recursive function: printing `n` down to `1`.
5. Implement `power(base, exp)` recursively (`base ** exp`).
6. Write an iterative and a recursive version of Fibonacci; print `fib(10)` for both.

---

# 7. File I/O

## 7.1 What file I/O means

**File I/O** is reading data from, and writing data to, files on disk — saving a program's
results so they survive after the program ends.

Workflow: **open → read/write → close** (or better: use `with`).

All examples below run relative to the working directory. You can create example files
yourself with small `.py` scripts or the code shown.

## 7.2 Opening files with `open()`

```python
file = open("note.txt", "r")   # "r" = read mode
# ... work with the file ...
file.close()                   # always close when done
```

The modern, safer way is the `with` statement (Section 7.10) — it closes automatically.

## 7.3 File modes

| Mode | Meaning                                   |
|------|-------------------------------------------|
| `"r"` | Read (default). Error if file missing    |
| `"w"` | Write. **Overwrites** or creates file    |
| `"a"` | Append. Adds to the end, creates if missing |
| `"x"` | Exclusive create. Error if file exists   |
| `"b"` | Binary mode (with another mode: `"rb"`)  |
| `"t"` | Text mode (default with another mode)    |
| `"+"` | Read **and** write (`"r+"`, `"w+"`)      |

The default is text mode `"t"`. Combine letters, e.g. `"rb"` for reading binary.

## 7.4 Writing files (`"w"`)

Adds or **overwrites** the file (careful — existing content is destroyed).

```python
with open("example.txt", "w") as f:
    f.write("Line one\n")
    f.write("Line two\n")
```

## 7.5 Reading whole files

```python
with open("example.txt", "r") as f:
    content = f.read()
print(content)
```

**Output:**
```
Line one
Line two
```

`read(n)` reads at most `n` characters:

```python
with open("example.txt", "r") as f:
    print(f.read(4))      # first 4 characters
```

**Output:**
```
Line
```

## 7.6 `readline()` and `readlines()`

- `readline()` reads one line at a time (keeps the newline).
- `readlines()` returns a list of all lines.

```python
with open("example.txt", "r") as f:
    first = f.readline()
    second = f.readline()
print(repr(first), repr(second))


with open("example.txt", "r") as f:
    lines = f.readlines()
print(lines)
```

**Output:**
```
'Line one\n' 'Line two\n'
['Line one\n', 'Line two\n']
```

`repr()` shows the raw string including escaped characters like `\n`.

## 7.7 Iterating over files directly

Files are iterable — the cleanest way to process line by line:

```python
with open("example.txt", "r") as f:
    for line in f:
        print("->", line.rstrip())   # rstrip() removes the trailing newline
```

**Output:**
```
-> Line one
-> Line two
```

## 7.8 Appending to files (`"a"`)

Adds to the end without deleting what's already there.

```python
with open("example.txt", "a") as f:
    f.write("Line three\n")
```

Then reading shows all three lines:

```python
with open("example.txt", "r") as f:
    print(f.read())
```

**Output:**
```
Line one
Line two
Line three
```

## 7.9 `"x"` mode — create only if it does NOT exist

Prevents accidental overwrites.

```python
try:
    with open("brand_new.txt", "x") as f:
        f.write("Only created once!\n")
    print("File created.")
except FileExistsError:
    print("File already exists!")
```

On first run:
```
File created.
```
On a second run:
```
File already exists!
```

## 7.10 `with` statement / context managers

`with` guarantees the file is closed even if an error occurs mid-operation.

```python
with open("example.txt", "r") as f:
    data = f.read()
# f is automatically closed here — no manual f.close() needed
print("Closed automatically:", f.closed)
```

**Output:**
```
Closed automatically: True
```

## 7.11 File paths

- **Relative** paths are interpreted from the current working directory.
- **Absolute** paths give the full location from the drive root.

```python
import os

# current working directory
print(os.getcwd())

# joining paths cross-platform (Windows "\", Linux/Mac "/")
path = os.path.join("data", "notes", "todo.txt")
print(path)

# does a file exist?
print(os.path.exists("example.txt"))
```

**Output (path values vary by machine):**
```
D:\python\Day-2
data\notes\todo.txt
True
```

## 7.12 Basic exception handling for file operations

Guard against missing files and permission problems.

```python
try:
    with open("does_not_exist.txt", "r") as f:
        print(f.read())
except FileNotFoundError:
    print("Sorry, that file does not exist.")
except PermissionError:
    print("You are not allowed to open that file.")
```

**Output:**
```
Sorry, that file does not exist.
```

A general fallback with `finally`:

```python
try:
    with open("example.txt", "r") as f:
        print(f.read())
except OSError as e:
    print("An OS error occurred:", e)
finally:
    print("Cleanup always runs.")
```

**Output:**
```
Line one
Line two
Line three
Cleanup always runs.
```

## 7.13 Working with text files — a practical example

Write user input to a file, then read it back.

```python
todos = ["buy milk", "learn Python", "water plants"]

with open("todos.txt", "w") as f:
    for item in todos:
        f.write(item + "\n")

with open("todos.txt", "r") as f:
    lines = [line.strip() for line in f]

print(lines)

with open("todos.txt", "a") as f:
    f.write("go to gym\n")

with open("todos.txt", "r") as f:
    final = [line.strip() for line in f]
print(final)
```

**Output:**
```
['buy milk', 'learn Python', 'water plants']
['buy milk', 'learn Python', 'water plants', 'go to gym']
```

## 7.14 Basic JSON file handling

Python's `json` module turns dictionaries/lists into JSON text (and back). Stored JSON files
can be read by other programs and languages.

```python
import json

person = {"name": "Ana", "age": 30, "skills": ["Python", "SQL"]}

# write
with open("person.json", "w") as f:
    json.dump(person, f, indent=2)

# read back
with open("person.json", "r") as f:
    loaded = json.load(f)

print(loaded)
print(loaded["skills"])

# in-memory conversion
text = json.dumps({"a": 1, "b": [1, 2]})
print(text)
print(json.loads(text))
```

**Output:**
```
{'name': 'Ana', 'age': 30, 'skills': ['Python', 'SQL']}
['Python', 'SQL']
{"a": 1, "b": [1, 2]}
{'a': 1, 'b': [1, 2]}
```

The file `person.json` contains:
```json
{
  "name": "Ana",
  "age": 30,
  "skills": [
    "Python",
    "SQL"
  ]
}
```

## 7.15 Common mistakes

1. Reading a file you opened in `"w"` mode (it's being rewritten).
2. Forgetting `"\n"` when writing lines — everything appears on one line.
3. The default `"r"` mode raising `FileNotFoundError` for typo'd filenames.
4. Manual `open()` without `.close()` — use `with` instead.
5. Mixing text and binary modes (e.g., encoding errors).

## 7.16 Key Takeaways

- Always use `with open(...) as f` — automatic cleanup. ✔
- `"w"` overwrites; `"a"` appends; `"r"` reads; `"x"` creates-only-once. ✔
- Files iterate line by line; wrap bytes/text handling with `"t"`/`"b"` modes. ✔
- `json.dump` / `json.load` move dict/list data to disk and back. ✔
- Handle `FileNotFoundError` and `PermissionError` with `try`/`except`. ✔

## 7.17 Practice Exercises

1. Write your name and age to a file, then read it back and print it.
2. Append three more lines to that file, then print its total line count.
3. Read a file and print each line with its line number (`1: text`).
4. Write a list of 5 numbers to a text file as JSON and load it back.
5. Wrap a file read in `try/except` and handle the "file missing" case gracefully.

---

# 8. OOPs / Object-Oriented Programming

## 8.1 What is OOP?

OOP (**Object-Oriented Programming**) is a way of organizing code around **objects** — bundles
of *data* (attributes) and *behavior* (methods). Instead of scattering data and functions
around your program, you model real-world things as objects that know how to act.

## 8.2 Why OOP is useful

- **Modelling**: classes mirror real-world concepts (a `Car`, a `User`, a `BankAccount`).
- **Reuse**: build once, extend with inheritance.
- **Data safety**: encapsulation hides internal details.
- **Organization**: large programs stay comprehensible.
- **Teamwork**: each object has a clear, contained responsibility.

## 8.3 Classes and objects

- A **class** is the *blueprint* / recipe.
- An **object** (instance) is a concrete thing built from that blueprint.

| Concept     | Analogy              | Python                |
|-------------|----------------------|-----------------------|
| Class       | Blueprint of a house | `class Car:`          |
| Object      | A specific house     | `my_car = Car()`      |
| Attribute   | Colour of the house  | `my_car.color`        |
| Method      | House's doorbell     | `my_car.drive()`      |

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name} says Woof!")

rex = Dog("Rex")   # create an OBJECT from the Dog CLASS
rex.bark()
```

**Output:**
```
Rex says Woof!
```

## 8.4 Creating a class

Minimum viable class:

```python
class Empty:
    pass

e = Empty()
print(e, type(e))
```

**Output:**
```
<__main__.Empty object at 0x...> <class '__main__.Empty'>
```

The memory address `0x...` will differ on every run — it's just the object's location.

## 8.5 `__init__()` — the constructor

`__init__` runs automatically when an object is created. It's where you set up instance
attributes. The name `self` refers to the object being created.

```python
class Person:
    def __init__(self, name, age):
        self.name = name          # instance attribute
        self.age = age

p = Person("Ana", 30)
print(p.name, p.age)
```

**Output:**
```
Ana 30
```

## 8.6 Instance attributes

Data that belongs to a single object. Each object has its own copies.

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

c1 = Car("Toyota", "red")
c2 = Car("Honda", "blue")

print(c1.brand, c1.color)   # Toyota red
print(c2.brand, c2.color)   # Honda blue

c1.color = "green"          # changing c1 does not affect c2
print(c1.color, c2.color)
```

**Output:**
```
Toyota red
Honda blue
green blue
```

## 8.7 Class attributes

Shared by **all** instances of the class. Defined inside the class but outside `__init__`.

```python
class Employee:
    company = "TechCorp"          # class attribute
    count = 0

    def __init__(self, name):
        self.name = name          # instance attribute
        Employee.count += 1

e1 = Employee("Ana")
e2 = Employee("Bob")

print(e1.company, e2.company)     # shared
print(Employee.company)           # accessible via the class too
print(Employee.count)             # 2 employees created
```

**Output:**
```
TechCorp TechCorp
TechCorp
2
```

If you assign `e1.company = "Other"`, you create an **instance attribute** that shadows the
class one for `e1` only:

```python
e1 = Employee("Ana")
e2 = Employee("Bob")
e1.company = "Freelance"          # only e1 gets its own
print(e1.company, e2.company, Employee.company)
```

**Output:**
```
Freelance TechCorp TechCorp
```

## 8.8 Instance methods

All regular methods take `self` as the first parameter.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def is_square(self):
        return self.width == self.height

r = Rectangle(4, 5)
print(r.area())
print(r.is_square())

s = Rectangle(3, 3)
print(s.is_square())
```

**Output:**
```
20
False
True
```

## 8.9 Class methods (`@classmethod`)

Methods that operate on the **class** rather than an instance. First parameter is `cls`.

Common uses: factory methods that create instances in alternative ways.

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    @classmethod
    def from_string(cls, data):
        name, email = data.split("|")
        return cls(name, email)       # builds an instance

u = User.from_string("Ana|ana@x.com")
print(u.name, u.email)
```

**Output:**
```
Ana ana@x.com
```

## 8.10 Static methods (`@staticmethod`)

Methods that don't need `self` or `cls` — just utility code related to the class.

```python
class MathUtils:
    @staticmethod
    def is_even(n):
        return n % 2 == 0

print(MathUtils.is_even(4))    # call via the class

# also callable via an instance
m = MathUtils()
print(m.is_even(7))
```

**Output:**
```
True
False
```

## 8.11 `self` explained

When Python calls `r.area()`, it actually calls `Rectangle.area(r)`. `self` is simply the
object itself, giving methods access to the instance's attributes.

```python
class Demo:
    def show(self):
        print("self is:", self)

d = Demo()
d.show()                   # Python passes d as self automatically
Demo.show(d)               # explicitly passing the object
```

Both lines print (address will differ):
```
self is: <__main__.Demo object at 0x...>
self is: <__main__.Demo object at 0x...>
```

## 8.12 Encapsulation

**Encapsulation** bundles data + methods and hides internal details behind a public
interface. "Private" attributes start with an underscore `_internal` (convention) or `__name`
(name-mangled, strongly hidden).

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance      # "private" attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient funds")

    def get_balance(self):
        return self.__balance

acc = BankAccount("Ana", 1000)
acc.deposit(250)
acc.withdraw(100)
print(acc.get_balance())          # 1150

# acc.__balance                 # AttributeError: hidden outside the class
print(acc._BankAccount__balance)  # name mangling: still reachable, but discouraged
```

**Output:**
```
1150
1150
```

## 8.13 Inheritance

A **child/subclass** inherits attributes and methods from a **parent/base class**, and can
add or override its own.

```python
class Animal:                      # parent / base class
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

    def move(self):
        print(f"{self.name} moves")

class Dog(Animal):                 # child class
    def speak(self):               # override the parent's speak()
        print(f"{self.name} barks")

class Cat(Animal):
    def speak(self):
        print(f"{self.name} meows")

animals = [Dog("Rex"), Cat("Whiskers"), Animal("Thing")]

for a in animals:
    a.speak()
    a.move()
```

**Output:**
```
Rex barks
Rex moves
Whiskers meows
Whiskers moves
Thing makes a sound
Thing moves
```

The child inherits `__init__` and `move()`, but overrides `speak()`.

## 8.14 Accessing the parent with `super()`

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def info(self):
        return f"Brand: {self.brand}"

class Motorcycle(Vehicle):
    def __init__(self, brand, cc):
        super().__init__(brand)     # call the parent constructor
        self.cc = cc

    def info(self):
        base = super().info()       # reuse parent logic
        return f"{base}, Engine: {self.cc}cc"

m = Motorcycle("Yamaha", 660)
print(m.info())
```

**Output:**
```
Brand: Yamaha, Engine: 660cc
```

## 8.15 Method overriding

When a child defines a method with the same name as the parent, the child's version wins
for child instances. Seen above with `speak()`.

## 8.16 Polymorphism

**Polymorphism** ("many forms") — the same method name behaves differently depending on the
object's class. Both the loop over `animals` above and the `len()` examples below show this.

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

class Square:
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2

shapes = [Circle(2), Square(3)]

for shape in shapes:
    print(shape.area())     # each object knows its own "area"
```

**Output:**
```
12.56636
9
```

built-in polymorphism:

```python
print(len("hello"))       # str length
print(len([1, 2, 3]))     # list length
print(len((1, 2)))        # tuple length
```

**Output:**
```
5
3
2
```

## 8.17 Abstraction

**Abstraction** means showing only the essential features and hiding implementation details.
You call `post.ogget_abstraction`… you interact with a clean interface without caring how it
works inside. Abstract base classes (from the `abc` module) let you define a *contract* that
subclasses must implement.

```python
from abc import ABC, abstractmethod

class Shape(ABC):                    # abstract class
    @abstractmethod
    def area(self):                  # contract: every Shape must have area()
        pass

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):                  # must be implemented here
        return 0.5 * self.base * self.height

t = Triangle(4, 3)
print(t.area())

# Shape() would raise: TypeError: Can't instantiate abstract class Shape
```

**Output:**
```
6.0
```

## 8.18 Composition

**Composition** — building complex objects from simpler ones by making one class "have" another.

```python
class Engine:
    def __init__(self, power):
        self.power = power

    def start(self):
        print(f"Engine ({self.power} hp) started")

class Car:
    def __init__(self, brand, engine):
        self.brand = brand          # Car HAS an Engine
        self.engine = engine        # composition

    def start(self):
        print(f"{self.brand} car:")
        self.engine.start()         # delegate to the engine

engine = Engine(120)
car = Car("Toyota", engine)
car.start()
```

**Output:**
```
Toyota car:
Engine (120 hp) started
```

Prefer composition over inheritance where the relationship is "has-a" rather than "is-a".

## 8.19 Special / dunder methods

Double-underscore (`__method__`) methods let your objects work with Python's built-in
functions and operators.

| Dunder method | Purpose                           |
|---------------|-----------------------------------|
| `__str__`     | Friendly string for `print()`     |
| `__repr__`    | Developer string, unambiguous     |
| `__len__`     | Support `len(obj)`                |
| `__eq__`      | Support `==` for your objects     |
| `__lt__`      | Support `<` (and thus sorting)    |
| `__add__`     | Support `+`                       |
| `__getitem__` | Support `obj[key]`                |

```python
class Book:
    def __init__(self, title, pages):
        self.title = title
        self.pages = pages

    def __str__(self):
        return f"Book('{self.title}')"

    def __repr__(self):
        return f"<Book title={self.title!r} pages={self.pages}>"

    def __len__(self):
        return self.pages

    def __eq__(self, other):
        return self.title == other.title

    def __lt__(self, other):
        return self.pages < other.pages

b1 = Book("Python 101", 300)
b2 = Book("Python 101", 300)
b3 = Book("Data Science", 500)

print(str(b1))        # friendly
print(repr(b1))       # developer-facing
print(len(b1))        # -> 300
print(b1 == b2)       # custom equality by title -> True
print(b1 < b3)        # -> True

books = [b3, b1]
books.sort()          # sorts using __lt__
print([str(b) for b in books])
```

**Output:**
```
Book('Python 101')
<Book title='Python 101' pages=300>
300
True
True
['Book('Python 101')', 'Book('Data Science')']
```

Best practice: `__repr__` for developers, `__str__` for end users. If you only define one,
`print()` falls back to `__repr__`.

## 8.20 The four pillars of OOP — review

| Pillar          | Meaning                                               | Python feature used          |
|-----------------|-------------------------------------------------------|------------------------------|
| Encapsulation   | Hide data, expose safe methods                        | `__private`, methods         |
| Inheritance     | Child reuses/extends parent code                      | `class Child(Parent)`        |
| Polymorphism    | Same interface, many behaviors                        | Overriding methods           |
| Abstraction     | Hide complex internals behind a simple interface      | Abstract base classes        |

## 8.21 A complete practical example — bank + employee

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        return f"{self.name}, {self.age} years old"

    def __str__(self):
        return f"Person({self.name})"


class Employee(Person):                      # inheritance
    def __init__(self, name, age, salary):
        super().__init__(name, age)          # parent constructor
        self.salary = salary                 # additional attribute

    def annual_income(self):
        return self.salary * 12

    def introduce(self):                     # method overriding
        return f"{super().introduce()} — salary {self.salary}"


class Manager(Employee):
    def __init__(self, name, age, salary, team_size):
        super().__init__(name, age, salary)
        self.team_size = team_size

    def annual_income(self):                 # polymorphism: bonus on top
        return super().annual_income() + self.team_size * 500


people = [
    Employee("Ana", 30, 3000),
    Manager("Bob", 40, 5000, 4),
]

for p in people:                             # polymorphism in action
    print(p.introduce())
    print("Annual income:", p.annual_income())
```

**Output:**
```
Ana, 30 years old — salary 3000
Annual income: 36000
Bob, 40 years old — salary 5000
Annual income: 62000
```

## 8.22 Common mistakes

1. Forgetting `self` as the first parameter of every instance method.
2. Forgetting `super().__init__(...)` in a child class.
3. Defining a class attribute intended as per-instance data.
4. Using `==` on objects without `__eq__` — default compares identity (same object?).
5. Instantiation missing parentheses: `Book` instead of `Book()`.

## 8.23 Key Takeaways

- A class is a blueprint; an instance is one object built from it. ✔
- `__init__` sets up instance attributes; `self` always points at the current object. ✔
- Encapsulation hides state; use `_`/`__`-prefixed names and methods. ✔
- Inheritance, overriding, and polymorphism make code reusable and flexible. ✔
- Dunder methods like `__str__`, `__len__`, `__eq__` integrate classes with built-ins. ✔

## 8.24 Practice Exercises

1. Create a `Student` class with `name`, `grade`, `roll_no` and a method `is_passing()` that returns `grade >= 40`.
2. Add a class attribute `school` and instantiate 3 students — verify it's shared.
3. Create `Shape` (abstract) with `area()`, then `Rectangle` and `Triangle` subclasses.
4. Make a `BankAccount` with `deposit`/`withdraw`/`get_balance` using encapsulation.
5. Implement `__eq__` and `__lt__` for a `Point` class so {{points can be compared}}{{and sorted}}.
6. Build `Animal` → `Dog`/`Cat` and show polymorphism in a loop.

---

# 9. Python Part-1 Cheat Sheet

## 9.1 Important syntax patterns

```python
# Variables & types
x = 5                     # int, float, str, bool, None, complex, list, dict, tuple, set
a, b = 1, 2               # multiple assignment
a, b = b, a               # swap

# Casting
int("5");  float("3.5");  str(10);  bool(0)

# Strings
s[0];  s[-1];  s[1:4];  s[::-1]          # index / slice / reverse
f"{name} is {age}"                        # f-string
s.upper();  s.lower();  s.strip();  s.split();  " ".join(list)

# Conditionals
if x > 0:
    pass
elif x < 0:
    pass
else:
    pass
"yes" if x else "no"                      # ternary

# Collections
li.append(x);  li.insert(i, x);  li.pop();  li.remove(x);  li.sort()
tu = (1, 2);  a, b = tu                   # tuple unpacking
d[key];  d.get(key, default);  d.items();  d.keys();  d.values()
[x ** 2 for x in range(5)]                # list comprehension
{x: x ** 2 for x in range(5)}             # dict comprehension
{x for x in range(5)}                     # set comprehension

# Loops
for i in range(10): ...
for i, v in enumerate(li): ...
for k, v in d.items(): ...
while condition: ...
break  /  continue  /  else               # loop helpers

# Functions
def f(a, b=0, *args, **kwargs) -> int:
    """Docstring."""
    return a
lambda x: x * 2

# Files
with open("file.txt", "r") as f:          # "r" "w" "a" "x" "+" "b" "t"
    f.read();  f.readline();  f.readlines()

# Classes
class Car:
    class_attr = 0
    def __init__(self, brand):
        self.brand = brand                # instance attr
    def drive(self): ...
    @classmethod
    def helper(cls): ...
    @staticmethod
    def util(): ...
    def __str__(self): ...
```

## 9.2 Commonly used methods / functions

| Area          | Built-ins                                  |
|---------------|---------------------------------------------|
| General       | `print`, `input`, `len`, `type`, `isinstance`, `range`, `sum`, `min`, `max`, `sorted`, `enumerate`, `zip`, `map`, `filter` |
| Strings       | `upper`, `lower`, `strip`, `split`, `join`, `replace`, `find`, `count`, `startswith`, `title`, `isdigit`, `isalpha` |
| Lists         | `append`, `insert`, `extend`, `remove`, `pop`, `index`, `count`, `sort`, `reverse`, `copy` |
| Dicts         | `get`, `keys`, `values`, `items`, `update`, `pop`, `setdefault`, `clear`, `copy` |
| Sets          | `add`, `update`, `remove`, `discard`, `pop`, `union`, `intersection`, `difference`, `isdisjoint`, `issubset`, `issuperset` |
| Files         | `open`, `close` (auto via `with`), `read`, `readline`, `readlines`, `write`, `writelines`, `flush` |
| Modules shown | `os.getcwd`, `os.path.join`, `os.path.exists`, `json.dump`, `json.load`, `json.dumps`, `json.loads`, `sys.getrecursionlimit`, `functools.reduce`, `abc.ABC`, `abc.abstractmethod` |

## 9.3 Operator reference

```python
# Arithmetic
+  -  *  /  //  %  **

# Comparison
==  !=  >  <  >=  <=

# Logical
and  or  not

# Identity
is  is not          # object identity, prefer with None

# Membership
in  not in          # strings, lists, tuples, dict keys, sets
```

## 9.4 Truthiness quick list

**Falsy:** `0`, `0.0`, `""`, `[]`, `()`, `{}`, `set()`, `None`
**Truthy:** everything else

## 9.5 Common exceptions beginners meet

| Exception         | Why it happens                                   |
|-------------------|--------------------------------------------------|
| `SyntaxError`     | Typo or bad grammar in code                       |
| `NameError`       | Variable not defined                              |
| `TypeError`       | Wrong type used in an operation                   |
| `ValueError`      | Right type, wrong value (`int("abc")`)            |
| `IndexError`      | List/tuple/string index out of range              |
| `KeyError`        | Dictionary lookup with a missing key              |
| `FileNotFoundError` | `open()` on a file that doesn't exist           |
| `RecursionError`  | Recursion without a base case                     |

---

## 10. Mixed Practice Questions

*Try these without looking at the answers, then run your solutions.*

1. Swap two variables without a temporary variable.
2. Print the data types of `7`, `7.0`, `"7"`, `[7]`, `(7,)`, `{7}`, `True`.
3. Convert a decimal string `"3.75"` to an integer. How do you deal with the error?
4. Reverse a string entered by the user and also report if it's a palindrome.
5. Count the vowels in a user-provided sentence.
6. Print letters at even indexes of `"Python"`.
7. Given `[10, 20, 30, 40, 50]`, print the first, last, and a reversed copy.
8. Merge two lists, remove duplicates, keep order.
9. From a list of numbers, produce a new list with negatives replaced by 0.
10. Find the second-largest number in a list (no `sort` allowed? or with it — your choice).
11. Build a dict mapping 1–10 to their squares. Print only even-key squares.
12. Count how many times each word appears in a sentence (return a dict).
13. Given two sets, print their union, intersection, difference, and symmetric difference.
14. Print the numbers 1–50, but "Fizz" for multiples of 3, "Buzz" for 5, "FizzBuzz" for 15.
15. Print the Fibonacci sequence up to a user limit using a loop.
16. Write `is_prime(n)` and print all primes below 50.
17. Write `sum_digits(number)` that sums the digits of e.g. `1234 -> 10`.
18. Write a recursive `power(base, exp)`.
19. Write `countdown(n)` recursively, then iteratively.
20. Write a function that returns both the min and the max of a list.
21. Save 5 random numbers to a file, read them back, and print their sum.
22. Read a text file and print the number of lines and total words.
23. Read a file backwards (last line first).
24. Create a JSON file holding 3 people with name/age/skills and load it.
25. Create class `Movie` with title, year, rating. Print a formatted "Best of" list.
26. Make `BankAccount` print the balance in a friendly way using `__str__`.
27. Make `Temperature` with `to_celsius` / `to_fahrenheit` methods and `__eq__`.
28. Create `ShapeArea` using inheritance for circle, rectangle, triangle.
29. Use a class attribute to count how many objects of that class were created.
30. Write a program that reads a CSV-ish text file and prints a small table using functions and loops.

---

## 11. Beginner Project: Student Database Manager

A complete mini-project combining **variables, data types, strings, conditionals, lists,
dictionaries, sets, tuples, loops, functions, file I/O, JSON, and OOP**.

Run this file; it manages a small student database with a text menu.

```python
import json

DATA_FILE = "students.json"


class Student:
    def __init__(self, name, grade, subject):
        self.name = name
        self.grade = grade            # int 0-100
        self.subject = subject

    def is_passing(self):
        return self.grade >= 40

    def to_dict(self):
        return {"name": self.name, "grade": self.grade, "subject": self.subject}

    def __str__(self):
        status = "passing" if self.is_passing() else "failing"
        return f"{self.name:12} {self.subject:12} {self.grade:3}  {status}"


def load_students():
    try:
        with open(DATA_FILE, "r") as f:
            raw = json.load(f)
    except FileNotFoundError:
        return []
    return [Student(**item) for item in raw]        # **item = keyword unpacking


def save_students(students):
    with open(DATA_FILE, "w") as f:
        json.dump([s.to_dict() for s in students], f, indent=2)


def add_student(students):
    name = input("Name: ").strip()
    subject = input("Subject: ").strip()
    while True:
        try:
            grade = int(input("Grade (0-100): "))
            if 0 <= grade <= 100:
                break
            print("Grade must be 0-100.")
        except ValueError:
            print("Please enter a number.")
    students.append(Student(name, grade, subject))
    save_students(students)
    print(f"Added {name}.\n")


def show_report(students):
    if not students:
        print("No students yet. Add some first!\n")
        return

    print(f"\n{'Name':12} {'Subject':12} {'Grade':3}  Status")
    print("-" * 45)
    for s in students:
        print(s)

    passing = [s for s in students if s.is_passing()]
    subjects = {s.subject for s in students}          # set: unique subjects
    passed_subjects = {s.subject for s in passing}

    print("-" * 45)
    print(f"Total students: {len(students)}")
    print(f"Passing: {len(passing)} ({len(passing) / max(len(students), 1) * 100:.1f}%)")
    print(f"Unique subjects: {subjects}")
    print(f"Subjects with passing students: {passed_subjects}\n")


def best_student(students):
    if not students:
        print("No data available.\n")
        return
    top = max(students, key=lambda s: s.grade)        # higher-order function
    print(f"Top student: {top.name} in {top.subject} with {top.grade}%\n")


def main():
    students = load_students()
    print("=== Student Database Manager ===")
    while True:
        print("1) Add student")
        print("2) Show report")
        print("3) Show top student")
        print("4) Quit")
        choice = input("Choose: ").strip()

        if choice == "1":
            add_student(students)
        elif choice == "2":
            show_report(students)
        elif choice == "3":
            best_student(students)
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Unknown choice. Try again.\n")


if __name__ == "__main__":
    main()
```

### How it brings everything together

| Concept used        | Where in the project                          |
|---------------------|-----------------------------------------------|
| Variables/types     | `name`, `grade`, `status` strings             |
| Conditionals        | `is_passing`, input validation, menu logic    |
| Collections         | `students` list, tuples from `json`, `sets`   |
| Loops               | `while` menu, `for` printing, comprehensions  |
| Functions           | `load`, `save`, `add`, `report`, `best`       |
| File I/O / JSON     | saving & loading `students.json`              |
| OOP                 | `Student` class with `__init__`, methods, `__str__` |
| List comprehension  | `[Student(**item) for item in raw]`, `passing`|

### How to try it

1. Save the code as `students_manager.py`.
2. Run it: `python students_manager.py`
3. Add a few students, view the report, quit, then re-run — the data persists in
   `students.json` because of file I/O + JSON.

---

*End of Python Part-1. You now have the fundamentals: values, logic, collections, loops,
functions, files, and OOP — enough to start building real programs. Good luck and keep
coding!*