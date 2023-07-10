---
layout: post
math: true
author: Tianbo Li, Min Lin, Kunhao Zheng
---

### The Bra-ket notation
In quantum mechanics, bra–ket notation, or Dirac notation, is used ubiquitously to denote quantum states. The notation uses angle brackets, \$\displaystyle \langle\$ and \$\displaystyle \rangle\$, and a vertical bar $\displaystyle |$, to construct "bras" and "kets".

A ket is of the form $\displaystyle |v\rangle$. Mathematically it denotes a **vector**, $\displaystyle \boldsymbol {v}$, in an abstract (complex) vector space $\displaystyle V$, and physically it represents a state of some quantum system.

A bra is of the form $\displaystyle \langle f|$. Mathematically it denotes a linear form $\displaystyle f:V\to \mathbb {C}$, i.e. **a linear map** that maps each vector in $\displaystyle V$ to a number in the complex plane $\displaystyle \mathbb {C}$. Letting the linear functional $\displaystyle \langle f|$ act on a vector $\displaystyle |v\rangle$ is written as $\displaystyle \langle f|v\rangle \in \mathbb {C}$.

#### Bras and kets as row and column vectors
In quantum chemistry, the wavefunction $\displaystyle \boldsymbol{\Psi} ( \boldsymbol r)$ is usually represented as vectors:
$$
\begin{equation}
| \boldsymbol{\Psi} \rangle = \sum_{i=1}^N a_i | g_i \rangle,
\end{equation}
$$

where $| \boldsymbol{\Psi} \rangle$ is called a "state vector", and $a_i$ are the coefficients, and $| g_i \rangle$ are the orthogonal **basis** vectors. Then the state vector $| \boldsymbol{\Psi} \rangle$ can be written as a column vector:

$$
\begin{equation}
    | \boldsymbol{\Psi} \rangle=\begin{pmatrix}
    a_1 \\
    a_2\\
    \vdots \\
    a_N
    \\
    \end{pmatrix}
\end{equation}
$$

and the bra notation $\langle \boldsymbol{\Psi} |$ denotes the conjugate transpose of $| \boldsymbol{\Psi} \rangle$, which is,

$$
    \langle \boldsymbol{\Psi} | = (a_1^*, a_2^*, \dots, a_N^*)
$$

The inner product of two state vectors can be written as

$$
\begin{align}
\langle \boldsymbol{\Psi}_a | \boldsymbol{\Psi}_b \rangle &= \int_{-\infty}^{+\infty} \boldsymbol{\Psi}^*_a(\boldsymbol x)\boldsymbol{\Psi}_b( \boldsymbol x)d\boldsymbol{x}\\
&= \int_{-\infty}^{+\infty} \sum_i \sum_j a_ib_j g_i(\boldsymbol{x})  g_j(\boldsymbol{x})  d\boldsymbol{x}   \\
&= \sum_i a_i^*b_i. 
\end{align}
$$

Suppose we have an operator $\hat A$, the **expectation** of $\hat A$ is defined as,

$$
\begin{align}
\langle \hat A \rangle_\Psi := \langle \boldsymbol{\Psi} | \hat A | \boldsymbol{\Psi} \rangle 
=  \int_{-\infty}^{+\infty} \boldsymbol{\Psi}^*(\boldsymbol x) \left( \hat A\boldsymbol{\Psi}( \boldsymbol x) \right) d\boldsymbol{x} 
\end{align}
$$

### Schrodinger Equation
Time-independent Schrödinger equation:

$$
\hat H | \boldsymbol{\Psi} \rangle = \varepsilon | \boldsymbol{\Psi} \rangle
$$

where $\hat H$ is the hamiltonian operator and $\varepsilon$ is the energy. 



>**Example** (Hamiltonian for Hydrogen atom).
>As there is only one electron in a Hydrogen atom, there are three components of the hamiltonian: nuclear kinetic energy,  electronic kinetic energy and the electron-nucleus attraction. Due to the Born-Oppenheimer approximation, the nucleus is much larger and is assumed frozen, the hamiltonian can be simplified as,
> $$\hat H = -\dfrac{1}{2}\nabla^2 - \dfrac{1}{r-R},$$
> where $\nabla^2$ is the Laplacian operator for the kinetic energy, and the second term is the Coulomb potential operator with $r$ and $R$ denote the location of electron and nucleus respectively.

>**Example** (Hamiltonian for water molecule).
>\begin{equation}
\hat H = \underbrace{-\sum_{i=1}^{10}\dfrac{1}{2}\nabla^2_{r_i}}_{\text{Kinetic energy} \\ \text{of electron i}} - \underbrace{\sum_{i=1}^{10} \dfrac{8}{|r_i - R_{O}|}}_{\text{Electron attraction} \\ \text{to the Oxygen atom}}  - \underbrace{\sum_{k=1}^2\sum_{i=1}^{10} \dfrac{1}{r_i-R_{H_k}} }_{\text{Electron attraction to} \\ \text{two Hydrogen atoms}} + \underbrace{ \sum_{i=1}^{10} \sum_{j=1}^{10} \dfrac{1}{r_i-r_j}}_{\text{Electron-electron} \\ \text{repulsion}} + \underbrace{ \sum_{i=1}^{3} \sum_{j=1}^{3} \dfrac{e_ie_j}{R_i-R_j}}_{\text{Nucleus-nucleus} \\ \text{repulsion}} 
\end{equation}


