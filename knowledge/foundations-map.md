---
title: Foundations Map
status: developing
created: 2026-08-09
updated: 2026-09-05
tags:
  - roadmap
  - intuition
  - econometrics
  - probability
  - statistics
---

# Foundations Map

## Purpose

This map is the big-picture story behind the material in this repository.

The goal is not to memorize isolated formulas. The goal is to understand why one idea leads to the next, what each assumption buys us, and what changes when an assumption is weakened or fails.

Use this page as a navigation hub. Click a topic to open the corresponding permanent note.

---

## The main story in one sentence

We begin with random variables because data are uncertain, use expectations and distributions to describe their behavior, use sampling theory to understand estimators, and then use those tools to build regression and time-series models.

---

# 1. From randomness to expectation

## [Random variables and distributions](probability/random-variables-and-distributions.md)

A dataset contains realized values, but before sampling we think of observations as random variables.

That distinction matters because econometrics asks questions such as:

- What would happen if we drew another sample?
- How variable is an estimator across samples?
- What is the probability of seeing an estimate this extreme?

Those are probability questions, so the story starts with random variables and distributions.

### Intuition

A random variable is a numerical outcome that is not known before the random process occurs.

Once we understand its distribution, we can ask where it is centered and how much it varies.

That leads naturally to expectation.

↓

## [Expectation](probability/expectation.md)

Expectation gives the long-run or probability-weighted center of a random variable.

For a random variable $X$,

$$
E[X]
$$

is not one observed value. It is a property of the distribution of $X$.

### Why do we need this for regression?

Regression is fundamentally about conditional expectations.

We eventually want to understand objects such as

$$
E[Y\mid X].
$$

So ordinary expectation is the foundation for conditional expectation.

↓

## [Variance, covariance and moments](probability/variance-covariance-and-moments.md)

Expectation tells us where a distribution is centered, but not how uncertain it is.

Variance measures spread:

$$
\operatorname{Var}(X)=E[(X-E[X])^2].
$$

Covariance tells us whether two random variables tend to move together.

This becomes essential later because:

- the variance of an estimator determines its precision;
- standard errors come from estimator variances;
- covariance between regressors matters in multiple regression;
- finite moments are needed for many large-sample results.

### Important intuition

A good estimator is not only centered correctly. We also want it to have little sampling variation.

That idea eventually leads to standard errors and test statistics.

↓

## [Joint distributions, independence and iid sampling](probability/joint-distributions-independence-and-iid.md)

Econometrics almost never studies one random variable in isolation.

We observe variables together, for example:

$$
(X_i,Y_i).
$$

Their joint distribution describes how they behave together.

Independence concerns whether knowing one random object changes what we know about another.

iid sampling gives us a clean repeated-sampling structure:

- identically distributed: observations come from the same population distribution;
- independent: one observation does not reveal information about another observation.

### Why do we need iid?

Because laws such as the LLN and CLT need assumptions about how observations are generated.

↓

# 2. Conditioning: the bridge to regression

## [Conditional expectation](probability/conditional-expectation.md)

Instead of asking

$$
E[Y],
$$

we ask

$$
E[Y\mid X].
$$

This means:

> What is the average value of $Y$ among observations with a given value of $X$?

This is the conceptual bridge from probability to regression.

### Example

Suppose:

- $Y$ = exam score;
- $X$ = hours studied.

Then

$$
E[Y\mid X=5]
$$

is the average exam score among students who study 5 hours.

Regression tries to model how this conditional mean changes with $X$.

↓

# 3. From population quantities to estimators

## [Parameters, estimators and estimates](statistics/parameters-estimators-and-estimates.md)

Now we separate three objects:

$$
\text{parameter}
\neq
\text{estimator}
\neq
\text{estimate}.
$$

A parameter is a fixed but unknown population quantity.

An estimator is a random rule based on the sample.

An estimate is the realized numerical value of that estimator in one particular sample.

### Example

$$
\beta_1
$$

is the population regression coefficient.

$$
\hat\beta_1
$$

is the estimator.

If a particular sample gives

$$
\hat\beta_1=2.4,
$$

then $2.4$ is the estimate.

### Why is this distinction important?

Because inferential statements such as variance, bias, consistency and sampling distributions are statements about the estimator $\hat\beta$, not about the fixed parameter $\beta$.

↓

## [Sampling distributions](statistics/sampling-distributions.md)

If we repeatedly drew samples and recalculated an estimator, we would obtain different values of $\hat\beta$.

The distribution of those possible estimator values is its sampling distribution.

