# Python
---

## Useful CLI Argument
Useful CLI options when running Python scripts: `python [cli-argument] script.py`

* `-c`: Run Python code directly from the command line.
  ```bash
  python -c "print('Hello World')"

* -m: Run a Python module. The directory must contain __main__.py, and all files in python are treated as modules.
    ```python
        <!-- File Structure -->
        root
            .venv # The virtual enviroment files
            module_a
                __init__.py
                __main__.py
                other_modules.py
            module_b
                __init__.py
                __main__.py
        <!-- End of file structure -->

        <!-- Terminal -->
        >>> python -m module_a
        >>> python -m module_b
        >>> python -m other_modules
        >>> python -m other-modules-in-.venv
    ```
* -i: Run Python in interactive mode; all other values defined in the script will be available.
  ```python
    <!-- scripts.py -->
    name = "West"
    <!-- end of scripts -->

    $bash: python -i scripts.py

    >>> Python
    >>> print(name)
    >>> West  
  ```
* -O run python in non debug mode this will remove all assert statement
  ```python
  assert False, "assert will be ignored"

  if __debug__:
    print("Won't print because -O is passed")
  ```
For more python cli argument check [Python Docs](https://docs.python.org/3/using/cmdline.html#using-on-general, "Python Cli documentation")

## Functions
* Python support default argument
  ```python
    def func(args="West") -> None:
        print(args)

    func() # West
    func("East") # East
  ```
* Keyword arguments and Positional arguments, 
  ```python
    # This function accepts keyword-only arguments
    def func(*, name) -> None:
        print(f"Keyword-only argument: {name}")

    # This function accepts both positional and keyword arguments
    def func_pos(pos_arg, /, **kwd_pos) -> None:
        print(f"Positional argument: {pos_arg}")
        print(f"Keyword arguments: {kwd_pos}")

    # Correct usage:
    func(name="West") # This works

    # This won't work because 'func' only accepts keyword arguments
    # func("args", name="West") 

    # Correct usage for the second function:
    func_pos("args", name="West") # This works

  ```

## Data Structures
Python has a collection of objects, that can be used to organized, stored and manipulated data

| Mutable Data Structures         | Immutable Data Structures           |
| ------------------------------- | ----------------------------------- |
| **List**                        | **Tuple**                           |
| **Dictionary**                  | **String**                          |
| **Set**                         | **Frozenset**                       |
| **Queue** (from `queue` module) | **Bytes**                           |
| **Deque** (from `collections`)  | **NamedTuple** (from `collections`) |

Mutable data can be modified while non mutable will result in the creation of a new object

### Common Pitfalls
    ```python
        def func(items=[]) -> None:
            items.append("foo")
            print(items)

        func() # ["foo"]
        # This will print foo twice because items is shared
        func() # ["foo", "foo"]

        # Fixed
        def func(items: list | None) -> None:
            if items is None:
                items = []
            items.append("foo")
            print(items)

        # Assume range returns a sequence of bytes
        for data in range(1, 200):
            # This creates many new strings in memory because strings are immutable
            name += str(data)  # Convert `data` to string for concatenation

        # Using StringIO for efficient string concatenation
        buffer = StringIO()

        for data in range(1, 200):
            # This is better because it avoids creating multiple new strings
            buffer.write(str(data))  # Use write() instead of append()

        # If you want to see the final concatenated result:
        result = buffer.getvalue()
        print(result)  # This will print the concatenated string of numbers
    ```
## Scope 
scope is a textual region program is directly accessible, we have 3 types of scope which are local, nonlocal and global
[Refer to these docs to learn it better](https://docs.python.org/3/tutorial/classes.html#scopes-and-namespaces-example)

## Classes
Classes provides a means of bundling data and functionality together, Python class support inheritance, polymorphism and staticmethod.

* Inheritance: Python has 2 functions that works with inheritance 
  ```python
    isinstance(isntance_object, Type) # compare if a given instance is a subclass of a given type

    issubclass(Type, Type) # compare 2 types 
  ```
  python doesn't support private variables but it has a convention of using __property to indicate a property or method is private

  