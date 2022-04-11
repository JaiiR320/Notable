---
tags: [DBII]
title: B Tree
created: '2022-04-09T19:31:05.414Z'
modified: '2022-04-10T02:15:00.187Z'
---

# B Tree
### Disk Based
- every node is 1 block
- each node holds N keys, N+1 pointers
- at least 50% full
- no empty space in middle of node

### Multi Level
- has one root and leaf nodes
- always start from root for processing

### Balanced Tree
- leaf nodes are all at same height

**size_of_key*N + size_of_pointer(N+1) = usable_space bytes**

Example.
Disk block = 4096 - 96 header
ID = int = 4 bytes
pointer = 10 bytes

N keys, N+1 pointers

4N + 10(N+1) = 4000 bytes
N = 285 nodes


