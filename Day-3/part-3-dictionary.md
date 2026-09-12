# Python Part 3 — Dictionary (Deep Dive)

> An in-depth, beginner-friendly guide to Python's **dictionary** (`dict`) data type —
> the mapping type that stores **key-value pairs**. Learn how to create, access, modify,
> iterate, nest, and merge dictionaries — all with runnable, practical examples.

---

## Table of Contents

1. [What is a Dictionary?](#1-what-is-a-dictionary)
2. [Creating Dictionaries](#2-creating-dictionaries)
3. [Dictionary Keys and Values](#3-dictionary-keys-and-values)
4. [Accessing Values](#4-accessing-values)
5. [Adding and Updating Items](#5-adding-and-updating-items)
6. [Removing Items](#6-removing-items)
7. [Dictionary Methods in Detail](#7-dictionary-methods-in-detail)
8. [Iterating Over Dictionaries](#8-iterating-over-dictionaries)
9. [Nested Dictionaries](#9-nested-dictionaries)
10. [Dictionary Comprehensions](#10-dictionary-comprehensions)
11. [Merging and Unpacking Dictionaries](#11-merging-and-unpacking-dictionaries)
12. [Dictionary Views (keys, values, items)](#12-dictionary-views-keys-values-items)
13. [Copying Dictionaries](#13-copying-dictionaries)
14. [Ordering Guarantees](#14-ordering-guarantees)
15. [Common Use Cases and Patterns](#15-common-use-cases-and-patterns)
16. [Common Mistakes and Gotchas](#16-common-mistakes-and-gotchas)
17. [Performance Notes](#17-performance-notes)
18. [Key Takeaways](#18-key-takeaways)
19. [Practice Exercises](#19-practice-exercises)
20. [Mini Project: Phone Book Manager](#20-mini-project-phone-book-manager)

---

# 1. What is a Dictionary?

A **dictionary** (short: **dict**) is a collection of **key-value pairs** that preserves
**insertion order** (guaranteed since Python 3.7). Think of a real dictionary: you look up a
*word* (the key) and you get its *definition* (the value). Python dicts work the same way —
you give a key and you instantly get its value.

```python
student = {"name": "Alice", "age": 20, "grade": "A"}
print(student)
print(student["name"])   # lookup by key
```

**Output:**
```
{'name': 'Alice', 'age': 20, 'grade': 'A'}
Alice
```

Key facts:

- Dictionaries map **unique keys** to **values**.
- Lookups by key are extremely **fast** (they use hashing, O(1) on average).
- Values can be **any** type — numbers, strings, lists, tuples, functions, even other dicts.
- Keys must be **immutable** (hashable): strings, numbers, tuples, booleans.
- Dictionaries are **mutable** — you can add, remove, and change items after creation.
- In Python 3.7+, dictionaries preserve **insertion order**.

---

# 2. Creating Dictionaries

## 2.1 With curly braces `{}`

This is the most common and readable way:

```python
person = {
    "name": "Bob",
    "age": 30,
    "job": "Engineer",
}
print(person)
```

**Output:**
```
{'name': 'Bob', 'age': 30, 'job': 'Engineer'}
```

## 2.2 The empty dictionary

An empty dict can be created with `{}` or the `dict()` constructor:

```python
empty1 = {}
empty2 = dict()

print(empty1, type(empty1))   # {} <class 'dict'>
print(empty2, type(empty2))   # {} <class 'dict'>
```

**Output:**
```
{} <class 'dict'>
{} <class 'dict'>
```

> **Important:** `{}` creates an *empty dictionary*, NOT an empty set. For an empty set
> you must use `set()`.

## 2.3 With the `dict()` constructor

`dict()` accepts keyword arguments:

```python
person = dict(name="Ana", age=25, city="Paris")
print(person)
```

**Output:**
```
{'name': 'Ana', 'age': 25, 'city': 'Paris'}
```

## 2.4 From a list of pairs

Pass an iterable of `(key, value)` pairs:

```python
pairs = [("name", "Eve"), ("age", 35)]
person = dict(pairs)
print(person)
```

**Output:**
```
{'name': 'Eve', 'age': 35}
```

This also works with a list of two-element lists or with `zip()`:

```python
keys = ["name", "age", "city"]
values = ["Bob", 40, "London"]
person = dict(zip(keys, values))
print(person)
```

**Output:**
```
{'name': 'Bob', 'age': 40, 'city': 'London'}
```

## 2.5 Using `fromkeys()` — default values for many keys

```python
marks = dict.fromkeys(["math", "english", "science"], 0)
print(marks)
```

**Output:**
```
{'math': 0, 'english': 0, 'science': 0}
```

---

# 3. Dictionary Keys and Values

## 3.1 What can be a key?

Keys must be **hashable** (immutable). That means:

| Can be a key | Cannot be a key |
|---|---|
| `str`  (`"name"`)   | `list`  |
| `int`  (`1`, `42`)  | `dict`  |
| `float` (`3.14`)    | `set`   |
| `bool` (`True`, `False`) | (any mutable object) |
| `tuple` (`(1, 2)`)  | |
| `None`              | |

```python
d = {
    "name": "Alice",        # string key
    1: "one",               # int key
    3.14: "pi",             # float key
    (1, 2): "tuple key",    # tuple key
    True: "boolean key",    # bool key
}

print(d["name"])
print(d[1])
print(d[(1, 2)])
```

**Output:**
```
Alice
one
tuple key
```

Lists, sets, and dicts cannot be keys:

```python
# d[[1, 2]] = "x"     # TypeError: unhashable type: 'list'
# d[{1, 2}] = "x"     # TypeError: unhashable type: 'set'
# d[{"a": 1}] = "x"   # TypeError: unhashable type: 'dict'
```

## 3.2 Keys must be unique

If you repeat a key, the **last** value wins:

```python
d = {"a": 1, "a": 2}
print(d)          # {'a': 2}
```

**Output:**
```
{'a': 2}
```

## 3.3 What can be a value?

Values can be **anything** — mutable or immutable:

```python
d = {
    "name": "Alice",
    "age": 25,
    "scores": [90, 85, 95],        # a list
    "address": {"city": "Delhi"},  # a nested dict
    "is_student": True,            # a boolean
    "tag": None,                   # None
}
print(d)
```

**Output:**
```
{'name': 'Alice', 'age': 25, 'scores': [90, 85, 95], 'address': {'city': 'Delhi'}, 'is_student': True, 'tag': None}
```

---

# 4. Accessing Values

## 4.1 Bracket notation `d[key]`

The fastest way — but raises `KeyError` if the key is missing:

```python
person = {"name": "Bob", "age": 40}

print(person["name"])     # Bob
print(person["age"])      # 40
```

**Output:**
```
Bob
40
```

```python
# print(person["city"])   # KeyError: 'city'
```

## 4.2 The safe `.get()` method

`.get(key, default)` returns the value, or the default instead of crashing:

```python
person = {"name": "Bob", "age": 40}

print(person.get("name"))               # Bob
print(person.get("city"))               # None  (default default!)
print(person.get("city", "Unknown"))    # Unknown
```

**Output:**
```
Bob
None
Unknown
```

`get()` never raises `KeyError`. Use it when the key may be absent.

## 4.3 `.setdefault(key, default)` — get OR insert

Returns the value if the key exists; otherwise inserts the key with the default and returns it:

```python
d = {"a": 1}

print(d.setdefault("a", 99))    # 1  (exists → return value)
print(d.setdefault("b", 10))    # 10 (missing → insert with 10)
print(d)                        # {'a': 1, 'b': 10}
```

**Output:**
```
1
10
{'a': 1, 'b': 10}
```

## 4.4 Checking for a key with `in`

Use the membership operator — it only checks **keys**:

```python
person = {"name": "Bob", "age": 40}

print("name" in person)       # True
print("city" in person)       # False
print("Bob" in person)        # False — checks KEYS, not values
```

**Output:**
```
True
False
False
```

To check whether a value exists, use `"Bob" in person.values()`.

## 4.5 Bracket vs `get()` — summary

| Situation | Use | Result |
|---|---|---|
| Key is guaranteed present | `d[key]` | value |
| Key may be missing | `d.get(key)` | value or `None` |
| Want a custom fallback | `d.get(key, "x")` | value or `"x"` |
| Want to insert if missing | `d.setdefault(key, v)` | value (inserted if needed) |

---

# 5. Adding and Updating Items

## 5.1 Add or update with `[]`

If the key exists, the value is **updated**; if not, it is **added**:

```python
person = {"name": "Bob"}

person["age"] = 40          # add a new key-value pair
person["name"] = "Robert"   # update an existing key

print(person)
```

**Output:**
```
{'name': 'Robert', 'age': 40}
```

## 5.2 Merge with `.update()`

`update()` merges another dict (or keyword args, or pairs) into this one. Existing keys are
overwritten; new keys are added:

```python
person = {"name": "Bob", "age": 40}

person.update({"age": 41, "city": "Paris"})
print(person)

person.update(job="Engineer")
print(person)
```

**Output:**
```
{'name': 'Bob', 'age': 41, 'city': 'Paris'}
{'name': 'Bob', 'age': 41, 'city': 'Paris', 'job': 'Engineer'}
```

## 5.3 Incrementing a value in a dict

A super-common pattern for counters:

```python
votes = {"A": 0, "B": 0}

votes["A"] += 1
votes["A"] += 1
votes["B"] += 1

print(votes)   # {'A': 2, 'B': 1}
```

**Output:**
```
{'A': 2, 'B': 1}
```

---

# 6. Removing Items

## 6.1 `pop(key, [default])` — remove and return the value

```python
person = {"name": "Ana", "age": 25, "city": "Berlin"}

removed = person.pop("city")
print(removed, person)
```

**Output:**
```
Berlin {'name': 'Ana', 'age': 25}
```

If the key is missing, `pop()` raises `KeyError` unless you give a default:

```python
person = {"name": "Ana"}
print(person.pop("age", "not found"))   # not found
```

**Output:**
```
not found
```

## 6.2 `popitem()` — remove and return the last inserted pair

Removes and returns an `(key, value)` tuple (the last one in insertion order):

```python
d = {"a": 1, "b": 2, "c": 3}
item = d.popitem()
print(item)          # ('c', 3)
print(d)             # {'a': 1, 'b': 2}
```

**Output:**
```
('c', 3)
{'a': 1, 'b': 2}
```

## 6.3 `del d[key]` — delete by key (statement)

```python
person = {"name": "Ana", "age": 25, "city": "Berlin"}

del person["city"]
print(person)

# del person["country"]   # KeyError: 'country'
```

**Output:**
```
{'name': 'Ana', 'age': 25}
```

## 6.4 `clear()` — remove everything

```python
d = {"a": 1, "b": 2}
d.clear()
print(d)      # {}
print(len(d)) # 0
```

**Output:**
```
{}
0
```

## 6.5 Removal methods comparison

| Method | Removes | Returns | Missing key? |
|---|---|---|---|
| `pop(key)` | key | value | `KeyError` |
| `pop(key, default)` | key | value or default | safe |
| `popitem()` | last item | `(key, value)` tuple | `KeyError` on empty |
| `del d[key]` | key | nothing | `KeyError` |
| `clear()` | everything | nothing | — |

---

# 7. Dictionary Methods in Detail

## 7.1 Full method reference

| Method                     | Description                                             |
|----------------------------|---------------------------------------------------------|
| `d.get(key, [default])`    | Value for key or default (never raises)                 |
| `d.setdefault(k, [v])`     | Get value; insert `k: v` if missing                     |
| `d.update(other)`          | Merge another dict / pairs / kwargs                     |
| `d.pop(k, [default])`      | Remove `k`, return its value                            |
| `d.popitem()`              | Remove & return the last `(key, value)` pair            |
| `d.keys()`                 | View of all keys                                        |
| `d.values()`               | View of all values                                      |
| `d.items()`                | View of all `(key, value)` pairs                        |
| `d.copy()`                 | Shallow copy                                            |
| `d.clear()`                | Remove everything                                       |
| `dict.fromkeys(seq, v)`    | New dict with keys from `seq`, all value `v`            |
| `dict.fromkeys(seq)`       | New dict with keys from `seq`, values `None`            |

## 7.2 `len()`, `in`, `any()`, `all()`, `sum()`

```python
d = {"a": 1, "b": 2, "c": 3}

print(len(d))               # 3
print("b" in d)             # True
print(2 in d.values())      # True
print(sum(d.values()))      # 6
```

**Output:**
```
3
True
True
6
```

---

# 8. Iterating Over Dictionaries

## 8.1 Keys by default

```python
person = {"name": "Ana", "age": 25, "city": "Berlin"}

for key in person:
    print(key)
```

**Output:**
```
name
age
city
```

## 8.2 Keys explicitly

```python
for key in person.keys():
    print(key)
```

## 8.3 Values

```python
for value in person.values():
    print(value)
```

**Output:**
```
Ana
25
Berlin
```

## 8.4 Keys and values together with `.items()`

```python
for key, value in person.items():
    print(f"{key} = {value}")
```

**Output:**
```
name = Ana
age = 25
city = Berlin
```

## 8.5 Using `enumerate` with a dict

```python
for index, key in enumerate(person):
    print(index, key)
```

**Output:**
```
0 name
1 age
2 city
```

## 8.6 Building a list from a dict

`list(d)` gives the keys. Use `.values()` / `.items()` for the rest:

```python
d = {"a": 1, "b": 2, "c": 3}

print(list(d))               # ['a', 'b', 'c']
print(list(d.keys()))        # ['a', 'b', 'c']
print(list(d.values()))      # [1, 2, 3]
print(list(d.items()))       # [('a', 1), ('b', 2), ('c', 3)]
```

**Output:**
```
['a', 'b', 'c']
['a', 'b', 'c']
[1, 2, 3]
[('a', 1), ('b', 2), ('c', 3)]
```

---

# 9. Nested Dictionaries

## 9.1 Storing records

Dictionaries inside dictionaries model real-world objects beautifully:

```python
users = {
    "alice": {"age": 30, "email": "alice@example.com"},
    "bob":   {"age": 25, "email": "bob@example.com"},
}

print(users["bob"]["email"])       # bob@example.com
print(users["alice"]["age"])       # 30
```

**Output:**
```
bob@example.com
30
```

## 9.2 Iterating over nested data

```python
for name, info in users.items():
    print(f"{name} is {info['age']} years old")
```

**Output:**
```
alice is 30 years old
bob is 25 years old
```

## 9.3 Deeper nesting — a grid / config

```python
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "credentials": {"user": "admin", "password": "secret"},
    },
    "debug": True,
}

print(config["database"]["port"])                    # 5432
print(config["database"]["credentials"]["user"])     # admin
```

**Output:**
```
5432
admin
```

## 9.4 Safe navigation on nested dicts

Dictionary `get()` + default helps avoid deep `KeyError`s:

```python
print(config.get("database", {}).get("name", "default_db"))
```

**Output:**
```
default_db
```

---

# 10. Dictionary Comprehensions

## 10.1 Basic pattern

```
{key_expression: value_expression for item in iterable if condition}
```

```python
squares = {n: n ** 2 for n in range(5)}
print(squares)
```

**Output:**
```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## 10.2 With a condition

```python
ages = {"Ana": 25, "Bob": 40, "Eve": 30}
adults = {name: age for name, age in ages.items() if age >= 30}
print(adults)
```

**Output:**
```
{'Bob': 40, 'Eve': 30}
```

## 10.3 Transforming keys or values

```python
words = ["cat", "dog", "elephant"]
lengths = {word: len(word) for word in words}
print(lengths)
```

**Output:**
```
{'cat': 3, 'dog': 3, 'elephant': 8}
```

## 10.4 Inverting a dict (swap keys and values)

```python
original = {"a": 1, "b": 2, "c": 3}
inverted = {value: key for key, value in original.items()}
print(inverted)
```

**Output:**
```
{1: 'a', 2: 'b', 3: 'c'}
```

> Note: if two keys share the same value, the later one wins during inversion.

## 10.5 Building a word-counter with a loop

A classic — count letter frequencies:

```python
text = "hello"
counts = {}
for ch in text:
    counts[ch] = counts.get(ch, 0) + 1
print(counts)
```

**Output:**
```
{'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

The one-liner version using `collections.Counter`:

```python
from collections import Counter
print(Counter("hello"))
```

**Output:**
```
Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})
```

---

# 11. Merging and Unpacking Dictionaries

## 11.1 Merge with `update()`

```python
first = {"a": 1, "b": 2}
second = {"b": 3, "c": 4}

first.update(second)
print(first)
```

**Output:**
```
{'a': 1, 'b': 3, 'c': 4}
```

## 11.2 Merge with `{**d1, **d2}` unpacking

Later dicts win for duplicate keys:

```python
first = {"a": 1, "b": 2}
second = {"b": 3, "c": 4}

merged = {**first, **second}
print(merged)
```

**Output:**
```
{'a': 1, 'b': 3, 'c': 4}
```

## 11.3 Merge with `|` (Python 3.9+)

The modern union operator:

```python
first = {"a": 1, "b": 2}
second = {"b": 3, "c": 4}

merged = first | second
print(merged)

first |= second        # in-place merge, like update()
print(first)
```

**Output:**
```
{'a': 1, 'b': 3, 'c': 4}
{'a': 1, 'b': 3, 'c': 4}
```

## 11.4 `**kwargs` — passing a dict to a function

```python
def show(**kwargs):
    for k, v in kwargs.items():
        print(k, "=", v)

show(name="Ana", age=25)
```

**Output:**
```
name = Ana
age = 25
```

You can also explode an existing dict into keyword arguments:

```python
show(**{"name": "Bob", "age": 40})
```

---

# 12. Dictionary Views (keys, values, items)

`keys()`, `values()`, and `items()` return **view objects**. They are dynamic — if the dict
changes, the view reflects the change automatically.

```python
d = {"a": 1, "b": 2}
view = d.keys()

print(view)          # dict_keys(['a', 'b'])

d["c"] = 3
print(view)          # dict_keys(['a', 'b', 'c'])  → updated automatically!
```

**Output:**
```
dict_keys(['a', 'b'])
dict_keys(['a', 'b', 'c'])
```

Views support membership checks:

```python
print("a" in d.keys())        # True
print(2 in d.values())        # True
print(("b", 2) in d.items())  # True
```

**Output:**
```
True
True
True
```

---

# 13. Copying Dictionaries

## 13.1 Aliasing — `b = a` does NOT copy

```python
a = {"name": "Alice", "age": 25}
b = a                    # another name for the SAME dict

b["age"] = 30
print(a)                 # {'name': 'Alice', 'age': 30}  → changed too!
print(a is b)            # True
```

**Output:**
```
{'name': 'Alice', 'age': 30}
True
```

## 13.2 Shallow copy — `.copy()`

```python
a = {"name": "Alice", "age": 25}
b = a.copy()             # independent copy

b["age"] = 30
print(a)                 # unchanged: {'name': 'Alice', 'age': 25}
print(b)                 # {'name': 'Alice', 'age': 30}
```

**Output:**
```
{'name': 'Alice', 'age': 25}
{'name': 'Alice', 'age': 30}
```

`dict(a)` also makes a shallow copy.

## 13.3 Shallow copy pitfall — nested values are shared

```python
a = {"scores": [1, 2, 3]}
b = a.copy()

b["scores"].append(4)    # mutates the SHARED inner list
print(a)                 # {'scores': [1, 2, 3, 4]}  → changed!
```

**Output:**
```
{'scores': [1, 2, 3, 4]}
```

## 13.4 Deep copy with `copy.deepcopy`

```python
import copy

a = {"scores": [1, 2, 3]}
b = copy.deepcopy(a)

b["scores"].append(4)
print(a)                # {'scores': [1, 2, 3]}  → untouched
print(b)                # {'scores': [1, 2, 3, 4]}
```

**Output:**
```
{'scores': [1, 2, 3]}
{'scores': [1, 2, 3, 4]}
```

---

# 14. Ordering Guarantees

- Python **3.6**: insertion order preserved (implementation detail in CPython).
- Python **3.7+**: insertion order is **guaranteed** by the language spec.

This means iteration and `.items()` give you items in the order they were added:

```python
d = {}
d["z"] = 1
d["a"] = 2
d["m"] = 3

for key in d:
    print(key)
```

**Output:**
```
z
a
m
```

---

# 15. Common Use Cases and Patterns

## 15.1 Counting frequencies

```python
words = ["apple", "banana", "apple", "cherry", "apple", "banana"]
counts = {}
for word in words:
    counts[word] = counts.get(word, 0) + 1
print(counts)
```

**Output:**
```
{'apple': 3, 'banana': 2, 'cherry': 1}
```

## 15.2 Grouping data

```python
students = [
    ("Ana", "Science"),
    ("Bob", "Math"),
    ("Eve", "Science"),
]

groups = {}
for name, subject in students:
    groups.setdefault(subject, []).append(name)

print(groups)
```

**Output:**
```
{'Science': ['Ana', 'Eve'], 'Math': ['Bob']}
```

## 15.3 Lookup tables / mapping

```python
def grade_from_score(score):
    table = {10: "A+", 9: "A", 8: "B", 7: "C"}
    return table.get(score, "Invalid")

print(grade_from_score(10))   # A+
print(grade_from_score(5))    # Invalid
```

**Output:**
```
A+
Invalid
```

## 15.4 Swapping keys and values (invert)

```python
code = {"A": 65, "B": 66, "C": 67}
reverse = {v: k for k, v in code.items()}
print(reverse)
```

**Output:**
```
{65: 'A', 66: 'B', 67: 'C'}
```

## 15.5 JSON-like structured data

Dictionaries map naturally to JSON:

```python
product = {
    "id": 101,
    "name": "Wireless Mouse",
    "price": 12.99,
    "colors": ["black", "white", "silver"],
    "in_stock": True,
}
print(product["name"], product["price"])
```

**Output:**
```
Wireless Mouse 12.99
```

## 15.6 Using a dict as a switch/case

```python
def operate(a, b, op):
    operations = {
        "add": a + b,
        "sub": a - b,
        "mul": a * b,
    }
    return operations.get(op, "Invalid operation")

print(operate(10, 5, "add"))    # 15
print(operate(10, 5, "div"))    # Invalid operation
```

**Output:**
```
15
Invalid operation
```

## 15.7 Dynamic values with functions as dict values

```python
def double(x): return x * 2
def triple(x): return x * 3

actions = {"double": double, "triple": triple}
print(actions["double"](5))    # 10
print(actions["triple"](5))    # 15
```

**Output:**
```
10
15
```

---

# 16. Common Mistakes and Gotchas

## 16.1 `KeyError` when using brackets

```python
d = {"name": "Bob"}
# print(d["city"])    # KeyError: 'city'
print(d.get("city", "unknown"))   # unknown
```

**Output:**
```
unknown
```

## 16.2 `{}` is a dict, not a set

```python
x = {}
print(type(x))        # <class 'dict'>
```

**Output:**
```
<class 'dict'>
```

## 16.3 Using a mutable object as a key

```python
# d = {["a", "b"]: 1}   # TypeError: unhashable type: 'list'
d = {("a", "b"): 1}     # tuple works
print(d[("a", "b")])
```

**Output:**
```
1
```

## 16.4 Modifying a dict while iterating over it

```python
d = {"a": 1, "b": 2, "c": 3}
# for k in d:
#    if d[k] == 2:
#        del d[k]     # RuntimeError: dictionary changed size during iteration
```

**Fix — iterate over a copy:**

```python
d = {"a": 1, "b": 2, "c": 3}
for k in list(d):
    if d[k] == 2:
        del d[k]
print(d)               # {'a': 1, 'c': 3}
```

**Output:**
```
{'a': 1, 'c': 3}
```

## 16.5 `in` checks keys, not values

```python
d = {"name": "Alice"}
print("Alice" in d)          # False!  (checks keys)
print("Alice" in d.values()) # True    (checks values)
```

**Output:**
```
False
True
```

## 16.6 Aliasing — `b = a` shares the dict

```python
a = {"x": 1}
b = a
b["x"] = 99
print(a)         # {'x': 99}  → shared object!
```

**Output:**
```
{'x': 99}
```

## 16.7 Overwriting duplicate keys silently

```python
d = {"a": 1, "a": 2}
print(d)     # {'a': 2}
```

**Output:**
```
{'a': 2}
```

## 16.8 Sorting a dict

Dicts can't be sorted by themselves, but you can build a sorted version:

```python
ages = {"Ana": 25, "Bob": 40, "Eve": 30}

by_name = dict(sorted(ages.items()))
print(by_name)

by_age = dict(sorted(ages.items(), key=lambda item: item[1]))
print(by_age)
```

**Output:**
```
{'Ana': 25, 'Bob': 40, 'Eve': 30}
{'Ana': 25, 'Eve': 30, 'Bob': 40}
```

---

# 17. Performance Notes

## 17.1 Lookup by key is O(1)

Dictionaries use a hash table, so reading `d[key]` is effectively instant — even for
millions of entries:

```python
import time
big = {i: i ** 2 for i in range(1_000_000)}

start = time.perf_counter()
value = big[999_999]
print(f"lookup time: {time.perf_counter() - start:.6f}s")
```

## 17.2 `in` on a dict checks keys in O(1)

```python
print(500_000 in big)      # True  (fast!)
print("hello" in big)      # False
```

## 17.3 One big trade-off: memory

Hash tables use extra memory for the speed. For huge data with numeric keys, a list of
tuples or arrays may be lighter — but for readable, fast key lookup, dicts win.

---

# 18. Key Takeaways

- A dict stores unique **key → value** pairs. ✔
- Keys must be hashable/immutable (`str`, `int`, `float`, `bool`, `tuple`). ✔
- `.get()` is the safe accessor; `in` checks keys. ✔
- Add/update with `d[new_key] = value` or `.update()`. ✔
- Remove with `.pop()`, `.popitem()`, `del`, or `.clear()`. ✔
- Iterate with `.keys()`, `.values()`, and `.items()`. ✔
- Dicts preserve insertion order (Python 3.7+). ✔
- Dict comprehensions make building lookup tables one line. ✔
- `{}` creates a dict — use `set()` for an empty set. ✔
- Lookups are O(1) — dicts are the fastest way to store keyed data. ✔

---

# 19. Practice Exercises

1. Create a dict called `car` with keys `brand`, `model`, `year`. Print each value.
2. Take a dict and print every `key = value` on its own line using `.items()`.
3. Build a `word_count(text)` function that returns a dict of word → frequency.
4. Use `.get()` to look up two keys — one present, one missing — with a default.
5. Merge two dicts using `.update()`, `{**a, **b}`, and `a | b`. Verify results are equal.
6. Invert a dict (swap keys and values) with a comprehension.
7. Given a list of numbers, return a dict where key = number, value = "even"/"odd".
8. Group a list of words by their first letter into a dict of lists.
9. Build a dict comprehension mapping numbers 1–10 to their cubes.
10. Nested challenge: store 3 students (each with name, marks list); print the topper's name.
11. Remove the item with key `"temp"` safely (may be missing) from a dict.
12. Create a config dict with a nested `database` section and read the host/port safely.
13. Write code that counts each character in a string using `counts[ch] = counts.get(ch, 0) + 1`.
14. What is the output of `{1: "a", 1.0: "b"}`? Try it — why does it happen?
15. Write a program that stores user input (name, age, city) into a dict and prints a summary.

---

# 20. Mini Project: Phone Book Manager

A small interactive phone book using a dictionary. Run this in a `.py` file:

```python
phone_book = {}

def add(name, number):
    phone_book[name] = number
    print(f"Added {name}: {number}")

def remove(name):
    if name in phone_book:
        del phone_book[name]
        print(f"Removed {name}")
    else:
        print(f"{name} not found")

def show(name):
    number = phone_book.get(name)
    if number:
        print(f"{name}: {number}")
    else:
        print(f"{name} not found")

def list_all():
    if not phone_book:
        print("Phone book is empty")
    else:
        for name, number in phone_book.items():
            print(f"{name}: {number}")

while True:
    print("\n1. Add  2. Remove  3. Search  4. List all  5. Exit")
    choice = input("Choose an option: ")
    if choice == "1":
        name = input("Name: ")
        number = input("Number: ")
        add(name, number)
    elif choice == "2":
        remove(input("Name to remove: "))
    elif choice == "3":
        show(input("Name to search: "))
    elif choice == "4":
        list_all()
    elif choice == "5":
        print("Goodbye!")
        break
    else:
        print("Invalid option")
```

**Sample run:**
```
1. Add  2. Remove  3. Search  4. List all  5. Exit
Choose an option: 1
Name: Alice
Number: 9876543210
Added Alice: 9876543210

1. Add  2. Remove  3. Search  4. List all  5. Exit
Choose an option: 4
Alice: 9876543210
```

---

*Dictionaries are the backbone of Python — used everywhere from JSON parsing to web
frameworks to data science. Master them and you can structure any kind of real-world data.
Happy coding!*