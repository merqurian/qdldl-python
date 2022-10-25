# qdldl-python

![github actions](https://github.com/oxfordcontrol/qdldl-python/workflows/Build/badge.svg?branch=master)

Python interface to the [QDLDL](https://github.com/oxfordcontrol/qdldl/)
free LDL factorization routine for quasi-definite linear systems: `Ax =
b`.


## Building
Only success so far has been building on linux. To do so: 

1. clone https://github.com/osqp/qdldl and build it
2. copy that directory under `c`
3. run python -m build -w


## Installation

This package can be directly installed via pip,

```
pip install qdldl
```

## Usage

Initialize the factorization with

```
import qdldl
F = qdldl.Solver(A)
```

where `A` must be a square quasi-definite matrix in [scipy sparse CSC
format](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csc_matrix.html).

The algorithm internally converts the matrix into upper triangular format. If `A` is already upper-triangular, you can specify it with the argument `upper=True` to the `qdldl.Solver` constructor.

To solve the linear system for a right-hand side `b`, just write

```
x = F.solve(b)
```

To update the factorization without changing the sparsity pattern of `A` you can run

```
F.update(A_new)
```

where `A_new` is a sparse matrix in CSR format with the same sparsity pattern as `A`.

The algorithm internally converts `A_new` into upper triangular format. If `A_new` is already upper-triangular, you can specify it with the argument `upper=True` to the `F.update` function.

