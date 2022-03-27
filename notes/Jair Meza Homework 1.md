---
tags: [DBII]
title: Jair Meza Homework 1
created: '2022-03-20T21:54:08.471Z'
modified: '2022-03-25T21:09:38.802Z'
---

# Jair Meza Homework 1

## Problem 1
setup:
- 5 platters, 8,192 tracks, 256 sectors/track
- sector 512 bytes
- 5400 RPM
- seek time: 1ms warmup, 500 tracks 1ms
- reading: 0.05 ms/sector
- block: 8K bytes (8*1024)
- 16 sectors for 1 block

### Q1
capacity = 5 platters * 2 sides/platter * 8192 tracks/surface * 256 sectors/track * 512 Bytes/sector
capacity = 10,737,418,240 bytes = **10 GB**

### Q2
10,737,418,240 bytes / 8192 bytes/block = **1,310,720 blocks**

### Q3
| process | best | worst | average |
|---------|------|-------|---------|
| seek | 0ms | 17.384ms | 9.192ms | 
| latency | 0ms | 11.11ms | 5.55ms |
| transfer | 0.8ms | 0.8ms | 0.8ms |
| **Total** | **0.8ms** | **29.295ms** | **15.542ms** | 

### Q4
8,192 bytes/block / 128 bytes/record = **64 records/block**
100,000 records / 64 records/block = 1,562.5 blocks -> **1563 blocks total** (cant read less than a block)
1563 reserved blocks * 16 sectors/block = **25,008 sectors total**

### Q5
seek = 1ms warmup + 1ms/500 tracks * 100 tracks = 1.2ms
latency = 60s/5400RPM * 1/2 = 5.55ms
transfer = 0.8ms * 10 blocks = 8ms
total = 8ms + 5.55ms + 1.2ms = **14.75ms**

### Q6
All of the blocks can be alligned on the same cylinder since there are 10 surfaces, and 10 blocks.

### Q7
The best way to store the blocks would be to allign 10 on the same cylinder, and the next 10 on the adjacent sectors, also on the same cylinder. That way, you read 10 blocks at once, and then the next 10 are next. Once the whole track is used, go to the next adjacent track to minimize seek time. If possible, aligning the data on the next track such that the end of the first track is aligned with the beginning of the next will reduce latency times. Any time a portion of a block is utilized, we round up because only whole blocks can be read.

**INITIAL DISK DELAY**
seek = 9.192ms
latency = 5.55ms

**MOVING TO NEW TRACK** (assumes tracks and blocks are aligned to reduce rotation latency)
seek = 1ms + 0.002ms
latency = 0ms

total transfer time = 0.8ms/block * 157 blocks (1563 total blocks / 10 surfaces = 156.3 but have to read the whole block) = 125.6ms

total average time to read = 125.6 + 1.002ms*9tracks + 9.192ms + 5.55ms = 
**149.36ms average**

## Problem 2
setup:
- header 8 bytes
- ID 4 bytes
- Name 25 bytes
- age 10 bytes
- DoB 10 bytes
- gender 1 byte
- address 60 bytes
- state 2 bytes

### Q1
4 byte boundaries
- header 8 bytes
- ID 4 bytes
- Name 25 + 3 bytes
- age 4 + 0 bytes
- DoB 10 + 2 bytes
- gender 1 + 3 byte
- address 60 bytes
- state 2 + 2 bytes

total: 8 + 4 + 28 + 4 + 12 + 4 + 60 + 4 = **124 bytes**

### Q2
8 byte boundaries
- header 8 bytes
- ID 4 + 4 bytes
- Name 25 + 7 bytes
- age 4 + 4 bytes
- DoB 10 + 6 bytes
- gender 1 + 7 byte
- address 60 + 4 bytes
- state 2 + 6 bytes

total: 8 + 8 + 32 + 8 + 16 + 8 + 64 + 8 = **152 bytes**

### Q3
4 * 1024 - 64 = 4032 bytes of usable space

4 byte boundary records: 4032/124 = 32 records
8 byte boundary records: 4032/152 = 26 records
















