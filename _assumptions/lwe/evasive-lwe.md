---
title: "Evasive LWE"
seo_title: "Evasive LWE"
family: "LWE"
graph_id: "Evasive-LWE"

last_modified_at: 2026-07-03
redirect_from:
  - /evasive_lwe/
  - /evasivelwe/
---

<style>
table.no-lines {
  margin: 0 auto 2em auto;
  width: max-content;
  max-width: 100%;
  display: block;
  overflow-x: auto;

  tbody tr:not(:last-child) td {
    border-bottom: none !important;
  }

  th, td {
    padding: 0.5em 1.5em !important;
  }
}
</style>

$$\newcommand{\aux}{\mathsf{aux}} \newcommand{\Samp}{\mathsf{Samp}} \newcommand{\tr}{\mathsf{T}}$$

Evasive LWE was first proposed by Wee in 2022 {% cite EC:Wee22 %}. The assumption intends to relate the hardness of two LWE problems with and without preimages. 

**Intuition**: Given a Gaussian preimage matrix $$\mat{U}$$ satisfying $$\mat{A} \cdot \mat{U} = \mat{P} \bmod q$$ for some target matrix $$\mat{P}$$, and some challenge $$\vec{c}^\tr$$ which is either an LWE sample vector $$\vec{s}^\tr \cdot \mat{A} + \vec{e}^\tr \bmod q$$ or uniformly random, the assumption asserts that the only meaningful use of $$\mat{U}$$ is to right-multiply $$\vec{c}^\tr$$ by it, obtaining $$\vec{s}^\tr \cdot \mat{P} + \text{error} \bmod q$$, and to attempt to distinguish using the resulting product together with the original challenge.

Formally, this is captured by a pair of $$\mathsf{Pre}$$ and $$\mathsf{Post}$$ experiments, where $$\mathsf{Post}$$ represents the LWE-with-preimages problem, and $$\mathsf{Pre}$$ represents an LWE problem induced by the said right-multiplication operation, which is without preimages and models the resulting product as fresh LWE samples. 

## Definition {% cite EC:Wee22 %}

Define two experiments: $$\mathsf{Pre}$$ and $$\mathsf{Post}$$.

| $$\mathsf{Pre}_\adv\left(1^\lambda\right)$$ | $$\mathsf{Post}_\bdv\left(1^\lambda\right)$$ |
| --- | --- |
| $$(\mat{P}, \mat{B}, \aux) \gets \Samp\left(1^\lambda\right)$$ | $$(\mat{P}, \mat{B}, \aux) \gets \Samp\left(1^\lambda\right)$$ |
| $$\mat{A} \sample \ZZ_q^{n \times m}$$ | $$\mat{A} \sample \ZZ_q^{n \times m}$$ |
| $$\vec{s} \sample \ZZ_q^{n}$$ | $$\vec{s} \sample \ZZ_q^{n}$$ |
| **if** $$b=0$$ **then** | **if** $$b=0$$ **then** |
| $$\quad \vec{e}_A \sample D_{\ZZ,\chi_A}^{m}, \vec{e}_B \sample D_{\ZZ,\chi_B}^{m_B}, \vec{e}_P \sample D_{\ZZ,\chi_P}^{m_P}$$ | $$\quad \vec{e}_A \sample D_{\ZZ,\chi_A}^{m}, \vec{e}_B \sample D_{\ZZ,\chi_B}^{m_B}$$ |
| $$\quad \vec{c}_A^\tr = \vec{s}^\tr \mat{A} + \vec{e}_A^\tr \bmod q$$ | $$\quad \vec{c}_A^\tr = \vec{s}^\tr \mat{A} + \vec{e}_A^\tr \bmod q$$ |
| $$\quad \vec{c}_B^\tr = \vec{s}^\tr \mat{B} + \vec{e}_B^\tr \bmod q$$ | $$\quad \vec{c}_B^\tr = \vec{s}^\tr \mat{B} + \vec{e}_B^\tr \bmod q$$ |
| $$\quad \vec{c}_P^\tr = \vec{s}^\tr \mat{P} + \vec{e}_P^\tr \bmod q$$ | $$\quad \mat{U} \sample D_{\Lambda_q^{\mat{P}}(\mat{A}), \sigma}$$ |
| **if** $$b=1$$ **then** | **if** $$b=1$$ **then** |
| $$\quad \vec{c}_A \sample \ZZ_q^{m}$$ | $$\quad \vec{c}_A \sample \ZZ_q^{m}$$ |
| $$\quad \vec{c}_B \sample \ZZ_q^{m_B}$$ | $$\quad \vec{c}_B \sample \ZZ_q^{m_B}$$ |
| $$\quad \vec{c}_P \sample \ZZ_q^{m_P}$$ | $$\quad \mat{U} \sample D_{\Lambda_q^{\mat{P}}(\mat{A}), \sigma}$$ |
| **return** $$b = \adv(\mat{A}, \mat{B}, \mat{P}, \vec{c}_A, \vec{c}_B, \vec{c}_P, \aux)$$ | **return** $$b = \bdv(\mat{A}, \mat{B}, \mat{P}, \vec{c}_A, \vec{c}_B, \mat{U}, \aux)$$ |
{: .no-lines }

