# Jupyter

JupyterLab is a web-based user interface for Project Jupyter

- enables you to work with documents like *Jupyter notebook*, text editors, terminals, etc.
- also handles data formats

# NumPy: Data analysis with Python
- commonly used Python data analysis package

## Lists of Lists for CSV Data
1. import csv library
2. open .csv file
3. pass in keyworf argument *delimiter=";"* to make sure records are split on semicolon char
4. call list type to get rows from file
5. assign the result to xxx

```python
import csv
with open('wineuality-red.csv', 'r',) as f:
    wines = list(csv.reader(f, delimiter=';'))

print(wines[:3])
[[xxx, xxx, xxx]]
```
## NumPy 2-Dimensional Arrays
- a 2-dimensional array is also known as a matrix, a way about thinking of a list in lists. A matrix has rows and columns
- in NumPy array, the number of *dimensions* is called the *rank* and each *dimension* is called an *axis*
    - the *rows are the first axis* and the *columns are the second axis*

## Creating a NumPy Array
- create a NumPy array by usng the `numpy.array` function
    1. import numpy package
    2. pass the list of lists in array function which converts it into the NumPy array
        a. exclude header row with list slicing
        b. specify keyword argument dtype to make sure each element is converted to a float.
```python
import csv
with open("winequality-red.csv", 'r') as f:
    wines = list(csv.reader(f, delimiter=";"))
import numpy as np
wines = np.array(wines[1:], dtype=np.float)
```
- you can check the number of rows and columns in data using the `.shape` method

## Using NumPy to read in files
- you can directly read csv files or other files into arrays
    this is done by using the `numpy.genfromtxt` function

```python
wines = np.genfromtxt("winequality-red.csv", delimiter=';', skip_header=1)
```
    - in this example...
        1. use the genfromtxt function to read in the .csv file
        2. specify keyword argument delimiter so fields are parsed
        3. specify keyword argument skip_header so header row is skipped

## Indexing NumPy Arrays
- use array indexing to select elements, groups, entire rows or columns etc.
    - numPy is zero indexed meaning the index of the first row is *0* and the index of the first column is *0*
    - select the element at *row 3 and column 4*
        a. `wines[row, column]`
        b. `wines[2,3]`

## Slicing NumPy Arrays
- if we want to select the first 3 items from the 4th column, we can do so by using a *:*
- the *:* indicates that we want to select all the elements from the starting index up to but not including the ending index (slice)
    - `wines[0:3, 3]` --> or `wines[:3, 3]`
    - --> this retrieves elements from beginning up to element 3
    - `wines[:, 3]` --> selects entire fourth column
    - `wines[3, :]` --> selects the entire fourth row

## Assigning Values to NumPy Arrays
- we can use indexing to assign values to certain elements in arrays
```python
wines[1,5] = 9
```

### 1-Dimensional NumPy Arrays
- known as a vector, this only needs a single index to retrieve an element. Each row and column in a 2-dimensional array is a 1-dimensional array
- if we slice wiens and retrieve only the third row, we get a  *1-dimensional array*

```python
third_wine = wines[3, :]
```
- we can then retrieve elements from the *third_wine* using a single index ... `third_wine[2]`
- `np.random.rand(3)` generates a random vector

### N-Dimensional NumPy Arrays
- when you have to deal with arrays that are greater than 3 dimensions make sure that you are accessing correctly... `earnings[1][0][1]` etc.

## NumPy Data Types
-  each NumPy array can store elements of a single data type
- you can find the data type of a NumPy array by accessing the `dtype` property

Important Data Types
a. float
b. int
c. string
d. object (Python object)

- to convert data types you can use the `numpy.ndarray.astype` method to convert an array to a different type
    - this copies the array and returns a new array with the specified data type
[<-- Back](README.md)