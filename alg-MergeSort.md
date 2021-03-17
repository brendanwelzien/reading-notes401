- time: O(n log n) (#number of processes * #number of sorts per process), space: O(n)
- break down the array into sorted parts (divide and conquer) and then bring back together in similar method of bubble sort

```python
def mergeSort(arr):
    if len(arr) > 1:
 
         # Find middle of array
        mid = len(arr)//2
 
        # Divide the array
        L = arr[:mid]
        R = arr[mid:]
 
        # Sort left side
        mergeSort(L)
        # Sort right side
        mergeSort(R)
 
        i = j = k = 0
 
        # Copy data to temporary arrays L[] and R[]
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1
 
        # Checking if any element was left
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1
 
        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
 
def printList(arr):
    for i in range(len(arr)):
        print(arr[i])
    print()
 
 
# Driver Code
if __name__ == '__main__':
    arr = [12, 11, 13, 5, 6, 7]
    print("Given array is", end="\n")
    printList(arr)
    mergeSort(arr)
    print("Sorted array is: ", end="\n")
    printList(arr)
```

