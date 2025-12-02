# QSVT Molecular Hamiltonian Filtering

**QSVT** is an algorithmic framework that, given a block encoding of a matrix, applies polynomial transform `p` to singular values while preserving its singular vectors.

Various quantum algorithms build upon this idea, like Grover's search and Shor's algorithm. QSVT is also applied to several Quantum Machine Learning tasks, including the construction of support matrix machines. 

We seek to explore the setup, implementation details and computational advantages of QSVT in a quantum inspired molecular analysis context. Here we use a molecular Hamiltonian matrix `H` as the input matrix. Conceptually, `H` is a matrix that encodes the electronic structure of a molecule, and it plays the role of the generic data matrix `X` to which the QSVT polynomial filter is applied. In the accompanying code, `H` is constructed from a molecular representation such as a SMILES string, but any procedure that produces a suitable Hamiltonian matrix can be used. This application attempts to apply a quantum inspired polynomial filter to molecular Hamiltonians to extract rich structural features that can improve property prediction and chemical insight. We run this against a classical Chebyshev filter to benchmark runtime performances and quality of information extracted.


---

### **QSVT (Quantum Singular Value Transformation): Why It Matters**

---

### **1. Sublinear scaling in matrix dimension (`polylog(N)`)**

If a Hamiltonian `H` of size `N x N` is efficiently block-encoded:

* **Classical:** applying a polynomial `f(H)` costs

  * `O(N^3)` for dense matrices
  * `O(N * nnz)` for sparse matrices

* **QSVT:** applying a degree-`d` polynomial `f(H)` costs

  * `O(d * polylog(N))`

This is the core asymptotic advantage.

---

### **2. Efficient spectral filtering**

QSVT can implement:

* projectors onto eigenvalue intervals
* high-pass / low-pass filters
* smooth approximations to `sign(H)`
* Fermi–Dirac (thermal) filters

Classically, this usually requires diagonalizing extremely large matrices.

---

### **3. Inverting large matrices (Quantum Linear System Solvers)**

Given a block-encoding of `H`:

* **Classical:** solving `H x = b` costs `O(N^3)`
* **QSVT:** approximate inversion costs

  * `poly(log N, kappa, 1/epsilon)`
    where `kappa` = condition number

This yields an exponential speedup in matrix size `N`.

---

### **4. Quantum Gibbs sampling (thermal states)**

Classically, sampling from the thermal state

```
rho ∝ exp(-beta * H)
```

is extremely costly for large `N`.

QSVT can approximate `exp(-beta * H)` using polynomial methods in
`poly(log N)` runtime.

---

### **5. No need to store H explicitly**

QSVT uses an oracle/block-encoding, not the matrix itself.
This is critical for:

* huge periodic materials
* tight-binding models with billions of orbitals
* graph Laplacians
* biomolecular quantum Hamiltonians

Memory usage stays logarithmic in system size.

---

### **6. Exponentially faster polynomial approximations**

Approximating functions of matrices (e.g., Chebyshev approximations):

* **Classical:** requires large matrix multiplications
* **QSVT:** requires only `O(d)` queries to the block-encoded `H`
  where `d` is the polynomial degree.

---
