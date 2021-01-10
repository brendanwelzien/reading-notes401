# Python Advanced Methods
- using an account class for this guide

## Object Initialization: `__init__`
```python
class Account:
    "" simple account for class""
    def __init__(self, owner, amount=0):
    ""constructor allows use to create objects from this class""
        self.owner = owner
        self.amount = amount
        self._transactions = []
acc = Account('brendan')
```
## Object Representation `__str__`, `__repr__`
1. `__repr__`: official string representation of an object, this is how you would make object of a class
2. `__str__`: the "informal" or nicely printable string representation of object
```python
class Account:
#...
    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)
```
## Iteration: `__len__`, `__getItem__`, `__reversed__`
- to iterate over account object, we need to add some transactions
```python
def add_transaction(self, amount):
    if not isinstance(amount, int):
        raise ValueError('please use int for amount')
    self._transactions.append(amount)
@property
def balance(self):
    return self.amount + sum(self._transactions)
```
- if we want to know questions like how many transactions were there, transaction number, and looping we need to use magic methods
```python
class Account:
    # ... (see above)

    def __len__(self):
        return len(self._transactions)

    def __getitem__(self, position):
        return self._transactions[position]
```
- use `@totalordering` from doing `from functools import total_ordering` to access eq and lt (equal and less than)
- the `__add__` method merges attributes together
```python
def __add__(self, other):
    owner = self.owner + other.owner
    start_amount = self.balance + other.balance
    return Account(owner, start_amount)
```
# Generators
- uses `yield` statement instead of `return` and utilizes `__iter__()` and `__next__()`
