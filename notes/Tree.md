---
tags: [Algorithms]
title: Tree
created: '2023-11-07T19:30:01.383Z'
modified: '2023-11-07T20:49:42.474Z'
---

# Tree
## What is a Spanning Tree
In an Undirected Graph, a subset of edges that is both ascyclic and connected
A tree is a graph that is connected and has no cycles
An n vertex graph is a tree if and only if it has n-1 edges and is connected
## Proving a Graph is a tree
Assume the graph is connected, n-1 edges
Remove all nodes and ad the first node, in the beginning, there are n connected components
Then we add each edge one by one, if the number of connected components decreases by at most 1
If the number does not change, then the graph has a cycle
We must add atleast n-1 edges to make the graph connected

Fact: If we remove 1 edge from a cycle in a connected graph, the graph remains connected
Proof:
  If the edge was a part of a path between u and v, replace it
  If it was not, then we good

Every Graph has a spanning tree
To make a tree, if the graph has a cycle, remove an edge then continue. 

Suppose T is connected and has n-1 edges
  It does not have a cycle
  This is because the bare minimum for connectivitiy is n-1 edged,
  if there is a cycle, break it, and if the number edges is n-2 then it is not connected anymore

## Minimum Spanning
Find a tree where the sum of the edge weights is minimized
In this we are just trying to find the **subset of edges** in the graph that minimizes the edge weight sum

### Cut and Cutset
a cut is a subset of nodes S the corresponding cutset D is a subset of edges with exactly one endpoint in S

## Algorithms determining MST
Assumptino: each edge has a unique value

Cut Property:
  Suppose S is any subset of nodes, and e is the minimum cost edge with exactly one endpoint in S, then MST contains e.

Pf:
  Syooise e=(x,y) does not belong to T*, and lets see what happens
  Since x,y are connected in T* there is a path P connecting them

### Prims Algorithm
Initialize S
Repeat n-1 times
  Add to T a minimum-cost edge with one endpoint in S
  add new node to S

Output is always connected, by nature the algorithm just grows off the starting nod

Runtime = O(mlog(n))

### Reverse Delete aproach
Find a cycle, delete the max-cost edge in the cycle, repeat

Cycle Property: 
  Let C be a cycle in G
  let f=u,v be the max cost edge belonging to C, 
  then any MST T* does not contain f (delete f from C, by extension G)

Runtime = m*n + n










