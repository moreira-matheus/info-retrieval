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

### Variable Byte Encoding

Prefix codes: UTF-8

<img src="./imgs/utf8.png" width="500">

Variable byte encoding (8 bit packets)

<img src="./imgs/variable-byte-encoding.png" width="500">

Compromise:

<img src="./imgs/compromise-vbe.png" width="500">

### Gamma encoding

Unary code

<img src="./imgs/unary-code.png" width="500">

Gamma encoding

<img src="./imgs/gamma-encoding.png" width="500">

First integers:

<img src="./imgs/gamma-first-ints.png" width="500">

More on Gamma encoding [here](https://www.geeksforgeeks.org/elias-gamma-encoding-in-python/).

### Shannon Entropy

Given some probability distribution, what is the *smallest average* number of bits that we can possibly achieve?

**Entropy**:

$$
H(X) = \mathbb{E}\big[I(X)\big] = -\sum_{x \in X(\Omega)} p_X(x) \log_{2} p_X(x)
$$

- $X$: random variable
- $I(X)$: amount of information (number of bits)
- $H(X)$: entropy, or the expected value of the amount of information that is carried by $X$.

Shannon's suggestion: $H(X) = \mathbb{E}\bigg[-\log_{2}\big(p_X(X)\big)\bigg]$

**Expected length of Gamma encoding (for any distribution)**:

$$
\mathbb{E}[L_{\gamma}(X)] \leq 3H(X) = 3\mathbb{E}[I(X)]
$$