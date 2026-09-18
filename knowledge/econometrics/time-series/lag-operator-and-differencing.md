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

The first difference `Delta X_t` tells us the change from the previous period.

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

In lag notation,

$$
(1-L)X_t=\varepsilon_t.
$$

This shows directly that the first-difference operator removes the `(1-L)` unit-root factor in the random-walk case.

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

## Seasonal difference

For a seasonal period `s`, the seasonal difference is

$$
\Delta_sX_t=X_t-X_{t-s}.
$$

Using the lag operator,

$$
\Delta_sX_t=(1-L^s)X_t.
$$

For monthly data with yearly seasonality,

$$
\Delta_{12}X_t=X_t-X_{t-12}.
$$

This compares an observation with the same season one full seasonal cycle earlier.

## Combining ordinary and seasonal differencing

If both trend and seasonality are present, the course uses

$$
\Delta_s\Delta X_t.
$$

The order of the two difference operators does not matter:

$$
\Delta_s\Delta X_t
=
\Delta\Delta_sX_t.
$$

For monthly data this can be written as

$$
\Delta_{12}\Delta X_t.
$$

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

$$
(1-L^s)X_t=X_t-X_{t-s},
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

## Order of integration

Week 3 formalizes the amount of differencing needed using the order of integration.

A time series is `I(d)` when `d` is the minimum number of ordinary differences required to obtain a stationary series.

### I(0)

The level is already stationary:

$$
X_t\sim I(0).
$$

### I(1)

The level is non-stationary but the first difference is stationary:

$$
X_t\sim I(1)
\quad\Longrightarrow\quad
\Delta X_t\sim I(0).
$$

### I(2)

Two ordinary differences are required:

$$
X_t\sim I(2)
\quad\Longrightarrow\quad
\Delta^2X_t\sim I(0).
$$

The word **minimum** matters. A stationary `I(0)` series does not become `I(1)` just because someone chooses to difference it once.

## Overdifferencing

Differencing more than necessary is called overdifferencing.

The Week 3 slides warn that differencing a series that is already stationary can:

- introduce unnecessary dependence;
- introduce moving-average structure into the errors;
- make estimation less efficient.

So the rule is not:

> keep differencing until the graph looks very smooth.

Instead:

> use the smallest number of differences required to obtain stationarity.

## Differencing and unit roots

The random walk connects differencing to unit roots.

Start with

$$
X_t=X_{t-1}+\varepsilon_t.
$$

In lag-polynomial form,

$$
(1-L)X_t=\varepsilon_t.
$$

The factor `(1-L)` corresponds to a unit root at `z=1`.

Applying the first-difference operator gives

$$
\Delta X_t=\varepsilon_t,
$$

which is stationary white noise.

This is why differencing is the natural transformation for an `I(1)` unit-root process.

## First difference versus growth rate

Do not confuse a first difference with a percentage growth rate.

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

A percentage growth rate is

$$
100\times\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

The course also relates growth rates to log differences in a separate note.

## Common mistakes

- `L` is an operator, not an ordinary scalar.
- `LX_t` means `X_{t-1}`, not `L times X_t` in the usual numeric sense.
- The first difference is a change in level, not a percentage change.
- Differencing does not automatically make every non-stationary series stationary.
- A random walk and its first difference are different processes.
- Ordinary and seasonal differencing solve different problems.
- `I(d)` refers to the minimum number of ordinary differences required.
- Do not difference a stationary series just to be safe.
- Overdifferencing can introduce unnecessary dependence and moving-average structure.
- A trend-stationary process and a unit-root process are not the same kind of non-stationarity.

## Retrieval questions

1. What does `LX_t` mean?
2. What does `L^jX_t` mean?
3. Show why `Delta X_t=(1-L)X_t`.
4. What is the conceptual difference between `X_t` and `Delta X_t`?
5. Why does first differencing a random walk produce white noise?
6. Derive the first difference of a deterministic linear trend.
7. What is a seasonal difference?
8. Why can ordinary and seasonal differencing be combined?
9. What does `I(0)`, `I(1)` and `I(2)` mean?
10. Why is the word minimum important in the definition of `I(d)`?
11. What is overdifferencing and why can it be harmful?
12. How is the factor `(1-L)` connected to a unit root?
13. What is the difference between a first difference and a growth rate?
14. Why is lag-operator notation useful?

## Related notes

- [Random walk](random-walk.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [Higher-order and seasonal differencing](higher-order-and-seasonal-differencing.md)
- [Log differences, growth rates and returns](log-differences-growth-and-returns.md)
- [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [Unit-root testing](unit-root-testing.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 1: Non-stationarity, Unit-Roots, and Differencing.
