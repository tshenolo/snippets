# Python Cheatsheet

This cheatsheet provides common Python syntax, data structures, control flow, functions, OOP concepts, and standard library examples.

## Basic Syntax & Variables

*   **Variables**: Dynamically typed. No explicit declaration needed.
    ```python
    name = "Alice"
    age = 30
    height = 5.8
    is_student = False
    ```
*   **Printing Output**:
    ```python
    print("Hello, World!")
    print(f"Name: {name}, Age: {age}") # f-strings (Python 3.6+)
    print("Name: {}, Age: {}".format(name, age)) # .format() method
    ```
*   **Comments**:
    ```python
    # This is a single-line comment
    """
    This is a
    multi-line comment (docstring if first statement in a module/function/class).
    """
    '''
    Also a multi-line comment.
    '''
    ```
*   **Input from User**:
    ```python
    user_input = input("Enter your name: ")
    print(f"Hello, {user_input}")
    age_str = input("Enter your age: ")
    age_num = int(age_str) # Convert string to integer
    ```

## Data Types

*   **Numbers**:
    *   Integers: `x = 10`, `y = -5`
    *   Floats: `pi = 3.14`, `price = 19.99`
    *   Complex: `c = 2 + 3j`
*   **Strings**: Immutable sequences of characters.
    ```python
    s1 = 'single quotes'
    s2 = "double quotes"
    s3 = """multi-line
    string"""
    # String methods
    print(s1.upper())       # 'SINGLE QUOTES'
    print(s2.lower())       # 'double quotes'
    print(s2.find('oub'))   # 1 (index)
    print(s2.replace('double', 'triple')) # 'triple quotes'
    print("apple,banana,cherry".split(',')) # ['apple', 'banana', 'cherry']
    print(" ".join(['Python', 'is', 'fun'])) # 'Python is fun'
    ```
*   **Booleans**: `True` or `False` (case-sensitive).
*   **Lists**: Ordered, mutable sequences.
    ```python
    my_list = [1, "hello", 3.14, True]
    print(my_list[0])      # 1 (access by index)
    my_list.append("new")  # Add item to end
    my_list.insert(1, 2)   # Insert 2 at index 1
    my_list.pop()          # Remove and return last item
    my_list.remove("hello")# Remove first occurrence of "hello"
    print(len(my_list))    # Get length
    numbers = [3, 1, 4, 1, 5, 9]
    numbers.sort()         # Sorts in-place
    print(numbers)
    ```
*   **Tuples**: Ordered, immutable sequences.
    ```python
    my_tuple = (1, "world", 2.71)
    print(my_tuple[1])     # "world"
    # my_tuple[0] = 5      # TypeError: 'tuple' object does not support item assignment
    # Often used for fixed collections of items or as dictionary keys (if elements are hashable)
    ```
*   **Dictionaries (dict)**: Unordered (ordered in Python 3.7+) collections of key-value pairs. Mutable.
    ```python
    my_dict = {"name": "Bob", "age": 25, "city": "New York"}
    print(my_dict["name"]) # "Bob" (access by key)
    print(my_dict.get("country", "USA")) # Get value, with default if key not found
    my_dict["email"] = "bob@example.com" # Add/update key-value pair
    del my_dict["city"]    # Delete key-value pair
    print(my_dict.keys())  # dict_keys(['name', 'age', 'email'])
    print(my_dict.values())# dict_values(['Bob', 25, 'bob@example.com'])
    print(my_dict.items()) # dict_items([('name', 'Bob'), ('age', 25), ...])
    for key, value in my_dict.items():
        print(f"{key}: {value}")
    ```
*   **Sets**: Unordered collections of unique items. Mutable.
    ```python
    my_set = {1, 2, 3, 3, "apple"} # {1, 2, 3, 'apple'} (duplicates removed)
    set1 = {1, 2, 3}
    set2 = {3, 4, 5}
    print(set1.union(set2))        # {1, 2, 3, 4, 5}
    print(set1 | set2)             # Union
    print(set1.intersection(set2)) # {3}
    print(set1 & set2)             # Intersection
    print(set1.difference(set2))   # {1, 2}
    print(set1 - set2)             # Difference
    my_set.add(4)
    my_set.remove(1) # Raises KeyError if item not found
    my_set.discard(10) # Does not raise error if item not found
    ```

## Operators

