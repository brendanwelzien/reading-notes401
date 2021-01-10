# Hashing and Tables
- a hash table is a form of list where elements are accessed via keyword
**Hash Item**
```python
class HashItem:
    def __init__(self, key, value):
        self.key = key
        self.value = value
```
**Hash Table**
```python
class HashTable:
    def __init__(self):
        self.size = 256
        self.slots = [None for i in range(self.size)]
        self.count = 0

    def _hash(self, key):
    mult = 1
    hv = 0
    for ch in key:
        hv += mult * ord(ch)
        mult += 1
    return hv % self.size
```
