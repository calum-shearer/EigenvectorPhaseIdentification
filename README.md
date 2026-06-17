# Eigenvalue preparation
In Eigenvalue_Preparation.ipynb we construct `eigenprep(U,d,t,K)` with the following inputs:
- $U$: a $2^n \times 2^n$ diagonal unitary matrix $U$ with $distinct$ eigenvalues $U |x \rangle = e^{2\pi i \varphi(x)}|x \rangle$, where $2^d\varphi(x) \in \mathbb{Z}$ and there exists precisely one eigenvector $|x'\rangle$ with $\varphi(x')=t$.
- $d$: integer such that $2^d\varphi(x) \in \mathbb{Z}$ for all $x$.
- $t$: Desired phase of ouput basis vector.
- $K$: Number of iterations of Grover Search used to find $|x' \rangle$. Defaults to the value maximizing the probability that the search is successful.
  
`eigenprep(U,d,t,K)` outputs a Quantum Circuit that prepares the desired state $|x'\rangle$ satisfying $\varphi(x')=t$ using Grover Search.

The circuit is standard Grover Search, where the Oracle tags the desired state $|x \rangle$ using Quantum Phase Estimation. Therefore we build our circuit in 3 stages:

- Quantum Phase Estimation circuit with $d$ bits of precision.
- Oracle circuit.
- Diffuser circuit.
- Grover circuit (compose Oracle and Diffuser $K$ times).

We also include a function generating a random diagonal of the desired form with specified $t$ and $x$ satisfying $\varphi(x)=t$, along with a function that returns the probability of the success of the Grover Search for such a random diagonal.

We plot $\log_2(\text{Probability of success})$ for $n=d=3 ... 9$, in order to verify that the chance of failure is $O(2^{-n})$ (although the probability of success is not monotone increasing for all $n$). We also include a histogram of outcomes simulated by AerSimulator.