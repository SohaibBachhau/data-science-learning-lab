# Course Map

This map connects the six weeks of **Introductory Econometrics for Business and Economics** to permanent notes in the `knowledge/` directory.

Course-specific summaries, examples and terminology belong in `course-notes/`. General explanations that remain useful beyond this course belong in `knowledge/`.

Status labels used below:

- **available**: a substantive permanent note exists;
- **planned**: the course covers the topic, but the permanent note will be created when the topic is studied;
- **course-specific**: the material should first be developed in the weekly course notes before deciding whether it needs a separate permanent note.

## Week 1: Knowledge clip series foundations

These notes support the probability and statistics used throughout the course:

- [Random variables and probability distributions](../../knowledge/probability/random-variables-and-distributions.md) **available**
- [Joint distributions, independence and iid sampling](../../knowledge/probability/joint-distributions-independence-and-iid.md) **available**
- [Expectation](../../knowledge/probability/expectation.md) **available**
- [Conditional expectation](../../knowledge/probability/conditional-expectation.md) **available**
- [Variance, covariance and moments](../../knowledge/probability/variance-covariance-and-moments.md) **available**
- [Convergence in probability](../../knowledge/probability/convergence-in-probability.md) **available**
- [Convergence in distribution](../../knowledge/probability/convergence-in-distribution.md) **available**
- [Parameters, estimators and estimates](../../knowledge/statistics/parameters-estimators-and-estimates.md) **available**
- [Sampling distributions](../../knowledge/statistics/sampling-distributions.md) **available**
- [Efficiency](../../knowledge/statistics/efficiency.md) **available**

## Week 2: Simple linear regression with one regressor, estimation

### Permanent knowledge

- [Linear regression model](../../knowledge/econometrics/linear-regression/linear-regression-model.md) **available**
- [Exogeneity](../../knowledge/econometrics/linear-regression/exogeneity.md) **available**
- [Correct specification](../../knowledge/econometrics/linear-regression/correct-specification.md) **available**
- [Ordinary least squares](../../knowledge/econometrics/linear-regression/ordinary-least-squares.md) **available**
- [Maximum likelihood](../../knowledge/econometrics/maximum-likelihood/maximum-likelihood.md) **available**

### Course-specific development

- California test-score example **course-specific**
- interpretation of estimated intercepts and slopes **course-specific**
- fitted values and residual calculations **course-specific**
- [measures of fit: $R^2$, SER and RMSE](../../knowledge/econometrics/linear-regression/measures-of-fit.md) **available**
- classical regression assumptions as presented in the slides **course-specific**

## Week 3: Simple linear regression with one regressor, inference

Course-specific review: [Week 3: Simple Linear Regression Inference](course-notes/week-3-simple-linear-regression-inference.md).

### Permanent knowledge

- [Joint distributions, independence and iid sampling](../../knowledge/probability/joint-distributions-independence-and-iid.md) **available**
- [Variance, covariance and moments](../../knowledge/probability/variance-covariance-and-moments.md) **available**
- [Convergence in probability](../../knowledge/probability/convergence-in-probability.md) **available**
- [Convergence in distribution](../../knowledge/probability/convergence-in-distribution.md) **available**
- [Law of large numbers](../../knowledge/probability/law-of-large-numbers.md) **available**
- [Central limit theorem](../../knowledge/probability/central-limit-theorem.md) **available**
- [Unbiasedness](../../knowledge/statistics/unbiasedness.md) **available**
- [Consistency](../../knowledge/statistics/consistency.md) **available**
- [Asymptotic normality](../../knowledge/statistics/asymptotic-normality.md) **available**
- [Sampling distribution of OLS](../../knowledge/econometrics/linear-regression/sampling-distribution-of-ols.md) **available**

### Planned permanent knowledge

- [standard errors](../../knowledge/statistics/sampling-distributions.md#standard-deviation-and-standard-error) **available**
- [hypothesis testing and confidence intervals](../../knowledge/statistics/hypothesis-testing-and-confidence-intervals.md) **available**
- binary regressors **planned**
- Slutsky's theorem is covered in [Convergence in distribution](../../knowledge/probability/convergence-in-distribution.md) **available**
- continuous mapping theorem is covered in [Convergence in probability](../../knowledge/probability/convergence-in-probability.md) **available**

## Week 4: Multiple regression, estimation and assumptions

Completed course review: [Week 4: Multiple Regression, Matrix OLS and Assumptions](course-notes/week-4-multiple-regression.md) (October 19 study session).

### Permanent knowledge now available

- [Omitted-variable bias](../../knowledge/econometrics/linear-regression/omitted-variable-bias.md) **available**
- [Multiple regression and adjusted fit](../../knowledge/econometrics/linear-regression/multiple-regression.md) **available**
- [Matrix OLS, projection matrices, residual orthogonality and covariance](../../knowledge/econometrics/linear-regression/matrix-ols-and-projections.md) **available**
- [Multicollinearity, binary regressors and the dummy-variable trap](../../knowledge/econometrics/linear-regression/multicollinearity-and-dummies.md) **available**

### Existing connected foundations

- [Exogeneity](../../knowledge/econometrics/linear-regression/exogeneity.md) **available**
- [Correct specification](../../knowledge/econometrics/linear-regression/correct-specification.md) **available**
- [Sampling distribution of OLS](../../knowledge/econometrics/linear-regression/sampling-distribution-of-ols.md) **available**

## Week 5: Multiple regression, testing and restricted estimation

Covered so far: [Week 5: Joint Testing (Started)](course-notes/week-5-joint-testing-start.md).

### Permanent knowledge now available

- [Joint testing: restrictions, restricted and unrestricted models, and the first homoskedastic F-test](../../knowledge/econometrics/linear-regression/joint-hypothesis-tests.md) **available**
- [Hypothesis testing and confidence intervals for an individual coefficient](../../knowledge/statistics/hypothesis-testing-and-confidence-intervals.md) **available**
- [Maximum likelihood](../../knowledge/econometrics/maximum-likelihood/maximum-likelihood.md) **available**

### Not yet recorded as completed

- full general linear-restriction calculations $R\beta=r$ **planned**
- robust Wald / F / chi-squared tests **planned**
- restricted least squares and Lagrange multipliers **planned**
- likelihood-ratio and Lagrange-multiplier tests **planned**
- control-variable choice and specification sensitivity checks **planned**

## Week 6: Nonlinear regression functions

### Existing foundations

- [Linear regression model](../../knowledge/econometrics/linear-regression/linear-regression-model.md) **available**
- [Correct specification](../../knowledge/econometrics/linear-regression/correct-specification.md) **available**
- [Maximum likelihood](../../knowledge/econometrics/maximum-likelihood/maximum-likelihood.md) **available**

### Planned permanent knowledge

- nonlinear regression functions **planned**
- nonlinear least squares **planned**
- numerical optimization and gradient descent **planned**
- polynomial regression **planned**
- logarithmic transformations **planned**
- linear-log, log-linear and log-log models **planned**
- elasticities and semi-elasticities **planned**
- interaction terms **planned**
- marginal effects **planned**

## Development rule

A planned link should become a permanent knowledge note only after the topic has been studied and can be explained with:

- intuition;
- a precise definition;
- assumptions;
- a derivation or proof outline;
- an example;
- a failure case;
- retrieval questions;
- links to exercises, derivations or code where useful.

Empty placeholder notes should not be created.

## Source materials

The weekly structure follows the six local lecture slide sets for the course. The original slide PDFs remain excluded from version control.
