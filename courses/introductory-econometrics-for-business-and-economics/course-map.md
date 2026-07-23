# Course Map

This map connects the six weeks of **Introductory Econometrics for Business and Economics** to permanent notes in the `knowledge/` directory.

Course-specific summaries, examples and terminology belong in `course-notes/`. General explanations that remain useful beyond this course belong in `knowledge/`.

Status labels used below:

- **available**: a substantive permanent note exists;
- **planned**: the course covers the topic, but the permanent note will be created when the topic is studied;
- **course-specific**: the material should first be developed in the weekly course notes before deciding whether it needs a separate permanent note.

## Foundation before Week 1

These notes support the probability and statistics used throughout the course:

- [Random variables and probability distributions](../../knowledge/probability/random-variables-and-distributions.md) **available**
- [Joint distributions, independence and iid sampling](../../knowledge/probability/joint-distributions-independence-and-iid.md) **available**
- [Expectation](../../knowledge/probability/expectation.md) **available**
- [Conditional expectation](../../knowledge/probability/conditional-expectation.md) **available**
- [Variance, covariance and moments](../../knowledge/probability/variance-covariance-and-moments.md) **available**
- [Parameters, estimators and estimates](../../knowledge/statistics/parameters-estimators-and-estimates.md) **available**
- [Sampling distributions](../../knowledge/statistics/sampling-distributions.md) **available**

## Week 1: Simple linear regression with one regressor, estimation

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
- $R^2$ and standard error of the regression **planned**
- classical regression assumptions as presented in the slides **course-specific**

## Week 2: Simple linear regression with one regressor, inference

### Permanent knowledge

- [Joint distributions, independence and iid sampling](../../knowledge/probability/joint-distributions-independence-and-iid.md) **available**
- [Variance, covariance and moments](../../knowledge/probability/variance-covariance-and-moments.md) **available**
- [Law of large numbers](../../knowledge/probability/law-of-large-numbers.md) **available**
- [Central limit theorem](../../knowledge/probability/central-limit-theorem.md) **available**
- [Unbiasedness](../../knowledge/statistics/unbiasedness.md) **available**
- [Consistency](../../knowledge/statistics/consistency.md) **available**
- [Asymptotic normality](../../knowledge/statistics/asymptotic-normality.md) **available**
- [Sampling distribution of OLS](../../knowledge/econometrics/linear-regression/sampling-distribution-of-ols.md) **available**

### Planned permanent knowledge

- standard errors **planned**
- hypothesis testing **planned**
- confidence intervals **planned**
- binary regressors **planned**
- Slutsky's theorem as a separate note **planned**
- continuous mapping theorem as a separate note **planned**

## Week 3: Multiple regression, estimation and assumptions

### Existing foundations

- [Linear regression model](../../knowledge/econometrics/linear-regression/linear-regression-model.md) **available**
- [Exogeneity](../../knowledge/econometrics/linear-regression/exogeneity.md) **available**
- [Correct specification](../../knowledge/econometrics/linear-regression/correct-specification.md) **available**
- [Ordinary least squares](../../knowledge/econometrics/linear-regression/ordinary-least-squares.md) **available**
- [Sampling distribution of OLS](../../knowledge/econometrics/linear-regression/sampling-distribution-of-ols.md) **available**

### Planned permanent knowledge

- omitted variable bias **planned**
- multiple regression and ceteris paribus interpretation **planned**
- matrix notation for regression **planned**
- matrix differentiation **planned**
- perfect and imperfect multicollinearity **planned**
- dummy-variable trap **planned**
- adjusted $R^2$ **planned**

## Week 4: Multiple regression, testing and restricted estimation

### Existing foundations

- [Sampling distributions](../../knowledge/statistics/sampling-distributions.md) **available**
- [Asymptotic normality](../../knowledge/statistics/asymptotic-normality.md) **available**
- [Maximum likelihood](../../knowledge/econometrics/maximum-likelihood/maximum-likelihood.md) **available**

### Planned permanent knowledge

- tests for individual coefficients **planned**
- joint hypothesis tests and the $F$ statistic **planned**
- general linear restrictions **planned**
- restricted least squares **planned**
- Lagrange multipliers **planned**
- Wald test **planned**
- likelihood-ratio test **planned**
- Lagrange-multiplier test **planned**
- control variables and specification choices **planned**

## Week 5: Nonlinear regression functions

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

## Week 6: Introduction to panel data analysis

### Existing foundations

- [Joint distributions, independence and iid sampling](../../knowledge/probability/joint-distributions-independence-and-iid.md) **available**
- [Exogeneity](../../knowledge/econometrics/linear-regression/exogeneity.md) **available**
- [Correct specification](../../knowledge/econometrics/linear-regression/correct-specification.md) **available**

### Planned permanent knowledge

- panel-data structure **planned**
- first-difference estimator **planned**
- entity fixed effects **planned**
- time fixed effects **planned**
- two-way fixed effects **planned**
- least-squares dummy-variable estimation **planned**
- within or entity-demeaned estimator **planned**
- strict exogeneity in panel data **planned**
- clustered and panel-appropriate standard errors **planned**
- random effects and the Hausman comparison **planned**

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
