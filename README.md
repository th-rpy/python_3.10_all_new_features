# Python 3.10 : What's the new ?

The release of ✨Python 3.10✨ is getting closer, so it's time to take a ride with the new version of Python and see what awesome new features will come with this new release👌 😍. 

## Install Python 3.10 Alpha version

To try these new features, we will have to install the Alpha/Beta version of Python 3.10. Remember that this last version is not yet stable. 
- If you are under Linux (Ubuntu), you just have to follow the steps below : 

     ```sh
     # Download the latest version for Linux
     wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0a6.tgz
     # Unpack Python source code
     tar xzvf Python-3.10.0a6.tgz
    cd Python-3.10.0a6
    # Compile Python source with static libraries
    ./configure --prefix=$HOME/python-3.10.0a6
    make
    make install
    $HOME/python-3.10.0a6/bin/python3.10
    ```
- If you are under Windows, you just have to **Download Python Executable** Installer from [here](https://www.python.org/ftp/python/3.10.0/python-3.10.0a6-amd64.exe), then you need to **Run Executable Installer**. 
- If you are on MacOs, I can't help you. I am not rich enough to buy a Mac!!! 😒, but this [link](https://opensource.com/article/19/5/python-3-default-mac) may help you. 

Yeeeep, Python 3.10 is finally installed ✌ , now we can take a look at all the new features . Let's start 😉😎. 

### New Type Union Operator
Instead of using typing.union to express the syntax **"either type X or type Y"**, the new version of python introduces the new union operator of type *X | Y*. This new operator allows us to code more cleanly and efficiently.

- **Old Version**
     ```python
    from typing import Union
    def square(number: Union[int, float]) -> Union[int, float]:
        return number ** 2
    isinstance('3', int | str)
    ```
- **New Version**
     ```python
    def square(number: int | float) -> int | float:
        return number ** 2
    isinstance('3', int | str)
    ```
This features was contributed by Ken Jin. Visit this link ([PEP 612](https://www.python.org/dev/peps/pep-0612)) for more details. 

### TypeAlias Annotation
The TypeAlias annotation concept was first introduced in PEP 484 (Python-Version: 3.5) . A reimplementation of this concept will be presented in PEP 613 (Python-Version: 3.10). The main reason for this reimplementation is that the old concept is very difficult for type checkers to distinguish between type aliases and ordinary assignments.  See the following example:
- **Old Version**
     ```python
    StrCache = 'Cache[str]'  # a type alias
    LOG_PREFIX = 'LOG[DEBUG]'  # a module constant
    ```
- **New Version**
     ```python
    StrCache: TypeAlias = 'Cache[str]'  # a type alias
    LOG_PREFIX = 'LOG[DEBUG]'  # a module constant
    ```
This features was contributed by  Mikhail Golubev. Visit this link ([PEP 613](https://www.python.org/dev/peps/pep-0613)) for more details.

### Better error messages in the parser
Suppose you want to write a code that manipulates for example a dictionary (or tuple , list or set ) and you forget to close the brackets (or the parentheses). If you are working with python 3, when you execute your code, the interpreter will display a syntax error like this one **"SyntaxError : unexpected EOF"**. 
However, with this new version, when you try to parse code that contains unclosed parentheses or brackets, the interpreter will displays a more informative error with the location of the unclosed parenthesis or brackets. 
- **Old Version**
     ```python
    File "example.py", line 3
    some_other_code = foo()
                    ^
    SyntaxError: invalid syntax
    ```
- **New Version**
     ```python
    File "example.py", line 1
    expected = {9: 1, 18: 2, 19: 2, 27: 3, 28: 3, 29: 3, 36: 4, 37: 4,
               ^
    SyntaxError: '{' was never closed
    ```
This features was contributed by Pablo Galindo and Batuhan Taskaya.

### Structural Pattern Matching

We can say that the most important feature will be introduced in this new Python 3. 
Pattern matching will be presented in the common form: match statement and case statements of patterns with associated actions.  Patterns can be: sequences, mappings, primitive data types as well as class instances. By using pattern matching, we are able to, for example, extract information from complex data types, plug into the data structure, and apply specific actions based on different data forms. This is not just the switch/case syntax we all know from other programming languages, but it also adds powerful functionality that we should explore. 

- **Example 1: Simple pattern: match to a literal** 
    ```python
    def func(x):
        match x:
            case "x1":
                return "x1 .."
            case "x2":
                return "x2"
            case "x3" | "x4":  # Multiple literals can be combined with `|`
                return "Yay, "
            case _:
                return "Just another x..."
    ```

- **Example 2: Patterns with a literal and variable** 
    ```python
    def func(X):  # X = (x, y, z)
        # point is an (x, y) tuple
        match point:
            case (0, 0):
                print("Origin")
            case (0, y):
                print(f"Y={y}")
            case (x, 0):
                print(f"X={x}")
            case (x, y):
                print(f"X={x}, Y={y}")
            case _:
                raise ValueError("Not a point")
    ```

- **Example 3: Patterns and classes** 
    ```python
    class Point:
        x: int
        y: int

        def location(point):
            match point:
                case Point(x=0, y=0):
                    print("Origin is the point's location.")
                case Point(x=0, y=y):
                    print(f"Y={y} and the point is on the y-axis.")
                case Point(x=x, y=0):
                    print(f"X={x} and the point is on the x-axis.")
                case Point():
                    print("The point is located somewhere else on the plane.")
                case _:
                    print("Not a point")
    ```

- **Example 4: Guard**
We can add an if clause to a pattern, called a guard. If the guard is false, match moves on to try the next case block. Note that the value capture takes place before the guard is evaluated:
    ```python
    match point:
        case Point(x, y) if x == y:
            print(f"The point is located on the diagonal Y=X at {x}.")
        case Point(x, y):
            print(f"Point is not on the diagonal.")
    ```
- **Example 5: Nested Patterns**
Patterns can be nested in arbitrary ways. For example, if our data is a short list of points, they could be matched in the following way:
    ```python
    match points:
        case []:
            print("No points in the list.")
        case [Point(0, 0)]:
            print("The origin is the only point in the list.")
        case [Point(x, y)]:
            print(f"A single point {x}, {y} is in the list.")
        case [Point(0, y1), Point(0, y2)]:
            print(f"Two points on the Y axis at {y1}, {y2} are in the list.")
        case _:
            print("Something else is found in the list.")
    ```
If you want to see more examples and a full tutorial, check out [PEP 636](https://www.python.org/dev/peps/pep-0636/).

# Conclusion
Python 3.10 brings many new interesting features, but as it is an alpha version (not yet stable), it is still far from being fully tested and ready for production. So it is not recommended to start using it right away.