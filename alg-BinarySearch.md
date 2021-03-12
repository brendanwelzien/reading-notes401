```python
# cuts in half the array and sets low and high in a loop, then does the same process until the array is shortened until the value is found
def binary_search(input_array, value):
    low = 0
    high = len(input_array) - 1
    while (low<=high):
        mid = (low+high) / 2
        if (input_array[mid] == value):
            return mid
        elif (input_array[mid] < value):
            low = mid + 1
        else:
            high = mid - 1
    return -1

test_list = [1,3,9,11,15,19,29]
test_val1 = 25
```