# Program 4 — Matrix Calculator (`matrix_calculator.py`)

## Aim
A single menu-driven calculator that adds, multiplies, transposes, and finds
the determinant of user-entered matrices, validating dimensions and
squareness before each operation.

## Logic
Addition and multiplication each check shapes before doing any arithmetic —
addition needs identical `rows x cols` on both sides, multiplication needs
`A`'s column count to match `B`'s row count. Multiplication itself is the
textbook triple-nested sum: `result[i][j] = sum(A[i][k] * B[k][j] for k)`.
Determinant is implemented as **recursive cofactor expansion along the first
row**: 1x1 and 2x2 are the base cases, and anything larger repeatedly builds
a "minor" matrix (drop row 0 and the current column) and recurses, alternating
the sign at each step. The worksheet only requires 2x2 and 3x3 to work, but
since the recursive version handles any size for about the same amount of
code, it's implemented generally rather than hard-coded to just those two
cases.

## Functions
- `add_matrices(a, b)` — validates matching shape, element-wise sum
- `multiply_matrices(a, b)` — validates `cols(A) == rows(B)`, standard triple loop
- `transpose(matrix)` — swaps rows and columns
- `is_square(matrix)` — helper used before determinant
- `determinant(matrix)` — recursive cofactor expansion (1x1 base case, 2x2 base case, general case for n > 2)
- `menu()` — interactive loop

## Sample Input / Output
```
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]

A + B          -> [[6, 8], [10, 12]]
A x B          -> [[19, 22], [43, 50]]
Transpose of A -> [[1, 3], [2, 4]]
Determinant(A) -> -2

M3 = [[6, 1, 1], [4, -2, 5], [2, 8, 7]]
Determinant(M3) -> -306   (checked against the known value for this matrix)
```

**Boundary cases tested:**
- Adding a 1x2 and a 1x3 matrix → `ValueError: Cannot add matrices of size 1x2 and 1x3`
- Multiplying a 1x2 by a 1x2 → `ValueError: Cannot multiply 1x2 by 1x2: columns of A must match rows of B`
- Determinant of a non-square (2x3) matrix → `ValueError: Determinant is only defined for square matrices`