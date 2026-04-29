---
title: "Leaky Learning with Errors"
seo_title: "Leaky-LWE"
family: "LWE"
subfamily: "LWE with Hints"
graph_id: "Leaky-LWE"
assumption_status: "standard"

last_modified_at: 2026-04-29
redirect_from:
  - /leakylwe/
  - /leaky-lwe/
  - /leakymlwe/
  - /leakylwe/
---

Following new works on relaxed versions of [LWE](/lwe/), Lai, Swarnakar, and Woo in {% cite CiC:LaiSwaWoo25 %} introduced the Leaky-LWE assumption with the idea of generalising the classical [LWE](/lwe/) assumption with additional linear information over the secret and/or the error with fewer restrictions than the standard [Hint-MLWE](/hint-mlwe/) and the [Error-Leakage](/hint-mlwe/#). This Leaky-LWE definition encompasses both the previous assumptions.


## Definition

### (Decision) Leaky-MLWE$^{\ell,\chi\_\mathbf{y}, \mathcal{\Gamma}}_{n,m,q,\chi\_\mathbf{s},\chi\_\mathbf{e}}$

We recall the standard [MLWE](/lwe/#module-lwe_nmqchimathcalr) parameters $n, q, m> 0$ with a distribution $\chi$ over $\mathcal{R}^{m+n}$. 
We consider $\ell > 0$ hints each with an associated distribution $\chi\_\mathbf{y}$ over $\\mathcal{R}^{m+n}$ and a set of hint-matrices $\Gamma := \\{ \mat{H} = (\mat{H}\_\mathbf{s},\mat{H}\_\mathbf{e}) \in \mathcal{R}^{\ell \times  n} \times \mathcal{R}^{\ell \times  m}: \\|\mat{H}^\top \mat{H}\\| \leq \beta\\}$.

Consider the original [MLWE](/lwe/#module-lwe_nmqchimathcalr) construction for a random matrix $\mat{A} \leftarrow \mathcal{U}(\mathcal{R}_q^{m\times n})$ and $\mathbf{r} := \begin{bmatrix}\mathbf{s} \\\\ \mathbf{e}\end{bmatrix}$ where $\mathbf{s} \leftarrow \chi\_\mathbf{s}$ and $\mathbf{e} \leftarrow \chi\_\mathbf{e}$. An adversary can select $\ell$ hint-matrices $\mat{H}_i$ knowing $ \mat{A}$, then it is given the associated $\ell$ hints as $\mathbf{z}_i = \mat{H}_i \mathbf{r} + \mathbf{y}_i$, where $\mat{H}_i \leftarrow \Gamma$ and $\mathbf{y}_i\leftarrow \chi\_i$. 

Finally, the adversary is asked to distinguish between the LWE distribution $(\mat{A}, \vec{b} = \mat{A}\vec{s} + \vec{e} \bmod q)$ and a uniformly random distribution over $\mathcal{R}\_q^{m \times n} \times \mathcal{R}\_q^m$ given $\ell$ honest hints $\mat{z}\_i$ and the involved hint-matrices $\mat{H}_i$.

<!-- ## Variants -->

## Hardness

[LWE](/lwe/) to Hint-MLWE when secrets and errors follow Discrete Gaussians Distribution. 

<!-- ## Constructions built from Leaky-MLWE -->

## Related Assumptions

- As presented before, [Hint-MLWE](/hint-mlwe/) is a special instance of LeakyLWE: $\\textsf{Hint-MLWE}^\{\ell,(\chi\_\mathbf{y})\_{i \in [\ell]}, \mathcal{U}(\mathcal{\Gamma})\}\_\{n,m,q,\chi\_\mathbf{s},\chi\_\mathbf{e}\} := \\textsf{Leaky-MLWE}^{\ell,\chi\_\mathbf{y}, \mathcal{\Gamma}}_{n,m,q,\chi\_\mathbf{s},\chi\_\mathbf{e}}$.

<!-- ## Further Reading Suggestions (Optional)

If there are any specific sections in papers, lecture notes, or well-written websites, which provide more insights on this assumption or immediately related topics, can be listed here, e.g.
- [Lecture notes](https://people.csail.mit.edu/vinodv/CS294/){:target="_blank"} by Vinod Vaikuntanathan
  - Lecture 3 on _Smoothing Parameter and Worst-case to Average-case Reduction for SIS_
  - Lecture 10 on _Ideal Lattices and Ring Learning with Errors_ -->
