---
tags: [Algorithms]
title: Dijkstra's Algorithm
created: '2023-10-31T19:14:43.365Z'
modified: '2023-11-07T19:26:43.306Z'
---

# Dijkstra's Algorithm
Directed graph, find shortest path between source S and target t.
To achieve this, use BFS to find if the node is reachable
Then compute scores

Most of the time the weights of the edges are positive as we are calculating effort, distance, energy etc. But there can be edges that are negai=tive, where they add value to taking the path such as downhill regenetive braking or financial transactions. 

### Dijkstra's Algorithm (G, l)
```
Let S be the set of explored nodes
  for each u in S, we store a distance d(u)
Initially S = |s| and d(s) = 0
While S!= V
  Select a node v notIn S with at least one edge from S for which
    d'(v) = min
  Add v to S and define d(v) = d'(v)
  ```

### Runtime
Naive approach n-1, at most adding n-1 nodes to S
runtime is O(nlog(m))

