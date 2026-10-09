---
title: Week 3 - Simple Linear Regression Inference
course: Introductory Econometrics for Business and Economics
status: developing
created: 2026-10-09
updated: 2026-10-09
last_reviewed: 2026-10-09
sources:
  - IEBE Week 3 slides
tags:
  - OLS
  - inference
  - standard errors
  - robust standard errors
  - t-statistic
  - hypothesis testing
  - p-value
  - confidence intervals
---

# Week 3: Simple Linear Regression Inference

## Central question

How do we use one estimated OLS coefficient and its sampling uncertainty to make statements about the unknown population coefficient?

## The big picture

The population coefficient $\beta_1$ is fixed but unknown. The OLS estimator $\hat\beta_1$ is random before the sample is observed because different random samples generally produce different estimates.

The Week 3 inference chain is:

```text
unknown population coefficient beta_1
-> random sample
-> estimate beta_hat_1
-> sampling distribution of beta_hat_1
-> variance / estimated variance / standard error
-> t-statistic
-> hypothesis test and p-value
-> confidence interval
```

Inference means using the observed sample, together with a model of sampling uncertainty, to learn about the unknown population parameter.

## 1. Sampling distribution of the OLS slope

The sampling distribution of $\hat\beta_1$ is the distribution of the values we would obtain if we repeatedly drew new random samples from the same population and recomputed the OLS slope each time.

Under the least-squares assumptions used in the course,

$$
E[\hat\beta_1]=\beta_1.
$$

So the sampling distribution is centered on the true population slope.

Its spread is measured by

$$
\operatorname{Var}(\hat\beta_1).
$$

A smaller variance means that repeated samples produce estimates that cluster more tightly around the population coefficient.

Once one sample has actually been observed, the numerical estimate is fixed. The randomness refers to the estimator across hypothetical repeated samples.

## 2. Large-sample normality

The exact finite-sample distribution of $\hat\beta_1$ can be complicated. In large samples, the Week 3 slides use the approximation

$$
\hat\beta_1
\overset{a}{\sim}
N\left(\beta_1,\sigma_{\hat\beta_1}^2\right).
$$

Equivalently,

$$
\frac{\hat\beta_1-\beta_1}{\sigma_{\hat\beta_1}}
\overset{d}{\longrightarrow}
N(0,1).
$$

The standardized expression measures the estimation error in units of the true sampling standard deviation.

This large-sample normal approximation is what allows us to use standard Normal critical values for hypothesis tests and confidence intervals.

## 3. Variance, estimated variance and standard error

These three objects should not be mixed up.

The true sampling variance is

$$
\operatorname{Var}(\hat\beta_1)
=
\sigma_{\hat\beta_1}^2.
$$

It describes the actual spread of the estimator across repeated samples. It is a population quantity and is generally unknown.

The estimated variance is

$$
\hat\sigma_{\hat\beta_1}^2.
$$

It is calculated from the observed sample and estimates the unknown sampling variance.

The standard error is

$$
SE(\hat\beta_1)
=
\sqrt{\hat\sigma_{\hat\beta_1}^2}.
$$

The standard error is therefore the estimated standard deviation of the sampling distribution of $\hat\beta_1$.

### Interpretation

A small standard error means the coefficient is estimated relatively precisely.

A large standard error means the coefficient is estimated relatively imprecisely.

For example, if

$$
\widehat{\operatorname{Var}}(\hat\beta_1)=0.16,
$$

then

$$
SE(\hat\beta_1)=\sqrt{0.16}=0.4.
$$

## 4. Homoskedasticity and robust standard errors

Homoskedasticity means that the conditional error variance is constant:

$$
\operatorname{Var}(u_i\mid X_i)=\sigma_u^2.
$$

Heteroskedasticity means that this conditional variance can change with $X_i$.

Under the original least-squares assumptions, heteroskedasticity does not by itself change the OLS coefficient estimate or automatically make OLS biased. The problem is that a standard-error formula that incorrectly assumes homoskedasticity can estimate the sampling variance incorrectly.

Heteroskedasticity-robust standard errors are designed to remain valid in large samples whether the errors are homoskedastic or heteroskedastic.

The practical distinction is:

```text
same OLS coefficient estimate
        |
        +-- homoskedasticity-only SE
        |
        +-- heteroskedasticity-robust SE
                |
                +-- possibly different t-statistic
                +-- possibly different p-value
                +-- possibly different confidence interval
```

Robust standard errors change the estimated uncertainty, not the fitted OLS coefficient.

They are not guaranteed to be larger than conventional standard errors in every sample.

## 5. The t-statistic

To test

$$
H_0:\beta_1=\beta_{1,0},
$$

the course uses

$$
t
=
\frac{\hat\beta_1-\beta_{1,0}}
{SE(\hat\beta_1)}.
$$

The best verbal interpretation is:

> The t-statistic tells us how many standard errors the estimated coefficient lies above or below the value assumed under the null hypothesis.

For example,

$$
t=-3.5
$$

means that $\hat\beta_1$ lies 3.5 standard errors below the null value.

The numerator must remain in the order

$$
\hat\beta_1-\beta_{1,0},
$$

because the sign matters for one-sided tests.

## 6. Two-sided hypothesis tests

A two-sided test has the form

$$
H_0:\beta_1=\beta_{1,0}
$$

against

$$
H_1:\beta_1\neq\beta_{1,0}.
$$

At the 5 percent level, the Week 3 large-sample rule is

$$
|t|>1.96
\quad\Rightarrow\quad
\text{reject }H_0.
$$

At the 1 percent level,

