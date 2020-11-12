# Classes and Objects
- objects are a container of variables and functions into a single entity
    - they get their variables and functions from classes... 
        - classes are basically a *template* to create objects
```python
class myClass:
    variable = "blah"

    def function(self):
        print("This is a message inside class")

myObject = myClass()

myObject.variable
```
- the object now holds an object of the myClass that contains the info nested within the class
- to access the variables inside the object you need to use in this case `myObject.variable`
    - you would then do something like . . . `print(myObject.variable)`

# Thinking Recursively in Python
To think recursively is to break down big problems into smaller chunks. This allows us to tackle big problems in smaller more attainable bits.

- a recursive function is a function where it will continue to call on itself until some condition is met to *return* a result
    - to maintain execution we must...
    1. Thread the state through each recursive call so the current state is part of current execution context or
    2. keep the state in a global scope

*Fixtures*
- when you write tests, you rarely will write only one or two
    - instead you will write a *test suite* which checks different paths of your code


[<-- Back](README.md)