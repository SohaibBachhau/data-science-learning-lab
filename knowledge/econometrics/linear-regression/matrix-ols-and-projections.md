---
title: Matrix OLS, Projection Matrices and Precision
status: developing
updated: 2026-10-31
sources:
  - IEBE Week 4 lecture slides
  - October 19 study session
tags: [linear-algebra, OLS, projection, covariance]
---

# Matrix OLS, Projection Matrices and Precision

## Central question

How can matrix algebra express and derive multiple-regression OLS, and why are residuals orthogonal to fitted values?

## Set-up and dimensions

Let $n$ be the number of observations and $k$ the number of regressors, excluding the intercept. Set $p=k+1$. Write

$$
Y=X\beta+u,
$$

where $Y$ and $u$ are $n\times1$ vectors, $X$ is an $n\times p$ matrix (its first column is ones when there is an intercept), and $\beta$ is a $p\times1$ coefficient vector. A candidate $b$ has the same dimensions as $\beta$.

The matrix $X'X$ is $p\times p$ and $X'Y$ is $p\times1$, so $(X'X)^{-1}X'Y$ is $p\times1$. We can use this inverse only when $X$ has full column rank.

## Derive the OLS estimator step by step

OLS minimizes the scalar

$$
S(b)=(Y-Xb)'(Y-Xb).
$$

Expanding,

$$
S(b)=Y'Y-Y'Xb-b'X'Y+b'X'Xb.
$$

Why can we combine the middle terms? Both $Y'Xb$ and $b'X'Y$ are $1\times1$ scalars, and transposing a scalar changes nothing:

$$
(Y'Xb)'=b'X'Y.
$$

Therefore,

$$
S(b)=Y'Y-2b'X'Y+b'X'Xb.
$$

The derivative with respect to the **vector** $b$ is

$$
\frac{\partial S}{\partial b}
=-2X'Y+2X'Xb,
$$

using the symmetry $(X'X)'=X'X$. The quadratic term's derivative is linear in $b$ because differentiating a quadratic removes one power of its argument, just as differentiating $x^2$ gives $2x$.

Set the gradient equal to zero:

$$
X'X\hat\beta=X'Y.
$$

If $X'X$ is invertible,

$$
\boxed{\hat\beta=(X'X)^{-1}X'Y.}
$$

Under full column rank this is the unique minimizer, because the quadratic has positive-definite curvature.

## Fitted values, projections and residuals

Define

$$
P=X(X'X)^{-1}X',\qquad M=I_n-P,
$$

where $P$ and $M$ are $n\times n$ matrices and $I_n$ is the identity matrix. Then

$$
\hat Y=X\hat\beta=PY,\qquad \hat u=Y-\hat Y=MY.
$$

$P$ projects the outcome vector onto the column space of $X$. $M$ keeps the component orthogonal to that space.

### Symmetry and idempotence

Because $X'X$ is symmetric, so is its inverse:

$$
P'=P.
$$

Furthermore,

$$
P^2=X(X'X)^{-1}\underbrace{X'X}_{\text{cancels}}(X'X)^{-1}X'=P.
$$

A matrix with $P^2=P$ is **idempotent**: projecting the already projected vector again has no effect.

For $M=I_n-P$,

$$
M'=M,\qquad M^2=(I_n-P)^2=I_n-2P+P^2=I_n-P=M.
$$

Our study exercise explicitly checked this $M^2=M$ identity.

### Residual orthogonality

The normal equations directly imply

$$
X'\hat u=X'(Y-X\hat\beta)=X'Y-X'X\hat\beta=0.
$$

Thus residuals are orthogonal to each regressor column, including the intercept. And because $\hat Y$ lies in the column space of $X$,

$$
\hat Y'\hat u=\hat\beta'X'\hat u=0.
$$

This is an exact **within-sample** property of OLS. It does **not** imply $E[u\mid X]=0$ for the unobserved population errors.

## Sampling decomposition and variance

Substitute the population model $Y=X\beta+u$:

$$
\hat\beta=(X'X)^{-1}X'(X\beta+u)
=\beta+(X'X)^{-1}X'u.
$$

If $E[u\mid X]=0$, then conditional on $X$,

$$
E[\hat\beta\mid X]=\beta.
$$

For a conditional error covariance matrix $\Omega=\operatorname{Var}(u\mid X)$,

$$
\operatorname{Var}(\hat\beta\mid X)
=(X'X)^{-1}X'\Omega X(X'X)^{-1}.
$$

Under conditional homoskedasticity with uncorrelated errors so that $\Omega=\sigma_u^2I_n$, this simplifies:

$$
\boxed{\operatorname{Var}(\hat\beta\mid X)
=\sigma_u^2(X'X)^{-1}.}
$$

Without homoskedasticity, a suitable heteroskedasticity-robust covariance estimator uses squared OLS residuals inside the sandwich, typically with a chosen finite-sample correction:

$$
\widehat V_{\mathrm{HC0}}
=(X'X)^{-1}X'\operatorname{diag}(\hat u_1^2,\ldots,\hat u_n^2)X(X'X)^{-1}.
$$

This robust expression is a **large-sample inference tool**, not an exact variance identity for a finite sample. A conventional or robust standard error for coefficient $j$ is the square root of the corresponding diagonal entry of its estimated covariance matrix.

### Precision intuition

More independent movement in the regressor of interest generally makes its coefficient easier to estimate. When two columns of $X$ are nearly redundant, $(X'X)^{-1}$ can contain large entries, leading to large coefficient variances even when $X'X$ remains invertible.

## Mistakes we resolved

- **Dimensions:** the transpose and inverse must make the product compatible; the output is a vector of $p$ coefficients.
- **Scalar transpose:** $Y'Xb=b'X'Y$ because both sides are equal scalar transposes, not because matrix multiplication commutes generally.
- **Quadratic derivative:** $\partial(b'Ab)/\partial b=(A+A')b$, which is $2Ab$ when $A$ is symmetric.
- **Projection twice:** $P^2=P$ and $M^2=M$, but ordinarily $PM=MP=0$, not $P$.
- **Sample vs population:** $X'\hat u=0$ is guaranteed by the minimization; exogeneity is an assumption.

## Retrieval questions

1. State the dimensions of $Y$, $X$, $b$, $X'X$ and $\hat\beta$.
2. Why are the two cross terms in $S(b)$ equal?
3. Derive the normal equations and the OLS formula.
4. Prove $P^2=P$ and $M^2=M$.
5. Explain geometrically why $X'\hat u=0$.
6. Show precisely where homoskedasticity simplifies the covariance matrix.

## Connections

- [Multiple regression](multiple-regression.md)
- [Multicollinearity and dummy variables](multicollinearity-and-dummies.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)

## Sources and review log

- IEBE Week 4 lecture slides; derivation and projection details extended from October 19, 2026 study session.
- Matrix derivation and orthogonality exercises completed; status `developing`.
