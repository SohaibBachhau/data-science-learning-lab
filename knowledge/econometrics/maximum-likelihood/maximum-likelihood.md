---
title: Maximum Likelihood
subject: econometrics
status: developing
created: 2026-07-23
updated: 2026-07-23
last_reviewed:
prerequisites:
  - probability distributions
  - logarithms
  - differentiation
sources:
  - Blasques, Advanced Econometric Methods
  - IEBE Week 1 slides
tags:
  - maximum likelihood
  - likelihood
  - log-likelihood
  - OLS
---

# Maximum Likelihood

## Central question

How can a fully specified probability model be used to estimate unknown parameters, and why does normal regression maximum likelihood produce the OLS coefficient estimates?

## Short answer

Maximum likelihood chooses the parameter value under which the observed sample has the greatest likelihood according to the assumed probability model. For independent normal regression errors with constant variance, maximizing the likelihood with respect to the regression coefficients is equivalent to minimizing the sum of squared residuals, so the maximum-likelihood coefficient estimator equals OLS.

## Probability model

Let the distribution of an observation $Y$ depend on an unknown parameter vector $\theta$. Its density or probability mass function is written as

$$
f(y;\theta).
$$

Before observing the data, $y$ is variable and $\theta$ is treated as a fixed parameter. The model describes how probabilities change across possible data values for each candidate $\theta$.

## Likelihood function

After observing $y$, the likelihood treats the data as fixed and evaluates the model as a function of the parameter:

$$
L(\theta;y)=f(y;\theta).
$$

The same mathematical expression can be viewed as a density in $y$ or a likelihood in $\theta$, but the interpretation differs.

A likelihood is not a probability distribution over $\theta$ in frequentist estimation. It need not integrate to one over the parameter space.

## Likelihood for an iid sample

If $Y_1,\ldots,Y_n$ are iid with density $f(y_i;\theta)$, their joint density factorizes:

$$
L_n(\theta)
=
\prod_{i=1}^n f(Y_i;\theta).
$$

Independence creates the product. Identical distribution allows the same density form to be used for each observation.

For independent but non-identically distributed observations, the likelihood can still be a product with observation-specific densities.

## Maximum-likelihood estimator

The maximum-likelihood estimator is

$$
\hat\theta_{ML}
=
\arg\max_{\theta\in\Theta}L_n(\theta),
$$

where $\Theta$ is the parameter space.

Because the sample is random, $\hat\theta_{ML}$ is a random variable before the data are observed.

## Log-likelihood

The log-likelihood is

$$
\ell_n(\theta)
=
\log L_n(\theta).
$$

For an independent sample,

$$
\ell_n(\theta)
=
\sum_{i=1}^n\log f(Y_i;\theta).
$$

The logarithm is strictly increasing, so

$$
\arg\max_{\theta}L_n(\theta)
=
\arg\max_{\theta}\ell_n(\theta).
$$

The log-likelihood is preferred because it converts products into sums, simplifies derivatives and reduces numerical underflow.

## Score and first-order condition

The score is the gradient of the log-likelihood:

$$
s_n(\theta)
=
\frac{\partial\ell_n(\theta)}{\partial\theta}.
$$

An interior maximum often satisfies

$$
s_n(\hat\theta_{ML})=0.
$$

This first-order condition alone does not guarantee a maximum. The objective's curvature, parameter boundaries and possible multiple optima must also be considered.

## Hessian and information

The Hessian is

