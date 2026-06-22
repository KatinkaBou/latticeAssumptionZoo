---
title: "Algebraic One-More-MLWE (AOM-MLWE)"
seo_title: "Algebraic One-More-MLWE"
family: "LWE"
subfamily: "LWE with Hints"
graph_id: "AOM-MLWE"

last_modified_at: 2026-06-22
redirect_from:
  - /algebraic-one-more-mlwe/
  - /algebraic-one-more-lwe/
  - /a-one-more-mlwe/
  - /a-one-more-lwe/
  - /aom-lwe/
  - /aom-mlwe/
  - /aomlwe/
  - /aommlwe/
---

Algebraic One-More-MLWE (AOM-MLWE) was introduced in 2024 by Espitau, Katsumata, and Takemure {% cite JC:EspKatTak25 %}. Given a MLWE samples (for $$k$$ secrets) and access to an oracle that can solve $$k$$ linear combinations of the secrets/errors, the assumption states that it is still hard to find a MLWE solution for the original inputs (not trivially induced by the queries). It is so hard that even an approximate MLWE solution suffices.  

The non-algebraic version One-More MLWE is not known to be hard, however this algebraic variant has been reduced from standard [MSIS](/sis/#module-sis) and [MLWE](/lwe/#module-lwe) recently by Zhu, and Tessaro {% cite C:ZhuTes25 %}.

## Definition

### Algebraic One-More-MLWE$$_{n,m,q,\mathcal{R},k,(\sigma_{i})_{i\in[k]}, \beta_w,\beta_\vec{s},\beta_\vec{e},\beta_b}$$ {#algebraic-one-more-mlwe}

_Consider the original [MLWE](/lwe/#module-lwe) parameters: let $$q \in \ZZ$$ be an odd prime, $$\mathcal{R} = \ZZ[X] / (X^N + 1)$$, $$\mathcal{R}_q = \ZZ_q[X] / (X^N + 1)$$ and consider the distributions $$\mathcal{D}_i := \mathcal{D}_{\sigma_{i}}.$$_

<ins>*Defining the inputs and the queries:*</ins>
_Let matrix $$\mat{A} \in \mathcal{R}_q^{m \times n}$$, and $$i \in [k]$$, $$\vec{s}_i \leftarrow \mathcal{D}^n_i$$, and $$\vec{e}_i \leftarrow \mathcal{D}^m_i$$. Given the challenge matrix $$\mat{A}$$ and the $$k$$ samples $$\vec{t}_i := \mat{A}\vec{s}_i + \vec{e}_i$$, an adversary chooses $$k-1$$ $$\vec{u}_j$$ and queries for  linear combinations of the secrets: $$\vec{d}_j = \sum_{j\in [k]}\vec{u}_j \cdot \begin{bmatrix} \vec{s}_i \\ \vec{e}_i\end{bmatrix}$$._

<ins>*Checking the queries:*</ins>
_This step is mandatory to avoid trivially induced solutions. First, parse the queries as $$\begin{bmatrix} \mathbf{v}^\top \\ \mat{D}\end{bmatrix} \leftarrow \begin{bmatrix} \vec{d}_1 \| \cdots \| \vec{d}_{k-1}\end{bmatrix}$$ ensuring $$\mat{D} \in \textsf{GL}(\mathcal{R}_q)$$, and define $$\vec{w} = (\vec{v}^\top\mat{D}^{-1})^\top $$.
Then, for all $$i\in [k-1]$$, ensure that $$\|w_i\| \leq \beta_w$$._

<ins>*Outputting a solution:*</ins>
_An adversary is asked to output $$\set{\vec{s}^*_i}_{i \in [k]}$$, $$\set{\vec{e}^*_i}_{i \in [k]}$$ and an approximation $$\vec{b}^*$$ such that:_ 

$$\text{for }i\in[k]: \|\vec{s}^*_i\| \leq \beta_\vec{s}, \|\vec{e}^*_i\| \leq \beta_\vec{e}, \|b^*_i\| \leq \beta_b,\text{ and }b_i\vec{t}_i = \mat{A}\vec{s}_i + \vec{e}_i.$$

## Variants

### (Selective) Algebraic One-More-MLWE$$_{n,m,q,\mathcal{R},k,(\sigma_i)_{i\in[k]}, \beta_w,\beta_\vec{s},\beta_\vec{e},\beta_b}$$ {#selective-algebraic-one-more-mlwe}

The definition is the same as the previous definition except that the $$\vec{u}_j$$ are chosen by the adversary before knowing $$\mat{A}$$.

### Algebraic One-More Uniform-MLWE$$_{n,m,q,\mathcal{R},k,(\sigma_i)_{i\in[k]}, \beta_w,\beta_\vec{s},\beta_\vec{e},\beta_b}$$ {#algebraic-one-more-uniform-mlwe}

The definition is the same as the previous definition except that the $$\vec{s}_i$$ are sampled uniformly from $$\mathcal{R}^n_q$$. In this setup, there is no need to check the bound $$\beta_\vec{s}$$. 

## Hardness

In order to gain confidence in the assumption, the hardness of selective AOM-Uniform was proven by Espitau, Katsumata, and Takemure {% cite JC:EspKatTak25 %}. Despite the hardness is only proven for secrets and errors following discrete Gaussians, Espitau, Katsumata, and Takemure {% cite JC:EspKatTak25 %} reduced AOM-Uniform MLWE to AOM-MLW in both adaptive and selective versions.

The hardness of the adaptive version was later reduced to the dual AOM-MISIS problem in Lemma 7 by Tessaro, and Zhu {% cite C:ZhuTes25 %} improving previously conjectured parameters which is reduced to both [MSIS](/lwe/#module-sis) and [MLWE](/lwe/#module-lwe). This proof, in the adaptive setting, strengthens the use of the assumption in direct application cases.



## Constructions built from Algebraic One-More-MLWE {#constructions}

- Threshold signatures {% cite JC:EspKatTak25 %}{% cite C:ZhuTes25 %}{% cite EPRINT:2026/419 %}

## Related Assumptions

- [Algebraic One-More-ISIS](/aom-misis/) defined the dual version of the assumption over the Inhomegeneous SIS.
- [One-More-ISIS](/om-isis/) defined the (non-algebraic) dual version of the assumption over the Inhomegeneous SIS.
- Algebraic One-More Discrete Logarithm {% cite C:NicRufSeu21 %} inspired Algebraic One-More-MLWE.

<!-- ## Further Reading Suggestions -->

