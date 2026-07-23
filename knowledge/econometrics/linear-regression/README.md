# Linear Regression

This directory develops the population model, assumptions, estimation method and sampling properties of ordinary least squares.

Recommended reading order:

1. [Linear regression model](linear-regression-model.md)
2. [Exogeneity](exogeneity.md)
3. [Correct specification](correct-specification.md)
4. [Ordinary least squares](ordinary-least-squares.md)
5. [Sampling distribution of OLS](sampling-distribution-of-ols.md)

The logical separation is important:

```text
regression equation
→ conditional mean restriction
→ estimation criterion
→ estimator decomposition
→ statistical properties
```

The OLS minimization problem can be solved without probabilistic assumptions. Unbiasedness, consistency, variance formulas and inference require additional assumptions, each with a distinct role.
