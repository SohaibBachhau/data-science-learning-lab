# The Story of Linear Regression

Status: `developing`

This page explains the logic of linear regression in ordinary language before the detailed mathematics.

## The story

Linear regression begins with a population question: how does the expected value of an outcome change with one or more explanatory variables?

We represent that relationship with a regression model. The fitted line or plane is meant to describe the systematic part of the relationship, while the error term collects what remains unexplained.

But the presence of an error term does not guarantee that the model is correct. A useful model needs a meaningful population restriction, especially on the conditional mean.

Exogeneity is central because it says that the remaining error has no systematic conditional mean once the regressors are known.

OLS then estimates the coefficients by choosing the values that minimize the sum of squared residuals.

That minimization can be done algebraically without assuming normality or homoskedasticity. Those assumptions enter later when we ask statistical questions such as whether OLS is unbiased, how variable it is, or how to construct standard errors.

This creates the basic chain:

```text
population relationship
→ linear conditional mean
→ error term
→ exogeneity
→ OLS minimization
→ estimator
→ sampling properties
→ standard errors and inference
```

## The key idea behind OLS uncertainty

An estimated slope is uncertain because the sample is only one realization.

The slope is easier to estimate when there is useful variation in the regressor and the outcome is not too noisy.

In multiple regression, what matters is not just variation in a regressor, but variation that is not already explained by the other regressors.

## What to remember

The regression equation is not the same as the assumption that the conditional mean is correctly specified.

OLS gives sample identities automatically, but population conclusions require assumptions.

More data can reduce sampling uncertainty, but it does not fix a fundamentally wrong identification assumption.

## Related notes

- [Linear regression index](README.md)
- [Linear regression model](linear-regression-model.md)
- [Correct specification](correct-specification.md)
- [Exogeneity](exogeneity.md)
- [Ordinary least squares](ordinary-least-squares.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)
