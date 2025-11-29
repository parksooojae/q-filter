# QSVT Molecular Hamiltonian Filtering

**QSVT** is an algorithmic framework that, given a block encoding of a matrix, applies polynomial transform `p` to singular values while preserving its singular vectors.

Various quantum algorithms build upon this idea, like Grover's search and Shor's algorithm. QSVT is also applied to several Quantum Machine Learning tasks, including the construction of support matrix machines. 

Here, we explore the setup, implementation details and computational advantages of QSVT in a quantum inspired molecular analysis context.

In this application, we use a molecular Hamiltonian matrix `H` as the input matrix. Conceptually, `H` is a matrix that encodes the electronic structure of a molecule, and it plays the role of the generic data matrix `X` to which the QSVT polynomial filter is applied. In the accompanying code, `H` is constructed from a molecular representation such as a SMILES string, but any procedure that produces a suitable Hamiltonian matrix can be used. This application attempts to apply a quantum inspired polynomial filter to molecular Hamiltonians to extract rich structural features that can improve property prediction and chemical insight. We run this against a classical Chebyshev filter to benchmark runtime performances and quality of information extracted.