*   **Arithmetic**: `+`, `-`, `*`, `/` (float division), `//` (integer division), `%` (modulo), `**` (exponentiation).
*   **Comparison**: `==`, `!=`, `>`, `<`, `>=`, `<=`.
*   **Logical**: `and`, `or`, `not`.
*   **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `//=` `**=`.
*   **Membership**: `in`, `not in` (used with sequences like lists, strings, tuples, sets, dict keys).
    ```python
    print(1 in [1, 2, 3])  # True
    print("a" not in "hello") # True
    ```
*   **Identity**: `is`, `is not` (checks if two variables point to the same object in memory).
    ```python
    a = [1, 2]
    b = [1, 2]
    c = a
    print(a == b) # True (values are the same)
    print(a is b) # False (different objects in memory)
    print(a is c) # True (c points to the same object as a)
    ```

## Control Flow

*   **If/Elif/Else**:
    ```python
    x = 10
    if x > 15:
        print("x is greater than 15")
    elif x > 5:
        print("x is greater than 5 but not 15")
    else:
        print("x is 5 or less")
    ```
*   **For Loops**: Iterate over a sequence.
    ```python
    fruits = ["apple", "banana", "cherry"]
    for fruit in fruits:
        print(fruit)

    for i in range(5): # range(5) generates 0, 1, 2, 3, 4
        print(i)

    for i in range(2, 6): # range(2, 6) generates 2, 3, 4, 5
        print(i)

    for i in range(0, 10, 2): # range(start, stop, step) generates 0, 2, 4, 6, 8
        print(i)
    ```
*   **While Loops**: Execute as long as a condition is true.
    ```python
    count = 0
    while count < 5:
        print(count)
        count += 1
    ```
*   **Break and Continue**:
    *   `break`: Exits the current loop prematurely.
    *   `continue`: Skips the rest of the current iteration and proceeds to the next.
    ```python
    for i in range(10):
        if i == 3:
            continue # Skip printing 3
        if i == 7:
            break    # Exit loop when i is 7
        print(i)
    ```
*   **Pass**: A null operation; does nothing. Used as a placeholder.
    ```python
    def my_empty_function():
        pass # To be implemented later
    ```

## Functions

*   **Defining Functions**:
    ```python
    def greet(name):
        """This function greets the person passed in as a parameter."""
        print(f"Hello, {name}!")

    greet("Alice") # Call the function
    ```
*   **Return Values**:
    ```python
    def add(x, y):
        return x + y

    result = add(5, 3)
    print(result) # 8
    ```
*   **Arguments**:
    *   Positional arguments: `add(5, 3)`
    *   Keyword arguments: `add(x=5, y=3)` or `add(y=3, x=5)`
    *   Default argument values:
        ```python
        def power(base, exponent=2):
            return base ** exponent
        print(power(3))    # 9 (uses default exponent 2)
        print(power(3, 3)) # 27
        ```
    *   Arbitrary arguments (`*args` for positional, `**kwargs` for keyword):
        ```python
        def print_all(*args, **kwargs):
            print("Positional arguments:", args) # args is a tuple
            print("Keyword arguments:", kwargs)   # kwargs is a dictionary

        print_all(1, "hello", name="John", age=30)
        # Positional arguments: (1, 'hello')
        # Keyword arguments: {'name': 'John', 'age': 30}
        ```
*   **Lambda Functions**: Small, anonymous functions defined with `lambda`.
    ```python
    multiply = lambda x, y: x * y
    print(multiply(4, 5)) # 20

    # Often used with functions like map(), filter(), sorted()
    numbers = [1, 2, 3, 4, 5]
    squared = list(map(lambda x: x**2, numbers)) # [1, 4, 9, 16, 25]
    evens = list(filter(lambda x: x % 2 == 0, numbers)) # [2, 4]
    ```
*   **Scope**: LEGB (Local, Enclosing function locals, Global, Built-in).
    ```python
    x_global = 10 # Global variable

    def my_func():
        x_local = 5 # Local variable
        print(x_local)
        print(x_global) # Can access global

    my_func()
    # print(x_local) # NameError: x_local is not defined outside the function

    def outer():
        message = "outer"
        def inner():
            # nonlocal message # Use 'nonlocal' to modify parent function's variable
            print(message) # Accesses 'message' from enclosing scope
        inner()
    outer()
    ```

## List Comprehensions

