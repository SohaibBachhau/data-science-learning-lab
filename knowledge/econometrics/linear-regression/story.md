# The Story of Linear Regression

Status: `developing`

This page explains the logic of linear regression in ordinary language before the detailed mathematics.

## The story

Linear regression begins with a population question: how does the expected value of an outcome change with one or more explanatory variables?

We represent that relationship with a regression model. The fitted line or plane is meant to describe the systematic part of the relationship, while the error term collects what remains unexplained.

But the presence of an error term does not guarantee that the model is correct. A useful model needs a meaningful population restriction, especially on the conditional mean.

Exogeneity is central because it says that the remaining error has no systematic conditional mean once the regressors are known.

OLS then estimates the coefficients by choosing the values that minimize the sum of squared residuals.

Once the line is fitted, each observation can be split into a fitted value and a residual. The residual is the observed outcome minus the fitted outcome. With an intercept, the residuals sum to zero and the fitted line passes through the sample means.

We can then ask how well the line fits the sample. $R^2$ describes the fraction of sample variation in $Y$ explained by the regression, while SER and RMSE describe the typical size of the residual in the units of $Y$.

That minimization can be done algebraically without assuming normality or homoskedasticity. Those assumptions enter later when we ask statistical questions such as whether OLS is unbiased, how variable it is, or how to construct standard errors.

This creates the basic chain:

```text
population relationship
→ linear conditional mean
→ error term
→ exogeneity
→ OLS minimization
→ fitted values and residuals
→ R-squared / SER / RMSE
→ estimator
→ sampling properties
→ standard errors and inference
```

## The key idea behind OLS uncertainty

An estimated slope is uncertain because the sample is only one realization.

The slope is easier to estimate when there is useful variation in the regressor and the outcome is not too noisy.

In multiple regression, what matters is not just variation in a regressor, but variation that is not already explained by the other regressors.

## From an estimate to inference

After OLS produces a coefficient estimate, the next question is not only "what is the estimate?" but also "how uncertain is it?"

Across repeated samples, $\hat\beta$ would change. Its sampling distribution describes that variation. The standard error estimates the typical size of those sample-to-sample changes.

Inference then compares the observed estimate with a population value proposed by a null hypothesis:

$
t
=
\frac{\hat\beta_j-\beta_{j,0}}
{SE(\hat\beta_j)}.
$

The t-statistic is therefore a distance measured in units of sampling uncertainty. A value such as $t=-3.5$ means that the estimate lies 3.5 standard errors below the value assumed under the null.

From there:

```text
coefficient estimate
-> standard error
-> distance from the null in SE units
-> t-statistic
-> p-value / test decision
-> confidence interval
```

A two-sided test asks whether the estimate is unusually far from the null in either direction. A one-sided test cares about only the direction stated in the alternative, so the sign of the t-statistic matters.

If heteroskedasticity is possible, a heteroskedasticity-robust standard error can be used. This changes the estimated uncertainty and therefore can change the t-statistic, p-value and confidence interval, but it does not change the OLS coefficient itself.

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
- [Measures of fit in simple linear regression](measures-of-fit.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)
