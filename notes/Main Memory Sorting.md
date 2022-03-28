---
attachments: [Clipboard_2022-03-28-11-35-49.png]
tags: [DBII]
title: Main Memory Sorting
created: '2022-03-28T15:28:22.865Z'
modified: '2022-03-28T16:45:41.035Z'
---

# Main Memory Sorting

## Preface

- Merge Sort
- Heap Sort
- Quick Sort

all nlog(n)

In DBMS, data is very large and does not fit in main memory

DBMS may use sorting explicitly with ORDER commands
May also use sorting implicitly with grouping by fields
SELECT name GROUP BY zipcode

Given 10GB of data memory is only ~100 MB

## Using Secondary Storage
General Wisdom
- I/O costs dominate
- Design algorithms to reduce I/O
- CPU overhead becomes less important

**1 I/O operation = 10^5 CPU operations**

## Merging 2 Sorted Lists
![](@attachment/Clipboard_2022-03-28-11-35-49.png)
2 pointers, pointing to the smallest in each list, take the smallest value of the pointers and advanced the used pointer by 1 position, then compare pointers again
O(n+m), since you go through each list once
If you have large lists, and can only view a certain number of entries at once, once a list is used up, ask for the next N entries and continue the merge.

## 2-Way External Sort (Naive Way)
Phase 1: Prepare
- read a page, sort it, write it
- only one page buffer required

Phase 2, 3...n: Merge
- take 2 blocks, merge into 1 block and write when full
- continue merging into the output block and writing
- take next 2 blocks and repeat
- once all pairs are sorted, sort the pairs with other pairs etc.

During merge step, you ONLY need 3 memory buffers, 2 for the blocks you want to merge, and the 3rd for the output. If the lists are larger than 1 block, then you only store the first block and pull in the second when you exhaust the block. Same with output, you only write to disk when the output is full, and then erase/write over.

Number of I/Os in each phase = 2n, reading all blocks and writing all blocks every phase
Number of merge phases = log2(n) + 1, you divide the initial number of runs by 2 each time
n, n/2, n/4... 1

### Total I/Os
2n(log2(n) + 1)

## M-way External Merge Sort
Buffer Pool usually has many frames, you can use all the buffers to merge

Phase 1: Prepare
- bring in M buffers, and sort into M blocks in memory
- write them back to disk
- sort m blocks into 1 giant list of size m, no need for output block
- this makes a list of blocks that are all sorted together, so the run is size m

number of runs after preperation phase = n/m, number of runs = m

Phase 2: Merge
- keep 1 buffer for output
- merge m-1 buffers together simultaneously
- take m-1 runs (collection of blocks that are sorted together)

number of merge phases = n/m, n/m/(m-1), n/m/(m-1)^2... 1
log m-1 (n/m)
number of I/Os = 2n, always reading all blocks and writing all blocks

### Total I/Os
2n(log m-1 (n/m) + 1) = number of I/Os

Example:
your buffer pool can hold 10 blocks and you have 1000 blocks to sort
you take 10 blocks, sort the 10 together, and write them back to dis
this makes a RUN of 10 blocks
do this 10 more times to sort create 10 sorted lists of 10 blocks each
then you take the first block of each list and hold 1 block for the output
in this case you can only hold 9 runs, so you merge these runs
then since you have 1 massive run and 1 small run, you can do the same step
take the first block of each run and merge


Example:
10 buffer page, 20,000 pages
m = 10, n = 20,000
2-way
- number of I/os = 2(20,000) * (1 + log2(20,000)) = 640,000 I/Os
m-way
number of I/Os = 2(20,000) (log 9 (20,000/10) + 1) = 200,000 I/Os

m-way is much lower number of I/Os, more effecient
















