---
title: Convergence in Distribution
subject: probability
status: developing
created: 2026-09-27
updated: 2026-09-27
last_reviewed: 2026-09-27
prerequisites:
  - probability distributions
  - convergence in probability
sources:
  - VU Knowledge Clip Series: Probability Theory, Convergence of Random Variables II
tags:
  - convergence in distribution
  - weak convergence
  - slutsky
  - limiting distributions
---

# Convergence in Distribution

## Central question

What does it mean for the distribution of a sequence of random variables to approach a limiting distribution?

## Short answer

A sequence $X_n$ converges in distribution to $X$ when its cumulative distribution functions converge to the CDF of $X$ at continuity points of the limiting CDF.

We write

$$
X_n\overset{d}{\longrightarrow}X.
$$

This describes convergence of distributions, not necessarily convergence of realized values.

## Formal idea

If $F_n$ is the CDF of $X_n$ and $F$ is the CDF of $X$, then

$$
F_n(x)\rightarrow F(x)
$$

at every continuity point of $F$.

## Relation to convergence in probability

Convergence in probability is stronger:

$$
X_n\overset{p}{\longrightarrow}X
\quad\Rightarrow\quad
X_n\overset{d}{\longrightarrow}X.
$$

The reverse does not generally hold.

This difference matters because consistency is a probability-limit statement, while the Central Limit Theorem is a distribution-limit statement.

## Slutsky's theorem

Suppose

$$
S_n\overset{d}{\longrightarrow}S
$$

and

$$
a_n\overset{p}{\longrightarrow}a,
$$

where $a$ is a constant. Then, under the usual continuity conditions,

$$
S_n+a_n\overset{d}{\longrightarrow}S+a,
$$

$$
S_na_n\overset{d}{\longrightarrow}aS,
$$

and if $a\neq 0$,

$$
\frac{S_n}{a_n}\overset{d}{\longrightarrow}\frac{S}{a}.
$$

Slutsky's theorem is especially useful when a statistic has a limiting distribution but contains unknown quantities that are replaced by consistent estimators.

## Standardization example

Suppose

$$
X_n\overset{d}{\longrightarrow}N(\mu,\sigma^2),
$$

$$
\mu_n\overset{p}{\longrightarrow}\mu,
$$

and

$$
\sigma_n\overset{p}{\longrightarrow}\sigma>0.
$$

Then Slutsky's theorem gives

$$
\frac{X_n-\mu_n}{\sigma_n}
\overset{d}{\longrightarrow}
N(0,1).
$$

The condition $\sigma>0$ ensures that division by the limiting scale is valid.

## Example: Student t distribution

As the degrees of freedom increase, a Student $t$ distribution approaches the standard normal distribution. This is an example of convergence in distribution.

## Common mistakes

- Treating convergence in distribution as numerical convergence of realized values.
- Assuming convergence in distribution automatically gives consistency.
- Forgetting the constant-limit condition in the common form of Slutsky's theorem.
- Dividing by a sequence whose probability limit is zero.
- Forgetting that a consistent estimator can be used inside a limiting distribution through Slutsky.

## Retrieval questions

1. Define convergence in distribution using CDFs.
2. Which implication is always valid: probability convergence to distribution convergence, or the reverse?
3. State the sum, product and ratio forms of Slutsky's theorem.
4. Why does standardizing with consistent mean and scale estimators still give a standard normal limit?
5. How does convergence in distribution enter the CLT?

## Connections

- [Convergence in probability](convergence-in-probability.md)
- [Central Limit Theorem](central-limit-theorem.md)
- [Asymptotic normality](../statistics/asymptotic-normality.md)
- [Consistency](../statistics/consistency.md)

## Sources

- VU Amsterdam, *Knowledge Clip Series: Probability Theory*, Convergence of Random Variables II.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-09-27 | Reviewed CDF convergence, relation to probability convergence and Slutsky's theorem | Reproduce the standardization exercise without notes |
