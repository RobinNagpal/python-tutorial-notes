### Range Function
- The range() function is used to generate a sequence of numbers.
e.g. `range(5)` generates a sequence of numbers from 0 to 4. 
- loop with range() function:
```
for i in range(5):
    print(i)
```

- list(range(5)) returns `[0, 1, 2, 3, 4]`
- list(range(5, 10)) returns `[5, 6, 7, 8, 9]`

### else Clauses on Loops
- Loop statements may have an else clause; it is executed when the loop terminates through exhaustion of the 
iterable (`with` `for`) or when the condition becomes false (with while), but not when the loop is terminated by a 
break statement.
- e.g. for loop with else clause:
```
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n//x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')
```
- e.g. while loop with else clause:
```
while n > 0:
    n = n - 1
    if n == 2:
        break
else:
    print('Loop ended normally')
```

### match Statements
- The match statement is used to compare a value against a set of possible patterns.
- e.g. match statement:
```
match n:
    case 0:
        print('n is zero')
    case 1:
        print('n is one')
    case _:
        print('n is neither zero nor one')
```

```
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

def where_is(point):
    match point:
        case Point(x=0, y=0):
            print("Origin")
        case Point(x=0, y=y):
            print(f"Y={y}")
        case Point(x=x, y=0):
            print(f"X={x}")
        case Point():
            print("Somewhere else")
        case _:
            print("Not a point")
```
- we can add if conditions to the match statement:
```
match point:
    case Point(x, y) if x == y:
        print(f"Y=X at {x}")
    case Point(x, y):
        print(f"Not on the diagonal")
```

### Defining Functions
- The keyword `def` introduces a function definition. It must be followed by the function name and the parenthesized
list of formal parameters. The statements that form the body of the function start at the next line, and must be indented.
- The first statement of the function body can optionally be a string literal; this string literal is the function’s 
documentation string, or docstring

#### Symbol Table
- The execution of a function introduces a new symbol table used for the local variables of the function. 
- More precisely, all variable assignments in a function store the value in the local symbol table; whereas variable
references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the
global symbol table, and finally in the table of built-in names.
- Thus, global variables cannot be directly assigned a value within a function (unless named in a global statement),
although they may be referenced.
- The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function
when it is called; thus, arguments are passed using call by value (where the value is always an object reference, not the
value of the object).

#### Return Statement
- In fact, even functions without a return statement do return a value: `None`.

#### Default Argument Values
e.g. function with default argument values:
```
def ask_ok(prompt, retries=4, reminder='Please try again!'):
    while True:
        ok = input(prompt)
        if ok in ('y', 'ye', 'yes'):
            return True
        if ok in ('n', 'no', 'nop', 'nope'):
            return False
        retries = retries - 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)
```

#### Keyword Arguments
- Functions can also be called using keyword arguments of the form `kwarg=value`.
- e.g. function with keyword arguments:
```
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")
```

```python
parrot(1000)                                          # 1 positional argument
parrot(voltage=1000)                                  # 1 keyword argument
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword
```
- When a final formal parameter of the form **name is present, it receives a dictionary (see Mapping Types — dict) 
containing all keyword arguments except for those corresponding to a formal parameter. 
```python
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])
```

#### Positional-or-Keyword only Arguments
- If / and * are not present in the function definition, arguments may be passed to a function by position or by keyword.
- e.g. function with positional-or-keyword arguments:
```
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```

#### Arbitrary Argument Lists
- A function can be called with an arbitrary number of arguments. These arguments will be wrapped up in a tuple 
(see Tuples and Sequences). 
- e.g. function with arbitrary argument lists:
```
def write_multiple_items(file, separator, *args):
    file.write(separator.join(args))
```

#### Unpacking Argument Lists
```python
def parrot(voltage, state='a stiff', action='voom'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.", end=' ')
    print("E's", state, "!")

d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
parrot(**d)
```


#### Lambda Expressions
```python
def make_incrementor(n):
    return lambda x: x + n

f = make_incrementor(42)
f(0)

f(1)
```

#### Documentation Strings
- If there are more lines in the documentation string, the second line should be blank, visually separating the summary 
from the rest of the description. The following lines should be one or more paragraphs describing the object’s calling 
conventions, its side effects, etc.

```python
def my_function():
    """Do nothing, but document it.

    No, really, it doesn't do anything.
    """
    pass
```

#### Function Annotations
- Function annotations are completely optional metadata information about the types used by user-defined functions
- e.g. function with annotations:
```python
def f(ham: str, eggs: str = 'eggs') -> str:
    print("Annotations:", f.__annotations__)
    print("Arguments:", ham, eggs)
    return ham + ' and ' + eggs

f('spam')

# Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
#     Arguments: spam eggs
# 'spam and eggs'

```
