# Econometrics

This directory contains permanent notes on statistical models and estimation methods used to study economic and observational data.

## Start here

For a quick narrative review of how the major branches connect, read [The Story of Econometrics](story.md).

## Current foundation

### Linear regression

1. [Linear regression story](linear-regression/story.md)
2. [Linear regression model](linear-regression/linear-regression-model.md)
3. [Exogeneity](linear-regression/exogeneity.md)
4. [Correct specification](linear-regression/correct-specification.md)
5. [Ordinary least squares](linear-regression/ordinary-least-squares.md)
6. [Sampling distribution of OLS](linear-regression/sampling-distribution-of-ols.md)
7. [Omitted-variable bias](linear-regression/omitted-variable-bias.md)
8. [Multiple regression and adjusted fit](linear-regression/multiple-regression.md)
9. [Matrix OLS and projection matrices](linear-regression/matrix-ols-and-projections.md)
10. [Multicollinearity and dummy variables](linear-regression/multicollinearity-and-dummies.md)
11. [Joint hypothesis tests (introductory F-test)](linear-regression/joint-hypothesis-tests.md)

### Maximum likelihood

1. [Maximum likelihood story](maximum-likelihood/story.md)
2. [Maximum likelihood](maximum-likelihood/maximum-likelihood.md)

### Time series

1. [Time series story](time-series/story.md)
2. [Time series econometrics](time-series/README.md)

## Main learning chain

```text
population relationship
→ conditional mean model
→ error term and exogeneity
→ specification of the estimand
→ estimation criterion
→ estimator decomposition
→ unbiasedness and consistency
→ asymptotic distribution
→ standard errors and inference
```

## Core distinctions

- A regression equation with an error term is an algebraic decomposition, not automatically a correctly specified conditional mean.
- OLS minimization creates exact sample identities, but population properties require assumptions.
- Exogeneity, homoskedasticity and normality are different assumptions with different roles.
- Predictive interpretation does not automatically imply causal interpretation.
- Correct specification must be stated relative to a target, such as a conditional mean or a full likelihood.

## Relationship with other subjects

The probability notes explain random variables, conditional expectations, moments and limit theorems. The statistics notes explain estimators, sampling distributions and asymptotic properties. The econometrics notes combine these ideas in regression, likelihood and time-series models.

## Status

The linear-regression, maximum-likelihood and time-series sections are currently `developing`. The foundation now includes Week 4 multiple regression and the opening Week 5 joint-test material. General robust joint tests, nonlinear regression, panel data and other advanced methods remain future work; avoid duplicating existing explanations.
