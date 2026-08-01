---
title: Ordinary Least Squares
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - linear regression model
  - differentiation
  - sample averages
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 and Week 3 slides
tags:
  - ordinary least squares
  - OLS
  - estimation
---

# Ordinary Least Squares

## Central question

How does ordinary least squares choose coefficient estimates from a sample, and which properties follow from the minimization problem alone?

## Short answer

Ordinary least squares chooses the coefficient values that minimize the sum of squared sample residuals. The minimization determines the fitted line and creates exact sample identities. Statistical properties such as unbiasedness, consistency and normality require additional assumptions about the data-generating process.

## Simple regression objective

For the model

$$
Y_i=\beta_0+\beta_1X_i+u_i,
$$

define the residual produced by candidate coefficients $b_0,b_1$ as

$$
e_i(b_0,b_1)=Y_i-b_0-b_1X_i.
$$

OLS solves

$$
(\hat\beta_0,\hat\beta_1)
=
\arg\min_{b_0,b_1}
\sum_{i=1}^n(Y_i-b_0-b_1X_i)^2.
$$

Squaring prevents positive and negative residuals from canceling and penalizes larger residuals more heavily.

## Derivation of the normal equations

The sum of squared residuals is

$$
SSR(b_0,b_1)
=
\sum_{i=1}^n(Y_i-b_0-b_1X_i)^2.
$$

Differentiate with respect to $b_0$:

$$
\frac{\partial SSR}{\partial b_0}
=
-2\sum_{i=1}^n(Y_i-b_0-b_1X_i).
$$

At the minimum,

$$
\sum_{i=1}^n\hat u_i=0,
$$

where

$$
\hat u_i=Y_i-\hat\beta_0-\hat\beta_1X_i.
$$

Differentiate with respect to $b_1$:

$$
\frac{\partial SSR}{\partial b_1}
=
-2\sum_{i=1}^nX_i(Y_i-b_0-b_1X_i).
$$

At the minimum,

$$
\sum_{i=1}^nX_i\hat u_i=0.
$$

These are the normal equations.

## Closed-form simple-regression estimators

Solving the normal equations gives

$$
\hat\beta_1
=
\frac{\sum_{i=1}^n(X_i-\bar X)(Y_i-\bar Y)}
{\sum_{i=1}^n(X_i-\bar X)^2}
$$

and

$$
\hat\beta_0
=
\bar Y-\hat\beta_1\bar X.
$$

The slope is sample covariance divided by sample variation in $X$, using the same unnormalized sums in numerator and denominator.

The denominator must be positive:

$$
\sum_{i=1}^n(X_i-\bar X)^2>0.
$$

Thus, the regressor must vary in the sample.

## Interpretation of the fitted values and residuals

The fitted value is

$$
\hat Y_i=\hat\beta_0+\hat\beta_1X_i.
$$

The residual is

$$
\hat u_i=Y_i-\hat Y_i.
$$

The fitted regression summarizes the sample relationship. It is not automatically the true population conditional mean.

## Exact sample identities with an intercept

When the model includes an intercept, OLS guarantees:

$$
\sum_{i=1}^n\hat u_i=0,
$$

$$
\sum_{i=1}^nX_i\hat u_i=0,
$$

$$
\bar{\hat Y}=\bar Y,
$$

and the fitted line passes through

$$
(\bar X,\bar Y).
$$

These are algebraic consequences of minimization. They do not prove population exogeneity.

In particular, the sample identity

$$
\frac{1}{n}\sum_{i=1}^n\hat u_i=0
$$

is not evidence that

$$
E[u_i\mid X_i]=0.
$$

## Matrix notation

For multiple regression, write

$$
Y=X\beta+u,
$$

where:

- $Y$ is an $n\times 1$ outcome vector;
- $X$ is an $n\times(k+1)$ regressor matrix when an intercept is included;
- $\beta$ is a $(k+1)\times 1$ parameter vector;
- $u$ is an $n\times 1$ error vector.

OLS minimizes