### Wave function 
A wave function in quantum physics is a mathematical description of the quantum state of an isolated quantum system. The wave function is a complex-valued probability amplitude, and the probabilities for the possible results of measurements made on the system can be derived from it.

Wave function tells the probability that a particle will be in the interval $a<r<b$:
$$
P\left( a<r<b \right) = \int_a^b | \Psi(r) |^2 dr.
$$

For an $N$-particle wave funtion $\Psi(r_1, r_2, \cdots, r_N)$, if the particle are indistinguishable, the marginal density can be defined by
$$
n(r) = \int | \Phi(r_1, r_2, \cdots, r_N) |^2 dr_2 \cdots dr_N
$$


The wave function must satisfy two specific conditions:

* **Normalization condition**:
    $$
    \int_{-\infty}^{\infty} |\Psi(r)|^2 dr = 1,
    $$
* **Anti-symmetry condition for fermions**:
    $$\hat P_{12}\Psi(r_1,r_2)= -\Psi(r_2,r_1).$$


### Optimization Objective
In this section, we introduce the problem as a optimization objective and constraints.
Define permutation operator as $(P_{ij}\Psi)(r_1,\cdots,r_i,\cdots,r_j,\cdots)=\Psi(r_1,\cdots,r_j,\cdots,r_i,\cdots)$

$$
\begin{align}
&\min_{\Psi}\langle\Psi|\hat{H}|\Psi\rangle\\
s.t.\;&\langle\Psi|\Psi\rangle=1\\
&P_{ij}\Psi=-\Psi;\;\forall{i,j}
\end{align}
$$

**Objective**: as mentioned above, the hamiltonian consists of multiple terms. The objective we optimize is the overall energy of the system.
**Constraints**: There're two constraints, 1. the square of the wave function has to be a probability density function. 2. The wave function of fermions needs to be anti-symmetric (Pauli exclusion principle).

### Anti-symmetry Constraint

To solve the above optimization problem, we need to optimize the function $\Psi$. From deep learning point of view, we can use a neural network $\hat{\Psi}_\theta(\boldsymbol{r})$. However, don't forget that $\Psi$ need to satisfy the antisymmetry constraint, which the neural network doesn't satisfy.

A general way to construct anti-symmetric wave-functions is through the antisymmetrizer $\mathcal{A}$. Which is defined as 

$$
\Psi_\theta=\mathcal{A}\hat{\Psi}_\theta=\sum_{\pi\in\Pi}(-1)^{\mathrm{inv}(\pi)}\hat{\Psi}_\theta(r_{\pi(1)},r_{\pi(2)},\cdots,r_{\pi(n)})
$$

Therefore, for any function $\hat{\Psi}_\theta$ that is not anti-symmetric, $\Psi_\theta=\mathcal{A}\hat{\Psi}_\theta$ is an anti-symmetric function. Notice that $\Pi$ contains $n!$ permutations, therefore, the calculation of the above $\mathcal{A}\hat{\Psi}_\theta$ is exponential in $n$. 

### Mean field and the Slater determinant 
One simplification in physics is to parameterize $\hat{\Psi}_\theta(r_1,r_2,\cdots,r_n)$ as the product of single particle wave functions. $\hat{\Psi}_\theta(r_1,r_2,\cdots,r_n)=\phi_1(r_1)\phi_2(r_2)\cdots\phi_n(r_n)$. Correspondingly, $\mathcal{A}\hat{\Psi}_\theta$ can be writen as a matrix determinant, which is called the Slater determinant. To simplify the notation, we omit the paramter $\theta$ in $\phi_i(r_j;\theta)$.

$$
\mathcal{A}\hat{\Psi}_\theta=\frac{1}{\sqrt{n!}}\begin{vmatrix}
\phi_1(r_1) & \phi_1(r_2) & \cdots & \phi_1(r_n) \\ 
\phi_2(r_1) & \phi_2(r_2) & \cdots & \phi_2(r_n) \\ 
\vdots & \vdots & \ddots & \vdots \\
\phi_n(r_1) & \phi_n(r_2) & \cdots & \phi_n(r_n)
\end{vmatrix}=|\phi_i(r_j)|
$$


The benefit of the mean field assumption is that the computation of the determinant only takes $O(n^3)$, which is much more efficient than $O(n!)$. However, the problem is that the correlation between particles are missing in the mean field picture. To make the approximator more accurate, usually multiple determinants are introduced, aka

$$
\begin{align}
\Psi_\theta=&\sum_{k=1}^K\gamma_k|\phi_i^k(r_j)|\\
&\sum_k\gamma_k^2=1
\end{align}
$$

When $K$ tends to infinity, the solution is considered as exact.