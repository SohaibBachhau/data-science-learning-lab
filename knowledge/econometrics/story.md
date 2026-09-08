# The Story of Econometrics

Status: `developing`

This page gives the big-picture story of the econometrics branch with minimal mathematics. Use it when you want to remember what the subject is doing before returning to the technical notes.

## The story

Econometrics takes economic or observational questions and turns them into statistical models that can be confronted with data.

We often begin with a population relationship we want to understand. For example, we may want to know how the expected value of an outcome changes with explanatory variables.

A regression equation gives us a way to represent that relationship, but writing an equation is not enough to make the model correct. The important part is what the model claims about the conditional mean and about the error term.

Exogeneity is one of the key assumptions. Roughly, it says that once we condition on the regressors, the remaining error does not systematically point upward or downward. This is what lets OLS target the intended population relationship under the model.

OLS then gives us an estimation rule: choose the coefficients that make the squared residuals as small as possible. The algebra tells us what the estimator is. Probability and statistics tell us when that estimator is unbiased, consistent, precise and approximately normal.

Maximum likelihood takes a different route. Instead of specifying only a conditional mean, it starts from a full probability model and chooses parameter values that make the observed data most likely under that model.

Time-series econometrics adds another complication: observations are ordered in time and can depend on their own past. That creates ideas such as autocorrelation, stationarity, trends, forecasting and dynamic models.

So the broad story is:

```text
economic question
→ population relationship
→ statistical model
→ assumptions
→ estimation
→ estimator properties
→ uncertainty and inference
→ interpretation
```

with major branches such as:

```text
econometrics
├── linear regression
├── maximum likelihood
└── time series
```

## What to remember

An error term does not automatically make a regression correctly specified.

OLS is an optimization method. Its statistical properties require assumptions.

Exogeneity, homoskedasticity and normality do different jobs.

Prediction and causal interpretation are not automatically the same.

Time-series models require us to think about dependence across time, not just dependence between different variables.

## When the detailed notes feel heavy

Start here, identify which part of the story you have forgotten, and then open only that detailed note.

## Related notes

- [Econometrics index](README.md)
- [Linear regression](linear-regression/README.md)
- [Maximum likelihood](maximum-likelihood/README.md)
- [Time series econometrics](time-series/README.md)
- [Foundations map](../foundations-map.md)
