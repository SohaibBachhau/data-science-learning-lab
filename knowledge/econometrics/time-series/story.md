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

So the story currently looks like this:

```text
observations through time
→ stochastic process
→ mean and variance
→ autocovariance
→ weak stationarity
→ autocorrelation
→ ACF
→ correlogram
```

## What comes next

The next step is to study two very simple processes that give us useful reference points.

White noise represents a stationary process with no autocorrelation at nonzero lags.

A random walk accumulates random shocks over time and is non-stationary.

That contrast will make the ideas of persistence, trends and differencing much more concrete.

Later Week 1 will connect these ideas to time-series components, non-stationarity, lag operators, differencing, seasonal differencing and log differences.

## What to remember right now

Stationarity does not mean the series is constant.

Stationarity does not mean autocorrelation must be zero.

It means the basic first- and second-moment structure is stable over time.

Autocovariance measures raw linear dependence across time. Autocorrelation standardizes that dependence.

The theoretical ACF belongs to the underlying stochastic process. The sample ACF is what we estimate from the one realization we observe.

## When you forget the mathematics

Start with this page. Once the story is back in your head, open [Basic properties of time series](basic-properties.md) for the formal definitions and derivations.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 2: Deterministic and Stochastic Processes.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 3: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
