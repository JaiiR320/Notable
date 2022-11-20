---
attachments: [Clipboard_2022-04-24-19-36-52.png, Clipboard_2022-04-24-19-39-11.png]
tags: [DBII]
title: Hash Table
created: '2022-04-11T16:11:28.285Z'
modified: '2022-04-25T00:02:40.087Z'
---

# Hash Table

- array of buckets
- start index 0 to N-1
- contains key, and hash of key
- collision may occur during hash, make good has function bruh
- hash gives bucket index, which buckets contain multiple keys
- buckets are not sorted, saves from unnecessary I/O's
- create overflow bucket for insertions, makes more I/O's, defeats purpose
- change hash function to avoid overflow
- static hashing not good when hashing function is fine, but overflow occurs

## Disk-based Hash-based index
- adaptation of main memory hash tabes
- only supports equality searches

has table has N buckets (static)
each bucket will be 1 disk block
hash must be deterministic, no randomness

hash function depends on data type
examples:

#### Integer
- k % N

other data types require converting somehow
#### String
- c1 + c2 + c3... % N

#### Date
- num of days until certain date

hash table holds
| Key | Record ID |
|-|-|

### Example has lookup
- search for key d
- h(d) = 0, bucket 0
- read bucket 0
- search for key d in bucket 0
  - if keys are sorted, use binary search

only required 1 I/O

### Deletion
search for key, then do deletion
keep bucket if empty, number of primary buckets fixed
push keys up, empty space at end only
if deletion frees space, move stuff from overflow to primary

# Summary for quiz 4

## Static Hashing 
ONLY EQUALITY SEARCH
Holds a constant N buckets
Each bucket is a disk page/block
hash function maps key to a bucket
Each bucket holds same num of keys
keep entries sorted, reduces cpu time, but makes insert and delete expensive
stores <key, RID>
Could have overflow bucket, extension of a bucket

1. hash key
2. read associated bucket from disk
3. search for key (sorted, use binary search)

deletion - search for key, delete and delete overflow bucket, push keys up to reduce empty space
insertion - hash key, place key in specified bucket, place in overflow if needed

### Summary
Number of buckets fixed
common hash function
overflow buckets suck
potentially slow search time

## Dynamic Hashing
no overflow bucket
primary bucket size unfixed

directory uses n bits (global depth)

### Proposed Hash Funciton
take the last n bits of the key, equal to the global depth
key: 101101
depth:  XXX
bucket: 101

![](@attachment/Clipboard_2022-04-24-19-36-52.png)

take the bucket assigned, place value in bucket
if bucket is full (local depth = global depth), add another bit to global
make a new bucket and assign to a directory, directories will point to 2 buckets initially
besides the new one and old full one
re hash to place full bucket entries into the two new buckets
old buckets hold old depth value (so if they fill no need to resize global dir)

![](@attachment/Clipboard_2022-04-24-19-39-11.png)

### Summary
Lookup
 - global depth: num of bits needed
 - search bucket

Insertion
 - if a bucket has room, add
 - if no room
  - add new page without doubling if local < global
  - double directory if local = global

## True or False
static hashing, the number of primary buckets is fixed - **TRUE**
static hashing, search for a key is garunteed for 1 I/O - **FALSE**
dynamic hashing, local depth can be larger than global - **FALSE**
dynamic hashing, assume the dir array is in memory, the search is garunteed 1 I/O - **TRUE**
dynamic hashing, if global = 3, then a local can be 1 - **TRUE**




























