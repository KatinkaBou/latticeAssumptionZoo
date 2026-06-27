---
title: "Equivocal LWE"
seo_title: "Equivocal LWE"
family: "LWE"
graph_id: "Equivocal-LWE"

last_modified_at: 2026-06-27
redirect_from:
  - /equivocal_lwe/
  - /equivocallwe/
---

Equivocal LWE was introduced by Cini, Lai, and Woo in 2025 {% cite C:CinLaiWoo25 %}. The assumption is designed to model model the BDGM framework {% cite EC:BDGM20 %} while abstracting away complications like the choice of the symmetric key encryption or encoding.

As the assumption is quite complex and closely related to a specific type of construction, it belongs to a category of cryptographic assumptions criticised in a position paper on cryptographic assumptions by Goldwasser and Kalai {% cite TCC:GolKal16 %}.

## Definition

We provide the informal but more intuitive definition given by Cini et al in Section 1.3 {% cite C:CinLaiWoo25 %}.
$$\newcommand{msg}{\mathsf{msg}}\newcommand{\SKE}{\mathsf{SKE}}\newcommand{sk}{\mathsf{sk}}\newcommand{Enc}{\mathsf{Enc}}\newcommand{ctxt}{\mathsf{ctxt}}$$

### Equivocal LWE$$_{\mathcal{R},q,h,k,d,p,t,s,\chi,\mathsf{SKE},\mathsf{Encode},\mathcal{E}}$$ {#equivocal-lwe}
_Let $$\SKE = (\Enc, \mathsf{Dec})$$ be a symmetric-key encryption scheme, let $$\mathsf{Encode}: \mathcal{S} \rightarrow \mathcal{R}_q^{p \ceil{\log q} \times k}$$ be a deterministic encoding algorithm, and let $$\mathcal{E}$$ be a distribution over $$\mathcal{R}_q^{t \times k}$$. The circuit $$\Phi$$ maps $$\mathcal{C}_\mathsf{tag}$$ to $$\mathcal{R}_q^{p \times h} \times \mathcal{R}_q^{h \times k}$$ and needs to be efficiently computable._

1. _$$\adv$$ chooses messages $$\msg_0, \msg_1, \msg_\mathsf{pad}$$, and a circuit $$\Phi$$._
2. _Generate an $$\SKE$$ secret key $$\sk$$. Encrypt $$\msg_\mathsf{pad}$$ as $$\mat{P} \leftarrow \SKE.\Enc(\sk, \msg_\mathsf{pad})$$._
3. _Sample an equivocal matrix $$\mat{B} \sample \mathcal{E}$$ and mask $$\mathsf{Encode}(\sk)$$ with the LWE sample $$\mat{C} = \mat{R}\mat{B} + \mat{E} + \mathsf{Encode}(\sk) \bmod q$$, where $$\mat{R} \sample \mathcal{R}_q^{p \ceil{\log q} \times t}$$ and $$\mat{E} \sample D_{\mathcal{R},\chi}^{p \ceil{\log q} \times k}$$._
4. _For each $$i \in \set{0,1}$$ do:_
  - _Encrypt $$\msg_i$$ as $$\ctxt_i \leftarrow \SKE.\Enc(\sk, \msg_i)$$._
  - _Run the circuit $$\Phi$$ on $$\ctxt_i$$ to obtain $$(\mat{H}_i, \mat{M}_i)$$._
  - _Compute $$\mat{L}_i^T = \mat{G}^{-1}(\mat{H} + \vec{1}^T \otimes \mat{P})$$. Let $$\mat{W}_i = \mat{L}_i \mat{C} + \mat{M}_i$$. Assert that $$\norm{\mat{W}_i - \mat{L}_i \mat{R} \mat{B} \bmod q} \leq s$$._
5. _Assert that $$\mat{M}_0 = \mat{M}_1$$._
6. _Choose $$b \sample \set{0,1}$$. Let $$\vec{w}_{b,i}$$ denote the row columns of $$\mat{W}_b$$. Equivocate $$\mat{L}_b \mat{R}$$ via $$\bar{\mat{R}}_i \mat{B} \sample \left(D_{\Lambda_q(\mat{B}),s,\vec{w}_{b,j}}\right)_{j \in [h]}$$ to obtain $$\mat{R}_b$$ satisfying $$\mat{R}_b \mat{B} \approx \mat{L}_b\mat{R}\mat{B}$$._
7. _Given $$\mat{B}$$, $$\mat{C}$$, $$\mat{P}$$, $$\ctxt_b$$, and $$\mat{R}_b$$, an adversary is asked to distinguish between $$b=0$$ and $$b=1$$._

The assumption crucially relies on the notion of equivocality. For this, they define an _induced distribution of equivocate_ for their primal trapdoor for $$(\mat{B}, \mathsf{td}) \sample \mathsf{pTrapGen}(1^t, 1^k, q)$$ and any $$\vec{r} \in \mathcal{R}_q^t$$, $$\vec{c} \in \mathcal{R}_q^k$$, $$s>0$$ satisfying $$\norm{\vec{c}^T - \vec{r}^T \mat{B} \bmod q} \leq s$$:

$$ \set{\vec{r} \mat{B} \bmod q \mid \vec{r} \leftarrow \mathsf{Equivocate}(\mathsf{td}, \vec{r}, \vec{c}, s)} \approx D_{\Lambda_q(\mat{B}),s,\vec{c}}. $$

The Induced Distribution of Equivocate property in their primal trapdoor definition is equivalent to requiring that the equivocated LWE error satisfies

$$ \left\{ \vec{e} \space \middle| \space \begin{array}{l} \vec{r} \leftarrow \mathsf{Equivocate}(\mathsf{td}, \vec{r}, \vec{c}, s) \\ \vec{e}^T = \vec{c}^T - \vec{r}^T \mat{B} \bmod q \end{array} \right\} \approx D_{\Lambda_q(\mat{B})+\vec{c},s} \bmod q $$

_for $$\vec{r}$$, $$\vec{c}$$ satisfying the same constraints. This is because $$\vec{c}^T - D_{\Lambda_q(\mat{B}),s,\vec{c}} = D_{\Lambda_q(\mat{B}) + \vec{c}, s}$$._

## Hardness

Cini et al. {% cite C:CinLaiWoo25 %} explore Equivocal LWE mainly via three cryptanalytic attempts: No-hint attacks, trivial distinguishing attacks based on differing quality of hints, and "zero-ising" attacks. A high-level description of these attack strategies can be found in Section 1.4 of {% cite C:CinLaiWoo25 %}.

## Constructions built from Equivocal LWE {#constructions}

- Indistinguishable Obfuscation {% cite C:CinLaiWoo25 %}
- Registered Attribute-Based Encryption {% cite EPRINT:MurSarMan25 %}
