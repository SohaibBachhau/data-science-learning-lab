# Lag Operator and Differencing

Status: `developing`

## Central question

How can lag notation and differencing be used to represent time dependence and remove certain forms of non-stationarity?

## Concise answer

The lag operator moves a variable backward in time:

$$
LX_t=X_{t-1}.
$$

First differencing compares the current value with the previous value:

$$
\Delta X_t=X_t-X_{t-1}=(1-L)X_t.
$$

Differencing can remove some deterministic and stochastic trends and may transform a non-stationary series into a stationary one.

## Lag operator

The lag or backshift operator `L` is defined by

$$
LX_t=X_{t-1}.
$$

Repeated application gives

$$
L^jX_t=X_{t-j}.
$$

Examples:

$$
L^2X_t=X_{t-2},
$$

$$
L^{12}X_t=X_{t-12}.
$$

The operator is notation for shifting the time index backward.

## Why the lag operator is useful

It lets us write time-series expressions more compactly.

For example,

$$
X_t-X_{t-1}
$$

can be written as

$$
X_t-LX_t
$$

and therefore

$$
(1-L)X_t.
$$

## First difference

The first-difference operator is

$$
\Delta X_t=X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta X_t=(1-L)X_t.
$$

The level `X_t` tells us the current value.

The first difference `\Delta X_t` tells us the change from the previous period.

## Random walk example

For a random walk,

$$
X_t=X_{t-1}+\varepsilon_t.
$$

Subtracting `X_{t-1}` gives

$$
X_t-X_{t-1}=\varepsilon_t,
$$

so

$$
\Delta X_t=\varepsilon_t.
$$

The level is non-stationary, while the first difference is white noise and stationary.

## Deterministic linear trend example

Suppose

$$
X_t=\beta_0+\beta_1 t+\varepsilon_t.
$$

Then

$$
X_{t-1}
=
\beta_0+\beta_1(t-1)+\varepsilon_{t-1}.
$$

Therefore,

$$
\Delta X_t
=
X_t-X_{t-1}
$$

becomes

$$
\Delta X_t
=
\beta_1+\varepsilon_t-\varepsilon_{t-1}.
$$

Equivalently,

$$
\Delta X_t=\beta_1+\Delta\varepsilon_t.
$$

The changing linear level is removed, leaving a constant increment plus differenced noise.

## Simple lag-operator algebra

Useful identities include:

$$
LX_t=X_{t-1},
$$

$$
L^jX_t=X_{t-j},
$$

$$
(1-L)X_t=X_t-X_{t-1},
$$

and

$$
(1-aL)X_t=X_t-aX_{t-1}.
$$

Do not treat `L` as an ordinary number. It is an operator acting on a time-indexed variable.

## Why differencing matters

Differencing changes the object we model.

Instead of modeling the level,

$$
X_t,
$$

we model the change,

$$
\Delta X_t.
$$

This can remove some forms of non-stationarity and reveal a more stable process.

The random-walk example is the clearest case:

$$
\text{non-stationary level}
\rightarrow
\text{first difference}
\rightarrow
\text{stationary white noise}.
$$

## Common mistakes

- `L` is an operator, not an ordinary scalar.
- `LX_t` means `X_{t-1}`, not `L\times X_t` in the usual numeric sense.
- The first difference is a change in level, not a percentage change.
- Differencing does not automatically make every non-stationary series stationary.
- A random walk and its first difference are different processes.

## Retrieval questions

1. What does `LX_t` mean?
2. What does `L^jX_t` mean?
3. Show why `\Delta X_t=(1-L)X_t`.
4. What is the conceptual difference between `X_t` and `\Delta X_t`?
5. Why does first differencing a random walk produce white noise?
6. Derive the first difference of a deterministic linear trend.
7. Why is lag-operator notation useful?

## Related notes

- [Random walk](random-walk.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture: Basic Properties of Time Series.
