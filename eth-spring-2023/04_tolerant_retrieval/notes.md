# Tolerant Retrieval

### Searching on a postings list

**Solution 1: hash table**

<img src="./imgs/hash-table.png">

Limitations:

- No support for  range queries: `a-c?`.
- Hash function not perfect in real life.
- Space requirements for collision avoidance.

**Solution 2: binary tree**

Binary search tree:

<img src="./imgs/binary-tree.png">

With postings:

<img src="./imgs/binary-tree-postings.png">

Alternative: postings only on leaves:

<img src="./imgs/binary-tree-leaves.png">