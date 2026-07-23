---
title: Random Variables and Probability Distributions
subject: probability
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - sample spaces
  - events
  - probability
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 and Week 2 slides
tags:
  - random variables
  - distributions
  - probability
---

# Random Variables and Probability Distributions

## Central question

How do we represent uncertain numerical outcomes and describe how likely their possible values are?

## Short answer

A random variable assigns a numerical value to each possible outcome of a random experiment. Its probability distribution describes how probability is allocated across those possible values.

## Intuition

The randomness is not in the mathematical rule itself. Once an outcome occurs, the rule assigns a definite number to it. The uncertainty comes from not knowing in advance which outcome will occur.

For example, when a die is rolled, the sample outcome may be one of six faces. The random variable $X$ can record the number shown. Before the roll, $X$ is uncertain. After the roll, we observe one realization, such as $x=4$.

## Formal definition

Let $\Omega$ be a sample space. A random variable is a measurable function

$$
X:\Omega\rightarrow\mathbb{R}.
$$

For introductory work, it is enough to understand that $X$ assigns a real number to every possible outcome in $\Omega$.

The distribution function of $X$ is

$$
F_X(x)=P(X\leq x).
$$

It gives the probability that the random variable takes a value no greater than $x$.

## Discrete random variables

A discrete random variable takes values in a finite or countable set. Its probability mass function is

$$
p_X(x)=P(X=x).
$$

It satisfies

$$
p_X(x)\geq 0
$$

and

$$
\sum_x p_X(x)=1.
$$

### Example: Bernoulli variable

Let $X=1$ when an event occurs and $X=0$ otherwise. Then

$$
P(X=1)=p,
$$

$$
P(X=0)=1-p.
$$

## Continuous random variables

A continuous random variable is described by a probability density function $f_X(x)$ such that

$$
f_X(x)\geq 0
$$

and

$$
\int_{-\infty}^{\infty}f_X(x)\,dx=1.
$$

Probabilities are obtained from areas under the density:

$$
P(a\leq X\leq b)=\int_a^b f_X(x)\,dx.
$$

For a continuous random variable,

$$
P(X=x)=0
$$

for every single value $x$. This does not mean that the value cannot occur. It means that a single point has zero area under a continuous density.

## Random variable, realization and observation

These terms must be separated carefully:

- $X$ is a random variable before its value is observed.
- $x$ is a possible or realized value of $X$.
- $X_i$ is the random variable associated with observation $i$ before sampling.
- $x_i$ is the numerical value actually observed in the sample.

A dataset contains realizations, but probability statements are made about the random variables that could have generated them.

## Joint distributions

When several random variables are studied together, their joint distribution describes their combined behavior. For two variables, the joint distribution determines probabilities such as

$$
P(X\leq x,Y\leq y).
$$

The marginal distribution of $X$ can be recovered from the joint distribution by summing or integrating over all possible values of $Y$.

## Conditional distributions

The conditional distribution of $Y$ given $X=x$ describes the distribution of $Y$ among cases for which $X=x$.

In econometrics, the conditional distribution of $Y$ given $X$ is important because regression models describe features of that conditional distribution, especially its mean.

## Example: outcome and regressor

Suppose $Y$ is a student's test score and $X$ is the student-teacher ratio in the student's district. Different districts generate different pairs $(X,Y)$.

The joint distribution describes how student-teacher ratios and test scores vary together in the population. The conditional distribution of $Y$ given $X=x$ describes test scores among districts with student-teacher ratio $x$.

## Common mistakes

- Treating a random variable and its observed realization as the same object.
- Thinking a density value is itself a probability.
- Thinking $P(X=x)=0$ means a continuous value is impossible.
- Speaking about the distribution of one variable when the argument actually depends on the joint distribution of several variables.
- Assuming a model specifies the entire distribution when it may specify only a conditional mean.

## Retrieval questions

1. What is random about a random variable?
2. What is the difference between $X$ and $x$?
3. What information does $F_X(x)$ provide?
4. Why is $P(X=x)=0$ for a continuous random variable?
5. What is the difference between a marginal and conditional distribution?
6. Why does regression depend on the joint distribution of $X$ and $Y$?

## Connections

- [Expectation](expectation.md)
- [Conditional expectation](conditional-expectation.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1 and Appendix A.
- *Introductory Econometrics for Business and Economics*, Week 1 and Week 2 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain the distinction between $X$ and $x$ without notes |
