---
title: Correct Specification
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - conditional expectation
  - linear regression model
  - exogeneity
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 3 and Week 4 slides
tags:
  - correct specification
  - misspecification
  - conditional mean
---

# Correct Specification

## Central question

When does a regression model represent the relevant feature of the population correctly, and why does an error term not guarantee correct specification?

## Short answer

A model is correctly specified for a particular target when its functional form, included variables, probability assumptions and parameter interpretation match the population feature being modeled. For a linear conditional mean model, correct specification requires

$$
E[Y\mid X]=X'\beta
$$

for some parameter vector $\beta$. Equivalently, with

$$
u=Y-X'\beta,
$$

it requires

$$
E[u\mid X]=0.
$$

## Why the error term does not guarantee correctness

For any chosen values of $\beta$, one can define

$$
u=Y-X'\beta.
$$

Then the identity

$$
Y=X'\beta+u
$$

holds exactly for every observation.

This algebraic identity says nothing by itself about whether $X'\beta$ equals the conditional mean, whether $\beta$ has the intended interpretation or whether the model supports valid inference.

The statistical content comes from restrictions on $u$, such as

$$
E[u\mid X]=0.
$$

Without such a restriction, the error may contain systematic patterns that the model should have represented explicitly.

## Correct conditional mean specification

A linear conditional mean is correctly specified when there exists a vector $\beta_0$ such that

$$
E[Y\mid X]=X'\beta_0.
$$

Define

$$
u=Y-X'\beta_0.
$$

Then

$$
E[u\mid X]
=
E[Y-X'\beta_0\mid X]
=
E[Y\mid X]-X'\beta_0
=
0.
$$

Thus, correct conditional mean specification and zero conditional mean are equivalent when the error is defined relative to the claimed conditional mean.

## Specification is relative to a target

A model can be correct for one purpose and incomplete for another.

Examples:

- A model may correctly describe $E[Y\mid X]$ without describing the conditional variance.
- A linear projection may be useful for prediction even when the true conditional mean is nonlinear.
- A predictive relationship may be correctly estimated but not have a causal interpretation.
- A conditional mean may be correct while a normal likelihood is incorrectly specified.

Therefore, the phrase "correctly specified" should identify which part of the data-generating process is being modeled.

## Sources of conditional mean misspecification

### Omitted relevant variables

Suppose the true conditional mean is

$$
E[Y\mid X,Z]
=
\beta_0+\beta_1X+\gamma Z.
$$

If $Z$ is omitted and related to $X$, the error contains $\gamma Z$ and generally satisfies

$$
E[u\mid X]\neq 0.
$$

### Incorrect functional form

Suppose

$$
E[Y\mid X]
=
\beta_0+\beta_1X+\beta_2X^2.
$$

A model containing only an intercept and $X$ leaves the systematic term $\beta_2X^2$ in the error. The average error then changes with $X$.

### Incorrect interactions

The effect of $X$ may depend on another variable $Z$. Omitting an interaction term can impose a constant slope when the true conditional mean has different slopes across values of $Z$.

### Incorrect dynamics

In time-series or panel settings, omitted lags, feedback or persistent entity effects can make the current error predictable from included regressors or their histories.

## Error, disturbance and residual

The population error is

$$
u=Y-X'\beta_0.
$$

It is generally unobserved because $\beta_0$ is unknown.

After estimating $\beta_0$, the sample residual is

$$
\hat u_i=Y_i-X_i'\hat\beta.
$$

Residuals can reveal patterns suggesting misspecification, but they are constrained by the estimation procedure. For OLS with an intercept, for example, sample residuals sum to zero even when the population model is misspecified.

## Best linear projection

Even when $E[Y\mid X]$ is nonlinear, one can define coefficients that minimize population mean squared error:

$$
\beta^{LP}
=
\arg\min_b E[(Y-X'b)^2].
$$

The projection error

$$
e=Y-X'\beta^{LP}
$$

satisfies the orthogonality condition

$$
E[Xe]=0.
$$

However, it generally does not satisfy

$$
E[e\mid X]=0.
$$

OLS can consistently estimate the best linear projection under weaker conditions than those required for the linear expression to equal the true conditional mean. The interpretation of the target changes.

## Correct likelihood specification

A full probability model specifies more than the conditional mean. For example, a normal regression likelihood may assume

$$
Y\mid X=x
\sim
N(x'\beta,\sigma^2).
$$

Correct likelihood specification requires the entire stated conditional distribution to match the population distribution, including its shape and variance.

The conditional mean could be correct while normality or homoskedasticity is false. In that case, OLS may still target the conditional mean coefficients, while likelihood-based variance formulas can be invalid unless adjusted.

## Misspecification and pseudo-true parameters

Under misspecification, an estimator can still converge to the parameter value that best approximates the population according to its objective function.

For least squares, this may be the best linear projection. For maximum likelihood, it is often the parameter that minimizes the Kullback-Leibler discrepancy between the true distribution and the chosen model family.

This limiting value is called a pseudo-true parameter. It is a legitimate mathematical target but may not equal the quantity originally intended by the researcher.

## Example

Suppose

$$
Y=1+2X+3X^2+\varepsilon
$$

with

$$
E[\varepsilon\mid X]=0.
$$

If we estimate

$$
Y=\alpha+\beta X+u,
$$

then

$$
u=3X^2+\varepsilon+1-\alpha+(2-\beta)X.
$$

No choice of $\alpha$ and $\beta$ generally makes

$$
E[u\mid X]=0
$$

for every $X$ because the model lacks $X^2$.

The equation still reproduces each observed $Y$ after defining $u$, but the linear conditional mean specification is incorrect.

## Diagnostics and substantive reasoning

Potential warning signs include:

- systematic residual patterns;
- instability across specifications or subsamples;
- omitted variables suggested by economic theory;
- implausible coefficient signs or magnitudes;
- failed specification tests;
- predictions that behave poorly outside the estimation range.

No diagnostic can prove that all relevant aspects of a model are correct. Specification assessment combines theory, data knowledge, graphical analysis and statistical testing.

## Common mistakes

- Thinking the identity $Y=X'\beta+u$ proves the model is correct.
- Treating a zero average sample residual as evidence of zero conditional mean.
- Saying a model is simply "correct" without identifying the modeled target.
- Assuming a correct conditional mean implies a correctly specified likelihood.
- Interpreting a pseudo-true projection coefficient as the intended causal parameter.
- Believing a large sample repairs persistent misspecification.

## Retrieval questions

1. Why can every regression equation be made to fit exactly by defining an error?
2. What additional restriction gives the equation statistical content?
3. State correct linear conditional mean specification.
4. Give three causes of conditional mean misspecification.
5. What is the difference between a correct conditional mean and a correct likelihood?
6. What orthogonality property does a best linear projection satisfy?
7. What is a pseudo-true parameter?

## Connections

- [Conditional expectation](../../probability/conditional-expectation.md)
- [Linear regression model](linear-regression-model.md)
- [Exogeneity](exogeneity.md)
- [Ordinary least squares](ordinary-least-squares.md)
- [Consistency](../../statistics/consistency.md)
- [Maximum likelihood](../maximum-likelihood/maximum-likelihood.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, chapters 1 and 2.
- *Introductory Econometrics for Business and Economics*, Week 3 and Week 4 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain why an exact algebraic identity can still be statistically misspecified |
