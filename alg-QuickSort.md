- time: average/best case = O(n log n), worst case = O(n^2), space: O(1) since we are only moving in place
- in most cases, quicksort is one of the *most* efficient sorting methods
- pick one of the values, known as the **pivot**: move everything that is larger than it on the right side and everything that is smaller on the left side
- do so recursively by picking a pivot for the upper and lower section of the array and sort them similarly
- quicksort may also usually be On^2 especially with the larger sets of data we are analyzing

```python
# divide the fcn
def partition(arr,low,high):
   i = (low - 1)
   pivot = arr[high] # pivot element
   for j in range(low , high):
      # If current element is smaller
      if arr[j] <= pivot:
         # increment
         i = i+1
         arr[i],arr[j] = arr[j],arr[i]
   arr[i+1],arr[high] = arr[high],arr[i+1]
   return (i+1)
# sort
def quickSort(arr,low,high):
   if low < high:
      # index
      part = partition(arr,low,high)
      # sort the partitions
      quickSort(arr, low, part-1)
      quickSort(arr, part+1, high)
arr = [2,13,6,8,4,5,9,3]
n = len(arr)
quickSort(arr,0,n-1)
print ("Sorted array is")
for i in range(n):
   print (arr[i],end=" ")
```