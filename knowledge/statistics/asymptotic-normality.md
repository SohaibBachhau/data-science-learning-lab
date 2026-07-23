---
title: Asymptotic Normality
subject: statistics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - consistency
  - central limit theorem
  - convergence in distribution
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - asymptotic normality
  - limiting distributions
  - inference
---

# Asymptotic Normality

## Central question

What does it mean for an estimator to be approximately normally distributed in large samples, and why is the estimator multiplied by $\sqrt{n}$?

## Short answer

An estimator is asymptotically normal when its centered and properly scaled estimation error converges in distribution to a normal random variable. A common form is

$$
\sqrt{n}(\hat\theta_n-\theta_0)
\overset{d}{\longrightarrow}
N(0,V).
$$

This result provides large-sample standard errors, confidence intervals and hypothesis tests.

## Intuition

Consistency says that $\hat\theta_n-\theta_0$ becomes small. Asymptotic normality describes the remaining uncertainty after magnifying that shrinking error by $\sqrt{n}$.

Without scaling, a consistent estimator often converges to the constant $\theta_0$, so its limiting distribution is degenerate. Scaling reveals the nontrivial shape of the estimation error.

## Formal statement

The statement

$$
\sqrt{n}(\hat\theta_n-\theta_0)
\overset{d}{\longrightarrow}
N(0,V)
$$

means that the distribution of the scaled estimation error approaches a normal distribution with mean zero and variance $V$.

For large $n$, this motivates

$$
\hat\theta_n
\approx
N\left(\theta_0,\frac{V}{n}\right).
$$

This is a finite-sample approximation derived from a limiting result.

## Why $\sqrt{n}$ scaling is common

Many estimators are functions of sample averages. A sample average typically has variance proportional to $1/n$, so its standard deviation is proportional to $1/\sqrt{n}$.

Therefore,

$$
\hat\theta_n-\theta_0=O_p(n^{-1/2})
$$

for a root-$n$ consistent estimator. Multiplying by $\sqrt{n}$ produces a limiting distribution with finite nonzero variance.

## Standardized form

If $V>0$, then

$$
\frac{\sqrt{n}(\hat\theta_n-\theta_0)}{\sqrt{V}}
\overset{d}{\longrightarrow}
N(0,1).
$$

Because $V$ is usually unknown, it is replaced by a consistent estimator $\hat V_n$. Slutsky's theorem then gives

$$
\frac{\sqrt{n}(\hat\theta_n-\theta_0)}{\sqrt{\hat V_n}}
\overset{d}{\longrightarrow}
N(0,1).
$$

## Large-sample standard error

From

$$
\hat\theta_n
\approx
N\left(\theta_0,\frac{V}{n}\right),
$$

an approximate standard deviation is

$$
\sqrt{\frac{V}{n}}.
$$

The estimated standard error is therefore

$$
\operatorname{SE}(\hat\theta_n)
=
\sqrt{\frac{\hat V_n}{n}}.
$$

Notation differs across textbooks. Sometimes the estimated variance of $\hat\theta_n$ itself is denoted directly by $\widehat{\operatorname{Var}}(\hat\theta_n)$.

## Confidence interval

An approximate two-sided $(1-\alpha)$ confidence interval is

$$
\hat\theta_n
\pm
z_{1-\alpha/2}\operatorname{SE}(\hat\theta_n),
$$

where $z_{1-\alpha/2}$ is the relevant standard normal critical value.

For a 95 percent interval,

$$
z_{0.975}\approx 1.96.
$$

The confidence level concerns the long-run coverage of the interval procedure across repeated samples, not a probability assigned to a fixed parameter after one interval has been observed.

## Hypothesis test

To test

$$
H_0:\theta_0=\theta_{null},
$$

use the statistic

$$
t
=
\frac{\hat\theta_n-\theta_{null}}
{\operatorname{SE}(\hat\theta_n)}.
$$

Under the null and regularity conditions,

$$
t\overset{d}{\longrightarrow}N(0,1).
$$

This justifies comparing the statistic with standard normal critical values in large samples.

## Asymptotic normality of OLS

For simple OLS without an intercept,

$$
\sqrt{n}(\hat\beta_n-\beta)
=
\frac{\frac{1}{\sqrt{n}}\sum_{i=1}^nX_i u_i}
{\frac{1}{n}\sum_{i=1}^nX_i^2}.
$$

The numerator is handled by a central limit theorem. The denominator is handled by a law of large numbers. Slutsky's theorem combines both limits.

Under appropriate assumptions,

$$
\sqrt{n}(\hat\beta_n-\beta)
\overset{d}{\longrightarrow}
N\left(
0,
\frac{E[X_i^2u_i^2]}{(E[X_i^2])^2}
\right),
$$

where $E[X_i u_i]=0$ has been used. Under homoskedasticity, this variance simplifies.

## Consistency and asymptotic normality

Asymptotic normality of the centered error usually implies consistency when the scaling diverges, such as $\sqrt{n}$, because

$$
\hat\theta_n-\theta_0
=
\frac{1}{\sqrt{n}}
\sqrt{n}(\hat\theta_n-\theta_0)
\overset{p}{\longrightarrow}0.
$$

However, consistency alone does not imply asymptotic normality. A consistent estimator can converge at a different rate or have a non-normal limiting distribution.

## Exact normality versus asymptotic normality

Exact normality means the estimator has a normal distribution for the stated finite sample size under the model assumptions.

Asymptotic normality means only that a transformed distribution approaches normality as $n$ grows.

In classical regression with normal errors and fixed regressors, OLS can have an exact conditional normal distribution. Under more realistic assumptions, normality is usually a large-sample approximation.

## Failure cases

Asymptotic normality can fail when:

- the relevant variance is infinite;
- observations have strong dependence not covered by the theorem;
- a parameter lies on a boundary;
- the model is weakly identified;
- the estimator is nonregular;
- a few extreme observations dominate the sample;
- the estimator converges at a rate other than $\sqrt{n}$.

## Common mistakes

- Saying the estimator itself converges in distribution to a non-degenerate normal distribution when it is consistent.
- Forgetting to center at the correct target.
- Forgetting the $\sqrt{n}$ scaling.
- Treating the asymptotic approximation as exact in a small sample.
- Using a normal limiting distribution without consistently estimating its variance.
- Assuming consistency automatically implies asymptotic normality.
- Mixing the asymptotic variance $V$ with the approximate finite-sample variance $V/n$.

## Retrieval questions

1. State a standard asymptotic normality result.
2. Why is the estimation error multiplied by $\sqrt{n}$?
3. What is the difference between $V$ and $V/n$ in the approximation?
4. How does a consistent variance estimator enter a standardized statistic?
5. What roles do the CLT, LLN and Slutsky's theorem play in OLS?
6. What is the difference between exact and asymptotic normality?
7. Why does consistency not guarantee asymptotic normality?

## Connections

- [Sampling distributions](sampling-distributions.md)
- [Consistency](consistency.md)
- [Central limit theorem](../probability/central-limit-theorem.md)
- [Sampling distribution of OLS](../econometrics/linear-regression/sampling-distribution-of-ols.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on least-squares normality.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Translate a limiting distribution into an approximate standard error |
