---
tags: [Algorithms]
title: Dynamic Programming
created: '2023-11-21T19:05:57.978Z'
modified: '2023-11-21T20:28:17.838Z'
---

# Dynamic Programming
independent sets are a subset of vertices of a graph where no two vertices are connectedd by an edge

## Weighted Interval Scheduling
Find a set of compatible intervals with the maximum possible weight
Intervals are compatible if they dont intersect
order jobs by their final stop time
find intervals that are compatible that
if we have interval j, find interval p(j) to be compatible 
OPT(j) = o if j = 0, or max(vj + OPT(p(j)), OPT(j-1))
this recursion will run at exponential time, which is bad since we are doing the same calculations many times.

## memoization approach
iterate over 1 to n, compute the optimal weight (p(n)) for each vertex.
save those numbers to a list
M[0] = 0
for j in 1, n:
  M[j] = max(M(j-1), wj + M[p(j)])

# Knapsack
You have a limited capacity and items with weight and capacity, find the subset of items that maxamizes weight and capacity.

n items
ith item has value v and weight wi
capacity W
overall 2n-1 nonnegative integers

goal: pick a subset of items of maximal value and weight at most W

do following case analysis
opt(1...j) item either includes n or not
if not 

Opt(i, w) is optimal sollution with elements from 1 to i, and weight at most w
if next item is too expensive, we can't take it

if we dont take the i'th item, then opt(i-1, w)
if we do take the i'th item, then opt(i-1, w-wi) + vi






































