# Python Part 2 — Lists and Tuples (Deep Dive)

> An in-depth, beginner-friendly guide to Python's two most important sequence types:
> **lists** (mutable) and **tuples** (immutable). Learn creation, indexing, slicing,
> methods, comprehensions, unpacking, copying, sorting, performance, and when to prefer
> one over the other — all with runnable, practical examples.

---

## Table of Contents

1. [Lists — The Basics](#1-lists--the-basics)
2. [Building Lists](#2-building-lists)
3. [Indexing, Slicing, and Stepping](#3-indexing-slicing-and-stepping)
4. [Adding and Removing Elements](#4-adding-and-removing-elements)
5. [List Methods in Detail](#5-list-methods-in-detail)
6. [Searching, Sorting, and Comparing](#6-searching-sorting-and-comparing)
7. [Copying Lists and Aliasing](#7-copying-lists-and-aliasing)
8. [Iterating, Unpacking, and `enumerate`](#8-iterating-unpacking-and-enumerate)
9. [Nested Lists and Matrices](#9-nested-lists-and-matrices)
10. [List Comprehensions](#10-list-comprehensions)
11. [Tuples — The Basics](#11-tuples--the-basics)
12. [Tuple Operations and Methods](#12-tuple-operations-and-methods)
13. [Why Tuples Exist: Immutability](#13-why-tuples-exist-immutability)
14. [Named Tuples](#14-named-tuples)
15. [Lists vs Tuples — Side by Side](#15-lists-vs-tuples--side-by-side)
16. [Common Mistakes and Gotchas](#16-common-mistakes-and-gotchas)
17. [Performance Notes](#17-performance-notes)
18. [Key Takeaways](#18-key-takeaways)
19. [Practice Exercises](#19-practice-exercises)
20. [Mini Project: Shopping Cart with Lists](#20-mini-project-shopping-cart-with-lists)

---

# 1. Lists — The Basics

## 1.1 What is a list?

A **list** is an **ordered**, **changeable** (**mutable**) collection of items, written in
square brackets `[]`. The order matters: the first item you add is at index `0`.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)
```

**Output:**
```
['apple', 'banana', 'cherry']
```

Key facts:
- Lists can hold **any type**: integers, floats, strings, booleans, and even other lists.
- A single list can mix types freely.
- Lists are **mutable** — you can add, remove, and change items after creation.

## 1.2 Lists can hold mixed types

```python
mixed = [1, "hello", 3.14, True, None, [10, 20]]
print(mixed)

print(len(mixed))     # number of items
print(type(mixed))    # it's a list
```

**Output:**
```
[1, 'hello', 3.14, True, None, [10, 20]]
6
<class 'list'>
```

## 1.3 The empty list

An empty list contains nothing. You'll often start with one and fill it in a loop.

```python
empty1 = []
empty2 = list()       # the list() constructor

print(empty1)
print(empty2)
print(len(empty1))    # 0
print([] == list())   # True — they are equal
```

**Output:**
```
[]
[]
0
True
```

## 1.4 Creating lists from other data with `list()`

The `list()` constructor converts iterables (strings, tuples, ranges, dict keys) into lists.

```python
from_str = list("abc")
print(from_str)                 # ['a', 'b', 'c']

from_tuple = list((1, 2, 3))
print(from_tuple)               # [1, 2, 3]

from_range = list(range(5))
print(from_range)               # [0, 1, 2, 3, 4]

from_dict = list({"name": "Ana", "age": 25})
print(from_dict)                # ['name', 'age']  -> keys only
```

**Output:**
```
['a', 'b', 'c']
[1, 2, 3]
[0, 1, 2, 3, 4]
['name', 'age']
```

---

# 2. Building Lists

## 2.1 The `list()` constructor

```python
nums = list(range(10, 16))
print(nums)   # [10, 11, 12, 13, 14, 15]
```

**Output:**
```
[10, 11, 12, 13, 14, 15]
```

## 2.2 Repeating lists with `*`

Multiplication repeats a list. (Beware: it repeats the **same objects** — see the gotcha
section later for nested lists.)

```python
base = ["a", "b"]
repeated = base * 3
print(repeated)

zeros = [0] * 5
print(zeros)
```

**Output:**
```
['a', 'b', 'a', 'b', 'a', 'b']
[0, 0, 0, 0, 0]
```

## 2.3 Combining lists with `+`

Concatenation builds a brand-new list (neither input is modified).

```python
a = [1, 2]
b = [3, 4]
c = a + b
print(c)

print(a, b)          # originals unchanged
```

**Output:**
```
[1, 2, 3, 4]
[1, 2] [3, 4]
```

## 2.4 Getting user input into a list

A classic pattern: keep asking until the user enters "done".

```python
items = []
while True:
    value = input("Enter a number (or 'done' to stop): ")
    if value == "done":
        break
    items.append(int(value))

print("You entered:", items)
print("Sum:", sum(items))
```

> `input()` always returns a string, so convert with `int(value)` when you need numbers.

## 2.5 The `range()` trick for sequential lists

```python
evens = list(range(0, 20, 2))
print(evens)                      # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

descending = list(range(10, 0, -1))
print(descending)                 # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

**Output:**
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

---

# 3. Indexing, Slicing, and Stepping

## 3.1 Positive and negative indexing

Index `0` is the first element; negative indices count from the end, starting at `-1`.

```python
nums = [10, 20, 30, 40]

#  index:  0    1    2    3
#  neg:   -4   -3   -2   -1

print(nums[0])     # 10
print(nums[3])     # 40
print(nums[-1])    # 40  (last)
print(nums[-2])    # 30
```

**Output:**
```
10
40
40
30
```

## 3.2 IndexError — going out of range

```python
nums = [10, 20, 30]
# print(nums[3])    # IndexError: list index out of range
# print(nums[-4])   # IndexError
```

**Output:**
```
(no output — the commented lines would crash the program)
```

Always check `len()` or use a loop when you're unsure how many items there are.

## 3.3 Slicing basics

`lst[start:stop]` — includes `start`, **excludes** `stop`.

```python
nums = [0, 1, 2, 3, 4, 5]

print(nums[2:5])    # [2, 3, 4]
print(nums[:3])     # [0, 1, 2]     (from the start)
print(nums[3:])     # [3, 4, 5]     (to the end)
print(nums[:])      # full copy
```

**Output:**
```
[2, 3, 4]
[0, 1, 2]
[3, 4, 5]
[0, 1, 2, 3, 4, 5]
```

## 3.4 Slicing with a step

`lst[start:stop:step]` — take every `step`-th element.

```python
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(nums[::2])     # [0, 2, 4, 6, 8]     every second
print(nums[1::2])    # [1, 3, 5, 7, 9]     odds
print(nums[::3])     # [0, 3, 6, 9]
print(nums[::-1])    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]  reversed!
```

**Output:**
```
[0, 2, 4, 6, 8]
[1, 3, 5, 7, 9]
[0, 3, 6, 9]
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

## 3.5 Slice with negative step (reversing)

```python
word = ["p", "y", "t", "h", "o", "n"]

print(word[::-2])    # ['n', 'h', 'y']  (right to left, every 2)
print(word[5:1:-1])  # ['n', 'o', 't', 'h']
print(word[3:0:-1])  # ['h', 't', 'y']
```

**Output:**
```
['n', 'h', 'y']
['n', 'o', 't', 'h']
['h', 't', 'y']
```

## 3.6 Slicing is safe with out-of-range bounds

Unlike a single index, a slice will not crash — it just clips to the list.

```python
nums = [1, 2, 3]

print(nums[0:99])     # [1, 2, 3]
print(nums[99:])      # []
print(nums[-99:3])    # [1, 2, 3]
```

**Output:**
```
[1, 2, 3]
[]
[1, 2, 3]
```

## 3.7 Assigning to a slice

You can replace a whole slice with new values in one step.

```python
nums = [1, 2, 3, 4, 5]

nums[1:4] = [20, 30, 40]     # replace middle three
print(nums)                  # [1, 20, 30, 40, 5]

nums[1:3] = [0, 0, 0, 0]     # replace two with four (size changes!)
print(nums)

nums[0:2] = []               # delete a slice
print(nums)
```

**Output:**
```
[1, 20, 30, 40, 5]
[1, 0, 0, 0, 0, 0, 40, 5]
[0, 0, 0, 0, 0, 40, 5]
```

---

# 4. Adding and Removing Elements

## 4.1 `append()` — add to the end

```python
cart = []
cart.append("shirt")
cart.append("shoes")
print(cart)
```

**Output:**
```
['shirt', 'shoes']
```

`append()` takes exactly **one** argument. To add many, use `extend()` or a loop.

```python
cart.append(["hat", "belt"])   # adds the list AS ONE item
print(cart)
```

**Output:**
```
['shirt', 'shoes', ['hat', 'belt']]
```

## 4.2 `insert()` — add at a specific position

```python
nums = [1, 2, 3]
nums.insert(0, 99)      # front
print(nums)

nums.insert(2, 50)      # middle
print(nums)

nums.insert(99, 7)      # too big -> appends to the end
print(nums)
```

**Output:**
```
[99, 1, 2, 3]
[99, 1, 50, 2, 3]
[99, 1, 50, 2, 3, 7]
```

## 4.3 `extend()` — add many items at once

```python
a = [1, 2]
b = [3, 4, 5]

a.extend(b)      # same as a = a + b but modifies a in place
print(a)

a.extend("xy")   # strings are iterables -> adds each character
print(a)
```

**Output:**
```
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 'x', 'y']
```

> `+` makes a new list. `extend()` changes the original. Use `extend()` inside a loop for
> better performance.

## 4.4 `remove()` — remove by value

Removes the **first** matching item. Raises `ValueError` if the value is not present.

```python
nums = [5, 2, 9, 2, 7]

nums.remove(2)      # removes the FIRST 2 only
print(nums)         # [5, 9, 2, 7]

nums.remove(999)    # ValueError: list.remove(x): x not in list
```

**Output:**
```
[5, 9, 2, 7]
```
*(the program would crash on the last line)*

Safe pattern — check first, or catch the error:

```python
nums = [5, 2, 9]
value = 999

if value in nums:
    nums.remove(value)
else:
    print(f"{value} not found")
```

**Output:**
```
999 not found
```

## 4.5 `pop()` — remove and return by index

`pop()` with **no argument** removes the last item. `pop(i)` removes item at index `i`.
Both **return** the removed value.

```python
nums = [10, 20, 30, 40]

last = nums.pop()        # removes 40
print(last, nums)

second = nums.pop(1)     # removes 20
print(second, nums)

# nums.pop(99)           # IndexError
```

**Output:**
```
40 [10, 20, 30]
20 [10, 30]
```

## 4.6 `del` — delete by index or slice

`del` is a statement, not a method. It removes without returning anything.

```python
nums = [10, 20, 30, 40, 50]

del nums[0]
print(nums)         # [20, 30, 40, 50]

del nums[1:3]       # delete a slice
print(nums)         # [20, 50]

del nums            # deletes the whole variable
# print(nums)       # NameError: name 'nums' is not defined
```

**Output:**
```
[20, 30, 40, 50]
[20, 50]
```

## 4.7 `clear()` — empty the list, keep the variable

```python
nums = [1, 2, 3]
print("before:", nums, len(nums))

nums.clear()
print("after:", nums, len(nums))
```

**Output:**
```
before: [1, 2, 3] 3
after: [] 0
```

---

# 5. List Methods in Detail

## 5.1 Full method reference

| Method            | Does                                                | Returns        |
|-------------------|-----------------------------------------------------|----------------|
| `append(x)`       | Add `x` at the end                                  | `None`         |
| `insert(i, x)`    | Insert `x` at index `i`                             | `None`         |
| `extend(iter)`    | Add all items of an iterable                        | `None`         |
| `remove(x)`       | Remove first `x` (ValueError if absent)             | `None`         |
| `pop([i])`        | Remove & return item at `i` (default last)          | removed item  |
| `clear()`         | Remove every item                                   | `None`         |
| `index(x, [s],[e])` | Index of first `x` (optional start/end)          | integer       |
| `count(x)`        | How many times `x` appears                          | integer       |
| `sort(key, rev)`  | Sort in place                                       | `None`         |
| `reverse()`       | Reverse in place                                    | `None`         |
| `copy()`          | Return a shallow copy                               | new list      |

Almost all mutating methods return `None`. If you `print` them you'll see `None`.

```python
nums = [3, 1, 2]
result = nums.sort()
print(result)        # None !
print(nums)          # [1, 2, 3]
```

**Output:**
```
None
[1, 2, 3]
```

## 5.2 `index()` with start and end bounds

```python
colors = ["red", "green", "blue", "green", "yellow"]

print(colors.index("green"))          # 1  (first match)
print(colors.index("green", 2))       # 3  (search from index 2)
# print(colors.index("purple"))       # ValueError
```

**Output:**
```
1
3
```

## 5.3 `count()`

```python
votes = ["yes", "no", "yes", "yes", "maybe"]
print(votes.count("yes"))     # 3
print(votes.count("maybe"))   # 1
print(votes.count("x"))       # 0
```

**Output:**
```
3
1
0
```

## 5.4 `enumerate` and methods working together

```python
scores = [50, 80, 90, 60]

for i, score in enumerate(scores):
    mark = "pass" if score >= 60 else "fail"
    print(i, score, mark)
```

**Output:**
```
0 50 fail
1 80 pass
2 90 pass
3 60 pass
```

---

# 6. Searching, Sorting, and Comparing

## 6.1 Membership with `in` and `not in`

```python
fruits = ["apple", "banana", "cherry"]

print("banana" in fruits)        # True
print("grape" in fruits)         # False
print("grape" not in fruits)     # True
```

**Output:**
```
True
False
True
```

## 6.2 Sorting with `sort()` (in place) vs `sorted()` (new list)

```python
nums = [5, 2, 8, 1]

nums.sort()        # modifies the original
print(nums)

scrambled = [9, 1, 6]
ordered = sorted(scrambled)      # leaves original alone
print(scrambled)
print(ordered)
```

**Output:**
```
[1, 2, 5, 8]
[9, 1, 6]
[1, 6, 9]
```

## 6.3 Reverse sorting

```python
nums = [5, 2, 8, 1]

nums.sort(reverse=True)
print(nums)                      # [8, 5, 2, 1]

print(sorted([3, 1, 2], reverse=True))   # [3, 2, 1]
```

**Output:**
```
[8, 5, 2, 1]
[3, 2, 1]
```

## 6.4 Sorting strings — case sensitivity

Capital letters sort before lowercase ones (by ASCII/Unicode code point).

```python
words = ["banana", "Apple", "cherry"]
words.sort()
print(words)          # ['Apple', 'banana', 'cherry']

words.sort(key=str.lower)
print(words)          # ['Apple', 'banana', 'cherry']  (case-insensitive)
```

**Output:**
```
['Apple', 'banana', 'cherry']
['Apple', 'banana', 'cherry']
```

## 6.5 Sorting with a custom key

Sort by length, by a map, or by any function.

```python
words = ["cat", "elephant", "dog", "hippopotamus"]
words.sort(key=len)
print(words)          # shortest → longest

people = [("Ana", 30), ("Bob", 20), ("Eve", 25)]
people.sort(key=lambda person: person[1])
print(people)         # sorted by age
```

**Output:**
```
['cat', 'dog', 'elephant', 'hippopotamus']
[('Bob', 20), ('Eve', 25), ('Ana', 30)]
```

## 6.6 `reverse()` and `reversed()`

- `list.reverse()` — reverse **in place**, returns `None`.
- `reversed(list)` — returns a lightweight iterator; wrap with `list()` to get a list.

```python
nums = [1, 2, 3, 4]
nums.reverse()
print(nums)                     # [4, 3, 2, 1]

nums2 = [1, 2, 3, 4]
print(list(reversed(nums2)))    # [4, 3, 2, 1]
print(nums2)                    # untouched
```

**Output:**
```
[4, 3, 2, 1]
[4, 3, 2, 1]
[1, 2, 3, 4]
```

## 6.7 Min, max, sum

```python
nums = [4, 7, 1, 9, 3]

print(min(nums))     # 1
print(max(nums))     # 9
print(sum(nums))     # 24
print(sum(nums) / len(nums))   # average = 4.8
```

**Output:**
```
1
9
24
4.8
```

## 6.8 Comparing lists

Lists compare element by element (like words in a dictionary).

```python
print([1, 2, 3] == [1, 2, 3])    # True
print([1, 2, 3] == [3, 2, 1])    # False — order matters
print([1, 2, 3] == [1, 2])       # False — lengths differ

print([1, 10] < [2, 1])          # True: 1 < 2
print([1, 2, 3] < [1, 2, 4])     # True: 3 < 4
```

**Output:**
```
True
False
False
True
True
```

---

# 7. Copying Lists and Aliasing

## 7.1 Aliasing: two names, one list

Assignment `b = a` does **not** copy the list — both variables point to the **same** object.

```python
a = [1, 2, 3]
b = a            # b is ANOTHER NAME for the same list

b.append(4)
print(a)         # a also changed! (a may surprise you if you forgot)
print(a is b)    # True — same object
```

**Output:**
```
[1, 2, 3, 4]
True
```

## 7.2 True copies: `copy()`, `list()`, slicing

Use these when you want an independent duplicate.

```python
a = [1, 2, 3]

c1 = a.copy()        # method
c2 = list(a)         # constructor
c3 = a[:]            # full slice

c1.append(99)

print(a)   # [1, 2, 3] — unchanged
print(c1)  # [1, 2, 3, 99]
print(c2, c3)
```

**Output:**
```
[1, 2, 3]
[1, 2, 3, 99]
[1, 2, 3] [1, 2, 3]
```

## 7.3 Shallow vs deep copy — the nested-list catch

A regular copy (`copy()`, `list()`, `[:]`) is **shallow**: nested lists are **shared**.

```python
inner = [1, 2]
matrix = [inner, [3, 4]]

shallow = matrix.copy()
shallow[0].append(999)      # modifies the SHARED inner list

print(matrix)               # [[1, 2, 999], [3, 4]]  -> changed!
print(shallow)              # also [[1, 2, 999], [3, 4]]
```

**Output:**
```
[[1, 2, 999], [3, 4]]
[[1, 2, 999], [3, 4]]
```

For fully independent nested lists, use `copy.deepcopy`.

```python
import copy

inner = [1, 2]
matrix = [inner, [3, 4]]

deep = copy.deepcopy(matrix)
deep[0].append(999)

print(matrix)     # [[1, 2], [3, 4]]  — original untouched
print(deep)       # [[1, 2, 999], [3, 4]]
```

**Output:**
```
[[1, 2], [3, 4]]
[[1, 2, 999], [3, 4]]
```

## 7.4 The `[x] * n` trap for nested lists

`[[]] * n` does **not** create n independent lists — it repeats the same inner list.

```python
rows = [[]] * 3
print(rows)          # [[], [], []]

rows[0].append("x")  # appends to the ONE shared inner list
print(rows)          # [['x'], ['x'], ['x']]  — surprise!
```

**Output:**
```
[[], [], []]
[['x'], ['x'], ['x']]
```

Correct way to build n independent lists:

```python
rows = [[] for _ in range(3)]
rows[0].append("x")
print(rows)          # [['x'], [], []]
```

**Output:**
```
[['x'], [], []]
```

---

# 8. Iterating, Unpacking, and `enumerate`

## 8.1 The basic loop

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(f"eat {fruit}")
```

**Output:**
```
eat apple
eat banana
eat cherry
```

## 8.2 Looping by index with `range(len(...))`

```python
fruits = ["apple", "banana", "cherry"]
for i in range(len(fruits)):
    print(i, fruits[i])
```

**Output:**
```
0 apple
1 banana
2 cherry
```

## 8.3 `enumerate()` — index and value together

`enumerate` is cleaner and faster than `range(len(...))`.

```python
fruits = ["apple", "banana", "cherry"]
for i, fruit in enumerate(fruits, start=1):
    print(f"{i}. {fruit}")
```

**Output:**
```
1. apple
2. banana
3. cherry
```

## 8.4 Iterating two lists at once with `zip()`

```python
names = ["Ana", "Bob", "Eve"]
ages = [25, 30, 28]

for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

**Output:**
```
Ana is 25
Bob is 30
Eve is 28
```

`zip()` stops at the shortest list.

```python
short = [1, 2]
long = [10, 20, 30, 40]
print(list(zip(short, long)))   # [(1, 10), (2, 20)]
```

**Output:**
```
[(1, 10), (2, 20)]
```

## 8.5 List unpacking

```python
coords = [3, 7]
x, y = coords
print(x, y)             # 3 7

first, second, third = [10, 20, 30]
print(first, second, third)
```

**Output:**
```
3 7
10 20 30
```

## 8.6 Advanced unpacking with `*`

The starred name collects "the rest".

```python
nums = [1, 2, 3, 4, 5]

head, *tail = nums
print(head, tail)        # 1 [2, 3, 4, 5]

first, *middle, last = nums
print(first, middle, last)   # 1 [2, 3, 4] 5

*all_items, final = nums
print(all_items, final)      # [1, 2, 3, 4] 5
```

**Output:**
```
1 [2, 3, 4, 5]
1 [2, 3, 4] 5
[1, 2, 3, 4] 5
```

## 8.7 Swapping two values

Python makes swapping trivial.

```python
a, b = 5, 9
a, b = b, a
print(a, b)      # 9 5

lst = [1, 2, 3]
lst[0], lst[2] = lst[2], lst[0]
print(lst)       # [3, 2, 1]
```

**Output:**
```
9 5
[3, 2, 1]
```

## 8.8 Converting between lists and other types

```python
s = "hello"
print(list(s))                     # ['h', 'e', 'l', 'l', 'o']

t = (1, 2, 3)
print(list(t))                     # [1, 2, 3]

d = {"a": 1, "b": 2}
print(list(d))                     # ['a', 'b']        keys
print(list(d.values()))            # [1, 2]            values
print(list(d.items()))             # [('a', 1), ('b', 2)]
```

**Output:**
```
['h', 'e', 'l', 'l', 'o']
[1, 2, 3]
['a', 'b']
[1, 2]
[('a', 1), ('b', 2)]
```

---

# 9. Nested Lists and Matrices

## 9.1 Reading a matrix

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]

print(matrix[0])       # [1, 2, 3]        (first row)
print(matrix[2][1])    # 8                (row 2, column 1)
```

**Output:**
```
[1, 2, 3]
8
```

## 9.2 Editing a matrix

```python
matrix = [[1, 2], [3, 4]]

matrix[1][0] = 99
print(matrix)          # [[1, 2], [99, 4]]

matrix.append([5, 6])  # add a row
print(matrix)
```

**Output:**
```
[[1, 2], [99, 4]]
[[1, 2], [99, 4], [5, 6]]
```

## 9.3 Printing a matrix row by row

```python
matrix = [[1, 2, 3], [4, 5, 6]]

for row in matrix:
    for cell in row:
        print(cell, end=" ")
    print()
```

**Output:**
```
1 2 3
4 5 6
```

## 9.4 Building matrices with comprehensions

```python
rows, cols = 3, 3
matrix = [[0] * cols for _ in range(rows)]
print(matrix)          # [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

identity = [[1 if r == c else 0 for c in range(3)] for r in range(3)]
print(identity)
```

**Output:**
```
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
[[1, 0, 0], [0, 1, 0], [0, 0, 1]]
```

## 9.5 Flattening a nested list

```python
nested = [[1, 2], [3, 4, 5], [6]]

flat = [num for row in nested for num in row]
print(flat)   # [1, 2, 3, 4, 5, 6]
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
```

---

# 10. List Comprehensions

## 10.1 The basic pattern

```
[expression for item in iterable if condition]
```

```python
squares = [n ** 2 for n in range(6)]
print(squares)                  # [0, 1, 4, 9, 16, 25]
```

**Output:**
```
[0, 1, 4, 9, 16, 25]
```

## 10.2 With a condition

```python
evens = [n for n in range(1, 21) if n % 2 == 0]
print(evens)
```

**Output:**
```
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

## 10.3 Transforming values

```python
words = ["cat", "dog", "elephant"]
lengths = [len(w) for w in words]
print(lengths)                       # [3, 3, 8]

uppercase = [w.upper() for w in words]
print(uppercase)                     # ['CAT', 'DOG', 'ELEPHANT']

temps_c = [0, 10, 20, 30]
temps_f = [c * 9 / 5 + 32 for c in temps_c]
print(temps_f)                       # [32.0, 50.0, 68.0, 86.0]
```

**Output:**
```
[3, 3, 8]
['CAT', 'DOG', 'ELEPHANT']
[32.0, 50.0, 68.0, 86.0]
```

## 10.4 `if`-`else` inside a comprehension

Put the conditional **before** the loop when you need both branches.

```python
nums = [-3, 5, -1, 8, -2]
labeled = ["pos" if n > 0 else "neg" for n in nums]
print(labeled)                      # ['neg', 'pos', 'neg', 'pos', 'neg']
```

**Output:**
```
['neg', 'pos', 'neg', 'pos', 'neg']
```

## 10.5 Nested loops in a comprehension

```python
pairs = [(a, b) for a in "XY" for b in "12"]
print(pairs)
# [('X', '1'), ('X', '2'), ('Y', '1'), ('Y', '2')]
```

**Output:**
```
[('X', '1'), ('X', '2'), ('Y', '1'), ('Y', '2')]
```

## 10.6 Comprehension vs loop — same result, less code

```python
# With a loop
result = []
for n in range(10):
    if n % 2 == 0:
        result.append(n ** 2)

# With a comprehension
result = [n ** 2 for n in range(10) if n % 2 == 0]

print(result)   # [0, 4, 16, 36, 64]
```

**Output:**
```
[0, 4, 16, 36, 64]
```

---

# 11. Tuples — The Basics

## 11.1 What is a tuple?

A **tuple** is an **ordered**, **immutable** (unchangeable) collection in round brackets `()`.
Once created, you cannot add, remove, or change items.

```python
point = (3, 7)
print(point)
print(type(point))     # <class 'tuple'>
```

**Output:**
```
(3, 7)
<class 'tuple'>
```

## 11.2 The comma makes a tuple, not the brackets

```python
a = (5)          # int  (just a number in brackets!)
b = (5,)         # tuple (comma makes it a tuple)
c = 5,           # tuple, brackets optional
d = 1, 2, 3      # tuple, brackets optional

print(a, type(a))
print(b, type(b))
print(c, type(c))
print(d, type(d))
```

**Output:**
```
5 <class 'int'>
(5,) <class 'tuple'>
(5,) <class 'tuple'>
(1, 2, 3) <class 'tuple'>
```

## 11.3 The one-item tuple — trailing comma is REQUIRED

Without the comma, `(5)` is just `5`. With the comma, you get a 1-item tuple.

```python
one = (5,)
print(one, len(one))     # (5,) 1

not_a_tuple = (5)
print(not_a_tuple, len(str(not_a_tuple)))   # it's an int!
```

**Output:**
```
(5,) 1
5 1
```

## 11.4 The empty tuple

```python
empty = ()
also = tuple()       # tuple() constructor
print(empty)
print(also)
print(len(empty))    # 0
```

**Output:**
```
()
()
0
```

## 11.5 Tuples from other data with `tuple()`

```python
print(tuple([1, 2, 3]))        # (1, 2, 3)
print(tuple("abc"))            # ('a', 'b', 'c')
print(tuple(range(4)))         # (0, 1, 2, 3)
print(tuple({"x": 1}))         # ('x',)  -> keys
```

**Output:**
```
(1, 2, 3)
('a', 'b', 'c')
(0, 1, 2, 3)
('x',)
```

## 11.6 Mixed types in tuples

```python
record = ("Nasa", 1969, ["apollo", "neil"])
print(record)
print(len(record))    # 3
```

**Output:**
```
('Nasa', 1969, ['apollo', 'neil'])
3
```

> Note: a tuple is immutable, but if it **contains** a list, that list itself is still
> mutable — you can't reassign the *slot* in the tuple, but you can modify the list inside.

```python
record = ("mission", [1, 2])
record[1].append(3)     # OK — the list inside can change
print(record)           # ('mission', [1, 2, 3])

# record[0] = "task"    # TypeError — can't reassign a slot
```

**Output:**
```
('mission', [1, 2, 3])
```

---

# 12. Tuple Operations and Methods

## 12.1 Indexing and slicing

Tuples support the **same** indexing and slicing as lists.

```python
t = (10, 20, 30, 40, 50)

print(t[0])        # 10
print(t[-1])       # 50
print(t[1:4])      # (20, 30, 40)
print(t[::2])      # (10, 30, 50)
print(t[::-1])     # (50, 40, 30, 20, 10)
```

**Output:**
```
10
50
(20, 30, 40)
(10, 30, 50)
(50, 40, 30, 20, 10)
```

## 12.2 Concatenation and repetition

These create **new** tuples; the originals are untouched.

```python
t1 = (1, 2)
t2 = (3, 4)

print(t1 + t2)       # (1, 2, 3, 4)
print(t1 * 3)        # (1, 2, 1, 2, 1, 2)
print(t1)            # still (1, 2)
```

**Output:**
```
(1, 2, 3, 4)
(1, 2, 1, 2, 1, 2)
(1, 2)
```

## 12.3 The only two methods: `count()` and `index()`

Tuples have no `append`, `remove`, `sort`, etc. — they can't change. They only support:

```python
t = (1, 2, 2, 3, 2)

print(t.count(2))     # 3
print(t.index(3))     # 3  (first position of 3)
print(t.index(2, 2))  # 2  (find 2 from index 2 onward)

# t.append(4)         # AttributeError: 'tuple' object has no attribute 'append'
```

**Output:**
```
3
3
2
```

## 12.4 Membership, length, min, max, sum

```python
t = (4, 9, 1, 7)

print(9 in t)       # True
print(10 in t)      # False
print(len(t))       # 4
print(min(t))       # 1
print(max(t))       # 9
print(sum(t))       # 21
```

**Output:**
```
True
False
4
1
9
21
```

## 12.5 Nested tuples

```python
grid = ((1, 2), (3, 4))
print(grid[1][0])      # 3

coords = ((0, 0), (1, 1), (2, 0))
for x, y in coords:
    print(f"x={x} y={y}")
```

**Output:**
```
3
x=0 y=0
x=1 y=1
x=2 y=0
```

## 12.6 Comparing tuples

```python
print((1, 2, 3) == (1, 2, 3))    # True
print((1, 2) == (2, 1))          # False — order matters
print((1, 2, 3) < (1, 2, 4))     # True
print((5, 1) > (4, 99))          # True — only 5 vs 4 is checked
```

**Output:**
```
True
False
True
True
```

## 12.7 Tuple comprehensions?

There's no "tuple comprehension". `(x for x in ...)` creates a **generator**, not a tuple.

```python
gen = (n ** 2 for n in range(4))
print(gen)                  # <generator object ...>

# If you really want a tuple, pass a comprehension/list to tuple():
t = tuple(n ** 2 for n in range(4))
print(t)                    # (0, 1, 4, 9)
```

**Output:**
```
<generator object gen at ...>  (address varies)
(0, 1, 4, 9)
```

---

# 13. Why Tuples Exist: Immutability

## 13.1 You cannot change a tuple

```python
t = (1, 2, 3)
# t[0] = 99      # TypeError: 'tuple' object does not support item assignment
# t.append(4)    # AttributeError
# del t[0]       # TypeError
print(t)
```

**Output:**
```
(1, 2, 3)
```

## 13.2 Why is immutability a feature?

1. **Safety** — you cannot accidentally modify shared data.
2. **Hashable** — tuples can be dictionary keys and set members (lists cannot).
3. **Faster** — smaller memory footprint and quick comparisons.
4. **Semantic clarity** — a tuple signals "this is fixed data".

```python
# A tuple works as a dict key:
moves = {(0, 0): "origin", (1, 1): "diagonal"}
print(moves[(1, 1)])

# A list does NOT:
# moves = {[0, 0]: "origin"}   # TypeError: unhashable type: 'list'
```

**Output:**
```
diagonal
```

Set membership:

```python
allowed = {(1, 2), (3, 4)}
print((1, 2) in allowed)     # True
print((9, 9) in allowed)     # False
```

**Output:**
```
True
False
```

## 13.3 Functions that return multiple values return a tuple

```python
def divmod_pair(a, b):
    return a // b, a % b      # the comma packs a tuple

pair = divmod_pair(17, 5)
print(pair, type(pair))       # (3, 2) <class 'tuple'>

q, r = divmod_pair(17, 5)     # unpack on the way back in
print(q, r)                   # 3 2
```

**Output:**
```
(3, 2) <class 'tuple'>
3 2
```

## 13.4 Swapping via tuple packing/unpacking

The right-hand side builds a tuple, then unpacks it into variables.

```python
a, b = 1, 2
a, b = b, a
print(a, b)     # 2 1
```

**Output:**
```
2 1
```

## 13.5 Tuple unpacking in depth

```python
coords = (3, 7)
x, y = coords
print(x, y)     # 3 7

record = ("Ana", 25, "Berlin")
name, age, city = record
print(name, age, city)     # Ana 25 Berlin

first, *rest = (10, 20, 30)
print(first, rest)         # 10 [20, 30]
```

**Output:**
```
3 7
Ana 25 Berlin
10 [20, 30]
```

> Need to ignore a value? Convention is to unpack it into `_`.

```python
name, _, city = ("Ana", 25, "Berlin")
print(name, city)     # Ana Berlin
```

**Output:**
```
Ana Berlin
```

## 13.6 Returning a value AND a status flag

A very common idiom — return `(result, ok)` or use an error code.

```python
def safe_divide(a, b):
    if b == 0:
        return None, False
    return a / b, True

result, ok = safe_divide(10, 2)
print(result, ok)     # 5.0 True

result, ok = safe_divide(10, 0)
print(result, ok)     # None False
```

**Output:**
```
5.0 True
None False
```

---

# 14. Named Tuples

## 14.1 What is a `namedtuple`?

A `namedtuple` is a tuple with **named fields** — you keep the benefits of a tuple (fixed,
immutable, lightweight) but can access items by name instead of index.

```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])

p = Point(3, 7)
print(p)             # Point(x=3, y=7)
print(p.x)           # 3  (access by name
print(p.y)           # 7
print(p[0])          # 3  (still indexable)
print(tuple(p))      # (3, 7)
```

**Output:**
```
Point(x=3, y=7)
3
7
3
(3, 7)
```

## 14.2 Real-world style example

```python
from collections import namedtuple

Student = namedtuple("Student", ["name", "grade", "city"])

s1 = Student("Ana", 85, "Berlin")
s2 = Student("Bob", 72, "Paris")

print(f"{s1.name} scored {s1.grade}")
print(f"{s2.name} scored {s2.grade}")

for student in (s1, s2):
    if student.grade >= 80:
        print(student.name, "distinction")
```

**Output:**
```
Ana scored 85
Bob scored 72
Ana distinction
```

## 14.3 Tuples vs namedtuples — a note

- Use a plain tuple for quick positional data (coordinates, function return values).
- Use a `namedtuple` when records have clear fields and you want readable code.

---

# 15. Lists vs Tuples — Side by Side

| Feature            | List                        | Tuple                        |
|--------------------|-----------------------------|------------------------------|
| Syntax             | `[1, 2, 3]`                 | `(1, 2, 3)`                  |
| Mutable?           | Yes                         | No                           |
| Size / speed       | Slightly larger & slower    | Smaller & faster             |
| Memory             | More (over-allocation)      | Less                         |
| Dict key / set item| No (unhashable)             | Yes (if hashable contents)   |
| Methods            | Rich (`append`, `sort`...)  | Only `count()`, `index()`    |
| Typical use        | Changing collections        | Fixed data, return values    |
| Iteration          | Allowed                     | Allowed                      |
| Can nest           | Yes                         | Yes                          |
| Unpacking          | Yes                         | Yes                          |

## 15.1 When to prefer a list

- The data will grow, shrink, or change (to-do lists, shopping carts, appending results).
- You need to sort, reverse, or pop.
- You collect items while looping.

```python
results = []
for n in range(5):
    results.append(n * 2)
print(results)     # [0, 2, 4, 6, 8]
```

**Output:**
```
[0, 2, 4, 6, 8]
```

## 15.2 When to prefer a tuple

- The data is fixed (co-ordinates, RGB color, days of the week).
- You need a dict key / set member.
- You return multiple values from a function.

```python
DAYS = ("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
RGB_RED = (255, 0, 0)

print(DAYS[0], RGB_RED)
```

**Output:**
```
Mon (255, 0, 0)
```

## 15.3 Performance comparison

Tuples are slightly cheaper to create and iterate. Let's measure with `timeit`.

```python
import timeit

list_time = timeit.timeit("[1, 2, 3, 4, 5] + [6, 7, 8, 9, 10]", number=1_000_000)
tuple_time = timeit.timeit("(1, 2, 3, 4, 5) + (6, 7, 8, 9, 10)", number=1_000_000)

print(f"list : {list_time:.4f}s")
print(f"tuple: {tuple_time:.4f}s")
```

**Output:**
```
(the exact numbers vary by machine, but the tuple is consistently a little faster)
```

> Rule of thumb: the difference is rarely important unless you build millions of objects.
> Pick the type that communicates intent — readability beats micro-optimization.

---

# 16. Common Mistakes and Gotchas

## 16.1 `(5)` is an int, not a tuple

```python
wrong = (5)
print(type(wrong))    # <class 'int'>

right = (5,)
print(type(right))    # <class 'tuple'>
```

**Output:**
```
<class 'int'>
<class 'tuple'>
```

## 16.2 Trying to modify a tuple

```python
t = (1, 2)
# t[0] = 99    # TypeError: 'tuple' object does not support item assignment
```

## 16.3 `sort()` returns `None`

```python
nums = [3, 1, 2]
result = nums.sort()
print(result)     # None !
print(nums)       # [1, 2, 3]
```

**Output:**
```
None
[1, 2, 3]
```

## 16.4 Mutating a list while iterating over it

Removing items inside a for-loop can skip elements.

```python
nums = [1, 2, 3, 4, 5]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)
print(nums)          # [1, 3, 5] accidentally right… but:

nums = [2, 2, 4, 2]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)
print(nums)          # [2]  ← wrong! 2 is left behind
```

**Output:**
```
[1, 3, 5]
[2]
```

Safe alternatives — iterate over a copy, or build a new list:

```python
nums = [2, 2, 4, 2]

# Option A: iterate over a copy
for n in nums[:]:
    if n % 2 == 0:
        nums.remove(n)
print(nums)          # []

# Option B: comprehension (cleanest)
nums = [2, 2, 4, 2]
nums = [n for n in nums if n % 2 != 0]
print(nums)          # []
```

**Output:**
```
[]
[]
```

## 16.5 Aliasing confusion

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)          # [1, 2, 3, 4]  — shared!
```

**Output:**
```
[1, 2, 3, 4]
```

Fix: `b = a.copy()` when you need independence.

## 16.6 The `[[]] * n` mistake

```python
rows = [[]] * 3
rows[0].append("x")
print(rows)       # [['x'], ['x'], ['x']]
```

**Output:**
```
[['x'], ['x'], ['x']]
```

## 16.7 Shallow copies with nested lists

```python
a = [[1, 2], [3]]
b = a.copy()
b[0].append(99)
print(a)          # [[1, 2, 99], [3]]  — inner list shared
```

**Output:**
```
[[1, 2, 99], [3]]
```

## 16.8 `sort()` on mixed types fails

```python
# [1, "two", 3.0].sort()   # TypeError: '<' not supported between 'str' and 'int'
```

## 16.9 Forgetting that indexing starts at 0

Off-by-one errors are the most common list bug:

```python
nums = [10, 20, 30]
print(nums[0])     # first
print(nums[-1])    # last — use -1, NOT len(nums)
```

**Output:**
```
10
30
```

## 16.10 Modifying the list size while using indices

```python
nums = [1, 2, 3, 4]
total = len(nums)
for i in range(total):
    if nums[i] % 2 == 0:      # IndexError after nums shrinks below i
        nums.remove(nums[i])
```

**Output:**
```
(IndexError: list index out of range — prefer comprehension-based removal)
```

---

# 17. Performance Notes

## 17.1 Flat lists — lookup by index is O(1)

Getting `lst[i]` by index is instant, no matter the list size.

```python
import time
big = list(range(10_000_000))

start = time.perf_counter()
x = big[-1]
print(f"index lookup: {time.perf_counter() - start:.6f}s")
```

## 17.2 `in` on a list is O(n) — scans item by item

```python
big = list(range(10_000_000))
print(10_000 in big)      # True — scans ~10k elements
print(9_500_000 in big)   # True — scans millions
```

> For heavy membership testing, use a `set` instead of a list.
> Note: insertion/removal at the START of a list (`insert(0, ...)`, `pop(0)`) is O(n)
> because every element shifts. Append/pop at the END is O(1) (amortized).

## 17.3 `append()` at the end is fast (amortized O(1))

```python
nums = []
for i in range(100_000):
    nums.append(i)      # fine
print(len(nums))
```

**Output:**
```
100000
```

## 17.4 `insert(0, ...)` and `pop(0)` are slow (O(n))

Prefer `append`/`pop` at the end, or use `collections.deque` for a true queue.

```python
from collections import deque

d = deque([1, 2, 3])
d.appendleft(0)      # O(1)
d.append(4)          # O(1)
print(list(d))       # [0, 1, 2, 3, 4]
```

**Output:**
```
[0, 1, 2, 3, 4]
```

## 17.5 Lists overallocate; tuples don't

A list reserves extra space so appends are cheap. A tuple stores exactly its items.
That's why tuples are smaller.

```python
import sys

lst = [1, 2, 3, 4]
tup = (1, 2, 3, 4)

print(f"list size  : {sys.getsizeof(lst)} bytes")
print(f"tuple size : {sys.getsizeof(tup)} bytes")
```

**Output:**
```
list size  : 120 bytes
tuple size : 72 bytes
```
*(numbers vary by Python version/platform — the tuple is always smaller)*

---

# 18. Key Takeaways

- **Lists** are ordered, mutable, mixed-type collections written with `[]`. ✔
- **Tuples** are ordered, immutable collections written with `()`. The **comma**, not the
  brackets, makes a tuple — `(5,)` vs `(5)`. ✔
- Indexing, slicing, concatenation, repetition, membership, and unpacking work for both. ✔
- Use `append`/`pop` (end of list) for speed; avoid `insert(0, ...)`/`pop(0)` in hot loops. ✔
- `b = a` creates an **alias**, not a copy; use `a.copy()`, `list(a)`, or `a[:]` for a copy,
  and `copy.deepcopy` for nested data. ✔
- Windows/gotchas: `sort()` returns `None`, `[[]] * n` shares inner lists, don't mutate a
  list mid-iteration. ✔
- Tuples are hashable, so they can be dict keys / set members; lists cannot. ✔
- Sequence built-ins that work on both: `len`, `min`, `max`, `sum`, `sorted`, `reversed`,
  `zip`, `enumerate`, `in`, `+`, `*`, slicing. ✔

## 18.1 Quick cheat sheet

| You want…            | Use                                   |
|----------------------|---------------------------------------|
| Empty container      | `[]` vs `()`                          |
| Add to the end       | `lst.append(x)`                       |
| Insert anywhere      | `lst.insert(i, x)`                    |
| Add many             | `lst.extend(iterable)`                |
| Remove last          | `x = lst.pop()`                       |
| Remove by value      | `lst.remove(x)` (first match)         |
| Remove by index      | `del lst[i]`                          |
| Sort (new list)      | `sorted(lst)`                         |
| Sort in place        | `lst.sort()`                          |
| Reverse (new)        | `list(reversed(lst))`  or `lst[::-1]` |
| Reverse in place     | `lst.reverse()`                       |
| Copy                 | `lst.copy()` or `lst[:]`              |
| Find first index     | `lst.index(x)`                        |
| Count                | `lst.count(x)`                        |
| Fixed data           | tuple — safest and smallest           |

---

# 19. Practice Exercises

## Lists

1. Create a list of the first 10 cubes and print it. What is the sum of all of them?
2. Given `nums = [3, 1, 4, 1, 5, 9, 2, 6]`, print (a) the max, (b) the min, (c) sorted
   ascending, (d) sorted descending.
3. Write a program that asks the user for 5 numbers, stores them in a list, then prints
   them in reverse.
4. Build a 3×3 matrix using nested `for` loops, fill it with `i * j`, and print it nicely.
5. Remove all even numbers from `[1, 2, 3, 4, 5, 6, 7, 8]` using a list comprehension.
6. Given `x = [1, 2, 3]` and `y = x`, predict the result of `y.append(4)` then `print(x)`.
   Explain your answer, then verify.
7. Flatten `[[1, 2], [3, 4], [5]]` into a single list.
8. Find the index of the value `5` in `[10, 5, 8, 5, 3]` — first only, and all positions.

## Tuples

9. Create a tuple `(1, 2, 3, 2, 1)`. How many times does `2` appear? At what index is `3`?
10. Make a 1-item tuple holding the number `42`, and an empty tuple. Print both with `type()`.
11. Predict the type of `(7)` vs `(7,)`. Verify with `type()`.
12. Unpack `("Dart", 4, None)` into three variables and print them.
13. Build a dictionary keyed by tuples: `(0,0)` → `"origin"`, `(1,1)` → `"diag"`. Look up both.
14. Write a function `swap(a, b)` that returns its two arguments swapped.
15. Can you sort a tuple of numbers? Try `sorted((3, 1, 2))`. What does it return?

## Challenge Problems

16. **Run-length encoder**: given `["a","a","b","c","c","c"]`, produce a list of tuples
    `[("a",2), ("b",1), ("c",3)]`.
17. **Histogram**: count how many times each number appears in a list using a dict, then
    print the most frequent number.
18. **Matrix transpose**: given a 2D list, return its transpose (rows ↔ columns) using one
    list comprehension.
19. **Zip back together**: given `names = ["Ana","Bob","Eve"]` and
    `scores = [88, 75, 92]`, build `[("Ana", 88), ("Bob", 75), ("Eve", 92)]`.
20. **Deduplicate preserving order**: from `[3, 1, 3, 2, 1, 4]` remove duplicates while
    keeping first-seen order.

---

# 20. Mini Project: Shopping Cart with Lists

A small, complete program that uses many of the things you just learned — lists, tuples,
comprehensions, and functions.

```python
cart = []          # each item is a tuple: (name, price)

def show_cart():
    if not cart:
        print("Your cart is empty.\n")
        return
    print("\n--- Shopping Cart ---")
    for i, (name, price) in enumerate(cart, 1):
        print(f"{i}. {name} - ${price:.2f}")
    total = sum(price for name, price in cart)
    print(f"Total: ${total:.2f}\n")

def add_item(name, price):
    cart.append((name, price))
    print(f"Added {name} for ${price:.2f}\n")

def remove_item(index):
    try:
        name, price = cart.pop(index - 1)
        print(f"Removed {name}\n")
    except IndexError:
        print("Invalid item number.\n")

while True:
    action = input("(a)dd, (r)emove, (s)how, (q)uit: ").lower()
    if action == "q":
        show_cart()
        print("Goodbye!")
        break
    elif action == "a":
        name = input("Item name: ")
        price = float(input("Price: "))
        add_item(name, price)
    elif action == "r":
        show_cart()
        index = int(input("Item number to remove: "))
        remove_item(index)
    elif action == "s":
        show_cart()
    else:
        print("Unknown choice, try again.\n")
```

## What this project practices

- Building up a list gradually with `append`. ✔
- Storing records as **tuples**: `(name, price)`. ✔
- Unpacking with `for i, (name, price) in enumerate(cart, 1)`. ✔
- A **generator expression** for the total: `sum(price for _, price in cart)`. ✔
- Using a **slice-like removal by position** with `cart.pop(index - 1)`. ✔
- Defensive programming with `try/except` for invalid input. ✔

> Tip: try extending it — add quantity per item, a discount code, or save to a file.

---

*End of Part 2. Continue to Part 3 for Dictionaries and Sets in depth, or revisit Part 1
for loops, functions, and OOP.*