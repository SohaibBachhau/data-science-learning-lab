---
title: Efficiency of Estimators
subject: statistics
status: developing
created: 2026-09-27
updated: 2026-09-27
last_reviewed: 2026-09-27
prerequisites:
  - estimators
  - sampling distributions
  - unbiasedness
sources:
  - VU Knowledge Clip Series: Statistics, Bias and Consistency of Estimators
tags:
  - efficiency
  - variance
  - estimator properties
---

# Efficiency of Estimators

## Central question

If two estimators are both centered on the correct parameter, which one gives more precise estimates across repeated samples?

## Short answer

In the course framing, when comparing unbiased estimators of the same parameter, the estimator with the smaller variance is more efficient.

A smaller variance means a tighter sampling distribution around the target.

## Intuition

Two estimators can both be unbiased but use the sample information very differently.

An estimator that uses only one observation can be centered correctly, yet fluctuate much more from sample to sample than an estimator that averages all observations.

Efficiency is therefore about precision, not about whether the center is correct.

## Example: estimators of a population mean

Let $X_1,\ldots,X_n$ be iid with

$$
E[X_i]=\mu
$$

and

$$
\operatorname{Var}(X_i)=\sigma^2.
$$

The sample mean

$$
\hat\mu_1=\bar X
$$

is unbiased and has

$$
\operatorname{Var}(\hat\mu_1)=\frac{\sigma^2}{n}.
$$

The estimator

$$
\hat\mu_4=X_1
$$

is also unbiased, but

$$
\operatorname{Var}(\hat\mu_4)=\sigma^2.
$$

So for $n>1$, the sample mean is more efficient.

Another unbiased estimator is

$$
\hat\mu_5=\frac{X_1+X_n}{2}.
$$

Using independence,

$$
\operatorname{Var}(\hat\mu_5)
=
\frac{1}{4}(\sigma^2+\sigma^2)
=
\frac{\sigma^2}{2}.
$$

For $n>2$,

$$
\frac{\sigma^2}{n}<\frac{\sigma^2}{2}<\sigma^2,
$$

so the full sample mean is the most precise of these three estimators.

## Unbiasedness, consistency and efficiency

These properties answer different questions:

- unbiasedness: is the estimator centered correctly at a given sample size?
- consistency: does the estimator converge to the target as the sample grows?
- efficiency: how tightly does the estimator vary around its target relative to alternatives?

One property does not replace the others.

## Common mistakes

- Thinking every unbiased estimator is equally good.
- Confusing low variance with low bias.
- Calling an estimator efficient without specifying the comparison class or target.
- Forgetting that using more independent information can reduce variance.

## Retrieval questions

1. How is efficiency defined in the course comparison of unbiased estimators?
2. Why is $X_1$ unbiased for $\mu$ but inefficient relative to $\bar X$?
3. Compute the variance of $(X_1+X_n)/2$ under iid sampling.
4. How do unbiasedness, consistency and efficiency differ?

## Connections

- [Unbiasedness](unbiasedness.md)
- [Consistency](consistency.md)
- [Sampling distributions](sampling-distributions.md)
- [Parameters, estimators and estimates](parameters-estimators-and-estimates.md)

## Sources

- VU Amsterdam, *Knowledge Clip Series: Statistics*, Bias and Consistency of Estimators.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-09-27 | Added after reviewing the three desirable estimator properties and mean-estimator exercises | Compare variances of several unbiased estimators from memory |
