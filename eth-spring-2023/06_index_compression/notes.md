# Index Compression

Notations used in book
- N: number of documents
- T: number of tokens (positional postings)
- M: number of terms (or types, if stemming/lemmtaization)

**Heap's law**

<img src="./imgs/heaps-law.png" width="500">

The number of terms (height of index) grows in the square root of number of tokens in collection.

**Zipf's law**

<img src="./imgs/zipfs-law-1.png" width="500">

<img src="./imgs/zipfs-law-2.png" width="500">

The frequency of terms is inversely proportional to their rank.

### Dictionary compression

Status quo: dictionary (list of terms) as a B+ tree.

**Approach 1**: Array

<img src="./imgs/array.png" width="500">

<u>Issue</u>: terms might exceed 20 bytes.

**Approach 2**: String

<img src="./imgs/string.png" width="500">

**Approach 3**: Blocked Storage

<img src="./imgs/blocked-storage.png" width="500">

**Approach 4**: Front coding

<img src="./imgs/front-coding.png" width="500">

<img src="./imgs/front-coding-2.png" width="500">

### Postings compression

In other words, we want to compress lists of integers.

**Naive approach**: fixed blocks of 4 bytes per integer -> lots of space still.

**Encoding gaps**:

<img src="./imgs/encoding-gaps.png" width="500">


