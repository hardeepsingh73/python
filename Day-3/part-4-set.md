# Python Part 4 — Set (Deep Dive)

> An in-depth, beginner-friendly guide to Python's **set** data type — the unordered,
> unique-value collection. Learn how to create sets, add and remove elements, run
> mathematical set operations (union, intersection, difference, symmetric difference),
> compare sets, use frozensets, and understand when sets are the best tool — all with
> runnable, practical examples.

---

## Table of Contents

1. [What is a Set?](#1-what-is-a-set)
2. [Creating Sets](#2-creating-sets)
3. [Set Properties](#3-set-properties)
4. [Adding Elements](#4-adding-elements)
5. [Removing Elements](#5-removing-elements)
6. [Membership Testing](#6-membership-testing)
7. [Set Operations (Union, Intersection, Difference...)](#7-set-operations-union-intersection-difference)
8. [Set Operators vs Methods](#8-set-operators-vs-methods)
9. [Comparing Sets](#9-comparing-sets)
10. [Iterating Over Sets](#10-iterating-over-sets)
11. [Frozen Sets](#11-frozen-sets)
12. [Set Comprehensions](#12-set-comprehensions)
13. [Removing Duplicates from a Sequence](#13-removing-duplicates-from-a-sequence)
14. [Common Use Cases and Patterns](#14-common-use-cases-and-patterns)
15. [Common Mistakes and Gotchas](#15-common-mistakes-and-gotchas)
16. [Performance Notes](#16-performance-notes)
17. [Dictionary vs Set — Side by Side](#17-dictionary-vs-set--side-by-side)
18. [Key Takeaways](#18-key-takeaways)
19. [Practice Exercises](#19-practice-exercises)
20. [Mini Project: Unique Visitor Tracker](#20-mini-project-unique-visitor-tracker)

---

# 1. What is a Set?

A **set** is an **unordered** collection of **unique** items, written in curly braces `{}`.
Think of a bag of items where:

- No item appears twice.
- Items have no order — there is no index, you cannot do `my_set[0]`.
- Membership tests (`x in my_set`) are extremely fast.

```python
colors = {"red", "green", "blue"}
print(colors)
print(type(colors))      # <class 'set'>
```

**Output:**
```
{'red', 'green', 'blue'}
<class 'set'>
```

Key facts:

- Sets are **mutable** — you can add and remove elements.
- Elements must be **hashable** (immutable): numbers, strings, tuples, booleans.
- Sets automatically remove duplicates.
- Sets support mathematical set operations.
- Useful for deduplication, membership tests, and comparing collections.

---

# 2. Creating Sets

## 2.1 With curly braces `{}`

```python
numbers = {1, 2, 3, 4, 5}
print(numbers)
```

**Output:**
```
{1, 2, 3, 4, 5}
```

## 2.2 The empty set — you MUST use `set()`

`{}` creates an **empty dictionary**, not a set!

```python
empty = set()          # the ONLY way to create an empty set
print(empty, type(empty))

trap = {}              # this is a dict, not a set!
print(trap, type(trap))
```

**Output:**
```
set() <class 'set'>
{} <class 'dict'>
```

## 2.3 Sets handle mixed types

```python
mixed = {1, "hello", 3.14, (1, 2), False}
print(mixed)
```

**Output:**
```
{False, 1, 3.14, 'hello', (1, 2)}
```

(Note that `False` equals `0` and `True` equals `1`, so they collapse into one element — see the gotcha section.)

## 2.4 From other iterables with `set()`

The `set()` constructor converts any iterable — and **removes duplicates**:

```python
from_string = set("hello")         # characters
print(from_string)

from_list = set([1, 2, 2, 3, 3, 3])
print(from_list)

from_tuple = set((1, 2, 2, 3))
print(from_tuple)

from_range = set(range(5))
print(from_range)
```

**Output:**
```
{'e', 'h', 'l', 'o'}
{1, 2, 3}
{1, 2, 3}
{0, 1, 2, 3, 4}
```

> Because sets are unordered, the **output order is not guaranteed** across runs.

---

# 3. Set Properties

## 3.1 Unordered — no indexing

```python
s = {10, 20, 30}
# print(s[0])    # TypeError: 'set' object is not subscriptable
```

Sets do not support indexing, slicing, or `.sort()`. If you need ordering, convert to a list.

## 3.2 Unique — duplicates vanish

```python
s = {1, 2, 3, 3, 2, 1}
print(s)          # {1, 2, 3}
print(len(s))     # 3
```

**Output:**
```
{1, 2, 3}
3
```

## 3.3 Mutable

You can add and remove elements (see below), but note that sets themselves are *unhashable* —
a set can never be a dict key or a member of another set.

## 3.4 Elements must be hashable

Valid members are the same as valid dict keys:

```python
ok = {1, 2.5, "text", True, (1, 2), None}
# bad = {[1, 2]}     # TypeError: unhashable type: 'list'
# bad = { {1, 2} }   # TypeError: unhashable type: 'set'
```

---

# 4. Adding Elements

## 4.1 `.add(x)` — add a single element

```python
s = set()
s.add(1)
s.add(2)
s.add(1)          # already present → ignored
print(s)          # {1, 2}
```

**Output:**
```
{1, 2}
```

## 4.2 `.update(iterable)` — add many elements

```python
s = {1, 2}
s.update([2, 3, 4])
print(s)

s.update("hi")          # strings are iterables → each character added
print(s)
```

**Output:**
```
{1, 2, 3, 4}
{'h', 1, 2, 3, 4, 'i'}
```

`.update()` accepts multiple iterables:

```python
s = {1}
s.update([2], (3, 4), "ab")
print(s)
```

**Output:**
```
{1, 2, 3, 4, 'a', 'b'}
```

---

# 5. Removing Elements

## 5.1 `.remove(x)` — raise error if missing

```python
s = {1, 2, 3}
s.remove(2)
print(s)          # {1, 3}

# s.remove(99)    # KeyError: 99
```

**Output:**
```
{1, 3}
```

## 5.2 `.discard(x)` — safe removal, no error

```python
s = {1, 2, 3}
s.discard(99)     # no error even though 99 is missing
print(s)          # {1, 2, 3}
```

**Output:**
```
{1, 2, 3}
```

## 5.3 `.pop()` — remove and return an ARBITRARY element

Sets are unordered, so `pop()` returns a **random-looking** element:

```python
s = {10, 20, 30}
removed = s.pop()
print(removed)     # could be 10, 20 or 30
print(s)
```

**Output:**
```
10
{20, 30}
```

# 5.4 `.clear()` — remove everything

```python
s = {1, 2, 3}
s.clear()
print(s)          # set()
print(len(s))     # 0
```

**Output:**
```
set()
0
```

---

# 6. Membership Testing

## 6.1 `in` and `not in`

Membership tests are the number-one reason sets exist:

```python
fruits = {"apple", "banana", "cherry"}

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

## 6.2 Why sets beat lists for this

For lists, `in` scans item by item → O(n). For sets, `in` uses a hash table → O(1) average.
With 1,000,000 items the difference is enormous.

---

# 7. Set Operations (Union, Intersection, Difference...)

## 7.1 Union `|` — everything from both sets

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)            # union operator
print(a.union(b))       # union method → same
```

**Output:**
```
{1, 2, 3, 4, 5, 6}
{1, 2, 3, 4, 5, 6}
```

## 7.2 Intersection `&` — only common elements

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a & b)                 # intersection operator
print(a.intersection(b))     # method → same
```

**Output:**
```
{3, 4}
{3, 4}
```

## 7.3 Difference `-` — in `a` but not in `b`

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a - b)             # difference operator (a minus b)
print(a.difference(b))   # method → same
```

**Output:**
```
{1, 2}
{1, 2}
```

Note the order matters:

```python
print(b - a)   # {5, 6}
```

**Output:**
```
{5, 6}
```

## 7.4 Symmetric difference `^` — in one OR the other, not both

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a ^ b)                     # symmetric difference operator
print(a.symmetric_difference(b)) # method → same
```

**Output:**
```
{1, 2, 5, 6}
{1, 2, 5, 6}
```

## 7.5 Visual summary

If `a = {1, 2, 3}` and `b = {3, 4}`:

| Operation | Symbol | Method | Result |
|---|---|---|---|
| Union | `a \| b` | `a.union(b)` | `{1, 2, 3, 4}` |
| Intersection | `a & b` | `a.intersection(b)` | `{3}` |
| Difference | `a - b` | `a.difference(b)` | `{1, 2}` |
| Symmetric difference | `a ^ b` | `a.symmetric_difference(b)` | `{1, 2, 4}` |

## 7.6 In-place update variants

These modify the original set instead of returning a new one:

```python
a = {1, 2, 3}
b = {3, 4}

a |= b          # update with union → {1, 2, 3, 4}
print(a)

a = {1, 2, 3}
a &= b          # intersection update → {3}
print(a)

a = {1, 2, 3}
a -= b          # difference update → {1, 2}
print(a)

a = {1, 2, 3}
a ^= b          # symmetric difference update → {1, 2, 4}
print(a)
```

**Output:**
```
{1, 2, 3, 4}
{3}
{1, 2}
{1, 2, 4}
```

---

# 8. Set Operators vs Methods

| Operator | Method | In-place method |
|---|---|---|
| `a \| b` | `a.union(b)` | `a.update(b)` / `a \|= b` |
| `a & b` | `a.intersection(b)` | `a.intersection_update(b)` / `a &= b` |
| `a - b` | `a.difference(b)` | `a.difference_update(b)` / `a -= b` |
| `a ^ b` | `a.symmetric_difference(b)` | `a.symmetric_difference_update(b)` / `a ^= b` |

**Operator vs method difference:** operators require the other operand to be a **set**.
Methods accept **any iterable**:

```python
s = {1, 2, 3}

print(s.union([3, 4]))     # {1, 2, 3, 4}  — list is fine
# print(s | [3, 4])        # TypeError: unsupported operand type(s) for |: 'set' and 'list'
```

**Output:**
```
{1, 2, 3, 4}
```

---

# 9. Comparing Sets

## 9.1 Equality `==` — same elements

Order does not matter — only the members:

```python
a = {1, 2, 3}
b = {3, 2, 1}
c = {1, 2}

print(a == b)    # True  — same elements
print(a == c)    # False — different elements
```

**Output:**
```
True
False
```

## 9.2 Subset / superset

```python
a = {1, 2, 3}
b = {1, 2}

print(b.issubset(a))       # True  — every b element is in a
print(b <= a)              # True  (subset operator)
print(a.issubset(a))       # True  — a set is a subset of itself

print(a.issuperset(b))     # True  — a contains all of b
print(a >= b)              # True  (superset operator)
```

**Output:**
```
True
True
True
True
True
```

## 9.3 Proper subset / superset (strict)

```python
print(b < a)       # True — b is a proper subset of a
print(a < a)       # False — a is NOT a proper subset of itself
print(a > b)       # True — a is a proper superset of b
```

**Output:**
```
True
False
True
```

## 9.4 Disjoint — no shared elements

```python
a = {1, 2, 3}
b = {8, 9}

print(a.isdisjoint(b))     # True — nothing in common
print(a.isdisjoint({3}))   # False — they share 3
```

**Output:**
```
True
False
```

---

# 10. Iterating Over Sets

Sets are unordered, so iteration gives elements in an arbitrary (but consistent within a run) order:

```python
fruits = {"apple", "banana", "cherry"}
for fruit in fruits:
    print(fruit)
```

**Output (order may vary):**
```
cherry
apple
banana
```

If you need a predictable order, sort first:

```python
for fruit in sorted(fruits):
    print(fruit)
```

**Output:**
```
apple
banana
cherry
```

---

# 11. Frozen Sets

A **frozenset** is an **immutable** set. It cannot be changed, but it IS hashable — so it can
be used as a dict key or inside another set.

```python
fs = frozenset([1, 2, 3])
print(fs)               # frozenset({1, 2, 3})
print(type(fs))         # <class 'frozenset'>
```

**Output:**
```
frozenset({1, 2, 3})
<class 'frozenset'>
```

Immutability:

```python
# fs.add(4)     # AttributeError: 'frozenset' object has no attribute 'add'
# fs.remove(1)  # AttributeError
```

**Hashable — usable as dict keys and set elements:**

```python
d = {frozenset(["a", "b"]): "pair"}
print(d[frozenset(["a", "b"])])     # pair

s = {frozenset([1, 2]), frozenset([3, 4])}
print(s)                            # {frozenset({1, 2}), frozenset({3, 4})}
```

**Output:**
```
pair
{frozenset({3, 4}), frozenset({1, 2})}
```

Frozen sets still support all the read-only set operations:

```python
a = frozenset([1, 2, 3])
b = frozenset([3, 4])
print(a | b)     # frozenset({1, 2, 3, 4})
print(a & b)     # frozenset({3})
print(a - b)     # frozenset({1, 2})
print(a ^ b)     # frozenset({1, 2, 4})
print(2 in a)    # True
```

**Output:**
```
frozenset({1, 2, 3, 4})
frozenset({3})
frozenset({1, 2})
frozenset({1, 2, 4})
True
```

---

# 12. Set Comprehensions

The syntax is exactly like a list comprehension, but with curly braces:

```
{expression for item in iterable if condition}
```

```python
evens = {n for n in range(10) if n % 2 == 0}
print(evens)          # {0, 2, 4, 6, 8}
```

**Output:**
```
{0, 2, 4, 6, 8}
```

More examples:

```python
squares = {n ** 2 for n in range(6)}
print(squares)                       # {0, 1, 4, 9, 16, 25}

words = ["cat", "dog", "bird", "elephant"]
lengths = {len(w) for w in words}    # duplicates collapse
print(lengths)                       # {3, 4, 8}

# extract unique letters
text = "hello world"
letters = {ch for ch in text}
print(letters)                       # {'w', 'h', 'e', 'l', 'o', 'd', 'r', ' '}
```

**Output:**
```
{0, 1, 4, 9, 16, 25}
{3, 4, 8}
{'h', 'o', 'l', 'r', 'd', 'e', 'w', ' '}
```

---

# 13. Removing Duplicates from a Sequence

The single most common set trick:

```python
numbers = [1, 2, 3, 3, 2, 1, 4, 5, 5]
unique = set(numbers)
print(unique)              # {1, 2, 3, 4, 5}

# back to a list (order NOT preserved)
unique_list = list(unique)
print(unique_list)         # order may vary
```

**Output:**
```
{1, 2, 3, 4, 5}
[1, 2, 3, 4, 5]
```

> If you need to keep the original order while removing duplicates, use a nested loop or
> dict-based deduplication:

```python
items = [4, 1, 4, 2, 1, 3]
seen = set()
ordered = []

for item in items:
    if item not in seen:
        seen.add(item)
        ordered.append(item)

print(ordered)    # [4, 1, 2, 3]  — order preserved!
```

**Output:**
```
[4, 1, 2, 3]
```

---

# 14. Common Use Cases and Patterns

## 14.1 Fast membership testing

```python
allowed_ips = {"192.168.1.10", "192.168.1.11", "192.168.1.12"}
print("192.168.1.10" in allowed_ips)    # True
print("10.0.0.1" in allowed_ips)        # False
```

## 14.2 Finding common items between two lists

```python
students_python = ["Ana", "Bob", "Eve"]
students_java = ["Bob", "Max", "Eve"]

print(set(students_python) & set(students_java))     # {'Eve', 'Bob'}
```

**Output:**
```
{'Eve', 'Bob'}
```

## 14.3 Finding unique items only in the first list

```python
print(set(students_python) - set(students_java))     # {'Ana'}
```

**Output:**
```
{'Ana'}
```

## 14.4 Counting unique characters in a string

```python
text = "abracadabra"
print(len(set(text)))    # 5  → {a, b, r, c, d}
```

**Output:**
```
5
```

## 14.5 Checking if two collections have anything in common

```python
def share_element(a, b):
    return not set(a).isdisjoint(b)

print(share_element([1, 2], [2, 3]))    # True
print(share_element([1, 2], [9, 8]))    # False
```

**Output:**
```
True
False
```

## 14.6 Checking if every element of a list is in a reference set

```python
required = {"name", "age", "city"}
form_fields = {"age", "name"}

print(required.issubset(form_fields))   # False
print(required.issuperset(form_fields)) # True
```

**Output:**
```
False
True
```

---

# 15. Common Mistakes and Gotchas

## 15.1 `{}` is a dict, not a set

```python
wrong = {}
print(type(wrong))     # <class 'dict'>

right = set()
print(type(right))     # <class 'set'>
```

**Output:**
```
<class 'dict'>
<class 'set'>
```

## 15.2 Trying to index a set

```python
s = {10, 20, 30}
# s[0]     # TypeError: 'set' object is not subscriptable
```

Convert to a list first: `list(s)[0]`.

## 15.3 Using a list as a set element

```python
# s = {[1, 2]}    # TypeError: unhashable type: 'list'
s = {(1, 2)}      # fine — tuple is hashable
print(s)
```

**Output:**
```
{(1, 2)}
```

## 15.4 Forgetting that `False` == `0` and `True` == `1`

Sets treat equal values as the same element:

```python
s = {0, False, 1, True}
print(s)        # {0, 1}
print(len(s))   # 2
```

**Output:**
```
{0, 1}
2
```

## 15.5 Mutating a set while iterating over it

```python
s = {1, 2, 3, 4}
# for x in s:
#     s.remove(x)     # RuntimeError: Set changed size during iteration
```

**Fix — iterate over a copy:**

```python
s = {1, 2, 3, 4}
for x in list(s):
    s.remove(x)
print(s)       # set()
```

**Output:**
```
set()
```

## 15.6 Order is unpredictable (but stable within a run)

Do not write code that depends on set iteration order. If you need order, sort or use a list.

```python
print(list({3, 1, 2}))    # the exact order varies; results from different runs may differ
```

## 15.7 `pop()` on a non-empty set returns an arbitrary element

Never assume which element `set.pop()` removes.

---

# 16. Performance Notes

## 16.1 `in` on a set is O(1); on a list it is O(n)

```python
import time

size = 1_000_000
data = list(range(size))           # 1 million integers
as_set = set(data)

start = time.perf_counter()
print(999_999 in as_set)           # instant
print(f"set membership:  {time.perf_counter() - start:.6f}s")

start = time.perf_counter()
print(999_999 in data)             # scans nearly a million items
print(f"list membership: {time.perf_counter() - start:.6f}s")
```

## 16.2 Set operations scale by set size

Union/intersection/difference over big sets are fast (hashed), but constructing the sets
from scratch costs time and memory.

## 16.3 Memory

Sets use hash tables, so they use more memory than an equivalent list — trade memory for
blazing-fast membership tests.

---

# 17. Dictionary vs Set — Side by Side

| Feature              | Dictionary                              | Set                                 |
|----------------------|-----------------------------------------|-------------------------------------|
| Written with         | `{"key": value}`                        | `{value}` or `set()`                |
| Empty literal        | `{}` (dict!)                            | `set()`                             |
| Stores               | key-value pairs                         | unique values only                  |
| Index / subscript    | By key                                  | Not subscriptable                   |
| Order                | Insertion order (3.7+)                  | Unordered                           |
| Duplicates           | Keys must be unique                     | Elements must be unique             |
| Element type         | Keys hashable, values anything          | All elements hashable (immutable)   |
| Mutable              | Yes                                     | Yes                                 |
| Immutable variant    | —                                       | `frozenset`                         |
| Fast lookup          | `d[key]`, `key in d` (keys)             | `x in s`                            |
| Typical use          | Lookup table, structured data, JSON     | Deduplication, membership, set math |
| Main methods         | `get`, `keys`, `values`, `items`        | `add`, `union`, `intersection`      |

---

# 18. Key Takeaways

- A set stores **unique**, **unordered**, **hashable** elements. ✔
- Create with `{...}`; the empty set **must** be `set()`. ✔
- Add with `.add()` / `.update()`; remove with `.remove()` (strict) and `.discard()` (safe). ✔
- Union `|`, intersection `&`, difference `-`, symmetric difference `^`. ✔
- Methods accept any iterable; operators require a set. ✔
- Compare with `==`, `issubset`, `issuperset`, `isdisjoint`. ✔
- `frozenset` is the immutable, hashable sibling. ✔
- Deduplicate any iterable with `set(iterable)`. ✔
- Membership tests are O(1) — beats lists by far. ✔
- Sets are unhashable and cannot contain each other (use `frozenset`). ✔

---

# 19. Practice Exercises

1. Create a set of 5 fruits; print its length and whether `"apple"` is in it.
2. Remove duplicates from `[1, 2, 2, 3, 4, 4, 4, 5]` and print the unique values.
3. Given two lists of numbers, print the common numbers, numbers in either, and numbers
   only in the first.
4. Count the number of unique characters in `"mississippi"`.
5. Add `6` to `{1, 2, 3}` with `.add()`, then add `[7, 8, 9]` with `.update()`.
6. Try `s.remove(999)` and `s.discard(999)` — what is the difference?
7. Given two sets, check whether one is a subset of the other and whether they are disjoint.
8. Write a set comprehension for all even numbers from 1 to 20.
9. Build a set of the lengths of a list of words (duplicates collapse automatically).
10. Create a `frozenset` and try to add an element. Explain the error.
11. Given three sets, find the element that appears in all three (intersection of three).
12. Write a function `unique_words(sentence)` returning the set of unique words.
13. Print the symmetric difference of two sets of email addresses that subscribed to both a
    discount and a newsletter.
14. Convert a set to a sorted list and iterate.
15. Mini-puzzle: `{1, 2} | {3, 4}` vs `{1, 2} + {3, 4}` — why does the second fail?

---

# 20. Mini Project: Unique Visitor Tracker

Track unique visitors per day and report daily stats using a set. Run in a `.py` file:

```python
visits = {
    "2025-01-01": {"alice", "bob", "carol"},
    "2025-01-02": {"bob", "dave", "alice"},
    "2025-01-03": {"eve", "alice"},
}

all_visitors = set()
for day in visits:
    all_visitors.update(visits[day])

print("Total unique visitors:", len(all_visitors))
print()

# Who visited both Day 1 and Day 2?
print("Visited day1 & day2:", visits["2025-01-01"] & visits["2025-01-02"])

# Who visited on all three days?
common = visits["2025-01-01"]
for day in visits:
    common &= visits[day]
print("Visited all three days:", common)

# A dictionary of daily counts
daily_counts = {day: len(visitors) for day, visitors in visits.items()}
print("Daily counts:", daily_counts)
```

**Output (order may vary):**
```
Total unique visitors: 5

Visited day1 & day2: {'bob', 'alice'}
Visited all three days: {'alice'}
Daily counts: {'2025-01-01': 3, '2025-01-02': 3, '2025-01-03': 2}
```

---

*Sets are a hidden superpower in Python — once you know them, deduplication, membership
tests, and comparing collections become one-liners. Happy coding!*