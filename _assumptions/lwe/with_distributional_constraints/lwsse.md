---
title: "Learning with Short and Sparse Errors (LWSSE)"
seo_title: "Learning with Short and Sparse Errors"
family: "LWE"
subfamily: "LWE with Distributional Constraints"
graph_id: "LWSSE"

last_modified_at: 2026-06-30
redirect_from:
  - /learning-with-short-and-sparse-errors/
  - /learning_with_short_and_sparse_errors/
  - /learningwithshortandsparseerrors/
---

The Learning with Short and Sparse Errors (LWSSE) problem was introdcued by Ghosal, Jain, Luo, Sahai, and Vafa in 2025 {% cite EC:GJLSV25 %}. It provides a slightly unusual definition of LWE, where the secret is of dimension $$m-n$$ and the error term is sampled sparsely from a discrete Gaussian distribution, i.e. the error term is zero for several coordinates.

## Definition

### LWSSE$$_{n,m,q,\eta,\gamma}$$ {#lwsse}
_Let $$q$$ be prime and $$y \in (0,1)$$. Define the distribution $$\mathcal{E}_{n,m,\eta,\gamma}$$ as a distribution over $$\ZZ$$ which samples $$0$$ with probability $$1-(m-n)^{-\gamma}$$ or a random element from $$D_{\ZZ,\eta}$$ with probability $$(m-n)^{-\gamma}$$. Sample $$\mat{A} \sample \ZZ_q^{m \times (m-n)}$$, $$\vec{s} \sample \ZZ_q^{m-n}$$, $$\vec{e} \sample \mathcal{S}_{n,m,\eta,\gamma}^m$$, and $$\vec{b} \sample \ZZ_q^m$$. An adverary is asked to distinguish between the distribution_

$$ (\mat{A}, \mat{A} \vec{s} + \vec{e}) \text{ and } (\mat{A}, \vec{b}). $$

## Hardness

There are no known reductions to LWSSE. Rather the authors {% cite EC:GJLSV25 %} provide upper bounds on the hardness of LWSSE by reducing it to $$\beta$$-CVP (Lemma 5.20), [LPN](/lpn/) (Lemma 5.15), and [LWE](/lwe/) (Lemma 5.10).
Otherwise, Ghosal et al. {% cite EC:GJLSV25 %} present some cryptanalysis of LWSSE in Section 7 of their paper and show the equivalence of LWSSE to [ISSIS](/issis/) in Lemma 5.5.

## Constructions built from LWSSE {#constructions}

- Public-Key Encryption {% cite EC:GJLSV25 %}

## Related Assumptions

- [Inhomogeneous Short and Sparse Integer Solution](/issis/) is the SIS-version of LWSSE.
