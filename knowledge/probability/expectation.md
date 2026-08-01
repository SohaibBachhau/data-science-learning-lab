---
title: Expectation
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - random variables
  - probability distributions
sources:
  - Blasques, Advanced Econometric Methods
  - course discussions and personal derivations
tags:
  - expectation
  - mean
  - moments
  - probability
---

# Expectation

## Central question

How can we summarize the average value of a random variable while taking the probabilities of its possible outcomes into account?

## Short answer

The expectation of a random variable is its probability-weighted average. It describes the center of the distribution in an average sense. It does not have to be the most likely value, a value that must occur or even a possible realization.

## Intuition

Suppose we could repeat the same random experiment many times. Under suitable conditions, the average of the observed outcomes would approach the expected value.

Expectation is therefore a population property of a random variable and its distribution. It is not the same as the sample average calculated from one finite dataset.

## Formal definition

### Discrete random variable

For a discrete random variable $X$,

$$
E[X]
=
\sum_x xP(X=x),
$$

provided

$$
E[|X|]
=
\sum_x |x|P(X=x)
<
\infty.
$$

### Continuous random variable

For a continuous random variable $X$ with density $f_X(x)$,

$$
E[X]
=
\int_{-\infty}^{\infty}xf_X(x)\,dx,
$$

provided

$$
E[|X|]
=
\int_{-\infty}^{\infty}|x|f_X(x)\,dx
<
\infty.
$$

The condition

$$
E[|X|]<\infty
$$

is called a finite first absolute moment.

## Notation

- $X$: a random variable
- $x$: a possible realization of $X$
- $P(X=x)$: probability mass at $x$
- $f_X(x)$: probability density of $X$
- $E[X]$: expectation of $X$

## Main properties

### Linearity

For constants $a$ and $b$,

$$
E[aX+b]=aE[X]+b.
$$

More generally,

$$
E[aX+bY]=aE[X]+bE[Y].
$$

Independence is not required for linearity of expectation.

### Expectation of a constant

For a constant $c$,

$$
E[c]=c.
$$

### Expectation of a function

For a suitable function $g$, the discrete formula is

$$
E[g(X)]
=
\sum_x g(x)P(X=x),
$$

and the continuous formula is

$$
E[g(X)]
=
\int_{-\infty}^{\infty}g(x)f_X(x)\,dx,
$$

provided the expectation exists.

### Nonnegative random variables

If

$$
Z\geq 0
$$

almost surely and

$$
E[Z]=0,
$$

then

$$
Z=0
$$

almost surely.

This property explains why

$$
E[X^2]=0
$$

can hold only when

$$
X=0
$$

almost surely.

## Example: fair die

Let $X$ be the result of a fair six-sided die. Then

$$
E[X]
=
\sum_{x=1}^{6}x\frac{1}{6}
=
\frac{1+2+3+4+5+6}{6}
=
3.5.
$$

The value $3.5$ cannot occur in one roll. It describes an average across repeated realizations.

## Example: Bernoulli random variable

Let

$$
X=
\begin{cases}
1 & \text{with probability }p,\\
0 & \text{with probability }1-p.
\end{cases}
$$

Then

$$
E[X]
=
1\cdot p+0\cdot(1-p)
=
p.
$$

The expectation equals the probability of success.

## Failure case: Cauchy distribution

For a standard Cauchy random variable,

$$
f_X(x)
=
\frac{1}{\pi(1+x^2)}.
$$

Its tails are sufficiently heavy that

$$
E[|X|]
=
\int_{-\infty}^{\infty}
|x|\frac{1}{\pi(1+x^2)}\,dx
=
\infty.
$$

Therefore, the standard Cauchy distribution has no finite expected value. Its symmetry around zero does not make its expectation equal to zero because the positive and negative parts do not converge absolutely.

## Connection to econometrics

Regression often models a conditional expectation:

$$
E[Y\mid X].
$$

For the linear model

$$
Y=X'\beta+u,
$$

the exogeneity condition

$$
E[u\mid X]=0
$$

implies

$$
E[Y\mid X]=X'\beta.
$$

Expectation also appears in consistency arguments. Laws of large numbers allow sample averages to converge to population expectations when their assumptions are satisfied.

## Common mistakes

- Treating expectation as the most likely outcome.
- Assuming the expected value must be a possible realization.
- Assuming every random variable has a finite expectation.
- Confusing a sample average with a population expectation.
- Thinking independence is required for linearity of expectation.
- Concluding that symmetry automatically guarantees a finite mean.
- Using $E[X]$ without checking the required moment condition.

## Retrieval questions

1. What is the intuitive meaning of $E[X]$?
2. Why can an expectation be impossible to observe as one realization?
3. What is the difference between $E[X]$ and a sample average?
4. Why do we require $E[|X|]<\infty$ in the standard definition?
5. Does linearity of expectation require independence?
6. Why does the Cauchy distribution not have a finite expectation?
7. When can $E[X^2]=0$?
8. How is expectation used in the regression model?

## Connections

- [Random variables and probability distributions](random-variables-and-distributions.md)
- [Conditional expectation](conditional-expectation.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Law of large numbers](law-of-large-numbers.md)
- [Central limit theorem](central-limit-theorem.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1 and Appendix A.
- Course discussions and personal derivations.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created and connected | Explain the concept without notes |