$$
S(b)=(Y-Xb)'(Y-Xb).
$$

Expand:

$$
S(b)=Y'Y-2b'X'Y+b'X'Xb.
$$

Differentiate with respect to $b$:

$$
\frac{\partial S(b)}{\partial b}
=
-2X'Y+2X'Xb.
$$

The first-order condition is

$$
X'X\hat\beta=X'Y.
$$

If $X'X$ is invertible,

$$
\hat\beta=(X'X)^{-1}X'Y.
$$

## Full-rank condition

The matrix $X'X$ is invertible when the columns of $X$ are linearly independent. Perfect multicollinearity violates this condition.

Examples include:

- including the same regressor twice;
- including an intercept and all categories of an exhaustive dummy-variable set;
- including a regressor that is an exact linear combination of others.

Imperfect multicollinearity does not prevent estimation, but it can make coefficient estimates imprecise.

## Estimator decomposition

Substitute the population model into OLS:

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

This decomposition separates the true parameter from the random estimation error. It is the starting point for derivations of unbiasedness, variance, consistency and asymptotic normality.

## OLS as a projection

The fitted vector is

$$
\hat Y=X\hat\beta
=X(X'X)^{-1}X'Y.
$$

Define the projection matrix

$$
P_X=X(X'X)^{-1}X'.
$$

Then

$$
\hat Y=P_XY.
$$

The residual vector is

$$
\hat u=Y-\hat Y=(I-P_X)Y.
$$

The normal equations imply

$$
X'\hat u=0.
$$

Geometrically, the residual vector is orthogonal to every column of $X$.

## Why least squares?

OLS is attractive because:

- it often has a closed-form solution;
- it is computationally simple;
- its geometry is clear;
- under suitable assumptions it has strong statistical properties;
- with normal homoskedastic errors it coincides with maximum likelihood for the regression coefficients.

These advantages do not make squared loss universally appropriate. Outliers can have large influence, and different objectives may be preferable for different targets or distributions.

## Sample fit

The total sum of squares is

$$
TSS=\sum_{i=1}^n(Y_i-\bar Y)^2.
$$

The explained sum of squares is

$$
ESS=\sum_{i=1}^n(\hat Y_i-\bar Y)^2.
$$

The residual sum of squares is

$$
SSR=\sum_{i=1}^n\hat u_i^2.
$$

With an intercept,

$$
TSS=ESS+SSR.
$$

The coefficient of determination is

$$
R^2=1-\frac{SSR}{TSS}.
$$

A high $R^2$ indicates strong in-sample fit relative to a mean-only benchmark. It does not establish causality, correct specification or out-of-sample performance.

## Common mistakes

- Thinking OLS assumptions are needed for the minimization formula itself.
- Treating sample residual orthogonality as proof of population exogeneity.
- Confusing the population error $u_i$ with the residual $\hat u_i$.
- Forgetting that $X'X$ must be invertible.
- Treating high $R^2$ as proof that a model is correct.
- Assuming OLS is robust to extreme outliers because it uses all observations.
- Interpreting an estimated association as causal without additional assumptions.

## Retrieval questions

1. State the OLS minimization problem.
2. Derive the two simple-regression normal equations.
3. Why does the fitted line pass through $(\bar X,\bar Y)$?
4. Derive the matrix OLS estimator.
5. What does the condition $X'\hat u=0$ mean geometrically?
6. Which sample identities follow from OLS and which population assumptions do not?
7. Write the OLS estimator decomposition and explain why it is useful.

## Connections

- [Linear regression model](linear-regression-model.md)
- [Exogeneity](exogeneity.md)
- [Correct specification](correct-specification.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)
- [Unbiasedness](../../statistics/unbiasedness.md)
- [Consistency](../../statistics/consistency.md)
- [Maximum likelihood](../maximum-likelihood/maximum-likelihood.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on the least-squares estimator.
- *Introductory Econometrics for Business and Economics*, Week 1 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Derive simple and matrix OLS without copying formulas |
