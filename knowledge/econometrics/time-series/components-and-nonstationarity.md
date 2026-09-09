# Time-Series Components and Sources of Non-Stationarity

Status: `developing`

## Central question

What visible structures can make a time series non-stationary, and how do trend, seasonality, cycles and changing variability differ?

## Concise answer

A time series may contain trend, seasonality, cycles and a remainder. Trend and seasonality can make the mean depend on time, while level-dependent variability can make the variance change with time. Cyclic behavior is different from seasonality because cycles do not have a fixed known period and can still be compatible with stationarity.

## Main time-series components

A common additive decomposition is

$$
X_t=T_t+S_t+R_t,
$$

where:

- `T_t` is the trend component;
- `S_t` is the seasonal component;
- `R_t` is the remainder.

Cycles are also discussed as a distinct source of medium- or long-run fluctuations.

## Trend

A trend is a long-term increase or decrease in the series. It does not need to be perfectly linear.

A deterministic linear trend can be written as

$$
X_t=\beta_0+\beta_1 t+\varepsilon_t.
$$

Then

$$
E(X_t)=\beta_0+\beta_1 t,
$$

so the mean depends on time.

This violates weak stationarity.

## Seasonality

Seasonality is a regular pattern with a fixed known period.

Examples include:

- monthly data with period `s=12`;
- quarterly data with period `s=4`.

If the expected level systematically differs by season, then the mean is not constant over time.

That makes the series non-stationary in the usual weak-stationarity sense.

## Cycles

Cycles are fluctuations around a trend without a fixed period.

A business cycle may last a different number of years each time.

This is the key difference:

> Seasonality repeats at a fixed known period, while cycles do not.

The course notes emphasize that cyclic behavior can be stationary.

## Remainder

The remainder is what remains after systematic components such as trend and seasonality are removed.

In the additive representation,

$$
R_t=X_t-T_t-S_t.
$$

The remainder is often the part we hope will look more stationary and less predictable.

## Additive decomposition

Use

$$
X_t=T_t+S_t+R_t
$$

when the magnitude of seasonal fluctuations does not depend strongly on the overall level of the series.

## Multiplicative decomposition

Use

$$
X_t=T_tS_tR_t
$$

when fluctuations grow or shrink with the level of the series.

For example, if seasonal movements are proportional to the level, a multiplicative representation is more natural.

Taking logs converts multiplication into addition:

$
\log X_t
=
\log T_t+\log S_t+\log R_t.
$

This is one reason logarithms are useful in time-series analysis.

## Classical decomposition and moving averages

The components `T_t`, `S_t` and `R_t` are not directly observed. Decomposition methods estimate them from the observed series.

The Week 1 lecture introduces classical decomposition, X-11 and STL. At this stage, the important intuition is the classical method.

A moving average smooths short-run fluctuations so that the underlying trend-cycle becomes easier to see.

For example, a simple centered 3-period moving average is

$
MA_t
=
\frac{X_{t-1}+X_t+X_{t+1}}{3}.
$

Classical decomposition roughly proceeds as follows:

1. estimate the trend-cycle with moving averages;
2. remove the estimated trend-cycle from the observed series;
3. estimate the seasonal component by averaging deviations for the same season;
4. treat what remains as the remainder.

X-11 and STL are alternative decomposition methods mentioned in the lecture, but Week 1 does not develop their algorithms in detail.

## Main sources of non-stationarity

The Week 1 lecture highlights several common sources:

- deterministic trend;
- stochastic trend;
- seasonality;
- level-dependent variability.

### Deterministic trend

A deterministic trend follows a predictable function of time, such as

$$
\beta_0+\beta_1 t.
$$

### Stochastic trend

A stochastic trend arises from accumulated random shocks, as in a random walk:

$$
X_t=X_{t-1}+\varepsilon_t.
$$

The path itself is random, and shocks can have persistent effects on the level.

### Level-dependent variability

Sometimes fluctuations become larger as the level of the series increases.

This can make the variance change over time, violating weak stationarity.

A variance-stabilizing transformation such as the logarithm can help when variability grows with the level.

## Visual checklist

When looking at a time-series plot, ask:

1. Is there a long-run upward or downward movement?
2. Is there a fixed repeating seasonal pattern?
3. Does the size of the fluctuations increase with the level?
4. Are there broader cycles without a fixed period?

The first three are common warning signs of non-stationarity. Cyclic movement alone does not automatically imply non-stationarity.

## Common mistakes

- A trend does not need to be linear.
- Seasonality and cycles are not the same.
- Cycles do not have a fixed known period.
- Additive and multiplicative decomposition are not interchangeable descriptions.
- A series can be non-stationary because its variance changes, even if its mean does not obviously trend.
- A stochastic trend is not the same thing as deterministic time trend.

## Retrieval questions

1. What are the main components of a time series?
2. What is the difference between seasonality and a cycle?
3. Why does a deterministic trend violate weak stationarity?
4. What makes a random walk a stochastic trend?
5. When is multiplicative decomposition more natural than additive decomposition?
6. Why can taking logs help with multiplicative structure or changing variability?
7. Which visual features should make you suspect non-stationarity?
8. What is the purpose of a moving average in classical decomposition?
9. What are the rough steps of classical decomposition?

## Related notes

- [Basic properties of time series](basic-properties.md)
- [Random walk](random-walk.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [Log differences, growth rates and returns](log-differences-growth-and-returns.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture: Basic Properties of Time Series.
