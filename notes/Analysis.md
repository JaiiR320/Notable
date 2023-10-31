---
tags: [Algorithms]
title: Analysis
created: '2023-10-27T18:05:44.346Z'
modified: '2023-10-27T19:24:35.978Z'
---

# Analysis
## Big O Notation and Worst Case
Obtain bound on largest possible runnning time of algorithm on input of size N.
Example:
```python
arr = {1, 2, 3, 4, 5} # N = 4
for i in range(len(arr)):
  if i == t:
    return i
```
worst case is you search through entire array, so O(N), best case O(1)
However, generalized, the run time is O(N) as it will scale directly with array size. 
Worst case is pessimistic. However, it is easy to analyze, makes no assumptions and is robust, therefore can be generalized to all cases. 

O(N) ~ O(2N)
constants are hard to find, and are extremely dependant on implementation. 
Easier to remove coeffecients to again generalize the behavior of the algorithm

The point is to compare algoritnms on LARGE ENOUGH data sets.
Example: 
A = 100n+10, B = n^2/n
A is faster than B even though the run time is only faster for n>200

Logarithms have smaller order of growth than polynomials
polnomials have smaller order of growth than exponentials

Quiz:
f(n) = 3n^2 + 17nlog2(n) + 1000
What is the run time?

Explination: the function is a polynomial of degree 2, making the runtime n^2, but n^3 is the upper boundbecause it will never exceed n^3. Since there is more to the polynomial, it is probably higher than n^2 but never higher than n^3

## Multiple Variables
for m, n, f(mn^2 + n^2), o(n) = mn^3 + n^2 and mn^3
it is never just mn^3 or n^2

## When is an algorithm reasonable
Running the algorithm and seeing how it performs is sometimes not enough as you may miss certain bad cases. When is the algorithm runtime reasonable. Assume tha algorithm returns the correct answer. 

First understand when the algoithm is inefficient. 
For all nontribial problems, there is a brute force that typically takes 2^n, which is very bad.
An algorithm is considered effecient if the run time is polynomial, sometimes the constants and exponents can be high which makes it inefficient, but that is rare. 

## Common Run Time
Constant time O(1)
- comparisons
- conditional branches
- deckarations
- accessing elements in arrays...

Linear time O(n)
```python
for c in s:
  if c is 'a':
    return c
```
Iterate over the list N times, but only once

Quadratic time O(n^2)
```python
m = -999
for i in range(1, n):
  for j in range(i+1, n):
    d = a[i] + a[j]
    if d > m:
      m = d
```
Iterate over the list N times, but twice, so N*N = N^2

Cubic time
```python
for i in range(0, n):
  for j in range(i+1, n):
    for k in range(j+1, n):
      if a[i] + a[j] + a[k] == 0
        return (i, j, k)
```
Three nested for loops iterating over the same N, thereforre N^3

Exponential Time
Usually on brute force algorithms, where you have to look at all subsets of the list
Total subsets = 2^n, or exponential










































