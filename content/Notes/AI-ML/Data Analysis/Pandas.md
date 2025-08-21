---
title: Pandas
draft: false
tags:
  - component
date: 21-Aug-2025
---
# References

# Introduction
Pandas is a powerful data manipulation library in Python, widely used for data analysis and data cleaning. It provides two primary data structures: Series and DataFrame. A Series is a one-dimensional array-like object, while a DataFrame is a two-dimensional, size-mutable, and potentially heterogeneous tabular data structure with labeled axes (rows and columns).
```python
# !pip install pandas
import micropip
await micropip.install('pandas')  

import pandas as pd
```
# Series
A Pandas Series is a one-dimensional array-like object that can hold any data type. It is similar to a column in a table.
```python
data=[1,2,3,4,5]
series=pd.Series(data)
print("Series \n",series)
print(type(series))
```
