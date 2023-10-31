---
tags: [Algorithms]
title: Graphs
created: '2023-10-27T19:25:34.776Z'
modified: '2023-10-27T19:50:27.070Z'
---

# Graphs
## Undirected Graphs
V nodes, E edges
Set of nodes is finite
m = number of edges, n = number of nodes
degree = number of neighbors of a node
max number of edges is nc2 or n(n-1)/2

two common representations of graphs

### Adjacency Matrix
a matrix nxn, where each element is a 0 or 1 depending on if the indeces are edges
Checking edges is O(1) as you just access the matrix at the indices. 

### Adjacency lists
Node-indexed array of linked lists
checking if U and V are neighbors, is O(degree(U)) because you go to U, and traverse U's list which is the degree of u to find V
Use lists to scan all neighbors of V in time O(degree(V))

### Handshake Lemma
Sum v in V degree v = 2|E|
the complexity scales with the sum of the degrees
for a graph with no edges and v vertices, as you add an edge, you increment the degree of the pair of nodes by 1, therefore double counting the edge in the total number of degrees in the graph

proof: when you scan all the vertices and increment the degrees, when you encounter the second half of a pair, you count the same edge twice.

### Paths and connectivity
A path is a sequence of nodes where each consecutive pair connects two nodes. 
