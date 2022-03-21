---
title: Homework 1
created: '2022-03-20T21:54:08.471Z'
modified: '2022-03-21T00:05:33.489Z'
---

# Homework 1

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
capacity = 10,737,418,240 bytes = 10 xB

### Q2
10,737,418,240 bytes / 8192 bytes/block = 1,310,720 blocks

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
total = 8ms + 5.55ms + 1.2ms = 14.75ms

### Q6
All of the blocks can be alligned on the same cylinder since there are 10 surfaces, and 10 blocks.

### Q7
The best way to store the blocks would be to allign 10 on the same cylinder, and the next 10 on the adjacent sectors, also on the same cylinder. That way, you read 10 blocks at once, and then the next 10 are next. Once the whole track is used, go to the next adjacent track to minimize seek time. If possible, aligning the data on the next track such that the end of the first track is aligned with the beginning of the next will reduce latency times.

**INITIAL DISK DELAY**
seek = 9.192ms
latency = 5.55ms

**MOVING TO NEW TRACK** (assumes tracks and blocks are aligned to reduce rotation latency)
seek = 1.002ms
latency = 0ms

total transfer time = 0.8ms/block * 1,563/10 blocks = 125.04ms

total average time to read = 125.04ms + 1.002ms*10tracks + 9.192ms + 5.55ms = 149.802ms average

assumes every 10 sequential blocks are alligned on the same cylinder, and all groupings of next 10 are sequentially alligned on the track, and the tracks are aligned such that the end of one track is aligned to the beginnning of another. This makes latency to align head on the next track 0. Have to traverse 10 cylinders, 25,008 sectors / 10 surfaces / 256 sectors/track ~ 9.7 -> 10 tracks 


## Problem 2




















