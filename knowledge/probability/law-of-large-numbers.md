---
title: Law of Large Numbers
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - expectation
  - iid sampling
  - convergence in probability
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 slides
tags:
  - law of large numbers
  - convergence in probability
  - consistency
---

# Law of Large Numbers

## Central question

Why do sample averages become close to population expectations as the sample grows?

## Short answer

A law of large numbers gives conditions under which a sample average converges in probability to the corresponding population mean.

## Intuition

Each observation contains random variation. When many observations are averaged, positive and negative deviations from the population mean tend to offset one another. The average becomes increasingly stable, provided the observations do not have excessive dependence or tails and the relevant expectation exists.

The law does not say every larger sample is closer than the previous one. It says that the probability of a substantial deviation becomes small as the sample size increases.

## A basic iid version

Let $Z_1,\ldots,Z_n$ be iid random variables with

$$
E[|Z_i|]<\infty.
$$

Then

$$
\bar Z_n
=
\frac{1}{n}\sum_{i=1}^n Z_i
\overset{p}{\longrightarrow}
E[Z_i].
$$

The notation $\overset{p}{\longrightarrow}$ means convergence in probability.

## Convergence in probability

A sequence of random variables $W_n$ converges in probability to a constant $c$ when, for every $\varepsilon>0$,

$$
P(|W_n-c|>\varepsilon)\rightarrow 0.
$$

Applied to the sample average, this means that for any fixed tolerance $\varepsilon$, the probability that $\bar Z_n$ differs from the population mean by more than $\varepsilon$ approaches zero.

## What the theorem does not say

It does not say:

- that every finite sample average equals the population mean;
- that the sample average changes monotonically toward the mean;
- that all distributions satisfy the theorem without conditions;
- that one observed sample proves the population expectation;
- that the sample average is unbiased under every sampling scheme.

## Why the finite first moment matters

The target $E[Z_i]$ must be a well-defined finite number. If $E[|Z_i|]=\infty$, the standard iid law of large numbers above cannot be applied.

The Cauchy distribution is the standard warning. Its sample mean does not concentrate around a fixed population mean because no finite population mean exists.

## Use in OLS consistency

For a simple regression without an intercept,

$$
Y_i=\beta X_i+u_i,
$$

the OLS estimator is

$$
\hat\beta_n
=
\frac{\sum_{i=1}^n X_iY_i}
{\sum_{i=1}^n X_i^2}.
$$

Substitute $Y_i=\beta X_i+u_i$:

$$
\hat\beta_n
=
\beta+
\frac{\sum_{i=1}^n X_i u_i}
{\sum_{i=1}^n X_i^2}.
$$

Divide numerator and denominator of the remainder by $n$:

$$
\hat\beta_n
=
\beta+
\frac{\frac{1}{n}\sum_{i=1}^n X_i u_i}
{\frac{1}{n}\sum_{i=1}^n X_i^2}.
$$

Under iid sampling and suitable finite moments, the law of large numbers gives

$$
\frac{1}{n}\sum_{i=1}^n X_i u_i
\overset{p}{\longrightarrow}
E[X_i u_i]
$$

and

$$
\frac{1}{n}\sum_{i=1}^n X_i^2
\overset{p}{\longrightarrow}
E[X_i^2].
$$

If exogeneity implies

$$
E[X_i u_i]=0
$$

and

$$
E[X_i^2]>0,
$$

then the continuous mapping theorem yields

$$
\frac{\frac{1}{n}\sum X_i u_i}
{\frac{1}{n}\sum X_i^2}
\overset{p}{\longrightarrow}
0.
$$

Therefore,

$$
\hat\beta_n\overset{p}{\longrightarrow}\beta.
$$

This is consistency.

## Assumptions and where they are used

### IID or another suitable sampling structure

This allows a law of large numbers to be applied to the sample averages. IID is sufficient, not universally necessary.

### Finite moments

We need the expectations of the averaged quantities to exist. In the OLS proof, this includes quantities such as $X_i u_i$ and $X_i^2$.

### Exogeneity or orthogonality

This makes the probability limit of the numerator zero:

$$
E[X_i u_i]=0.
$$

### Variation in the regressor

The condition

$$
E[X_i^2]>0
$$

prevents the probability limit of the denominator from being zero.

## Law of large numbers versus central limit theorem

The law of large numbers identifies where a sample average goes:

$$
\bar Z_n\overset{p}{\longrightarrow}\mu.
$$

The central limit theorem describes the approximate distribution of its scaled error:

$$
\sqrt{n}(\bar Z_n-\mu).
$$

The LLN is mainly about consistency. The CLT is mainly about uncertainty and inference.

## Example: Bernoulli sample proportion

Let $Z_i$ equal one when observation $i$ is a success and zero otherwise, with $P(Z_i=1)=p$. Then

$$
E[Z_i]=p
$$

and

$$
\bar Z_n=\frac{1}{n}\sum_{i=1}^n Z_i
$$

is the sample proportion of successes. The law of large numbers gives

$$
\bar Z_n\overset{p}{\longrightarrow}p.
$$

## Common mistakes

- Saying the LLN guarantees exact equality in a large finite sample.
- Using the LLN without checking that the relevant expectation exists.
- Confusing convergence in probability with unbiasedness.
- Forgetting that OLS consistency also needs the probability limit of the denominator to be nonzero.
- Treating iid as the only possible condition under which an LLN can hold.
- Assuming the LLN itself provides standard errors or a limiting normal distribution.

## Retrieval questions

1. State a basic iid law of large numbers.
2. Define convergence in probability.
3. Why is a finite first moment required in the stated theorem?
4. How is the LLN used separately on the numerator and denominator of the OLS remainder?
5. Which assumption makes $E[Xu]=0$?
6. Why must $E[X^2]$ be positive?
7. What is the difference between the LLN and the CLT?

## Connections

- [Expectation](expectation.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Central limit theorem](central-limit-theorem.md)
- [Consistency](../statistics/consistency.md)
- [Ordinary least squares](../econometrics/linear-regression/ordinary-least-squares.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on least-squares consistency.
- *Introductory Econometrics for Business and Economics*, Week 2 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Reproduce the OLS consistency argument from the estimator decomposition |
