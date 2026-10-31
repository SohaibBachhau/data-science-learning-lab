---
title: Week 4 - Multiple Regression, Matrix OLS and Assumptions
course: Introductory Econometrics for Business and Economics
status: developing
created: 2026-10-31
updated: 2026-10-31
sources:
  - IEBE Week 4 slides
  - October 19 study session
tags: [OVB, multiple-regression, matrix-OLS, projections, multicollinearity, dummies, adjusted-R-squared]
---

# Week 4: Multiple Regression, Matrix OLS and Assumptions

## What we actually covered

On October 19 we went through the Week 4 learning sequence, including practice with matrix dimensions, algebra, projection and residual-maker identities, omitted-variable-bias signs, full rank, dummy-variable coding, adjusted $R^2$ and the conditional coefficient-variance formula. This course note records the class context and links to full reusable explanations rather than duplicating them.

## 1. Why multiple regression?

A one-regressor estimate can mix the relationship of $X$ with $Y$ and the influence of an omitted $Z$ correlated with $X$. In the population model $Y=\beta_0+\beta_1X+\beta_2Z+u$, the short-regression slope has probability limit

$$
\operatorname{plim}\hat\alpha_1
=\beta_1+\beta_2\frac{\operatorname{Cov}(X,Z)}{\operatorname{Var}(X)},
$$

under the stated exogeneity and sampling assumptions.

Our sign drill: $\beta_2<0$ and $\operatorname{Cov}(X,Z)>0$ give **negative** asymptotic bias. The estimator tends to fall **below** the true partial slope, which does not necessarily mean the estimated slope itself must be negative.

Course example: the STR coefficient changes from about $-2.28$ in a simple regression to $-1.10$ after adding PctEL. Interpret the latter holding PctEL fixed; do not infer causality automatically.

Permanent notes: [OVB](../../../knowledge/econometrics/linear-regression/omitted-variable-bias.md) and [multiple regression](../../../knowledge/econometrics/linear-regression/multiple-regression.md).

## 2. Matrix language and derivation

With $n$ observations, $k$ regressors and an intercept, $X$ is $n\times(k+1)$, $Y$ is $n\times1$ and $\beta$ is $(k+1)\times1$. The least-squares objective is

$$
S(b)=(Y-Xb)'(Y-Xb)
=Y'Y-2b'X'Y+b'X'Xb.
$$

The key explanations we practiced:

- $Y'Xb$ and $b'X'Y$ are **equal scalars**, since transposition preserves a scalar. Matrix multiplication is not generally commutative.
- Differentiating the quadratic term gives $2X'Xb$ because $X'X$ is symmetric.
- Setting the vector gradient to zero gives the normal equations $X'X\hat\beta=X'Y$.
- Under full column rank, $\hat\beta=(X'X)^{-1}X'Y$.

Permanent note: [Matrix OLS and projections](../../../knowledge/econometrics/linear-regression/matrix-ols-and-projections.md).

## 3. Projection and residual-maker matrices

Define $P=X(X'X)^{-1}X'$ and $M=I-P$. They are symmetric and idempotent:

$$
P'=P,\quad P^2=P,\qquad M'=M,\quad M^2=M.
$$

The fitted values are $PY$ and residuals $MY$. We proved $M^2=I-2P+P^2=M$. The normal equations also imply

$$
X'\hat u=0.
$$

This is the sample-residual orthogonality result from optimization. It is **not** a test of the unobserved population restriction $E[u\mid X]=0$.

## 4. Fit, rank and binary regressors

Adjusted $R^2$ penalizes adding regressors:

$$
\bar R^2=1-\frac{n-1}{n-k-1}(1-R^2).
$$

In our numerical comparison with $n=100$:

- Model A: $k=2$, $R^2=0.50$, adjusted $R^2=1-(99/97)(0.50)\approx0.4897$.
- Model B: $k=3$, $R^2=0.51$, adjusted $R^2=1-(99/96)(0.49)\approx0.4947$.

B wins on adjusted fit, too. We corrected a statement about which model had the larger **ordinary** $R^2$.

Perfect multicollinearity means exact dependence among columns and no unique inverse. Strong but imperfect multicollinearity permits OLS but can inflate standard errors. With two exhaustive category indicators $D_A$ and $D_B$ plus an intercept, $D_A+D_B=1$ creates the dummy trap. Omit a reference-category dummy (or omit the intercept and reinterpret coefficients).

Permanent note: [Multicollinearity and dummies](../../../knowledge/econometrics/linear-regression/multicollinearity-and-dummies.md).

## 5. What can we say about uncertainty?

The OLS decomposition is

$$
\hat\beta-\beta=(X'X)^{-1}X'u.
$$

With conditional zero-mean errors, it supports unbiasedness. If the conditional error covariance is $\sigma_u^2I_n$, then

$$
\operatorname{Var}(\hat\beta\mid X)=\sigma_u^2(X'X)^{-1}.
$$

For heteroskedastic errors, the covariance has a sandwich form instead. Homoskedasticity is not what makes the algebraic OLS coefficient exist.

## Quick exam checklist

1. Identify the included and omitted regressors, then calculate the **sign** of OVB.
2. Check the dimensions and full-rank condition before using $(X'X)^{-1}$.
3. Expand the SSE objective and derive the normal equations.
4. Prove symmetry/idempotence and distinguish sample orthogonality from exogeneity.
5. Interpret binary coefficients against the correct baseline.
6. Compute adjusted $R^2$ with $k$ excluding the intercept.
7. State assumptions before claiming unbiasedness or a variance formula.

## Retrieval questions

1. Why is the covariance term divided by $\operatorname{Var}(X)$ in OVB?
2. Prove that $P^2=P$ and $M^2=M$.
3. Why is $Y'Xb=b'X'Y$?
4. What makes $X'X$ noninvertible?
5. Why can adjusted $R^2$ fall after adding a variable?
6. Why do robust SEs change inference, rather than the OLS fitted coefficients?

## Status and source

- **Covered in teaching/practice:** the topics listed here.
- **Still needs review:** harder independent matrix derivations, broader robust-covariance calculations and mixed exam questions.
- Source: IEBE Week 4 slides, paraphrased; October 19 tutoring/practice outcomes.
