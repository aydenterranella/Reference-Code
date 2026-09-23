# Python Reference Sheet

A practical, example-heavy reference for Python. Every code block is meant to be copied, run, and tweaked. Comments after `#` show what a line returns or prints.

> Examples target **Python 3.10+**. Anything that needs a newer version is marked.

---

## Table of Contents

**Basics**
- [Variables & Data Types](#variables--data-types)
- [Comments](#comments)
- [Operators](#operators)
- [Strings](#strings)
- [String Formatting](#string-formatting) ⭐ in depth
- [Input/Output](#inputoutput)

**Control Flow**
- [Conditionals](#conditionals)
- [Loops](#loops) ⭐ in depth

**Data Structures**
- [Lists](#lists)
- [Tuples](#tuples)
- [Sets](#sets)
- [Dictionaries](#dictionaries)
- [Comprehensions](#comprehensions)

**Functions**
- [Functions](#functions)
- [Lambda Functions](#lambda-functions)
- [Map, Filter, Zip](#map-filter-zip)
- [*args and **kwargs](#args-and-kwargs)
- [Common Built-in Functions](#common-built-in-functions)

**Working with Data**
- [Error Handling](#error-handling)
- [File Handling](#file-handling)
- [JSON](#json)
- [Working with Dates & Times](#working-with-dates--times)
- [Regular Expressions](#regular-expressions)

**Going Further**
- [Classes (OOP Basics)](#classes-oop-basics)
- [Modules & Imports](#modules--imports)
- [Decorators](#decorators)
- [Generators](#generators)
- [Unpacking & Advanced Assignment](#unpacking--advanced-assignment)
- [Common Patterns](#common-patterns)
- [Useful Shortcuts](#useful-shortcuts)
- [Code Style (PEP 8)](#code-style-pep-8)
- [Virtual Environments & pip](#virtual-environments--pip)

---

## Variables & Data Types

```python
# Variables (no declaration needed, just assign)
name = "Alice"          # String (str)
age = 25                # Integer (int)
price = 19.99           # Float (decimal number)
is_active = True        # Boolean (True/False, capitalized!)
items = None            # NoneType (means "no value")

# Check type
type(name)              # <class 'str'>
type(age)               # <class 'int'>
isinstance(age, int)    # True
isinstance(price, (int, float))  # True (matches either type)

# Variables can change type at any time
x = 5
x = "five"              # Totally fine in Python

# Multiple assignment
a, b, c = 1, 2, 3
x = y = z = 0           # All three set to 0

# Underscores in numbers are ignored; they're just for readability
population = 8_000_000_000
```

### Naming Rules

```python
user_name = "sam"       # snake_case: the Python convention for variables
MAX_SPEED = 100         # ALL_CAPS: convention for constants (Python won't stop you changing it)
_temp = 3               # Leading underscore: "internal use" by convention
player2 = "Bo"          # Numbers are fine, just not at the start

# 2nd_place = "Al"      # SyntaxError: can't start with a number
# my-var = 1            # SyntaxError: no dashes
# class = "A"           # SyntaxError: can't use keywords (if, for, class, def...)
# Names are case-sensitive: age, Age, and AGE are three different variables
```

### Type Conversion

```python
int("42")               # 42
int(3.99)               # 3 (chops off the decimal, does NOT round)
# int("3.5")            # ValueError! Use int(float("3.5")) instead
float("3.14")           # 3.14
float(7)                # 7.0
str(100)                # "100"
str(3.5)                # "3.5"
bool(0)                 # False
bool(42)                # True
bool("")                # False (empty string)
bool("hi")              # True
bool([])                # False (empty list)
list("abc")             # ["a", "b", "c"]

# "Falsy" values act like False in an if: 0, 0.0, "", [], {}, set(), None, False
# Everything else is "truthy"
```

## Comments

```python
# Single-line comment

x = 5  # Inline comment (two spaces before the #)

"""
Triple-quoted strings are often used as
multi-line comments.
"""

def area(r):
    """Return the area of a circle with radius r."""   # Docstring: describes the function
    return 3.14159 * r ** 2

help(area)              # Prints the docstring
```

## Operators

### Arithmetic

```python
7 + 2       # 9
7 - 2       # 5
7 * 2       # 14
7 / 2       # 3.5     Division ALWAYS returns a float
6 / 2       # 3.0     ...even when it divides evenly
7 // 2      # 3       Floor division (rounds down)
-7 // 2     # -4      Rounds DOWN, not toward zero
7 % 2       # 1       Modulus (remainder)
2 ** 3      # 8       Exponent
9 ** 0.5    # 3.0     Square root

# Handy % tricks
n = 47
n % 2 == 0          # False (checks if n is even)
n % 10              # 7 (last digit)

# Convert minutes to hours + minutes
minutes = 135
minutes // 60       # 2
minutes % 60        # 15
divmod(135, 60)     # (2, 15) (both at once)

# Floats aren't always exact
0.1 + 0.2           # 0.30000000000000004 (use formatting or round() to display)
```

### Assignment Shortcuts

```python
x = 10
x += 5      # x = x + 5   → 15
x -= 3      # x = x - 3   → 12
x *= 2      # x = x * 2   → 24
x /= 4      # x = x / 4   → 6.0
x %= 4      # x = x % 4   → 2.0
x **= 3     # x = x ** 3  → 8.0
# Python has no x++ or x--. Use x += 1
```

### Comparison, Logical, Membership, Identity

```python
# Comparison (return True/False)
5 == 5      # True    Equal (two = signs! One = is assignment)
5 != 3      # True    Not equal
5 > 3       # True
5 < 3       # False
5 >= 5      # True
5 <= 4      # False
"apple" < "banana"  # True (alphabetical)
"Zebra" < "apple"   # True (uppercase sorts before lowercase!)

# Chained comparisons
age = 15
13 <= age <= 19     # True (same as 13 <= age and age <= 19)

# Logical
True and False      # False  (both must be True)
True or False       # True   (at least one True)
not True            # False  (flips it)

# Membership
"a" in "cat"            # True
3 in [1, 2, 3]          # True
"x" not in "cat"        # True
"name" in {"name": "Al"}  # True (checks dictionary keys)

# Identity: `is` checks for the SAME object, == checks for equal values
a = [1, 2]
b = [1, 2]
a == b                  # True (same contents)
a is b                  # False (two separate lists)
result = None
result is None          # True (always use `is` for None checks)
```

### Order of Operations

```python
2 + 3 * 4       # 14 (multiplication first)
(2 + 3) * 4     # 20
2 ** 3 ** 2     # 512 (right to left: 3**2 = 9, then 2**9)
-2 ** 2         # -4 (** happens before the minus sign!)
(-2) ** 2       # 4

# Order: ()  →  **  →  -x  →  * / // %  →  + -  →  comparisons  →  not  →  and  →  or
```

## Strings

```python
# Single or double quotes both work
a = 'hi'
b = "it's easy"         # Use double quotes when the string has an apostrophe
c = 'She said "hi"'

# Common methods (strings never change; methods return a NEW string)
text = "Hello, World!"
text.lower()            # "hello, world!"
text.upper()            # "HELLO, WORLD!"
text.swapcase()         # "hELLO, wORLD!"
"hello world".title()   # "Hello World"
"hello world".capitalize()  # "Hello world"
"  hi  ".strip()        # "hi" (remove whitespace from both ends)
"  hi  ".lstrip()       # "hi  "
"  hi  ".rstrip()       # "  hi"
"xxhixx".strip("x")     # "hi" (strip specific characters)
text.replace("l", "L")      # "HeLLo, WorLd!"
text.replace("l", "L", 1)   # "HeLlo, World!" (only the first 1)
text.find("World")      # 7 (index where found)
text.find("xyz")        # -1 (not found)
text.index("World")     # 7 (like find, but ValueError if not found)
text.count("l")         # 3
len(text)               # 13
```

### Split & Join

```python
"a,b,c".split(",")              # ["a", "b", "c"]
"one two   three".split()       # ["one", "two", "three"] (no argument = split on any whitespace)
"a-b-c-d".split("-", 1)         # ["a", "b-c-d"] (split only once)
"line1\nline2".splitlines()     # ["line1", "line2"]

"-".join(["a", "b", "c"])       # "a-b-c"
"".join(["a", "b", "c"])        # "abc"
", ".join(["x", "y"])           # "x, y"
" ".join(str(n) for n in [1, 2, 3])  # "1 2 3" (join only works on strings!)
```

### Combining Strings

```python
"Hello" + " " + "World"     # "Hello World"
"ha" * 3                    # "hahaha"
"-" * 20                    # "--------------------" (handy for dividers)
"Age: " + str(25)           # "Age: 25" (convert numbers first)
# "Age: " + 25              # TypeError: can only concatenate str to str
```

### Indexing & Slicing

```python
text = "Hello, World!"
#       H e l l o ,   W o r l d !
#       0 1 2 3 4 5 6 7 8 9 ...       ← positive indexes
#                      ... -3 -2 -1   ← negative indexes count from the end

text[0]                 # "H" (first character)
text[-1]                # "!" (last character)
text[0:5]               # "Hello" (index 0 up to, NOT including, 5)
text[:5]                # "Hello" (start defaults to 0)
text[7:]                # "World!" (index 7 to the end)
text[-6:]               # "World!" (last 6 characters)
text[::2]               # "Hlo ol!" (every 2nd character)
text[::-1]              # "!dlroW ,olleH" (reversed)

# Strings can't be changed in place
word = "cat"
# word[0] = "b"         # TypeError
word = "b" + word[1:]   # "bat" (build a new string instead)
```

### Checking Content

```python
"hello123".isalnum()    # True  (letters and numbers only)
"hello".isalpha()       # True  (letters only)
"12345".isdigit()       # True  (digits only)
"hello".islower()       # True
"HELLO".isupper()       # True
"  ".isspace()          # True
"py" in "python"        # True

"hello.py".endswith(".py")          # True
"hello.py".startswith("he")         # True
"photo.JPG".lower().endswith((".jpg", ".png"))  # True (a tuple means "any of these")
```

### Padding & Alignment

```python
"hi".ljust(6)           # "hi    "
"hi".rjust(6)           # "    hi"
"hi".center(6)          # "  hi  "
"hi".center(6, "*")     # "**hi**"
"42".zfill(5)           # "00042"
# f-strings can do all of this and more; see String Formatting below
```

### Escape Characters & Special Strings

```python
print("Line 1\nLine 2")     # \n = new line
print("Col1\tCol2")         # \t = tab
print("She said \"hi\"")    # \" = a quote inside quotes
print("C:\\Users\\me")      # \\ = one backslash
print(r"C:\Users\new")      # r"..." = raw string, backslashes stay as-is

# Multi-line strings
poem = """Roses are red,
Violets are blue."""

# Character codes
ord("A")                # 65
chr(65)                 # "A"
```

## String Formatting

Formatting controls how values **look** when you turn them into text: decimal places, padding, alignment, commas, percentages, and so on. **f-strings** (put an `f` before the quotes) are the modern way to do it.

### f-String Basics

```python
name = "Alice"
age = 25

print(f"{name} is {age} years old")     # Alice is 25 years old

# Any expression works inside {}
print(f"Next year: {age + 1}")          # Next year: 26
print(f"Shout: {name.upper()}")         # Shout: ALICE
print(f"Adult? {age >= 18}")            # Adult? True
print(f"Letters: {len(name)}")          # Letters: 5
print(f"Status: {'adult' if age >= 18 else 'minor'}")  # Status: adult

scores = {"math": 90}
print(f"Math: {scores['math']}")        # Math: 90
# Use different quotes inside {} than outside
# (Python 3.12+ allows the same quotes, but mixing is safer)

# Forgetting the f is a common mistake
print("{name}")                         # {name}  ← printed literally!
```

### The Format Spec: `{value:spec}`

Everything after the `:` inside the braces controls the formatting. The parts always go in this order (all optional):

```
{value:[fill][align][sign][0][width][,][.precision][type]}
```

| Part | Options | What it does |
|---|---|---|
| **fill** | any character | Character used for padding (default is a space) |
| **align** | `<` `>` `^` | Left, right, or center |
| **sign** | `+`, `-`, or a space | Show `+` on positive numbers (or a space) |
| **0** | `0` | Pad numbers with zeros |
| **width** | a number | Minimum total width |
| **grouping** | `,` or `_` | Thousands separator |
| **.precision** | `.2` etc. | Digits after the decimal point |
| **type** | `f` `d` `%` `e` `g` `x` `b` `o` `s` | How to display the value |

```python
# Putting it all together:
f"{1234.5:*>12,.2f}"    # '****1,234.50'
#          │││ │ ││
#          │││ │ │└─ f  = fixed-point decimal
#          │││ │ └── .2 = 2 decimal places
#          │││ └──── ,  = thousands separator
#          ││└────── 12 = total width of 12
#          │└─────── >  = align right
#          └──────── *  = pad with *
```

### Decimal Places

```python
pi = 3.14159265

f"{pi:.2f}"             # '3.14'
f"{pi:.4f}"             # '3.1416' (rounds)
f"{pi:.0f}"             # '3'
f"{10:.2f}"             # '10.00' (works on ints too)
f"{19.5:.2f}"           # '19.50' (good for money)

# Fixing float weirdness for display
total = 0.1 + 0.2
print(total)            # 0.30000000000000004
print(f"{total:.2f}")   # 0.30
# Formatting only changes how it LOOKS. total itself is unchanged
```

### Thousands Separators

```python
f"{1000000:,}"          # '1,000,000'
f"{1234567.891:,}"      # '1,234,567.891'
f"{1234567.891:,.2f}"   # '1,234,567.89'
f"{1234567:_}"          # '1_234_567'
```

### Percentages

`%` multiplies by 100 and adds a percent sign.

```python
f"{0.8567:.1%}"         # '85.7%'
f"{0.8567:.0%}"         # '86%'
f"{0.5:%}"              # '50.000000%' (default is 6 decimals)

correct, total = 17, 20
print(f"Score: {correct / total:.0%}")   # Score: 85%
```

### Width & Alignment

The brackets below show where the padding goes.

```python
f"[{'hi':<8}]"          # '[hi      ]'  left
f"[{'hi':>8}]"          # '[      hi]'  right
f"[{'hi':^8}]"          # '[   hi   ]'  center

# Default alignment: strings go left, numbers go right
f"[{'hi':8}]"           # '[hi      ]'
f"[{42:8}]"             # '[      42]'

# Custom fill character (must come right before the < > ^)
f"[{'hi':*^8}]"         # '[***hi***]'
f"[{'hi':-<8}]"         # '[hi------]'
f"[{'hi':.>8}]"         # '[......hi]'
f"{'':=^20}"            # '====================' (a line of 20 = signs)
f"{' MENU ':=^20}"      # '======= MENU ======='

# Width variables work with nested braces
pi = 3.14159265
width = 10
f"[{'hi':>{width}}]"    # '[        hi]'
decimals = 3
f"{pi:.{decimals}f}"    # '3.142'
f"{pi:{width}.{decimals}f}"   # '     3.142'
```

### Zero Padding

```python
f"{7:03}"               # '007'
f"{42:05}"              # '00042'
f"{3.5:08.3f}"          # '0003.500' (width 8 includes the dot and decimals)
f"{-7:04}"              # '-007' (the sign counts toward the width)

# Great for file names and times
for i in range(1, 4):
    print(f"photo_{i:03}.jpg")
# photo_001.jpg
# photo_002.jpg
# photo_003.jpg

h, m, s = 9, 5, 3
print(f"{h:02}:{m:02}:{s:02}")         # 09:05:03
```

### Signs

```python
f"{5:+}"                # '+5'  (always show the sign)
f"{-5:+}"               # '-5'
f"{5: }"                # ' 5'  (space for positives, so they line up with negatives)
f"{-5: }"               # '-5'

change = 3.456
print(f"Change: {change:+.1f}")       # Change: +3.5
```

### Number Bases & Scientific Notation

```python
f"{255:b}"              # '11111111' (binary)
f"{255:o}"              # '377' (octal)
f"{255:x}"              # 'ff' (hex)
f"{255:X}"              # 'FF' (hex, uppercase)
f"{255:#x}"             # '0xff' (# adds the prefix)
f"{5:08b}"              # '00000101' (8-bit binary)

f"{123456789:e}"        # '1.234568e+08'
f"{123456789:.2e}"      # '1.23e+08'
f"{0.000123:.1e}"       # '1.2e-04'

# g = "general": drops trailing zeros, switches to scientific for tiny/huge numbers
f"{2.50:g}"             # '2.5'
f"{100.0:g}"            # '100'
f"{0.00001234:g}"       # '1.234e-05'
```

### Debugging with `=`

Adding `=` prints the expression **and** its value. Handy for quick debugging.

```python
x = 10
y = 3
name = "Alice"

print(f"{x=}")              # x=10
print(f"{x + y=}")          # x + y=13
print(f"{x / y = :.2f}")    # x / y = 3.33  (spaces around = are kept)
print(f"{name=}")           # name='Alice'  (shows quotes)
```

### `!r` and `!s`: repr vs str

```python
name = "Alice"
f"{name}"               # 'Alice'   → prints as: Alice
f"{name!r}"             # "'Alice'" → prints as: 'Alice' (with quotes)

# !r is great for spotting hidden whitespace
entry = "yes "
print(f"[{entry}]")     # [yes ]
print(f"{entry!r}")     # 'yes '
```

### Escaping Braces

```python
name = "Alice"
f"{{name}}"             # '{name}' (double braces = literal brace)
f"{{{name}}}"           # '{Alice}'
f"Set: {{1, 2}}"        # 'Set: {1, 2}'
```

### Dates in f-Strings

```python
from datetime import datetime
now = datetime(2026, 9, 22, 14, 5)

f"{now:%Y-%m-%d}"       # '2026-09-22'
f"{now:%B %d, %Y}"      # 'September 22, 2026'
f"{now:%A}"             # 'Tuesday'
f"{now:%I:%M %p}"       # '02:05 PM'
f"{now:%m/%d/%y}"       # '09/22/26'
# Full list of codes in Working with Dates & Times
```

### Multi-line f-Strings

```python
name = "Alice"
score = 92.456

report = f"""
Student: {name}
Score:   {score:.1f}
Grade:   {'A' if score >= 90 else 'B'}
"""
print(report)
#
# Student: Alice
# Score:   92.5
# Grade:   A

# Long lines: put strings side by side inside ( ); Python joins them
message = (
    f"Hello {name}, "
    f"your score is {score:.1f} "
    f"out of 100"
)
# 'Hello Alice, your score is 92.5 out of 100'
```

### `print()` Options

```python
print("a", "b", "c")                # a b c (commas add a space)
print("a", "b", "c", sep="")        # abc
print("a", "b", "c", sep=", ")      # a, b, c
print("2026", "09", "22", sep="-")  # 2026-09-22

print("Loading", end="")            # end="" means no newline
print("...")                        # Loading...
print("Hello", end="!\n")           # Hello!
print()                             # Blank line

nums = [1, 2, 3]
print(nums)                         # [1, 2, 3]
print(*nums)                        # 1 2 3 (* unpacks the list)
print(*nums, sep=" -> ")            # 1 -> 2 -> 3

import sys
print("Something broke", file=sys.stderr)   # Print to the error stream
```

### Older Styles: `.format()` and `%`

You'll see these in older code and tutorials. The format spec after `:` works the same as in f-strings.

```python
# .format()
"{} is {} years old".format("Alice", 25)         # 'Alice is 25 years old'
"{0} {1} {0}".format("ha", "ho")                 # 'ha ho ha' (reuse by position)
"{name} scored {score:.1f}".format(name="Bo", score=91.26)   # 'Bo scored 91.3'

data = {"name": "Bo", "score": 91.26}
"{name} scored {score:.1f}".format(**data)       # 'Bo scored 91.3'

# Reusable templates are the main reason to still use .format()
row = "{:<10}|{:>8.2f}"
row.format("apple", 1.5)            # 'apple     |    1.50'
row.format("watermelon", 12)        # 'watermelon|   12.00'

# format() built-in: format one value
format(3.14159, ".2f")              # '3.14'
format(1234567, ",")                # '1,234,567'

# % formatting (oldest style)
"%s is %d years old" % ("Alice", 25)   # 'Alice is 25 years old'
"%.2f" % 3.14159                    # '3.14'
"%5d|" % 42                         # '   42|'
"%-5d|" % 42                        # '42   |'
# %s = string, %d = integer, %f = float
```

### Recipe: Printing a Table

```python
students = [("Alice", 92.5, 0.95), ("Bob", 78.0, 0.8), ("Charlie", 85.33, 1.0)]

print(f"{'Name':<10}{'Score':>8}{'Attend':>8}")
print("-" * 26)
for name, score, attend in students:
    print(f"{name:<10}{score:>8.1f}{attend:>8.0%}")
# Name         Score  Attend
# --------------------------
# Alice         92.5     95%
# Bob           78.0     80%
# Charlie       85.3    100%
```

Size columns to fit the longest item:

```python
items = ["pen", "notebook", "backpack"]
width = max(len(item) for item in items)    # 8
for item in items:
    print(f"{item:>{width}} |")
#      pen |
# notebook |
# backpack |
```

### Recipe: Receipt with Dot Leaders

```python
cart = {"Coffee": 3.5, "Bagel": 2.25, "Orange Juice": 4.0}

for item, price in cart.items():
    print(f"{item:.<20}${price:>6.2f}")
print(f"{'TOTAL':.<20}${sum(cart.values()):>6.2f}")
# Coffee..............$  3.50
# Bagel...............$  2.25
# Orange Juice........$  4.00
# TOTAL...............$  9.75
```

### Recipe: Progress Bar

```python
done, total = 7, 20
width = 20
filled = width * done // total              # 7
bar = "#" * filled + "-" * (width - filled)
print(f"[{bar}] {done / total:.0%}")        # [#######-------------] 35%
```

### Recipe: Money

```python
balance = 1000
for year in range(1, 6):
    balance *= 1.05
    print(f"Year {year}: ${balance:>10,.2f}")
# Year 1: $  1,050.00
# Year 2: $  1,102.50
# Year 3: $  1,157.62
# Year 4: $  1,215.51
# Year 5: $  1,276.28

# Negative money
amount = -42.5
print(f"-${abs(amount):,.2f}" if amount < 0 else f"${amount:,.2f}")   # -$42.50
```

### Format Spec Quick Reference

| Spec | Example | Result |
|---|---|---|
| `.2f` | `f"{3.14159:.2f}"` | `3.14` |
| `,` | `f"{1234567:,}"` | `1,234,567` |
| `,.2f` | `f"{1234.5:,.2f}"` | `1,234.50` |
| `.1%` | `f"{0.256:.1%}"` | `25.6%` |
| `<8` | `f"[{'hi':<8}]"` | `[hi      ]` |
| `>8` | `f"[{'hi':>8}]"` | `[      hi]` |
| `^8` | `f"[{'hi':^8}]"` | `[   hi   ]` |
| `*^8` | `f"[{'hi':*^8}]"` | `[***hi***]` |
| `05` | `f"{42:05}"` | `00042` |
| `+` | `f"{5:+}"` | `+5` |
| `x` / `X` | `f"{255:x}"` | `ff` |
| `b` | `f"{5:b}"` | `101` |
| `08b` | `f"{5:08b}"` | `00000101` |
| `.2e` | `f"{12345:.2e}"` | `1.23e+04` |
| `g` | `f"{2.50:g}"` | `2.5` |
| `=` | `f"{x=}"` | `x=10` |
| `!r` | `f"{'hi'!r}"` | `'hi'` |
| `%Y-%m-%d` | `f"{date:%Y-%m-%d}"` | `2026-09-22` |

### Common Formatting Mistakes

```python
# 1. Forgetting the f
name = "Al"
print("Hi {name}")          # Hi {name}   ← oops
print(f"Hi {name}")         # Hi Al

# 2. Number formats on a string (common with input(), which returns strings)
price = "3.5"
# f"{price:.2f}"            # ValueError: Unknown format code 'f' for object of type 'str'
f"{float(price):.2f}"       # '3.50'

# 3. Number formats on None
value = None
# f"{value:.2f}"            # TypeError: unsupported format string passed to NoneType
f"{value}"                  # 'None' (plain {} is fine)

# 4. Thinking formatting changes the value
x = 2.567
f"{x:.1f}"                  # '2.6'
x                           # 2.567 (still the same; use round(x, 1) to change the number)
```

## Input/Output

```python
# Output
print("Hello")
print("Value:", 42)             # Value: 42 (commas add a space)
print(f"Name: {name}, Age: {age}")
# (see String Formatting above for sep, end, and more)

# Input (ALWAYS returns a string)
name = input("Enter your name: ")
age = int(input("Enter age: "))          # Convert to int
price = float(input("Enter price: "))    # Convert to float

# Common mistake
age = input("Age: ")            # user types 20
# age + 1                       # TypeError: "20" is a string!
int(age) + 1                    # 21

# Several values on one line (user types: 3 4 5)
a, b, c = input("Three numbers: ").split()              # "3", "4", "5" (strings)
a, b, c = map(int, input("Three numbers: ").split())    # 3, 4, 5 (ints)
nums = [int(x) for x in input("Numbers: ").split()]     # Any amount → list of ints

# Clean up yes/no answers
answer = input("Continue? (y/n): ").strip().lower()
if answer in ("y", "yes"):
    print("Continuing...")

# Keep asking until the input is valid → see Loops > While Loops
```

## Conditionals

```python
if condition:
    # code
elif another_condition:
    # code
else:
    # code
```

Python checks conditions **top to bottom** and runs only the **first** one that's True.

```python
score = 87
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"         # ← This one runs, and the rest are skipped
elif score >= 70:
    grade = "C"
else:
    grade = "F"
print(grade)            # B

# Order matters! This version is buggy:
if score >= 70:
    grade = "C"         # 87 matches here first, so it never reaches the >= 80 check
elif score >= 80:
    grade = "B"
```

### Combining Conditions

```python
temp = 72
raining = False
if temp > 65 and not raining:
    print("Go outside")

day = "Saturday"
if day == "Saturday" or day == "Sunday":
    print("Weekend!")
if day in ("Saturday", "Sunday"):       # Cleaner version of the line above
    print("Weekend!")

# Range check
score = 85
if 80 <= score < 90:
    print("B range")

# Careful: this is always True!
# if day == "Saturday" or "Sunday":     # "Sunday" by itself is truthy
```

### Nested Conditions

```python
logged_in = True
is_admin = False

if logged_in:
    if is_admin:
        print("Admin panel")
    else:
        print("Dashboard")      # ← This runs
else:
    print("Please log in")
```

### Truthiness

Empty things count as `False`, so you can check them directly.

```python
cart = []
if cart:                    # Same as: if len(cart) > 0
    print("Checking out")
else:
    print("Cart is empty")  # ← This runs

name = ""
if not name:
    print("Name is required")

result = None
if result is None:          # Use `is None` when 0 or "" are valid values
    print("No result yet")
```

### Ternary Operator (one-line if/else)

```python
age = 18
status = "adult" if age >= 18 else "minor"    # "adult"

x = 7
print("even" if x % 2 == 0 else "odd")        # odd

# Works anywhere a value goes
fee = 0 if age < 5 else 12
count = 3
label = f"{count} item{'s' if count != 1 else ''}"   # "3 items" (or "1 item" when count is 1)
```

### Match Statement (Python 3.10+)

Like a cleaner `if/elif` chain when you're comparing one value against many options.

```python
command = "stop"
match command:
    case "start":
        print("Starting")
    case "stop" | "quit":           # | means "or"
        print("Stopping")           # ← This runs
    case _:                         # _ matches anything (like else)
        print("Unknown command")

# Match can also pull values out of tuples/lists
point = (0, 5)
match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"On the y-axis at {y}")   # ← On the y-axis at 5
    case (x, 0):
        print(f"On the x-axis at {x}")
    case (x, y):
        print(f"At ({x}, {y})")

# Add conditions with `if` (called a guard)
age = 15
match age:
    case n if n < 13:
        print("Child")
    case n if n < 20:
        print("Teen")               # ← This runs
    case _:
        print("Adult")
```

## Loops

Loops repeat code. Python has two kinds:

- **`for`**: runs once **for each item** in a collection (list, string, range, dict, file...). Use it when you know what you're looping over.
- **`while`**: keeps running **while a condition is True**. Use it when you don't know ahead of time how many repeats you need.

### For Loop Basics

```python
# Loop over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
# apple
# banana
# cherry

# Loop over a string (one character at a time)
for letter in "hey":
    print(letter)
# h
# e
# y

# The loop variable can be named anything, so pick something descriptive
for score in [90, 85, 77]:
    print(score + 5)
# 95
# 90
# 82

# Indented lines run every time; unindented lines run once, after the loop
for n in [1, 2, 3]:
    print(n)            # Runs 3 times
print("Done")           # Runs once
```

### `range()`: Looping a Set Number of Times

`range(start, stop, step)` produces a sequence of numbers. **The stop value is never included.**

```python
list(range(5))              # [0, 1, 2, 3, 4]       start defaults to 0
list(range(1, 6))           # [1, 2, 3, 4, 5]       use stop + 1 to include the end
list(range(0, 20, 5))       # [0, 5, 10, 15]        step by 5
list(range(10, 0, -1))      # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]   count down with a negative step
list(range(10, -1, -2))     # [10, 8, 6, 4, 2, 0]
list(range(5, 0))           # []   (can't count up from 5 to 0; use a negative step)
len(range(0, 100, 10))      # 10
# (wrap range in list() just to SEE the numbers; for loops don't need it)
```

```python
# Repeat something N times. Use _ when you don't need the number
for _ in range(3):
    print("Hip hip hooray!")

# Sum 1 to 100
total = 0
for n in range(1, 101):
    total += n
print(total)                # 5050

# Times table
for i in range(1, 6):
    print(f"7 x {i} = {7 * i}")
# 7 x 1 = 7
# 7 x 2 = 14
# 7 x 3 = 21
# 7 x 4 = 28
# 7 x 5 = 35

# Countdown
for i in range(3, 0, -1):
    print(i)
print("Liftoff!")
# 3
# 2
# 1
# Liftoff!

# Even numbers only
for n in range(0, 11, 2):
    print(n, end=" ")       # end=" " keeps it on one line
print()                     # Finish the line
# 0 2 4 6 8 10
```

### `enumerate()`: Index and Value Together

```python
colors = ["red", "green", "blue"]

# Works, but clunky:
for i in range(len(colors)):
    print(i, colors[i])

# Better: enumerate gives you both
for i, color in enumerate(colors):
    print(i, color)
# 0 red
# 1 green
# 2 blue

# Start counting at 1 (nice for numbered lists)
for num, color in enumerate(colors, start=1):
    print(f"{num}. {color}")
# 1. red
# 2. green
# 3. blue
```

**When you actually need `range(len(...))`:** changing items by position, or comparing an item with its neighbor.

```python
# Change items in place
prices = [10, 20, 30]
for i in range(len(prices)):
    prices[i] = prices[i] * 2
print(prices)               # [20, 40, 60]

# Compare each item with the next one (note the - 1 so i + 1 stays in range)
temps = [70, 72, 71, 75]
for i in range(len(temps) - 1):
    change = temps[i + 1] - temps[i]
    print(f"{temps[i]} -> {temps[i + 1]} ({change:+})")
# 70 -> 72 (+2)
# 72 -> 71 (-1)
# 71 -> 75 (+4)
```

### `zip()`: Loop Over Several Lists at Once

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

for name, age in zip(names, ages):
    print(f"{name} is {age}")
# Alice is 25
# Bob is 30
# Charlie is 35

# Three lists
cities = ["NYC", "LA", "Chicago"]
for name, age, city in zip(names, ages, cities):
    print(f"{name} ({age}) lives in {city}")

# zip stops at the SHORTEST list
for a, b in zip([1, 2, 3], ["x", "y"]):
    print(a, b)
# 1 x
# 2 y        (3 is silently dropped)
# zip(a, b, strict=True) raises an error instead if lengths differ (3.10+)

# zip + enumerate (note the parentheses around the pair)
for i, (name, age) in enumerate(zip(names, ages), start=1):
    print(f"{i}. {name}: {age}")

# Build a dictionary from two lists
dict(zip(names, ages))      # {"Alice": 25, "Bob": 30, "Charlie": 35}

# Loop over neighbors without indexes
temps = [70, 72, 71, 75]
for before, after in zip(temps, temps[1:]):
    print(after - before, end=" ")     # 2 -1 4
print()
```

### Looping Over Dictionaries

```python
scores = {"Alice": 92, "Bob": 78, "Charlie": 85}

for name in scores:                     # Keys (default)
    print(name)

for score in scores.values():           # Values only
    print(score)

for name, score in scores.items():      # Keys AND values (most common)
    print(f"{name}: {score}")
# Alice: 92
# Bob: 78
# Charlie: 85

# Alphabetical by key
for name in sorted(scores):
    print(name, scores[name])

# Highest score first (sort by value)
for name, score in sorted(scores.items(), key=lambda item: item[1], reverse=True):
    print(f"{name:<8}{score}")
# Alice   92
# Charlie 85
# Bob     78

# Numbered
for rank, (name, score) in enumerate(scores.items(), start=1):
    print(f"{rank}. {name} - {score}")
```

### `reversed()` and `sorted()`

```python
for n in reversed([1, 2, 3]):
    print(n, end=" ")       # 3 2 1
print()

for word in sorted(["pear", "fig", "apple"]):
    print(word, end=" ")    # apple fig pear
print()

for word in sorted(["pear", "fig", "apple"], key=len):
    print(word, end=" ")    # fig pear apple (shortest first)
print()

for letter in reversed("abc"):
    print(letter, end="")   # cba
print()
```

### While Loops

A `while` loop checks its condition **before every pass**. When the condition becomes False, it stops. Something inside the loop has to change the condition, or it runs forever.

```python
# Countdown
n = 3
while n > 0:
    print(n)
    n -= 1              # Without this line, the loop never ends!
print("Liftoff!")
# 3
# 2
# 1
# Liftoff!

# Loop until a goal is reached (you don't know how many years ahead of time)
balance = 1000
years = 0
while balance < 2000:
    balance *= 1.07     # 7% growth per year
    years += 1
print(f"Doubled in {years} years")      # Doubled in 11 years

# Count the digits in a number
n = 4096
digits = 0
while n > 0:
    n //= 10            # Chop off the last digit
    digits += 1
print(digits)           # 4

# Process a list until it's empty
tasks = ["email", "code", "lunch"]
while tasks:            # An empty list is False, so this stops when it's empty
    task = tasks.pop(0)
    print(f"Doing {task}, {len(tasks)} left")
# Doing email, 2 left
# Doing code, 1 left
# Doing lunch, 0 left
```

### `while True` + `break`

When the exit condition is easiest to check in the **middle** of the loop, loop forever and `break` out.

```python
# Keep asking until the user quits
while True:
    text = input("Say something (or 'quit'): ")
    if text == "quit":
        break
    print(f"You said: {text}")

# Input validation: keep asking until the answer is valid
while True:
    entry = input("Pick a number 1-10: ")
    if entry.isdigit() and 1 <= int(entry) <= 10:
        number = int(entry)
        break
    print("Invalid, try again.")
print(f"You picked {number}")

# Same idea with try/except (also handles negatives and decimals)
while True:
    try:
        age = int(input("Age: "))
        break
    except ValueError:
        print("Please enter a whole number.")

# Menu loop
while True:
    print("\n1) Add  2) Show  3) Quit")
    choice = input("> ")
    if choice == "1":
        print("Adding...")
    elif choice == "2":
        print("Showing...")
    elif choice == "3":
        print("Bye!")
        break
    else:
        print("Invalid choice")
```

**Full example: number guessing game**

```python
import random

secret = random.randint(1, 100)
guesses = 0

while True:
    guess = int(input("Guess (1-100): "))
    guesses += 1
    if guess < secret:
        print("Too low!")
    elif guess > secret:
        print("Too high!")
    else:
        print(f"Got it in {guesses} guesses!")
        break
```

> **Stuck in an infinite loop?** Press `Ctrl+C` in the terminal to stop the program.

### `break`, `continue`, and `pass`

| Keyword | What it does |
|---|---|
| `break` | Exit the loop immediately |
| `continue` | Skip the rest of this pass and jump to the next one |
| `pass` | Do nothing (a placeholder so the code is valid) |

```python
# break: stop at the first number over 10
for n in [3, 8, 12, 5, 20]:
    if n > 10:
        print(f"Found {n}")
        break
    print(f"Checked {n}")
# Checked 3
# Checked 8
# Found 12        (5 and 20 are never checked)

# continue: skip even numbers
for n in range(1, 8):
    if n % 2 == 0:
        continue
    print(n, end=" ")       # 1 3 5 7
print()

# continue: skip blank or commented lines
lines = ["name=Al", "", "# comment", "age=30"]
for line in lines:
    if not line or line.startswith("#"):
        continue
    print(line)
# name=Al
# age=30

# pass: placeholder for code you'll write later
for n in range(3):
    pass    # TODO
```

### The Loop `else` Clause

A loop's `else` block runs **only if the loop finished without hitting `break`**. It's handy for "search, and do something if not found."

```python
nums = [3, 5, 7]
for n in nums:
    if n % 2 == 0:
        print(f"Found even number {n}")
        break
else:
    print("No even numbers")    # ← Runs, because break never happened
# No even numbers

# Find prime numbers
for n in range(2, 20):
    for d in range(2, n):
        if n % d == 0:
            break               # Found a divisor, so not prime
    else:
        print(n, end=" ")       # No divisor found, so it's prime
print()
# 2 3 5 7 11 13 17 19

# Works with while too
attempts = 0
while attempts < 3:
    attempts += 1
    if input("Password: ") == "secret":
        print("Welcome!")
        break
else:
    print("Locked out")         # Only if all 3 attempts failed
```

### Nested Loops

The inner loop runs **completely** for each pass of the outer loop.

```python
for outer in range(1, 3):
    for inner in ["a", "b", "c"]:
        print(outer, inner)
# 1 a
# 1 b
# 1 c
# 2 a
# 2 b
# 2 c

# Multiplication grid
for row in range(1, 4):
    for col in range(1, 5):
        print(f"{row * col:4}", end="")
    print()                     # New line after each row
#    1   2   3   4
#    2   4   6   8
#    3   6   9  12

# Triangle
for i in range(1, 5):
    print("*" * i)
# *
# **
# ***
# ****

# Pyramid
height = 4
for i in range(1, height + 1):
    print(f"{'*' * (2 * i - 1):^{2 * height - 1}}")
#    *
#   ***
#  *****
# *******
```

**Looping over 2D lists (grids):**

```python
grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]

# Print as a grid
for row in grid:
    for value in row:
        print(value, end=" ")
    print()
# 1 2 3
# 4 5 6
# 7 8 9

# With positions
for r, row in enumerate(grid):
    for c, value in enumerate(row):
        if value == 5:
            print(f"5 is at row {r}, column {c}")   # 5 is at row 1, column 1

# Sum every row
for row in grid:
    print(sum(row), end=" ")    # 6 15 24
print()

# Every pair of items (without repeats)
players = ["Ana", "Ben", "Cy"]
for i in range(len(players)):
    for j in range(i + 1, len(players)):
        print(f"{players[i]} vs {players[j]}")
# Ana vs Ben
# Ana vs Cy
# Ben vs Cy
```

**`break` only exits the innermost loop.** To escape all loops, use a flag or put the loops in a function and `return`:

```python
grid = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Option 1: a flag
target = 5
found = False
for row in grid:
    for value in row:
        if value == target:
            found = True
            break               # Exits the inner loop only
    if found:
        break                   # Exits the outer loop

# Option 2: a function (cleaner)
def find(grid, target):
    for r, row in enumerate(grid):
        for c, value in enumerate(row):
            if value == target:
                return (r, c)   # return exits everything at once
    return None

find(grid, 8)                   # (2, 1)
```

### Common Loop Patterns

These show up constantly. Each one is shown with a loop, and the built-in shortcut if there is one.

```python
nums = [4, 8, 15, 16, 23, 42]

# Accumulator: add things up
total = 0
for n in nums:
    total += n
# total = 108          Shortcut: sum(nums)

# Counter: count items that match
count = 0
for n in nums:
    if n % 2 == 0:
        count += 1
# count = 4            Shortcut: sum(1 for n in nums if n % 2 == 0)

# Find the max yourself
biggest = nums[0]
for n in nums:
    if n > biggest:
        biggest = n
# biggest = 42         Shortcut: max(nums)

# Transform: build a new list
doubled = []
for n in nums:
    doubled.append(n * 2)
# [8, 16, 30, 32, 46, 84]    Shortcut: [n * 2 for n in nums]

# Filter: keep some items
big = []
for n in nums:
    if n > 10:
        big.append(n)
# [15, 16, 23, 42]           Shortcut: [n for n in nums if n > 10]

# Search: find the first match
emails = ["bob@x.com", "admin@site.org", "amy@x.com"]
found = None
for e in emails:
    if e.startswith("admin"):
        found = e
        break
# found = "admin@site.org"
# Shortcut: next((e for e in emails if e.startswith("admin")), None)

# Any / all
has_negative = False
for n in nums:
    if n < 0:
        has_negative = True
        break
# False                Shortcut: any(n < 0 for n in nums)
#                      Also:     all(n > 0 for n in nums)  → True
```

```python
# Count occurrences with a dictionary
text = "the cat and the hat"
counts = {}
for word in text.split():
    counts[word] = counts.get(word, 0) + 1
# {"the": 2, "cat": 1, "and": 1, "hat": 1}

# Group items
words = ["apple", "avocado", "banana", "blueberry", "cherry"]
by_letter = {}
for w in words:
    first = w[0]
    if first not in by_letter:
        by_letter[first] = []
    by_letter[first].append(w)
# {"a": ["apple", "avocado"], "b": ["banana", "blueberry"], "c": ["cherry"]}

# Running average
readings = [68, 71, 75, 70]
total = 0
for count, r in enumerate(readings, start=1):
    total += r
    print(f"Reading {count}: running avg = {total / count:.1f}")
# Reading 1: running avg = 68.0
# Reading 2: running avg = 69.5
# Reading 3: running avg = 71.3
# Reading 4: running avg = 71.0

# Build a string
word = "loop"
backwards = ""
for ch in word:
    backwards = ch + backwards
# "pool"               Shortcut: word[::-1]

# Count vowels
vowels = 0
for ch in "Programming is fun":
    if ch.lower() in "aeiou":
        vowels += 1
# vowels = 5

# FizzBuzz (classic interview question)
for i in range(1, 16):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

### Loop → Comprehension

A loop that only builds a list can usually be written as a one-line comprehension (see [Comprehensions](#comprehensions)).

```python
# Loop
squares = []
for x in range(1, 6):
    if x % 2 == 1:
        squares.append(x ** 2)

# Comprehension (same result)
squares = [x ** 2 for x in range(1, 6) if x % 2 == 1]   # [1, 9, 25]
#          └─what─┘ └─────loop──────┘ └──filter──┘
```

Use a regular loop when the body is more than one simple expression, or when it *does* something (prints, writes a file) instead of building a list.

### Don't Modify a List While Looping Over It

```python
# Bug: removing items shifts everything, so the loop skips some
nums = [1, 2, 2, 3, 4]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)
print(nums)             # [1, 2, 3]  ← one 2 survived!

# Fix 1: build a new list
nums = [1, 2, 2, 3, 4]
nums = [n for n in nums if n % 2 != 0]
print(nums)             # [1, 3]

# Fix 2: loop over a copy
nums = [1, 2, 2, 3, 4]
for n in nums[:]:       # nums[:] is a copy
    if n % 2 == 0:
        nums.remove(n)
print(nums)             # [1, 3]

# Dictionaries raise an error instead
stock = {"apple": 0, "pear": 3, "fig": 0}
# for k in stock:
#     if stock[k] == 0:
#         del stock[k]      # RuntimeError: dictionary changed size during iteration
for k in list(stock):       # Loop over a copy of the keys
    if stock[k] == 0:
        del stock[k]
print(stock)                # {'pear': 3}
```

### `itertools`: Loop Power Tools

```python
from itertools import product, combinations, permutations, chain, pairwise, zip_longest, count

# product: every combination (replaces nested loops)
for size, color in product(["S", "M"], ["red", "blue"]):
    print(size, color)
# S red
# S blue
# M red
# M blue

list(combinations([1, 2, 3], 2))   # [(1, 2), (1, 3), (2, 3)]  (order doesn't matter)
list(permutations([1, 2, 3], 2))   # [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
list(chain([1, 2], [3], [4, 5]))   # [1, 2, 3, 4, 5] (glue lists together)
list(pairwise([1, 2, 3, 4]))       # [(1, 2), (2, 3), (3, 4)] (neighbors, 3.10+)
list(zip_longest([1, 2, 3], ["a"], fillvalue="-"))   # [(1, "a"), (2, "-"), (3, "-")]

# count() goes forever, so always break out
for i in count(start=10, step=5):
    if i > 25:
        break
    print(i, end=" ")       # 10 15 20 25
print()
```

### Common Loop Mistakes

```python
# 1. Off-by-one: range stops BEFORE the end value
for i in range(1, 10):      # 1 to 9, not 10!
    pass
for i in range(1, 11):      # 1 to 10
    pass

# 2. Infinite while loop: forgot to update the variable
count = 0
# while count < 5:
#     print(count)          # count never changes → runs forever (Ctrl+C to stop)

# 3. Changing the loop variable doesn't change the list
nums = [1, 2, 3]
for n in nums:
    n = n * 10              # Only changes the temporary variable n
print(nums)                 # [1, 2, 3]  ← unchanged
nums = [n * 10 for n in nums]   # Do this instead → [10, 20, 30]

# 4. Wrong indentation: this print runs EVERY pass instead of once at the end
total = 0
for n in [1, 2, 3]:
    total += n
    print(total)            # Prints 1, 3, 6. Unindent it to print only 6

# 5. The loop variable keeps its last value after the loop
for i in range(5):
    pass
print(i)                    # 4

# 6. Resetting inside the loop instead of before it
for n in [1, 2, 3]:
    total = 0               # Bug: reset every pass
    total += n
print(total)                # 3 (not 6)
```

## Lists

```python
fruits = ["apple", "banana", "cherry"]
mixed = [1, "two", 3.0, True]   # Can hold different types
empty = []

# Access
fruits[0]               # "apple"
fruits[-1]              # "cherry" (last item)
# fruits[10]            # IndexError: list index out of range

# Slicing (same rules as strings)
nums = [3, 1, 4, 1, 5]
nums[1:3]               # [1, 4]
nums[:2]                # [3, 1]
nums[-2:]               # [1, 5]
nums[::-1]              # [5, 1, 4, 1, 3] (reversed copy)

# Looking things up
len(nums)               # 5
4 in nums               # True
nums.index(4)           # 2 (position of the first 4)
nums.count(1)           # 2
min(nums)               # 1
max(nums)               # 5
sum(nums)               # 14
```

### Changing a List

```python
fruits = ["apple", "banana", "cherry"]

fruits[0] = "orange"            # fruits is now ["orange", "banana", "cherry"]
fruits.append("grape")          # Add one item to the end
fruits.insert(1, "kiwi")        # Insert at index 1
fruits.extend(["fig", "lime"])  # Add several items to the end
fruits.remove("banana")         # Remove first matching value (ValueError if missing)
last = fruits.pop()             # Remove & return the last item
first = fruits.pop(0)           # Remove & return the item at index 0
del fruits[0]                   # Delete by index (no return value)
fruits.clear()                  # Remove everything

# append vs extend
a = [1, 2]
a.append([3, 4])                # a is now [1, 2, [3, 4]] (adds the list as ONE item)
b = [1, 2]
b.extend([3, 4])                # b is now [1, 2, 3, 4]

# Combine & repeat
[1, 2] + [3, 4]                 # [1, 2, 3, 4]
[0] * 5                         # [0, 0, 0, 0, 0]
```

### Sorting

```python
nums = [3, 1, 2]
new = sorted(nums)              # new = [1, 2, 3]; nums is unchanged
nums.sort()                     # nums is now [1, 2, 3] (returns None)
nums.sort(reverse=True)         # nums is now [3, 2, 1]
# nums = nums.sort()            # Bug! nums becomes None

words = ["banana", "apple", "Cherry", "fig"]
sorted(words)                   # ["Cherry", "apple", "banana", "fig"] (uppercase sorts first)
sorted(words, key=str.lower)    # ["apple", "banana", "Cherry", "fig"] (ignore case)
sorted(words, key=len)          # ["fig", "apple", "banana", "Cherry"] (by length)

# Sort by part of each item
people = [("Al", 30), ("Bea", 25), ("Cy", 35)]
sorted(people, key=lambda p: p[1])      # [("Bea", 25), ("Al", 30), ("Cy", 35)]
```

### Copying (Gotcha!)

```python
a = [1, 2, 3]
b = a                   # b is NOT a copy; both names point to the same list
b.append(4)
print(a)                # [1, 2, 3, 4]  ← a changed too!

c = a.copy()            # A real copy (also: a[:] or list(a))
c.append(5)
print(a)                # [1, 2, 3, 4]  ← a is unaffected
```

### Nested Lists (2D)

```python
grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]
grid[0]                 # [1, 2, 3] (first row)
grid[1][2]              # 6 (row 1, column 2)
grid[-1][-1]            # 9
len(grid)               # 3 (rows)
len(grid[0])            # 3 (columns)

# Make a 3x3 grid of zeros
board = [[0] * 3 for _ in range(3)]     # Correct
# board = [[0] * 3] * 3                 # Wrong: all 3 rows are the SAME list
```

## Tuples

```python
# Tuples are like lists but immutable (can't change after creation)
coords = (10, 20)
rgb = (255, 128, 0)

# Access (same as lists)
coords[0]               # 10
coords[-1]              # 20
len(rgb)                # 3
128 in rgb              # True
# coords[0] = 5         # TypeError: tuples can't be changed

# Unpack
x, y = coords           # x = 10, y = 20
r, g, b = rgb

# Single-element tuple (needs a trailing comma)
single = (42,)
not_a_tuple = (42)      # Just the number 42

# Convert
tuple([1, 2, 3])        # (1, 2, 3)
list((1, 2, 3))         # [1, 2, 3]

# Common uses: returning multiple values, and as dictionary keys (lists can't be keys)
distances = {(0, 0): "home", (3, 4): "school"}
distances[(3, 4)]       # "school"

# Looping over a list of tuples
points = [(1, 2), (3, 4), (5, 6)]
for x, y in points:
    print(f"x={x}, y={y}")
```

## Sets

```python
# Unordered collection of unique items (no duplicates, no indexing)
colors = {"red", "green", "blue"}
empty = set()               # NOT {}, that's an empty dict

# Add/remove
colors.add("yellow")
colors.remove("red")        # Error if not found
colors.discard("red")       # No error if not found

# Membership checks are very fast with sets
"green" in colors           # True

# Set operations
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a | b       # {1, 2, 3, 4, 5, 6}   Union: in either
a & b       # {3, 4}               Intersection: in both
a - b       # {1, 2}               Difference: in a but not b
a ^ b       # {1, 2, 5, 6}         Symmetric difference: in one but not both
{1, 2} <= a # True                 Subset

# Remove duplicates from a list
nums = [1, 2, 2, 3, 3, 3]
unique = list(set(nums))    # [1, 2, 3] (order not guaranteed)
unique_ordered = list(dict.fromkeys(nums))  # [1, 2, 3] (keeps original order)

# Real example: who turned in both assignments?
hw1 = {"Alice", "Bob", "Cara"}
hw2 = {"Bob", "Cara", "Dan"}
hw1 & hw2       # {"Bob", "Cara"}
hw1 - hw2       # {"Alice"} (did hw1 but not hw2)
hw1 | hw2       # Everyone who turned in anything

# Unique letters in a word
set("mississippi")          # {"m", "i", "s", "p"}
```

## Dictionaries

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "NYC"
}

# Access
person["name"]              # "Alice"
person.get("name")          # "Alice"
person.get("phone")         # None (no error if missing)
person.get("phone", "N/A")  # "N/A" (custom default)
# person["phone"]           # KeyError!

# Modify
person["age"] = 26          # Update value
person["job"] = "Dev"       # Add new key
del person["city"]          # Delete key
age = person.pop("age")     # Remove & return the value
person.update({"age": 30, "city": "LA"})   # Add/overwrite several at once
person.setdefault("hobbies", [])           # Add key only if it's missing

# Methods
person.keys()               # All keys
person.values()             # All values
person.items()              # Key-value pairs
"name" in person            # True (checks keys)
len(person)                 # Number of keys

# Loop through (more in Loops > Looping Over Dictionaries)
for key, value in person.items():
    print(f"{key}: {value}")
```

### Nested Dictionaries & Lists of Dictionaries

```python
team = {
    "name": "Robotics",
    "members": ["Ana", "Ben"],
    "robot": {"weight": 120, "wheels": 4},
}
team["robot"]["weight"]         # 120
team["members"][0]              # "Ana"
team["members"].append("Cy")    # Change the inner list

# A list of dictionaries is how most real data looks (like rows in a table)
students = [
    {"name": "Alice", "grade": 92},
    {"name": "Bob", "grade": 78},
    {"name": "Cara", "grade": 85},
]
for s in students:
    print(f"{s['name']:<6} {s['grade']}")

best = max(students, key=lambda s: s["grade"])      # {"name": "Alice", "grade": 92}
passing = [s["name"] for s in students if s["grade"] >= 80]   # ["Alice", "Cara"]
average = sum(s["grade"] for s in students) / len(students)   # 85.0
```

### Counting with a Dictionary

```python
votes = ["red", "blue", "red", "green", "red"]
tally = {}
for v in votes:
    tally[v] = tally.get(v, 0) + 1
# {"red": 3, "blue": 1, "green": 1}

# Winner
max(tally, key=tally.get)       # "red"
# (collections.Counter does this for you; see Common Patterns)
```

## Comprehensions

A comprehension builds a list, dict, or set in one line.

```
[ expression   for item in iterable   if condition ]
  └─ what to     └─ loop over this ─┘  └─ optional
     keep                                 filter
```

### List Comprehensions

```python
# Basic
squares = [x ** 2 for x in range(5)]           # [0, 1, 4, 9, 16]

# Transform each item
names = ["alice", "bob"]
[n.title() for n in names]                      # ["Alice", "Bob"]
[len(n) for n in names]                         # [5, 3]
[int(d) for d in "2026"]                        # [2, 0, 2, 6]
[w.strip() for w in " a , b ,c".split(",")]     # ["a", "b", "c"]

# Filter: `if` goes at the END
[x for x in range(10) if x % 2 == 0]            # [0, 2, 4, 6, 8]
[w for w in ["hi", "hello", "yo"] if len(w) > 2]   # ["hello"]

# if/else: goes at the FRONT (it's a ternary, and every item is kept)
["even" if x % 2 == 0 else "odd" for x in range(4)]   # ["even", "odd", "even", "odd"]
[x if x > 0 else 0 for x in [-2, 5, -1, 3]]           # [0, 5, 0, 3]

# Nested: reads left to right like nested for loops
[(r, c) for r in range(2) for c in range(3)]
# [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2)]

grid = [[1, 2], [3, 4], [5, 6]]
[n for row in grid for n in row]                # [1, 2, 3, 4, 5, 6] (flatten)
[[n * 10 for n in row] for row in grid]         # [[10, 20], [30, 40], [50, 60]]
```

### Dictionary & Set Comprehensions

```python
# Dictionary comprehension: {key: value for ...}
{x: x ** 2 for x in range(5)}                   # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
{name: len(name) for name in ["Al", "Bea"]}     # {"Al": 2, "Bea": 3}

prices = {"apple": 1.0, "melon": 3.5, "kiwi": 0.5}
{k: v * 2 for k, v in prices.items()}           # {"apple": 2.0, "melon": 7.0, "kiwi": 1.0}
{k: v for k, v in prices.items() if v >= 1}     # {"apple": 1.0, "melon": 3.5}

# Flip keys and values
{v: k for k, v in {"a": 1, "b": 2}.items()}     # {1: "a", 2: "b"}

# Set comprehension
{len(w) for w in ["hi", "hey", "hello", "yo"]}  # {2, 3, 5}

# Generator expression: no brackets needed inside a function call
sum(x ** 2 for x in range(5))                   # 30
max(len(w) for w in ["hi", "hello"])            # 5
```

## Functions

```python
# Define a function
def greet(name):
    return f"Hello, {name}!"

# Call a function
message = greet("Alice")        # "Hello, Alice!"

# Default parameters
def greet(name="World"):
    return f"Hello, {name}!"

greet()                         # "Hello, World!"
greet("Bo")                     # "Hello, Bo!"

# Multiple parameters
def add(a, b):
    return a + b

# Return multiple values (actually returns a tuple)
def get_stats(numbers):
    return min(numbers), max(numbers)

low, high = get_stats([1, 2, 3, 4, 5])     # low = 1, high = 5
```

### Keyword Arguments

```python
def describe(name, age, city):
    return f"{name}, {age}, from {city}"

describe("Al", 30, "NYC")                   # By position
describe(age=30, city="NYC", name="Al")     # By name, any order
describe("Al", city="NYC", age=30)          # Mix: positional first, then named

def power(base, exp=2):
    return base ** exp

power(3)            # 9
power(3, 3)         # 27
power(2, exp=10)    # 1024
```

### Return Values

```python
# return exits the function immediately
def safe_divide(a, b):
    if b == 0:
        return None     # Stops here
    return a / b

safe_divide(10, 2)      # 5.0
safe_divide(10, 0)      # None

# No return statement → the function returns None
def say_hi():
    print("hi")

result = say_hi()       # Prints "hi"; result is None

# Common mistake: printing instead of returning
def double_bad(x):
    print(x * 2)        # Shows the value but doesn't give it back
def double(x):
    return x * 2

# double_bad(5) + 1     # TypeError (None + 1)
double(5) + 1           # 11
```

### Docstrings & Type Hints

```python
def average(numbers: list[float]) -> float:
    """Return the average of a list of numbers."""
    return sum(numbers) / len(numbers)

# Type hints (: list[float] and -> float) are notes for humans and editors.
# Python does NOT enforce them at runtime.

def greet(name: str, excited: bool = False) -> str:
    return f"Hi {name}{'!' if excited else '.'}"
```

### Scope (Local vs Global)

```python
count = 0                   # Global variable

def show():
    print(count)            # Reading a global is fine

def increment():
    global count            # Needed to CHANGE a global
    count += 1

def local_example():
    temp = 5                # Local: only exists inside this function
    return temp

# print(temp)               # NameError: temp doesn't exist out here

# Usually better: pass values in and return results instead of using globals
def increment(n):
    return n + 1
count = increment(count)
```

### Mutable Default Gotcha

```python
def add_item(item, items=[]):   # Bug! The same list is reused on every call
    items.append(item)
    return items

add_item("a")                   # ["a"]
add_item("b")                   # ["a", "b"]  ← surprise!

def add_item(item, items=None): # Fix: default to None, make a new list inside
    if items is None:
        items = []
    items.append(item)
    return items
```

### Putting It Together

```python
def letter_grade(score):
    """Convert a number score to a letter grade."""
    if score >= 90:
        return "A"
    if score >= 80:
        return "B"
    if score >= 70:
        return "C"
    return "F"

def report(scores):
    """Print a formatted grade report."""
    for name, score in scores.items():
        print(f"{name:<8}{score:>5}  {letter_grade(score)}")
    avg = sum(scores.values()) / len(scores)
    print(f"{'Average':<8}{avg:>5.1f}")

report({"Alice": 92, "Bob": 78, "Cara": 85})
# Alice      92  A
# Bob        78  C
# Cara       85  B
# Average  85.0
```

## Lambda Functions

```python
# Small anonymous (unnamed) one-line functions
square = lambda x: x ** 2
square(5)               # 25

add = lambda a, b: a + b
add(3, 4)               # 7

# Mostly used as a `key` for sort, min, max
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort(key=lambda s: s[1])           # Sort by score
max(students, key=lambda s: s[1])           # ("Bob", 92)

words = ["banana", "kiwi", "apple"]
sorted(words, key=lambda w: w[-1])          # ["banana", "apple", "kiwi"] (by last letter)

# Sort by two things: grade (high to low), then name (A to Z)
people = [("Al", 90), ("Cy", 85), ("Bo", 90)]
sorted(people, key=lambda p: (-p[1], p[0]))   # [("Al", 90), ("Bo", 90), ("Cy", 85)]
```

## Map, Filter, Zip

```python
nums = [1, 2, 3, 4]

# map: apply a function to every item
list(map(lambda x: x * 2, nums))    # [2, 4, 6, 8]
list(map(str, nums))                # ["1", "2", "3", "4"]
list(map(int, ["5", "6"]))          # [5, 6]

# filter: keep items where the function returns True
list(filter(lambda x: x % 2 == 0, nums))   # [2, 4]

# Comprehensions usually read better:
[x * 2 for x in nums]               # Same as the map above
[x for x in nums if x % 2 == 0]     # Same as the filter above

# zip: pair up items from multiple lists
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]
list(zip(names, scores))
# [("Alice", 85), ("Bob", 92), ("Charlie", 78)]

for name, score in zip(names, scores):
    print(f"{name}: {score}")

# "Unzip" with *
pairs = [("a", 1), ("b", 2)]
letters, numbers = zip(*pairs)      # ("a", "b") and (1, 2)
```

## *args and **kwargs

```python
# *args: accept any number of positional arguments (arrives as a tuple)
def add_all(*args):
    return sum(args)

add_all(1, 2, 3)         # 6
add_all(1, 2, 3, 4, 5)   # 15

# **kwargs: accept any number of keyword arguments (arrives as a dict)
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25)
# name: Alice
# age: 25

# Can combine both
def func(a, b, *args, **kwargs):
    pass

# The reverse: * and ** UNPACK when calling a function
nums = [1, 2, 3]
add_all(*nums)              # Same as add_all(1, 2, 3)

info = {"name": "Bo", "age": 30}
print_info(**info)          # Same as print_info(name="Bo", age=30)
```

## Common Built-in Functions

```python
len(x)          # Length of string, list, etc.
range(n)        # Numbers 0 to n-1
range(a, b)     # Numbers a to b-1
range(a, b, s)  # Numbers a to b-1, step s

int(x)          # Convert to integer
float(x)        # Convert to float
str(x)          # Convert to string
bool(x)         # Convert to boolean
list(x)         # Convert to list

max(list)       # Maximum value
min(list)       # Minimum value
sum(list)       # Sum of all values
abs(x)          # Absolute value
round(x, n)     # Round to n decimal places
divmod(a, b)    # (a // b, a % b)
pow(a, b)       # a ** b

sorted(list)    # Return sorted copy
reversed(list)  # Return reversed iterator
enumerate(list) # Returns index and value pairs
zip(a, b)       # Pairs up items
any(iterable)   # True if at least one item is truthy
all(iterable)   # True if every item is truthy

type(x)         # Type of x
isinstance(x, int)  # Is x an int?
help(x)         # Show documentation
dir(x)          # List everything x can do
```

```python
# Examples
round(3.14159, 2)       # 3.14
round(7.6)              # 8
round(2.5)              # 2  ← .5 rounds to the nearest EVEN number
round(3.5)              # 4
abs(-7)                 # 7
max(3, 9, 4)            # 9 (works on separate values too)
max(["kiwi", "fig", "banana"], key=len)   # "banana"
sum([0.5, 1.5], 10)     # 12.0 (start value 10)
```

## Error Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
except Exception as e:
    print(f"Error: {e}")
finally:
    print("This always runs")
```

```python
# else runs only if NO error happened
try:
    num = int(input("Number: "))
except ValueError:
    print("That's not a number")
else:
    print(f"You entered {num}")
finally:
    print("Done")

# Catch several error types in one block
try:
    value = int(["5"][0]) / 0
except (ValueError, ZeroDivisionError) as e:
    print(f"Problem: {e}")

# Raise your own errors
def set_age(age):
    if age < 0:
        raise ValueError(f"Age can't be negative: {age}")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(e)            # Age can't be negative: -5

# Retry loop
while True:
    try:
        age = int(input("Age: "))
        break
    except ValueError:
        print("Please enter a whole number.")
```

### Common Error Types

| Error | Cause | Example |
|---|---|---|
| `ValueError` | Right type, bad value | `int("abc")` |
| `TypeError` | Wrong type for the operation | `"a" + 1` |
| `IndexError` | List index out of range | `[1, 2][5]` |
| `KeyError` | Missing dictionary key | `{"a": 1}["b"]` |
| `ZeroDivisionError` | Dividing by zero | `10 / 0` |
| `NameError` | Variable not defined (often a typo) | `print(nmae)` |
| `AttributeError` | That type doesn't have that method | `[1, 2].push(3)` |
| `FileNotFoundError` | File doesn't exist | `open("nope.txt")` |
| `IndentationError` | Inconsistent indentation | Mixing tabs and spaces |
| `SyntaxError` | Code isn't valid Python | Missing `:` or `)` |

## File Handling

```python
# Read file
with open("file.txt", "r") as f:
    content = f.read()          # Read entire file as one string
    # or
    lines = f.readlines()       # Read as a list of lines (each ends with \n)

# Write file (creates it, or ERASES it if it exists)
with open("file.txt", "w") as f:
    f.write("Hello, World!")

# Append to file
with open("file.txt", "a") as f:
    f.write("New line\n")

# `with` closes the file automatically, even if an error happens
```

| Mode | Meaning |
|---|---|
| `"r"` | Read (default). Error if the file doesn't exist |
| `"w"` | Write. Creates the file or **erases** it first |
| `"a"` | Append. Adds to the end |
| `"x"` | Create. Error if the file already exists |
| `"r+"` | Read and write |
| `"rb"` / `"wb"` | Binary mode (images, etc.) |

```python
# Loop over lines (best for big files, reads one line at a time)
with open("file.txt") as f:
    for line in f:
        print(line.strip())     # strip() removes the trailing \n

# With line numbers
with open("file.txt") as f:
    for num, line in enumerate(f, start=1):
        print(f"{num:>3}: {line.rstrip()}")

# Write several lines (write() does NOT add newlines for you)
names = ["Alice", "Bob", "Cara"]
with open("names.txt", "w") as f:
    for name in names:
        f.write(name + "\n")

# print() can write to files too, and adds the newline for you
with open("report.txt", "w") as f:
    for name, score in [("Alice", 92), ("Bob", 78)]:
        print(f"{name:<8}{score:>4}", file=f)

# Read numbers from a file (one per line)
with open("numbers.txt") as f:
    numbers = [int(line) for line in f if line.strip()]

# Always specify encoding for text with special characters
with open("file.txt", encoding="utf-8") as f:
    text = f.read()

# Check if a file exists
from pathlib import Path
if Path("file.txt").exists():
    print("Found it")
```

### CSV Files

```python
import csv

# Read (each row becomes a dict using the header row)
with open("scores.csv", newline="") as f:
    for row in csv.DictReader(f):
        print(row["name"], row["score"])    # Values are always strings!

# Write
with open("scores.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "score"])      # Header
    writer.writerow(["Alice", 92])
    writer.writerows([["Bob", 78], ["Cara", 85]])
```

## JSON

```python
import json

# Python dict to JSON string
data = {"name": "Alice", "age": 25}
json_str = json.dumps(data)              # '{"name": "Alice", "age": 25}'
json_pretty = json.dumps(data, indent=2) # Pretty-printed

# JSON string to Python dict
parsed = json.loads(json_str)
parsed["name"]                            # "Alice"

# Read/write JSON files
with open("data.json", "r") as f:
    data = json.load(f)

with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

# Example: save and load a high score list
scores = [{"player": "Al", "score": 120}, {"player": "Bo", "score": 95}]
with open("scores.json", "w") as f:
    json.dump(scores, f, indent=2)

with open("scores.json") as f:
    loaded = json.load(f)
for entry in loaded:
    print(f"{entry['player']}: {entry['score']}")
```

## Working with Dates & Times

```python
from datetime import datetime, date, timedelta

# Current date/time
now = datetime.now()
today = date.today()

# Create specific date
birthday = date(2000, 5, 15)
meeting = datetime(2026, 9, 22, 14, 5)

# Format dates
meeting.strftime("%Y-%m-%d")        # "2026-09-22"
meeting.strftime("%B %d, %Y")       # "September 22, 2026"
meeting.strftime("%I:%M %p")        # "02:05 PM"
f"{meeting:%A, %b %d}"              # "Tuesday, Sep 22" (same codes work in f-strings)

# Parse a string into a date
datetime.strptime("2026-09-22", "%Y-%m-%d")     # datetime(2026, 9, 22, 0, 0)

# Date math
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
diff = date(2026, 12, 25) - date(2026, 9, 22)   # timedelta object
print(diff.days)                                 # 94
```

| Code | Meaning | Example |
|---|---|---|
| `%Y` | 4-digit year | `2026` |
| `%y` | 2-digit year | `26` |
| `%m` | Month (01–12) | `09` |
| `%B` | Month name | `September` |
| `%b` | Short month name | `Sep` |
| `%d` | Day (01–31) | `22` |
| `%A` | Weekday name | `Tuesday` |
| `%a` | Short weekday | `Tue` |
| `%H` | Hour, 24-hour (00–23) | `14` |
| `%I` | Hour, 12-hour (01–12) | `02` |
| `%M` | Minute | `05` |
| `%S` | Second | `00` |
| `%p` | AM/PM | `PM` |

## Regular Expressions

```python
import re

text = "My email is alice@example.com and bob@test.org"

# Search for pattern
match = re.search(r"\d+", "There are 42 apples")
if match:
    print(match.group())        # "42"

# Find all matches
emails = re.findall(r"[\w.]+@[\w.]+", text)
# ["alice@example.com", "bob@test.org"]

# Replace
cleaned = re.sub(r"\d+", "X", "abc123def456")
# "abcXdefX"

# Groups: pull out parts of a match with ( )
m = re.search(r"(\w+)@(\w+)\.com", text)
m.group(1)                      # "alice"
m.group(2)                      # "example"

# Check if a whole string matches
bool(re.fullmatch(r"\d{3}-\d{4}", "555-1234"))   # True

# Common patterns
r"\d"       # Digit (0-9)
r"\w"       # Word character (a-z, A-Z, 0-9, _)
r"\s"       # Whitespace
r"."        # Any character except newline
r"+"        # One or more
r"*"        # Zero or more
r"?"        # Zero or one
r"{3}"      # Exactly 3
r"[abc]"    # Character class (a, b, or c)
r"^"        # Start of string
r"$"        # End of string
```

## Classes (OOP Basics)

```python
class Dog:
    # Class variable (shared by all instances)
    species = "Canis familiaris"

    # Constructor
    def __init__(self, name, age):
        self.name = name        # Instance variable
        self.age = age

    # Method
    def bark(self):
        return f"{self.name} says Woof!"

    # String representation
    def __str__(self):
        return f"{self.name}, age {self.age}"

# Create objects
my_dog = Dog("Rex", 5)
print(my_dog.name)          # Rex
print(my_dog.bark())        # Rex says Woof!
print(my_dog)               # Rex, age 5

# Inheritance
class Puppy(Dog):
    def __init__(self, name, age, toy):
        super().__init__(name, age)
        self.toy = toy

    def play(self):
        return f"{self.name} plays with {self.toy}"
```

### Methods That Change State

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        self.balance -= amount

    def __str__(self):
        return f"{self.owner}: ${self.balance:,.2f}"

acct = BankAccount("Alice", 100)
acct.deposit(50)
acct.withdraw(30)
print(acct)                 # Alice: $120.00

# Lists of objects work great with loops
accounts = [BankAccount("Al", 500), BankAccount("Bo", 1200)]
for a in accounts:
    print(a)
total = sum(a.balance for a in accounts)    # 1700
```

### Dataclasses (Less Boilerplate)

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float

p = Point(1, 2)
print(p)                    # Point(x=1, y=2) (__init__ and __repr__ written for you)
p == Point(1, 2)            # True (__eq__ too)
```

## Modules & Imports

```python
# Import entire module
import math
math.sqrt(16)               # 4.0

# Import specific items
from math import sqrt, pi
sqrt(16)                    # 4.0

# Import with alias
import numpy as np

# Common standard library modules
import os               # File system operations
import sys              # System-specific parameters
import math             # Math functions
import random           # Random numbers
import datetime         # Date and time
import json             # JSON encoding/decoding
import re               # Regular expressions
import collections      # Specialized containers
```

```python
# Importing your own file: if you have helpers.py in the same folder
from helpers import my_function

# Only run code when the file is run directly (not when imported)
def main():
    print("Running!")

if __name__ == "__main__":
    main()
```

## Decorators

```python
# A decorator wraps a function to add behavior
def timer(func):
    import time
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f}s")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(1)

slow_function()     # Prints: slow_function took 1.00s
```

## Generators

```python
# Generators produce values one at a time (memory efficient)
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for num in countdown(5):
    print(num)              # 5, 4, 3, 2, 1

# Get values one at a time with next()
gen = countdown(3)
next(gen)                   # 3
next(gen)                   # 2

# Generator expression (like list comp but with parentheses)
squares = (x**2 for x in range(1000000))  # Doesn't store all in memory
```

## Unpacking & Advanced Assignment

```python
# List/tuple unpacking
first, *rest = [1, 2, 3, 4, 5]
# first = 1, rest = [2, 3, 4, 5]

first, *middle, last = [1, 2, 3, 4, 5]
# first = 1, middle = [2, 3, 4], last = 5

# Dictionary merging (Python 3.9+)
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}
merged = dict1 | dict2     # {"a": 1, "b": 3, "c": 4}

# Walrus operator (Python 3.8+): assign and use in one step
if (n := len("hello")) > 3:
    print(f"Length {n} is greater than 3")
```

## Common Patterns

```python
# Counting items
from collections import Counter
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
counts = Counter(words)
# Counter({"apple": 3, "banana": 2, "cherry": 1})
counts.most_common(2)       # [("apple", 3), ("banana", 2)]
Counter("hello")            # Counter({"l": 2, "h": 1, "e": 1, "o": 1})

# Default dictionary
from collections import defaultdict
grouped = defaultdict(list)
for name, score in [("Alice", 85), ("Bob", 92), ("Alice", 90)]:
    grouped[name].append(score)
# {"Alice": [85, 90], "Bob": [92]}

# Enumerate with start index
for i, item in enumerate(["a", "b", "c"], start=1):
    print(f"{i}. {item}")   # 1. a, 2. b, 3. c

# any() and all()
nums = [2, 4, 6, 8]
all(x % 2 == 0 for x in nums)   # True (all even)
any(x > 5 for x in nums)        # True (at least one > 5)

# Clamp a value between a min and max
speed = 150
max(0, min(speed, 100))         # 100
```

## Useful Shortcuts

```python
# Swap variables
a, b = b, a

# Multiple assignment
x, y, z = 1, 2, 3

# Check if string is a number
"123".isdigit()     # True

# Join list to string
", ".join(["a", "b", "c"])  # "a, b, c"

# Reverse a string or list
"hello"[::-1]       # "olleh"

# Check if a word is a palindrome
word = "racecar"
word == word[::-1]  # True

# Random
import random
random.randint(1, 10)       # Random int 1-10 (both ends included)
random.random()             # Random float 0.0 to 1.0
random.choice(my_list)      # Random item from list
random.sample(my_list, 3)   # 3 random items, no repeats
random.shuffle(my_list)     # Shuffle list in place
```

## Code Style (PEP 8)

PEP 8 is Python's official style guide. Following it makes your code easier for others (and future you) to read.

```python
# Indentation: 4 spaces per level (not tabs)
def example():
    if True:
        print("4 spaces each level")

# Naming
player_score = 10           # Variables & functions: snake_case
MAX_PLAYERS = 4             # Constants: UPPER_SNAKE_CASE
class GameBoard:            # Classes: PascalCase
    pass

# Spaces around operators and after commas
total = price * quantity + tax      # Good
total=price*quantity+tax            # Hard to read
print(a, b, c)                      # Good
print( a,b ,c )                     # Bad

# No spaces around = for keyword arguments or defaults
def greet(name="World"):            # Good
    pass
greet(name="Al")                    # Good

# Break long lines inside parentheses
total = (first_value
         + second_value
         + third_value)

# Two blank lines between top-level functions/classes, one between methods
# Imports at the top of the file, one per line
# Keep lines under about 79-100 characters
```

**Let a tool do it for you:**

```bash
pip install black
black my_file.py            # Reformats the file automatically

pip install ruff
ruff check my_file.py       # Finds style problems and common bugs
ruff format my_file.py      # Reformats (like black)
```

## Virtual Environments & pip

```bash
# Create a virtual environment
python -m venv myenv

# Activate it
myenv\Scripts\activate          # Windows
source myenv/bin/activate       # Mac/Linux

# Install packages
pip install requests
pip install requests==2.28.0    # Specific version
pip install -r requirements.txt # From file

# Save current packages
pip freeze > requirements.txt

# Deactivate
deactivate
```
