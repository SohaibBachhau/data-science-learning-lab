---
title: Random Variables and Probability Distributions
subject: probability
status: developing
created: 2026-07-23
updated: 2026-09-06
last_reviewed: 2026-09-06
prerequisites:
  - sample spaces
  - events
  - probability
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 and Week 2 slides
  - VU Knowledge Clip Series: Probability Theory, Random Variables and Probability Distributions (2026)
  - KCS Probability Theory exercises (2026)
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

## Outcomes and events

Before defining a random variable, separate the underlying probability objects:

- an **outcome** is one possible result of the random experiment;
- a **realized outcome** is the particular outcome that actually occurs;
- an **event** is a set of outcomes.

For two coin tosses, the sample space is

$
\Omega=\{HH,HT,TH,TT\}.
$

Each element is an outcome. The event "both tosses show the same face" is

$
A=\{HH,TT\}.
$

A random variable then assigns numerical values to individual outcomes. For example,

$
X(HH)=-1,\qquad X(HT)=0,\qquad X(TH)=0,\qquad X(TT)=1.
$

This distinction is useful because an event is not an "outcome that has not happened yet." It is a collection of outcomes defined independently of whether the experiment has already been performed.

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

For a continuous random variable with density $f_X$,

$
F_X(x)=\int_{-\infty}^{x}f_X(t)\,dt.
$

If the support has a lower bound $L$ and $f_X(t)=0$ for $t<L$, then the same CDF can be computed as

$
F_X(x)=\int_L^x f_X(t)\,dt
$

for values of $x$ inside the support. The definition still starts at $-\infty$; the shorter integral works because there is zero density below $L$.

The probability to the right of $x$ is a tail probability,

$
P(X>x)=1-F_X(x),
$

not the CDF itself.

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

The height $f_X(x)$ is a **density**, not the probability $P(X=x)$. A higher density means probability is more concentrated locally, but actual interval probabilities depend on area, so both density and interval width matter.

Probabilities are obtained from areas under the density:

$$
P(a\leq X\leq b)=\int_a^b f_X(x)\,dx.
$$

For a continuous random variable,

$$
P(X=x)=0
$$

for every single value $x$. This does not mean that the value cannot occur. It means that a single point has zero area under a continuous density.

## Linear transformations of a normal random variable

A particularly useful property of the normal distribution is that a linear transformation of a normal random variable is still normal.

Suppose

$$
A\sim N(\mu,\sigma^2)
$$

and define

$$
B=aA+c,
$$

where $a$ and $c$ are constants. Then

$$
B\sim N(a\mu+c,a^2\sigma^2).
$$

This formula combines two simpler transformation rules.

### Adding a constant

If

$$
B=A+c,
$$

then

$$
B\sim N(\mu+c,\sigma^2).
$$

Adding a constant shifts every possible value by the same amount. Therefore, the center of the distribution moves, but its spread does not change.

The expectation changes because

$$
E[A+c]=E[A]+c=\mu+c.
$$

The variance does not change because

$$
\operatorname{Var}(A+c)=\operatorname{Var}(A)=\sigma^2.
$$

#### Numerical example

Let

$$
A\sim N(10,4).
$$

Here the mean is $10$, the variance is $4$ and the standard deviation is $2$.

If

$$
B=A+3,
$$

then

$$
B\sim N(13,4).
$$

Every value has moved three units to the right. The standard deviation remains $2$.

### Multiplying by a constant

If

$$
B=aA,
$$

then

$$
B\sim N(a\mu,a^2\sigma^2).
$$

The mean is multiplied by $a$:

$$
E[aA]=aE[A]=a\mu.
$$

The variance is multiplied by $a^2$:

$$
\operatorname{Var}(aA)=a^2\operatorname{Var}(A)=a^2\sigma^2.
$$

The standard deviation is therefore multiplied by $|a|$:

$$
\operatorname{SD}(aA)=|a|\sigma.
$$

The square on $a$ is important. Variance measures squared deviations from the mean, so multiplying all deviations by $a$ multiplies their squared values by $a^2$.

