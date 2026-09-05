# Basic Properties of Time Series

Status: `developing`

## Central question

How can we describe the stable probabilistic structure of a variable observed over time?

## Concise answer

A time series is modeled as a stochastic process `{X_t}`, while the observed data `{x_t}` are one realization of that process. Important properties are the mean, variance and autocovariance. A weakly stationary process has a constant mean and an autocovariance that depends only on the lag between observations, not on the calendar time at which they are observed.

## Stochastic process and realization

A deterministic process has values that are completely determined by time or past values. For example,

$$
x_t = 2t.
$$

A stochastic process contains randomness. Each `X_t` is a random variable. The observed value `x_t` is one realization of that random variable.

Thus:

$$
\{X_t\}
\quad \text{is the stochastic process,}
$$

while

$$
\{x_t\}
\quad \text{is one observed realization.}
$$

## Mean function

The mean function of a stochastic process is

$$
\mu_X(t) = E(X_t).
$$

It gives the expected value of the process at time `t`.

If the mean changes with time, for example

$$
E(X_t) = 2t,
$$

the process cannot be weakly stationary.

## Autocovariance

The autocovariance function is

$$
\gamma_X(t,s) = \operatorname{Cov}(X_t,X_s).
$$

It measures linear dependence between the same process observed at two different times.

For a lag `h`,

$$
\operatorname{Cov}(X_t,X_{t-h})
$$

asks how values `h` periods apart tend to move together.

Positive autocovariance means values separated by that lag tend to be above or below their means together. Negative autocovariance means one tends to be above its mean when the other is below. Zero autocovariance means there is no linear dependence at that lag.

Variance is a special case:

$$
\operatorname{Var}(X_t)
=
\operatorname{Cov}(X_t,X_t)
=
\gamma_X(t,t).
$$

## Weak stationarity

A process `{X_t}` with finite second moments is weakly stationary, or covariance stationary, if:

1. the mean does not depend on time,

$$
E(X_t)=\mu_X,
$$

and

2. the autocovariance depends only on the lag `h`,

$$
\operatorname{Cov}(X_t,X_{t-h})=\gamma_X(h).
$$

The second condition means that only the distance between observations matters.

For example, all of the following are lag-1 covariances:

$$
\operatorname{Cov}(X_2,X_1),
$$

$$
\operatorname{Cov}(X_{51},X_{50}),
$$

and

$$
\operatorname{Cov}(X_{1001},X_{1000}).
$$

Under weak stationarity, they must all equal the same quantity:

$$
\gamma_X(1).
$$

## Why weak stationarity implies constant variance

Variance corresponds to lag zero:

$$
\operatorname{Var}(X_t)
=
\operatorname{Cov}(X_t,X_t)
=
\gamma_X(0).
$$

Since the autocovariance may depend only on the lag, `\gamma_X(0)` cannot depend on `t`. Therefore a weakly stationary process has constant variance.

## Autocorrelation

For a weakly stationary process, the autocorrelation at lag `h` is

$$
\rho_X(h)
=
\frac{\gamma_X(h)}{\gamma_X(0)}.
$$

It standardizes autocovariance so that the value lies between -1 and 1.

At lag zero,

$$
\rho_X(0)=1.
$$

For `h>0`, the autocorrelation does not have to be zero. It is zero only when

$$
\gamma_X(h)=0.
$$

White noise is a special case in which the autocovariance and autocorrelation are zero at every nonzero lag.

## Exercise-book result: why correlation depends only on lag

Start from the ordinary correlation between `X_t` and `X_{t-h}`:

$$
\rho_X(t,t-h)
=
\frac{
\operatorname{Cov}(X_t,X_{t-h})
}{
\sqrt{
\operatorname{Var}(X_t)
\operatorname{Var}(X_{t-h})
}
}.
$$

Weak stationarity gives

$$
\operatorname{Cov}(X_t,X_{t-h})=\gamma_X(h),
$$

and

$$
\operatorname{Var}(X_t)
=
\operatorname{Var}(X_{t-h})
=
\gamma_X(0).
$$

Therefore,

$$
\rho_X(t,t-h)
=
\frac{\gamma_X(h)}{\gamma_X(0)}
=
\rho_X(h).
$$

So the correlation also depends only on the lag.

## Why stationarity matters

In time-series data we normally observe only one realization of a stochastic process. Stationarity lets observations from different periods provide information about the same underlying quantities.

For example, if the process is stationary, every pair of observations one period apart provides information about the same lag-1 autocovariance `\gamma_X(1)`.

This stability is what makes it possible to estimate time-dependence from historical observations and use it for modeling and forecasting.

If the mean, variance or lag relationships changed arbitrarily over time, older observations would not necessarily tell us about the same statistical relationships as newer observations.

## Common mistakes

- Stationarity does not mean every observation is constant.
- Stationarity does not mean autocovariance is zero.
- Weak stationarity allows `\gamma_X(1)`, `\gamma_X(2)`, and other lags to differ.
- The restriction is that the covariance at a given lag cannot depend on the calendar time `t`.
- `\rho_X(h)=0` is not a general property of stationary series. It is a special property when `\gamma_X(h)=0`.

## Retrieval questions

1. What is the difference between `X_t` and `x_t`?
2. What does `\gamma_X(h)` measure?
3. Why is variance equal to the lag-zero autocovariance?
4. What are the two conditions for weak stationarity?
5. Why can `\gamma_X(1)` be nonzero in a stationary process?
6. Why does weak stationarity imply `\rho_X(t,t-h)=\rho_X(h)`?
7. Why is stationarity useful when we observe only one time-series realization?

## Related notes

- [Time Series Econometrics](README.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 2: Deterministic and Stochastic Processes.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 3: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
