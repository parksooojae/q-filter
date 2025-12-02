# QSVT Molecular Hamiltonian Filtering

**QSVT** is an algorithmic framework that, given a block encoding of a matrix, applies polynomial transform `p` to singular values while preserving its singular vectors.

Various quantum algorithms build upon this idea, like Grover's search and Shor's algorithm. QSVT is also applied to several Quantum Machine Learning tasks, including the construction of support matrix machines. 

We seek to explore the setup, implementation details and computational advantages of QSVT in a quantum inspired molecular analysis context. Here we use a molecular Hamiltonian matrix `H` as the input matrix. Conceptually, `H` is a matrix that encodes the electronic structure of a molecule, and it plays the role of the generic data matrix `X` to which the QSVT polynomial filter is applied. In the accompanying code, `H` is constructed from a molecular representation such as a SMILES string, but any procedure that produces a suitable Hamiltonian matrix can be used. This application attempts to apply a quantum inspired polynomial filter to molecular Hamiltonians to extract rich structural features that can improve property prediction and chemical insight. We run this against a classical Chebyshev filter to benchmark runtime performances and quality of information extracted.


QSVT (Quantum Singular Value Transformation) is useful only when the Hamiltonian is large and accessed as an oracle.

Sublinear scaling in matrix dimension (polylog(N))
If a matrix H ∈ ℂⁿˣⁿ is block-encoded efficiently:

classical: applying a polynomial f(H) costs O(N³) (dense) or O(N·nnz) (sparse)

QSVT: applying a degree-d polynomial f(H) costs O(d · polylog N)

This is the fundamental advantage.

Efficient spectral filtering (projectors onto eigenvalue bands)
QSVT can implement:

projectors onto eigenvalue intervals,

high-pass / low-pass spectral filters,

smooth approximations to sign(H),

Fermi–Dirac filters (thermal states).

Classically, this requires diagonalizing huge matrices.

Inverting huge matrices
Quantum linear system solvers (QLSAs) are built on QSVT.

Given a block-encoding of H:

classical: solving Hx=b takes O(N³)

QSVT: inversion with cost poly(log N, κ, 1/ε)

This is exponential in N speedup.

Quantum Gibbs sampling (thermal states)
Classical sampling from:

𝜌 ∝ 𝑒 − 𝛽 𝐻 ρ∝e −βH

is extremely expensive for large N.

QSVT can approximate exp(-βH) using polynomial approximations in poly(log N) time.

No need to store H explicitly
This matters for:

huge periodic systems

tight-binding models with billions of orbitals

graph Laplacians

protein-scale Hamiltonians

QSVT accesses H through a block-encoding oracle, not as a matrix.

Exponentially faster polynomial approximations
Approximating a function f(H) via Chebyshev polynomials:

classical: requires large dense matrix multiplications

QSVT: implemented with O(d) calls to a block-encoded H