This is where ideas such as

$$
E[\hat\beta],
$$

$$
\operatorname{Var}(\hat\beta),
$$

and

$$
P(\hat\beta \leq c)
$$

become meaningful.

### Intuition

The sampling distribution tells us how reliable an estimation procedure is before we happen to observe one particular sample.

↓

# 4. What makes an estimator good?

## [Unbiasedness](statistics/unbiasedness.md)

An estimator is unbiased if

$$
E[\hat\theta]=\theta.
$$

Across repeated samples, it is centered on the true parameter.

### Important

Unbiasedness is a finite-sample property.

It does not tell us that one particular estimate is close to the truth.

↓

## [Consistency](statistics/consistency.md)

An estimator is consistent if

$$
\hat\theta \xrightarrow{p} \theta
$$

as the sample size becomes large.

### Intuition

As we collect more data, the estimator concentrates around the true parameter.

This is different from unbiasedness.

An estimator can be biased in small samples but still consistent.

### What mathematical tool often gives consistency?

The law of large numbers.

↓

# 5. Why large samples help

## [Law of Large Numbers](probability/law-of-large-numbers.md)

The LLN says that sample averages converge toward their population expectations under suitable conditions.

For example,

$$
\frac{1}{n}\sum_{i=1}^n X_i
\xrightarrow{p}
E[X].
$$

### Intuition

Random fluctuations average out when we have enough independent information.

### Why do we care in econometrics?

Many estimators can be written as functions of sample averages.

If those sample averages converge to the right population quantities, the estimator can become consistent.

↓

## [Central Limit Theorem](probability/central-limit-theorem.md)

Consistency tells us that an estimator gets close to the true value.

But for inference we need more:

> How does the estimator fluctuate around the truth?

The CLT tells us that properly standardized sums or averages often become approximately normal in large samples.

A typical form is

$$
\frac{\sqrt{n}(\bar X-\mu)}{\sigma}
\Rightarrow
N(0,1).
$$

### Intuition

The LLN tells us where an estimator goes.

The CLT tells us the approximate shape of its remaining sampling uncertainty.

↓

## [Asymptotic normality](statistics/asymptotic-normality.md)

The CLT leads to results of the form

$$
\sqrt{n}(\hat\theta-\theta)
\Rightarrow
N(0,V).
$$

This is what allows us to construct approximate:

- standard errors;
- confidence intervals;
- test statistics;
- p-values.

### Standardization intuition

If

$$
\hat\theta
$$

has mean approximately $\theta$ and standard error $SE(\hat\theta)$, then

$$
\frac{\hat\theta-\theta}{SE(\hat\theta)}
$$

measures how far the estimator is from the truth in units of its own sampling uncertainty.

↓

# 6. Regression enters

## [The linear regression model](econometrics/linear-regression/linear-regression-model.md)

Now we model the relationship between $Y$ and regressors $X$.

In simple form,

$$
Y_i=\beta_0+\beta_1X_i+u_i.
$$

The regression coefficient $\beta_1$ describes how the conditional mean of $Y$ changes with $X$ when the model is correctly specified.

### Important intuition

Writing

$$
Y_i=\beta_0+\beta_1X_i+u_i
$$

does not by itself mean the model is correct.

We can always define an error term as whatever is left over.

The important question is what assumptions we make about that error.

↓

## [Correct specification](econometrics/linear-regression/correct-specification.md)

The key population claim in a correctly specified linear conditional-mean model is

$$
E[Y\mid X]=X'\beta.
$$

Equivalently, if

$$
u=Y-X'\beta,
$$

then

$$
E[u\mid X]=0.
$$

### Intuition

The regression function should capture the systematic conditional mean.

The remaining error should not systematically depend on $X$.

↓

## [Exogeneity](econometrics/linear-regression/exogeneity.md)

A central assumption is

$$
E[u\mid X]=0.
$$

### What does this buy us?

It says that once we condition on $X$, the error does not have a systematic positive or negative mean.

That is what allows OLS to target the population regression coefficients rather than systematically absorbing omitted information correlated with $X$.

### If exogeneity fails

This is a major branch.

OLS can become biased or inconsistent.

More data alone does not repair the underlying identification problem.

Future methods may include:

- instrumental variables;
- fixed effects;
- difference-in-differences;
- other causal-identification methods.

These should be added as permanent notes when they are actually studied.

↓

# 7. Ordinary least squares

## [Ordinary Least Squares](econometrics/linear-regression/ordinary-least-squares.md)

OLS chooses coefficients that minimize the sum of squared residuals:

