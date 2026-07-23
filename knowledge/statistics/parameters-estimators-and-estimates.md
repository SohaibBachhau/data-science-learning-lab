---
title: Parameters, Estimators and Estimates
subject: statistics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - random variables
  - sampling
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 and Week 2 slides
tags:
  - parameters
  - estimators
  - estimates
  - sampling
---

# Parameters, Estimators and Estimates

## Central question

What is the difference between a population parameter, an estimator and the numerical estimate obtained from one sample?

## Short answer

A parameter is a fixed but usually unknown feature of a population or model. An estimator is a rule, based on random sample data, for learning about that parameter. An estimate is the numerical value produced by the estimator after a particular sample has been observed.

## Parameter

A parameter is a nonrandom quantity that characterizes the population or the assumed probability model.

Examples include:

$$
\mu=E[X],
$$

$$
\sigma^2=\operatorname{Var}(X),
$$

and a regression coefficient $\beta$.

In frequentist statistics, the parameter is fixed. Our uncertainty concerns its unknown value, not randomness in the parameter itself.

## Estimator

An estimator is a function of random sample variables:

$$
\hat\theta_n=T(X_1,\ldots,X_n).
$$

Before the sample is observed, $X_1,\ldots,X_n$ are random variables. Therefore, $\hat\theta_n$ is also a random variable and has a sampling distribution.

The subscript $n$ emphasizes that the estimator can depend on sample size.

## Estimate

After the observed values $x_1,\ldots,x_n$ are inserted into the estimator, we obtain

$$
\hat\theta_n=T(x_1,\ldots,x_n).
$$

The result is a realized estimate, a number rather than a random variable.

The same symbol is commonly used for the estimator and its realized value. The surrounding context must clarify which meaning is intended.

## Example: sample mean

The population parameter is

$$
\mu=E[X].
$$

The estimator is

$$
\bar X_n=\frac{1}{n}\sum_{i=1}^n X_i.
$$

If the observed values are $2$, $4$ and $6$, the estimate is

$$
\bar x_3=\frac{2+4+6}{3}=4.
$$

A different random sample would generally produce a different estimate.

## Example: OLS slope

In a simple regression, $\beta_1$ is the unknown population slope. The OLS estimator with an intercept is

$$
\hat\beta_1
=
\frac{\sum_{i=1}^n (X_i-\bar X)(Y_i-\bar Y)}
{\sum_{i=1}^n (X_i-\bar X)^2}.
$$

Before sampling, this is a random variable because it depends on the random observations. After observing the sample, it becomes a numerical slope estimate.

## Estimand

The estimand is the precise population quantity the analysis aims to estimate. For example, the estimand might be:

- the population mean $E[Y]$;
- the best linear projection coefficient;
- a conditional mean effect;
- a causal effect under specified assumptions.

Being explicit about the estimand prevents confusion about what an estimator is supposed to recover.

## Estimation error

The estimation error is

$$
\hat\theta_n-\theta.
$$

It is random before the sample is observed. Statistical properties such as bias, variance, mean squared error and consistency describe this error across repeated hypothetical samples.

## Standard error

The standard deviation of an estimator is

$$
\operatorname{SD}(\hat\theta_n).
$$

Because it usually depends on unknown population quantities, it must be estimated. The resulting estimate is called the standard error:

$$
\operatorname{SE}(\hat\theta_n).
$$

A standard error measures estimated sampling uncertainty. It is not the same as the standard deviation of the raw data or the standard deviation of regression residuals.

## Properties of estimators

Important properties include:

- unbiasedness: whether $E[\hat\theta_n]=\theta$;
- variance: how dispersed estimates are across samples;
- mean squared error: expected squared estimation error;
- consistency: whether $\hat\theta_n$ approaches $\theta$ as $n$ grows;
- asymptotic normality: whether a scaled estimation error approaches a normal distribution.

No single property fully determines whether an estimator is useful.

## Common mistakes

- Calling an unknown parameter random in a frequentist derivation.
- Treating the estimate from one sample as the true parameter.
- Forgetting that an estimator has a distribution across possible samples.
- Confusing the standard error of an estimator with the standard deviation of observations.
- Using the same symbol without stating whether it denotes the random estimator or the realized estimate.
- Discussing estimator quality without identifying the estimand.

## Retrieval questions

1. What is the difference between a parameter, estimator and estimate?
2. Why is an estimator a random variable?
3. What is an estimand?
4. What is estimation error?
5. Why does a different sample usually produce a different estimate?
6. What is the difference between an estimator's standard deviation and its estimated standard error?

## Connections

- [Sampling distributions](sampling-distributions.md)
- [Unbiasedness](unbiasedness.md)
- [Consistency](consistency.md)
- [Asymptotic normality](asymptotic-normality.md)
- [Ordinary least squares](../econometrics/linear-regression/ordinary-least-squares.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1.
- *Introductory Econometrics for Business and Economics*, Week 1 and Week 2 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Give one original example of a parameter, estimator and estimate |