### Evasive LWE$$_{q,n,m,m_B,m_P,\chi_A,\chi_B,\chi_P,\sigma}$$ {#evasive-lwe}
_Let $$\Samp$$ be a ppt algorithm which, on input $$1^\lambda$$, outputs $$(\mat{P}, \mat{B}, \aux)$$ $$\in$$ $$\ZZ_q^{n \times m_P} \times \ZZ_q^{n \times m_B} \times \set{0,1}^*$$, where $$\aux$$ contains all coin tosses used by $$\Samp$$. Let $$\chi_A$$, $$\chi_B$$, $$\chi_P$$, and $$\sigma$$ be positive Gaussian widths. The evasive LWE assumption states that for any ppt $$\Samp$$ and $$\bdv$$ there exists a ppt $$\adv$$, a polynomial $$\poly{\cdot}$$ and a negligible function $$\negl{\cdot}$$, such that_

$$ \mathsf{Adv}_\adv^\mathsf{Pre}(\lambda) \geq \mathsf{Adv}_\bdv^\mathsf{Post}(\lambda) / \poly{\lambda} - \negl{\lambda}. $$


**Status**: The work {% cite EC:Wee22 %} discusses the "public-coin sampler" property of its assumption, and the literature commonly refers to it as "public-coin evasive LWE". There are numerous evasive LWE variants and related attacks, including incomparable variants carrying the same name (see "Variants" below). No existing attack applies to the above version, except under unnatural choices of parameters (see Note 2 below). A special case of this assumption, together with standard LWE, is known to imply the succinct LWE assumption (see "Evasive LWE (Wee24)" below).

**Note 1 (adaptation from {% cite EC:Wee22 %})**: The above definition is adapted from {% cite EC:Wee22 %} with the following changes: (1) each error vector and the preimage matrix $$\mat{U}$$ is equipped with its own Gaussian width parameter, and (2) the distinguishers $$\adv$$ and $$\bdv$$ are explicitly given $$\mat{P}$$ as input.
The first is to allow for more general parameter settings, for the potential of more fine-grained analyses in different regimes. The second is only for clarity and does not change the assumption, since $$\mat{P}$$ is recoverable from the coin tosses of $$\Samp$$, which are included in $$\aux$$.
There are also minor presentation and notational changes, which do not affect the actual assumption and are there to increase consistency with the other entries in this Zoo.

**Note 2 (on sensitivity to Gaussian width)**: In Remark 2 of {% cite EC:Wee22 %}, it is noted that the Gaussian widths of the errors and preimages influence the assumption strength, in that larger error and preimage widths in $$\mathsf{Post}$$ (hence harder to win $$\mathsf{Post}$$), and/or smaller error widths in $$\mathsf{Pre}$$ (hence easier to win $$\mathsf{Pre}$$), lead to a weaker assumption. In {% cite TCC:AMYY25 %} it is shown that if the error width $$\chi_P$$ in $$\mathsf{Pre}$$ is super-polynomially larger than the error and preimage widths $$\chi_A,\sigma$$ in $$\mathsf{Post}$$, then there are simple counterexamples to the assumption. The counterexamples crucially rely on these unusual parameter choices and do not apply otherwise.


