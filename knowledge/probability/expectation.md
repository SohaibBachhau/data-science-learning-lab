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
tags:
  - expectation
  - mean
  - moments
  - probability
---

# Expectation

## Central question

How can we summarize the average value of a random variable while
taking the probabilities of its possible outcomes into account?

## Short answer

The expectation of a random variable is its probability-weighted
average.

It describes the centre of the distribution in an average sense.
It does not necessarily describe an outcome that must occur, or even
an outcome that is possible.

## Intuition

Suppose we could repeat the same random experiment many times.

The average of the observed outcomes would tend to approach the
expected value, provided the relevant conditions for a law of large
numbers are satisfied.

The expectation therefore represents the long-run average associated
with the probability distribution.

It is a property of the random variable and its distribution, not of
one particular realized observation.

## Formal definition

### Discrete random variable

For a discrete random variable $X$,

$$
E[X]
=
\sum_x xP(X=x),
$$

provided that

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
\int_{-\infty}^{\infty} x f_X(x)\,dx,
$$

provided that

$$
E[|X|]
=
\int_{-\infty}^{\infty} |x|f_X(x)\,dx
<
\infty.
$$

The condition $E[|X|] < \infty$ is called a finite first moment.

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
E[aX+b]
=
aE[X]+b.
$$

More generally,

$$
E[aX+bY]
=
aE[X]+bE[Y].
$$

Independence is not required for linearity of expectation.

### Expectation of a constant

For a constant $c$,

$$
E[c]=c.
$$

### Expectation of a function

For a function $g$,

$$
E[g(X)]
=
\sum_x g(x)P(X=x)
$$

in the discrete case, and

$$
E[g(X)]
=
\int_{-\infty}^{\infty} g(x)f_X(x)\,dx
$$

in the continuous case, provided the expectation exists.

## Example: fair die

Let $X$ represent the result of a fair six-sided die.

$$
E[X]
=
\sum_{x=1}^{6}x\frac{1}{6}
=
\frac{1+2+3+4+5+6}{6}
=
3.5.
$$

The value $3.5$ cannot occur in one roll.

This shows that the expected value does not need to be a possible
realization. It describes an average across repeated realizations.

## Example: Bernoulli random variable

Let

$$
X =
\begin{cases}
1 & \text{with probability } p,\\
0 & \text{with probability } 1-p.
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

The expectation of a Bernoulli random variable equals its probability
of success.

## Failure case: Cauchy distribution

Not every random variable has a finite expectation.

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
|x|
\frac{1}{\pi(1+x^2)}
\,dx
=
\infty.
$$

Therefore, the standard Cauchy distribution does not have a finite
expected value.

Its symmetry around zero does not make its expectation equal to zero.

## Connection to econometrics

Expectation is fundamental in regression because the regression
function often models a conditional expectation:

$$
E[Y\mid X].
$$

For the linear model

$$
Y=X\beta+\varepsilon,
$$

the exogeneity condition

$$
E[\varepsilon\mid X]=0
$$

implies

$$
E[Y\mid X]=X\beta.
$$

Expectation also appears in consistency proofs. Laws of large numbers
allow sample averages to converge to population expectations when
their assumptions are satisfied.

## Common mistakes

- Treating the expectation as the most likely outcome.
- Assuming the expected value must be a possible realization.
- Assuming every random variable has an expectation.
- Confusing a sample average with a population expectation.
- Thinking independence is required for linearity of expectation.
- Concluding that symmetry automatically guarantees a finite mean.

## Retrieval questions

1. What is the intuitive meaning of $E[X]$?
2. Why can the expectation be a value that is impossible to observe?
3. What is the difference between $E[X]$ and a sample average?
4. Why do we require $E[|X|] < \infty$?
5. Does linearity of expectation require independence?
6. Why does the Cauchy distribution not have a finite expectation?
7. How is expectation used in the regression model?

## Connections

- [Conditional expectation](conditional-expectation.md)
- [Variance](variance.md)
- [Law of large numbers](law-of-large-numbers.md)
- [Random variables](random-variables.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1 and
  Appendix A.
- Course discussions and personal derivations.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain the concept without notes |
