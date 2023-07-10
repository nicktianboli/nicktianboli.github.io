---
layout: post
math: true
author: Tianbo Li, Min Lin
---


### Hohenburg-Kohn Theorems
It can be seen that the density functionals significantly reduce the computaional complexity in many ways, but the question is, did the single electron density tell you all needed for calculating the ground state energy of a many-body quantum system. A short answer is yes. The following Hohenburg-Kohn theorems state the relation between ground state energy and the electron density.
 
 
> <span style="color:#AF2406"> Theorem 1. The ground-state energy and all other ground-state electronic properties are uniquely determined by the electron density. </span>

> <span style="color:#AF2406"> Theorem 2. For a trial density function $n'(\boldsymbol r)$, the energy functional $E[n'(\boldsymbol r)]$ cannot be less than the true ground-state energy of the molecule. </span>

Hohenburg-Kohn theorems tell that the ground-state energy of a quantum system is an one-to-one mapping to its density $n(\boldsymbol r)$, which enable the application of density functional theory.


### Constrained Search Form

As Hohenburg-Kohn theorem tells us the existence of such functional $E$ such that $E(n(r))$ is the energy of the system. We can then search for the density that minimizes this energy to find the ground state. 

$$
\min_{n(r)} E(n(r))
$$

However, the exact form of $E$ is not generally available. The constrained search form give an exact definition:

$$
\begin{align}
\min_{n(r)} &\min_{\Psi}\left<\Psi|H|\Psi\right>\\
s.t.& \quad N\int_{r_2,\cdots,r_n}\Psi^2(r)=n(r_1)
\end{align}
$$

Namely, $E$ itself is an optimization that finds the minimum energy, given the density $n(r)$ is known before hand.


### Kohn-Sham DFT

First let's see the conclusion, the functional can be separated into a few terms,

$$
E(n)=T(n)+E_{ext}(n)+E_H(n)+E_{xc}(n)
$$

This is possible only if we make certain assumptions on the wave function. Because otherwise the kinetic energy will be dependent on the wave function $\Psi$ instead of the density $n$.

This key assumption is that the electrons are non-interacting. Kohn-Sham DFT assumes non-interacting particles that has orthogonal wave functions. If we use Slater determinant to construct the many body wave function, it is as follows.

$$
\Psi(\mathbb{x})=\frac{1}{\sqrt{n!}}\sum_{\pi}\sigma(\pi)\prod_i^n\phi_i(x_{\pi[i]})
$$
Note that in Kohn-Sham DFT, the $\phi$-s are subject to,
$$
\left<\phi_i|\phi_j\right>=\delta_{i,j}
$$

#### Kinetic Energy
Applying the Kinetic part of Hamiltonian on $\Psi$

$$
\begin{align}
-\nabla^2\Psi(\mathbb{x})&=
-\frac{1}{\sqrt{n!}}\sum_\pi\sigma(\pi)\sum_{j=1}^n\prod_{i\neq{j}}^n\phi_{\pi^{-1}(i)}(x_{i})\nabla^2\phi_{\pi^{-1}(j)}(x_{j})
\end{align}
$$

Kinetic Energy is

$$
\begin{align}
\int\Psi^*(\boldsymbol{x})\hat{T}\Psi(\boldsymbol{x})d\boldsymbol{x}&=-\frac{1}{2}\int\Psi^*(\boldsymbol{x})\nabla^2\Psi(\boldsymbol{x})\\
&=-\frac{1}{2}\frac{1}{N!}\sum_{\pi}\sigma^2(\pi)\sum_{j}^N\int\phi^*_{\pi^{-1}(j)}(x_j)\nabla^2\phi_{\pi^{-1}(j)}(x_j)dx_j\prod_{i\neq{j}}^n\int_{x_{i}}\phi_{\pi^{-1}(i)}^2(x_{i})dx_i\\
&=-\frac{1}{2}\frac{1}{N!}\sum_{\pi}\sum_{j}^N\int\phi^*_{\pi^{-1}(j)}(x_{j})\nabla^2\phi_{\pi^{-1}(j)}(x_j)dx_j\\
&=-\frac{1}{2}\frac{1}{N!}N!\sum_j^N\int\phi^*_j(x)\nabla^2\phi_j(x)dx\\
&=-\frac{1}{2}\sum_{j=1}^N\int\phi^*_j(x)\nabla^2\phi_j(x)dx\\
&=\sum_j^N\hat{T}_j
\end{align}
$$

Which is equal to sum of per particle kinetic energy.

#### Electron-Electron Repulsion Energy

