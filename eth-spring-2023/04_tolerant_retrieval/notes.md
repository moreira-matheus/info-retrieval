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

Design choice: [)-intervals

<img src="./imgs/binary-tree-intervals.png">

**Solution 3: B+ tree**

<img src="./imgs/b-plus-tree-example.png">

- All leaves at same depth.
- All non-leaf nodes have between 3 and 5 children. (But it's fine if the root has less.)
- Actual terms (and postings lists) only at the leaves. (Keys in grey only for comparison purposes.) -> Hence, the plus.

B+ trees often have extra leaf pointers:

<img src="./imgs/b-plus-tree-pointers.png">

General case: number of children between $d+1$ and $2d+1$, $d \geq 1$.

- It means, the number of keys is between $d$ and $2d$.

More on B-Trees [here](https://www.tutorialspoint.com/data_structures_algorithms/b_trees.htm) and [here](https://www.cs.usfca.edu/~galles/visualization/BTree.html).

### Wildcards

Tailing wildcard (easier):



<img src="./imgs/tailing-wildcard.png">

Leading wildcard:

<p float="left" align="middle">
    <img src="./imgs/leading-wildcard-1.png" width="250">
    <img src="./imgs/leading-wildcard-2.png" width="250">
    <img src="./imgs/leading-wildcard-3.png" width="250">
</p>

Single-wildcard query:

`Zu*ch` $\rightarrow$ `Zu*` AND `*ch`.

<img src="./imgs/single-wildcard.png">

<u>There might be false positives!</u>

### Permuterm index

<img src="./imgs/permuterm-index.png">

<img src="./imgs/permuterm-index-b-tree.png">