$$
H_n(\theta)
=
\frac{\partial^2\ell_n(\theta)}
{\partial\theta\partial\theta'}.
$$

At a strict local maximum, the Hessian is negative definite under regular conditions.

The Fisher information measures the curvature and expected variability of the score. Under correct specification and regularity conditions, common expressions are

$$
I(\theta)
=
-E[H_i(\theta)]
$$

and

$$
I(\theta)
=
E[s_i(\theta)s_i(\theta)'].
$$

The equality of these two expressions is an information-matrix equality that relies on regularity and correct specification.

## Normal regression model

Consider

$$
Y_i=\beta_0+\beta_1X_i+u_i
$$

with

$$
u_i\mid X_i\sim N(0,\sigma^2).
$$

Then

$$
Y_i\mid X_i
\sim
N(\beta_0+\beta_1X_i,\sigma^2).
$$

The conditional density is

$$
f(Y_i\mid X_i;\beta_0,\beta_1,\sigma^2)
=
\frac{1}{\sqrt{2\pi\sigma^2}}
\exp\left[
-\frac{(Y_i-\beta_0-\beta_1X_i)^2}{2\sigma^2}
\right].
$$

Assuming conditional independence, the likelihood is the product of these densities.

## Normal regression log-likelihood

The log-likelihood is

$$
\ell(\beta_0,\beta_1,\sigma^2)
=
-\frac{n}{2}\log(2\pi)
-\frac{n}{2}\log(\sigma^2)
-\frac{1}{2\sigma^2}
\sum_{i=1}^n
(Y_i-\beta_0-\beta_1X_i)^2.
$$

For a fixed positive $\sigma^2$, the first two terms do not depend on $\beta_0$ or $\beta_1$. Maximizing the log-likelihood over the regression coefficients is therefore equivalent to minimizing

$$
\sum_{i=1}^n
(Y_i-\beta_0-\beta_1X_i)^2.
$$

Hence,

$$
\hat\beta_{ML}=\hat\beta_{OLS}.
$$

The equality concerns the coefficient estimates under this normal homoskedastic model.

## ML estimate of the error variance

After substituting the coefficient estimates, maximizing with respect to $\sigma^2$ gives

$$
\hat\sigma^2_{ML}
=
\frac{1}{n}\sum_{i=1}^n\hat u_i^2.
$$

This differs from the common degrees-of-freedom-corrected OLS estimator

$$
\hat\sigma^2
=
\frac{1}{n-k-1}\sum_{i=1}^n\hat u_i^2.
$$

The ML variance estimator uses $n$ and is generally biased downward in finite samples because it does not correct for estimated regression coefficients. It is nevertheless consistent under suitable assumptions.

## Why normality produces squared loss

The normal density contains the exponential term

$$
\exp\left(-\frac{u_i^2}{2\sigma^2}\right).
$$

Taking logs produces a negative multiple of $u_i^2$. Therefore, choosing the parameters that make normal residuals most likely is the same as minimizing their squared values.

Different distributional assumptions produce different objective functions. For example, a Laplace error model leads to minimizing absolute residuals rather than squared residuals.

## Correct specification

Maximum likelihood specifies an entire probability distribution, not only a conditional mean.

For the normal regression likelihood to be correctly specified, the stated conditional distribution must match the true one, including:

- the conditional mean function;
- the conditional variance structure;
- the distributional shape;
- the independence or dependence structure used in the joint likelihood.

A correct linear conditional mean does not imply that normality and homoskedasticity are correct.

## Consistency and asymptotic normality

Under identification, correct specification and regularity conditions,

$$
\hat\theta_{ML}
\overset{p}{\longrightarrow}
\theta_0
$$

and

$$
\sqrt{n}(\hat\theta_{ML}-\theta_0)
\overset{d}{\longrightarrow}
N(0,I(\theta_0)^{-1}).
$$

The intuition for consistency is that the average log-likelihood converges to its population expectation, which is uniquely maximized at the true parameter.

The intuition for asymptotic normality is that a Taylor expansion of the score around the true parameter combines a central limit theorem for the score with a law of large numbers for the Hessian.

## Misspecified maximum likelihood

When the chosen distribution family is wrong, the estimator may still converge to a pseudo-true parameter that maximizes the population expected log-likelihood.

The usual inverse-information variance formula may then be incorrect. A sandwich covariance matrix is generally needed because the expected Hessian and score variance need not coincide.

## Likelihood versus probability of the hypothesis

The likelihood compares how compatible different parameter values are with the observed data within the chosen model. It does not directly provide

$$
P(\theta\mid Y).
$$

A posterior probability for the parameter requires a Bayesian model with a prior distribution and Bayes' rule.

## Example: Bernoulli likelihood

Let $Y_i\in\{0,1\}$ be iid Bernoulli with success probability $p$. Then

$$
L(p)
=
\prod_{i=1}^n p^{Y_i}(1-p)^{1-Y_i}.
$$

The log-likelihood is

$$
\ell(p)
=
\sum_{i=1}^n
\left[
Y_i\log p+(1-Y_i)\log(1-p)
\right].
$$

Differentiating and solving the first-order condition gives

$$
\hat p_{ML}=\bar Y.
$$

Thus, the sample proportion is the maximum-likelihood estimator of the Bernoulli success probability.

## Common mistakes

- Treating likelihood as a probability distribution over the parameter.
- Forgetting that independence is what turns a joint likelihood into a product.
- Saying the log transformation changes the maximizer.
- Assuming a zero score always identifies a global maximum.
- Believing normality is required to calculate OLS rather than to derive OLS from a normal likelihood and obtain exact distribution theory.
- Assuming a correct conditional mean implies a correctly specified likelihood.
- Using the inverse-information variance formula under misspecification without checking its validity.
- Confusing the ML error-variance denominator $n$ with the degrees-of-freedom-corrected denominator.

## Retrieval questions

1. What changes when a density is viewed as a likelihood?
2. Why does the likelihood factorize for independent observations?
3. Why is maximizing the log-likelihood equivalent to maximizing the likelihood?
4. Define the score and Hessian.
5. Derive why normal regression ML and OLS give the same coefficient estimates.
6. Why do the ML and corrected OLS variance estimators use different denominators?
7. What changes under likelihood misspecification?

## Connections

- [Random variables and distributions](../../probability/random-variables-and-distributions.md)
- [Ordinary least squares](../linear-regression/ordinary-least-squares.md)
- [Correct specification](../linear-regression/correct-specification.md)
- [Consistency](../../statistics/consistency.md)
- [Asymptotic normality](../../statistics/asymptotic-normality.md)

## Sources

- Francisco Blasques, *Advanced Econometric Methods*, Chapter 1, sections on maximum likelihood.
- *Introductory Econometrics for Business and Economics*, Week 1 slides.

## Review log

| Date | Result | Next action |
|---|---|---|
| 2026-07-23 | Initial note created | Derive the normal regression log-likelihood and its OLS equivalence |
