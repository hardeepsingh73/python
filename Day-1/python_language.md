# Python Programming Language

## Table of Contents

1. [Introduction to Python](#1-introduction-to-python)
2. [Python Character Set](#2-python-character-set)
3. [Variables](#3-variables)
4. [Rules for Identifiers](#4-rules-for-identifiers)
5. [Data Types](#5-data-types)
6. [Keywords](#6-keywords)
7. [Comments in Python](#7-comments-in-python)
8. [Operators](#8-operators)
9. [Type Conversion](#9-type-conversion)
10. [Input in Python](#10-input-in-python)
11. [Quick Revision / Cheat Sheet](#11-quick-revision--cheat-sheet)
12. [Practice Questions](#12-practice-questions)

---

## 1. Introduction to Python

### What is Python?

Python is a high-level, interpreted, general-purpose programming language. It was designed to be easy to read and simple to implement. Python code is written using English-like syntax, which makes it one of the most beginner-friendly programming languages available today.

### History and Background

| Detail | Information |
|---|---|
| **Creator** | Guido van Rossum |
| **First Released** | February 20, 1991 |
| **Latest Stable Version** | Python 3.14 (released October 2025) |
| **License** | Open Source (PSF License) |
| **Website** | https://www.python.org |

Python was conceived in the late 1980s as a successor to the ABC language. Guido van Rossum began implementing Python in December 1989 at Centrum Wiskunde & Informatica (CWI) in the Netherlands. The language was named after the British comedy series *Monty Python's Flying Circus*, not the snake.

### Why Python is Popular

- **Easy to Learn**: Simple syntax that resembles natural English.
- **Versatile**: Used in web development, data science, AI, automation, and more.
- **Large Community**: Millions of developers worldwide contribute and provide support.
- **Rich Ecosystem**: Thousands of libraries and frameworks are available.
- **Cross-Platform**: Runs on Windows, macOS, Linux, and more.
- **Free and Open Source**: No licensing costs.

### Key Features of Python

1. **Interpreted Language** - No compilation needed; code runs line by line.
2. **Dynamically Typed** - No need to declare variable types explicitly.
3. **Extensive Standard Library** - Comes with many built-in modules.
4. **Multiple Programming Paradigms** - Supports procedural, object-oriented, and functional programming.
5. **Automatic Memory Management** - Built-in garbage collector handles memory.
6. **Interactive Mode** - Test code snippets directly in the Python interpreter.

### Advantages and Disadvantages

**Advantages:**
- Beginner-friendly syntax
- Rapid development and prototyping
- Extensive library support
- Strong community backing
- Cross-platform compatibility

**Disadvantages:**
- Slower execution speed compared to compiled languages like C/C++
- Not ideal for mobile development
- Global Interpreter Lock (GIL) limits true multi-threading
- High memory consumption

### Common Applications of Python

| Application Area | Examples |
|---|---|
| Web Development | Django, Flask, FastAPI |
| Data Science & Analytics | Pandas, NumPy, Matplotlib |
| Machine Learning & AI | TensorFlow, PyTorch, scikit-learn |
| Automation / Scripting | File handling, web scraping, task automation |
| Game Development | Pygame, Panda3D |
| Desktop Applications | Tkinter, PyQt |
| Cybersecurity | Penetration testing tools, network scanners |
| DevOps | Ansible, SaltStack |

### Python Versions

Python has two major version lines:
- **Python 2** (legacy, officially end-of-life since January 1, 2020)
- **Python 3** (current and recommended)

Always use **Python 3** for new projects. The currently recommended stable version is **Python 3.13 or 3.14** (Python 3.12 also works with the examples in this guide).

### Hello, World! Program

The simplest Python program prints a message to the screen:

```python
print("Hello, World!")
```

**Output:**
```
Hello, World!
```

### How Python Code is Executed

1. You write Python code in a file with a `.py` extension (e.g., `hello.py`).
2. The Python interpreter reads the file.
3. The interpreter translates your code into **bytecode** (an intermediate form).
4. The bytecode is executed by the **Python Virtual Machine (PVM)**.
5. Results or output are displayed.

```bash
# Running a Python file from the command line
python hello.py
```

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using Python 2 syntax | Use Python 3 syntax |
| Forgetting quotation marks around strings | Use `"text"` or `'text'` |
| Mixing tabs and spaces for indentation | Use 4 spaces consistently |

---

## 2. Python Character Set

The **character set** defines the valid characters that can be used in a Python program. Python supports a wide range of characters.

### Letters

Both uppercase and lowercase English alphabets are valid:

```
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
a b c d e f g h i j k l m n o p q r s t u v w x y z
```

### Digits

Numeric characters from 0 to 9:

```
0 1 2 3 4 5 6 7 8 9
```

### Special Characters

```
! @ # $ % ^ & * ( ) - _ + = [ ] { } | \ : ; " ' < > , . / ? ~ `
```

### Whitespace Characters

| Character | Description |
|---|---|
| Space (` `) | Regular space |
| Tab (`\t`) | Horizontal tab |
| Newline (`\n`) | Line break |
| Carriage return (`\r`) | Carriage return |
| Form feed (`\f`) | Form feed |

### Escape Characters

Escape characters start with a backslash (`\`) and represent special characters:

| Escape Sequence | Description |
|---|---|
| `\n` | Newline |
| `\t` | Tab |
| `\\` | Backslash |
| `\'` | Single quote |
| `\"` | Double quote |
| `\r` | Carriage return |
| `\0` | Null character |
| `\b` | Backspace |

```python
# Using escape characters
print("Line1\nLine2")    # Newline
print("Name:\tAlice")    # Tab
print("Path: C:\\Users") # Backslash
```

**Output:**
```
Line1
Line2
Name:	Alice
Path: C:\Users
```

### Unicode Support

Python 3 supports **Unicode** by default, meaning you can use characters from virtually any writing system:

```python
print("Hello")           # English
print("Hola")            # Spanish
print("Bonjour")         # French
print("123")             # Digits as string
print("Hello @ # $ %")  # Special characters
```

**Output:**
```
Hello
Hola
Bonjour
123
Hello @ # $ %
```

---

## 3. Variables

### What is a Variable?

A variable is a named container that stores a value in memory. Think of it as a labeled box where you can put data inside and retrieve it later by using the label.

### Creating Variables

In Python, you create a variable simply by assigning a value to a name. No declaration keyword is needed.

```python
name = "Alice"
age = 25
height = 5.6
is_student = True
```

### Variable Assignment

The `=` operator is used to assign a value to a variable. The value is stored on the right side, and the variable name is on the left side.

```python
# Basic assignment
x = 10
print(x)  # Output: 10
```

### Dynamic Typing

Python is **dynamically typed**, meaning you do not need to specify the data type of a variable. The type is determined automatically at runtime.

```python
x = 10        # x is an integer
x = "Hello"   # x is now a string (type changed automatically)
x = 3.14      # x is now a float
```

### Multiple Variable Assignment

You can assign values to multiple variables in a single line:

```python
# Method 1: Multiple assignment
a, b, c = 1, 2, 3
print(a, b, c)  # Output: 1 2 3

# Method 2: Unpacking a sequence
x, y, z = "apple", "banana", "cherry"
print(x, y, z)  # Output: apple banana cherry
```

### Assigning the Same Value to Multiple Variables

```python
# All three variables point to the same value
a = b = c = 0
print(a, b, c)  # Output: 0 0 0
```

### Reassigning Variables

Variables can be reassigned to different values and even different types at any time:

```python
x = 5
print(x)  # Output: 5

x = 20
print(x)  # Output: 20

x = "Now I am a string"
print(x)  # Output: Now I am a string
```

### Variables with Different Data Types

```python
integer_var = 100
float_var = 99.5
string_var = "Python"
boolean_var = True
list_var = [1, 2, 3]
tuple_var = (4, 5, 6)
dict_var = {"key": "value"}
```

### Constants Convention

Python does not have true constants, but by convention, variables meant to be constants are written in **UPPERCASE**:

```python
PI = 3.14159
MAX_SIZE = 100
APP_NAME = "MyApp"
```

> Note: This is only a convention. Python will not prevent you from reassigning these variables.

### Good Naming Practices

| Practice | Example |
|---|---|
| Use descriptive names | `user_name` instead of `x` |
| Use snake_case for variables | `first_name`, `total_price` |
| Use UPPER_CASE for constants | `MAX_VALUE`, `API_KEY` |
| Avoid single-letter names (unless in loops) | Use `count` instead of `c` |
| Avoid using Python built-in names | Do not name a variable `list` or `print` |

```python
# Good naming examples
student_name = "Alice"
total_score = 95.5
MAX_RETRY_COUNT = 3

# Bad naming examples (avoid these)
x = "Alice"          # Not descriptive
STUDENTNAME = "Alice" # Hard to read
```

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using a keyword as a variable name | Use a different name (e.g., `my_list` not `list`) |
| Starting a variable name with a number | Start with a letter or underscore |
| Not initializing a variable before use | Assign a value before using |
| Using reserved built-in names | Avoid names like `print`, `input`, `type` |

---

## 4. Rules for Identifiers

### What is an Identifier?

An identifier is a name given to a variable, function, class, module, or other entity in Python. Identifiers are how you refer to these entities in your code.

### Rules for Identifiers

1. **Must begin with a letter (A-Z or a-z) or an underscore (`_`).**
2. **Cannot begin with a digit (0-9).**
3. **Can contain letters, digits, and underscores only.**
4. **Cannot contain spaces or special characters** (like `@`, `#`, `$`, `%`, etc.).
5. **Identifiers are case-sensitive** (`name`, `Name`, and `NAME` are three different identifiers).
6. **Cannot use Python keywords as identifiers.**

### Valid vs Invalid Identifiers

| Identifier | Valid? | Reason |
|---|---|---|
| `my_variable` | ✅ Valid | Starts with a letter, uses underscores |
| `_private_var` | ✅ Valid | Starts with an underscore |
| `count2` | ✅ Valid | Contains letters and digits |
| `MAX_VALUE` | ✅ Valid | All uppercase with underscore |
| `userName` | ✅ Valid | Contains letters (camelCase) |
| `2variable` | ❌ Invalid | Starts with a digit |
| `my variable` | ❌ Invalid | Contains a space |
| `my-var` | ❌ Invalid | Contains a hyphen (special character) |
| `$price` | ❌ Invalid | Starts with a special character |
| `my@var` | ❌ Invalid | Contains `@` |
| `for` | ❌ Invalid | `for` is a keyword |
| `print` | ⚠️ Not Recommended | `print` is a built-in function |
| `_` | ✅ Valid | Single underscore is allowed |

### Naming Conventions

| Convention | Description | Example |
|---|---|---|
| `snake_case` | All lowercase with underscores; used for variables and functions | `my_variable`, `calculate_total()` |
| `PascalCase` | Each word starts with a capital letter; used for classes | `MyClass`, `StudentRecord` |
| `camelCase` | First word lowercase, rest capitalized; less common in Python | `myVariable` |
| `_private` | Leading underscore indicates private/internal use | `_internal_var` |
| `__double_leading` | Name mangling for class-specific attributes | `__private_attr` |
| `UPPER_CASE` | All uppercase with underscores; used for constants | `MAX_SIZE`, `API_URL` |

```python
# snake_case (Pythonic way for variables and functions)
student_name = "Alice"
def calculate_area():
    pass

# PascalCase (for class names)
class StudentRecord:
    pass

# UPPER_CASE (for constants)
MAX_SIZE = 100
```

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using hyphens in names | Use underscores: `my_var` not `my-var` |
| Using spaces in names | Use underscores: `first_name` not `first name` |
| Using built-in function names as variables | Rename: `my_list` not `list` |
| Using non-English characters (risky) | Stick to ASCII letters and underscores |

---

## 5. Data Types

Data types define the kind of value a variable can hold and what operations can be performed on it. Python has several built-in data types.

### Overview of Built-in Data Types

| Data Type | Category | Mutable? | Example |
|---|---|---|---|
| `int` | Numeric | Immutable | `42` |
| `float` | Numeric | Immutable | `3.14` |
| `complex` | Numeric | Immutable | `2 + 3j` |
| `bool` | Boolean | Immutable | `True` |
| `str` | Text | Immutable | `"Hello"` |
| `list` | Sequence | Mutable | `[1, 2, 3]` |
| `tuple` | Sequence | Immutable | `(1, 2, 3)` |
| `set` | Set | Mutable | `{1, 2, 3}` |
| `dict` | Mapping | Mutable | `{"key": "value"}` |
| `NoneType` | Special | Immutable | `None` |

### Detailed Explanation of Each Data Type

#### 1. int (Integer)

Integers are whole numbers without a decimal point. They can be positive, negative, or zero.

```python
a = 10
b = -5
c = 0
large_number = 1_000_000  # Underscores for readability (Python 3.6+)

print(type(a))  # Output: <class 'int'>
print(type(b))  # Output: <class 'int'>
```

**Common use case:** Counting, indexing, and any whole number operations.

**Important characteristics:**
- No size limit (Python supports arbitrarily large integers)
- Supports standard arithmetic operations

---

#### 2. float (Floating-Point)

Floats are numbers with a decimal point.

```python
pi = 3.14159
temperature = -2.5
scientific = 1.5e2  # 150.0 (scientific notation)

print(type(pi))  # Output: <class 'float'>
```

**Common use case:** Measurements, calculations requiring decimal precision.

**Important characteristics:**
- Limited precision (approximately 15-17 decimal digits)
- Can represent very large or very small numbers using scientific notation

---

#### 3. complex (Complex Number)

Complex numbers have a real and an imaginary part.

```python
z = 3 + 4j
real_part = z.real    # 3.0
imaginary_part = z.imag  # 4.0

print(type(z))  # Output: <class 'complex'>
```

**Common use case:** Scientific and engineering calculations.

---

#### 4. bool (Boolean)

Boolean values represent truth values: `True` or `False`.

```python
is_active = True
is_admin = False

print(type(is_active))  # Output: <class 'bool'>

# Booleans are a subclass of integers
print(True + True)   # Output: 2
print(False * 10)    # Output: 0
```

**Common use case:** Conditions, flags, logical operations.

**Important characteristics:**
- `bool` is a subclass of `int`
- `True` equals `1`, `False` equals `0`

---

#### 5. str (String)

Strings are sequences of characters enclosed in quotes.

```python
name = "Alice"
greeting = 'Hello, World!'
multi_line = """This is
a multi-line
string."""
empty = ""

print(type(name))  # Output: <class 'str'>
print(len(name))   # Output: 5
```

**Common use case:** Text manipulation, data display, file paths.

**Important characteristics:**
- Immutable (cannot change individual characters after creation)
- Supports indexing and slicing
- Supports concatenation (`+`) and repetition (`*`)

```python
# String operations
first = "Hello"
second = "World"
combined = first + " " + second  # "Hello World"
repeated = "Ha" * 3             # "HaHaHa"
```

---

#### 6. list (List)

Lists are ordered, mutable collections that can hold multiple items.

```python
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
nested = [[1, 2], [3, 4]]
empty = []

print(type(numbers))  # Output: <class 'list'>
print(numbers[0])     # Output: 1
```

**Common use case:** Collections of items that need to be modified.

**Important characteristics:**
- Ordered (maintains insertion order)
- Mutable (can add, remove, and change elements)
- Allows duplicate values
- Can contain elements of different types

---

#### 7. tuple (Tuple)

Tuples are ordered, immutable collections.

```python
coordinates = (10, 20)
colors = ("red", "green", "blue")
single = (42,)      # Note the comma for single-element tuple
empty = ()

print(type(coordinates))  # Output: <class 'tuple'>
print(colors[1])          # Output: green
```

**Common use case:** Fixed collections of data, dictionary keys, function return values.

**Important characteristics:**
- Ordered
- Immutable (cannot be modified after creation)
- Allows duplicate values
- Faster than lists for iteration

---

#### 8. set (Set)

Sets are unordered collections of unique elements.

```python
numbers = {1, 2, 3, 4, 5}
mixed_set = {1, "hello", 3.14}
empty_set = set()  # Note: {} creates an empty dict, not a set

print(type(numbers))  # Output: <class 'set'>
```

**Common use case:** Removing duplicates, membership testing, set operations.

**Important characteristics:**
- Unordered (no indexing)
- No duplicate elements
- Mutable (can add and remove elements)
- Supports mathematical set operations (union, intersection, difference)

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)   # Union: {1, 2, 3, 4, 5}
print(a & b)   # Intersection: {3}
print(a - b)   # Difference: {1, 2}
```

---

#### 9. dict (Dictionary)

Dictionaries are collections of key-value pairs.

```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

empty_dict = {}

print(type(student))   # Output: <class 'dict'>
print(student["name"]) # Output: Alice
```

**Common use case:** Storing structured data, JSON-like data, lookups.

**Important characteristics:**
- Key-value pairs
- Keys must be immutable (strings, numbers, tuples)
- Mutable
- Keys must be unique within a dictionary

---

#### 10. NoneType

`None` represents the absence of a value.

```python
result = None

print(type(result))  # Output: <class 'NoneType'>
print(result is None)  # Output: True
```

**Common use case:** Default values, representing absence of data, functions that do not return a value.

---

### Mutable vs Immutable Data Types

| Mutable (Can Change) | Immutable (Cannot Change) |
|---|---|
| `list` | `int` |
| `dict` | `float` |
| `set` | `complex` |
| | `bool` |
| | `str` |
| | `tuple` |
| | `NoneType` |

```python
# Immutable example
name = "Alice"
# name[0] = "B"  # This would cause an error!
name = "Bob"      # Reassigning creates a new object

# Mutable example
numbers = [1, 2, 3]
numbers[0] = 10   # This works! [10, 2, 3]
numbers.append(4) # [10, 2, 3, 4]
```

### Checking the Type of a Value

Use the `type()` function:

```python
print(type(42))         # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type("hello"))    # <class 'str'>
print(type(True))       # <class 'bool'>
print(type([1, 2]))     # <class 'list'>
print(type((1, 2)))     # <class 'tuple'>
print(type({1, 2}))     # <class 'set'>
print(type({"a": 1}))   # <class 'dict'>
print(type(None))       # <class 'NoneType'>
```

You can also use `isinstance()` to check:

```python
x = 42
print(isinstance(x, int))    # True
print(isinstance(x, float))  # False
```

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using `{}` to create an empty set | Use `set()` for empty sets |
| Forgetting the comma in single-element tuples | Write `(42,)` not `(42)` |
| Assuming floats are perfectly precise | Be aware of floating-point rounding |
| Trying to modify immutable types | Reassign the variable instead |

---

## 6. Keywords

### What are Keywords?

Keywords are **reserved words** in Python that have special meanings. They are used to define the syntax and structure of the language. You **cannot** use keywords as variable names, function names, or any other identifiers.

### Why Keywords Cannot Be Used as Identifiers

Python uses keywords to recognize language constructs. If you try to use a keyword as an identifier, Python will raise a `SyntaxError` because it cannot distinguish between the keyword and your variable.

```python
# This will cause an error
for = 10  # SyntaxError: invalid syntax
```

### Python Keywords (Python 3.12+)

From Python 3.12 onward there are **35 keywords**:

| Keyword | Description |
|---|---|
| `False` | Boolean false value |
| `None` | Represents absence of a value |
| `True` | Boolean true value |
| `and` | Logical AND operator |
| `as` | Create an alias (with import or with statement) |
| `assert` | Assert that a condition is true |
| `async` | Declare an asynchronous function |
| `await` | Wait for an asynchronous result |
| `break` | Exit the current loop |
| `class` | Define a class |
| `continue` | Skip to the next loop iteration |
| `def` | Define a function |
| `del` | Delete a reference |
| `elif` | Else if condition (in if-elif-else) |
| `else` | Default block in conditionals/loops |
| `except` | Handle an exception |
| `finally` | Block that always executes (try-except) |
| `for` | Loop over a sequence |
| `from` | Import specific parts of a module |
| `global` | Declare a global variable |
| `if` | Conditional statement |
| `import` | Import a module |
| `in` | Check membership / loop iteration |
| `is` | Identity comparison |
| `lambda` | Create an anonymous function |
| `nonlocal` | Access a variable in the enclosing scope |
| `not` | Logical NOT operator |
| `or` | Logical OR operator |
| `pass` | Null operation (do nothing) |
| `raise` | Raise an exception |
| `return` | Return a value from a function |
| `try` | Try a block of code for exceptions |
| `while` | Loop while a condition is true |
| `with` | Context manager (resource handling) |
| `yield` | Produce a value from a generator |

### Checking Python Keywords Programmatically

Python provides a built-in `keyword` module:

```python
import keyword

# Print all keywords
print(keyword.kwlist)

# Check if a word is a keyword
print(keyword.iskeyword("for"))     # True
print(keyword.iskeyword("hello"))   # False
```

### Quick Example Using Keywords

```python
# Demonstrating several keywords
import keyword

for word in ["for", "if", "while", "my_var", "class"]:
    if keyword.iskeyword(word):
        print(f"'{word}' is a keyword")
    else:
        print(f"'{word}' is NOT a keyword")
```

**Output:**
```
'for' is a keyword
'if' is a keyword
'while' is a keyword
'my_var' is NOT a keyword
'class' is a keyword
```

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using `True`/`False` with wrong capitalization | Write `True` and `False` exactly |
| Using `None` as a variable name | Use `result` or `value` instead |
| Using `class` as a variable name | Use `class_name` instead |

---

## 7. Comments in Python

### What are Comments?

Comments are notes in your code that are ignored by the Python interpreter. They are meant for human readers to understand the code better.

### Why Comments are Useful

- Explain what the code does
- Make code easier to understand and maintain
- Help other developers (and your future self)
- Mark temporary code or todo items

### Single-Line Comments

Use the hash symbol (`#`) to write a comment on a single line:

```python
# This is a single-line comment
name = "Alice"  # This is an inline comment

# Calculate the area of a rectangle
length = 10
width = 5
area = length * width
```

### Multi-Line Comments

Python does not have a dedicated multi-line comment syntax. You can use multiple `#` lines:

```python
# This is a multi-line comment
# written using multiple hash symbols.
# Each line starts with #.
# It is commonly used for longer explanations.
```

### Docstrings (Documentation Strings)

Docstrings are strings written at the beginning of modules, functions, classes, or methods using triple quotes (`""" """` or `''' '''`). They are used to document what the code does.

```python
"""This module provides utility functions for data processing."""

def calculate_average(numbers):
    """
    Calculate the average of a list of numbers.

    Parameters:
        numbers (list): A list of numerical values.

    Returns:
        float: The average of the numbers.
    """
    return sum(numbers) / len(numbers)
```

You can access docstrings at runtime:

```python
print(calculate_average.__doc__)
```

### Comments vs Docstrings

| Feature | Comments | Docstrings |
|---|---|---|
| Syntax | `# comment` | `"""documentation"""` |
| Purpose | Explain code logic | Document code behavior |
| Accessible at runtime | No | Yes (via `__doc__`) |
| Placement | Anywhere in code | Beginning of module/function/class |
| PEP 257 | Not covered | Defined by PEP 257 |

### Best Practices for Writing Comments

**Good comments:**
```python
# Calculate the total price after applying a 10% discount
discount = 0.10
total = price * (1 - discount)
```

**Bad comments (avoid these):**
```python
# This variable stores the discount
discount = 0.10  # Obvious and unnecessary
# I am writing this code to do something important
# TODO: fix this later
```

### Guidelines:
- Write comments that explain **why**, not **what**.
- Keep comments up to date with code changes.
- Do not over-comment obvious code.
- Use docstrings for all public functions and classes.

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using `//` for comments (like in C/Java) | Use `#` for comments in Python |
| Forgetting to close triple quotes in docstrings | Always use matching `"""` pairs |
| Commenting out code and forgetting to remove it | Clean up old commented code |

---

## 8. Operators

Operators are special symbols that perform operations on values (operands).

### Arithmetic Operators

Used for mathematical calculations:

| Operator | Name | Example | Output |
|---|---|---|---|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `5 / 3` | `1.6667` |
| `//` | Floor Division | `5 // 3` | `1` |
| `%` | Modulus (remainder) | `5 % 3` | `2` |
| `**` | Exponentiation | `5 ** 3` | `125` |

```python
print(10 + 3)   # 13
print(10 - 3)   # 7
print(10 * 3)   # 30
print(10 / 3)   # 3.3333333333333335
print(10 // 3)  # 3
print(10 % 3)   # 1
print(10 ** 3)  # 1000
```

### Assignment Operators

Used to assign and update values:

| Operator | Example | Equivalent To |
|---|---|---|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `//=` | `x //= 3` | `x = x // 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `**=` | `x **= 3` | `x = x ** 3` |

```python
x = 10
x += 5   # x is now 15
x *= 2   # x is now 30
x -= 10  # x is now 20
print(x) # Output: 20
```

### Comparison Operators

Used to compare two values. They always return `True` or `False`:

| Operator | Name | Example | Output |
|---|---|---|---|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal to | `5 >= 5` | `True` |
| `<=` | Less than or equal to | `5 <= 3` | `False` |

```python
print(10 == 10)  # True
print(10 != 5)   # True
print(10 > 5)    # True
print(10 < 5)    # False
print(10 >= 10)  # True
print(10 <= 5)   # False
```

### Logical Operators

Used to combine conditional statements:

| Operator | Description | Example | Output |
|---|---|---|---|
| `and` | True if both conditions are true | `True and False` | `False` |
| `or` | True if at least one condition is true | `True or False` | `True` |
| `not` | Reverses the boolean value | `not True` | `False` |

```python
x = 10

print(x > 5 and x < 20)  # True  (both conditions true)
print(x > 5 or x < 3)    # True  (first condition true)
print(not (x > 5))       # False (reverses True to False)
```

### Bitwise Operators

Used to perform operations on binary representations of integers:

| Operator | Name | Example | Output | Explanation |
|---|---|---|---|---|
| `&` | AND | `5 & 3` | `1` | `101 & 011 = 001` |
| `\|` | OR | `5 \| 3` | `7` | `101 \| 011 = 111` |
| `^` | XOR | `5 ^ 3` | `6` | `101 ^ 011 = 110` |
| `~` | NOT | `~5` | `-6` | Inverts all bits |
| `<<` | Left Shift | `5 << 1` | `10` | `101 << 1 = 1010` |
| `>>` | Right Shift | `5 >> 1` | `2` | `101 >> 1 = 10` |

```python
a = 5    # Binary: 101
b = 3    # Binary: 011

print(a & b)   # 1
print(a | b)   # 7
print(a ^ b)   # 6
print(a << 1)  # 10
print(a >> 1)  # 2
```

### Membership Operators

Used to test if a value is found in a sequence (string, list, tuple, set, dict):

| Operator | Description | Example | Output |
|---|---|---|---|
| `in` | True if value is found | `"a" in "apple"` | `True` |
| `not in` | True if value is not found | `"x" in "apple"` | `False` |

```python
fruits = ["apple", "banana", "cherry"]

print("apple" in fruits)      # True
print("grape" in fruits)      # False
print("grape" not in fruits)  # True
print("H" in "Hello")         # True
```

### Identity Operators

Used to compare the memory locations of two objects:

| Operator | Description | Example | Output |
|---|---|---|---|
| `is` | True if both variables point to the same object | `a is b` | Depends |
| `is not` | True if variables point to different objects | `a is not b` | Depends |

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a is b)       # False (same values, different objects)
print(a is c)       # True  (same object)
print(a == b)       # True  (same values)
print(a is not b)   # True
```

> Note: Use `==` to compare values, and `is` to compare object identity.

### Operator Precedence

Python evaluates operators in a specific order, from highest to lowest precedence:

| Precedence | Operator | Description |
|---|---|---|
| 1 (Highest) | `**` | Exponentiation |
| 2 | `~`, `+`, `-` | Unary NOT, unary plus, unary minus |
| 3 | `*`, `/`, `//`, `%` | Multiplication, division, floor division, modulus |
| 4 | `+`, `-` | Addition, subtraction |
| 5 | `<<`, `>>` | Bitwise shifts |
| 6 | `&` | Bitwise AND |
| 7 | `^` | Bitwise XOR |
| 8 | `\|` | Bitwise OR |
| 9 | `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in` | Comparison, identity, membership |
| 10 | `not` | Logical NOT |
| 11 | `and` | Logical AND |
| 12 (Lowest) | `or` | Logical OR |

```python
# Precedence example
result = 2 + 3 * 4      # 14 (multiplication before addition)
result = (2 + 3) * 4    # 20 (parentheses have highest precedence)
result = 2 ** 3 ** 2    # 512 (right to left: 2 ** 9)
```

> Tip: Use parentheses `()` to make the order of operations clear, even when not strictly necessary.

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| Using `=` for comparison instead of `==` | Use `==` to compare values |
| Using `is` to compare values | Use `==` for value comparison |
| Forgetting operator precedence | Use parentheses to clarify |
| Confusing `//` with `/` | `//` is floor division, `/` is regular division |

---

## 9. Type Conversion

### What is Type Conversion?

Type conversion (also called **type casting**) is the process of converting a value from one data type to another.

### Implicit Type Conversion (Automatic)

Python automatically converts one type to another when safe. This is done by the Python interpreter without any explicit instruction.

```python
# int to float (automatic)
x = 10
y = 3.5
result = x + y  # x is automatically converted to float
print(result)   # Output: 13.5
print(type(result))  # Output: <class 'float'>

# bool to int (automatic)
print(True + 5)   # Output: 6 (True becomes 1)
print(False + 5)  # Output: 5 (False becomes 0)
```

**Rules of implicit conversion:**
- `bool` can be implicitly converted to `int` or `float`, but not the reverse for all cases.
- `int` can be implicitly converted to `float`.
- Lower types are promoted to higher types to prevent data loss.

### Explicit Type Conversion (Casting)

You manually convert a value from one type to another using built-in functions.

| Function | Converts To | Example | Output |
|---|---|---|---|
| `int()` | Integer | `int("42")` | `42` |
| `int()` | Float to int | `int(3.9)` | `3` (truncates, does not round) |
| `float()` | Float | `float("3.14")` | `3.14` |
| `float()` | Int to float | `float(5)` | `5.0` |
| `str()` | String | `str(42)` | `"42"` |
| `bool()` | Boolean | `bool(1)` | `True` |
| `complex()` | Complex | `complex(3, 4)` | `(3+4j)` |
| `list()` | List | `list("abc")` | `['a', 'b', 'c']` |
| `tuple()` | Tuple | `tuple([1,2])` | `(1, 2)` |
| `set()` | Set | `set([1,1,2])` | `{1, 2}` |

#### int()

```python
print(int("42"))      # 42
print(int(3.9))       # 3 (truncates towards zero)
print(int(-3.9))      # -3
print(int(True))      # 1
print(int("3.14"))    # Error! Cannot convert float string directly
```

#### float()

```python
print(float("3.14"))  # 3.14
print(float(5))       # 5.0
print(float("10"))    # 10.0
print(float("abc"))   # Error! Invalid literal
```

#### str()

```python
print(str(42))        # "42"
print(str(3.14))      # "3.14"
print(str(True))      # "True"
print(str(None))      # "None"
```

#### bool()

```python
print(bool(1))        # True
print(bool(0))        # False
print(bool("hello"))  # True
print(bool(""))       # False (empty string)
print(bool([]))       # False (empty list)
print(bool([0]))      # True (non-empty list)
print(bool(None))     # False
```

#### list(), tuple(), set()

```python
# String to list
print(list("Python"))  # ['P', 'y', 't', 'h', 'o', 'n']

# String to tuple
print(tuple("Python"))  # ('P', 'y', 't', 'h', 'o', 'n')

# List to set (removes duplicates)
print(set([1, 1, 2, 3, 3]))  # {1, 2, 3}

# Tuple to list
print(list((1, 2, 3)))  # [1, 2, 3]
```

### Common Errors in Type Conversion

```python
# Error 1: Converting non-numeric string to int
# int("hello")  # ValueError: invalid literal

# Error 2: Converting float string to int directly
# int("3.14")   # ValueError: invalid literal
# Fix:
print(int(float("3.14")))  # 3

# Error 3: Converting invalid value
# int("10.5")   # ValueError
```

### Summary Table: Valid and Invalid Conversions

| Conversion | Valid? | Example | Result |
|---|---|---|---|
| `int("42")` | ✅ | String to int | `42` |
| `int("3.14")` | ❌ | Float string to int | Error |
| `int(float("3.14"))` | ✅ | Float string → float → int | `3` |
| `float("3.14")` | ✅ | String to float | `3.14` |
| `float("abc")` | ❌ | Non-numeric string | Error |
| `str(42)` | ✅ | Int to string | `"42"` |
| `bool(0)` | ✅ | Zero to bool | `False` |
| `bool("")` | ✅ | Empty string to bool | `False` |

---

### Common Mistakes

| Mistake | Correction |
|---|---|
| `int("3.14")` raises ValueError | Use `int(float("3.14"))` |
| Assuming `int()` rounds | `int()` truncates; use `round()` for rounding |
| Forgetting `bool("")` is `False` | Empty strings, 0, None, and empty collections are `False` |
| Confusing `str(10)` with `10` | `str(10)` is `"10"` (a string), not the number `10` |

---

## 10. Input in Python

### Basic input() Syntax

The `input()` function reads a line of text from the user (from the keyboard).

```python
variable_name = input("Prompt message: ")
```

- The string inside `input()` is a prompt displayed to the user.
- The function always returns the input as a **string**.

### Reading Strings

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")
```

**Output:**
```
Enter your name: Alice
Hello, Alice!
```

### Reading Integers

Since `input()` returns a string, you must convert it:

```python
age = int(input("Enter your age: "))
print("You will be", age + 1, "next year.")
```

**Output:**
```
Enter your age: 25
You will be 26 next year.
```

### Reading Floating-Point Numbers

```python
height = float(input("Enter your height in meters: "))
print("Your height is", height, "meters.")
```

**Output:**
```
Enter your height in meters: 5.6
Your height is 5.6 meters.
```

### Taking Multiple Inputs

#### Using split()

```python
# Take two numbers separated by space
a, b = input("Enter two numbers: ").split()
a = int(a)
b = int(b)
print("Sum:", a + b)
```

**Output:**
```
Enter two numbers: 10 20
Sum: 30
```

#### Using map()

```python
# Take two numbers in one line
a, b = map(int, input("Enter two numbers: ").split())
print("Sum:", a + b)
```

**Output:**
```
Enter two numbers: 15 25
Sum: 40
```

#### Taking multiple space-separated values

```python
# Take three floats in one line
x, y, z = map(float, input("Enter three numbers: ").split())
print("Average:", (x + y + z) / 3)
```

**Output:**
```
Enter three numbers: 10 20 30
Average: 20.0
```

### Input Validation Basics

Since `input()` always returns a string, invalid conversions will cause errors. You can use `try`/`except` to handle this:

```python
try:
    age = int(input("Enter your age: "))
    if age < 0:
        print("Age cannot be negative.")
    else:
        print("Your age is", age)
except ValueError:
    print("Invalid input. Please enter a whole number.")
```

**Output (invalid input):**
```
Enter your age: abc
Invalid input. Please enter a whole number.
```

### Common Mistakes When Using input()

| Mistake | Example | Problem | Fix |
|---|---|---|---|
| Forgetting to convert | `age = input("Age: ")` | `age` is a string | `age = int(input(...))` |
| Converting wrong type | `int("hello")` | ValueError | Use validation |
| Confusing `input()` return type | `num = input("Num: ")` | Always returns `str` | Always convert if needed |
| Not handling empty input | User just presses Enter | May cause errors | Add validation |

### Practical Examples

#### Example 1: Taking User's Name
```python
name = input("What is your name? ")
print("Welcome to Python,", name + "!")
```

#### Example 2: Taking Age
```python
age = int(input("How old are you? "))
if age >= 18:
    print("You are an adult.")
else:
    print("You are a minor.")
```

#### Example 3: Adding Two Numbers
```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))
result = num1 + num2
print("The sum is:", result)
```

#### Example 4: Taking Multiple Numbers in One Line
```python
numbers = list(map(int, input("Enter numbers separated by space: ").split()))
print("You entered:", numbers)
print("Sum:", sum(numbers))
print("Average:", sum(numbers) / len(numbers))
```

**Output:**
```
Enter numbers separated by space: 10 20 30 40 50
You entered: [10, 20, 30, 40, 50]
Sum: 150
Average: 30.0
```

---

## 11. Quick Revision / Cheat Sheet

### Variables
```python
name = "Alice"          # String
age = 25                # Integer
height = 5.6            # Float
is_student = True       # Boolean
```

### Data Types
| Type | Example | Mutable |
|---|---|---|
| `int` | `42` | No |
| `float` | `3.14` | No |
| `complex` | `2+3j` | No |
| `bool` | `True` | No |
| `str` | `"hello"` | No |
| `list` | `[1, 2, 3]` | Yes |
| `tuple` | `(1, 2, 3)` | No |
| `set` | `{1, 2, 3}` | Yes |
| `dict` | `{"a": 1}` | Yes |
| `NoneType` | `None` | No |

### Operators
```python
# Arithmetic: + - * / // % **
# Comparison: == != > < >= <=
# Logical: and or not
# Assignment: = += -= *= /= //= %= **=
# Membership: in not in
# Identity: is is not
```

### Type Conversion
```python
int("42")       # String to int
float("3.14")   # String to float
str(42)         # Int to string
bool(0)         # To boolean (False)
list("abc")     # To list ['a','b','c']
```

### Input/Output
```python
name = input("Enter name: ")     # Read string
age = int(input("Enter age: "))  # Read integer
print("Hello,", name)            # Print output
```

### Comments
```python
# Single line comment
"""
Multi-line
comment / docstring
"""
```

### Keywords
```python
import keyword
print(keyword.kwlist)  # View all keywords
```

### Checking Types
```python
type(x)            # Returns the type
isinstance(x, int) # Checks if x is an int
```

---

## 12. Practice Questions

### Section 1: Variables and Identifiers

**1.** Create a variable called `first_name` and assign your name to it. Then print it.

**2.** What will happen if you try to run `2name = "Alice"`? Why?

**3.** Write a program that swaps the values of two variables without using a third variable.

**4.** Identify which of the following are valid identifiers and explain why the invalid ones are invalid:
- `_count`
- `2nd_place`
- `my-name`
- `totalScore`
- `for`
- `__init__`

**5.** Assign the same value `0` to three variables `a`, `b`, and `c` in a single line.

### Section 2: Data Types

**6.** What is the data type of each of the following?
- `42`
- `3.14`
- `"True"`
- `True`
- `[1, 2, 3]`
- `(1, 2)`
- `{1, 2, 3}`
- `None`
- `{"name": "Alice"}`

**7.** Write a program to check whether a given value is a string, integer, or float using `type()`.

**8.** What is the difference between a list and a tuple? Give one example of each.

**9.** What is the difference between a mutable and immutable data type? Name two of each.

**10.** Why does `set()` need parentheses to create an empty set, while `{}` creates an empty dictionary?

### Section 3: Keywords and Comments

**11.** Write a program that checks whether a user-entered word is a Python keyword or not.

**12.** What is the difference between a comment and a docstring?

**13.** Write a single-line comment and a multi-line docstring for a function that adds two numbers.

**14.** How many keywords does Python 3.12+ have? Name any five.

### Section 4: Operators

**15.** What will be the output of the following?
```python
print(10 / 3)
print(10 // 3)
print(10 % 3)
print(2 ** 5)
```

**16.** Write a program that takes the length and width of a rectangle as input and calculates its area and perimeter.

**17.** What is the difference between `==` and `is`? Give an example.

**18.** What will be the output?
```python
print(3 > 2 and 5 < 1)
print(3 > 2 or 5 < 1)
print(not (3 > 2))
```

### Section 5: Type Conversion

**19.** Convert the string `"3.14"` to a float, then to an integer. What is the final result? Why?

**20.** What will `bool("")`, `bool("False")`, `bool(0)`, `bool(None)`, and `bool([1])` return? Explain each.

### Section 6: Input

**21.** Write a program that asks the user for their name and age, then prints a message saying whether they are an adult (18+) or a minor.

**22.** Write a program that takes two numbers as input on the same line (space-separated) and prints their sum, difference, product, and division.

**23.** Write a program that takes a list of numbers (space-separated) from the user and prints the largest and smallest numbers.

**24.** Write a program that takes a temperature in Celsius as input and converts it to Fahrenheit using the formula: `F = (C × 9/5) + 32`.

**25.** What error will you get if you run `int(input("Enter a number: "))` and the user types `hello`? How can you handle this error gracefully?

---

*This documentation covers the fundamental building blocks of Python programming. Practice each concept with hands-on coding exercises to build a strong foundation. Happy coding!*
