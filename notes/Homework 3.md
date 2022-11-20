---
attachments: [Clipboard_2022-04-27-22-41-51.png]
tags: [DBII]
title: Homework 3
created: '2022-04-27T21:51:11.554Z'
modified: '2022-04-28T02:46:52.303Z'
---

# Homework 3
## Problem 1
![](@attachment/Clipboard_2022-04-27-22-41-51.png)

## Problem 2
### Part 1
a. non-blocking, you only output an item if it is not already in the buffer
b. non-blocking becuase since X is sorted, you can output when X changes
c. blocking since you have to consume the whole record to acocunt for all stats
d. blocking, you output only until relation is sorted
e. non-blocking, you can use the btree to output
f. non-blocking, you can produce tuples before reading the entire relation
g. non-blocking, you produce the tuples as they are read, and can output right after

### Part 2
a. 
- done in 1 pass if the output can fit in 199 blocks. 
- Has to have less than M-1 = 199 tuples, I/Os = B(R) = 1000
- Two pass can be used which equals 3B(R) = 3000 I/Os

b. 
- one pass, 
- no constraints since main memory stores group statistics
- I/Os = B(R) = 1000

c. 
- can be done in 1 pass
- must be less than 199 groups, 1000 I/Os 
- two pass with 3000 I/Os

d. 
- cannot be 1 pass
- N/A
- two pass, 3000 I/Os

e.
- can be done in 1 pass
- no size constraint
- can take between 70 I/Os average and 70,000 I/0s worst case

f. 
- can be done in 1 pass
- must be able to fit S in memory
- B(S) + B(R) = 1000 + 150 = 1150 I/Os

g.
- can be done in 1 pass
- only 1 memory buffer
- B(S) + B(R) = 1150 I/Os
