# Eigenvalue preparation
We construct a function `eigenprep(U,d,t,K)` with the following inputs:
- $U$: a $2^n \times 2^n$ diagonal unitary matrix $U$ with $distinct$ eigenvalues $U |x \rangle = e^{2\pi i \varphi(x)}|x \rangle$, where $2^d\varphi(x) \in \mathbb{Z}$ and there exists precisely one eigenvector $|x'\rangle$ with $\varphi(x')=t$.
- $d$: integer such that $2^d\varphi(x) \in \mathbb{Z}$ for all $x$.
- $t$: Desired phase of ouput basis vector.
- $K$: Number of iterations of Grover Search used to find $|x' \rangle$. Defaults to the value maximizing the probability that the search is successful.
  
`eigenprep(U,d,t,K)` outputs a Quantum Circuit that prepares the desired state $|x'\rangle$ satisfying $\varphi(x')=t$ using Grover Search.

The circuit is standard Grover Search, where the Oracle tags the desired state $|x \rangle$ using Quantum Phase Estimation. Therefore we build our circuit in 3 stages:

- Quantum Phase Estimation circuit with $d$ bits of precision.
- Oracle circuit
- Diffuser circuit
- Grover circuit (compose Oracle and Diffuser $K$ times)