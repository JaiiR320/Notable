---
attachments: [Clipboard_2022-04-02-12-52-51.png]
tags: [DBII]
title: Scanning files
created: '2022-04-02T16:38:40.715Z'
modified: '2022-04-02T17:59:50.907Z'
---

# Scanning files

Index Lookup
```SQL
SELECT *
FROM Transactions
WHERE TID=1000
```
This query is cheap because the index can be used to lookup. Cheaper to use index than full table scan

Full Table
```SQL
SELECT * 
FROM Transactions;
```
Selects everything from transactions, so full table is cheaper than index because there is no added processing for index.

## Full Table Scan
Given a table: 
- must know how many blocks
- where each block is

First insert creates a new block for records, and as the block fills up, the system creates a second block. Any table created will have a **Data File** and will create a **Directory File**

Directory file contains blocks with small recprd entries that point to a data block. The first entry points to block 1, second entry points to block 2 etc. 
Points to block ID <Disk, Platter, Surface...>
Only requires 1 memory block

![](@attachment/Clipboard_2022-04-02-12-52-51.png)

### Cost
N, where N is number of blocks

## Index Lookup
Usually more effecient than full table scan
Index file consists of records (index entries) that point to record with that ID
Assumes records are sorted by the column we want to index

#### Index affects
- Query Time
- Insertion
- Deletion/Update
- Space overhead

Indexing adds a lot of overhead, but can improve query times. If indexing is necessary for queries, thne you can add indexing.

#### Access types supported
Equality Search (x = 100)
Range Search (10 < x < 100)

### Dense Index
Has one entry for each data tuple
Index entries are very small, can put more in a single block
Binary search over index blocks
Can have multiple dense indice for a table because the table does not have ot be sorted since the indices are directly pointing to a record. 
If you query for an index that does not exist, you don't have to look for the record if the index does not exist in the first pace. You can stop right there.
The actual order f the index entries are sorted, not necessarily the table entries  

Deliting by index, move other indices up and leave empty space at the end. Data may or may not move inside it's block

### Sparse Index
1 entry for every block
Each entry of the sparse index points to the beginning of the blocks holding the records
Has to be sorted file, if unsorted then it will not work
Less indices than dense
You can only have 1 sparse index for a table, because the table must be sorted on 1 column for sparse index.
If you search for an index that does not exist, you still have to search the data block because we don't know if the record exists explicitly

Deleting an entry that is not the first will leave empty space in the data block
index will not change
Deleting the index will require updating the index, swap the second entry for the index
Deliting from the index, must update index and leave empty space at END not middle

Insertion, follow pointer to appropriate block, if there is space and the record is new, put it at the end IN ORDER
DBMS May have 10% free space to allow for easy insertion
Overflow blocks is an extension so that you dont have to push down records, block has some extensions

## Example
record = 200 bytes
10^6 records
disk block = 4KB = 4096, header = 96 bytes

Data File: 4000 / 200 = 20 records per block
10^6 records / 20 records per block = 50000 blocks

Dense:
4000 bytes / 20 bytes per entry  = 200 indices per block
10^6 entries / 200 entries per block = 5000 blocks for indices

Sparse:
4000 bytes / 20 bytes per entry  = 200 indices per block
50000 entries / 200 entries per block = 250 blocks


























