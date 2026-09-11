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

## Components in observed time series

Real time series often contain several visually different components.

A common additive representation is

$$
X_t=T_t+S_t+R_t,
$$

where `T_t` is trend, `S_t` is seasonality and `R_t` is the remainder.

Trend is a long-run increase or decrease.

Seasonality is a repeating pattern with a fixed known period, such as 12 months or 4 quarters.

Cycles are also repeated up-and-down movements, but unlike seasonality they do not have a fixed period. Cyclic behavior can still be compatible with stationarity.

A multiplicative representation,

$$
X_t=T_tS_tR_t,
$$

is useful when fluctuations grow with the level of the series. Taking logs converts this into an additive form.

## Where non-stationarity can come from

Week 1 highlights several common sources of non-stationarity:

- deterministic trend;
- stochastic trend;
- seasonality;
- level-dependent variability.

A deterministic trend changes predictably with time.

A stochastic trend, such as a random walk, is driven by accumulated shocks.

Seasonality makes the expected level depend on where we are in the seasonal cycle.

Level-dependent variability can make the variance change as the series level changes.

These are the kinds of patterns we look for before applying stationary time-series models.

## Lag operator and differencing

The lag operator is compact notation for moving backward in time:

$$
LX_t=X_{t-1}.
$$

More generally,

$$
L^jX_t=X_{t-j}.
$$

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta X_t=(1-L)X_t.
$$

The key conceptual move is that differencing changes the object we model.

Instead of modeling the level `X_t`, we model how much it changed from the previous period.

For a random walk,

$$
X_t=X_{t-1}+\varepsilon_t,
$$

so

$$
\Delta X_t=\varepsilon_t.
$$

The level is non-stationary, while the first difference is stationary white noise.

Differencing also removes a deterministic linear trend in the sense that

$$
X_t=\beta_0+\beta_1t+\varepsilon_t
$$

becomes

$$
\Delta X_t=\beta_1+\Delta\varepsilon_t.
$$

The growing level is replaced by a constant increment.

## Week 2 begins: modeling stationary dynamics

Once a series is stationary, the next question is not just whether it is stable, but how values depend on the past.

This is where AR, MA and ARMA models enter.

An autoregressive model, or AR model, says that the current value depends on earlier values of the same series.

The simplest example is

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

The previous value carries forward through `phi`, while `epsilon_t` is the new shock arriving today.

Because `X_{t-1}` itself contains older shocks, an AR model can carry the influence of a shock far into the future. The effect may shrink over time, but it does not have to disappear after a fixed number of periods.

A moving-average model, or MA model, works differently. It models the current value directly using current and past shocks.

For example,

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1}.
$$

This MA(1) remembers today's shock and yesterday's shock directly, but no shock further back.

So the easiest distinction to remember is:

> AR remembers past values. MA remembers past shocks.

An ARMA model combines the two ideas. In ARMA(p,q), `p` counts the number of AR lags and `q` counts the number of MA shock lags.

The mathematics used later to decide whether an ARMA model is stationary involves polynomials, roots and the unit circle. Those are general mathematical ideas, so their detailed explanation is kept in the mathematics branch and linked from the time-series notes.

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
→ trend / seasonality / cycles / changing variability
→ sources of non-stationarity
→ lag operator
→ differencing and transformations
→ stationary dynamics
→ AR: past values
→ MA: past shocks
→ ARMA: both mechanisms together
```

## What comes next

For Week 2, the next steps are lag-polynomial notation, stationarity and causality, statistical properties of ARMA models, invertibility and parameter estimation.

## What to remember right now

Stationarity does not mean the series is constant.

Stationarity does not mean autocorrelation must be zero.

White noise is stationary and has zero autocorrelation at nonzero lags.

IID is stronger than white noise because independence is stronger than zero covariance.

A random walk accumulates shocks, so shocks have persistent effects on the level.

Trend and seasonality are common sources of non-stationarity.

Seasonality has a fixed known period; cycles do not.

The lag operator moves a variable backward in time.

Differencing changes levels into changes and can remove some forms of non-stationarity.

AR models use past values of the series.

MA models use current and past shocks.

ARMA models combine both mechanisms.

## When you forget the mathematics

Start with this page. Once the story is back in your head, use the detailed notes:

- [Basic properties of time series](basic-properties.md)
- [White noise and IID noise](white-noise-and-iid.md)
- [Random walk](random-walk.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [AR, MA and ARMA models](arma-models.md)
- [Complex numbers, polynomials and roots](../../mathematics/complex-numbers-and-polynomials.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 2: Deterministic and Stochastic Processes.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 3: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 4: Simple Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, part 2: Autoregressive Moving Average (ARMA) Models.