$$
|t|>2.58
\quad\Rightarrow\quad
\text{reject }H_0.
$$

Because the alternative allows deviations in either direction, both tails matter and the absolute value is used.

## 7. One-sided hypothesis tests

For a lower-tail alternative,

$$
H_0:\beta_1\geq\beta_{1,0}
$$

against

$$
H_1:\beta_1<\beta_{1,0},
$$

we reject at the 5 percent level when the statistic is sufficiently negative:

$$
t<-1.645.
$$

For an upper-tail alternative,

$$
H_0:\beta_1\leq\beta_{1,0}
$$

against

$$
H_1:\beta_1>\beta_{1,0},
$$

we reject at the 5 percent level when

$$
t>1.645.
$$

Do not use $|t|$ for a one-sided test. The direction of the alternative determines the relevant tail.

## 8. p-values

The p-value measures how extreme the observed statistic would be if the null hypothesis were true.

For a two-sided test,

$$
p
=
P\left(|t|>|t_{calc}|\mid H_0\right).
$$

A small p-value means the observed result would be unusual under $H_0$.

At significance level $\alpha$,

$$
p<\alpha
\quad\Rightarrow\quad
\text{reject }H_0.
$$

A p-value is not the probability that the null hypothesis is true.

For one-sided tests, only the tail specified by the alternative hypothesis is used.

## 9. Confidence intervals

A large-sample 95 percent confidence interval for $\beta_1$ is

$$
\hat\beta_1
\pm
1.96SE(\hat\beta_1).
$$

The margin of error is

$$
1.96SE(\hat\beta_1).
$$

For a corresponding two-sided 5 percent test:

$$
\beta_{1,0}\notin 95\%\text{ CI}
\iff
\text{reject }H_0,
$$

while

$$
\beta_{1,0}\in 95\%\text{ CI}
\iff
\text{do not reject }H_0.
$$

The frequentist interpretation is repeated-sampling based: if the procedure were repeated over many samples, about 95 percent of the constructed intervals would contain the fixed true parameter.

## 10. California test-score example from the slides

The Week 3 example estimates

$$
\widehat{TestScore}
=
698.9-2.28STR.
$$

Using the homoskedasticity-only standard error for the slope,

$$
SE(\hat\beta_1)=0.48.
$$

Testing

$$
H_0:\beta_1=0
$$

gives

$$
t
=
\frac{-2.28-0}{0.48}
=
-4.75.
$$

The null is rejected at both the 5 percent and 1 percent levels.

The slides also compare the conventional standard error with a heteroskedasticity-robust standard error. The coefficient estimate remains approximately

$$
\hat\beta_1=-2.279,
$$

while the robust standard error is about

$$
0.519.
$$

The point estimate does not change. The estimated uncertainty does.

## 11. Exam procedure

For a single-coefficient inference question:

1. Identify the null value $\beta_{1,0}$.
2. Check whether the alternative is two-sided, lower-tail or upper-tail.
3. Use the requested standard error, especially the robust SE when robust inference is requested.
4. Calculate
   $$
   t=\frac{\hat\beta_1-\beta_{1,0}}{SE(\hat\beta_1)}.
   $$
5. Choose the correct critical region from the alternative hypothesis.
6. State reject or do not reject $H_0$.
7. If a p-value is given, verify that it gives the same decision.
8. If a confidence interval is requested, calculate the margin first and then subtract and add it carefully.

## 12. Mistakes to avoid

- Using $|t|$ for a one-sided test.
- Forgetting that a negative t-statistic means the estimate lies below the null value.
- Reversing $\hat\beta_1-\beta_{1,0}$.
- Interpreting the p-value as $P(H_0\text{ is true})$.
- Saying "accept $H_0$" instead of "do not reject $H_0$."
- Thinking a robust standard error changes $\hat\beta_1$.
- Assuming a robust SE must always be larger.
- Confusing the variance of the errors with the variance of $\hat\beta_1$.
- Confusing the true sampling variance, its estimated variance and the standard error.
- Making arithmetic mistakes when adding and subtracting the confidence-interval margin.

## 13. Retrieval questions

1. What does the sampling distribution of $\hat\beta_1$ represent?
2. Why is $\hat\beta_1$ random before sampling but fixed after one sample is observed?
3. What is the difference between $\sigma_{\hat\beta_1}^2$, $\hat\sigma_{\hat\beta_1}^2$ and $SE(\hat\beta_1)$?
4. What does $t=-2.5$ mean in words?
5. Why can robust standard errors change a test decision without changing the OLS coefficient?
6. Why do we use $|t|$ for a two-sided test but not for a one-sided test?
7. What does a p-value mean under the null?
8. How are a 95 percent confidence interval and a two-sided 5 percent test connected?
9. Why does large-sample normality make inference possible?

## Connections

- [Sampling distributions](../../../knowledge/statistics/sampling-distributions.md)
- [Hypothesis testing and confidence intervals](../../../knowledge/statistics/hypothesis-testing-and-confidence-intervals.md)
- [Sampling distribution of OLS](../../../knowledge/econometrics/linear-regression/sampling-distribution-of-ols.md)
- [Asymptotic normality](../../../knowledge/statistics/asymptotic-normality.md)
- [Linear regression story](../../../knowledge/econometrics/linear-regression/story.md)

## Sources

- *Introductory Econometrics for Business and Economics*, Week 3 slides, especially the sections on sampling distributions, standard errors, hypothesis tests, confidence intervals and extended least-squares assumptions.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-10-09 | Reviewed the full inference chain and completed mixed calculations for t-tests and confidence intervals | Revisit with exam-style regression output and one-sided/two-sided mixed questions |