Concise way to create lists.
```python
squares = [x**2 for x in range(10)] # [0, 1, 4, ..., 81]
even_squares = [x**2 for x in range(10) if x % 2 == 0] # [0, 4, 16, 36, 64]

# Equivalent for loop for 'squares':
# squares = []
# for x in range(10):
#   squares.append(x**2)

# Dictionary comprehensions
names = ["Alice", "Bob", "Charlie"]
name_lengths = {name: len(name) for name in names} # {'Alice': 5, 'Bob': 3, 'Charlie': 7}

# Set comprehensions
nums = [1, 2, 2, 3, 4, 4, 5]
unique_squares = {x**2 for x in nums} # {1, 4, 9, 16, 25}
```

## Object-Oriented Programming (OOP)

*   **Classes and Objects**:
    ```python
    class Dog:
        # Class attribute (shared by all instances)
        species = "Canis familiaris"

        # Constructor (initializer)
        def __init__(self, name, age):
            # Instance attributes
            self.name = name
            self.age = age

        # Instance method
        def bark(self):
            print(f"{self.name} says Woof!")

        def get_age(self):
            return self.age

    # Create objects (instances)
    my_dog = Dog("Buddy", 3)
    another_dog = Dog("Lucy", 5)

    print(my_dog.name)        # Buddy
    my_dog.bark()             # Buddy says Woof!
    print(Dog.species)        # Canis familiaris
    print(another_dog.get_age()) # 5
    ```
*   **Inheritance**:
    ```python
    class GoldenRetriever(Dog): # GoldenRetriever inherits from Dog
        def __init__(self, name, age, color="golden"):
            super().__init__(name, age) # Call constructor of the parent class (Dog)
            self.color = color

        # Override parent's method
        def bark(self):
            print(f"{self.name} says Gentle Woof!")

        def fetch(self):
            print(f"{self.name} is fetching the ball!")

    my_golden = GoldenRetriever("Charlie", 2)
    my_golden.bark()  # Charlie says Gentle Woof!
    my_golden.fetch() # Charlie is fetching the ball!
    print(my_golden.species) # Canis familiaris (inherited)
    ```
*   **Encapsulation**: Using naming conventions for "private" attributes (e.g., `_protected`, `__private` - name mangling). Python doesn't have true private attributes like Java or C++.
*   **Polymorphism**: Objects of different classes can respond to the same method call.

## Decorators

A way to modify or enhance functions or methods. A decorator is a function that takes another function and extends its behavior without explicitly modifying it.
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Something is happening before the function is called.")
        result = func(*args, **kwargs)
        print("Something is happening after the function is called.")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    print(f"Hello, {name}!")

say_hello("World")
# Output:
# Something is happening before the function is called.
# Hello, World!
# Something is happening after the function is called.

# Example: Timing a function
import time
def timer_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Function {func.__name__} took {end_time - start_time:.4f} seconds")
        return result
    return wrapper

@timer_decorator
def slow_function():
    time.sleep(1)
    print("Function finished.")

