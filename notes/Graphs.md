---
tags: [Algorithms]
title: Graphs
created: '2023-10-27T19:25:34.776Z'
modified: '2023-11-07T19:48:37.575Z'
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

## Handshake Lemma
Sum v in V degree v = 2|E|
the complexity scales with the sum of the degrees
for a graph with no edges and v vertices, as you add an edge, you increment the degree of the pair of nodes by 1, therefore double counting the edge in the total number of degrees in the graph

proof: when you scan all the vertices and increment the degrees, when you encounter the second half of a pair, you count the same edge twice.

### Paths and connectivity
A path is a sequence of nodes where each consecutive pair connects two nodes. 
Connected components are a set of vertices that are all connected. For any pair of nodes in that component, there is a path between them.

Definition: a undirected gaph is connected if for every pair of nodex u, v, there exists a path between u and v. 

Fact: Two different connected componnets are disjoint. 

Cycle
Def: a simple path in which all nodes are distinc

Connected graphs have atleast n-1 edges, but does not proove a graph is connected if it has n-1 edges

### Shortest Path Algorithm
Shortest path meaning fewest number of edges. If path does not exist, assume it is infinity. Distance to itself is 0. 
#### BFS
Essence of BFS is you start at a node, and look at the next layer or d=1. Then look at next layer etc. until you search through entire graph. 
Layer 1: Distance = 1 if it is a neighbor. 
Layer 2: All neighbors of L1, but not any node from L1/previous layers.
Layer i+1: Set of all neighbors that do not belong to previous layers.
Li is a layer where the nodes are distance i from s. 

Algorithm;
```
set a discovered list
initialize List[0]

while L[i] not empty:
  initialize L[i+1]
  for node u in L[i]
    if u discovered:
      discovered[u] = true:
```
runtime is dependant on the degree of each of the nodes.
Therefore, handshake lemma tellls us the number of processes.

## Bipartie Graphs
The graph is Bipartite when the nodes of the graph can be colored white or blue such that every edge has one white and one blue end.

### Bipartite Lemma
A graph g that is bipartite **cannot** have an odd numbered cycle. 

Lemma: Let G be a connected graph, and let L0...Li be the layets produced by BFS starting at node s
Exactly one of the following holds
  **NO** edge of G joins two nodes of the same layer and G is bipartite
  **An** edge of G joins two nodes of the same layer and G contains an odd length cycle, G is not bipartite. 

Bipartite when no nodes on the same level contain edges, and white nodes are even, blue odd or visa versa.

Lowest Common Ancestor
Vertes C in a layer i less j such that there exists a path from c to x and v with all vertices of the pashs belonging to layers with indices in [i,j]
j is the maximum index where such a c exists.

### Practice problem:

For any graph of nodes n, with edges n-1 probe there is at least 1 leaf

Handshake lemma states Sum(deg(n)) = 2e,
proof by contradiction, e = n-1, 2(n-1) = 2n-2 != 2e, for this to work, there hass to be atleast 2 nodes with degree 1 such that 





## Directed Graphs
Suppose you have a directed graph with no self-referencing nodes. How many nodes can you have?
n^2 - n


### Strong Connectivity
Strong connectivity is whenevery pair of nodes is mutually reachable. 
To check, run BFS from every point to see if the others are reachable

Better approach is to 

### Strong Connectivity Lemma
Let S be a node in G. G is strongly connected if every node is reachable from s, and s is reachable from every node.

Look at any pair of vertices, u and v. 
Proof: 
path from u to v: concatenate u~s and s~v
Path from v to u: concatenate v~s and s~u

G can be determined strongly connected in O(m+n) time
Pick any node s
Run BFS from node s in G
Run BFS from node s in G reverse
v is reachable from s in G reverse, directed path from v to s in G

return true if all nodes reached in both BFS executions
correctness follows immediately from previous lemma

If both BFS executions discovers all nodes. This happens if the graph is strongly connected, therefore proving that it is. 

### Strong components
A maximal subset of mutually reachable nodes. For example, a collection of nodes that are strongly connected are a strong component. 
You can find all strong components in O(m+n) time

#### Recap
Direted graphs:
  Directed reachability can be done in time O(v + e)
  Strong connectivity: every pair is reachable from eachother

## Directed Acyclic Graphs
A DAG is a directed graph that contains no directed cycles
A tpoological order of a directed graph G=(V, E) is an ordering of its nodes as v... so that for every edge we have no backward edge. 


### Lemma
if G has a topological order, then G has to be a DAG
Cannot have a cycle that goes back. The ordering keeps moving forward.

How do you know if a graph is a DAG?
Does every DAG have a topological ordering?
If so, how do we compute?






































