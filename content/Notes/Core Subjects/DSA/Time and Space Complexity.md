---
title: Time and Space Complexity
draft: false
tags: 
date: 10-Aug-2025
---
# Time Complexity
## What is Time Complexity?
The rate at which the time, required to run a code, changes with respect to the input size, is considered the time complexity.
![[Pasted image 20250810133149.png]]
## 3 rules to calculate time complexity
- calculate the time complexity for the worst-case scenario.
- it usaually depends on loops and recursion
- avoid including the elementary operation (constant terms).
    - **elementary operations**
        - Arithmetic operations
        - Comparison of primitive types
        - Input and output of primitive types
- avoid the lower values.
- $10^8 operations = 1 second$
## Types
### Linear Complexity O(n)
```c++
for (int j=n; j>=1; j--)
```
### Logarithmic Complexity O(logn) (base=k)
```c++
for (int i=1; i<=n; i*=k) 
// or, 
for (int i=n; i>=1; i/=k)
```
### Sqrt Complexity O(sqrt(n))
```c++
for (int i=1; i<=sqrt(n); i++) 
// or, 
for (int i=1; i*i<n; i++)
```
### Quadratic complexity O(n^2)
```c++
for (int i=0; i<n; i++) 
	for (int j=0; j<n; j++)
```
### Linearithmic complexity O(Nlogk)
```c++
for (int i=0; i<n; i++) 
	for (int i=1; i<=n; i*=k)
```
## Time Complexity based on Constraints
![[Pasted image 20250810133922.png]]
## Recursive Time Complexity
![[Pasted image 20250810134001.png]]
![[Pasted image 20250810134014.png]]
# Space Complexity
## What is Space Complexity?
The term space complexity generally refers to the memory space that a code uses while being executed.
## Types
Space complexity generally represents the summation of auxiliary space and the input space.
- Auxiliary space refers to the space that we use additionally to solve a problem.
- Input space refers to the space that we use to store the inputs.
## Why data should not be manipulated?
- If a question of adding two numbers like a and b is asked,
	- one of the possible methods will be b = a+b. In this case, the space complexity is definitely reduced as we are not using any extra variable but this is not a good practice to manipulate the given inputs or data.
- In an interview, we must be careful that we will not manipulate the given data even if the space complexity becomes 2N instead of N. If the interviewer specifically instructs us to manipulate, then only we should attempt this method.
- Note: A company may use the same data for different purposes. That is why we should not attempt to manipulate the given data for reducing the space complexity. So, we will never manipulate the given data i.e. the inputs until the interviewer specifically says so.
# Asymptotic Notation
![[Pasted image 20250810134231.png]]
![[Pasted image 20250810134249.png]]
![[Pasted image 20250810134302.png]]
![[Pasted image 20250810134321.png]]

