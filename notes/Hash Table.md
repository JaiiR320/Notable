---
tags: [DBII]
title: Hash Table
created: '2022-04-11T16:11:28.285Z'
modified: '2022-04-11T16:47:12.897Z'
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

























