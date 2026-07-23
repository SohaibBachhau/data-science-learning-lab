---
title: Exogeneity
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - conditional expectation
  - covariance
  - linear regression model
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - exogeneity
  - zero conditional mean
  - orthogonality
---

# Exogeneity

## Central question

What condition prevents the regression error from varying systematically with the regressors, and why is that condition central to OLS?

## Short answer

A standard regression exogeneity condition is

$$
E[u_i\mid X_i]=0.
$$

It says that for every value of the regressors, the average error is zero. This makes the regression function equal to the conditional mean and supports unbiasedness, consistency and interpretation of OLS coefficients.

## Intuition

The error contains everything affecting $Y$ that is not included in the systematic regression component. Exogeneity requires those omitted influences to balance out on average at every value of $X$.

It does not require the error to be zero for each observation. Positive and negative errors are allowed. The requirement concerns the average error within every regressor group.

## Zero conditional mean

For

$$
Y_i=X_i'\beta+u_i,
$$

the zero conditional mean condition is

$$
E[u_i\mid X_i]=0.
$$

Taking the conditional expectation gives

$$
E[Y_i\mid X_i]
=
X_i'\beta+E[u_i\mid X_i]
=
X_i'\beta.
$$

Thus, the specified linear function equals the true conditional mean.

## Conditional mean independence in a simple regression

For

$$
Y_i=\beta_0+\beta_1X_i+u_i,
$$

zero conditional mean means

$$
E[u_i\mid X_i=x]=0
$$

for every relevant $x$.

This is also called mean independence of $u_i$ from $X_i$. It is weaker than full independence because higher moments or the shape of the error distribution may still depend on $X_i$.

For example, it is possible that

$$
E[u_i\mid X_i]=0
$$

while

$$
\operatorname{Var}(u_i\mid X_i)
$$

changes with $X_i$. This is heteroskedasticity.

## Exogeneity implies unconditional zero mean

By the law of iterated expectations,

$$
E[u_i]
=
E[E[u_i\mid X_i]]
=
0.
$$

The reverse is false. An unconditional mean of zero can result from positive conditional means for some values of $X$ canceling negative conditional means for others.

## Exogeneity implies orthogonality

When the required moments exist,

$$
E[X_i u_i]
=
E[E[X_i u_i\mid X_i]]
=
E[X_iE[u_i\mid X_i]]
=
0.
$$

If $E[u_i]=0$, this gives

$$
\operatorname{Cov}(X_i,u_i)=0.
$$

The reverse is not generally true. Orthogonality is weaker than zero conditional mean.

### Why the reverse can fail

Suppose $X$ is symmetric around zero and

$$
u=X^2-E[X^2].
$$

Then $u$ is a deterministic function of $X$, so

$$
E[u\mid X]=u\neq 0
$$

in general. Yet symmetry may produce

$$
E[Xu]=E[X^3]-E[X]E[X^2]=0.
$$

Thus, $X$ and $u$ can be uncorrelated while the conditional mean of $u$ clearly depends on $X$.

## Exogeneity and OLS unbiasedness

The OLS estimator in matrix form is

$$
\hat\beta
=
\beta+(X'X)^{-1}X'u.
$$

Conditional on $X$,

$$
E[\hat\beta\mid X]
=
\beta+(X'X)^{-1}X'E[u\mid X].
$$

Therefore, if

$$
E[u\mid X]=0,
$$

then

$$
E[\hat\beta\mid X]=\beta.
$$

The assumption eliminates the expected estimation remainder.

## Exogeneity and OLS consistency

For consistency, a weaker moment condition can be sufficient:

$$
E[X_i u_i]=0.
$$

Together with sampling, finite-moment and identification conditions, this makes the probability limit of the OLS numerator zero.

Thus, the assumptions commonly used for finite-sample unbiasedness can be stronger than those required for consistency.

## Exogeneity with the full regressor sample

In random-regressor finite-sample derivations, the course uses a condition such as

$$
E[u_i\mid X_1,\ldots,X_n]=0.
$$

In matrix notation,

$$
E[u\mid X]=0.
$$

This conditions on the entire observed regressor matrix and directly supports conditional unbiasedness.

## Strict exogeneity in panel data

For a panel model,

$$
Y_{it}=\beta X_{it}+\alpha_i+u_{it},
$$

a common assumption is

$$
E[u_{it}\mid X_{i1},\ldots,X_{iT},\alpha_i]=0.
$$

This says the current error has mean zero given the entity's entire regressor history and its fixed effect. It is stronger than conditioning only on the current regressor $X_{it}$.

## Sources of exogeneity failure

### Omitted variables

If an omitted determinant of $Y$ is correlated with $X$, it becomes part of $u$ and causes

$$
E[u\mid X]\neq 0.
$$

### Simultaneity

If $X$ and $Y$ are jointly determined, shocks to $Y$ can be related to $X$.

### Measurement error

Measurement error in a regressor can create dependence between the observed regressor and the composite error.

### Sample selection

Selection into the observed sample can make the error distribution depend on the regressors.

### Incorrect functional form

If the true conditional mean is nonlinear but a linear function is imposed, the omitted nonlinear component enters the error and can have nonzero conditional mean.

## Predictive and causal meaning

Zero conditional mean gives the coefficient a conditional-mean predictive interpretation. A causal interpretation additionally requires that the conditioning set removes relevant confounding and that the variation in $X$ corresponds to the causal comparison of interest.

The mathematical condition is precise, but whether it is credible depends on the economic setting and data collection process.

## Common mistakes

- Interpreting exogeneity as $u_i=0$.
- Treating $E[u_i]=0$ as sufficient.
- Treating zero covariance as equivalent to zero conditional mean.
- Thinking exogeneity requires homoskedasticity or normality.
- Assuming the existence of an error term makes the regressors exogenous.
- Giving a causal interpretation solely because OLS was used.
- Forgetting that panel-data strict exogeneity conditions on the full regressor history.

## Retrieval questions

1. State the zero conditional mean assumption in words and symbols.
2. Why does it imply that the linear regression function equals $E[Y\mid X]$?
3. Why does it imply $E[Xu]=0$?
4. Why does $E[Xu]=0$ not generally imply $E[u\mid X]=0$?
5. How is exogeneity used in the OLS unbiasedness proof?
6. Name four mechanisms that can violate exogeneity.
7. What is strict exogeneity in a panel model?

## Connections

- [Conditional expectation](../../probability/conditional-expectation.md)
- [Variance, covariance and moments](../../probability/variance-covariance-and-moments.md)
- [Linear regression model](linear-regression-model.md)
- [Correct specification](correct-specification.md)
- [Ordinary least squares](ordinary-least-squares.md)
- [Unbiasedness](../../statistics/unbiasedness.md)
- [Consistency](../../statistics/consistency.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on the linear regression model.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.
- *Introductory Econometrics for Business and Economics*, Week 6 slides for strict exogeneity in panel data.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain the hierarchy from zero conditional mean to orthogonality |
