---
title: Omitted-Variable Bias
status: developing
updated: 2026-10-31
sources:
  - IEBE Week 4 lecture slides
  - October 19 study session
tags: [regression, exogeneity, omitted-variable-bias]
---

# Omitted-Variable Bias

## Central question

When does excluding an important variable distort the estimated effect of a regressor, and in which direction?

## Short answer and intuition

Suppose we want to measure how class size affects test scores. Schools differ in many other ways, such as language background and resources. Excluding a factor is not automatically a problem, because all models omit something. **Omitted-variable bias (OVB)** arises when the excluded factor both affects the outcome and is associated with an included regressor. OLS then partly attributes the excluded factor's relationship with the outcome to the included regressor.

This is primarily an **exogeneity problem**. A larger sample generally does not remove it.

## Derivation and notation

Let the population model be

$$
Y_i=\beta_0+\beta_1X_i+\beta_2Z_i+u_i,
$$

where $Y$ is the outcome, $X$ the included regressor of interest, $Z$ the omitted explanatory factor, and $u$ the remaining error. Assume the true equation has $E[u_i\mid X_i,Z_i]=0$ and finite relevant moments, with $\operatorname{Var}(X_i)>0$.

If we regress $Y$ only on an intercept and $X$, the population slope of this shorter regression is

$$
\alpha_1=\frac{\operatorname{Cov}(X,Y)}{\operatorname{Var}(X)}.
$$

Substituting the population model and applying covariance linearity gives

$$
\alpha_1
=\beta_1+\beta_2\frac{\operatorname{Cov}(X,Z)}{\operatorname{Var}(X)}
+\frac{\operatorname{Cov}(X,u)}{\operatorname{Var}(X)}.
$$

Under the stated exogeneity assumption, $\operatorname{Cov}(X,u)=0$. Therefore,

$$
\boxed{\alpha_1-\beta_1
=\beta_2\frac{\operatorname{Cov}(X,Z)}{\operatorname{Var}(X)}.}
$$

With random sampling and suitable regularity conditions, the simple-regression OLS slope converges in probability to $\alpha_1$. This expression is the **asymptotic omitted-variable bias relative to $\beta_1$**. It is not, without additional assumptions, an exact finite-sample expectation formula.

## Two conditions and the sign rule

For nonzero bias in this simple setup, both must hold:

1. $\beta_2\neq 0$: $Z$ contributes to $Y$ after accounting for $X$.
2. $\operatorname{Cov}(X,Z)\neq 0$: $Z$ is associated with $X$.

Because $\operatorname{Var}(X)>0$, the sign is the product of the signs of $\beta_2$ and $\operatorname{Cov}(X,Z)$.

| Effect of $Z$ on $Y$ | Association of $X$ with $Z$ | Bias in omitted-$Z$ slope |
|---|---|---|
| Positive | Positive | Positive |
| Positive | Negative | Negative |
| Negative | Positive | Negative |
| Negative | Negative | Positive |

A negative bias means the short-regression estimate tends to be **below** the true partial coefficient, not necessarily that both coefficients are negative.

### Our worked sign exercise

We considered $\beta_2<0$, $\operatorname{Cov}(X,Z)>0$, and $\operatorname{Var}(X)>0$. Then

$$
\beta_2\frac{\operatorname{Cov}(X,Z)}{\operatorname{Var}(X)}<0.
$$

So the estimated $X$ coefficient is pushed downward relative to $\beta_1$. The important step was separating the **sign of the bias** from the **sign of the estimated coefficient**.

### California class-size illustration

In the course example, student-teacher ratio (STR) predicts test scores. The simple slope is approximately $-2.28$. After controlling for percentage of English learners (PctEL), it is approximately $-1.10$. A higher PctEL predicts lower scores, while STR and PctEL tend to be positively associated. This is consistent with **downward bias** in the simple STR slope.

The comparison illustrates the mechanism; it does not by itself prove that the adjusted coefficient is causal or that all relevant confounding has been removed.

## A failure case

If a missing variable affects the outcome but is unrelated to $X$, omitting it can increase unexplained variation without producing this particular slope bias. Conversely, a variable correlated with $X$ but irrelevant to $Y$ after conditioning also need not bias the slope.

Including every conceivable variable is not automatically correct. A bad control, a mediator or a collider can introduce its own identification problems.

## Common mistakes

- “Every omitted variable creates bias.” Both conditions matter.
- “A big sample solves OVB.” A biased probability limit remains biased.
- “Adding any control makes the coefficient causal.” Controls need a defensible identifying role.
- “Negative bias means negative coefficient.” Bias is a difference from the target coefficient.
- Confusing the conditional error mean assumption with the exact sample identity that OLS residuals are orthogonal to regressors.

## Retrieval questions

1. Explain the two OVB conditions without a formula.
2. Derive the population simple-regression slope after omitting $Z$.
3. If $\beta_2<0$ and $\operatorname{Cov}(X,Z)<0$, is bias positive or negative?
4. Why does increasing $n$ not automatically remove OVB?
5. How is this related to $E[u\mid X]=0$?

## Connections

- [Exogeneity](exogeneity.md)
- [Correct specification](correct-specification.md)
- [Multiple regression](multiple-regression.md)
- [Linear regression story](story.md)

## Sources and review log

- IEBE Week 4 lecture slides, omitted-variable-bias section. Paraphrased and extended with derivation.
- October 19, 2026: sign exercise completed; marked `developing` for future causal-identification review.
