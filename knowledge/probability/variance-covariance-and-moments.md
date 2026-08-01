---
title: Variance, Covariance and Moments
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - expectation
  - random variables
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - variance
  - covariance
  - moments
  - finite moments
---

# Variance, Covariance and Moments

## Central question

How can we measure the spread of one random variable, the linear co-movement of two random variables and the existence of the population quantities used in statistical arguments?

## Short answer

Variance measures expected squared distance from the mean. Covariance measures whether two variables tend to be above or below their means together. Moments are expectations of powers or other functions of random variables, and finite-moment assumptions ensure that these quantities are mathematically well defined and usable in asymptotic results.

## Variance

For a random variable $X$ with finite second moment, the variance is

$$
\operatorname{Var}(X)
=
E[(X-E[X])^2].
$$

An equivalent formula is

$$
\operatorname{Var}(X)
=
E[X^2]-(E[X])^2.
$$

Variance is always nonnegative because a square cannot be negative.

The standard deviation is

$$
\operatorname{SD}(X)=\sqrt{\operatorname{Var}(X)}.
$$

It is measured in the same units as $X$.

## Why square the deviations?

If deviations from the mean were averaged directly, positive and negative deviations would cancel:

$$
E[X-E[X]]=0.
$$

Squaring makes every deviation nonnegative and gives greater weight to large deviations.

## When is the variance zero?

Because $(X-E[X])^2\geq 0$, we have

$$
\operatorname{Var}(X)=0
$$

if and only if

$$
X=E[X]
$$

with probability one. Thus, a random variable has zero variance exactly when it is constant almost surely.

Similarly, because $X^2\geq 0$,

$$
E[X^2]=0
$$

if and only if

$$
X=0
$$

with probability one.

A nonnegative random variable can have expectation zero only when it is zero almost surely.

## Variance under transformations

For constants $a$ and $b$,

$$
\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X).
$$

Adding a constant shifts every value equally and therefore does not change spread. Multiplication by $a$ scales deviations by $a$, so squared deviations scale by $a^2$.

## Covariance

For random variables $X$ and $Y$ with finite second moments,

$$
\operatorname{Cov}(X,Y)
=
E[(X-E[X])(Y-E[Y])].
$$

An equivalent formula is

$$
\operatorname{Cov}(X,Y)
=
E[XY]-E[X]E[Y].
$$

Interpretation:

- positive covariance means that large values of $X$ tend to occur with large values of $Y$;
- negative covariance means that large values of $X$ tend to occur with small values of $Y$;
- zero covariance means no linear population co-movement, but nonlinear dependence may remain.

## Correlation

When both variances are positive and finite, correlation is

$$
\operatorname{Corr}(X,Y)
=
\frac{\operatorname{Cov}(X,Y)}
{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}}.
$$

Correlation is unit-free and lies between $-1$ and $1$.

## Main covariance properties

$$
\operatorname{Cov}(X,Y)=\operatorname{Cov}(Y,X),
$$

$$
\operatorname{Cov}(X,X)=\operatorname{Var}(X),
$$

and for constants $a,b,c,d$,

$$
\operatorname{Cov}(aX+b,cY+d)=ac\operatorname{Cov}(X,Y).
$$

The variance of a sum is

$$
\operatorname{Var}(X+Y)
=
\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y).
$$

If $X$ and $Y$ are independent and have finite second moments, then their covariance is zero.

## Moments

A raw moment of order $k$ is

$$
E[X^k],
$$

when it exists.

An absolute moment of order $k$ is

$$
E[|X|^k].
$$

Important examples are:

- first absolute moment: $E[|X|]$;
- second moment: $E[X^2]$;
- fourth moment: $E[X^4]$.

A statement such as "the fourth moment is finite" means

$$
E[|X|^4]<\infty.
$$

For real $X$, $|X|^4=X^4$.

## Why finite moments matter

Different results require different moments.

### Existence of the mean

A standard sufficient condition for a well-defined finite expectation is

$$
E[|X|]<\infty.
$$

This is called a finite first absolute moment.

### Existence of variance

A finite variance requires

$$
E[X^2]<\infty.
$$

A finite second moment also implies a finite first moment.

### Central limit theorem

A basic iid central limit theorem requires finite variance.

### Introductory OLS inference

The IEBE least-squares assumptions require finite fourth moments of $X$ and $Y$. This stronger condition helps establish that quantities such as $X_i u_i$ have finite variance, which is needed in the asymptotic normality argument.

Using the Cauchy-Schwarz inequality,

$$
E[X^2u^2]
\leq
\sqrt{E[X^4]E[u^4]}.
$$

Thus, finite fourth moments of $X$ and $u$ imply a finite second moment for $Xu$.

## Bounded versus finite moments

In some econometrics texts, "bounded moments" is used informally to mean that the relevant moments are finite. In a sequence setting, it can also mean a uniform bound such as

$$
\sup_t E[|X_t|^k]<\infty.
$$

The exact meaning should be checked from the assumptions being used.

## Failure case: Cauchy distribution

The standard Cauchy density is

$$
f_X(x)=\frac{1}{\pi(1+x^2)}.
$$

Its tails decline too slowly for the first absolute moment to be finite:

$$
E[|X|]=\infty.
$$

Therefore, its expectation is not defined as a finite population mean. Symmetry around zero does not solve this problem because the positive and negative tail integrals do not converge absolutely.

The sample mean of iid Cauchy observations also has a Cauchy distribution, so averaging does not make it concentrate around zero.

## Example: Bernoulli variable

If $X$ is Bernoulli with success probability $p$, then

$$
E[X]=p
$$

and, because $X^2=X$,

$$
\operatorname{Var}(X)
=
E[X^2]-(E[X])^2
=
p-p^2
=
p(1-p).
$$

## Connection to regression

For the regression error $u$, the conditional zero mean assumption

$$
E[u\mid X]=0
$$

implies, when moments exist,

$$
\operatorname{Cov}(X,u)=0.
$$

The conditional variance

$$
\operatorname{Var}(u\mid X)
$$

describes how the spread of the error changes with the regressors. Homoskedasticity means this conditional variance is constant. Heteroskedasticity means it varies with $X$.

## Common mistakes

- Saying variance can be negative.
- Confusing $E[X^2]$ with $(E[X])^2$.
- Thinking $E[X^2]=0$ can occur for a genuinely varying random variable.
- Treating zero covariance as independence.
- Assuming symmetry guarantees a finite expectation.
- Using an expectation, variance or covariance without checking that the required moments exist.
- Assuming finite fourth moments are always necessary rather than one convenient sufficient condition used in the course.

## Retrieval questions

1. Why is variance always nonnegative?
2. When does $E[X^2]=0$?
3. Derive $\operatorname{Var}(X)=E[X^2]-(E[X])^2$.
4. What does covariance measure, and what does zero covariance fail to rule out?
5. What is a finite first moment?
6. Why do finite fourth moments help in the OLS central limit theorem?
7. Why does the standard Cauchy distribution not have a finite mean?

## Connections

- [Expectation](expectation.md)
- [Conditional expectation](conditional-expectation.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Law of large numbers](law-of-large-numbers.md)
- [Central limit theorem](central-limit-theorem.md)
- [Exogeneity](../econometrics/linear-regression/exogeneity.md)
- [Sampling distribution of OLS](../econometrics/linear-regression/sampling-distribution-of-ols.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1 and Appendix A.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain why $E[X^2]=0$ implies $X=0$ almost surely |
