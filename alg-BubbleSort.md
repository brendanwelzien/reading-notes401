- time : worst case: O(n^2), best case: O(n) (for smaller arrays)
- space: O(1)
- bubble sort takes the first two indexes (`x[0]` and `x[1]`) and compares the values, if one is larger then it switches. Then you move onto the next two (`x[1]` and `x[2]`). Repeat and go through array x amount of times until all values are sorted
```python
def bubbleSort(arr): 
    n = len(arr) 
  
    # Traverse through all elements in array
    for i in range(n-1): 
    # range(n) also work but outer loop will repeat one time more than it is needed. 
  
        # Last i elements are already in place 
        for j in range(0, n-i-1): 
  
            # traverse the array from 0 to n-i-1 
            # Swap if the element found is greater 
            # than the next element 
            if arr[j] > arr[j+1] : 
                arr[j], arr[j+1] = arr[j+1], arr[j] 
  
# Driver code to test above 
arr = [64, 34, 25, 12, 22, 11, 90] 
  
bubbleSort(arr)
```