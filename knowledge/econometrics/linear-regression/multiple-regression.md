---
title: Multiple Regression and Adjusted Fit
status: developing
updated: 2026-10-31
sources:
  - IEBE Week 4 lecture slides
  - October 19 study session
tags: [multiple-regression, interpretation, adjusted-r-squared]
---

# Multiple Regression and Adjusted Fit

## Central question

What changes when we move from one explanatory variable to several, and how should we interpret a coefficient?

## Intuition

A simple regression compares outcomes across observations with different values of one regressor, allowing all other characteristics to vary alongside it. Multiple regression attempts to isolate the association between $Y$ and one regressor **holding the others fixed**. It is useful when the explanatory variables are correlated and we want to distinguish their partial contributions.

## Model and interpretation

With $k$ regressors and an intercept,

$$
Y_i=\beta_0+\beta_1X_{1i}+\cdots+\beta_kX_{ki}+u_i.
$$

Here $Y_i$ is observation $i$'s outcome, $X_{ji}$ its value of regressor $j$, $\beta_j$ a population coefficient and $u_i$ an error term.

If the conditional mean is correctly specified so that $E[u_i\mid X_{1i},\ldots,X_{ki}]=0$, increasing $X_j$ by one unit while **holding all other regressors fixed** changes the conditional expected outcome by $\beta_j$. This is a partial association, not automatically a causal effect. A causal reading needs additional identification assumptions.

### Example

The lecture contrasts

$$
\widehat{TestScore}=698.9-2.28\,STR
$$

with

$$
\widehat{TestScore}=686.0-1.10\,STR-0.65\,PctEL.
$$

In the second fitted regression, the $-1.10$ coefficient means one more student per teacher is associated with a predicted score about 1.10 points lower **at the same percentage of English learners**. It is not the change from moving both STR and PctEL together.

## OLS with several regressors

The coefficient estimates minimize the residual sum of squares:

$$
\min_{b_0,\ldots,b_k}\sum_{i=1}^n
\left(Y_i-b_0-\sum_{j=1}^k b_jX_{ji}\right)^2.
$$

Matrix notation makes the solution and its assumptions clearer; see [Matrix OLS and projections](matrix-ols-and-projections.md).

The fitted and residual values satisfy

$$
\hat Y_i=\hat\beta_0+\sum_{j=1}^k\hat\beta_jX_{ji},
\qquad
\hat u_i=Y_i-\hat Y_i.
$$

With an intercept, sample residuals sum to zero and are orthogonal in sample to every included regressor. These are **algebraic OLS identities**, not proof of population exogeneity.

## Model fit: $R^2$, adjusted $R^2$, SER and RMSE

Define $\mathrm{RSS}=\sum_i\hat u_i^2$ and $\mathrm{TSS}=\sum_i(Y_i-\bar Y)^2$, where $\bar Y$ is the sample mean of $Y$. For an OLS model with an intercept and nonzero TSS,

$$
R^2=1-\frac{\mathrm{RSS}}{\mathrm{TSS}}.
$$

Adding regressors cannot lower ordinary in-sample $R^2$, even if they add little useful information. **Adjusted $R^2$** includes a degrees-of-freedom penalty:

$$
\boxed{\bar R^2=1-\frac{n-1}{n-k-1}\frac{\mathrm{RSS}}{\mathrm{TSS}}}
=1-\frac{n-1}{n-k-1}(1-R^2),
$$

where $n$ is sample size and $k$ counts regressors *excluding* the intercept. We require $n>k+1$.

Other measures of the residual spread, in units of $Y$, are

$$
SER=\sqrt{\frac{\mathrm{RSS}}{n-k-1}},
\qquad
RMSE=\sqrt{\frac{\mathrm{RSS}}{n}}.
$$

Under the usual intercept setup and $k>0$, $\bar R^2\leq R^2$; adjusted $R^2$ can be negative. Neither metric independently proves causation or out-of-sample prediction quality.

### Our adjusted-$R^2$ comparison

Both models used $n=100$ observations:

| Model | Regressors $k$ | $R^2$ | Calculation | Adjusted $R^2$ |
|---|---:|---:|---|---:|
| A | 2 | 0.50 | $1-(99/97)(0.50)$ | $0.4897$ |
| B | 3 | 0.51 | $1-(99/96)(0.49)$ | $0.4947$ |

Model B wins by adjusted $R^2$ **because** the small fit improvement outweighs the extra-regressor penalty. During practice we corrected the mistaken statement that B had the smaller *ordinary* $R^2$: its ordinary $R^2$ is higher, but that alone is not the adjusted-fit decision rule.

## Assumptions and limitations

Useful least-squares conditions in the course are: zero conditional error mean, iid observations, sufficient finite moments, and no perfect multicollinearity (full column rank). Homoskedasticity is an **additional** condition for the simple OLS covariance formula and the Gauss-Markov result; conditional normality is an additional condition for conventional exact Normal-based inference.

Strong correlation among regressors without exact dependence leaves OLS computable but may make individual coefficient estimates imprecise. See [Multicollinearity and dummy variables](multicollinearity-and-dummies.md).

## Common mistakes

- Reading a multiple-regression coefficient as an unconditional effect.
- Assuming “holding constant” itself guarantees causality.
- Believing $R^2$ can fall when another regressor is added to the **same** OLS sample with an intercept.
- Confusing $k$ with the number of coefficients including the intercept.
- Believing adjusted $R^2$ must rise when ordinary $R^2$ rises.

## Retrieval questions

1. What does “holding the other variables constant” mean?
2. Why did the STR coefficient change when PctEL was included?
3. Why does ordinary $R^2$ never decrease when adding a regressor?
4. When can adjusted $R^2$ decrease?
5. How do SER and RMSE differ in their denominators?

## Connections

- [Omitted-variable bias](omitted-variable-bias.md)
- [Matrix OLS and projections](matrix-ols-and-projections.md)
- [Measures of fit in simple regression](measures-of-fit.md)
- [Exogeneity](exogeneity.md)

## Sources and review log

- IEBE Week 4 lecture slides, multiple-regression and fit sections; explanations paraphrased.
- October 19, 2026: completed adjusted-fit numerical comparison; status remains `developing`.
