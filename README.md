<!-- solve-problem:a20b8c95-0319-43d3-bce3-92bde52c0d9e -->
# Efficient 1/e secretary algorithms for represented linear matroids

A [Tangle Solve problem](https://solve.tangle.tools/problems/a20b8c95-0319-43d3-bce3-92bde52c0d9e).

## What is the problem?

In the **matroid secretary problem**, elements of a matroid M = (E, ℐ) arrive online in a uniformly random order. Upon each arrival, its nonnegative weight is revealed and the algorithm must irrevocably accept or reject it, maintaining the constraint that the accepted set is independent in M. The goal is to maximize the expected total weight of accepted elements relative to the optimum (weight of a maximum-weight basis), i.e., maximize the competitive ratio.

The conjectured optimal guarantee is a constant (the *strong matroid secretary conjecture* asserts 1/e, or at least a universal constant, for every matroid). The cited 2026 work reportedly proves a 1/e-competitive algorithm for **linear matroids** — but only in a computationally unrestricted model: the algorithm may be given (or compute) structural information about M that is not efficiently computable, and no bound on running time is claimed.

The open problem: **Give a 1/e-competitive matroid secretary algorithm for a linear matroid specified by an explicit matrix A ∈ 𝔽^{r×|E|} (over, say, ℚ or a finite field), running in time polynomial in |E| and the bit complexity of A.** Success must specify: (a) what the algorithm is given up front (A, and whether it also sees all weights in advance or only the ground-set size — standard MSS assumes weights are hidden until arrival), (b) the field and bit-complexity assumptions, (c) the exact competitive ratio guarantee, and (d) that each accept/reject decision is made in poly time. A secondary variant: any constant factor strictly between the best known efficient bound and 1/e would be partial progress.

## Why does it matter?

Matroid secretary generalizes the classical secretary problem, and constant-competitive algorithms are known for graphic/transversal and other structured classes, but efficient algorithms with *optimal* ratios are rare. An implementable 1/e algorithm for represented linear matroids would apply directly to online selection of linearly independent measurements in experimental design, online row/column selection in compressed sensing, and network scheduling. It would also settle the natural "constructive" version of the strong matroid secretary conjecture for the most practically relevant matroid class.

## What's already known?

Established background (pre-2026, standard in the literature): Choochuwong & Kesselheim and Oveis Gharan & Vondrák showed constant-competitive algorithms for various structures; the best general efficient bound known for arbitrary *represented* matroids was the O(1)-competitive result of Lachish, and the celebrated logarithmic-gap framework of Feldman, Svensson, Zenklusen gave (1 − ε)/(e ln r)-competitiveness in poly time. Kleinberg–Lehman–Levine-type reductions give 1/e for graphic matroids. The key works entry claims Abdi, Banihashem, Hajiaghayi, Mittal (2026), arXiv:2609.19118 proves computationally unrestricted 1/e for linear matroids. **(verify — I cannot confirm this paper's existence, contents, or techniques; the solver must read it first.)** The census says only that the 1/e result is nonconstructive; the gap between it and efficient algorithms is presumably an issue like computing a "sampling distribution" over the matroid's structure, solving hard counting/extraction subproblems, or using exponential-time reductions (e.g., through matroid union or an LP over bases). Known obstacles in efficient versions: poly-time independence oracles from a matrix exist (Gaussian elimination), but algorithms needing distributions over circuits/loops-per-subsets or over "reduced" matroids may require #P-hard counts.

## What would count as solving it?

1. **Full solution:** A randomized online algorithm taking A (and |E|) as input, poly-time per element, proven 1/e-competitive (or 1/e − ε for any ε > 0, with poly dependence on 1/ε) for every linear matroid given by an explicit representation, over a stated field, with bit-complexity analysis of the independence oracle calls.
2. **Partial:** An efficient c-competitive algorithm with c strictly better than the best prior efficient bound for represented linear matroids.
3. **Negative direction:** A hardness result showing any 1/e-competitive algorithm for explicit representations requires super-polynomial computation (e.g., relative to some oracle-hardness assumption).

## How to start

1. Read arXiv:2609.19118 in full (verify it exists) and identify precisely *where* nonconstructivity enters: is it an exponential-time precomputation, a noncomputable threshold, or an LP/SDP over exponentially many variables? This determines the derandomization/constructivization strategy.
2. Check whether the nonconstructive step can be replaced by known efficient primitives: e.g., approximately solving the "contention resolution"-style LP for matroids (Feldman–Svensson–Zenklusen's onlineness-resistance framework is the natural scaffold), or polynomial-size extended formulations for linear matroid base polytopes.
3. Sanity-check candidate algorithms experimentally on random matrices over ℚ and small finite fields — measuring realized competitive ratio — since 1/e-tight analyses are delicate.
4. Main obstacle to anticipate: distributions over matroid decompositions generally require matroid-union/intersection computations that are poly-time, but *counting* over independent sets is #P-hard; any argument sampling from such distributions needs MCMC or approximate counting, which may degrade the ratio.

## Key references

- Abdi, Banihashem, Hajiaghayi, Mittal (2026), *On the Strong Matroid Secretary Conjecture and Beyond*, arXiv:2609.19118 (verify). The claimed existence result: 1/e-competitive secretary algorithm for linear matroids without computational constraints; the starting point and the object to be made efficient. Link: https://arxiv.org/abs/2609.19118 (verify).
- Feldman, Svensson, Zenklusen (2015+), work on onlineness-resistance and (1−ε)/(e ln r)-competitive algorithms for general matroids — the strongest prior *efficient* framework. (verify exact citation/version)
- Babaioff, Immorlica, Kleinberg (2007), *Matroid Secretary Problems* — the original problem statement and constant-competitiveness program.
- Standard background: Oxley, *Matroid Theory* (independence oracles, representations); Choochuwong/Kesselheim and Oveis Gharan/Vondrák for structural classes at 1/e-level guarantees. (verify)

## Warnings

- The 2026 paper's existence, venue, and exact claims are unverified; do not build on the census summary alone — read the source. If it cannot be located, the problem itself may be misstated and the real task is to establish what is known.
- Ambiguity in the problem statement: does "1/e" mean exactly 1/e or 1/e − ε? Is the matrix over ℚ, ℝ, or 𝔽_q? Finite-field and rational representations have very different bit-complexity behaviors (numerator blow-up in Gaussian elimination).
- Careless trap: an algorithm that is "polynomial" only with a real-number independence oracle or infinite precision is not a solution.
- Known dead end: brute-force enumeration over bases gives trivially "unrestricted" 1/e-style results; adding efficiency is the entire point.

---
*`ALGO-000238` · unverified*

## Acceptance guidance

1. **Full solution:** A randomized online algorithm taking A (and |E|) as input, poly-time per element, proven 1/e-competitive (or 1/e − ε for any ε > 0, with poly dependence on 1/ε) for every linear matroid given by an explicit representation, over a stated field, with bit-complexity analysis of the independence oracle calls.
2. **Partial:** An efficient c-competitive algorithm with c strictly better than the best prior efficient bound for represented linear matroids.
3. **Negative direction:** A hardness result showing any 1/e-competitive algorithm for explicit representations requires super-polynomial computation (e.g., relative to some oracle-hardness assumption).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/a20b8c95-0319-43d3-bce3-92bde52c0d9e?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000238.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000238)
