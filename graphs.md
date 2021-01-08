# Graphs Data Structure
- a graph is a non-linear data structure that can be seen as a collection of *vertices* or *nodes* by line segments named **edges**
1. Vertex = called a node, is a data object that can have zero or more adjacent vertices
2. Edge = an edge is a connection between two nodes
3. Neighbor = the neighbors of a node are its adjacent nodes... are connceted via an edge
4. Degree = degree of a vertex is number of edges connected to that vertex

## Directed vs. Undirected
- an `undirected graph` is a graph where each edge is undirected or bi-directional
    - there are no directions fiven to point to specific vertices
- a `directed graph` also called a *Digraph* is graph where every edge is directed
    - each node is directed at another node with a requirement of what should be referenced next

## Complete vs. Connected vs. Disconnected
- a `complete` graph is when all nodes are connected to all other nodes
- a `connected` graph is when all the *vertices*/*nodes* have at least one edge
- a `disconnected` graph is where some vertices may not have edges (stand-alone/islands)

## Acyclic vs Cyclic
- a `acyclic` graph is a **directed** graph WITHOUT cycles
    - a cycle is when a node can end up back at itself
    - this also known as a **tree**
- a `cyclic` graph is one that has cycles
    - a cycle is defined as a path of a positive length that starts and ends at same vertex

## Graph Representation
Graphs are represented through:
1. Adjacency Matrix
2. Adjacency List

**Adjacency Matrix**
- represented through a 2-D array, if there are n vertices, then we look at `n x n` Boolean matrix
- each row and column represents each vertex of DS
    - the elements of both column and row must add up to `1` if there is an edge that connected the two, or `0` if there is not a connection
    - a *sparse* graph is one with few connections where a *dense* graph is one with many connections
    - in a adjacency matrix, an undirected graph will always be symmetric, this is not the case for a directed graph
![am](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/AdjMatrix.PNG)
**Adjacency List**
- most common way to represent graphs
- it is a collectoin of linked lsits or array that lists all other vertices that are connected
![al](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/AdjList.PNG)

## Weighted Graphs
- a weighted graph is a graph with numbers assigned to its edges... These numbers are called weights
![weighted](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/weightGraph.PNG)
- with adjacency *lists*, you must include both the weight and the name of the adjacent vertex
![alweighted](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/weightList.PNG)

## Traversals
- traversals are like when you would traverse a tree

**Breadth First**, all nodes need to be connected
- starting at a specific vertex/node, and must be specified when calling the `BreadthFirst()` method
- to prevent behavior of an endless loop with a cycle graph we need to *flag* it, like setting it from *false* to *true*
- breadth-first is when you *visit all nodes that are closest to the root*, then traverse outwards

*Algorithm for Breadth First*
1. Enqueue the declared start node into queue
2. Create a loop that will run while the node still has nodes present
3. Dequeue the first node from the queue
4. If the Dequeue'd node has unvisited child nodes, mark the unvisited children as visited and re-insert them back into the queue

![breadthfirst](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/BreadthFirst.PNG)
- visual shows levels of which nodes will be added to the queue... The nodes that are one away = C, E, B
- two nodes away = F, G, D
```python
ALGORITHM BreadthFirst(vertex)
    DECLARE nodes <-- new List()
    DECLARE breadth <-- new Queue()
    breadth.Enqueue(vertex)

    while (breadth is not empty)
        DECLARE front <-- breadth.Dequeue()
        nodes.Add(front)

        for each child in front.Children
            if(child is not visited)
                child.Visited <-- true
                breadth.Enqueue(child)   

    return nodes;
```
- breakdown copied from CodeFellows.github.io -->

1. We have declared that our starting node (or root) is going to be Node A.
2. The first thing we want to do is Enqueue the root
3. Next, we enter a while loop. We want this loop to keep running until there are no more nodes in our queue.
4. Once we are in the while loop, we want to Dequeue the front node and then check to see if it has any children.
5. If there are children of the node we are currently looking at, we want to mark each one as “visited”. By marking each child node as visited, this will help us know that we have already seen that node before, and won’t accidently push us into an infinite loop if the graph was cyclic. In addition to marking each child node as visited, we want to place any of its children that have not yet been visited into the queue.
6. The process will complete until the queue is empty.
7. Once the while loop breaks, we can then return the order list. This order list will contain, in order, of all the nodes that we traversed too.

A few things to note about breadth-first traversals:

1. If there are any disconnected nodes (such as islands) with the graph data structure, they will not be traversed.
2. Breadth-first only outputs the nodes that are connected in some relation to the root that you pass in.

**Depth First**

**Algorithm**
1. `Push` the root node into the stack
2. Start a while loop while the stack is not empty
3. `Peek` at the top node in the stack
4. If the top node has unvisited children, mark the top node as visited, and then `push` any unvisited children back into the stack
5. If the top node does not have any unvisited children, `pop` that node off the stack
6. Repeat until the stack is empty
![depthtraversal](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/assets/Depth1.PNG)

1. Look at node `A`'s children (B and D), since B is first and has not yet been visited, it gets `pushed` into the stack
2. Before looking at the rest of `Node A`'s children, we continue going through `Node B` and visit those children
3. `Node C` gets `pushed` into stack
4. `Node G` is up, but now we must go backwards and `pop` off until we visit a child node (Node D) that has not yet been visited, think of snaking in a draft
5. After complete traversal, `Node A` gets popped off

## World Use of Graphs
1. GPS and Mapping
2. Driving Directions
3. Social Networks
4. Airline Traffic
5. Netflix uses graphs for suggestions of products

