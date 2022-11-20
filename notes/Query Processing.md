---
attachments: [Clipboard_2022-04-24-20-42-40.png]
tags: [DBII]
title: Query Processing
created: '2022-04-25T00:05:43.054Z'
modified: '2022-04-25T01:15:56.520Z'
---

# Query Processing

Most DBMS apply top down 

## Relational Algebra
σ : select
π : project
x : cartesian product
ρ : rename
`<-` : arrow signifies renaming column
⋈ : theta join (R ⋈c S = σc(RXS))
δ : delete duplicates
γ : grouping

A - B : tuples that are in A and not B
A ∩ B : tuples that are in both A and B (and)
A ∪ B : tuples in either
A x B : combines relations
π a(B) : selects column given predicate (author)
ρ x(E) : renames relation


### Selection
| A | B | C |
|---|---|---|
| 1 | 2 | 5 |
| 3 | 4 | 6 |
| 1 | 2 | 7 |

σ(c >= 6)(R) (rows where column C >= 6)
| A | B | C |
|---|---|---|
| 3 | 4 | 6 |
| 1 | 2 | 7 |

### Projection
| A | B | C |
|---|---|---|
| 1 | 2 | 5 |
| 3 | 4 | 6 |
| 1 | 2 | 7 |

π(A, B)(R) (tuples from column A, B)
| A | B |
|---|---|
| 3 | 4 |
| 1 | 2 |

### Cartesian Product
R
|A|B|
|-|-|
|1|2|
|3|4|

S
|C|D|
|-|-|
|5|6|
|7|8|

RxS
|A|B|C|D|
|-|-|-|-|
|1|2|5|6|
|1|2|7|8|
|3|4|5|6|
|3|4|7|8|


![](@attachment/Clipboard_2022-04-24-20-42-40.png)


## Two Pass Algorithms
First pass - do a prep and write intermediate to disk
second pass - read from disk and compute final result

sort based algorithms
first pass does a sort
second pass relies on sort, and can be pipelined

hash based algorithms
partitino input relation
will work on each partition seperately

compared to single pass
more I/Os, handles larger relateions



