$$
\sum_{i=1}^n \hat u_i^2.
$$

The estimator can be written as

$$
\hat\beta=(X'X)^{-1}X'Y.
$$

Substituting

$$
Y=X\beta+u
$$

gives the central decomposition

$$
\hat\beta
=
\beta+(X'X)^{-1}X'u.
$$

### Why is this decomposition so useful?

It shows exactly why estimation error exists:

$$
\hat\beta-\beta
=
(X'X)^{-1}X'u.
$$

From here we can study:

- bias;
- variance;
- consistency;
- asymptotic normality;
- effects of regressor variation;
- effects of correlation among regressors.

↓

# 8. How precise is OLS?

## [Sampling distribution of OLS](econometrics/linear-regression/sampling-distribution-of-ols.md)

Under suitable assumptions, the variance of OLS depends on both:

1. how noisy the outcome is;
2. how much useful information exists in the regressors.

In simple regression under homoskedasticity,

$$
\operatorname{Var}(\hat\beta_1\mid X)
=
\frac{\sigma_u^2}
{\sum_{i=1}^n(X_i-\bar X)^2}.
$$

### Branch: little variation in $X$

If

$$
\sum(X_i-\bar X)^2
$$

is small, the denominator is small.

Therefore,

$$
\operatorname{Var}(\hat\beta_1)
$$

and

$$
SE(\hat\beta_1)
$$

are large.

### Intuition

To estimate a slope, we need to observe how $Y$ behaves at meaningfully different values of $X$.

If almost everyone has the same $X$, the slope is hard to learn.

This feeds directly into the test statistic:

$$
t=
\frac{\hat\beta_1-\beta_{1,0}}
{SE(\hat\beta_1)}.
$$

Larger uncertainty means a smaller absolute test statistic, holding the estimated distance from the null fixed.

---

# 9. Branch: correlated regressors

In multiple regression,

$$
Y=\beta_0+\beta_1X_1+\beta_2X_2+\cdots+u.
$$

The important quantity is not merely the total variation in $X_1$.

What matters is the variation in $X_1$ that cannot already be explained by the other regressors.

A useful form of the variance expression is

$$
\operatorname{Var}(\hat\beta_1\mid X)
\propto
\frac{1}
{\sum(X_{1i}-\bar X_1)^2(1-R_1^2)},
$$

where $R_1^2$ comes from regressing $X_1$ on the other regressors.

### If correlation among regressors is high

Then

$$
R_1^2\uparrow
$$

so

$$
1-R_1^2\downarrow.
$$

This means less unique variation is available to identify $\beta_1$.

Therefore:

$$
SE(\hat\beta_1)\uparrow
$$

and individual $t$-statistics tend to become smaller in absolute value.

### Intuition

Multiple regression asks:

> What happens to $Y$ when $X_1$ changes while the other regressors are held fixed?

If $X_1$ almost never changes independently of the other regressors, the data contain little information for answering that question.

If correlation becomes perfect, the coefficients cannot be separately identified by OLS.

A dedicated multicollinearity note should be added once this topic is developed further.

---

# 10. Branch: homoskedasticity versus heteroskedasticity

The general conditional variance of OLS can be written as

$$
\operatorname{Var}(\hat\beta\mid X)
=
(X'X)^{-1}X'\Omega X(X'X)^{-1}.
$$

## If errors are homoskedastic

Then

$$
\Omega=\sigma^2I,
$$

and this simplifies to

$$
\operatorname{Var}(\hat\beta\mid X)
=
\sigma^2(X'X)^{-1}.
$$

This gives the classical OLS standard-error formula.

## If errors are heteroskedastic

The coefficient estimator can still target the correct coefficient under exogeneity, but the classical variance formula is generally wrong.

So the branch is:

```text
Exogeneity holds
        |
        +-- Homoskedastic errors
        |       |
        |       +-- classical OLS standard errors
        |
        +-- Heteroskedastic errors
                |
                +-- OLS coefficients may still be valid
                +-- classical standard errors are not
                +-- use heteroskedasticity-robust inference
```

A dedicated robust-standard-errors note should be added when this is studied in detail.

---

# 11. Branch: normality versus no normality

## If we assume normal errors

Suppose

$$
u\mid X\sim N(0,\sigma^2I).
$$

Then OLS has an exact conditional normal distribution.

Normality also gives a complete likelihood for the regression model.

This leads to:

## [Maximum likelihood](econometrics/maximum-likelihood/maximum-likelihood.md)

For normal regression, maximizing the likelihood with respect to $\beta$ gives the same coefficient estimator as OLS.

So:

```text
Normal regression assumption
        |
        +-- write normal likelihood
        |
        +-- maximize with respect to beta
        |
        +-- beta-hat_ML = beta-hat_OLS
```

### If we do not assume normality

OLS does not automatically disappear.

Under suitable exogeneity and moment conditions, we can use large-sample theory instead:

```text
No exact normality
        |
        +-- LLN
        |     |
        |     +-- consistency
        |
        +-- CLT
              |
              +-- asymptotic normality
                    |
                    +-- approximate inference
```

This is one of the most important branches in econometrics:

> Exact normality is one route to inference. Large-sample theory is another.

---

# 12. Branch: transformations of normal variables

The normal distribution is closed under linear transformations.

If

$$
A\sim N(\mu,\sigma^2)
$$

and

$$
B=aA+c,
$$

then

$$
B\sim N(a\mu+c,a^2\sigma^2).
$$

This matters because standardization is exactly such a transformation.

For example,

$$
Z=\frac{A-\mu}{\sigma}
$$

gives

$$
Z\sim N(0,1).
$$

The same idea appears when standardizing estimators for hypothesis testing.

See [Random variables and distributions](probability/random-variables-and-distributions.md) for the full transformation discussion.

---

# 13. Regression fit and $R^2$

OLS does more than estimate coefficients. It also divides the observed sample variation in $Y$ into explained and unexplained parts.

The total sample variation is

$$
TSS=\sum_{i=1}^n(Y_i-\bar Y)^2.
$$

With an intercept,

$$
TSS=ESS+RSS.
$$

Then

$$
R^2
=
\frac{ESS}{TSS}
=
1-\frac{RSS}{TSS}.
$$

### Intuition

$R^2$ asks:

> Of the observed variation in $Y$ around its sample mean, what fraction is accounted for by the fitted regression?

A high $R^2$ does not by itself establish causality, correct specification, or valid inference.

See [Ordinary Least Squares](econometrics/linear-regression/ordinary-least-squares.md).

---


# 14. Branch: time series and dependence over time

Cross-sectional econometrics often starts from observations indexed by individuals, firms or other units. Time-series econometrics instead studies variables indexed by time:

$
X_1,X_2,\ldots,X_T.
$

The ordering matters because observations at different dates may be statistically related.

## [Basic properties of time series](econometrics/time-series/basic-properties.md)

A time series is modeled as a stochastic process `{X_t}`. The observed values `{x_t}` form one realization of that process.

The first objects we use to describe the process are:

$
E(X_t)
$

for its mean and

$
\operatorname{Cov}(X_t,X_{t-h})
$

for dependence between observations `h` periods apart.

This leads to the autocovariance function.

### Why stationarity enters

With only one observed historical path, we need some stability over time if observations from different periods are to teach us about the same underlying relationships.

Weak stationarity requires:

$
E(X_t)=\mu
$

and

$
\operatorname{Cov}(X_t,X_{t-h})=\gamma(h).
$

The second condition says that dependence may vary with the lag `h`, but not with the calendar date `t`.

Because variance is the lag-zero autocovariance,

$
\operatorname{Var}(X_t)=\gamma(0),
$

weak stationarity also implies constant variance.

### From autocovariance to autocorrelation

The autocorrelation function standardizes the autocovariance:

$
\rho(h)=\frac{\gamma(h)}{\gamma(0)}.
$

It tells us how strongly values separated by `h` periods are linearly related on a scale from -1 to 1.

This creates a new econometric branch:

```text
[Random variables and covariance]
        |
        v
[Stochastic process {X_t}]
        |
        v
[Mean and autocovariance over time]
        |
        v
[Weak stationarity]
        |
        +--> [Autocorrelation / ACF]
        |
        +--> [White noise]
        |
        +--> [Random walk and non-stationarity]
        |
        +--> [Differencing and transformations]
        |
        v
[ARMA and later time-series models]
```

This branch will be expanded only as those topics are actually studied.

---

# 15. The current trunk

At the current stage, the main conceptual chain is:

```text
[Random variables]
        |
        v
[Expectation]
        |
        +--> [Variance / covariance / moments]
        |
        v
[Conditional expectation]
        |
        v
[Parameters and estimators]
        |
        v
[Sampling distributions]
        |
        +--> [Unbiasedness]
        |
        +--> [LLN] --> [Consistency]
        |
        +--> [CLT] --> [Asymptotic normality]
        |
        v
[Conditional mean E[Y|X]]
        |
        v
[Linear regression model]
        |
        +--> [Correct specification]
        |
        +--> [Exogeneity]
        |
        v
[OLS]
        |
        +--> [Sampling distribution of OLS]
        |       |
        |       +--> little variation in X
        |       +--> correlated regressors
        |       +--> homoskedasticity / heteroskedasticity
        |       +--> test statistics and confidence intervals
        |
        +--> [R-squared]
        |
        +--> normality branch
                |
                +--> exact normal inference
                +--> [Maximum likelihood]

[Variance / covariance / moments]
        |
        +--> [Stochastic process over time]
                |
                +--> [Weak stationarity]
                |       |
                |       +--> [Autocorrelation / ACF]
                |
                +--> [White noise / random walk]
                |
                +--> [Differencing]
                        |
                        +--> later ARMA and non-stationary models
```

The labels above correspond to the linked sections in this document.

---

# 16. Assumption map

A useful way to study econometrics is to ask what each assumption actually buys us.

| Assumption or condition | What it gives us | What happens if it fails? |
|---|---|---|
| iid or suitable weak dependence | clean repeated-sampling theory | LLN/CLT may need modification |
| finite moments | expectations/variances and asymptotic tools exist | some standard results can fail |
| correct conditional mean | regression targets $E[Y\mid X]$ correctly | specification error |
| exogeneity | OLS targets the intended population coefficient | bias/inconsistency can arise |
| sufficient variation in $X$ | precise slope estimation | large standard errors |
| no perfect multicollinearity | separate coefficients can be estimated | OLS coefficients not separately identified |
| homoskedasticity | classical OLS variance formula | need robust variance estimation |
| normality | exact finite-sample normal likelihood/inference | often use asymptotic theory instead |
| large $n$ plus regularity conditions | LLN and CLT approximations become useful | asymptotic approximations may be poor |
| weak stationarity in a time-series setting | stable mean, variance and lag-based dependence structure | historical periods may not describe one stable probabilistic relationship |

---

# 17. How to use this map

When learning a new result, do not only ask:

> What is the formula?

Also ask:

1. What problem are we trying to solve?
2. Which earlier concept does this result depend on?
3. Which assumption is doing the work?
4. What would happen if that assumption were removed?
5. Is the result exact, conditional, finite-sample, or asymptotic?
6. Which permanent note contains the detailed treatment?

The goal is to turn econometrics into a connected story rather than a collection of formulas.

---

# 18. Current linked notes

## Probability

- [Random variables and distributions](probability/random-variables-and-distributions.md)
- [Joint distributions, independence and iid sampling](probability/joint-distributions-independence-and-iid.md)
- [Expectation](probability/expectation.md)
- [Conditional expectation](probability/conditional-expectation.md)
- [Variance, covariance and moments](probability/variance-covariance-and-moments.md)
- [Law of Large Numbers](probability/law-of-large-numbers.md)
- [Central Limit Theorem](probability/central-limit-theorem.md)

## Statistics

- [Parameters, estimators and estimates](statistics/parameters-estimators-and-estimates.md)
- [Sampling distributions](statistics/sampling-distributions.md)
- [Unbiasedness](statistics/unbiasedness.md)
- [Consistency](statistics/consistency.md)
- [Asymptotic normality](statistics/asymptotic-normality.md)

## Econometrics

- [Econometrics index](econometrics/README.md)
- [Linear regression index](econometrics/linear-regression/README.md)
- [Linear regression model](econometrics/linear-regression/linear-regression-model.md)
- [Correct specification](econometrics/linear-regression/correct-specification.md)
- [Exogeneity](econometrics/linear-regression/exogeneity.md)
- [Ordinary Least Squares](econometrics/linear-regression/ordinary-least-squares.md)
- [Sampling distribution of OLS](econometrics/linear-regression/sampling-distribution-of-ols.md)
- [Maximum likelihood index](econometrics/maximum-likelihood/README.md)
- [Maximum likelihood](econometrics/maximum-likelihood/maximum-likelihood.md)
- [Time series index](econometrics/time-series/README.md)
- [Basic properties of time series](econometrics/time-series/basic-properties.md)

## Course connection

- [Introductory Econometrics course map](../courses/introductory-econometrics-for-business-and-economics/course-map.md)

---

# Review log

| Date | Result | Next action |
|---|---|---|
| 2026-08-09 | Initial intuitive foundations map created | Extend branches only when new material is actually studied |
| 2026-09-05 | Added the time-series branch through stochastic processes, autocovariance and weak stationarity | Extend toward white noise, random walks and differencing as Week 1 is completed |
