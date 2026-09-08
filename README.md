# Symmetries in Transformers Computing Boolean Functions

This project studies the computational capacity of a single layers transformers, and relates this to the number of attention heads required to represent boolean functions. We aimed to verify and extend the results of an autoresearch repository provided by [Verified Mechanisms](https://verifiedmechanisms.ai/).

The model receives an input sequence of Boolean variables together with a fixed query token. Only the residual stream at the query token is read by the classifier. For a Boolean function $f$, its **head complexity** $H^*(f)$ is the minimum number of attention heads required to compute it.

## What I did

- Reconstructed the central results of the repository in a self-contained [18-page write-up](https://github.com/ben-meiring/transformer-symmetries/blob/main/transformer_symmetries_writeup.pdf).
- Developed a symmetry-based method for analyzing whole classes of Boolean functions using group orbits and Reynolds-averaged Walsh characters.
- Reduced the search for the lowest-degree invariant separator to a linear-programming feasibility problem.
- Produced Lean-verified proofs of two symmetry-based lower bounds.
- Built an interactive **Theorem Atlas** to organize the repository's results, dependencies, open questions, and refuted hypotheses.

## A quick example: cyclic symmetry

For a Boolean function $f$, let $H^*(f)$ denote the minimum number of attention heads required to compute it, and let $\deg_{\pm}(f)$ denote the minimum degree of a polynomial whose sign reproduces $f$. These quantities satisfy

$$
\deg_{\pm}(f)\leq H^*(f),
$$

so any lower bound on threshold degree gives the same lower bound on the number of attention heads.

Consider four sign-valued inputs $z_i \in \{-1,1\}$ arranged on a cycle. Cyclic rotations are identified under the action

$$
g(z_1,z_2,z_3,z_4)=(z_2,z_3,z_4,z_1).
$$

The 16 possible inputs collapse into six rotation orbits:

$$
O_0,\quad O_1,\quad O_{\mathrm{adj}},\quad
O_{\mathrm{opp}},\quad O_3,\quad O_4.
$$

Here $O_{\mathrm{adj}}$ contains configurations whose two positive entries are adjacent, while $O_{\mathrm{opp}}$ contains those whose positive entries are opposite.

Define the invariant Boolean function

$$
F(z)=
\begin{cases}
+1, & \text{if at least one adjacent pair is positive},\\
-1, & \text{otherwise}.
\end{cases}
$$

The degree-one invariant

$$
I_1(z)=\frac{1}{4}\sum_{i=1}^{4}z_i
$$

distinguishes the orbits by Hamming weight. However, the oppositely labelled orbits $O_{\mathrm{adj}}$ and $O_{\mathrm{opp}}$ both map to $I_1=0$, so no degree-one invariant can separate the classes.

Adding the degree-two invariant

$$
I_{\mathrm{opp}}(z)=\frac{1}{2}(z_1z_3+z_2z_4)
$$

resolves this collision. In the resulting two-dimensional invariant space, the line

$$
P_F(z)=I_1(z)-\frac{1}{2}I_{\mathrm{opp}}(z)=0
$$

separates the positive and negative orbits.

 <br>
<table>
  <tr>
    <td width="50%" align="center">
      <img src="pictures/c4-degree-one-orbit-projection.png"
           alt="Degree-one orbit projection"
           width="100%">
      <br>
      <em>(a) Projection onto the degree-one invariant. The oppositely labelled orbits
      O<sub>adj</sub> and O<sub>opp</sub> coincide.</em>
    </td>
    <td width="50%" align="center">
      <img src="pictures/c4-i1-iopp-orbit-separation.png"
           alt="Degree-two orbit separation"
           width="100%">
      <br>
      <em>(b) Adding the degree-two invariant separates the positive and negative orbits.</em>
    </td>
  </tr>
</table>
<br>

Therefore $F$ has threshold degree two, giving the head-complexity lower bound $H^*(F)\geq2$. More generally, Reynolds averaging shows that any sign-representing polynomial for a symmetric function can be replaced by an invariant one without increasing its degree.

## Read and explore

- **[Read the full write-up](writeup/rs-takehome-meiring.pdf)**
- **[Open the interactive Theorem Atlas](https://ben-meiring.github.io/rs-takehome/)**
- **[Browse my fork of the original repository](https://github.com/ben-meiring/rs-takehome)**
- **[View the original Verified Mechanisms repository](https://github.com/VerifiedMechanisms/rs-takehome)**

## Repository structure

```text
.
├── README.md
├── assets/
│   ├── c4-degree-one-orbit-projection.png
│   └── c4-i1-iopp-orbit-separation.png
├── writeup/
│   └── rs-takehome-meiring.pdf
└── assignment-source/
```
