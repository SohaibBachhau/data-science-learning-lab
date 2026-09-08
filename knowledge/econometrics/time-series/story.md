# The Story of Time Series Econometrics

Status: `developing`

This page is the low-friction narrative for time series. It will grow as the course progresses. The aim is to make it easy to remember what each topic is for before opening the detailed mathematics.

## The story so far

A time series is a sequence of observations recorded through time, such as daily stock prices, monthly unemployment or quarterly GDP growth.

The important difference from ordinary cross-sectional data is that order matters. Today's observation may be related to yesterday's observation, and that relationship can itself contain useful information.

We model the observed sequence as one realization of an underlying stochastic process.

Each `X_t` is a random variable. The number we actually observe at time `t` is written `x_t`.

Once we think of the data as coming from a stochastic process, we want to describe its basic behavior.

The mean tells us the expected level of the process.

The variance tells us how much it fluctuates around that level.

Autocovariance asks whether observations of the same process at different times tend to move together.

The lag `h` simply tells us how far apart the two observations are.

Stationarity then gives us a form of stability. For a weakly stationary process, the mean and variance do not change over time, and the covariance between observations depends only on how far apart they are, not on the specific calendar date.

This matters because we normally observe only one historical path. If the basic statistical relationship changed arbitrarily at every date, old observations would tell us much less about the same underlying process.

Autocorrelation takes the autocovariance and puts it on a standardized scale between -1 and 1:

$$
\rho(h)=\frac{\gamma(h)}{\gamma(0)}.
$$

The important idea is simpler than the formula:

> How strongly are observations `h` periods apart related?

The autocorrelation function, or ACF, collects that relationship across many lags.

A correlogram is simply a plot of the estimated sample autocorrelations across those lags.

## White noise: the benchmark shock process

White noise is the simplest stationary benchmark.

It has zero mean, constant variance and zero autocovariance at every nonzero lag. In other words, past shocks do not have a linear relationship with current shocks.

Its theoretical ACF is therefore 1 at lag 0 and 0 at every nonzero lag.

IID noise is stronger than white noise.

IID means the observations are independent and identically distributed. A useful way to remember it is:

> Every observation is a fresh draw from the same distribution.

White noise only rules out linear dependence through covariance. Independence rules out all dependence.

## Random walk: accumulated shocks

A random walk is built from white-noise shocks:

$$
X_t=X_{t-1}+\varepsilon_t.
$$

So white noise is the sequence of shocks, while the random walk is the accumulated total of those shocks.

A shock today changes the level today and remains embedded in future levels. This creates persistence and a stochastic trend.

The mean of the basic random walk can stay constant, but the variance grows over time:

$$
\operatorname{Var}(X_t)=t\sigma_\varepsilon^2.
$$

Its autocovariance also depends on calendar time:

$$
\operatorname{Cov}(X_t,X_{t-h})
=
(t-h)\sigma_\varepsilon^2.
$$

That violates weak stationarity.

So the contrast is:

```text
white noise
→ stationary
→ no autocorrelation at nonzero lags

random walk
→ accumulated white-noise shocks
→ variance grows over time
→ non-stationary
```

## The first differencing idea

The random walk also gives us our first important transformation.

From

$$
X_t=X_{t-1}+\varepsilon_t,
$$

we get

$$
X_t-X_{t-1}=\varepsilon_t.
$$

Therefore,

$$
\Delta X_t=\varepsilon_t.
$$

The random walk itself is non-stationary, but its first difference is white noise and stationary.

This is the first example of a central time-series strategy:

> If the level of a series is non-stationary, a transformation such as differencing may produce a stationary series that is easier to model.

## The story in one chain

```text
observations through time
→ stochastic process
→ mean and variance
→ autocovariance
→ weak stationarity
→ autocorrelation / ACF
→ white noise
→ IID as a stronger dependence assumption
→ random walk
→ non-stationarity
→ first differencing
```

## What comes next

The next Week 1 topics are time-series components and broader sources of non-stationarity: trend, seasonality, cycles and level-dependent variability.

After that come lag operators, ordinary differencing, seasonal differencing and log differences.

## What to remember right now

Stationarity does not mean the series is constant.

Stationarity does not mean autocorrelation must be zero.

White noise is stationary and has zero autocorrelation at nonzero lags.

IID is stronger than white noise because independence is stronger than zero covariance.

A random walk accumulates shocks, so shocks have persistent effects on the level.

A random walk has increasing variance and is therefore non-stationary.

Differencing a random walk gives white noise.

## When you forget the mathematics

Start with this page. Once the story is back in your head, use the detailed notes:

- [Basic properties of time series](basic-properties.md)
- [White noise and IID noise](white-noise-and-iid.md)
- [Random walk](random-walk.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 2: Deterministic and Stochastic Processes.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 3: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 4: Simple Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
