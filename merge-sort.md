```python
def merge_sort(arr):
  if len(arr) > 1:
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    merge_sort(left)
    merge_sort(right)
    i = 0 # left half
    j = 0 # right half
    k = 0 # whole arr iterator

    while i < len(left) and j < len(right):
      if left[i] <= right[j]:
        arr[k] = left[i]
        i += 1
      else:
        arr[k] = right[j]
        j += 1
      k += 1

    # remaining
    while i < len(left):
      arr[k] = left[i] # position of k index is at left index now
      k += 1
      i += 1

    while j < len(right):
      arr[k] = right[j]
      k += 1
      j += 1
  return arr

if __name__ == "__main__":
  arr = [7, 3, 14, 9, 10]
  merge_sort(arr)
  print(arr)
```