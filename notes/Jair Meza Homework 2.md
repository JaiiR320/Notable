---
attachments: [Clipboard_2022-04-09-22-25-32.png, Clipboard_2022-04-09-22-37-16.png, Clipboard_2022-04-09-22-38-33.png, Clipboard_2022-04-09-22-39-59.png, Clipboard_2022-04-09-22-42-42.png]
tags: [DBII]
title: Jair Meza Homework 2
created: '2022-04-06T16:05:09.542Z'
modified: '2022-04-10T02:43:03.174Z'
---

# Jair Meza Homework 2

## Problem 1

### b
Total IOs = 2n(log m-1 (n/m) + 1) 
log4(40) = 2.6 ~ 3 + 1 = 4
2(200) * 4
1600 IOs

prep = 200/5 = 40
merge 1 = 40/4 = 10
merge 2 = 10 / 4 = 3

### a
log7(200/8) = 1.6 ~ 2 + 1 = 3
2(200) * 3 = 1200 IOs

prep = 200/8 = 25
merge 1 = 25/7 = 4
merge 2 = 4/7 = 1

## Problem 2

### 1
1,000,000 blocks data
20 records / block
20,000,000 records
k1 = primary key
K1, K2 = 20 bytes
record pointer = 8 bytes
8KB 

yes, the dense list will point to the K1 column, and each index record will be 20 + 8 bytes.
8192 bytes / 28 bytes = 292 records in a block
2,000,000 records / 292 records per block = **68,494 blocks**

### 2
Yes, because K1 is the primary key, which is sorted. The index records are 20 + 8 bytes.
292 records in a block
1,000,000 / 292 = **3,425 blocks**

### 3
Yes, dense index's do not require sorted columns. 292 records / block.
2,000,000 records / 292 records per block = **68,494 blocks**

### 4
No a sparse index cannot be created unless K2 is sorted.

### 5
Yes, a sparse index can be created as the second level index. The sparse index entries will point to a block in the first level index.
68,494 blocks blocks total (from part 1)
second 1
68,494 blocks / 292 records = **235 blocks**
total blocks = 235 + 68,494 = **68,729 blocks**

### 6
Yes a second level index can be created on top of the first level sparse index.
second level
3,425 blocks / 292 entries = 12 blocks
total blocks = 3,425 + 12 = **3,437 blocks**

## Problem 3
### 1
start at N1
35 > 13 -> N3
31 < 35 < 43 -> N8
35 not in N8

### 2
start at N1
[9, 21]
9 < 13 -> N2
9 > 7 -> N5
N5 -> N6 to get next
stop at N6

### 3
insert 4
4 < 13 -> N2
4 < 7 -> N4
N4 full, split N4 
insert 4 into new node
insert 4 into N2
update pointers
![](@attachment/Clipboard_2022-04-09-22-25-32.png)
"sorry its a bit messy, entire right branch stays the same"

### 4
![](@attachment/Clipboard_2022-04-09-22-37-16.png)
![](@attachment/Clipboard_2022-04-09-22-38-33.png)
![](@attachment/Clipboard_2022-04-09-22-39-59.png)

### 5
[6, 13]
start at N1
6 < 13 -> N2
6 < 7 -> N6
N6 -> N7 -> N8 to get rest

### 6
delete 23
![](@attachment/Clipboard_2022-04-09-22-42-42.png)



















