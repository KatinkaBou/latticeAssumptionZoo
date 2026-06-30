---
title: "Inhomogeneous Short and Sparse Integer Solution (ISSIS)"
seo_title: "Inhomogeneous Short and Sparse Integer Solution"
family: "SIS"
graph_id: "ISSIS"

last_modified_at: 2026-06-30
redirect_from:
  - /inhomogeneous-short-and-sparse-decision/
  - /inhomogeneous_short_and_sparse_decision/
  - /inhomogeneousshortandsparsedecision/
---

The ISSIS assumption was introdcued by Ghosal, Jain, Luo, Sahai, and Vafa in 2025 under the name _Inhomogeneous Short and Sparse Decision_ assumption {% cite EC:GJLSV25 %}. The problem is a sparse variant of [ISIS](/sis/#inhomogeneous-sis) where the solution vector $$\vec{s}$$ does not only have to be short but it has to have low Hamming-weight.

## Definition

### ISSIS$$_{n,m,q,\eta,\gamma,\beta}$$ {#issis}
_Let $$q$$ be prime and $$\gamma \in (0,1)$$. Define the distribution $$\mathcal{E}_{n,m,\eta,\gamma}$$ as a distribution over $$\ZZ$$ which samples $$0$$ with probability $$1-(m-n)^{-\gamma}$$ or a random element from $$D_{\ZZ,\eta}$$ with probability $$(m-n)^{-\gamma}$$. Sample $$\mat{A} \sample \ZZ_q^{n \times m}$$ and $$\vec{r} \sample \mathcal{E}_{n,m,\eta,\gamma}^m$$. Given $$\mat{A}$$ and $$\vec{t} = \mat{A} \vec{r}$$, an adversary is asked to find a short, low Hamming-weight vector $$\vec{s} \in \ZZ^m$$ s.t._

$$ \mat{A} \vec{s} = \vec{t} \land \norm{\vec{s}}_\infty \leq \beta \land \operatorname{hw}(\vec{s}) \leq 2m(m-n)^{-\gamma}. $$

Note that the authors also define a decisional variant of ISSIS, where $$\mat{A} \vec{s}$$ should be distinguished from a uniform distribution over $$\ZZ_q^m$$. They prove that the decisional version is equivalent to the search version in Theorem 5.4.

## Hardness

In Section 5.2 of {% cite EC:GJLSV25 %}, the authors show that ISSIS is equivalent to the [Learning with Short and Sparse Errors](/lwsse/) problem.

## Constructions built from ISSIS {#constructions}

- Public-Key Encryption in combination with [LW2E](/lw2e/) {% cite EC:GJLSV25 %}

## Related Assumptions

- [Learning with Short and Sparse Errors](/lwsse/) is the LWE equivalent of ISSIS.
