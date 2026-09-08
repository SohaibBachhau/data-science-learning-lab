# White Noise and IID Noise

Status: `developing`

## Central question

What does it mean for time-series shocks to contain no systematic dependence over time, and how is that different from being iid?

## Concise answer

A white-noise process has zero mean, constant variance and zero autocovariance at every nonzero lag. IID noise is a stronger condition: observations are independent and all come from the same distribution.

## White noise

Write

$$
\{\varepsilon_t\} \sim WN(0,\sigma_\varepsilon^2).
$$

This means:

$$
E(\varepsilon_t)=0,
$$

$$
\operatorname{Var}(\varepsilon_t)=\sigma_\varepsilon^2,
$$

and for every nonzero lag `h`,

$$
\operatorname{Cov}(\varepsilon_t,\varepsilon_{t-h})=0.
$$

So white noise has no linear dependence across time.

## Why white noise is weakly stationary

The mean is constant:

$$
E(\varepsilon_t)=0.
$$

The variance is constant:

$$
\operatorname{Var}(\varepsilon_t)=\sigma_\varepsilon^2.
$$

The autocovariance depends only on the lag:

$$
\gamma_\varepsilon(h)=
\begin{cases}
\sigma_\varepsilon^2, & h=0,\\
0, & h\neq 0.
\end{cases}
$$

Therefore white noise is weakly stationary.

## ACF of white noise

Because

$$
\rho_\varepsilon(h)=\frac{\gamma_\varepsilon(h)}{\gamma_\varepsilon(0)},
$$

we have

$$
\rho_\varepsilon(0)=1
$$

and

$$
\rho_\varepsilon(h)=0
\quad \text{for } h\neq 0.
$$

In a finite sample, estimated autocorrelations will generally not be exactly zero because of sampling variation.

## IID noise

IID means:

- independent;
- identically distributed.

Identically distributed means every observation follows the same probability distribution.

Independent means that knowing one observation does not change the probability distribution of another.

A useful intuition is:

> IID observations are fresh draws from the same distribution.

For example, repeated rolls of the same fair die with replacement are iid.

## Why IID is stronger than white noise

Independence is stronger than zero covariance.

If observations are independent and have the same finite mean and variance, then they are uncorrelated and satisfy the white-noise conditions after centering appropriately.

But zero covariance does not imply independence. Two variables can be dependent in a nonlinear way while still having covariance zero.

Therefore:

$$
\text{IID} \Rightarrow \text{white noise}
$$

under the usual finite-moment setup, but in general

$$
\text{white noise} \nRightarrow \text{IID}.
$$

## Concrete distinction

White noise says:

> There is no linear predictability from past shocks.

IID says:

> The observations are fully independent draws from the same distribution.

So IID gives stronger information about the joint distribution.

## Common mistakes

- White noise does not mean every realization equals zero.
- White noise does not require observations to be independent.
- Zero covariance is weaker than independence.
- Identically distributed does not mean observations take identical realized values.
- A sample correlogram of white noise will not show exact zeros at every lag.

## Retrieval questions

1. What three conditions define white noise?
2. Why is white noise weakly stationary?
3. What does the ACF of theoretical white noise look like?
4. What do the two letters in iid mean?
5. Why is independence stronger than zero covariance?
6. Why can white noise fail to be iid?
7. What does "identically distributed" mean in plain language?

## Related notes

- [Basic properties of time series](basic-properties.md)
- [Random walk](random-walk.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 4: Simple Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
