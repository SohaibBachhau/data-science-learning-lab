---
title: Central Limit Theorem
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - expectation
  - variance
  - iid sampling
  - convergence in distribution
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 slides
tags:
  - central limit theorem
  - asymptotic normality
  - inference
---

# Central Limit Theorem

## Central question

Why do properly standardized sample averages often have approximately normal distributions in large samples?

## Short answer

A central limit theorem states that, under suitable conditions, the scaled difference between a sample average and its population mean converges in distribution to a normal random variable.

## Intuition

The law of large numbers says that an average becomes close to its population mean. The central limit theorem goes further by describing the shape and scale of the remaining sampling error.

The unscaled error $\bar Z_n-\mu$ shrinks toward zero. Multiplying it by $\sqrt{n}$ keeps the fluctuations visible. The theorem says that these rescaled fluctuations approach a normal distribution.

## A basic iid version

Let $Z_1,\ldots,Z_n$ be iid with

$$
E[Z_i]=\mu
$$

and

$$
0<\operatorname{Var}(Z_i)=\sigma^2<\infty.
$$

Then

$$
\sqrt{n}(\bar Z_n-\mu)
\overset{d}{\longrightarrow}
N(0,\sigma^2).
$$

Equivalently,

$$
\frac{\sqrt{n}(\bar Z_n-\mu)}{\sigma}
\overset{d}{\longrightarrow}
N(0,1).
$$

## Convergence in distribution

The notation

$$
W_n\overset{d}{\longrightarrow}W
$$

means that the distribution function of $W_n$ converges to the distribution function of $W$ at continuity points of the limiting distribution.

It does not mean that the realized values of $W_n$ converge numerically to a realized value of $W$.

## Why the square root of the sample size appears

For iid observations,

$$
\operatorname{Var}(\bar Z_n)
=
\frac{\sigma^2}{n}.
$$

Therefore,

$$
\operatorname{SD}(\bar Z_n)
=
\frac{\sigma}{\sqrt{n}}.
$$

The typical size of the sampling error is therefore proportional to $1/\sqrt{n}$. Multiplying by $\sqrt{n}$ produces a quantity with a non-degenerate limiting variance.

## Approximation for a finite sample

For large $n$, the theorem motivates the approximation

$$
\bar Z_n
\approx
N\left(\mu,\frac{\sigma^2}{n}\right).
$$

This is an approximation, not an exact equality in general. It may be poor in small samples, especially for highly skewed or heavy-tailed distributions.

## Use in OLS asymptotic normality

For a simple regression without an intercept,

$$
\hat\beta_n-\beta
=
\frac{\frac{1}{n}\sum_{i=1}^n X_i u_i}
{\frac{1}{n}\sum_{i=1}^n X_i^2}.
$$

Multiply by $\sqrt{n}$:

$$
\sqrt{n}(\hat\beta_n-\beta)
=
\frac{\frac{1}{\sqrt{n}}\sum_{i=1}^n X_i u_i}
{\frac{1}{n}\sum_{i=1}^n X_i^2}.
$$

Under iid sampling, $E[X_i u_i]=0$ and finite variance of $X_i u_i$, the central limit theorem gives

$$
\frac{1}{\sqrt{n}}\sum_{i=1}^n X_i u_i
\overset{d}{\longrightarrow}
N(0,\operatorname{Var}(X_i u_i)).
$$

The law of large numbers gives

$$
\frac{1}{n}\sum_{i=1}^n X_i^2
\overset{p}{\longrightarrow}
E[X_i^2].
$$

Slutsky's theorem then implies

$$
\sqrt{n}(\hat\beta_n-\beta)
\overset{d}{\longrightarrow}
N\left(
0,
\frac{\operatorname{Var}(X_i u_i)}{(E[X_i^2])^2}
\right).
$$

## Assumptions and where they are used

### Zero mean of the summand

The condition

$$
E[X_i u_i]=0
$$

centers the numerator at zero. In regression this follows from an appropriate exogeneity condition.

### Finite variance of the summand

The basic iid CLT requires

$$
\operatorname{Var}(X_i u_i)<\infty.
$$

The course uses finite fourth moments as a convenient sufficient condition. By Cauchy-Schwarz,

$$
E[X_i^2u_i^2]
\leq
\sqrt{E[X_i^4]E[u_i^4]}.
$$

### IID or another suitable dependence structure

IID permits use of the basic theorem. More advanced CLTs allow certain forms of heterogeneity and dependence.

### Nonzero denominator limit

The condition

$$
E[X_i^2]>0
$$

allows division by the probability limit of the denominator.

## Slutsky's theorem

A useful version states that if

$$
A_n\overset{d}{\longrightarrow}A
$$

and

$$
B_n\overset{p}{\longrightarrow}b,
$$

where $b$ is a constant, then

$$
A_nB_n\overset{d}{\longrightarrow}bA
$$

and, when $b\neq 0$,

$$
\frac{A_n}{B_n}\overset{d}{\longrightarrow}\frac{A}{b}.
$$

This combines the CLT result for a numerator with the LLN result for a denominator.

## Continuous mapping theorem

If

$$
W_n\overset{p}{\longrightarrow}w
$$

and $g$ is continuous at $w$, then

$$
g(W_n)\overset{p}{\longrightarrow}g(w).
$$

For example, if a variance estimator converges to a positive variance, taking its square root preserves convergence.

## Example: sample proportion

For iid Bernoulli variables with success probability $p$,

$$
\sqrt{n}(\bar Z_n-p)
\overset{d}{\longrightarrow}
N(0,p(1-p)).
$$

Thus, for large $n$,

$$
\bar Z_n
\approx
N\left(p,\frac{p(1-p)}{n}\right).
$$

## Failure cases

The basic theorem cannot be applied when the variance is infinite. It can also fail under strong dependence or when a small number of observations dominate the sum.

The standard Cauchy distribution is an important example. Its sample average remains Cauchy, so it does not approach a normal distribution under the usual scaling.

## Common mistakes

- Saying the raw sample average converges to a normal distribution rather than to the constant $\mu$.
- Forgetting the $\sqrt{n}$ scaling.
- Treating the limiting normal distribution as exact in every finite sample.
- Applying the basic iid CLT when the variance is infinite.
- Confusing convergence in distribution with convergence in probability.
- Using the CLT for the OLS numerator but forgetting the LLN and Slutsky steps for the denominator.

## Retrieval questions

1. State a basic iid central limit theorem.
2. Why is the sample average multiplied by $\sqrt{n}$?
3. What is the difference between the LLN and the CLT?
4. What role does finite variance play?
5. How are the CLT, LLN and Slutsky's theorem combined in OLS?
6. Why do finite fourth moments help establish a finite variance for $Xu$?
7. Why is asymptotic normality useful for inference?

## Connections

- [Law of large numbers](law-of-large-numbers.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Asymptotic normality](../statistics/asymptotic-normality.md)
- [Sampling distribution of OLS](../econometrics/linear-regression/sampling-distribution-of-ols.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, section on least-squares normality.
- *Introductory Econometrics for Business and Economics*, Week 2 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain the roles of the CLT, LLN and Slutsky in one proof |
