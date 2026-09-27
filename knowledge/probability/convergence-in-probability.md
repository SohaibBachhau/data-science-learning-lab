---
title: Convergence in Probability
subject: probability
status: developing
created: 2026-09-27
updated: 2026-09-27
last_reviewed: 2026-09-27
prerequisites:
  - random variables
  - probability distributions
sources:
  - VU Knowledge Clip Series: Probability Theory, Convergence of Random Variables I
tags:
  - convergence in probability
  - continuous mapping theorem
  - consistency
  - probability limits
---

# Convergence in Probability

## Central question

What does it mean for a sequence of random variables to become arbitrarily close to another random variable or constant with high probability?

## Short answer

A sequence $X_n$ converges in probability to $X$ when, for every tolerance $\varepsilon>0$,

$$
P(|X_n-X|>\varepsilon)\rightarrow 0.
$$

We write

$$
X_n\overset{p}{\longrightarrow}X.
$$

The probability of being meaningfully far from the limit becomes negligible as $n$ grows.

## Intuition

Convergence in probability does not mean that $X_n=X$ once $n$ is large. The sequence can still differ from the limit in any finite sample. What changes is the probability of a deviation larger than a fixed tolerance.

If the limit is a constant $c$, then

$$
X_n\overset{p}{\longrightarrow}c
$$

means that $X_n$ becomes increasingly concentrated around $c$.

## Continuous Mapping Theorem

If

$$
X_n\overset{p}{\longrightarrow}X
$$

and $h$ is continuous at the relevant values, then

$$
h(X_n)\overset{p}{\longrightarrow}h(X).
$$

This lets us transform probability limits.

Examples:

$$
X_n\overset{p}{\longrightarrow}X
\quad\Rightarrow\quad
e^{X_n}\overset{p}{\longrightarrow}e^X,
$$

and

$$
X_n\overset{p}{\longrightarrow}c
\quad\Rightarrow\quad
X_n-c\overset{p}{\longrightarrow}0.
$$

If $Y_n\overset{p}{\longrightarrow}Y$ and $Y\neq 0$, then the ratio map is continuous at the limit and

$$
\frac{X_n}{Y_n}
\overset{p}{\longrightarrow}
\frac{X}{Y}.
$$

The nonzero denominator condition matters.

## Connection to consistency

Consistency is convergence in probability applied to estimators.

An estimator $\hat\theta_n$ is consistent for $\theta$ when

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta.
$$

The Law of Large Numbers is one of the main tools used to establish such probability limits.

## Common mistakes

- Interpreting convergence in probability as eventual exact equality.
- Forgetting that the definition must hold for every fixed $\varepsilon>0$.
- Dividing probability limits when the denominator limit is zero.
- Confusing convergence in probability with convergence in distribution.
- Calling a transformation result "linearity" when the relevant tool is the Continuous Mapping Theorem.

## Retrieval questions

1. State the definition of convergence in probability.
2. Why does $X_n\overset{p}{\to}X$ not imply $X_n=X$ for large finite $n$?
3. State the Continuous Mapping Theorem.
4. Why is a nonzero limiting denominator needed for a ratio?
5. How is consistency related to convergence in probability?

## Connections

- [Law of Large Numbers](law-of-large-numbers.md)
- [Convergence in distribution](convergence-in-distribution.md)
- [Consistency](../statistics/consistency.md)
- [Central Limit Theorem](central-limit-theorem.md)

## Sources

- VU Amsterdam, *Knowledge Clip Series: Probability Theory*, Convergence of Random Variables I.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-09-27 | Reviewed definition, CMT, ratio condition and equivalence with subtracting a constant | Reproduce the epsilon definition and CMT from memory |
