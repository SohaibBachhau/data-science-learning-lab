---
title: Unbiasedness
subject: statistics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - parameters estimators and estimates
  - expectation
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - unbiasedness
  - finite sample
  - estimator properties
---

# Unbiasedness

## Central question

Is an estimator centered on the true parameter across repeated samples of a fixed size?

## Short answer

An estimator $\hat\theta_n$ is unbiased for $\theta$ when

$$
E[\hat\theta_n]=\theta.
$$

This is a finite-sample statement about the center of the estimator's sampling distribution.

## Intuition

Imagine repeating the sampling process many times, always using samples of the same size $n$. If the estimates average to the true parameter, the estimator is unbiased.

An individual estimate can still be far from the truth. Unbiasedness does not guarantee accuracy in one sample.

## Bias

The bias of an estimator is

$$
\operatorname{Bias}(\hat\theta_n)
=
E[\hat\theta_n]-\theta.
$$

The estimator is unbiased when this quantity equals zero.

Bias can depend on sample size. An estimator may be biased for every finite $n$ while the bias approaches zero as $n$ grows.

## Example: sample mean

For iid observations with finite expectation $E[X_i]=\mu$,

$$
\bar X_n=\frac{1}{n}\sum_{i=1}^n X_i.
$$

By linearity of expectation,

$$
E[\bar X_n]
=
\frac{1}{n}\sum_{i=1}^n E[X_i]
=
\frac{1}{n}\sum_{i=1}^n \mu
=
\mu.
$$

Therefore, the sample mean is unbiased for the population mean.

Independence is not needed for this expectation calculation. Identical means and existence of the expectations are enough. Independence becomes important for other properties such as its usual variance formula and large-sample results.

## Conditional unbiasedness of OLS

For the multiple regression model

$$
Y=X\beta+u,
$$

the OLS estimator is

$$
\hat\beta=(X'X)^{-1}X'Y.
$$

Substituting the model gives

$$
\hat\beta
=
\beta+(X'X)^{-1}X'u.
$$

Condition on the regressor matrix $X$:

$$
E[\hat\beta\mid X]
=
\beta+(X'X)^{-1}X'E[u\mid X].
$$

If

$$
E[u\mid X]=0,
$$

then

$$
E[\hat\beta\mid X]=\beta.
$$

Applying the law of iterated expectations,

$$
E[\hat\beta]
=
E[E[\hat\beta\mid X]]
=
\beta.
$$

Thus, conditional unbiasedness implies unconditional unbiasedness.

## Where the assumptions are used

### Zero conditional mean

The condition $E[u\mid X]=0$ eliminates the expected OLS remainder term.

### Full column rank

The matrix $X'X$ must be invertible for the displayed OLS estimator to be uniquely defined.

### Existence of expectations

The relevant expectations must be finite.

Homoskedasticity and normality are not required for the unbiasedness derivation above.

## Unbiasedness versus consistency

Unbiasedness concerns the expected value at a given sample size:

$$
E[\hat\theta_n]=\theta.
$$

Consistency concerns the probability that the estimator is close to the parameter as sample size grows:

$$
\hat\theta_n\overset{p}{\longrightarrow}\theta.
$$

Neither property automatically implies the other.

An unbiased estimator can remain highly variable and therefore fail to become concentrated around the parameter. A biased estimator can be consistent if its bias and variance vanish as $n$ increases.

## Bias versus variance

The mean squared error is

$$
E[(\hat\theta_n-\theta)^2]
=
\operatorname{Var}(\hat\theta_n)
+
\operatorname{Bias}(\hat\theta_n)^2.
$$

This decomposition shows why zero bias is not the only goal. A slightly biased estimator with much lower variance can have lower mean squared error.

## Failure case: omitted variable bias

Suppose the true model contains an omitted factor $Z$ that affects $Y$ and is correlated with the included regressor $X$. Then the omitted factor becomes part of the regression error, causing

$$
E[u\mid X]\neq 0.
$$

The OLS remainder no longer has conditional expectation zero, so the OLS slope is generally biased.

The mere presence of an error term does not prevent bias. The relationship between the error and regressors is decisive.

## Common mistakes

- Interpreting unbiasedness as "the estimate equals the truth."
- Thinking unbiasedness improves automatically when the sample grows.
- Confusing unbiasedness with consistency.
- Believing normal errors are required for OLS unbiasedness.
- Assuming $E[u]=0$ is enough for OLS unbiasedness.
- Ignoring the estimator's variance when judging its quality.

## Retrieval questions

1. Define the bias of an estimator.
2. Why can an unbiased estimate still be far from the true parameter?
3. Derive conditional unbiasedness of OLS from its estimator decomposition.
4. Which assumption sets the expected OLS remainder to zero?
5. Why are homoskedasticity and normality unnecessary for this derivation?
6. What is the difference between unbiasedness and consistency?
7. State the bias-variance decomposition of mean squared error.

## Connections

- [Parameters, estimators and estimates](parameters-estimators-and-estimates.md)
- [Sampling distributions](sampling-distributions.md)
- [Consistency](consistency.md)
- [Conditional expectation](../probability/conditional-expectation.md)
- [Exogeneity](../econometrics/linear-regression/exogeneity.md)
- [Sampling distribution of OLS](../econometrics/linear-regression/sampling-distribution-of-ols.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Derive OLS unbiasedness and name each assumption used |
