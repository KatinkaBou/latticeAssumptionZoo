---
title: "Sparse LWE"
seo_title: "Sparse LWE"
family: "LWE"
subfamily: "LWE with Distributional Constraints"
graph_id: "Sparse-LWE"
assumption_status: "standard"

last_modified_at: 2026-05-05
redirect_from:
  - /sparselwe/
  - /sparse_lwe/
  - /sparse-lwe/
---

There exist different definitions of Sparse LWE. In this section, we focus on the Sparse LWE assumption defined by Jain, Lin, and Saha in 2024 {% cite C:JaiLinSah24 %} where the LWE distribution is defined for a sparse matrix $$\mat{A}$$, where each row has a fixed sparsity.  

It is important to understand that Sparse LWE is also defined in the cryptanalysis community where their *sparsity* denotes the sparsity of the secret and/or the error.{% cite EPRINT:2025/1002 %}{% cite EPRINT:2025/1990 %} 
## Definition

### $$k$$-sparse distribution $$\mathcal{S}^\textsf{sparse}_{n,k,q}$$ {#k-sparse-distribution}

The idea is to construct a vector of size $$n$$ where $$k-n$$ coordinates are set to $$0$$, the others are chosen uniformly at random from $$\mathbb{Z}_q$$. In this setup, the output vector has at most $$k$$ non-zero coordinates. 

- Sample a set $$S \subset [n]$$ with $$\vert S \vert = k$$,
- Return $$\vec{v} \xleftarrow{\$} \mathbb{Z}_q^n$$, for all $$i \notin S,$$ set $$v_i = 0$$.

### Sparse LWE$$_{n,m,q,\chi_\mathbf{e},k}$$ {#sparse-lwe}

_Let $$\mat{A} = \begin{bmatrix} \vec{a}_0 \\ \vdots \\ \vec{a}_{m-1} \end{bmatrix}$$ where $$\vec{a}_i \xleftarrow{\$} \mathcal{S}^\textsf{sparse}_{n,k,q}$$. Let the secret vector $$\vec{s} \in \ZZ_q^n$$ be uniformly sampled from $$\ZZ_q$$ and the noise vector $$\vec{e} \in \ZZ_q^m$$ be sampled from the error distribution $$\chi_\mathbf{e}$$. An adversary is asked to distinguish between the Sparse LWE distribution $$(\mat{A}, \vec{b} = \mat{A} \cdot \vec{s} + \vec{e} \bmod q)$$ and elements sampled from $${(\mathcal{S}^\textsf{sparse}_{n,k,q})}^m \times \mathcal{U}(\ZZ_q^m)$$._

## Hardness

The authors reduce LWE$$_{k,m,q,\mathcal{U}(\ZZ_q),\chi_\mathbf{e}}$$ to Sparse LWE$$_{n,m,q,\chi_\mathbf{e},k}$$ for some very restrictive parameter regime: $$q$$ prime and $$m < q$$ (which does not preserve the dimension).

The idea of the proof is to translate the matrix $$\mat{A}$$ to another one with $k$-sparse rows $$\mat{A}'$$ such that $$\mat{A}'\mat{C} = \mat{A}$$. Finally, a new instance $$(\mat{A}',\vec{b}' = \mat{A}'\vec{r} + \vec{b})$$ is constructed, where $$\vec{b}'$$ is either uniform if $$\vec{b}$$ is, or equals $$\vec{b}' = \mat{A}'\vec{s}' + \vec{e}$$ where $$\vec{s}' = \mat{C}\vec{r} + \vec{s}$$ if $$\vec{b}$$ is honestly constructed. 

They also provide some interesting analysis for different choices of $$k$$: choosing $$k =O(1)$$ or $$O(\log n)$$, the associated LWE instance is easy to solve. If $$k = \Theta(n)$$ i.e. too large, then Sparse LWE is not that really sparse and is not truly sparse. 

The original authors also provided some cryptanalysis attempts for other parameter regimes that might be useful in practice. In their Section 7 {% cite C:JaiLinSah24 %}, the authors analyse some attacks exploiting the sparsity in order to better understand the assumption. 

## Constructions built from Spars LWE {#constructions}

- Homomorphic encryption {% cite C:JaiLinSah24 %}

## Related Assumptions

It might be important to understand that Sparse LWE is also defined in the cryptanalysis community where their "sparsity" denotes the sparsity of the secret and/or the error. {% cite EPRINT:2025/1002 %} {% cite EPRINT:2025/1990 %}

