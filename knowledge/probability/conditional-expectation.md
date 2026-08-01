---
title: Conditional Expectation
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - expectation
  - joint distributions
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 2 and Week 3 slides
tags:
  - conditional expectation
  - regression function
  - law of iterated expectations
---

# Conditional Expectation

## Central question

How does the expected value of one random variable change when information about another variable is known?

## Short answer

The conditional expectation $E[Y\mid X]$ is the mean of $Y$ after using the information contained in $X$. It is itself a random variable because its value depends on the random value of $X$.

## Intuition

The unconditional expectation $E[Y]$ averages over the entire population. The conditional expectation $E[Y\mid X=x]$ averages only over the part of the population for which $X=x$.

Suppose $Y$ is income and $X$ is years of education. Then $E[Y]$ is average income in the whole population, while $E[Y\mid X=16]$ is average income among people with 16 years of education.

## Formal definition

For discrete random variables,

$$
E[Y\mid X=x]
=
\sum_y yP(Y=y\mid X=x),
$$

provided the conditional expectation exists.

For continuous random variables,

$$
E[Y\mid X=x]
=
\int_{-\infty}^{\infty}y f_{Y\mid X}(y\mid x)\,dy.
$$

As a function of $x$, define

$$
m(x)=E[Y\mid X=x].
$$

Substituting the random variable $X$ into this function gives

$$
E[Y\mid X]=m(X).
$$

Thus, $E[Y\mid X]$ is a random variable, while $E[Y\mid X=x]$ is a number for a fixed value $x$.

## Main properties

### Known functions of the conditioning variable can be taken outside

For a suitable function $g$,

$$
E[g(X)Y\mid X]=g(X)E[Y\mid X].
$$

Once we condition on $X$, the value $g(X)$ is known.

### Linearity

For constants $a$ and $b$,

$$
E[aY+bZ\mid X]
=
aE[Y\mid X]+bE[Z\mid X].
$$

### Conditioning a known quantity

$$
E[g(X)\mid X]=g(X).
$$

### Independence

If $Y$ is independent of $X$ and the expectation exists, then

$$
E[Y\mid X]=E[Y].
$$

The reverse is not generally true. Mean independence is weaker than full independence.

## Law of iterated expectations

The law of iterated expectations states that

$$
E[E[Y\mid X]]=E[Y].
$$

Intuitively, first averaging $Y$ within each group defined by $X$ and then averaging those group means using the distribution of $X$ returns the overall mean.

A more general nested version is

$$
E[E[Y\mid X,Z]\mid X]=E[Y\mid X].
$$

## Derivation of the discrete law of iterated expectations

Starting from the definition,

$$
E[E[Y\mid X]]
=
\sum_x E[Y\mid X=x]P(X=x).
$$

Substitute the conditional expectation:

$$
E[E[Y\mid X]]
=
\sum_x\sum_y yP(Y=y\mid X=x)P(X=x).
$$

Using

$$
P(Y=y\mid X=x)P(X=x)=P(X=x,Y=y),
$$

we obtain

$$
E[E[Y\mid X]]
=
\sum_y y\sum_x P(X=x,Y=y)
=
\sum_y yP(Y=y)
=
E[Y].
$$

## Conditional expectation in regression

The population regression function is often defined as

$$
m(x)=E[Y\mid X=x].
$$

A linear conditional mean model states that

$$
E[Y\mid X=x]=\beta_0+\beta_1x.
$$

The associated error is

$$
u=Y-E[Y\mid X].
$$

By construction,

$$
E[u\mid X]=0.
$$

This zero conditional mean property follows because

$$
E[u\mid X]
=
E[Y-E[Y\mid X]\mid X]
=
E[Y\mid X]-E[Y\mid X]
=
0.
$$

## Conditional versus unconditional zero mean

The condition

$$
E[u\mid X]=0
$$

implies

$$
E[u]=0
$$

by the law of iterated expectations.

However,

$$
E[u]=0
$$

does not imply

$$
E[u\mid X]=0.
$$

Positive average errors for some values of $X$ can cancel negative average errors for other values of $X$.

## Connection to covariance

If $E[u\mid X]=0$ and the required moments exist, then

$$
E[Xu]
=
E[E[Xu\mid X]]
=
E[XE[u\mid X]]
=
0.
$$

If $E[u]=0$, this implies

$$
\operatorname{Cov}(X,u)=0.
$$

The reverse implication is not generally valid. Zero covariance rules out only a linear average relationship, while zero conditional mean rules out any systematic change in the mean of $u$ with $X$.

## Example

Suppose

$$
Y=2+3X+u
$$

and

$$
E[u\mid X]=0.
$$

Then

$$
E[Y\mid X]
=
E[2+3X+u\mid X]
=
2+3X+E[u\mid X]
=
2+3X.
$$

The coefficient $3$ is the change in the conditional mean of $Y$ associated with a one-unit increase in $X$.

## Failure case

Suppose instead that

$$
E[u\mid X]=X^2.
$$

Then

$$
E[Y\mid X]
=
\beta_0+\beta_1X+X^2.
$$

The linear expression $\beta_0+\beta_1X$ is not the true conditional mean. Including an error term in the equation does not automatically make the conditional mean specification correct.

## Common mistakes

- Treating $E[Y\mid X]$ as a fixed number rather than a random variable.
- Confusing $E[Y\mid X]$ with $E[Y\mid X=x]$.
- Assuming $E[u]=0$ is equivalent to $E[u\mid X]=0$.
- Thinking mean independence is the same as full statistical independence.
- Forgetting that the law of iterated expectations averages conditional means using the distribution of the conditioning variable.

## Retrieval questions

1. What is the difference between $E[Y]$, $E[Y\mid X]$ and $E[Y\mid X=x]$?
2. Why is $E[Y\mid X]$ a random variable?
3. State the law of iterated expectations.
4. Why does $E[u\mid X]=0$ imply $E[u]=0$?
5. Why does $E[u]=0$ not imply $E[u\mid X]=0$?
6. How does conditional expectation define the population regression function?
7. Why can $X$ be taken outside $E[Xu\mid X]$?

## Connections

- [Expectation](expectation.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Linear regression model](../econometrics/linear-regression/linear-regression-model.md)
- [Exogeneity](../econometrics/linear-regression/exogeneity.md)
- [Correct specification](../econometrics/linear-regression/correct-specification.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1.
- *Introductory Econometrics for Business and Economics*, Week 2 and Week 3 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Derive the law of iterated expectations without looking |
