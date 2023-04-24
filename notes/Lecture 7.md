---
tags: [CS4513]
title: Lecture 7
created: '2023-04-03T15:15:58.291Z'
modified: '2023-04-03T16:45:16.919Z'
---

# Lecture 7
## RAID
RAID - Redundant Array of Inexpensive Disks
large fast and reliable with some form of redundency

RAID design 1 - striping
Each disk holds consecutive blocks
NxB blocks, not reliable becuase no redundency
very fast, all disks are utilized often in parallel
single request latency vs steady-state throughput

parity
use xor to create parity
even number of 1s outputs a 0, odd outputs a 1
if a column is lose, use the parity bit to determine if data is a 1 or 0
(N-1) x B capacity

raid-5 parity - rotating parity
identical to raid 4, but parity stored in round robin
Each disk holds a parity block in a round robin format
all 4 disks can be used at the same time, 
NxR MB/s because all disks are in parallel
N/4 x R MB/s writes as allows for parallelism across requests
can scale with more disks

RAID-0 good for performance and not reliability
RAID-1 good for random IO and reliability
RAID-5 for capacity and reliability

## Crash Consistency
file system data structures must persist on crash, power loss etc. 
two solutions
journaling(write ahead logging) and fsck(file system checker, old)

concsistency = bitmap and inode agree
























