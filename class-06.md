# Readings for Game of Greed

## How to use the Random Module
*What is it ?* --> The random module provides access to functions that support various operations... Most importantly, it allows you to generate random numbers

*When to use it?* --> When we want a computer to pick a random number in a given range... from a list.. a card from a deck.. a coin or dice, etc.

*Random Functions*
- if want a random integer, we can use the *Randint* function.. it takes **two parameters** --> *lowest and highest number*
```python
import random
print random.randint(0, 5)
# the output with be anywhere from 1-5

# for larger numbers...
import random
random.random() * 100
```

*Choice Function*
- generate a ranodom value from the sequence sequence
    - random.choice( ['red', 'black', 'green'])
    - the choice function can be used for choosing a random element from a list
```python
import random
mylist = [1, 30, False, 40, "Beef"]
random.choice(mylist)
```

*Shuffle Function*
- the shuffle function shuffles elements in list in place, so they are in a random order
    - random.shuffle(list)
```python
from random import shuffle
x = [[i] for i in range(10)]
shuffle (x)
#Output:
# print x gives [[9], [2], [7], ....]
```

*Randrange*
- generate a randomly selected element from range(start, stop, step)
```python
random.randrange(start, stop[, step])
import random
for i in range(3):
    print random.randrange(0, 101, 5)
```

- example taken from @pythonforbeginners.com
```python
import random
import itertools

outcomes = { 'heads':0,
             'tails':0,
             }
sides = outcomes.keys()

for i in range(10000):
    outcomes[ random.choice(sides) ] += 1

print 'Heads:', outcomes['heads']
print 'Tails:', outcomes['tails']
```
```python
#$ python random_choice.py

#Heads: 4984
#Tails: 5016
```
## Risk Analysis in Software Testing and Performance
- the probability of unwanted incidents are known as *risks*
    - in software testing, risk analysis is the process of identifying the risks in apps or software and prioritizing them to test
    - after this, the process of assigning the level of risk is done
*Why use risk analysis?*
- using it highlights the potential problem areas and helps mitigate the risk moving forward
    - people create test plans based off various factors such as...
    1. Use of new hardware
    2. Use of new technology
    3. Use of a new automation tool
    4. Sequence of code
    5. Availability of test resources for app

- This helps assess the risk magnitude factors as labeled from low to high

*Risk Identification*
- there are several sets of risks included in this process
1. Business Risks: most common risk and may come from company or customer, not the project
2. Testing Risks: you should be wel acquainted with the platform you are working on alongside the testing tools
3. Premature Release Risk: A fair amount of knowledge to analyze the risk associated with releasing unsatisfactory or untested software is required
4. Softwware Risks: You should be well versed with risks associated with the software development process

*Risk Assessment*
1. Early forecast of unwanted situation in project
2. Estimating potential loss of such a situation
3. Making decision to deal with such a situation
4. Avoid future consequences
    - perspectives to consider through this process:
        - *Effect*, *Cause*, *Likelihood*

*How to perform Risk Analysis*
- three steps
1. Searching the Risk
2. Analyzing the impact of each individual risk
3. Measures for the risk identified



## Dependency Injection
- what is it and how to use it?
- *dependency injection* is a technique whereby one object or static method supplies dependencies of another object
- "When class A uses some funcitonality of class B, then its said that class A has a dependency of class B"
    - *transferring the task of creating the object to someone else and directly using the dependency is called dependency injection*

**3 types of dependency injectiom**
1. constructor injection: dependencies are provided through a class constructor
2. setter injection: the client exposes a setter method that the injector uses to inject the dependency
3. interface injection: dependency provides an injector method that will inject the dependency into any client passed to it. Clients need to implement an interface that exposes a *setter* method that *accepts* the dependency

    **Dependency injection's responsbilities:**
    1. create the objects
    2. know which classes require those objects
    3. provide them all those objects
[<-- Back](README.md)