## Variants

The intuition behind evasive LWE has been formalised in numerous ways in the literature, primarily by defining different pairs of $$\mathsf{Pre}$$ and $$\mathsf{Post}$$ experiments, or changing the quantification of the sampler class. Many variants are formally incomparable. Sometimes different definitions are referred to by the same name (e.g. "public-coin evasive LWE"), while some are not given a specific name beyond "evasive LWE".

To avoid confusion or misunderstanding that may arise from naming, the following list of variants **refers to each by the paper which introduced it**, instead of trying to endow each with a name. If a particular assumption name has been used in the paper, this is noted below.

The list attempts to include the majority of variants in the literature, but is not meant to be exhaustive.

IW: The tags are incomplete. Not sure how to make them compatible with the zoo globally.

### Evasive LWE (WWW22)

The work {% cite TCC:WatWeeWu22 %} defines a variant for constructing a multi-authority ABE for subset policies. The $$\mathsf{Pre}$$ and $$\mathsf{Post}$$ experiments consist of multiple tuples of LWE samples (with their preimages in $$\mathsf{Post}$$) and further LWE samples with a correlated LWE secret.
Similar to {% cite EC:Wee22 %}, the work {% cite TCC:WatWeeWu22 %} discusses the "public-coin sampler" property of the assumption, and it is commonly called "public-coin evasive LWE".

### Evasive LWE (VWW22) <a href="#" class="status-badge status-broken" data-tooltip="This assumption has been compromised by known attacks.">broken</a> {#private-coin-evasive-lwe}

The work {% cite AC:VaiWeeWic22 %} defines a variant for proving the witness encryption (WE) and null-iO constructions in {% cite C:CheVaiWee18 %} secure. It quantifies over a class of samplers that can generate the secret $$\vec{s}$$, the image $$\mat{P}$$ and the auxiliary input $$\aux$$ together. The matrix $$\mat{A}$$ is not available to the distinguishers. Likewise, $$\mat{P}$$ and the coins used by $$\Samp$$ are not necessarily available. The work {% cite AC:VaiWeeWic22 %} calls this "private-coin evasive LWE".

The first attack and fix on this variant are given in {% cite AC:BrzUnaWoo24 %}. The proposed fix is subsequently broken by {% cite AC:BrzUnaWoo24 %} in its eprint update, concurrently also in {% cite C:DJMMV25 %} and {% cite C:HsiJaiLin25 %}. None of the attacks applies to the WE and null-iO constructions in {% cite C:CheVaiWee18 %}.

A morally similar (although formally different) assumption is given in {% cite C:Tsabary22 %}, also used for constructing WE and attacked in {% cite AC:BrzUnaWoo24 %}.

### Evasive LWE (HLL23) <a href="#" class="status-badge status-broken" data-tooltip="This assumption has been compromised by known attacks.">broken</a> {#circular-evasive-lwe}

The work {% cite FOCS:HsiLinLuo23 %} introduces a variant called "evasive circular small-secret LWE" for constructing unbounded-depth ABE. The $$\mathsf{Pre}$$ and $$\mathsf{Post}$$ experiments involve, among others, a GSW encryption of the LWE secret and circular LWE samples where the matrix encodes the GSW encryption.  

An attack on this assumption is given in {% cite TCC:AMYY25 %}. The attack does not apply to the ABE construction in {% cite FOCS:HsiLinLuo23 %}.

### Evasive LWE (ARYY23) <a href="#" class="status-badge status-broken" data-tooltip="This assumption has been compromised by known attacks.">broken</a>

The work {% cite C:ARYY23 %} defines a variant for constructing multi-input ABE. It is similar to the VWW22 variant, with a difference being that the matrix $$\mat{A}$$ is given to the distinguishers. This makes the two formally incomparable. 

The first attack and fix on this variant are given in {% cite AC:BrzUnaWoo24 %}. The proposed fix is subsequently broken by {% cite AC:BrzUnaWoo24 %} in its eprint update, concurrently also in {% cite C:DJMMV25 %} and {% cite C:HsiJaiLin25 %}. None of the attacks applies to the multi-input ABE construction in {% cite C:ARYY23 %}.

