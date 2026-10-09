# Program 3 — Sparse Matrix Representation and Operations (`sparse_matrix.py`)

## Aim
Convert a full matrix to its sparse triple representation and back, and add
two matrices that are already in sparse form — producing a sparse result
without ever reconstructing either input as a full matrix — then display
both the sparse and full forms so they can be compared.

## Logic
A sparse matrix is stored as `{"rows": m, "cols": n, "triples": [...]}`,
where `triples` holds only the non-zero `(row, col, value)` entries in
row-major order (this ordering is what makes the addition trick below
possible). `to_sparse` / `from_sparse` are a straight scan-and-rebuild pair.
`add_sparse` is the interesting part: since both triple lists are already
sorted by `(row, col)`, addition is done with a **two-pointer merge** — the
same idea as the merge step in merge sort. At each step it compares the
current position from each list: whichever position is earlier gets copied
straight to the result, and when both lists are at the same position, the
values are added together (and dropped if they cancel to zero). This never
touches a full `m x n` grid, so the cost scales with the number of non-zero
entries, not with `m * n`.

## Functions
- `to_sparse(matrix)` — full list-of-lists → `{"rows", "cols", "triples"}`
- `from_sparse(sparse)` — rebuilds the full matrix from the triples
- `add_sparse(sparse_a, sparse_b)` — two-pointer merge addition, sparse in and sparse out; validates matching dimensions first
- `menu()` — lets you either convert-and-verify a single matrix, or add two

## Sample Input / Output
Using the worksheet's own matrix D from Section B Q4:

```
D = [[0, 0, 5],
     [0, 8, 0],
     [3, 0, 0],
     [0, 0, 0]]

Sparse form (rows=4, cols=3, non-zero=3):
  (0, 2, 5)
  (1, 1, 8)
  (2, 0, 3)

Reconstructed full form matches original: True
```

Sparse addition, verified against ordinary full-matrix addition on a 6x6
example (four non-zero entries in the result, matching a brute-force
element-by-element sum computed independently):

```
A+B sparse (rows=6, cols=6, non-zero=4):
  (0, 5, 1)
  (1, 1, 10)
  (2, 4, 10)
  (5, 0, 2)
Matches brute-force full addition: True
```

**Boundary case tested:**
- Adding a 1x2 sparse matrix to a 2x1 sparse matrix → `ValueError: Dimension mismatch: 1x2 vs 2x1`

## Note for Section D
This program is the one Section D asks you to run for the space-optimization
comparison — build a >=6x6 matrix that's roughly 80% zero and one that's
under 20% zero, convert both with `to_sparse`, and record `len(triples)`
against the full `rows * cols` count for each.