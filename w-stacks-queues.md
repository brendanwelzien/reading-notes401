# Stacks
- stack is LIFO (stack of plates)
    - uses `push` and `pop` and `peek`
**Node**
```python
class Node:
 def __init__(self, data=None):
    self.data = data
    self.next = None
```

**Stack**
```python
class Stack:
 def __init__(self):
    self.top = None
    self.size = 0
```

**Push**
```python
 def push(self, data):
 node = Node(data)
    if self.top:
        node.next = self.top
        self.top = node
    else:
        self.top = node
        self.size += 1
```
**Pop**
```python
def pop(self):
 if self.top:
    data = self.top.data
    self.size -= 1
    if self.top.next:
        self.top = self.top.next
    else:
        self.top = None
    return data
 else:
    return None
```
**Peek**
```python
def peek(self):
 if self.top
    return self.top.data
 else:
    return None
```

**Bracket-Matching Application**
```python
def check_brackets(statement):
 stack = Stack()
    for ch in statement:
        if ch in ('{', '[', '('):
            stack.push(ch)
        if ch in ('}', ']', ')'):
            last = stack.pop()
        if last is '{' and ch is '}':
            continue
        elif last is '[' and ch is ']':
            continue
        elif last is '(' and ch is ')':
            continue
        else:
            return False
 if stack.size > 0:
    return False
 else:
    return True
```

# Queues
- first in first out (FIFO) (standing in line first, first to be served)
    - uses `enqueue`, `dequeue`, and `Size()`
## List-Based Queue
```python
class ListQueue:
 def __init__(self):
 self.items = []
 self.size = 0
```
- initialize empty list
**Enqueue**
- uses `insert` method of `list` class to insert items at **front** of list
```python
def enqueue(self, data):
 self.items.insert(0, data)
 self.size += 1
```
**Dequeue**
- removes item from queue, uses `pop()` method
```python
def dequeue(self):
 data = self.items.pop()
 self.size -= 1
 return data
```
## Stack-Based Queue
```python
class Queue:
 def __init__(self):
 self.inbound_stack = []
 self.outbound_stack = []
```
- the inbound stack is used to store elements added to the queue, nothing else

**Enqueue**
```python
def enqueue(self, data):
 self.inbound_stack.append(data)
```
**Dequeue**
- elements deleted from queue only through outbound stack
```python
if not self.outbound_stack:
 while self.inbound_stack:
    self.outbound_stack.append(self.inbound_stack.pop())
return self.outbound_stack.pop()
```
## Node-Based Queue
- can be implemented using doubly-linked list, insertion, and deletion operations
```python
class Queue:
def __init__(self):
 self.head = None
 self.tail = None
 self.count = 0
```
**Enqueue**
```python
 def enqueue(self, data):
    new_node = Node(data, None, None)
    if self.head is None:
        self.head = new_node
        self.tail = self.head
    else:
        new_node.prev = self.tail
        self.tail.next = new_node
        self.tail = new_node
 self.count += 1
```
**Dequeue** (removes node at front of queue)
```python
def dequeue(self):
    current = self.head
    if self.count == 1:
        self.count -= 1
        self.head = None
        self.tail = None
    elif self.count > 1:
        self.head = self.head.next
        self.head.prev = None
        self.count -= 1
```

