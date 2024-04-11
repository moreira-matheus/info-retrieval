# Index Construction

### Blocked Sort-Based Indexing (BSBI)

- Divided huge collections into batches.
- Process batches one by one in memory.
    - Parse and read termID-docID pairs into memory.
    - Generate termIDs:
        - Strategy 1: Do a first pass to build term-termID mapping.
        - Strategy 2: On the fly.
    - Sort termID-docID pairs (by docID then termID).
    - Write pairs back to disk (term-termID mapping stays in memory).
- Write back to disk intermediate results.
- Merge intermediate results into final index ([traversal](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)).

Complexity:
- First step (processing): $\mathcal{O}(T\log{}T)$.
- Second step (merging): $\mathcal{O}(T)$.
- Ultimately: $\mathcal{O}(T\log{}T)$.

More [here](https://nlp.stanford.edu/IR-book/html/htmledition/blocked-sort-based-indexing-1.html).

### Single-Pass In-Memory Indexing (SPIMI)

- When processing batches, it already starts building a standard inverted index (instead of only termID-docId pairs).
- It stores the terms in the index (instead of termIDs): no term-termID mapping held in memory.
- In the final merge, "proto" standard inverted index are merged (instead of termID-docId pairs)

Complexity:
- First step (processing): $\mathcal{O}(T\log{}M)$.
- Second step (merging): $\mathcal{O}(T)$.
- Ultimately: $\mathcal{O}(T)$.

More [here](https://nlp.stanford.edu/IR-book/html/htmledition/single-pass-in-memory-indexing-1.html).

### MapReduce

Task 1: Mapping
- The set of all Pokémon is distributed among, say, 10 people, to be counted.

Task 2: Reducing
- Each person is responsible for consolidating the number of a different Pokémon.

More [here](https://www.databricks.com/br/glossary/mapreduce).