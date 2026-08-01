---
title: Sampling Distribution of OLS
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - ordinary least squares
  - conditional expectation
  - variance and covariance
  - central limit theorem
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - OLS
  - sampling distribution
  - homoskedasticity
  - heteroskedasticity
---

# Sampling Distribution of OLS

## Central question

How does the OLS estimator vary across possible samples, and which assumptions determine its mean, variance and large-sample distribution?

## Short answer

The OLS estimator is random because it is calculated from random data. Its exact properties follow from the decomposition

$$
\hat\beta
=
\beta+(X'X)^{-1}X'u.
$$

Zero conditional mean determines its conditional expectation. The conditional covariance matrix of the errors determines its conditional variance. Central limit theorems provide an approximately normal distribution in large samples.

## Why OLS is random

Before sampling, the observations $(X_i,Y_i)$ are random. Therefore,

$$
\hat\beta=(X'X)^{-1}X'Y
$$

is a random vector. Different random samples generally produce different coefficient estimates.

The sampling distribution describes these possible values and their probabilities under the assumed data-generating process.

## Estimator decomposition

Starting from

$$
Y=X\beta+u,
$$

substitute into the OLS estimator:

$$
\hat\beta
=
(X'X)^{-1}X'(X\beta+u).
$$

Therefore,

$$
\hat\beta
=
\beta+(X'X)^{-1}X'u.
$$

The second term is the estimation error:

$$
\hat\beta-\beta
=
(X'X)^{-1}X'u.
$$

## Conditional expectation

Condition on the full regressor matrix $X$:

$$
E[\hat\beta\mid X]
=
\beta+(X'X)^{-1}X'E[u\mid X].
$$

Under zero conditional mean,

$$
E[u\mid X]=0,
$$

so

$$
E[\hat\beta\mid X]=\beta.
$$

By the law of iterated expectations,

$$
E[\hat\beta]=\beta.
$$

This gives conditional and unconditional unbiasedness.

## Conditional variance in the general case

Because $\beta$ and $X$ are fixed after conditioning on $X$,

$$
\operatorname{Var}(\hat\beta\mid X)
=
\operatorname{Var}((X'X)^{-1}X'u\mid X).
$$

Using the rule $\operatorname{Var}(AZ)=A\operatorname{Var}(Z)A'$,

$$
\operatorname{Var}(\hat\beta\mid X)
=
(X'X)^{-1}X'\Omega X(X'X)^{-1},
$$

where

$$
\Omega=\operatorname{Var}(u\mid X)=E[uu'\mid X]
$$

under zero conditional mean.

This is the general conditional variance formula.

## Homoskedastic and uncorrelated errors

The classical conditional variance assumption is

$$
\operatorname{Var}(u\mid X)=\sigma^2 I_n.
$$

It combines:

- homoskedasticity: every error has conditional variance $\sigma^2$;
- no conditional correlation across observations: off-diagonal conditional covariances are zero.

Substituting into the general formula gives

$$
\operatorname{Var}(\hat\beta\mid X)
=
\sigma^2(X'X)^{-1}.
$$

This simpler formula does not remain valid under heteroskedasticity.

## Heteroskedasticity

Heteroskedasticity means

$$
\operatorname{Var}(u_i\mid X)
$$

is not constant across observations or regressor values.

Under zero conditional mean and suitable sampling assumptions, heteroskedasticity does not by itself bias OLS. However, the classical variance formula is wrong, so conventional standard errors, tests and confidence intervals may be invalid.

Heteroskedasticity-robust standard errors estimate the general sandwich variance rather than imposing $\Omega=\sigma^2I_n$.

## Simple regression variance intuition

For a simple regression with an intercept and homoskedastic errors,

$$
\operatorname{Var}(\hat\beta_1\mid X)
=
\frac{\sigma^2}
{\sum_{i=1}^n(X_i-\bar X)^2}.
$$

The slope is more precise when:

- the error variance $\sigma^2$ is smaller;
- there is more variation in the regressor;
- the sample size increases in a way that increases total regressor variation.

If the observed $X_i$ values are nearly identical, the denominator is small and the slope is imprecisely estimated.

## Exact normality under classical normal errors

If, conditional on $X$,

$$
u\mid X\sim N(0,\sigma^2I_n),
$$

then OLS is a linear transformation of a normal vector. Therefore,

$$
\hat\beta\mid X
\sim
N\left(\beta,\sigma^2(X'X)^{-1}\right).
$$

This is an exact finite-sample conditional distribution.

Normality is not required for OLS to be unbiased or consistent. Its main role here is to deliver exact finite-sample distribution theory.

## Large-sample distribution

Under iid sampling, finite moments, exogeneity and full-rank conditions,

$$
\sqrt{n}(\hat\beta-\beta)
\overset{d}{\longrightarrow}
N(0,V),
$$

where the heteroskedasticity-robust asymptotic variance is

$$
V
=
Q^{-1}SQ^{-1},
$$

with

$$
Q=E[X_iX_i']
$$

and

$$
S=E[X_iX_i'u_i^2].
$$

Here $X_i$ is a column vector of regressors for observation $i$.

The derivation combines:

1. an estimator decomposition;
2. a central limit theorem for $n^{-1/2}\sum X_i u_i$;
3. a law of large numbers for $n^{-1}\sum X_iX_i'$;
4. Slutsky's theorem.

## Estimating the error variance under homoskedasticity

The population error variance $\sigma^2$ is unknown. A common estimator is

$$
\hat\sigma^2
=
\frac{\sum_{i=1}^n\hat u_i^2}{n-k-1},
$$

where $k+1$ is the number of estimated coefficients including the intercept.

The degrees-of-freedom correction accounts for the coefficients estimated from the same data.

The estimated covariance matrix is

$$
\widehat{\operatorname{Var}}(\hat\beta\mid X)
=
\hat\sigma^2(X'X)^{-1}.
$$

Its diagonal elements are estimated coefficient variances. Their square roots are standard errors.

## Standardized statistics

For coefficient $j$, a large-sample statistic for testing

$$
H_0:\beta_j=\beta_{j,0}
$$

is

$$
t_j
=
\frac{\hat\beta_j-\beta_{j,0}}
{\operatorname{SE}(\hat\beta_j)}.
$$

Under the null and suitable conditions,

$$
t_j\overset{d}{\longrightarrow}N(0,1).
$$

An approximate 95 percent confidence interval is

$$
\hat\beta_j
\pm
1.96\operatorname{SE}(\hat\beta_j).
$$

## Finite-sample versus asymptotic statements

- $E[\hat\beta\mid X]=\beta$ is a finite-sample conditional mean result.
- $\operatorname{Var}(\hat\beta\mid X)$ is an exact conditional variance formula under stated assumptions.
- Exact normality requires normal conditional errors.
- Asymptotic normality uses large-sample limit theorems and does not require normal errors.

These claims should not be mixed.

## Common mistakes

- Treating $\hat\beta$ as fixed because one numerical estimate was observed.
- Using the homoskedastic variance formula when errors are heteroskedastic.
- Thinking heteroskedasticity automatically biases OLS.
- Assuming normal errors are required for unbiasedness or consistency.
- Confusing the error variance $\sigma^2$ with a coefficient variance.
- Forgetting that the covariance matrix has off-diagonal elements describing co-movement between coefficient estimates.
- Mixing exact conditional normality with large-sample asymptotic normality.

## Retrieval questions

1. Why is the OLS estimator a random variable?
2. Derive $E[\hat\beta\mid X]$ from the estimator decomposition.
3. Derive the general conditional variance matrix.
4. Which assumption simplifies it to $\sigma^2(X'X)^{-1}$?
5. Why does heteroskedasticity affect standard errors but not necessarily unbiasedness?
6. What conditions give exact conditional normality?
7. Which four ingredients produce the large-sample normal distribution of OLS?

## Connections

- [Ordinary least squares](ordinary-least-squares.md)
- [Exogeneity](exogeneity.md)
- [Variance, covariance and moments](../../probability/variance-covariance-and-moments.md)
- [Sampling distributions](../../statistics/sampling-distributions.md)
- [Unbiasedness](../../statistics/unbiasedness.md)
- [Consistency](../../statistics/consistency.md)
- [Asymptotic normality](../../statistics/asymptotic-normality.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, sections on least-squares estimation, consistency and normality.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Derive the conditional variance matrix and explain every matrix dimension |
