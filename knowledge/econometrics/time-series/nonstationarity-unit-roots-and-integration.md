# Non-Stationarity, Unit Roots and Integration

Status: `developing`

## Central question

How do we recognize non-stationary behavior, what is a unit root, and how does differencing turn some non-stationary series into stationary ones?

## Concise answer

Week 3 starts from the limitation of Week 2:

> ARMA models are designed for stationary time series.

A time series is non-stationary when its mean and/or autocovariance changes over time. In this course, the main Week 3 focus is non-stationarity caused by trend and seasonality, especially unit-root non-stationarity.

The main chain is:

```text
spot non-stationarity
-> remove trend / seasonality when appropriate
-> determine the order of integration
-> distinguish unit-root from explosive non-stationarity
-> test for a unit root
-> later model the transformed series with ARIMA / SARIMA
```

## Recall: weak stationarity

A weakly stationary process has:

1. a mean that does not depend on time;
2. an autocovariance that depends only on the lag, not on the calendar date.

So a non-stationary process violates at least one of those stability conditions.

Week 3 treats non-stationarity mainly through trends and seasonality.

## How to spot non-stationarity

The course gives two broad routes:

1. visual inspection;
2. statistical testing.

### Time-series plot

Warning signs include:

- a clear upward or downward trend;
- a regular seasonal pattern;
- variability that increases with the level of the series.

If variability grows with the level, a logarithmic transformation can help stabilize the variance.

### ACF

For a stationary series, the ACF tends to fall toward zero relatively quickly.

For non-stationary data, the ACF often decreases slowly.

Seasonality can appear as significant autocorrelations at regular seasonal lags.

For monthly data, for example, a seasonal pattern may show up around lags 12, 24, 36, and so on.

## Removing trend and seasonality by differencing

### First difference

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta X_t=(1-L)X_t.
$$

A first difference can remove a deterministic linear trend and is also the key transformation for a random walk.

### Seasonal difference

For a seasonal period `s`,

$$
\Delta_sX_t=X_t-X_{t-s}.
$$

For monthly data with yearly seasonality,

$$
\Delta_{12}X_t=X_t-X_{t-12}.
$$

This compares a month with the same month one year earlier.

### Combining both

If a series contains both an ordinary trend and seasonality, we may use both differences:

$$
\Delta_s\Delta X_t.
$$

The course notes that the order does not matter:

$$
\Delta_s\Delta X_t
=
\Delta\Delta_sX_t.
$$

## Order of integration

The order of integration is the minimum number of ordinary differences required to make a series stationary.

A series is denoted

$$
X_t\sim I(d)
$$

when it becomes stationary after differencing `d` times.

### I(0)

`I(0)` means the series is already stationary.

No ordinary differencing is needed.

### I(1)

`I(1)` means the level is non-stationary but the first difference is stationary:

$$
X_t\sim I(1)
\qquad\Longrightarrow\qquad
\Delta X_t\sim I(0).
$$

### I(2)

`I(2)` means two ordinary differences are needed:

$$
X_t\sim I(2)
\qquad\Longrightarrow\qquad
\Delta^2X_t\sim I(0).
$$

The important word is **minimum**. If the original series is stationary, it is `I(0)`; we do not difference it anyway and then relabel it `I(1)`.

## Overdifferencing

Differencing is not harmless.

If a series is already stationary and we difference it again, the course warns that this can:

- introduce unnecessary dependence;
- introduce moving-average structure into the errors;
- make estimation less efficient.

So the goal is not "difference until it looks very stable."

The goal is:

> use the smallest amount of differencing needed to obtain stationarity.

## Unit-root non-stationarity

Return to the AR(1) model:

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

For the stationary AR(1) case,

$$
|\phi|<1.
$$

If

$$
\phi=1,
$$

the model becomes

$$
X_t=X_{t-1}+\varepsilon_t,
$$

which is a random walk.

The random walk is non-stationary.

## Why it is called a unit root

Write the AR(1) in lag-polynomial form:

$$
(1-\phi L)X_t=\varepsilon_t.
$$

The characteristic equation is

$$
1-\phi z=0.
$$

So the root is

$$
z=\frac{1}{\phi}.
$$

For a random walk,

$$
\phi=1,
$$

therefore

$$
z=1.
$$

That is the source of the term **unit root**.

More generally, a root on the unit circle satisfies

$$
|z|=1.
$$

In the simple real-valued AR(1) unit-root case emphasized here,

$$
z=1.
$$

## Do not confuse "no unit root" with "stationary"

For the root convention used in this course:

$$
|z|>1
\quad\Rightarrow\quad
\text{stationary},
$$

$$
|z|=1
\quad\Rightarrow\quad
\text{unit-root non-stationary},
$$

