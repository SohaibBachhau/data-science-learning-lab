---
title: Joint Distributions, Independence and IID Sampling
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
  - IEBE Week 2 slides
tags:
  - joint distributions
  - independence
  - iid
  - random sampling
---

# Joint Distributions, Independence and IID Sampling

## Central question

What does it mean for observations to be independent and identically distributed, and which objects are assumed to be iid in econometrics?

## Short answer

A joint distribution describes several random variables together. Independence means that learning the value of one random object does not change the distribution of another. Identically distributed means that the objects follow the same probability law. In a cross-sectional regression, the iid assumption usually applies to the observation vectors $(X_i,Y_i)$, not to $X_i$ and $Y_i$ within the same observation.

## Joint distributions

For two discrete random variables $X$ and $Y$, the joint probability mass function is

$$
p_{X,Y}(x,y)=P(X=x,Y=y).
$$

For continuous variables, a joint density $f_{X,Y}(x,y)$ describes their combined distribution.

A joint distribution contains more information than two separate marginal distributions because it also describes how the variables move together.

For example, knowing the separate distributions of education and income does not tell us whether highly educated people tend to have higher incomes. That relationship is part of their joint distribution.

## Marginal distributions

The marginal distribution of one variable is obtained from the joint distribution by summing or integrating over the other variable.

For discrete variables,

$$
p_X(x)=\sum_y p_{X,Y}(x,y).
$$

For continuous variables,

$$
f_X(x)=\int_{-\infty}^{\infty}f_{X,Y}(x,y)\,dy.
$$

## Conditional distributions

The conditional distribution of $Y$ given $X=x$ describes the behavior of $Y$ within the part of the population for which $X=x$.

For discrete variables,

$$
P(Y=y\mid X=x)=\frac{P(X=x,Y=y)}{P(X=x)},
$$

provided $P(X=x)>0$.

## Independence of random variables

Random variables $X$ and $Y$ are independent when their joint distribution factorizes into their marginal distributions.

For discrete variables,

$$
P(X=x,Y=y)=P(X=x)P(Y=y)
$$

for all relevant $x$ and $y$.

Equivalently, when the conditional distribution is defined,

$$
P(Y=y\mid X=x)=P(Y=y).
$$

This means that knowing $X$ does not change what we know about the distribution of $Y$.

## Independence is stronger than zero covariance

If $X$ and $Y$ are independent and the required moments exist, then

$$
\operatorname{Cov}(X,Y)=0.
$$

The reverse is generally false. Zero covariance rules out a linear relationship in the population, but nonlinear dependence can remain.

### Example

Let $X$ be symmetric around zero and let

$$
Y=X^2.
$$

Then $Y$ is completely determined by $X$, so they are not independent. Yet symmetry can produce

$$
\operatorname{Cov}(X,Y)=\operatorname{Cov}(X,X^2)=0.
$$

## Independence across observations

Suppose the dataset contains observation vectors

$$
Z_i=(X_i,Y_i),\qquad i=1,\ldots,n.
$$

Independence across observations means that the random vector $Z_i$ for one sampled unit does not provide information about the random vector $Z_j$ for another sampled unit.

It does not mean that $X_i$ and $Y_i$ are independent within observation $i$. Indeed, regression is useful precisely because $X_i$ and $Y_i$ may be related.

## Identically distributed observations

The observations are identically distributed when every vector $Z_i=(X_i,Y_i)$ follows the same joint distribution.

This means that the same population data-generating mechanism applies to every observation. It does not mean that all observations have the same realized values.

Different observations can have different $X_i$ values and therefore different conditional means $E[Y_i\mid X_i]$, while the pairs $(X_i,Y_i)$ still come from the same joint population distribution.

## IID sampling

The notation

$$
Z_1,\ldots,Z_n\overset{iid}{\sim}P
$$

means:

1. the vectors $Z_1,\ldots,Z_n$ are independent of one another;
2. each vector has the same distribution $P$.

In introductory cross-sectional econometrics, the least-squares sampling assumption is often written as

$$
(X_i,Y_i),\qquad i=1,\ldots,n,
$$

being iid draws from their joint distribution.

A simple random sample from a stable population is a common reason this assumption may be plausible.

## What iid does not mean

IID does not mean:

- every observed value is the same;
- $X_i$ and $Y_i$ are independent within an observation;
- all conditional distributions $Y\mid X=x$ have the same mean;
- observations have no common variables or shared model parameters;
- the assumption is suitable for every type of data.

## Time series and panel data

IID observations are often inappropriate for time series because adjacent observations can be serially dependent.

For panel data, repeated measurements for the same entity are generally dependent over time. A panel-data sampling assumption may instead require the entity-level histories to be iid across entities:

$$
(X_{i1},\ldots,X_{iT},u_{i1},\ldots,u_{iT}),
\qquad i=1,\ldots,n.
$$

Thus, observations can be dependent within an entity while entities are independent across $i$.

## Why iid is useful

IID assumptions make it possible to apply standard laws of large numbers and central limit theorems. These results connect sample averages to population expectations and provide large-sample approximations to estimator distributions.

IID is a sufficient framework used in introductory derivations. More advanced econometrics permits many forms of dependence and non-identical distributions, provided suitable alternative assumptions hold.

## Common mistakes

- Saying that $X$ and $Y$ must be independent because the sample is iid.
- Interpreting identically distributed as identically valued.
- Applying iid directly to individual panel observations when repeated observations belong to the same entity.
- Assuming that different conditional expectations contradict identical joint distributions.
- Treating zero covariance as equivalent to independence.

## Retrieval questions

1. What information is contained in a joint distribution that is absent from marginal distributions?
2. Which objects are usually iid in a cross-sectional regression?
3. Why can $E[Y\mid X=x]$ vary with $x$ even when observations are identically distributed?
4. Does iid sampling imply that $X_i$ and $Y_i$ are independent?
5. Why is zero covariance weaker than independence?
6. How is an iid assumption adapted for panel data?

## Connections

- [Random variables and distributions](random-variables-and-distributions.md)
- [Conditional expectation](conditional-expectation.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Law of large numbers](law-of-large-numbers.md)
- [Central limit theorem](central-limit-theorem.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1.
- *Introductory Econometrics for Business and Economics*, Week 2 slides.
- *Introductory Econometrics for Business and Economics*, Week 6 slides for the entity-level panel sampling distinction.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Explain iid sampling in one sentence and give a regression example |
