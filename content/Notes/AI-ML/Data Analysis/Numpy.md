---
title: Numpy
draft: false
tags:
  - component
date: 21-Aug-2025
---
# References

# Introduction
Numpy provides support for arrays and matrices, along with a collection of mathematical functions to operate on these data structures
```python
!pip install numpy

import numpy as np
```

# Array
```python
# 1d array
arr1 = array([1,2,3,4,5])
print(arr1) # [1,2,3,4,5]
print(type(arr1)) # <class 'numpy.ndarray'>
print(arr1.shape) # (5,)

arr1.reshape(1,5) # array([[1, 2, 3, 4, 5]`]) 1 row and 5 columns

# 2d array
arr2=np.array([[1,2,3,4,5],[2,3,4,5,6]])
print(arr2) # [[1 2 3 4 5] [2 3 4 5 6]]
print(arr2.shape) # (2,5)

np.arange(0,10,2).reshape(5,1) # array([[0], [2], [4], [6], [8]])
np.ones((3,4)) # array([[1., 1., 1., 1.], [1., 1., 1., 1.], [1., 1., 1., 1.]])

## identity matrix
np.eye(3) # array([[1., 0., 0.], [0., 1., 0.], [0., 0., 1.]])

## Attributes of Numpy Array
arr = np.array([[1, 2, 3], [4, 5, 6]])

print("Array:\n", arr)
print("Shape:", arr.shape) # Output: (2, 3)
print("Number of dimensions:", arr.ndim) # Output: 2
print("Size (number of elements):", arr.size) # Output: 6
print("Data type:", arr.dtype) # Output: int32 (may vary based on platform)
print("Item size (in bytes):", arr.itemsize) # Output: 8 (may vary based on platform)

## Logical operation
data=np.array([1,2,3,4,5,6,7,8,9,10])
data[(data>=5) & (data<=8)] # array([5, 6, 7, 8])
```
## Slicing and Indexing
```python
arr=np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print(arr[1:,1:3]) # [[ 6 7] [10 11]]
print(arr[0][0]) # 1
print(arr[0:2,2:]) # [[3 4] [7 8]]
print(arr[1:,2:]) # [[7, 8], [11, 12]]

## Modify array elements
arr[0,0]=100
print(arr) # [[100 2 3 4] [ 5 6 7 8] [ 9 10 11 12]]
arr[1:]=100
print(arr) # [[100 2 3 4] [100 100 100 100] [100 100 100 100]]

```
# Universal Function
```python
arr=np.array([2,3,4,5,6])

## square root
print(np.sqrt(arr)) # [1.41421356 1.73205081 2. 2.23606798 2.44948974]

## Exponential
print(np.exp(arr)) # [ 7.3890561 20.08553692 54.59815003 148.4131591 403.42879349]

## Sine
print(np.sin(arr)) # [ 0.90929743 0.14112001 -0.7568025 -0.95892427 -0.2794155 ]

## natural log
print(np.log(arr)) # [0.69314718 1.09861229 1.38629436 1.60943791 1.79175947]
```
# Vector
```python
arr1=np.array([1,2,3,4,5])
arr2=np.array([10,20,30,40,50])

### Element Wise addition
print("Addition:", arr1+arr2) # Addition: [11 22 33 44 55]

## Element Wise Substraction
print("Substraction:", arr1-arr2) # Substraction: [ -9 -18 -27 -36 -45]

# Element-wise multiplication
print("Multiplication:", arr1 * arr2) # Multiplication: [ 10 40 90 160 250]

# Element-wise division
print("Division:", arr1 / arr2) # Division: [0.1 0.1 0.1 0.1 0.1]


```
# Statistics
```python
### statistical concepts--Normalization
##to have a mean of 0 and standard deviation of 1
data = np.array([1, 2, 3, 4, 5])

# Calculate the mean and standard deviation
mean = np.mean(data)
std_dev = np.std(data)

# Normalize the data
normalized_data = (data - mean) / std_dev
print("Normalized data:", normalized_data) # Normalized data: [-1.41421356 -0.70710678 0. 0.70710678 1.41421356]

# Mean
mean = np.mean(data)
print("Mean:", mean) # Mean: 5.5

# Median
median = np.median(data)
print("Median:", median) # Median: 5.5

# Standard deviation
std_dev = np.std(data)
print("Standard Deviation:", std_dev) # Standard Deviation: 2.8722813232690143

# Variance
variance = np.var(data)
print("Variance:", variance) # Variance: 8.25
```