and

$$
|z|<1
\quad\Rightarrow\quad
\text{explosive non-stationary}.
$$

So the statement

> "the process is stationary because it does not have a unit root"

is too broad.

A root can lie inside the unit circle, so the process has no unit root but is still non-stationary because it is explosive.

The correct stationarity condition is:

$$
\boxed{\text{all AR roots satisfy }|z|>1.}
$$

## Why differencing removes the unit root

For a random walk,

$$
X_t=X_{t-1}+\varepsilon_t.
$$

Subtract `X_{t-1}`:

$$
X_t-X_{t-1}=\varepsilon_t.
$$

Therefore

$$
\Delta X_t=\varepsilon_t.
$$

The level `X_t` is non-stationary, but its first difference is white noise and therefore stationary.

In lag-operator notation,

$$
(1-L)X_t=\varepsilon_t.
$$

Since

$$
\Delta=1-L,
$$

differencing removes the unit-root factor.

This is the key connection:

```text
unit root
-> non-stationary level
-> factor (1-L)
-> first difference
-> stationary transformed series
```

## Mean reversion and persistence

A useful way to distinguish the stationary and unit-root cases is to think about what happens after a shock.

### Stationary AR(1)

Suppose

$$
X_t=0.8X_{t-1}+\varepsilon_t.
$$

A shock's effect is multiplied over time by

$$
0.8,\;0.8^2,\;0.8^3,\ldots
$$

and therefore becomes smaller.

The process is mean-reverting.

### Unit-root case

If

$$
X_t=X_{t-1}+\varepsilon_t,
$$

a shock changes the level and remains embedded in future levels.

Its effect does not decay through a coefficient smaller than one.

That is why random-walk shocks are persistent.

## Deterministic trend versus stochastic trend

A deterministic trend has a predictable time path, for example

$$
X_t=\beta_0+\beta_1t+u_t,
$$

where `u_t` is stationary.

The mean changes predictably with `t`.

A stochastic trend arises from accumulated random shocks, as in the random walk.

These two cases can both look like trending data, but their economic and statistical structure is different.

This distinction matters when choosing the specification of the unit-root test.

## Trend-stationarity

A trend-stationary series can be written conceptually as

$$
X_t=\text{deterministic trend}+u_t,
$$

where `u_t` is stationary.

The level `X_t` is not weakly stationary because its mean changes with time, but deviations from the deterministic trend are stationary.

For example,

$$
X_t=2+0.5t+u_t.
$$

Then

$$
E(X_t)=2+0.5t,
$$

so the mean is not constant.

But after removing the deterministic trend,

$$
X_t-(2+0.5t)=u_t,
$$

and `u_t` is stationary.

This is different from a unit-root process, where the trend comes from accumulated stochastic shocks.

## Why the distinction matters later

When we test for a unit root, we must decide whether the stationary alternative should allow:

- stationarity around zero;
- stationarity around a non-zero constant;
- trend-stationarity around a deterministic trend.

Those are the deterministic specifications used in the ADF and KPSS material.

## Common mistakes

- A unit root is not `|z|<1`; it is a root on the unit circle, `|z|=1`.
- "No unit root" is not automatically the same as "stationary."
- A root inside the unit circle corresponds to explosive non-stationarity under the course convention.
- `I(1)` does not mean "non-stationary in general." It specifically means one ordinary difference is needed to obtain stationarity.
- Trend-stationary is not the same as weakly stationary in levels.
- A deterministic trend and a stochastic trend can look similar in a graph but have different underlying structures.
- Differencing should not be applied mechanically to an already stationary series.
- A seasonal difference is not the same as an ordinary first difference.

## Retrieval questions

1. What makes a weakly stationary process stationary?
2. What visual patterns can suggest non-stationarity?
3. How does the ACF typically differ between stationary and non-stationary data?
4. What is the first-difference operator?
5. What is a seasonal difference?
6. What does `I(0)`, `I(1)` and `I(2)` mean?
7. Why is the minimum number of differences important?
8. What is overdifferencing?
9. Why is a random walk a unit-root process?
10. Derive the AR(1) root `z=1/phi`.
11. What is the difference between `|z|>1`, `|z|=1` and `|z|<1`?
12. Why is "no unit root therefore stationary" an incorrect statement?
13. Show why differencing a random walk gives white noise.
14. What is the intuition behind permanent shocks in a unit-root process?
15. What is the difference between deterministic-trend and unit-root non-stationarity?
16. What does trend-stationary mean?

## Related notes

- [Random walk](random-walk.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [AR, MA and ARMA models](arma-models.md)
- [Unit-root testing](unit-root-testing.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 1: Non-stationarity, Unit-Roots, and Differencing.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 exercise book.
