# Python Scope and LEGB Rule: Resolving Names in your Code
- the concept of *scope* rules how variables and names are identified in code... It determines visibility of a variable in the code

The Python scope concept is presented using a rule known as **LEGB rule**

## Understanding Scope
- in programming, the *scope* of a name defines area of a program where you can ambiguously access its information
1. *Global Scope*: names that you define in this scope are available everywhere
2. *Local Scope*: Names that you define in this scope are only available or visible to code within the scope

- Python avoids some common scoping issues by creating *programs*
    - when you can access value of a given name from someplace, you will say that the name is *in scope*, if you cannot access the name, then you will say the name is *out of scope*
*KEY NOTES*
`"Since Python is a dynamically-typed language, variables in Python come into existence when you first assign them a value. On the other hand, functions and classes are available after you define them using def or class, respectively. Finally, modules exist after you import them. As a summary, you can create Python names through one of the following operations:"`
----- | ------
Operation | Statement
Assignments | x = value
Import Operations | import module or from module import name
Function Definitions | def my_func():...
Argument definitions in context of fcns | def my_func(arg1, arg2..)
Class definitions | class MyClass

- *All of these operAtions create or update new Pytghon names because they all assign a anem to a variable, constant, function, class instance, module or other Python object

# Python Scope vs Namespace
- a python scope determines where in your program a name is visible. Python scopes are implemented as **dictionaries** that map names to objects... These dictionaries are commonly called **namespaces**
    - they are stored concretely as **.__dict__.**
```python
import sys
sys.__dict__.keys()
# dict_keys(['__name__, __doc__, __package__... arg, ps1, ps2'])
```
- after you import *sys*, you can use.keys() to inspect the keys of sys.__dict__.
    - this returns a list with all the names defined at the top ldevel of the module

**Example of Usage**
- suppose you need to use the name ps1, which is defined in *sys*. if you know how .__dict__ and namespaces work in Python, then you can reference ps1 in minimum two different ways...
    1. using the dot notation on the module's name in form module.name
    2. using a subscription operation on .__dict__ in the form module.__dict__['name']
    ```python
    sys.ps1
    # or
    sys.__dict__['ps1']
    ```
- whenever you use a name, Python searches through different scope levels or namespaces to determine whether the name exists

## Using the LEGB Rule for Python Scope
- Python resolves names using **LEGB Rule**, which is named after Python scope for names... The letters stand for *Local, Enclosing, Global, and Built-In*
    - Local (or function) scope: code block or body of any Python function or lambda expression... This Python scope contains names that you define inside function.. it is created at **function call**, *not* at **function definition**
    - Enclosing (or nonlocal scope): special scope that only exists for nested function, then the enclosing scope is the scope of the outer or enclosing function. The names in the enclosing scope are visible from the code of the inner and enclosing functions
    - Global (or module) scope: the top-most scope in Python program, script, or module. This Python scope contains all names that you define at top level of a program or a module. Names in this Python scope are visible from everywhere in your code
    - Built-in Scope: special Python scope that is created or loaded whenever you run a script or open interactive sesh. This scope contains names usuch as keywords, functions, exceptions, and other attributes that are built into Python. Names in this Python scope are also available from everywhere in your code. This is because it is *automatically* loaded by Python when you *run a program or script*

# Functions: The Local Scope
- the **local scope** or function scope is a Python scope created at function calls... Every time you call a function, you are *also creating a new local scope*
    - by default, parameters and names that you assign inside a function exist *only* within the function or local scope associated with the function call
    - when *the function returns*, the *local scope* is destroyed and the *names are forgotten*
- EXAMPLE taken from *realpython.com* -->
```python
>>> def square(base):
...     result = base ** 2
...     print(f'The square of {base} is: {result}')
...
>>> square(10)
The square of 10 is: 100
>>> result  # Isn't accessible from outside square()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    result
NameError: name 'result' is not defined
>>> base  # Isn't accessible from outside square()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    base
NameError: name 'base' is not defined
>>> square(20)
The square of 20 is: 400
```

## Nested Functions: The Enclosing (nonlocal) Scope (KEY)
- the Enclosing or nonlcoal scope is observed when you nest functions inside other functions
- it takes the form of the local scope of any enclosing function's local scope. Names that you define in python enclosing scope are known as **nonlocal names**
- EXAMPLE taken from *realpython.com* -->
```python
>>> def outer_func():
...     # This block is the Local scope of outer_func()
...     var = 100  # A nonlocal var
...     # It's also the enclosing scope of inner_func()
...     def inner_func():
...         # This block is the Local scope of inner_func()
...         print(f"Printing var from inner_func(): {var}")
...
...     inner_func()
...     print(f"Printing var from outer_func(): {var}")
...
>>> outer_func()
Printing var from inner_func(): 100
Printing var from outer_func(): 100
>>> inner_func()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'inner_func' is not defined
```
- there is a NameError bc the last statement of inner_func tries to access *another_var*, at this point *another_var* is not defined yet

## Modules: The Global Scope (KEY)
- from the moment you start a Python program, you are in the *global scope*... Internally Python turns your program main script into a module called **__main__** to maintain execution... The namespace of this module is the *main global scope* of the program
*note* - global scope and global names are closely assocaited with the module files... If you define a name at the top level of any Python module, then that name is considered global to the module, hence *module scope*

- when you run a program, the module or script is loadeed with the special name *__main__*
    - to inspect names within your global scope, you can use *dir()*
    - if you call *dir()* with no arguments, you get the list of names available
    - there is only *one global python scope* per program execution--> exists until program terminates and all names are forgotten
```python
var = 90
def func():
    return var      <-- `you can access var from inside func()`

func()
90
var  <-- `remains unchanged
90
```
- inside func(), you can access freely or reference the value of var, but you cannot assign global names inside functions unless you explicitly declare them as global names using a *global statement*

- **when you assign a value to a name, one of two things can happen**
    1. you *create** a new name
    2. you **update** an existing name

### Ways to modify content of global and nonlocal names
1. **global**
2. **nonlocal**

### The Global Statement
- when you try to assign a value to a global name inside a func, you create a new local name in the func scope... to *modify* use the *global statement*
    - you can define a list of names that will be treated as global names
    - do this by using the *global* keyword followed by 1+ names separated by commas

```python
>>> counter = 0  # A global name
>>> def update_counter():
...     global counter  # Declare counter as global
...     counter = counter + 1  # Successfully update the counter
...
>>> update_counter()
>>> counter
1
>>> update_counter()
>>> counter
2
>>> update_counter()
>>> counter
3
```

### The nonlocal Statement
- nonlocal names can be accessed from inner functions, but not assigned or updated like global
    - if you want to *modify*, you need to use a **nonlocal statement**
- the *nonlocal statement* consists of nonlocal keyword followed by 1+ names separated by commas
```python
>>> def func():
...     var = 100  # A nonlocal variable
...     def nested():
...         nonlocal var  # Declare var as nonlocal
...         var += 100
...
...     nested()
...     print(var)
...
>>> func()
200
```
- with the nonlocal var, you are telling Python that you are modifying var inside nested() and then increment it which is reflected in the nonlocal name var which now has a value of 200
- unlike global, you *cannot* use *nonlocal* outside of nested function






[<-- Back](README.md)