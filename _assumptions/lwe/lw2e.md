---
title: "Learning with Two Errors (LW2E)"
seo_title: "Learning with Two Errors"
family: "LWE"
graph_id: "LW2E"
assumption_status: "implied"

last_modified_at: 2026-06-30
redirect_from:
  - /learning-with-two-errors/
  - /learning_with_two_errors/
  - /learningwithtwoerrors/
  - /learning-with-2-errors/
  - /learning_with_2_errors/
  - /learningwith2errors/
---

The Learning with two Errors problem was introdcued by Ghosal, Jain, Luo, Sahai, and Vafa in 2025 {% cite EC:GJLSV25 %}. The assumption essentially states [LWE](/lwe/) with a discrete Gaussian error and uniformly chosen secret is hard in the presence of another error term, which is zero with probability $$1-n^{-\delta}$$ and a uniformly random element otherwise.

## Definition

### LW2E$$_{n,m,q,\sigma,\delta}$$ {#lw2e}
_Let $$q$$ be prime and $$\delta \in (0,1)$$. Define the distribution $$\mathcal{S}_{n,q,\delta}$$ s.t. it outputs $$0$$ with probability $$1-n^{-\delta}$$ and a uniformly random element from $$\ZZ_q$$ with probability $$n^{-\delta}$$. Sample $$\mat{A} \sample \ZZ_q^{m \times n}$$, $$\vec{s} \sample \ZZ_q^n$$, $$\vec{e}_1 \sample D_{\ZZ^m, \sigma}$$, $$\vec{e}_2 \sample \mathcal{S}_{n,q,\delta}^m$$, and $$\vec{b} \sample \ZZ_q^m$$. An adversary is asked to distinguish between the distribution_

$$ (\mat{A}, \mat{A} \vec{s} + \vec{e}_1 + \vec{e}_2) \text{ and } (\mat{A}, \vec{b}). $$

## Hardness

Lemma 6.7 in {% cite EC:GJLSV25 %} states that Search-LW2E$$_{n,m,q,\sigma,\delta}$$ is hard if Search-LPN$$_{n,m,q,\delta}$$ or Search-LWE$$_{n,m,q,D_{\ZZ,\sigma}}$$ are hard. Then, Corollary 6.4 states that Decision-LW2E is at least as hard as Search-LW2E. The authors discuss the hardness of LW2E in the presence of LWE and LPN breaking oracles as well as $$\beta$$-CVP oracles further in Section 6.3 and 6.4.

## Constructions built from LW2E {#constructions}

- Public-Key Encryption {% cite EC:GJLSV25 %}

## Related Assumptions

- [Learning with Errors](/lwe/) can be reduced to LW2E.
- [Learning Parity with Noise](/lpn/) can be reduced to LW2E.
