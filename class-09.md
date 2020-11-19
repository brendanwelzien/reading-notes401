# Statistics in Python

- an *event* is some outcome of interest
    - the outcome of the event is found by stating the *sample space*
    - the action is called a *trial*
example
```python
import random
def coin_trial():
heads = 0
for i in range(100):
    if random.random() <= 0.5:
        heads +=1
    return heads
def simulate(n):
    trials = []
    for i in range(n):
        trials.append(coin_trial())
    return(sum(trials)/n)
simulate(10)
>>> 5.4
simulate(100)
>>> 4.83
simulate(1000)
>>> 5.055
simulate(1000000)
>>> 4.999781
# taken from dataquest.io
```
- the more trials performed, the *deviation* away from the average decreases

Normal Distribution
- symmetry and shape
- as you get farther from the mean (average) the frequency drops immensely
- *central limit theorem* & *three sigma rule*

*central limit theorem*
- if we make many estimates, the CLT says the distribution of these estimates will look like normal distribution (expected probabiblity over the more trials done)

*Three sigma rule*
- the 68-95.99.7 rule
- expression of how many of our observations fall within a distance of the mean
    - 68% observations will fall between on st dv. of mean.. 95% within two and 99.7% withiin three
- *z-score* is a calculation that answers the question--> *Given a data point, how many st. dv. is it away from the mean?*
`z = Xi - u / sigma`
- xi = data point in question
- u = mean
- sigma = standard deviation
    - the z-score references the z-table giving cumulative probability

## Enriching Python CLasses with Dunder (Magic, Special) Methods

What are Dunder methods?
- special methods are a set of predefined methods you can use to improve classes
    - recgonizable through double underscores... `__init__` or `__str__`
    - these are often called *special methods*

example of a python class with dunder methods taken from dbader.org
```python
from functools import total_ordering


@total_ordering
class Account:
    'A simple account class'

    def __init__(self, owner, amount=0):
        'This is the constructor that lets us create objects from this class'
        self.owner = owner
        self.amount = amount
        self._transactions = []

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(self.owner,
                                                               self.amount)

    def add_transaction(self, amount):
        if not isinstance(amount, int):
            raise ValueError('please use int for amount')
        self._transactions.append(amount)

    @property
    def balance(self):
        return self.amount + sum(self._transactions)

    def __len__(self):
        return len(self._transactions)

    def __getitem__(self, position):
        return self._transactions[position]

    def __reversed__(self):
        return self[::-1]

    def __eq__(self, other):
        return self.balance == other.balance

    def __lt__(self, other):
        return self.balance < other.balance

    def __add__(self, other):
        owner = '{}&{}'.format(self.owner, other.owner)
        start_amount = self.amount + other.amount
        acc = Account(owner, start_amount)
        for t in list(self) + list(other):
            acc.add_transaction(t)
        return acc

    def __call__(self):
        print('Start amount: {}'.format(self.amount))
        print('Transactions: ')
        for transaction in self:
            print(transaction)
        print('\nBalance: {}'.format(self.balance))

    def __enter__(self):
        print('ENTER WITH: making backup of transactions for rollback')
        self._copy_transactions = list(self._transactions)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('EXIT WITH:', end=' ')
        if exc_type:
            self._transactions = self._copy_transactions
            print('rolling back to previous transactions')
            print('transaction resulted in {} ({})'.format(exc_type.__name__, exc_val))  # noqa E501
        else:
            print('transaction ok')


if __name__ == '__main__':
    acc = Account('bob', 10)
    acc.add_transaction(20)
    acc.add_transaction(-10)
    acc.add_transaction(50)
    acc.add_transaction(-20)
    acc.add_transaction(30)
    assert acc.balance == 80
    assert list(reversed(acc)) == [30, -20, 50, -10, 20]
```
- when you start a class, you need a special method to construct objects from the class... this is the `def __init__` dunder
    - self.xxx = xxx

Object representation: str and repr
- common to provide a string representation of your object for consumer of your class
    1. __repr__: the official string representation of an object. This is how you would make an object of the class
    2. __str__: the informal or nicely printable string representation of an object


[<-- Back](README.md)