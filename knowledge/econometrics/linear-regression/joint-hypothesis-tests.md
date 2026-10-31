---
title: Joint Hypothesis Tests: The First F-test
status: developing
updated: 2026-10-31
sources:
  - IEBE Week 5 lecture slides
  - October 19 study session
tags: [multiple-regression, joint-testing, F-test]
---

# Joint Hypothesis Tests: The First F-test

## Central question

How do we test whether **several** regression coefficients satisfy a proposed set of restrictions simultaneously?

## Why this matters

An individual $t$-test answers a question about one coefficient. A joint question such as “Do class size and expenditure matter together?” concerns a **set of restrictions**. Performing several separate 5% tests and rejecting if any one rejects generally produces a different overall false-rejection rate. A joint test takes the restrictions and dependence among estimators into account.

## Joint null and alternative

For a population model

$$
Y_i=\beta_0+\beta_1X_{1i}+\beta_2X_{2i}+\beta_3X_{3i}+u_i,
$$

consider

$$
H_0:\beta_1=0\text{ and }\beta_2=0.
$$

There are $q=2$ restrictions. The alternative says **at least one** of the restrictions is false. It does **not** require both coefficients to be nonzero.

Under $H_0$, we can exclude the first two regressors from this illustrative equation, leaving the restricted model with $X_3$ and an intercept. The unrestricted model includes all three.

## Why separate tests can fail

Imagine, solely for illustration, that two separate test statistics are independent and each test has a true-null rejection probability of 0.05. Rejecting the joint null when **either** individual test rejects produces

$$
P(\text{at least one false rejection})
=1-(1-0.05)^2
=0.0975.
$$

That is 9.75%, not the intended 5%. If the tests are correlated, the number is not generally 9.75%, but the naive procedure still lacks the intended general 5% calibration.

## Restricted versus unrestricted fits

Let $\mathrm{RSS}_R$ and $\mathrm{RSS}_U$ be the residual sums of squares from restricted and unrestricted OLS on the **same observations**, and let $q$ be the number of independent restrictions. The unrestricted fit cannot have a larger RSS because it permits at least as many coefficient choices:

$$
\mathrm{RSS}_U\leq\mathrm{RSS}_R.
$$

Under homoskedasticity, the familiar nested-model statistic is

$$
\boxed{
F=
\frac{(\mathrm{RSS}_R-\mathrm{RSS}_U)/q}
{\mathrm{RSS}_U/(n-k_U-1)}
},
$$

where $n$ is sample size and $k_U$ the number of unrestricted regressors excluding the intercept.

For models with an intercept and the same $Y$ observations, the equivalent $R^2$ form is

$$
\boxed{
F=
\frac{(R_U^2-R_R^2)/q}
{(1-R_U^2)/(n-k_U-1)}.
}
$$

The numerator is the extra fit gained per restriction removed. The denominator represents remaining unexplained variation per unrestricted residual degree of freedom. A sufficiently large statistic is evidence against **all restrictions holding simultaneously**.

### Lecture numerical example

The course compares a restricted model with $R_R^2=0.4149$ to an unrestricted model with $R_U^2=0.4366$, using $n=420$, $k_U=3$ and $q=2$:

$$
F=
\frac{(0.4366-0.4149)/2}{(1-0.4366)/(420-3-1)}
\approx 8.01.
$$

The restricted model removes class-size and expenditure regressors, keeping a language-background control. Since $8.01$ exceeds the approximate 5% critical value near 3 for an $F$ test with 2 numerator degrees of freedom and large denominator degrees of freedom, the joint null is rejected in this example.

## Scope and assumptions

The **RSS/$R^2$ formula above is homoskedasticity-only**. Under the classical normal linear model with the relevant conditional variance assumptions, its null reference distribution is exactly $F_{q,n-k_U-1}$. Under appropriate weaker assumptions it may be justified asymptotically, but one should not assume the conventional statistic is heteroskedasticity-robust.

A robust joint Wald test uses an estimated robust covariance matrix, which was listed as a **next step**, not completed in our October 19 session. The same is true for the full matrix derivation of general linear restrictions $R\beta=r$, restricted OLS by Lagrange multipliers, LR and LM tests. Keep those marked for future study rather than treating them as mastered.

## Individual versus joint significance

It is entirely possible for individual $t$ tests to look weak while a joint test is significant, particularly when coefficient estimates are correlated. Conversely, a joint rejection says only that the combined set of restrictions is not consistent with the data at the chosen level. It does not identify which specific coefficient is nonzero or imply a causal effect.

## Common mistakes

- Treating “and” in the joint null as “and” in the alternative; the alternative needs **at least one** violation.
- Using $q$ equal to the number of all coefficients rather than the number of restrictions.
- Mixing restricted and unrestricted $R^2$ values from different samples.
- Treating the overall regression F statistic as automatically the test of any chosen subset.
- Using the conventional $R^2$ formula while claiming robust inference.
- Concluding which coefficient is significant solely from joint rejection.

## Retrieval questions

1. Why is a pair of separate 5% tests not automatically a 5% joint test?
2. State the null and alternative when two coefficients should both be zero.
3. Which model is restricted and which has weakly higher $R^2$?
4. Explain each denominator and degree of freedom in the F formula.
5. Why is the simple $R^2$ formula not a robust F test?
6. Does joint rejection say both coefficients are nonzero?

## Connections

- [Multiple regression](multiple-regression.md)
- [Matrix OLS and projections](matrix-ols-and-projections.md)
- [Hypothesis tests and confidence intervals](../../statistics/hypothesis-testing-and-confidence-intervals.md)

## Sources and review log

- IEBE Week 5 lecture slides, joint-testing sections; example recalculated and extended.
- October 19, 2026: entered Week 5, covered joint-null logic and restricted/unrestricted homoskedastic F intuition. General robust tests still to study. Status `developing`.
