# The Story of Maximum Likelihood

Status: `developing`

This page gives the intuition behind maximum likelihood before the formal likelihood, score and Hessian calculations.

## The story

Maximum likelihood begins by specifying a probability model for the data.

That model tells us how plausible different observations would be for different parameter values.

Once we observe the data, we turn the probability model around and ask a new question:

> Which parameter values make the data we actually observed most plausible under the model?

The likelihood function records that plausibility as a function of the unknown parameters.

The maximum-likelihood estimator chooses the parameter values that maximize the likelihood.

In practice we usually work with the log-likelihood because products become sums and the mathematics is easier.

The score is the derivative of the log-likelihood. At an interior maximum, the score is typically zero. The Hessian describes curvature and helps us understand whether we are at a maximum and how much information the data contain about the parameters.

In normal linear regression, maximizing the likelihood with respect to the regression coefficients gives the same coefficient estimates as OLS. The methods arrive there from different starting points: OLS minimizes squared residuals, while maximum likelihood maximizes the probability model.

So the story is:

```text
probability model
→ likelihood of observed data
→ log-likelihood
→ maximize over parameters
→ score and curvature
→ estimator
→ consistency and asymptotic normality
→ inference
```

## What to remember

A likelihood is a function of the parameters after the observed data are treated as fixed.

Maximum likelihood depends on the probability model being specified. If the model is misspecified, the estimator may converge to a pseudo-true parameter rather than the parameter we originally intended.

## Related notes

- [Maximum likelihood index](README.md)
- [Maximum likelihood](maximum-likelihood.md)
- [Econometrics story](../story.md)
