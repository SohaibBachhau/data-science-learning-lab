---
title: Multicollinearity and Dummy Variables
status: developing
updated: 2026-10-31
sources:
  - IEBE Week 4 lecture slides
  - October 19 study session
tags: [full-rank, multicollinearity, dummy-variables]
---

# Multicollinearity and Dummy Variables

## Central question

Why do some combinations of regressors make OLS impossible to compute, while others merely make estimates imprecise?

## The intuition

Multiple regression tries to measure the effect of one regressor while holding the others fixed. If a regressor is **exactly determined** by other columns, there is no independent direction of variation from which its coefficient can be identified. If it is merely **almost determined** by them, that independent direction exists but may be tiny, producing noisy estimates.

## Perfect versus imperfect multicollinearity

Suppose $X$ is the $n\times p$ regression matrix, including an intercept when needed.

**Perfect multicollinearity** means its columns are linearly dependent: for some nonzero vector $a$, $Xa=0$. Then $X$ lacks full column rank, $X'X$ is singular, and the usual unique OLS formula $(X'X)^{-1}X'Y$ cannot be used. Examples include accidentally inserting the same regressor twice or including all mutually exhaustive category indicators with an intercept.

**Imperfect multicollinearity** means regressors are strongly, but not perfectly, correlated. As long as $X$ retains full column rank, unique OLS coefficients are calculable. However, it may be difficult to separate their partial associations and their standard errors may become large.

Under homoskedastic, conditionally uncorrelated errors,

$$
\operatorname{Var}(\hat\beta\mid X)=\sigma_u^2(X'X)^{-1}.
$$

Near-collinearity affects the inverse and hence precision. It does not **by itself** create the same bias as omitted variables, and does not automatically violate conditional exogeneity.

### Our practice distinction

We reasoned that imperfect multicollinearity does **not** make the inverse impossible, because the variables are not exact linear combinations. It leaves only limited independent movement, which can increase coefficient standard errors. By contrast, perfect multicollinearity destroys full rank.

## A binary (dummy) regressor

A dummy variable $D_i$ equals either zero or one. In the simple conditional-mean model

$$
E[Y_i\mid D_i]=\beta_0+\beta_1D_i,
$$

we have

$$
E[Y\mid D=0]=\beta_0,\qquad
E[Y\mid D=1]=\beta_0+\beta_1.
$$

Therefore,

$$
\beta_1=E[Y\mid D=1]-E[Y\mid D=0].
$$

For an additional covariate $X$, the interpretation of a coefficient on $D$ in an additive linear conditional mean is the predicted group difference **at the same $X$**. That interpretation need not be causal.

## The dummy-variable trap

Suppose every observation is either in group A or group B. Write $D_A=1$ for A and $D_B=1$ for B. For all observations,

$$
1=D_A+D_B.
$$

If the regression includes an intercept, $D_A$ and $D_B$, its columns are linearly dependent. OLS cannot uniquely estimate all three coefficients.

Two standard fixes:

1. **Keep the intercept and omit one dummy**. If B is omitted, the intercept represents the B baseline and the coefficient on $D_A$ is A minus B.
2. **Omit the intercept and keep both dummies**. Each coefficient gives its corresponding group mean in the no-other-regressor example.

With more than two mutually exclusive, exhaustive categories, keep one fewer dummy than the number of categories when using an intercept.

### Our practice correction

We identified that including both category indicators plus the constant causes perfect multicollinearity **because the two indicators sum exactly to the constant column**. The issue is not simply that dummy variables are correlated.

## A counterexample

Two binary variables do not automatically cause the dummy trap. If they represent separate, possibly overlapping characteristics, such as “works part-time” and “has a driver's licence,” the columns may be linearly independent. The problem depends on exact column relations in the actual design matrix.

## Common mistakes

- “High correlation means OLS is impossible.” Only exact linear dependence makes the ordinary inverse singular.
- “Multicollinearity automatically biases OLS.” Not if exogeneity otherwise holds.
- “All dummy regressors have to be dropped.” Usually omit a single baseline category, not all category indicators.
- “A dummy coefficient is a derivative.” It is a discrete zero-to-one comparison.
- “Including one control always removes OVB.” The remaining conditional error assumption must be credible.

## Retrieval questions

1. Define full column rank in terms of a nonzero vector $a$.
2. Why does $D_A+D_B=1$ cause a problem when the intercept is included?
3. Explain the two standard dummy-trap fixes and how coefficient interpretation changes.
4. Can an OLS model be unbiased but have imprecise coefficients due to correlated regressors?
5. When is a dummy coefficient a difference in conditional means?

## Connections

- [Matrix OLS and projections](matrix-ols-and-projections.md)
- [Multiple regression](multiple-regression.md)
- [Omitted-variable bias](omitted-variable-bias.md)

## Sources and review log

- IEBE Week 4 lecture slides, multicollinearity and binary-regressor sections; paraphrased and extended.
- October 19, 2026: full-rank and dummy-trap practice completed. Status `developing`.
