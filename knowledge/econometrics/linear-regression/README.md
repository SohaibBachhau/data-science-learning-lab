# Linear Regression

This directory develops the population model, assumptions, estimation method and sampling properties of ordinary least squares.

## Start here

For a quick conceptual review, read [The Story of Linear Regression](story.md).

Recommended reading order:

1. [Linear regression model](linear-regression-model.md)
2. [Exogeneity](exogeneity.md)
3. [Correct specification](correct-specification.md)
4. [Ordinary least squares](ordinary-least-squares.md)
5. [Measures of fit in simple linear regression](measures-of-fit.md)
6. [Sampling distribution of OLS](sampling-distribution-of-ols.md)
7. [Omitted-variable bias](omitted-variable-bias.md)
8. [Multiple regression and adjusted fit](multiple-regression.md)
9. [Matrix OLS and projections](matrix-ols-and-projections.md)
10. [Multicollinearity and dummy variables](multicollinearity-and-dummies.md)
11. [Joint hypothesis tests: first F-test](joint-hypothesis-tests.md)

The logical separation is important:

```text
regression equation
→ conditional mean restriction
→ estimation criterion
→ fitted values and residuals
→ measures of fit
→ estimator decomposition
→ statistical properties
```

The OLS minimization problem can be solved without probabilistic assumptions. Unbiasedness, consistency, variance formulas and inference require additional assumptions, each with a distinct role.

## October 2026 learning update

Week 4 multiple-regression mechanics have been added in detail, including the matrix OLS derivation and practice corrections. The Week 5 joint-testing note covers the opening homoskedastic F-test only; broader robust/general tests remain on the course map as planned.
