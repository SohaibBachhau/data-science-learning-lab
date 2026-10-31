---
title: Week 5 - Joint Testing (Started)
course: Introductory Econometrics for Business and Economics
status: developing
created: 2026-10-31
updated: 2026-10-31
sources:
  - IEBE Week 5 slides
  - October 19 study session
tags: [joint-hypothesis, restricted-regression, F-test]
---

# Week 5: Joint Testing (Started)

## Progress boundary

After finishing the Week 4 multiple-regression session on October 19, we started Week 5. We covered the **reason for joint testing**, a joint null versus its alternative, restricted/unrestricted regressions, and the homoskedastic $R^2$-based F-statistic. This is a **partial Week 5 note**, not a claim to have completed every method listed in the slides.

The reusable explanation is in [Joint hypothesis tests](../../../knowledge/econometrics/linear-regression/joint-hypothesis-tests.md).

## Why one t-test per coefficient is insufficient

Suppose the null is $H_0:\beta_1=0$ **and** $\beta_2=0$. The alternative says $\beta_1\neq0$ **or** $\beta_2\neq0$ (possibly both). If we reject whenever either of two independent 5% tests rejects, the total false-rejection probability is

$$
1-0.95^2=0.0975,
$$

not 0.05. Independence here is a teaching simplification; the actual coefficient estimates may be correlated.

## Restricted and unrestricted models

The unrestricted regression estimates both $\beta_1$ and $\beta_2$ freely. The restricted regression imposes both zero restrictions. Because the unrestricted model can choose more coefficients, it cannot fit the same sample worse in terms of in-sample OLS RSS.

The course's **homoskedasticity-only** statistic is

$$
F=
\frac{(R_U^2-R_R^2)/q}
{(1-R_U^2)/(n-k_U-1)}.
$$

Here $q$ is the number of restrictions, $k_U$ is the number of unrestricted regressors **without** the intercept, $n$ is the common sample size and $R_U^2,R_R^2$ are the two models' $R^2$ values.

In the class-size / expenditure example, $R_U^2=0.4366$, $R_R^2=0.4149$, $n=420$, $k_U=3$, $q=2$:

$$
F=\frac{(0.4366-0.4149)/2}{(1-0.4366)/416}\approx8.01.
$$

We reject the joint zero restrictions at the conventional 5% level using the appropriate F reference distribution. This does not tell us that *both* slopes are nonzero or that either is causal.

## Not yet recorded as completed

The slides go on to formal general restrictions $R\beta=r$, heteroskedasticity-robust Wald/F or chi-squared procedures, restricted estimation by Lagrange multipliers, likelihood-ratio and LM tests, and specification/control-variable analysis. These need their own study and practice before being marked learned. Week 6 nonlinear regression is also **not** marked complete.

## Next retrieval practice

1. Explain how two separate tests can have a familywise error rate above 5%.
2. State a joint null and its logically correct alternative.
3. Identify $q$, $n$, $k_U$, $R_U^2$ and $R_R^2$ from a regression output.
4. Compute the F-statistic without looking at the formula.
5. Explain why this F-statistic must not be advertised as heteroskedasticity-robust.

## Sources and review

- IEBE Week 5 slides, joint-testing portion; formulas and numerical example checked.
- October 19, 2026: introductory joint-testing coverage; status `developing`.
