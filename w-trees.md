# Trees
```python
class Node:
    def __init__(self, data):
    self.data = data
    self.right_child = None
    self.left_child = None
```
## Binary Trees
- each node has a maximum of *two* children
## Binary Search Trees
- same structure as binary tree, but left sub-tree are <= value of node and right sub-tree >= of node
```python
class Tree:
    def __init__(self):
        self.root_node = None
```
- operations for a BST in maintaining BST principles
    1. `insert`
    2. `remove`

**Finding minimum and maximum nodes**
- to find the node with *smallest value*, start traversal from root of tree and to the *left* and the opposite for the *maximum value*

**Minimum** O(h) (dependent on height of tree)
```python
def find_min(self):
 current = self.root_node
 while current.left_child:
    current = current.left_child
 return current
```
**Inserting** O(h)
```python
def insert(self, data):
    node = Node(data)
    if self.root_node is None:
        self.root_node = node
    else:
    current = self.root_node
    parent = None
    while True:
        parent = current
    # now we compare value to check whether it has left child node
    if node.data < current.data:
        current = current.left_child
        if current is None:
            parent.left_child = node
            return
    # now we compare value to check for greater value or equal
    else:
        current = current.right_child
        if current is None:
            parent.right_child = node
            return
```

**Deleting**
- our node class does not have a reference to a parent. Need a helper method to search for and return node with its parent node
```python
def get_node_with_parent(self, data):
    parent = None
    current = self.root_node
    if current is None:
        return (parent, None)
    while True:
        if current.data == data:
            return (parent, current)
        elif current.data > data:
            parent = current
            current = current.left_child
        else:
            parent = current
            current = current.right_child
    return (parent, current)
```

```python
 def remove(self, data):
    parent, node = self.get_node_with_parent(data)
    if parent is None and node is None:
        return False
    # Get children count
    children_count = 0
    if node.left_child and node.right_child:
        children_count = 2
    elif (node.left_child is None) and (node.right_child is None):
        children_count = 0
    else:
        children_count = 1
    
    if children_count == 0:
        if parent:
            if parent.right_child is node:
                parent.right_child = None
            else:
                parent.left_child = None
        else:
            self.root_node = None
    
    elif children_count == 1:
        next_node = None
        if node.left_child:
            next_node = node.left_child
        else:
            next_node = node.right_child
        if parent:
            if parent.left_child is node:
                parent.left_child = next_node
            else:
                parent.right_child = next_node
        else:
            self.root_node = next_node
    # for two children
    else:
        parent_of_leftmost_node = node
        leftmost_node = node.right_child
        while leftmost_node.left_child:
            parent_of_leftmost_node = leftmost_node
            leftmost_node = leftmost_node.left_child
    node.data = leftmost_node.data
```

## Tree Traversal
- can be done `depth-first` or `breadth-first`
### Depth-First Traversal
- recursive approach using `in-order`, `pre-order`, and `post-order`

**In-Order** (LEFT, PARENT, RIGHT)
```python
def inorder(self, root_node):
    current = root_node
    if current is None:
        return
    self.inorder(current.left_child)
    print(current.data)
    self.inorder(current.right_child)
```

**Pre-Order** (PARENT, LEFT, RIGHT)
```python
 def preorder(self, root_node):
    current = root_node
    if current is None:
        return
    print(current.data)
    self.preorder(current.left_child)
    self.preorder(current.right_child)
```

**Post-Order** (LEFT, RIGHT, PARENT)
```python
def postorder(self, root_node):
    current = root_node
    if current is None:
        return
    self.postorder(current.left_child)
    self.postorder(current.right_child)
    print(current.data)
```
### Breadth-First
- this type of traversal starts from the root of the tree and visits the node from one level of tree to another
- possible by queuing data structure
```python
from collections import deque
class Tree:
    def breadth_first(self):
        list_of_nodes = []
        traversal_queue = deque([self.root_node])
        # enqueue root node and keep a list of visited nodes, dequeue class is used to maintain a queue
        while len(traversal_queue) > 0:
        node = traversal_queue.popleft()
        list_of_nodes.append(node.data)
        if node.left_child:
            traversal_queue.append(node.left_child)

        if node.right_child:
            traversal_queue.append(node.right_child)
        return list_of_nodes
```
- the node at the front of queue is popped off and appended to *list_of_nodes*, the first if will enqueue the left child node of the node, same for right
