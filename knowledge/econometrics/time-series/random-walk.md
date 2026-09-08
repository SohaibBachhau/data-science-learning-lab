# Random Walk

Status: `developing`

## Central question

Why is a random walk non-stationary, and how does it differ from white noise?

## Concise answer

A random walk accumulates shocks:

$$
X_t=X_{t-1}+\varepsilon_t.
$$

Because past shocks remain embedded in the level of the series, its variance grows with time and its autocovariance depends on calendar time as well as the lag. Therefore it is not weakly stationary.

## Definition

Let

$$
\varepsilon_t \sim WN(0,\sigma_\varepsilon^2).
$$

A random walk can be written recursively as

$$
X_t=X_{t-1}+\varepsilon_t.
$$

Starting from zero, this is equivalent to

$$
X_t=\varepsilon_1+\varepsilon_2+\cdots+\varepsilon_t.
$$

The process therefore accumulates all past shocks.

## Intuition

White noise is the sequence of shocks.

A random walk is the accumulated total of those shocks.

A shock today changes the level today and is carried forward into future levels. This produces a stochastic trend.

## Mean

Because each shock has mean zero,

$$
E(X_t)
=
E(\varepsilon_1+\cdots+\varepsilon_t)
=
0.
$$

So the random walk satisfies the constant-mean condition.

## Variance

Because the white-noise shocks are uncorrelated,

$$
\operatorname{Var}(X_t)
=
\sum_{i=1}^t \operatorname{Var}(\varepsilon_i).
$$

Hence,

$$
\operatorname{Var}(X_t)
=
t\sigma_\varepsilon^2.
$$

The variance grows with `t`, so it is not constant.

This already violates weak stationarity.

## Autocovariance

For `h>0`,

$$
X_t
=
\varepsilon_1+\cdots+\varepsilon_{t-h}
+
\varepsilon_{t-h+1}+\cdots+\varepsilon_t,
$$

while

$$
X_{t-h}
=
\varepsilon_1+\cdots+\varepsilon_{t-h}.
$$

The two variables share the first `t-h` shocks.

Therefore,

$$
\operatorname{Cov}(X_t,X_{t-h})
=
(t-h)\sigma_\varepsilon^2.
$$

This depends on `t`, not only on the lag `h`.

So the random walk also violates the autocovariance condition for weak stationarity.

## Why it is non-stationary

Weak stationarity requires:

$$
\operatorname{Var}(X_t)=\gamma(0)
$$

to be constant and

$$
\operatorname{Cov}(X_t,X_{t-h})=\gamma(h)
$$

to depend only on `h`.

For a random walk:

$$
\operatorname{Var}(X_t)=t\sigma_\varepsilon^2
$$

and

$$
\operatorname{Cov}(X_t,X_{t-h})=(t-h)\sigma_\varepsilon^2.
$$

Both reveal time dependence.

## Conditional mean and variance

From

$$
X_t=X_{t-1}+\varepsilon_t,
$$

the conditional mean is

$$
E(X_t\mid X_{t-1})
=
X_{t-1},
$$

because the new shock has mean zero.

Thus the best one-step-ahead conditional mean forecast is the current level.

The conditional variance is

$$
\operatorname{Var}(X_t\mid X_{t-1})
=
\sigma_\varepsilon^2.
$$

This differs from the unconditional variance,

$$
\operatorname{Var}(X_t)=t\sigma_\varepsilon^2.
$$

Once the current level is known, the only new uncertainty for the next period is the new shock.

## First differencing

Subtract `X_{t-1}` from both sides:

$$
X_t-X_{t-1}=\varepsilon_t.
$$

Using the first-difference notation,

$$
\Delta X_t=\varepsilon_t.
$$

Therefore the random walk itself is non-stationary, while its first difference is white noise and is stationary.

This is the first major example of transforming a non-stationary time series into a stationary one.

## Common mistakes

- A constant mean does not by itself imply stationarity.
- The variance of a random walk is not constant.
- Random-walk shocks are temporary as shocks but permanent in their effect on the level.
- The random walk is not white noise; its first difference is white noise.
- The autocovariance depends on both the lag and the time index.

## Retrieval questions

1. What is the recursive definition of a random walk?
2. Why can a random walk be described as accumulated shocks?
3. Derive `E(X_t)`.
4. Derive `Var(X_t)`.
5. Why does the variance prove non-stationarity?
6. Why is `Cov(X_t,X_{t-h})=(t-h)\sigma^2`?
7. Why does that covariance violate weak stationarity?
8. What are `E(X_t\mid X_{t-1})` and `Var(X_t\mid X_{t-1})`?
9. Why does first differencing a random walk produce white noise?

## Related notes

- [White Noise and IID Noise](white-noise-and-iid.md)
- [Basic properties of time series](basic-properties.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 4: Simple Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
