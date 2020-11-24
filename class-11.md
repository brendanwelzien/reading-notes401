# Pandas
- to import it is... `import pandas as pd`

## Object Creation
- creating a *Series* by passing a list of values, letting pandas create an integer index
    - example taken from pandas.pydata.org
```python
In [3]: s = pd.Series([1, 3, 5, np.nan, 6, 8])

In [4]: s
Out[4]: 
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
```
## Viewing Data

- how to view the top and bottom rows of the frame
`df.head()` and `df.tail()`
- display the index, columns
`df.index` and `df.columns`

- `DataFrame.to_numpy()` gives a NumPy representation of the underlying data
    - --> *NumPy* arrays have one dtype for the entire array, while pandas DataFrames have one dtype per column
    - `df.describe()` shows a quick summary of your data

Label | Usage
-----|------
getting (selection a column) | `df['A']`
selecting by position | `df.loc[]`
boolean indexing | `df[df[A] > 0]`





[<-- Back](README.md)