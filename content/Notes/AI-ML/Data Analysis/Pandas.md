---
title: Pandas
draft: true
tags:
  - component
date: 21-Aug-2025
---
# References

# Introduction
Pandas is a powerful data manipulation library in Python, widely used for data analysis and data cleaning. It provides two primary data structures: Series and DataFrame. A Series is a one-dimensional array-like object, while a DataFrame is a two-dimensional, size-mutable, and potentially heterogeneous tabular data structure with labeled axes (rows and columns).
```python
!pip install pandas

import pandas as pd
```
# Series
A Pandas Series is a one-dimensional array-like object that can hold any data type. It is similar to a column in a table.
```python
data=[1,2,3,4,5]
series=pd.Series(data)
print("Series \n",series)
# - Series
# 0 1
# 1 2
# 2 3
# 3 4
# 4 5
# dtype: int64
print(type(series)) # <class 'pandas.core.series.Series'>

## Create a Series from dictionary
data={'a':1,'b':2,'c':3}
series_dict=pd.Series(data)
print(series_dict)
# a 1
# b 2
# c 3
# dtype: int64

data=[10,20,30]
index=['a','b','c']
pd.Series(data,index=index)
# a 1
# b 2
# c 3
# dtype: int64
```
# Dataframe
```python
## reading data from csv files
# df=pd.read_csv('sales_data.csv')

## create a Dataframe from a dictionary oof list
data={
	'Name':['Krish','John','Jack'],
	'Age':[25,30,45],
	'City':['Bangalore','New York','Florida']
}

df=pd.DataFrame(data)
print(df)
print(type(df))
# Name Age City
# 0 Krish 25 Bangalore
# 1 John 30 New York
# 2 Jack 45 Florida
# <class 'pandas.core.frame.DataFrame'>

## Create a Data frame From a List of Dictionaries
data=[
	{'Name':'Krish','Age':32,'City':'Bangalore'},
	{'Name':'John','Age':34,'City':'Bangalore'},
	{'Name':'Bappy','Age':32,'City':'Bangalore'},
	{'Name':'JAck','Age':32,'City':'Bangalore'}
]

df=pd.DataFrame(data)
print(df)
print(type(df))
# Name Age City
# 0 Krish 32 Bangalore
# 1 John 34 Bangalore
# 2 Bappy 32 Bangalore
# 3 JAck 32 Bangalore
# <class 'pandas.core.frame.DataFrame'>

print(df.head(2))
# Name Age City
# 0 Krish 32 Bangalore
# 1 John 34 Bangalore
print(df.tail(2))
# Name Age City
# 2 Bappy 32 Bangalore
# 3 JAck 32 Bangalore
print(df["Name"])
# 0 Krish 
# 1 John 
# 2 Bappy 
# 3 JAck
# Name: Name, dtype: object
print(df.loc[0])
# Name Krish 
# Age 25 
# City Bangalore 
# Name: 0, dtype: object
print(df.iloc[0])
# Name Krish 
# Age 25 
# City Bangalore 
# Name: 0, dtype: object
print(df.at[2,'Age']) # 32
print(df.iat[2,0]) # Bappy

# Adding a column
df['Salary']=[50000,60000,70000,80000]
print(df)
# Name Age City Salary
# 0 Krish 32 Bangalore 50000
# 1 John 34 Bangalore 60000
# 2 Bappy 32 Bangalore 70000
# 3 JAck 32 Bangalore 80000

## Remove a column
df.drop('Salary',axis=1,inplace=True)
print(df)
# Name Age City
# 0 Krish 32 Bangalore
# 1 John 34 Bangalore
# 2 Bappy 32 Bangalore
# 3 JAck 32 Bangalore

# Add age to the column
df['Age']=df['Age']+1
print(df)
# Name Age City
# 0 Krish 33 Bangalore
# 1 John 35 Bangalore
# 2 Bappy 33 Bangalore
# 3 JAck 33 Bangalore

df.drop(0,inplace=True)
print(df)
# Name Age City
# 1 John 35 Bangalore
# 2 Bappy 33 Bangalore
# 3 JAck 33 Bangalore

print("Data types:\n", df.dtypes)
# Data types:
# Name object
# Age int64
# City object
# dtype: object

print("Statistical summary:\n", df.describe())
# Statistical summary:
# Age
# count 3.000000
# mean 33.666667
# std 1.154701
# min 33.000000
# 25% 33.000000
# 50% 33.000000
# 75% 34.000000
# max 35.000000

df['new col']=[50000,60000]
## Handling Missing Values
print(df.isnull().any())
# Name False
# Age False
# City False
# dtype: bool
print(df.isnull().sum())
# Name 0
# Age 0
# City 0
# dtype: int64

df_filled=df.fillna(0)
# filling missing values with the mean of the column
df['Age_fillNA']=df['Age'].fillna(df['Age'].mean())

# change data type
df['Age_fillNA']=df['Age'].fillna(df['Age'].mean()).astype(int)

## Renaming Columns
df=df.rename(columns={'City':'Hometown'})
print(head(2))
# Name Age Hometown Age_fillNA
# 1 John 35 Bangalore 35
# 2 Bappy 33 Bangalore 33

df['New_Age']=df['Age'].apply(lambda x:x*2)
print(head(2))
# Name Age Hometown Age_fillNA New_Age
# 1 John 35 Bangalore 35 70
# 2 Bappy 33 Bangalore 33 66

## Data Aggregating And Grouping
df['Category']=['A', 'B', 'A']
print(df)
# Name Age Hometown Age_fillNA New_Age Category
# 1 John 35 Bangalore 35 70 A
# 2 Bappy 33 Bangalore 33 66 B
# 3 JAck 32 Bangalore 32 64 A

grouped_mean=df.groupby('Category')['Age'].mean()
print(grouped_mean)
# Category Age
# A 33.5
# B 33.0
# Name: Age, dtype: float64
```


