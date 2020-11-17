# List Comprehensions in Python
- list comprehensions provide a way to create lists
    - this consists of brackets containing an expression followed by a *for clause* the 0+ *for* or *if* clauses
    - the result will be a new list resulting from evaluating the expression...
    ```python
    new_list = [expression(i) for i in old_list if filter(i)]
    ```
*Syntax*
```python
[ expression for item in list if conditional ]
```
- this is the equivalent for
```python
for item in list:
    if conditional:
    expression
```
- examples

```python
x = [i for i in range(10)]
print x
[0,1,2...]
```


[<-- Back](README.md)