$$
\begin{align}
E_{ee}&=\int_\mathbb{x} p(\mathbb{x})\sum_{a<b}\frac{1}{|x_a-x_b|}\\
&=\frac{1}{2}\int_\mathbb{x}\Psi^2(\mathbb{x})\sum_{a\neq b}\frac{1}{|x_a-x_b|}\\
&=\frac{1}{2}\frac{1}{n!}\int_\mathbb{x}\sum_{\pi,\pi'}\sigma(\pi)\sigma(\pi')\prod_j^n\phi^*_{\pi^{-1}(j)}(x_j)\prod_k^n\phi_{\pi'^{-1}(k)}(x_k)\sum_{a\neq b}\frac{1}{|x_a-x_b|}
\end{align}
$$

For terms with $\pi$ and $\pi'$ such that $\pi^{-1}(j)\neq \pi'^{-1}(j)$ for any $j\not\in\{a,b\}$, the integration will be zero.

**Two terms are left**, 

**first term** where $\pi=\pi'$

$$
\begin{align}
&\frac{1}{2n!}\int_\mathbb{x}\sum_{\pi}\prod_j^n\phi^2_{\pi^{-1}(j)}(x_j)\sum_{a\neq b}\frac{1}{|x_a-x_b|}\\
=&\frac{1}{2n!}\sum_{\pi}\sum_{a\neq b}\int_{x_a,x_b}\phi^2_{\pi^{-1}(a)}(x_a)\phi^2_{\pi^{-1}(b)}(x_b)\frac{1}{|x_a-x_b|}\\
=&\frac{1}{2}\sum_{a\neq b}\int_{x_1,x_2}\phi^2_{a}(x_1)\phi^2_{b}(x_2)\frac{1}{|x_1-x_2|}
\end{align}
$$

We can also rewrite it as,

$$
\begin{align}
&\frac{1}{2}\int_{x_1,x_2}\sum_{a,b}\phi^2_{a}(x_1)\phi^2_{b}(x_2)\frac{1}{|x_1-x_2|}-\sum_{a}\phi^2_{a}(x_1)\phi^2_{a}(x_2)\frac{1}{|x_1-x_2|}\\
=&\frac{1}{2}\int_{x_1,x_2}\rho(x_1)\rho(x_2)\frac{1}{|x_1-x_2|}-\sum_{a}\phi^2_{a}(x_1)\phi^2_{a}(x_2)\frac{1}{|x_1-x_2|}
\end{align}
$$


**Another term** is when $\pi$ and $\pi'$ differs by swapping $a$ and $b$.

$$
\begin{align}
&-\frac{1}{2}\sum_{a\neq b}\int_{x_1,x_2}\phi^*_{a}(x_1)\phi^*_b(x_1)\phi_{a}(x_2)\phi_{b}(x_2)\frac{1}{|x_1-x_2|}\\
=&-\frac{1}{2}\int_{x_1,x_2}\sum_{a,b}\phi^*_{a}(x_1)\phi^*_b(x_1)\phi_{a}(x_2)\phi_{b}(x_2)\frac{1}{|x_1-x_2|}+\sum_{a}\phi^2_{a}(x_1)\phi^2_{a}(x_2)\frac{1}{|x_1-x_2|}
\end{align}
$$

Note that the second terms cancel each other.

Therefore,

$$
\begin{align}
&\frac{1}{2}\int_{x_1,x_2}\rho(x_1)\rho(x_2)\frac{1}{|x_1-x_2|}-\sum_{a,b}\phi^*_{a}(x_1)\phi^*_b(x_1)\phi_{a}(x_2)\phi_{b}(x_2)\frac{1}{|x_1-x_2|}\\
=&\frac{1}{2}\int_{x_1,x_2}\left(\rho(x_1)\rho(x_2)-\left|\sum_{a}\phi^*_{a}(x_1)\phi_{a}(x_2)\right|^2\right)\frac{1}{|x_1-x_2|}
\end{align}
$$

More often, we write 
$$
\begin{align}
\rho_S(x_1,x_2)=&\left(\rho(x_1)\rho(x_2)-\left|\sum_{a}\phi^*_{a}(x_1)\phi_{a}(x_2)\right|^2\right)\\
=&\rho(x_1)\rho_S(x_2|x_1)\\
=&\rho(x_1)\rho(x_2)-h_X(x_2|x_1)\rho(x_1)
\end{align}
$$

where $\rho_S$ is the joint probability of two particle, when the particles are non-interacting.

This term treats the exchange exactly, when the wave function is constructed from Slater determinant of orthonormal orbitals. However, due to the mean field assumption, the correlation is missing. In DFT, this term together with the correlation error are writen as $E_{xc}$.

So finally, we get that

$$
V_{ee}=\underbrace{\int\rho(r_1)\rho(r_2)\frac{1}{|r_1-r_2|}}_{E_H}+\underbrace{\int-\rho(r_1)h_X(r_2|r_1)\frac{1}{|r_1-r_2|}}_{E_X}
$$


#### Exc and LDA
A simple exchange energy density approximation is the local density approximation (LDA)


$$E_{\rm x}^{\mathrm{LDA}}[n] = - \frac{3}{4}\left( \frac{3}{\pi} \right)^{1/3}\int n(\mathbf{r})^{4/3}\ \mathrm{d}\mathbf{r}$$


### Density functionals
<img src=https://i.imgur.com/I9SP2Lj.png alt="drawing" width="600"/>

Unlike the wave functional methods, DFT methods utilize the marginal electron density $n(\boldsymbol r)$ as input, and derive all kinds of functionals for approximating the ground state energy. A typical method computes the ground state energy in the following manner:
\begin{equation}
E[n(\boldsymbol r)] = \underbrace{E_{kin}[n(\boldsymbol r)]}_{\text{kinetic energy} \\  \text{functional}}+ \underbrace{E_{ext}[n(\boldsymbol r)]}_{\text{external potential} \\  \text{energy functional}} + \underbrace{E_{ele}[n(\boldsymbol r)]}_{\text{electron repulsion} \\  \text{energy functional}} +\underbrace{E_{xc}[n(\boldsymbol r)]}_{\text{exchange-correlation} \\  \text{energy functional}} 
\end{equation}

One of the earliest schemes for the density functional is the **Thomas-Ferimi method**. Each component can be defined by,
\begin{align}
E_{TF}:&= E_k[n(\boldsymbol r)] + E_{xc}[n(\boldsymbol r)] \\
&=\dfrac{3}{10}(3\pi^2)^{2/3} \int n(\boldsymbol r)^{5/3}d\boldsymbol r \\
E_{ext}&= \int n(\boldsymbol r) v_{ext}(\boldsymbol r) d\boldsymbol r\\
E_{ele}&= \dfrac12\int \int \dfrac{n( \boldsymbol r)n( \boldsymbol r')}{|\boldsymbol r - \boldsymbol r'|} d\boldsymbol r d \boldsymbol r'.
\end{align}
>




### Kohn-sham equation
In VMC and other many body wave function methods, the wave function often takes a 3N- or 4N-dimensional variable as input, which results in an expensive compututation load. Kohn-sham methods, equation is defined by,
\begin{align}
    \left(  -\dfrac{1}{2}\nabla ^2 +  v_{eff}(\boldsymbol{r})  \right) \psi_i (\boldsymbol{r}) =  \varepsilon \psi_i(\boldsymbol{r} )
\end{align}

where $v_{eff}(\boldsymbol{r})$ is the effective potential defined by,
$$
\begin{align}
v_{eff}(\boldsymbol{r})  = v_{ext}(\boldsymbol{r}) + \int d^3 \boldsymbol{r}' \dfrac{n(\boldsymbol{r}')}{\vert \boldsymbol{r} - \boldsymbol{r}'\vert}  + v_{xc}(\boldsymbol{r}),
\end{align}
$$
and
\begin{align}
    n(\boldsymbol{r}) = \sum_{i=1}^{N}\big\vert{\psi_i(\boldsymbol{r} )}\big\vert^2,
\end{align}
in which $N$ is the total number of electrons.

#### Non-interacting electrons

![](https://i.imgur.com/pRV5u0H.png)

#### Optimization
##### Self-consistency Field method.
![](https://i.imgur.com/oxsMIQy.png =500x)

The total energy of kohn-sham equation with respect to single particle wave function can be expressed as
\begin{align}
E_{gs} &  %\sum_i^N \min_{\psi_i} \langle \psi_i |\hat h_i |\psi_i \rangle \\
=\sum_i^N \min_{\psi_i} \Big\{ -\int \psi_i(\boldsymbol{r}) \left( \dfrac12\nabla^2 \psi_i(\boldsymbol{r}) \right) d\boldsymbol{r} - \int v_{ext}(\boldsymbol{r}) |\psi_i(\boldsymbol{r})|^2 d\boldsymbol{r} \\
& +  \dfrac12\int \int  \dfrac{|\psi_i(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'  + \int v_{xc}\big(\{\psi_j(\boldsymbol{r} )\} \big) |\psi_i(\boldsymbol{r})|^2 d\boldsymbol{r}
\Big\}
\end{align}
Let $s$ denote the single-particle energy:
\begin{equation}
s(\psi_i) :=  -\int \psi_i(\boldsymbol{r}) \left( \dfrac12\nabla^2 \psi_i(\boldsymbol{r}) \right) d\boldsymbol{r} -  \int v_{ext}(\boldsymbol{r}) |\psi_i(\boldsymbol{r})|^2 d\boldsymbol{r} + \int v_{xc}(\boldsymbol{r}) |\psi_i(\boldsymbol{r})|^2 d\boldsymbol{r}
\end{equation}
and then the total energy can be simplified as
\begin{align}
E &=   \sum_i^N \min_{\psi_i}  \left\{ s(\psi_i) +\dfrac12 \int \int  \dfrac{|\psi_i(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'   \right\} \\
&= \sum_i^N \min_{\psi_i}  \left\{ s(\psi_i) + \int \int  \dfrac{|\psi_i^{\text{old}}(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'  - \int \int  \dfrac{\left( |\psi_i^{\text{old}}(\boldsymbol{r})|^2  -\dfrac12 |\psi_i(\boldsymbol{r})|^2\right)|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'  \right\} \\
\end{align}

#### Updating $\psi_i$ in the Kohn-Sham Equation.
The Kohn-Sham Equation is minimizing:
\begin{align}
\sum_i^N \min_{\psi_i}  \left\{ s(\psi_i) + \int \int  \dfrac{|\psi_i^{\text{old}}(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}' \right\} 
\end{align}

It suffices to see that when update $\psi_i$ the reminder term does not increase. Let $\psi_i^{\text{old}}$ be fixed, we have

\begin{align}
&\int \int  \dfrac{\left(|\psi_i^{\text{old}}(\boldsymbol{r})|^2  -\dfrac12 |\psi_i(\boldsymbol{r}')|^2\right)|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'  \\
=& - \dfrac12 \int \int  \dfrac{ \left(|\psi_i^{\text{old}}(\boldsymbol{r})|^2 -|\psi_i(\boldsymbol{r}')|^2\right)^2 }{\vert \boldsymbol{r}-\boldsymbol{r}' \vert }d\boldsymbol{r}d\boldsymbol{r}' + \text{Const}
\end{align}
It can be seen that when updating $\psi_i$ with $\psi_i^{\text{old}}$ fixed, the above term will always be negative. 

#### Updating $\psi^{\text{old}}_i \leftarrow \psi_i$ .
Obviously the reminder term become zero, and $s(\psi_i)$ does not change as we update  $\psi^{\text{old}}_i$, we only need to prove that 
\begin{align}
\int \int  \dfrac{|\psi_i^{\text{old}}(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}' \leqslant \int \int  \dfrac{|\psi_i(\boldsymbol{r})|^2|\psi_i(\boldsymbol{r}')|^2}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert}d\boldsymbol{r}d\boldsymbol{r}'.
\end{align}

We can see that this is acutally a similarity measure between two density functions:
\begin{equation}
D(n^{\text{old}}, n) := \mathbb{E}_{\boldsymbol{r}\sim n^{\text{old}}} \mathbb{E}_{\boldsymbol{r}'\sim n} \left[\dfrac{1}{\vert \boldsymbol{r}-\boldsymbol{r}' \vert} \right] 
\end{equation}

Therefore, the above similarity measure reach maxima when $n^{\text{old}} = n$.


### Learning orthonormal wave functions
#### Basis set
![](https://i.imgur.com/XdyShhO.png)


One of the most commonly-used basis function is the Gaussian-type orbitals (GTO). A Gaussian basis centered at $\boldsymbol{r}'= (x', y', z')^\top$ of order $l, m, n$ is defined by,
\begin{equation}
    g_{l, m, n}(\boldsymbol{r}; \zeta, \boldsymbol{r}') = c(x-\boldsymbol{r}'_x)^l(y-\boldsymbol{r}'_y)^m(z-\boldsymbol{r}'_z)^n e^{-\zeta\Vert \boldsymbol{r}-\boldsymbol{r}'\Vert^2}
\end{equation}
with normalization constant:
\begin{equation}
    c = \left(  \dfrac{2\zeta}{\pi} \right)^{\frac34} \left( \dfrac{(8\zeta)^{l+m+n} l!m!n! }{(2l)!(2m)!(2n)!}\right)^{\frac12}
\end{equation}



##### Atomic orbitals.
Atomic orbitals is defined by a linear combination of Gaussian basis:
$$
\phi_k(x) = \sum_i c_{ki} g_i
$$
where the parameter of the Gaussian basis and $c_{ki}$ can be loaded from the basis sets.

##### Molecular orbitals.
Molecular orbitals is also a linear combination of atomic orbitals (LCAO):
$$
\psi_j(x) = \sum_k^N \alpha_{jk} \phi_k(x)
$$
and $\alpha_{jk}$ are the paramters that need to be learned.

Here we introduce a vectorized notation
$$
\begin{align}
\boldsymbol \Psi = (\psi_1, \psi_2, \cdots, \psi_N)^\top :&= A \boldsymbol (\phi_1, \phi_2, \cdots, \phi_N)^\top \\
:&= A \boldsymbol \Phi
\end{align}
$$

#### Orthogonalization
The molecular orbitals must satisfy the orthogonal condition.

$$\langle\psi_i|\psi_j\rangle=\delta_{ij}.$$

However, the Gaussian-type basis many not be orthogonal, ie. 

$$
|\boldsymbol \Phi \rangle \langle \boldsymbol \Phi |  \neq \boldsymbol I
$$

Therefore we need to apply a PCA-like methods to get orthogonal orbitals.

Denote $\boldsymbol B := |\boldsymbol \Phi \rangle \langle \boldsymbol \Phi |$, and apply eigen-decomposition we have:
$$
U\Sigma U^\top = \boldsymbol B
$$

Let
$$
D = U^\top \Sigma^{-1/2}
$$

Thus
$$
D^\top D = B^{-1}
$$

Then it can be seen that:
$$
 |\boldsymbol \Psi \rangle \langle \boldsymbol \Psi | = A \boldsymbol B A^\top
$$


Therefore, if A is an orthogonal matrix, then the wave functions are orthogonal.

Let $Q,R=\mathrm{QR}(\Theta)$, where $\Theta$ is a trainable paramter. Since QR decomposition is differentiable, it is possible to use $A$ to calculate the energy, and pass the gradient to $\Theta$.

<!-- 
In DFT methods, $\psi$ is represented a weighted sum of analytical basis functions $\{g_i\}$.
$$\psi_i(x)=\sum_kW_{ik}g_k(x)$$

where $W_{ik}$ is the $\{i,k\}$th element in the matrix $W$. Let $B_{k,k'}=\langle g_k|g_{k'}\rangle$, 
$$\langle\phi_i|\phi_j\rangle=\delta_{ij}=\int_x\sum_{k,k'}W_{ik}b_k(x)W_{jk'}g_{k'}(x)=W_iBW_j^\top$$

Namely, we need to constrain $WBW^\top=I$. If we perform cholesky decomposition $B=LL^\top$, it becomes $WL(WL)^\top=I$. Therefore, we can parameterize $W$ with parameter matrix $\Theta$, let $Q,R=\mathrm{QR}(\Theta)$, then $W=QL^{-1}$. Since QR decomposition is differentiable, it is possible to use $W$ to calculate the energy, and pass the gradient to $\Theta$. -->


#### Numerical integration
In the implementation of DFT, the integrals are computing via numberical methods such as Gaussian quadrature or monte carlo intergration. 

##### Gauss Quadrature
Suppose we have a polynorminal function:
$$
f(x) = \sum_n c_n x^n
$$

We would like to know the following integral:
$$
\int_{-1}^{1} f(x) dx \approx \sum_i w_i f(x_i) 
$$

The question is that, how can we find a set of points $\{ x_i \}$  and a set of weights $\{ w_i \}$ such that the above summation will be close enough to the integral? 

We can see that the LHS of the above equation can be written as,
$$
\int_{-1}^{1} f(x) dx =  \sum_n c_n \int_{-1}^{1} x^ndx 
$$

The RHS can be written as,
$$
\sum_i w_i f(x_i) = \sum_i w_i  \sum_n c_n x_i^n = \sum_n c_n  \sum_i w_i x_i^n
$$

Therefore, the following equation must holds for each $n$.
$$
\int_{-1}^{1} x^ndx = \sum_i w_i x_i^n
$$

Apparently the integral of LHS can be easily obtained by analycial integration, and hence we have a system of equations with 2m parameters:
\begin{align}
    w_1 + w_2 + \cdots + w_k &= 0\\
    w_1x_1+ w_2x_2 + \cdots + w_kx_k &= 0 \\
    w_1x_1^2 + w_2x_2^2 + \cdots + w_kx_k^2 &= \dfrac23 \\
     w_1x_1^3 + w_2x_2^3 + \cdots + w_kx_k^3 &= 0 \\
     \vdots
\end{align}

Solving the above equation we can get $\{w_i\}$ and $\{x_i\}$.

##### Gauss-Legendre Quaduature
The typical Gauss Quaduature requires (2k-1) equations for sovling the system and get the points and associated weights. This can be simplified by using orthogonal basis. 