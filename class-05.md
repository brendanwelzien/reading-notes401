# Linked List
*What is a linked list?* 
- It is a sequence of Nodes that are connected to each other. It is defined by each node which references the next node in the link
    - There are two types of *linked list*... *Singly* and *Doubly*
Singly: refers to the # of references that a node has... So there is only one reference and the reference points to the `next` node
Doubly: refers to there being two references within the node. There is a reference to both the `next` and `previous` node
Node: Nodes are the individual items or links that live in the list. Each node contains data pertaining to the link.

Next: Each node contains a property called `next` and this contains the reference to the next node
Head: the head is reference type of type `node` to the first node in a linked list
Current: the `current` refers to the type of `node` that is currently being looked at... Used traditionally when traversing through a full linked list -- 

*Traversing*
- when traversing through a linked list, you are not able to use a `foreach` or a `for` loop and you need to depend on the `next` value in each node for guidance.
- The `next` property will lead you to the next node where you can extract data accordingly.
    - traverse by using a `while()` loop so we can check the next node is not a *null*... We can then avoid a *NullReferenceError*
    - the while loop will end eventually since the last node will get a null error

*BigO*
- In this case, for **time** it would be O(n), at its worst case the node we are looking for will be the very last
- In this case, for **space** it would be O(1), since there is no additional space being used than what is given

*Adding a Node*
- it is important to consider OOO(Order of Operations) since each link/node is properly assigned
Steps:
    1. set `current` equal to `head`. This guarantees us that we are starting from beginning
    2. Instantiate the new node that is being added through `add()`
    - `newNode.Next` is set to null, so we want to set to same location as `head` since we are starting there
    - printing nodes requires another loop and we then have `current` equaling the next node in the list

## Side Notes about Linked Lists
- memory maangement is the biggest difference between linked lists and arrays
    - linked lists use memory in non-linear ways compared to arrays... the memory is *scattered*
    - arrays are static data structures whereas linked lists are dynamic data structures
    
[<-- Back](README.md)