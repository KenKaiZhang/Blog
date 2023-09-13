# Python Concepts

Python is a **strongly-typed** language where type coercion (implicit conversion of data types) is not allowed.

- `"1" + 2` results in an error

Python executes each atate line by line, making it a **interpreted language** that is **dynamically typed** since it checks data types during execution

---

**PEP 8 (Python Enhancement Proposal)**: the official design documentation highlighting new features for Python or its processes

- Sets style guidelines for Python Code keeping contribution to Python open-source community uniform

---

**scope**: block of code where objects remain relevant

- **local scope**: objects available in the current function

```python
def cope():
    value = 1
    print(value)
scope()

OUTPUT: 1
```

- **enclosing/non-local scope**: objects created in a nested function and only available in there

```python
def parent_nest():
    value1 = 5
    def child_nest():
        value2 = 10     # enclosing scope
        print(value1)
        print(value2)
    child_nest()
parent_nest()

OUTPUT:
5
10
```

- **global scope**: objects available from inception

```python
value = 1
def local_scope():
    print(value)
scope()

OUTPUT: 1
```

- **built-in scope**: objects built into python

```python
False   True    class
None    and     or
...
```

---

Python does not require predefined data types on variable declaration, but types can be checked with `type()` and `isinstance()`

**None**:

- `None`: null values

**Numeric**

- `int`: integer literals including hex, octal, and binary
- `float`: literals with decimal
- `complex`: complex numbers defined using `complex(real, img)`
- `bool`: true/false

**Sequence**: allows for `in` and `not in`

- `list`: mutable
- `tuple`: immutable
- `range`: immutable sequence of numbers
- `str`: immutable sequece of textual data

**Map**: allows for map hashing

- `dict`: **key**, **value** pairs

**Set**

- `set`: mutable collection of distinct hashed objects
- `frozenset`: immutable collection of distinct hashed object

---

**`pass`**: null operation that fills up empty blocks of code that would cause errors if not filled

**`break`**: terminates the ongoing loop

**`continue`**: skips to next iteration of ongoing loop

---

**global variables**: public variables that are defined in the global scope, readable from anywhere

- Requires the `global` keyword to be modifiable in a function

```python
x = "hello world"

def change_global():
    x = "goodbye world"

change_global()
print(x)

OUTPUT:
goodbye world
```

**protected variables**:

---