slow_function()
```

## Modules and Packages

*   **Modules**: A file containing Python definitions and statements (e.g., `my_module.py`).
*   **Importing Modules**:
    ```python
    import math # Import the whole module
    print(math.sqrt(16)) # 4.0

    from math import pi, factorial # Import specific items
    print(pi)
    print(factorial(5)) # 120

    from math import * # Import all names (generally discouraged)
    print(sqrt(25))

    import math as m # Import with an alias
    print(m.sin(m.pi/2)) # 1.0
    ```
*   **Packages**: A collection of modules in a directory hierarchy. The directory must contain an `__init__.py` file (can be empty) to be considered a package.
    ```
    my_package/
        __init__.py
        module1.py
        module2.py
        sub_package/
            __init__.py
            module3.py
    ```
    ```python
    # Assuming my_package is in PYTHONPATH or current directory
    import my_package.module1
    my_package.module1.some_function()

    from my_package import module2
    module2.another_function()

    from my_package.sub_package.module3 import yet_another_function
    yet_another_function()
    ```

## File I/O (Input/Output)

*   **Reading from a file**:
    ```python
    # Recommended way using 'with' (ensures file is closed)
    try:
        with open("myfile.txt", "r") as f: # "r" for read mode
            content = f.read() # Read entire file
            print(content)

        with open("myfile.txt", "r") as f:
            for line in f: # Read line by line (memory efficient)
                print(line.strip()) # strip() removes leading/trailing whitespace

        with open("myfile.txt", "r") as f:
            lines = f.readlines() # Read all lines into a list
            print(lines)
    except FileNotFoundError:
        print("Error: File not found.")
    ```
*   **Writing to a file**:
    ```python
    # "w" for write mode (overwrites file if it exists, creates if not)
    with open("output.txt", "w") as f:
        f.write("Hello, Python!\n")
        f.write("This is a new line.")

    # "a" for append mode (adds to end of file, creates if not)
    with open("output.txt", "a") as f:
        f.write("\nAppending this line.")
    ```
*   **File Modes**:
    *   `'r'`: Read (default).
    *   `'w'`: Write (truncates file).
    *   `'a'`: Append.
    *   `'x'`: Exclusive creation (fails if file exists).
    *   `'b'`: Binary mode (e.g., `'rb'`, `'wb'`).
    *   `'+'`: Read and Write (e.g., `'r+'`, `'w+'`).

## Error Handling (Exception Handling)

*   **Try/Except/Else/Finally**:
    ```python
    try:
        numerator = int(input("Enter numerator: "))
        denominator = int(input("Enter denominator: "))
        result = numerator / denominator
    except ValueError:
        print("Invalid input. Please enter numbers.")
    except ZeroDivisionError:
        print("Error: Cannot divide by zero.")
    except Exception as e: # Catch any other exceptions
        print(f"An unexpected error occurred: {e}")
    else:
        # Executed if no exceptions were raised in the try block
        print(f"Result is: {result}")
    finally:
        # Always executed, whether an exception occurred or not
        # Useful for cleanup (e.g., closing files, database connections)
        print("Calculation attempt finished.")
    ```
*   **Raising Exceptions**:
    ```python
    def get_age(age_val):
        if age_val < 0:
            raise ValueError("Age cannot be negative.")
        return age_val

    try:
        my_age = get_age(-5)
    except ValueError as e:
        print(e) # Age cannot be negative.
    ```

## Common Standard Library Modules

*   **`os`**: Interacting with the operating system.
    ```python
    import os
    print(os.getcwd()) # Get current working directory
    # os.mkdir("new_dir")
    # os.rename("old.txt", "new.txt")
    print(os.path.exists("myfile.txt"))
    print(os.listdir(".")) # List files and directories
    ```
*   **`sys`**: System-specific parameters and functions.
    ```python
    import sys
    print(sys.argv) # Command-line arguments (list, script name is argv[0])
    # sys.exit(0) # Exit script
    print(sys.platform) # e.g., 'linux', 'win32'
    ```
*   **`datetime`**: Working with dates and times.
    ```python
    import datetime
    now = datetime.datetime.now()
    print(now)
    today = datetime.date.today()
    print(today)
    print(now.strftime("%Y-%m-%d %H:%M:%S")) # Format date
    date_str = "2023-01-15"
    parsed_date = datetime.datetime.strptime(date_str, "%Y-%m-%d").date()
    print(parsed_date)
    ```
*   **`json`**: Encoding and decoding JSON data.
    ```python
    import json
    data = {"name": "Eve", "age": 28, "city": "London"}
    json_string = json.dumps(data, indent=4) # Encode to JSON string
    print(json_string)

    parsed_data = json.loads(json_string) # Decode JSON string to Python dict
    print(parsed_data["name"])
    ```
*   **`re`**: Regular expression operations.
    ```python
    import re
    text = "The rain in Spain stays mainly in the plain."
    matches = re.findall("ai", text)
    print(matches) # ['ai', 'ai', 'ai', 'ai']

    search_result = re.search(r"\bS\w+", text) # Find word starting with S
    if search_result:
        print(search_result.group()) # Spain
    ```
*   **`math`**: Mathematical functions.
    ```python
    import math
    print(math.sqrt(25))  # 5.0
    print(math.pi)        # 3.14159...
    print(math.ceil(4.2)) # 5
    print(math.floor(4.8))# 4
    ```
*   **`random`**: Generating pseudo-random numbers.
    ```python
    import random
    print(random.randint(1, 10)) # Random integer between 1 and 10 (inclusive)
    print(random.random())       # Random float between 0.0 and 1.0
    my_list = [1, 2, 3, 4, 5]
    print(random.choice(my_list)) # Random element from list
    random.shuffle(my_list)       # Shuffle list in-place
    print(my_list)
    ```

This provides a much more detailed and actionable cheatsheet for Python. I'll continue with `javascript.md`.The `python.md` cheatsheet has been successfully enhanced with detailed syntax examples, code snippets for data structures, control flow, functions, OOP, decorators, and common standard library modules, all formatted as requested.

Next, I will enhance `javascript.md` in a similar fashion, focusing on ES6+ features, DOM manipulation, and common array/object methods.
