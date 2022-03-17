---
attachments: [Clipboard_2022-03-17-12-39-15.png, Clipboard_2022-03-17-12-46-36.png]
tags: [DBII]
title: Storage
created: '2022-03-17T15:59:40.787Z'
modified: '2022-03-17T16:46:42.368Z'
---

# Storage
#### Brush up on
- SQL 
- Query Operators
- imperative query execution plan
- transaction

#### ACID
- Atomic
- Consistent
- Independent
- Durability

### Size Translations
| Power | Size |
|-|-|
| 2^10 | KB |
| 2^20 | MB |
| 2^30 | GB |

## Disk
num platters * 2 faces * 8192 tracks * 256 sectors * 512 bytes / sector
p * 2^1 * 2^13 * 2^8 * 2^9
p * 2^33, 2^30 = 1GB, 2^3 = 8, 8GB per platter

### Disk properties
many platters with 2 sides, and many tracks per side
tracks contain data, and each track has a number of sectors
cylinder are tracks aligned vertically on all surfaces of platter
1 head for every surface, 4 platters = 8 surfaces = 8 heads
must read 1 block at a time, cannot access data randomly
1 block consists of multiple sectors
best placement for sequential data is on the same tracks but different platters (the cylinder)
Disk Image [^1]

#### How it works
the arm has to seek a specific track that the block is on
the arm moves linearly to the correct track
then the spindle spins the disk/platters so the head is on the 1st byte of the block
the head then reads/writes on the block as the spindle spins the disk
as this happens, the read/write can happen simultaneously on the cylinder

## Seek, Latency, Transfer time
I/O always 1 block of memory = 1 unit of data, has to be completed
1 block is 4KB or 8KB depending on config
Seek time is time to put the head on the right track
latency timie is time until head is at the first byte of the block
time to read the block is transfer time

### Best, Worst, Average Disk Time
| Type | Best | Worst | Average |
|------|------|-------|---------|
| Seek | head is on the correct track, 0ms | need to travel all tracks, warmup + time/n tracks | warmup + half tracks |
| Latency | head is on first byte, no rotation | head is on second byte, nearly full rotation | head is halfway to first byte, half rotation |
| Transfer | 1 full block | 1 full block | 1 full block |
Transfer is always constant

## Optimization
Putting the similar data on the cylinder can speed up I/O operations
This is because the seek and latency will be the same for each block, meaning they are ligned up simultaneously
Total Disk latency is just calculated as if reading 1 block, because they are all read at the same time
After the cylinder is taken up, putting blocks on the next track will be the next best option

#### Disk Striping
distributing data among more disks will speed up also. Puting the blocks on the same cylinder on different disks will be ideal. Since each disk works independently, the block-pairs do not need to be on the same cylinder.

#### Disk Mirroring
Multiple disks, but some are copies. Advantage is you can recover from failure.
The same content that is on disk 1, is also on disk 2. You can split up requests to access data on a disk by giving those requests to other disks. Load balancing. If you have 8 disks, you are reducing your capacity by half. When you write, you have to write on the mirror so it adds overhead.

#### Disk Scheduling
Disk controller controls the disks, and may have a sequence of block requests. Scheduling takes care of reducing time. 

### SCAN scheduling
Input
- current position of head
- direction left(outer), right(inner)
- queue of requests

Algorithm
- Move in decided direction
- serve requests in the order of seeing them (closest to head)
- reach end of disk in this direction (only complete current requests not new)
- reverse direction
- serve remaining requests in this direction

New requests are served after the direction is reversed, so the head has to go to the end before reversing

#### Example
Request Sequence = {176, 79, 34, 60, 92, 11, 41, 114}
initial position = 50
direction = left

![](@attachment/Clipboard_2022-03-17-12-39-15.png)



[^1]: ![](@attachment/Clipboard_2022-03-17-12-46-36.png)






