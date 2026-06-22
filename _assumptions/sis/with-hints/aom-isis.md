---
title: "Algebraic One-More-MISIS (AOM-MISIS)"
seo_title: "Algebraic One-More-MISIS"
family: "SIS"
subfamily: "SIS with Hints"
graph_id: "AOM-MISIS"

last_modified_at: 2026-06-22
redirect_from:
  - /algebraic-one-more-isis/
  - /algebraic_one_more_isis/
  - /aomisis/
  - /aommisis/
  - /aom-misis/
  - /aom_misis/
  - /algebraic-one-more-module-isis/
  - /algebraic_one_more_module_isis/
---

Algebraic One-More-MISIS (AOM-ISIS) was introduced in 2025 by Zhu, and Tessaro {% cite C:ZhuTes25 %}, extending the notion of Algebraic One-More Preimage Resistance {% cite EC:TesZhu23 %} for (lattice-based) hash-function. Given $$k$$ [normal-form MSIS](/sis/#normal-form-sis) targets and access to an oracle that can solve $$k$$ linear combinations of the secrets, the assumption states that it remains hard to find a short solution for another bounded linear combination of the inputs, excluding trivial induced solutions.

## Definition

### Algebraic One-More-MSIS$$_{n,m,q,\mathcal{R},k,(\sigma_i)_{i\in[k]}, \beta_w,\beta_\vec{s},\beta_b}$$ {#algebraic-one-more-module-sis}

_Consider the original [MSIS](/sis/#module-sis) parameters: let $$q \in \ZZ$$ be an odd prime, $$\mathcal{R} = \ZZ[X] / (X^N + 1)$$, $$\mathcal{R}_q = \ZZ_q[X] / (X^N + 1)$$ and consider the distributions $$\mathcal{D}_i := \mathcal{D}_{\sigma_{i}}.$$_

<ins>*Defining the input and the queries:*</ins>
_Let matrix $$\mat{A} = \begin{bmatrix} \mat{A}' | \mat{I}_n\end{bmatrix} \in \mathcal{R}_q^{m \times n}$$ (in a normal form), and $$i \in [k]$$, $$\vec{s}_i \leftarrow \mathcal{D}^m$$. Given the challenge matrix $$\mat{A}$$ and the $$k$$ targets $$\vec{t}_i := \mat{A}\vec{s}_i$$, an adversary chooses $$k-1$$ $$\vec{u}_j$$ and queries for linear combinations of the secrets $$\vec{d}_j = \sum_{j\in [k]}\vec{u}_j \vec{s}_i$$._

<ins>*Asserting the queries:*</ins>
_This step is mandatory to avoid trivially induced solutions. The adversary is only allowed to query the oracle for input that are orthogonal to a small non-zero vector $$\vec{w}$$ such that $$\vec{u}_j^\top \vec{w} = 0$$ and $$\|(\frac{w_1}{\sigma_1}, \dots, \frac{w_{k-1}}{\sigma_{k-1}})\| \leq \beta_w$$. The adversary is only allowed to output a valid solution to a linear combination $$\vec{b}^*$$ non-orthogonal to $$\vec{w}$$ i.e $$\vec{b}^{*\top}\vec{w} \neq 0$$._

<ins>*Outputting a solution:*</ins>
_An adversary is asked to output $$\vec{s}^*$$ and an approximation $$\vec{b}^*$$ such that:_ 

$$\|\vec{s}^*\| \leq \beta_\vec{s}, \|(b^*_i \cdot \sigma_1, \dots, b^*_{k-1} \cdot \sigma_{k-1})\| \leq \beta_b, \text{ and }\sum_{i\in[k]}b^*_i\vec{t}_i = \mat{A}\vec{s}^*.$$

## Hardness

The hardness was proven in Theorem 1 by Tessaro, and Zhu {% cite C:ZhuTes25 %} and reduced from the hardness of [MSIS](/sis/#module-sis) and [MLWE](/lwe/#module-lwe) for a judicious choice of parameters. Due to the definition, the hardness is only proven for secrets sampled from discrete Gaussian distributions.

## Constructions built from Algebraic One-More-ISIS {#constructions}

- Threshold signatures {% cite AC:ChaTesZhu24 %}{% cite JC:EspKatTak25 %}{% cite C:ZhuTes25 %}{% cite EPRINT:2026/419 %}

## Related Assumptions

- [Algebraic One-More-MLWE](/aom-mlwe/) defined the dual version of the assumption over the Module LWE.
- [One-More-ISIS](/om-isis/) defined the (non-algebraic) version of the assumption.
- Algebraic One-More Discrete Logarithm {% cite C:NicRufSeu21 %} inspired Algebraic One-More-MSIS.

<!-- ## Further Reading Suggestions -->
