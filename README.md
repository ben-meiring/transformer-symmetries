# Symmetries in Transformers Computing Boolean Functions

This project studies how the computational capacity of a simple transformer depends on its number of attention heads. It was completed as part of a research assessment by [Verified Mechanisms](https://verifiedmechanisms.ai/) based on an autoresearch repository containing roughly 200 theorems about the Boolean functions computed by a single attention layer.

The model receives an input sequence of Boolean variables together with a fixed query token. Only the residual stream at the query token is read by the classifier. For a Boolean function $f$, its **head complexity** $H^*(f)$ is the minimum number of attention heads required to compute it.

## What I did

* Reconstructed the central results of the repository in a self-contained [18-page write-up](writeup/rs-takehome-meiring.pdf).

* Derived the scalar normal form of an attention head and showed how threshold degree gives a general lower bound on head complexity:

  \(\deg_{\pm}(f) \leq H^*(f).\)

* Used this framework to recover the exact head complexity of parity:

  \(H^*(\mathrm{PARITY}_n)=n.\)

* Developed a symmetry-based method for analyzing whole classes of Boolean functions. The method reduces the threshold-degree problem from all $2^n$ Boolean inputs to the orbits of a group action, using Reynolds-averaged Walsh characters as invariant features.

* Gave an explicit cyclic four-bit example in which the lowest-degree invariant separator can be found geometrically, and formulated the general search as a linear-programming feasibility problem.

* Produced Lean-verified proofs of two symmetry-based lower bounds.

* Built an interactive **Theorem Atlas** to organize the repository's results, dependencies, open questions, and refuted hypotheses.

## Read and explore

* **[Read the full write-up](writeup/rs-takehome-meiring.pdf)**
* **[Open the interactive Theorem Atlas](https://ben-meiring.github.io/rs-takehome/)**
* **[Browse my fork of the original repository](https://github.com/ben-meiring/rs-takehome)**
* **[View the original Verified Mechanisms repository](https://github.com/VerifiedMechanisms/rs-takehome)**

## Main idea

If a Boolean function is invariant under a finite group $G$, its inputs split into group orbits and the function is constant on each orbit. Reynolds averaging produces a degree-controlled basis of invariant polynomial features,

\(I_S(z)=\frac{1}{|G|}\sum_{g\in G}\chi_S(gz),\)

where $\chi_S(z)=\prod_{i\in S}z_i$ is a Walsh character. Any sign-representing polynomial can be averaged over the group without increasing its degree, so restricting the search to invariant polynomials loses no generality.

Each orbit can therefore be represented as a point in invariant-feature space. Determining the threshold degree becomes the problem of finding the lowest-degree collection of invariant features that linearly separates the positive and negative orbit labels.

## Repository structure

```text
.
├── README.md
├── writeup/
│   └── rs-takehome-meiring.pdf
└── assignment-source/     # linked copy of my rs-takehome fork
```

The `assignment-source` directory is included as a Git submodule pointing to my fork of the assessment repository.
