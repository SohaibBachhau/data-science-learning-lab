---
title: Hypothesis Testing and Confidence Intervals
subject: statistics
status: developing
created: 2026-09-30
updated: 2026-09-30
last_reviewed: 2026-09-30
prerequisites:
  - sampling distributions
  - standard errors
  - asymptotic normality
sources:
  - VU Knowledge Clip Series: Statistics, Hypothesis Testing, p-Value, and Confidence Intervals
  - VU Knowledge Clip Series: Statistics exercises, Section 5.1
tags:
  - hypothesis testing
  - p-value
  - confidence intervals
  - t-test
  - inference
---

# Hypothesis Testing and Confidence Intervals

## Central question

How can a random sample be used to assess a claim about an unknown population parameter while accounting for sampling uncertainty?

## Short answer

A hypothesis test compares an estimate with the value claimed under a null hypothesis and scales the difference by its standard error. A p-value measures how extreme the observed test statistic is under the null. A confidence interval gives a range of parameter values that are compatible with the data at the corresponding confidence level.

## Intuition

A difference between an estimate and a hypothesized value does not by itself tell us much. The same numerical difference can be small when the estimator is noisy and large when the estimator is precise.

The test statistic therefore asks how many standard errors the estimate lies away from the value claimed under the null.

For a population mean, the course writes

$$
t
=
\frac{\bar X-\mu_0}{SE(\bar X)}.
$$

Here:

- $\bar X$ is the sample mean;
- $\mu_0$ is the value claimed under the null hypothesis;
- $SE(\bar X)$ measures sampling uncertainty.

## Null and alternative hypotheses

A two-sided test can be written as

$$
H_0:\mu=\mu_0
$$

against

$$
H_1:\mu\neq\mu_0.
$$

The null hypothesis is the claim we start with. The alternative is what we test against.

## Standard error of the sample mean

For an iid sample, the course uses

$$
SE(\bar X)
=
\frac{s}{\sqrt n},
$$

where

$$
s^2
=
\frac{1}{n-1}
\sum_{i=1}^n
(X_i-\bar X)^2.
$$

Thus,

$$
t
=
\frac{\sqrt n(\bar X-\mu_0)}{s}.
$$

## Why the test statistic is approximately standard Normal

Under the null hypothesis, $\mu=\mu_0$, so

$$
t
=
\frac{\sqrt n(\bar X-\mu)}{s}.
$$

Rewrite this as

$$
t
=
\frac{\sqrt n(\bar X-\mu)}{\sigma}
\cdot
\frac{\sigma}{s}.
$$

The Central Limit Theorem gives

$$
\frac{\sqrt n(\bar X-\mu)}{\sigma}
\overset{d}{\longrightarrow}
N(0,1).
$$

Consistency of the sample variance gives

$$
s
\overset{p}{\longrightarrow}
\sigma,
$$

so

$$
\frac{\sigma}{s}
\overset{p}{\longrightarrow}
1.
$$

By Slutsky's theorem,

$$
t
\overset{d}{\longrightarrow}
N(0,1).
$$

This is an asymptotic result.

## Critical-value decision rule

For the large-sample two-sided 5% test used in the course, the standard Normal critical values are approximately

$$
-1.96
\quad\text{and}\quad
1.96.
$$

Therefore,

$$
|t_{calc}|>1.96
$$

leads to rejection of $H_0$ at the 5% significance level.

If

$$
|t_{calc}|\leq1.96,
$$

we fail to reject $H_0$.

Failing to reject the null is not the same as proving or accepting that the null is true.

## p-value

The p-value is the probability, under $H_0$, of obtaining a test statistic at least as extreme as the observed one.

For the two-sided setting, larger values of $|t_{calc}|$ correspond to smaller p-values.

At the 5% significance level, the course decision rule is

$$
p\leq0.05
\quad\Rightarrow\quad
\text{reject }H_0.
$$

The p-value is calculated under the null hypothesis. It is not the probability that the null hypothesis is true.

