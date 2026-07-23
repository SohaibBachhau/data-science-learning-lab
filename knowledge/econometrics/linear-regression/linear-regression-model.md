---
title: Linear Regression Model
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - random variables
  - conditional expectation
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 and Week 3 slides
tags:
  - linear regression
  - conditional mean
  - error term
---

# Linear Regression Model

## Central question

What does a linear regression equation claim about the relationship between an outcome, regressors and an error term?

## Short answer

A linear regression model decomposes an outcome into a systematic linear component and an error:

$$
Y_i=\beta_0+\beta_1X_i+u_i.
$$

The equation alone is an algebraic decomposition. Its statistical and economic meaning depends on additional assumptions about the conditional distribution of $u_i$ given $X_i$.

## Components

In the simple regression model,

$$
Y_i=\beta_0+\beta_1X_i+u_i,
$$

- $Y_i$ is the dependent variable or outcome;
- $X_i$ is the regressor or explanatory variable;
- $\beta_0$ is the intercept parameter;
- $\beta_1$ is the slope parameter;
- $u_i$ is the error term;
- $i$ indexes observations.

The parameters are fixed but unknown population quantities. The observed data are realizations of the random variables $(X_i,Y_i)$.

## What the error term represents

The error term collects the difference between the observed outcome and the model's systematic component:

$$
u_i=Y_i-\beta_0-\beta_1X_i.
$$

It may contain:

- omitted determinants of $Y_i$;
- unobserved characteristics;
- measurement error;
- unpredictable shocks;
- nonlinear features not represented by the model;
- approximation error.

The presence of an error term guarantees that the equation can reproduce each observed $Y_i$ once $u_i$ is defined as the residual population component. It does not guarantee that the systematic part is correctly specified or useful for prediction, interpretation or causal analysis.

## Linear in variables and linear in parameters

The simple model is linear in both $X$ and the parameters. More generally, a regression is called linear when it is linear in its unknown parameters.

For example,

$$
Y=\beta_0+\beta_1X+\beta_2X^2+u
$$

is nonlinear in $X$ but linear in the parameters $\beta_0,\beta_1,\beta_2$.

By contrast,

$$
Y=\beta_0+e^{\beta_1X}+u
$$

is nonlinear in $\beta_1$.

## Conditional mean interpretation

Take the conditional expectation of the simple model:

$$
E[Y_i\mid X_i]
=
\beta_0+\beta_1X_i+E[u_i\mid X_i].
$$

If

$$
E[u_i\mid X_i]=0,
$$

then

$$
E[Y_i\mid X_i]
=
\beta_0+\beta_1X_i.
$$

Only under this condition does the linear systematic component equal the true conditional mean.

The slope then has the predictive conditional-mean interpretation

$$
E[Y_i\mid X_i=x+1]-E[Y_i\mid X_i=x]=\beta_1.
$$

For a continuous regressor,

$$
\frac{\partial E[Y_i\mid X_i=x]}{\partial x}=\beta_1.
$$

## Intercept interpretation

Under the zero conditional mean assumption,

$$
\beta_0=E[Y_i\mid X_i=0].
$$

This interpretation can be mathematically correct but empirically unhelpful when $X=0$ is outside the relevant data range.

## Multiple regression

With $k$ regressors,

$$
Y_i
=
\beta_0+\beta_1X_{1i}+\cdots+\beta_kX_{ki}+u_i.
$$

In vector notation,

$$
Y_i=X_i'\beta+u_i,
$$

where $X_i$ includes an intercept when appropriate.

Under

$$
E[u_i\mid X_i]=0,
$$

the conditional mean is

$$
E[Y_i\mid X_i]=X_i'\beta.
$$

The coefficient $\beta_j$ measures the change in the conditional mean associated with changing $X_{ji}$ by one unit while holding the other included regressors fixed.

## Population model versus fitted regression

The population model contains unknown parameters and unobserved errors:

$$
Y_i=\beta_0+\beta_1X_i+u_i.
$$

After estimation, the fitted regression is

$$
\hat Y_i=\hat\beta_0+\hat\beta_1X_i.
$$

The sample residual is

$$
\hat u_i=Y_i-\hat Y_i.
$$

The population error $u_i$ and sample residual $\hat u_i$ are not the same object. The residual depends on estimated coefficients and is observable after estimation. The population error depends on unknown parameters and is generally unobservable.

## Predictive versus causal interpretation

A conditional mean relationship is predictive. It tells us how outcomes differ on average across observed values of $X$.

A causal interpretation requires additional assumptions about how $X$ is assigned and whether changes in $X$ can be separated from confounding factors. Zero conditional mean with a sufficiently rich set of controls is one possible route, but its credibility is an empirical and institutional question, not merely an algebraic fact.

## Example: test scores and class size

A simple population model is

$$
\text{TestScore}_i
=
\beta_0+\beta_1\text{STR}_i+u_i,
$$

where $\text{STR}_i$ is the student-teacher ratio.

The error includes other determinants of test scores, such as language background, family characteristics and school resources. If these omitted determinants are related to class size, zero conditional mean may fail and the simple OLS slope may not isolate the intended relationship.

## Common mistakes

- Thinking the presence of $u_i$ automatically makes a model correctly specified.
- Treating the population error and sample residual as identical.
- Interpreting $\beta_1$ causally without additional assumptions.
- Assuming "linear regression" always means the graph is a straight line in every regressor.
- Forgetting that a coefficient in multiple regression holds the other included regressors fixed.
- Giving the intercept an empirical interpretation when $X=0$ is outside the data range.

## Retrieval questions

1. What are the roles of $Y_i$, $X_i$, $\beta$ and $u_i$?
2. Why does including an error term not guarantee correct specification?
3. Which condition turns the systematic component into the conditional mean?
4. What is the difference between an error and a residual?
5. What does "linear in parameters" mean?
6. How does the interpretation of a coefficient change in multiple regression?
7. Why is prediction not automatically causation?

## Connections

- [Conditional expectation](../../probability/conditional-expectation.md)
- [Exogeneity](exogeneity.md)
- [Correct specification](correct-specification.md)
- [Ordinary least squares](ordinary-least-squares.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on the linear regression model.
- *Introductory Econometrics for Business and Economics*, Week 1 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain why the equation and the conditional mean claim are different |
