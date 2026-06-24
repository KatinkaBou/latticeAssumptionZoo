---
title: "Partial Vandermonde LWE (PV-LWE)"
seo_title: "Partial Vandermonde LWE"
family: "LWE"
graph_id: "PV-LWE"

last_modified_at: 2026-06-24
redirect_from:
  - /pv_lwe/
  - /pvlwe/
  - /partial-vandermonde-lwe/
  - /partial_vandermonde_lwe/
  - /partialvandermondelwe/
---

Partial Vandermonde LWE (PV-LWE) was proposed by Boudgoust, Sakzad, and Steinfeld in 2022 {% cite DCC:BouSakSte22 %} as an LWE alternative to the Partial Vandermonde Knapsack problem (also referred to as _Partial Fourier Recovery Problem_) {% cite ACNS:HPSSW14 %}{% cite ACISP:LuZhaAu18 %}.

## Definition

Before we can define PV-LWE, we need to define some preliminaries.

### Partial Vandermonde Transform$$_{\nu,n,q}$$
_Let $$\set{\omega_j}_{j \in [n]}$$ be the set of primitive $$\nu$$-th roots of unity in $$\ZZ_q$$. We divide the set $$\set{\omega_j}_{j \in [n]}$$ into two disjoint subsets $$\Omega$$ and $$\Omega^c$$ of size $$\abs{\Omega} = t$$ and $$\abs{\Omega^c} = n - t$$. The partial Vandermonde transform matrix $$\bar{\mat{V}}_\Omega \in \ZZ_q^{t \times n}$$ and its complement $$\bar{\mat{V}}_{\Omega^c} \in \ZZ_q^{(n-t) \times n}$$ are given by_

$$ \bar{\mat{V}}_\Omega = 
\begin{bmatrix}
  1 &\omega_{i_1} &\dots &\omega_{i_1}^{n-1} \\
  \vdots &\vdots & &\vdots \\
  1 &\omega_{i_t} &\dots &\omega_{i_t}^{n-1} \\
\end{bmatrix} \text{ and } \bar{\mat{V}}_{\Omega^c} = 
\begin{bmatrix}
  1 &\omega_{i_{t+1}} &\dots &\omega_{i_{t+1}}^{n-1} \\
  \vdots &\vdots & &\vdots \\
  1 &\omega_{i_n} &\dots &\omega_{i_n}^{n-1} \\
\end{bmatrix},
$$

_where $$\omega_{i_j} \in \Omega$$ for $$j \in [t]$$ and $$\omega_{i_{t+k}} \in \Omega^c$$ for $$k \in [n-t]$$._

Define the set $$\mathcal{P}_t := \set{\Omega \subset \set{\omega_j}_{j \in [n]} : \abs{\Omega} = t}$$ of all subsets of primitive $$\nu$$-th roots of unity in $$\ZZ_q$$ of size $$t$$.

### PV-LWE$$_{n,q,\beta,\nu,t,\chi}$$ {#pv-lwe}
_Let $$\chi$$ be a distribution over $$\ZZ^n$$ and fix $$\vec{s} \in \ZZ_q^t$$. Sample $$\Omega \sample \mathcal{U}(\mathcal{P}_t)$$, $$\vec{e} \sample \chi$$, and $$\vec{u} \sample \ZZ_q^n$$. An adversary is asked to distinguish between the distribution_

$$ \left( \bar{\mat{V}}_\Omega, \bar{\mat{V}}_\Omega^T \cdot \vec{s} + \vec{e} \right) \text{ and } \left( \bar{\mat{V}}_\Omega, \vec{u} \right). $$

## Hardness

Boudgoust et al. show that PV-LWE is equivalent to the decision version of PV-Knapsack in Lemma 6 and 7 of {% cite DCC:BouSakSte22 %}.
In subsequent work, Boudgoust, Gachon, and Pellet-Mary {% cite C:BouGacPel22 %} present an efficient distinguisher for some proposed sets of parameters and a polynomial-time distinguisher for the decisional PV-Knapsack problem, which works for random instances of $$\Omega$$ with non-negligible probability. Further, they reduce the bit-security of parameter sets drastically. Further, Das and Joux {% cite EC:DasJou24 %} provide a key recovery attack for a non-negligible (but efficiently identifiable) number of weak keys.

## Constructions built from PV-LWE {#constructions}

- Signatures {% cite ACNS:HPSSW14 %}{% cite ACISP:LuZhaAu18 %}
- Aggregate Signature {% cite EPRINT:DHSS20 %}
- Public-Key Encryption {% cite DCC:BouSakSte22 %}

## Related Assumptions

- Partial Vandermonde Knapsack (also known as _Partial Fourier Recovery Problem_) {% cite ACNS:HPSSW14 %}{% cite ACISP:LuZhaAu18 %} is equivalent to PV-LWE.
- [Partial Vandermonde SIS](/pv-sis/) is the SIS version of PV-LWE.
