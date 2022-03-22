---
attachments: [Clipboard_2022-03-21-11-34-25.png, Clipboard_2022-03-21-11-35-08.png, Clipboard_2022-03-21-11-36-00.png, Clipboard_2022-03-21-11-38-06.png, Clipboard_2022-03-21-12-36-39.png]
title: Records
created: '2022-03-21T15:30:44.936Z'
modified: '2022-03-21T16:44:44.670Z'
---

# Records

## Fixed v Variable length records
Records are rows in a table, coumns are fields
Fixed length records have the same size [^1]
Variable length has different sized records [^2]
Vriable length definex a maximum and can save space when less than max is utilized
To determine type, look at DB table schema/CREATE table statement, if the variables are fixed size then its fixed, otherwise variable
varchar2(30) by definition, varchar is variable length with a cap in size, therefore the whole record will be variable.
Table of fixed and variable data types [^3]

## File storage
File data is split into fixed block size, and are sequential.

### Representing Tuples
All fields are aligned with 4 or 8 byte boundaries and concatenated
Each record has a header holding some information
Each column/variable MUST BE MULTIPLE OF N, if name(30) the system adds 2 more bytes to make it 4 byte aligned and 8 byte aligned
Columns must start on a byte that is a multiple of N
Alignments mean they add bytes to make it a multiple of 4, 8 or 16 depending on setup

#### Headers
Holds metadata information such as pointer to schema information, length of record/tuple, timestamp etc.

## Packing records into blocks
Start with block header
- timestamp of last modified/accessed
- links to next and previous block
- **info about record offsets**

Followed by sequence of records
May end with unused space
Records cannot be cut across multiple blocks

### Accessing Fixed-Length records
First step - get the block in memory
Then the block header will be checked by DBMS, looking for record 2, and theres more than 1 record, valid
Then figure out where the record is stored, DBMS knows size of headers
The record is fixed length records, can determine exactly how many bytes to skip to reach a record
header + record size*# of skips
To get specific columns, the DBMS knows the schema of the table, and can skip over the correct number of bytes to reach a column
If the variable is padded to be byte aligned, then only the correct number of bytes are read and the empty n bytes are skipped

### Accessing Variable Length records
More complex than fixed records
Header of Variable length records
- Record header holds the record length, fixed records do not have to but may
- Variable fields starting byte is stored in header
- All fixed length variables are placed at the beginning of the record, and all variable are at end
- Byte alignment is also included
- Header contains offset of every variable length column EXCEPT for the first, since it can be easily determined

### Calculating records/block
Fixed record
Record size r, block size b
Floor(b*1024/r) = 12
records cannot span across 2 blocks

Variable record, we can only estimate a range

## Packing Records into Blocks
- Packed approach
- BitMap/Unpackeed
- Variable Length Slot Directory

### Packed Approach
will only work for fixed length records
Block is divided into slots, size is equla to record size
Slot is ready to be occupied by a record
Keep block header info
Record 1 goes to slot 1, record 2 to slot 2, and so on
Check if there is space by checking if there are empty slots, counter is incremented to keep track of the next unused slot
Record ID is a unique identifier (Block ID, slot #)
Block id is track and sector location, slot # is the slot that the record is on
Delete operation, move last record and put it in the deleted record's place, decrement N
Record ID changes, not good, record ID may be stored in other places creating disparities
Don't change record ID  
Limitations
- only fixed
- deletion changes record ID

### BitMap/unpacked
Allow empty spaces between slots, need to keep track of which slot has data
Record/slot header has bitmap, 0 is empty, 1 is full
Insertion, put a record in an empty space (0), increment N and set bit to 1
Update, is easy
Deletion, go to N and decrement, go to bitmap and flip N bit to 0
Limitations
- better, but wastes space
- fixed length

Major issue: variable length records

### Variable Length
Keep track of number of records N
Header is at bottom, data starts at top
Header contains slot arrray
Record then starts at byte 0, slot in header holds start for each record
Header says there is 1 record that starts at byte 0, then we cna jump straight to the record
RID = (Block ID, Slot number in array), block I slot N, check array index 1 for offset
Record ID will not change [^4]

Updating record can be problematic, record size could change
Move record to another place in the block, update offset in slot array. ID stays the same
If there is no more space in the block, then the DBMS is forced to move the record to another block, therefore changing the ID




[^1]: ![](@attachment/Clipboard_2022-03-21-11-35-08.png)
[^2]: ![](@attachment/Clipboard_2022-03-21-11-36-00.png)
[^3]: ![](@attachment/Clipboard_2022-03-21-11-38-06.png)
[^4]: ![](@attachment/Clipboard_2022-03-21-12-36-39.png)





































