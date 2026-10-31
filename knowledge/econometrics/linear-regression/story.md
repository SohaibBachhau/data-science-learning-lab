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


## The next chapter: holding other variables constant

In the first version of our story, there is only one regressor. But a relationship we see in data may mix several different influences. If language background affects test scores and is correlated with class size, a class-size-only regression can accidentally attribute part of the language-background pattern to class size. This is the intuition behind [omitted-variable bias](omitted-variable-bias.md).

[Multiple regression](multiple-regression.md) lets us compare outcomes at the same values of other included regressors. The meaning of a slope becomes “one regressor changes while the others are held fixed.” This gives a partial association; it is not automatic proof of a causal effect.

The larger regression becomes easier to handle with [matrix notation](matrix-ols-and-projections.md). OLS still minimizes squared residuals, but now it projects the entire outcome vector onto the space spanned by the regressors. The fitted part lies in that space, while the residual points in a perpendicular direction. That is why sample residuals are orthogonal to every regressor, even if the population exogeneity assumption is false.

This geometry also explains two problems that initially sound similar. With **perfect** [multicollinearity](multicollinearity-and-dummies.md), one regressor column adds no new direction and the coefficient vector is not uniquely identified. With **imperfect** multicollinearity, there is a new direction, but so little independent variation that the estimate can be imprecise. Including every category dummy together with an intercept is a classic perfect-dependence mistake.

After estimating more than one slope, we often want to test them **together**. Two individual 5% tests do not normally form a valid 5% joint test. A first [joint F-test](joint-hypothesis-tests.md) compares how much fit is lost when a group of coefficients is restricted. The homoskedastic R-squared version is only the beginning; robust and general matrix forms still require separate study.

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