### Evasive LWE (Wee24)

The work {% cite C:Wee24 %} considers a special case of the assumption in {% cite EC:Wee22 %}, where $$\mat{B}$$ and $$\vec{c}_B$$ are dropped. This special case is informally described in {% cite EC:Wee22 %} although not formalised therein. The work {% cite C:Wee24 %} shows that, under appropriate parameters, this special case together with the standard LWE assumption implies the $$\ell$$-succinct LWE assumption.

### Evasive LWE (BÜW24 Def. 7)

The work {% cite AC:BrzUnaWoo24 %} (Definition 7) attempts to provide a general definition to capture different versions of "public-coin evasive LWE" in the literature. This is called "public-coin evasive LWE" in {% cite AC:BrzUnaWoo24 %}.

### Evasive LWE (BÜW24 Def. 8, 9) <a href="#" class="status-badge status-broken" data-tooltip="This assumption has been compromised by known attacks.">broken</a>

The work {% cite AC:BrzUnaWoo24 %} attempts to characterise "private-coin evasive LWE" variants in the literature. It provides two different definitions (Definitions 8 and 9), called "private-coin binding evasive LWE" and "private-coin hiding evasive LWE" respectively.

After its publication, the eprint update of {% cite AC:BrzUnaWoo24 %} provides attacks on both variants. Concurrently, {% cite C:DJMMV25 %} and {% cite C:HsiJaiLin25 %} also provide attacks on these variants using different techniques.

### Evasive LWE (BDJMMPV25) <a href="#" class="status-badge status-broken" data-tooltip="This assumption has been compromised by known attacks.">broken</a>

The work {% cite C:BDJMMPV25 %} defines a variant for constructing pseudorandom iO, a primitive introduced in the same work. The construction, and therefore also the assumption, is attacked in {% cite TCC:AMYY25 %}.

### Evasive LWE (AKY25)

In the first eprint appearance of {% cite EPRINT:AgrKumYam24b %}, the ARYY23 variant is used to construct pseudorandom functional encryption, a primitive introduced in the same work. The construction, and therefore also the assumption, is attacked in {% cite TCC:AMYY25 %}. Subsequently, {% cite EPRINT:AgrKumYam24b %} refines its construction and defines a restricted form of the assumption that is sufficient for proving the security of the refined construction.

JNS: Define as many variants as you see fit / seems useful. Just copy the broken-badge wherever needed.


## Constructions built from Evasive LWE {#constructions}

IW: Suggestion: add a disclaimer on that the list is not exhaustive. 

IW: Consistency note: I wrote evasive LWE with small letter e throughout. I'm not sure what's the convention of the Zoo, whether assumptions should begin with capital or small letter.

- Broadcast Encryption {% cite EC:Wee22 %}
- Witness Encryption {% cite C:Tsabary22 %}{% cite AC:VaiWeeWic22 %}
- Zero-Knowledge SNARKs for UP {% cite C:MatPetVai24 %}
- SNARGs for NP {% cite STOC:JKLM25 %}
- Pseudorandom Obfuscation {% cite C:BDJMMPV25 %}
- Pseudorandom Functional Encryption {% cite EPRINT:AgrKumYam24b %}{% cite EPRINT:AgrKumYam24c %}
- Multi-Authority ABE {% cite TCC:WatWeeWu22 %}
- ABE for Turing Machines {% cite C:AgrKumYam24 %}
- Constant-Input ABE {% cite C:ARYY23 %}
- Unbounded Depth ABE {% cite FOCS:HsiLinLuo23 %}

## Related Assumptions 

- [Evasive SIS](/evasive-sis/) is the SIS version of evasive LWE.
- [$$\ell$$-Succinct LWE](/l-succinct-lwe/) is an assumption implied by evasive LWE (Wee22, Wee24) together with standard LWE. A number of applications formerly from evasive LWE are now known from $$\ell$$-succinct LWE.

## Further Reading Suggestions

- [Workshop session from Simons Institute](https://simons.berkeley.edu/talks/optimal-broadcast-encryption-more-evasive-lwe) by Hoeteck Wee.