#### Numerical example

Again let

$$
A\sim N(10,4).
$$

If

$$
B=2A,
$$

then

$$
E[B]=2(10)=20
$$

and

$$
\operatorname{Var}(B)=2^2(4)=16.
$$

Therefore,

$$
B\sim N(20,16).
$$

The original standard deviation was $2$. After multiplying the random variable by $2$, the new standard deviation is $4$.

### Multiplying and then adding

For the general transformation

$$
B=aA+c,
$$

combine both rules:

$$
E[B]=a\mu+c
$$

and

$$
\operatorname{Var}(B)=a^2\sigma^2.
$$

The constant $c$ changes the location but not the variance.

#### Numerical example with a negative multiplier

Let

$$
A\sim N(10,4)
$$

and define

$$
B=-2A+5.
$$

The new mean is

$$
E[B]=-2(10)+5=-15.
$$

The new variance is

$$
\operatorname{Var}(B)=(-2)^2(4)=16.
$$

Therefore,

$$
B\sim N(-15,16).
$$

The negative multiplier reflects the distribution around zero before the shift is applied. It does not make the variance negative because the multiplier is squared.

#### Numerical example with division

Let

$$
A\sim N(10,4)
$$

and define

$$
B=\frac{1}{2}A-1.
$$

Then

$$
E[B]=\frac{1}{2}(10)-1=4
$$

and

$$
\operatorname{Var}(B)=\left(\frac{1}{2}\right)^2(4)=1.
$$

Therefore,

$$
B\sim N(4,1).
$$

### Standardization as an important special case

If

$$
A\sim N(\mu,\sigma^2),
$$

then subtracting the mean and dividing by the standard deviation gives

$$
Z=\frac{A-\mu}{\sigma}.
$$

This is a linear transformation with

$$
a=\frac{1}{\sigma}
$$

and

$$
c=-\frac{\mu}{\sigma}.
$$

The transformed mean is

$$
E[Z]=0
$$

and the transformed variance is

$$
\operatorname{Var}(Z)=1.
$$

Therefore,

$$
Z\sim N(0,1).
$$

This is the standard normal distribution.

### Rule to remember

If

$$
A\sim N(\mu,\sigma^2),
$$

then

$$
\boxed{aA+c\sim N(a\mu+c,a^2\sigma^2)}.
$$

The location rule is linear, while the variance rule contains a square.

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
- Forgetting that multiplying a random variable by $a$ multiplies its variance by $a^2$, not by $a$.
- Confusing variance $\sigma^2$ with standard deviation $\sigma$ when transforming a normal random variable.
- Thinking that adding a constant changes the variance.

## Retrieval questions

1. What is random about a random variable?
2. What is the difference between $X$ and $x$?
3. What information does $F_X(x)$ provide?
4. Why is $P(X=x)=0$ for a continuous random variable?
5. If $A\sim N(\mu,\sigma^2)$, what is the distribution of $aA+c$?
6. Why does adding a constant change the mean but not the variance?
7. Why does multiplying by $a$ multiply the variance by $a^2$?
8. If $A\sim N(10,4)$, what is the distribution of $2A+3$?
9. How does the linear-transformation rule produce the standard normal distribution?
10. What is the difference between a marginal and conditional distribution?
11. Why does regression depend on the joint distribution of $X$ and $Y$?

## Connections

- [Expectation](expectation.md)
- [Conditional expectation](conditional-expectation.md)
- [Joint distributions, independence and iid sampling](joint-distributions-independence-and-iid.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1 and Appendix A.
- *Introductory Econometrics for Business and Economics*, Week 1 and Week 2 slides.
- Standard probability result for affine transformations of normally distributed random variables.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain the distinction between $X$ and $x$ without notes |
| 2026-08-01 | Added linear transformations of normal variables | Reproduce the transformation rule and numerical examples without notes |
| 2026-09-06 | Reviewed VU Probability Theory clip 1 and exercises; clarified outcomes versus events, PDF height versus probability, and practical CDF limits | Continue with Normal Distribution and Moments I |