## Confidence interval

The course gives the large-sample 95% confidence interval for a mean as

$$
\left[
\bar X-1.96SE(\bar X),
\;
\bar X+1.96SE(\bar X)
\right].
$$

More generally, the large-sample $(1-\alpha)100\%$ interval is

$$
\left[
\bar X-z_{1-\alpha/2}SE(\bar X),
\;
\bar X+z_{1-\alpha/2}SE(\bar X)
\right].
$$

## Frequentist interpretation of a confidence interval

A 95% confidence interval is a procedure that, if repeated over many new samples, would contain the true parameter about 95% of the time.

The parameter is treated as fixed. Therefore the course interpretation is not that there is a 95% probability that the already constructed interval contains the fixed parameter.

## Connection between tests and confidence intervals

For the corresponding two-sided 5% test and 95% confidence interval:

- if $\mu_0$ lies outside the confidence interval, reject $H_0:\mu=\mu_0$;
- if $\mu_0$ lies inside the confidence interval, fail to reject $H_0$.

These are two ways of expressing the same large-sample inference decision.

## Exact t distribution under Normal sampling

If, in addition, the observations are Normally distributed, the course states that under the null

$$
t\mid H_0
\sim
t_{n-1}.
$$

This is an exact finite-sample result under that additional Normality assumption.

The large-sample standard Normal approximation instead uses

$$
t\mid H_0
\approx
N(0,1).
$$

For smaller samples, the exact $t_{n-1}$ distribution has heavier tails than the standard Normal. As the degrees of freedom increase, the t distribution approaches the standard Normal.

## Example

Suppose

$$
\bar X=18,
\qquad
\mu_0=20,
\qquad
SE(\bar X)=1.
$$

Then

$$
t
=
\frac{18-20}{1}
=
-2.
$$

For the two-sided 5% large-sample rule,

$$
|-2|=2>1.96,
$$

so the null is rejected.

The sign shows the direction of the difference, while the absolute value determines extremeness in the two-sided test.

## Common mistakes

- Looking only at $\bar X-\mu_0$ and ignoring the standard error.
- Forgetting the sign of the test statistic.
- Saying that failing to reject $H_0$ proves $H_0$ is true.
- Interpreting the p-value as the probability that $H_0$ is true.
- Saying that a realized 95% confidence interval contains the fixed parameter with 95% probability.
- Treating the large-sample $N(0,1)$ approximation as an exact finite-sample statement.
- Forgetting that the exact $t_{n-1}$ result in the exercise uses the additional Normal sampling assumption.

## Retrieval questions

1. Why do we divide $\bar X-\mu_0$ by a standard error?
2. What does the sign of a test statistic tell us?
3. Why does a larger $|t|$ correspond to a smaller p-value?
4. What is the 5% two-sided critical-value rule under the standard Normal approximation?
5. Why do we say "fail to reject" rather than "accept" the null?
6. How should a 95% confidence interval be interpreted in repeated samples?
7. How are a two-sided 5% test and a 95% confidence interval connected?
8. How do the CLT, consistency of $s$, and Slutsky's theorem justify the large-sample t-statistic?
9. When does the course use the exact $t_{n-1}$ distribution?

## Connections

- [Sampling distributions](sampling-distributions.md)
- [Asymptotic normality](asymptotic-normality.md)
- [Consistency](consistency.md)
- [Central Limit Theorem](../probability/central-limit-theorem.md)
- [Convergence in distribution and Slutsky's theorem](../probability/convergence-in-distribution.md)

## Sources

- VU Knowledge Clip Series: Statistics, *Hypothesis Testing, p-Value, and Confidence Intervals*.
- VU Knowledge Clip Series: Statistics exercises, Section 5.1, *t-test*.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-09-30 | Reviewed null and alternative hypotheses, t-statistics, p-values, critical values, confidence intervals, and the CLT plus Slutsky derivation | Reuse these ideas when testing regression coefficients |
