---
title: Measures of Fit in Simple Linear Regression
subject: econometrics
status: developing
created: 2026-10-01
updated: 2026-10-01
last_reviewed: 2026-10-01
prerequisites:
  - ordinary least squares
  - fitted values and residuals
sources:
  - VU Introductory Econometrics for Business and Economics, Week 2 slides
tags:
  - R-squared
  - residual sum of squares
  - standard error of regression
  - RMSE
  - goodness of fit
---

# Measures of Fit in Simple Linear Regression

## Central question

After fitting an OLS line, how can we describe how well that line fits the observed sample?

## Short answer

The course uses two complementary ideas. $R^2$ measures the fraction of the sample variation in $Y$ explained by the regression, while the standard error of the regression, SER, measures the typical size of the residual in the units of $Y$. RMSE measures essentially the same residual size as SER but uses $n$ rather than $n-2$ in the denominator.

## Starting point: actual, predicted and residual

For each observation,

$$
Y_i=\hat Y_i+\hat u_i,
$$

where

$$
\hat Y_i=\hat\beta_0+\hat\beta_1X_i
$$

is the fitted value and

$$
\hat u_i=Y_i-\hat Y_i
$$

is the OLS residual.

The residual is observable after estimating the regression, but it carries a hat because it is an estimate of the unobserved population error $u_i$.

## Total, explained and residual variation

The total sum of squares is

$$
TSS
=
\sum_{i=1}^n
(Y_i-\bar Y)^2.
$$

It measures the total sample variation in $Y$ around its sample mean.

The explained sum of squares is

$$
ESS
=
\sum_{i=1}^n
(\hat Y_i-\bar Y)^2.
$$

It measures the part of the variation in $Y$ represented by movement in the fitted values.

The course denotes the residual sum of squares by

$$
RSS
=
\sum_{i=1}^n
\hat u_i^2.
$$

This is the part left unexplained by the fitted regression.

With an intercept, OLS gives the decomposition

$$
TSS=ESS+RSS.
$$

So the total variation is split into explained variation and residual variation.

## R-squared

The regression $R^2$ is

$$
R^2
=
\frac{ESS}{TSS}.
$$

Using $TSS=ESS+RSS$, this is equivalently

$$
R^2
=
1-\frac{RSS}{TSS}.
$$

The course interpretation is the fraction of the sample variance of $Y$ explained by the regression.

Its range in this simple OLS setting with an intercept is

$$
0\leq R^2\leq1.
$$

An $R^2$ of $0.70$ means that 70% of the sample variation in $Y$ is explained by the fitted regression.

A higher $R^2$ means a better in-sample fit, holding the outcome and sample fixed. A low $R^2$ does not by itself imply that a regression is useless.

## Standard error of the regression

The standard error of the regression is

$$
SER
=
\sqrt{
\frac{1}{n-2}
\sum_{i=1}^n
\hat u_i^2
}.
$$

The SER measures the typical size of an OLS residual.

It has the same units as $Y$. For example, if $Y$ is measured in test-score points, the SER is also measured in test-score points.

A lower SER means smaller residuals on average and therefore a tighter in-sample fit, when comparing models for the same outcome on the same data.

## Why the denominator is n minus 2

The denominator $n-2$ is a degrees-of-freedom correction.

In simple linear regression, two parameters are estimated from the sample:

$$
\beta_0
\quad\text{and}\quad
\beta_1.
$$

They are estimated by $\hat\beta_0$ and $\hat\beta_1$, so two degrees of freedom are used. This leaves

$$
n-2
$$

for estimating the residual spread.

This parallels the ordinary sample-variance correction $n-1$, where one parameter, the sample mean, has been estimated.

## Why the mean residual is zero

The first-order condition for the OLS intercept gives

$$
\sum_{i=1}^n\hat u_i=0.
$$

Therefore,

$$
\bar{\hat u}
=
\frac{1}{n}
\sum_{i=1}^n\hat u_i
=
0.
$$

This is why the SER can be written directly using $\sum_i\hat u_i^2$ rather than deviations of the residuals from their own mean.

## RMSE

The root mean squared error is

$$
RMSE
=
\sqrt{
\frac{1}{n}
\sum_{i=1}^n
\hat u_i^2
}.
$$

The course treats RMSE and SER as measuring essentially the same thing: the typical size of the residual.

The difference is the denominator:

$$
SER:\quad n-2,
$$

$$
RMSE:\quad n.
$$

For the same fitted regression,

$$
RMSE<SER
$$

when $n>2$, because RMSE divides the same sum of squared residuals by the larger denominator $n$ before taking the square root.

As $n$ becomes large, the numerical difference between $n$ and $n-2$ becomes small.

## R-squared versus SER and RMSE

These measures answer different questions.

$R^2$ is unitless and asks what fraction of the sample variation in $Y$ is explained.

SER and RMSE retain the units of $Y$ and ask how large the residuals typically are.

For in-sample fit, and ignoring model-complexity or overfitting issues:

- higher $R^2$ indicates better fit;
- lower SER indicates better fit;
- lower RMSE indicates better fit.

These statements concern fit. They do not establish causality or correct specification.

## Course example

For the California test-score regression, the Week 2 slides report approximately

$$
R^2=0.05
$$

and

$$
SER=18.6.
$$

The first number says that the student-teacher-ratio regression explains about 5% of the sample variation in test scores. The second says that the residuals are typically on the order of 18.6 test-score points.

## Common mistakes

- Confusing the population error $u_i$ with the fitted residual $\hat u_i$.
- Thinking $R^2$ is measured in the units of $Y$.
- Interpreting a high $R^2$ as proof of causality.
- Assuming a low $R^2$ makes a regression automatically useless.
- Forgetting that SER uses $n-2$ in simple regression because two coefficients were estimated.
- Treating SER and RMSE as conceptually different measures of error size when, in this course, their main difference is the denominator.
- Comparing RMSE values across outcomes measured in different units without care.

## Retrieval questions

1. What does $TSS$ measure?
2. What is the difference between $ESS$ and $RSS$?
3. Why does $TSS=ESS+RSS$ hold for OLS with an intercept?
4. Interpret $R^2=0.70$ in words.
5. What does SER measure, and what are its units?
6. Why is the SER denominator $n-2$ in simple regression?
7. Why is $\bar{\hat u}=0$?
8. What is the difference between SER and RMSE?
9. Why can a low $R^2$ still be compatible with a useful regression?

## Connections

- [Linear regression model](linear-regression-model.md)
- [Ordinary least squares](ordinary-least-squares.md)
- [Sampling distribution of OLS](sampling-distribution-of-ols.md)

## Sources

- VU *Introductory Econometrics for Business and Economics*, Week 2 slides, sections on predicted values, residuals, $R^2$, SER and RMSE.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-10-01 | Reviewed $TSS=ESS+RSS$, $R^2$, SER, RMSE, residual notation and the $n-2$ degrees-of-freedom correction | Reuse these measures when multiple regression introduces adjusted $R^2$ |
