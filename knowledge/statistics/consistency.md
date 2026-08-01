---
title: Consistency
subject: statistics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - estimators
  - convergence in probability
  - law of large numbers
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 slides
tags:
  - consistency
  - probability limits
  - asymptotics
---

# Consistency

## Central question

Does an estimator become arbitrarily close to the true parameter with high probability as the sample size grows?

## Short answer

An estimator $\hat\theta_n$ is consistent for $\theta$ when

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta.
$$

This means that the probability of an estimation error larger than any fixed tolerance approaches zero as $n$ increases.

## Formal definition

For every $\varepsilon>0$,

$$
P(|\hat\theta_n-\theta|>\varepsilon)
\rightarrow 0
$$

as

$$
n\rightarrow\infty.
$$

Equivalently,

$$
P(|\hat\theta_n-\theta|\leq\varepsilon)
\rightarrow 1.
$$

## Intuition

Consistency is a large-sample reliability property. It does not require the estimator to be exactly correct in a finite sample. It says that with enough suitable data, the estimator concentrates around its target.

A consistent estimator can still perform poorly when $n$ is small. Consistency alone does not describe how quickly the estimator approaches the parameter.

## Example: sample mean

Under a law of large numbers, if $X_1,\ldots,X_n$ are iid and

$$
E[|X_i|]<\infty,
$$

then

$$
\bar X_n
=
\frac{1}{n}\sum_{i=1}^nX_i
\overset{p}{\longrightarrow}
E[X_i].
$$

Therefore, the sample mean is consistent for the population mean.

## OLS consistency

For the simple regression without an intercept,

$$
Y_i=\beta X_i+u_i,
$$

the OLS estimator satisfies

$$
\hat\beta_n
=
\beta+
\frac{\frac{1}{n}\sum_{i=1}^nX_i u_i}
{\frac{1}{n}\sum_{i=1}^nX_i^2}.
$$

Under an appropriate law of large numbers,

$$
\frac{1}{n}\sum_{i=1}^nX_i u_i
\overset{p}{\longrightarrow}
E[X_i u_i]
$$

and

$$
\frac{1}{n}\sum_{i=1}^nX_i^2
\overset{p}{\longrightarrow}
E[X_i^2].
$$

If

$$
E[X_i u_i]=0
$$

and

$$
E[X_i^2]>0,
$$

then

$$
\hat\beta_n
\overset{p}{\longrightarrow}
\beta.
$$

The proof works because the random remainder converges in probability to zero.

## Assumptions and their roles

### Sampling and dependence conditions

An iid assumption is one sufficient condition for applying a standard law of large numbers. More general weak-dependence assumptions can also deliver consistency.

### Finite moments

The expectations to which the sample averages converge must exist. In the displayed OLS argument, the relevant quantities include $X_i u_i$ and $X_i^2$.

### Exogeneity or orthogonality

The condition

$$
E[X_i u_i]=0
$$

makes the numerator's probability limit zero.

A stronger conditional assumption such as

$$
E[u_i\mid X_i]=0
$$

implies this orthogonality when the moments exist.

### Identification

The condition

$$
E[X_i^2]>0
$$

ensures that the denominator does not converge to zero. More generally, the data must contain enough variation to distinguish the parameter.

## Correct specification and pseudo-true limits

An estimator can converge even when the model is incorrectly specified. In that case, it may converge to a pseudo-true parameter rather than the structural or conditional-mean parameter the researcher intended.

Consistency must therefore always be stated with its target:

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta_0.
$$

Saying only that an estimator is "consistent" is incomplete unless the estimand is clear.

## Consistency versus unbiasedness

Unbiasedness is a finite-sample expectation property:

$$
E[\hat\theta_n]=\theta.
$$

Consistency is a limiting concentration property:

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta.
$$

A consistent estimator can be biased in finite samples if the bias disappears as $n$ grows. An unbiased estimator need not be consistent if its variance does not shrink.

## A sufficient mean squared error condition

If

$$
E[(\hat\theta_n-\theta)^2]\rightarrow 0,
$$

then $\hat\theta_n$ is consistent by Markov's inequality.

Because

$$
E[(\hat\theta_n-\theta)^2]
=
\operatorname{Var}(\hat\theta_n)
+
\operatorname{Bias}(\hat\theta_n)^2,
$$

it is sufficient that both variance and squared bias approach zero.

## Continuous mapping

If

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta
$$

and $g$ is continuous at $\theta$, then

$$
g(\hat\theta_n)\overset{p}{\longrightarrow}g(\theta).
$$

This allows consistency to pass through continuous transformations such as addition, multiplication, division by a nonzero limit and square roots of positive quantities.

## Common mistakes

- Interpreting consistency as a guarantee for one finite sample.
- Saying an estimator is consistent without identifying its limiting target.
- Confusing consistency with unbiasedness.
- Assuming more observations solve omitted-variable bias or another persistent specification problem.
- Applying a law of large numbers without checking moments or dependence.
- Forgetting the identification condition that keeps the denominator away from zero.
- Assuming convergence of numerator and denominator automatically permits division when the denominator limit is zero.

## Retrieval questions

1. Define consistency using an $\varepsilon$ probability statement.
2. What does consistency say, and what does it not say, about finite samples?
3. Reproduce the OLS estimator decomposition used in its consistency proof.
4. Which condition makes the numerator's probability limit zero?
5. Why must the denominator have a nonzero limit?
6. Can an incorrectly specified estimator converge? If so, to what kind of target?
7. What is the relationship between mean squared error convergence and consistency?

## Connections

- [Unbiasedness](unbiasedness.md)
- [Asymptotic normality](asymptotic-normality.md)
- [Law of large numbers](../probability/law-of-large-numbers.md)
- [Correct specification](../econometrics/linear-regression/correct-specification.md)
- [Ordinary least squares](../econometrics/linear-regression/ordinary-least-squares.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on least-squares consistency.
- *Introductory Econometrics for Business and Economics*, Week 2 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain every assumption in the OLS consistency proof |
