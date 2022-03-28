---
attachments: [Clipboard_2022-03-24-16-14-11.png, Clipboard_2022-03-28-10-03-30.png, Clipboard_2022-03-28-10-03-46.png]
title: Buffer Manager
created: '2022-03-24T19:47:49.210Z'
modified: '2022-03-28T14:03:46.816Z'
---

# Buffer Manager

Higher-level component interact with Buffer Manager
Manages blocks that should be in memory and for how long
Any processing requires data to be in main memory

## Buffer Management in BDMS
DBMS is allocated a buffer pool, which is an array of objects (frames) in main memory
Frames or memory page are equal in size of disk blocks
Metadata structure holds block ID and Frame ID that it is placed in
Since in memory, placement in the pool is irrelevant, random access
Only I/O to write back to disk is necessary when data changes, dirty bit

### Metadata Example
| BID | Frame ID | Dirty |
|-----|----------|-------|
| B20 | F1 | 0 | 
| B15 | F12 | 1 |
| B3 | F36 | 0 |

### Summary
Buffer pool is chunk of memory allocated for DBMS that contains frames equal in size as system block size. Frames may be empty or contain a disk page.
Flow of events [^1]

## Buffer Pool Scheduling
![](@attachment/Clipboard_2022-03-28-10-03-30.png)
![](@attachment/Clipboard_2022-03-28-10-03-46.png)

[^1]:![](@attachment/Clipboard_2022-03-24-16-14-11.png)
