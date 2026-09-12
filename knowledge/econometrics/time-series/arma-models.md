# AR, MA and ARMA Models

Status: `developing`

This note starts Week 2: stationary time-series models.

For the mathematical background on polynomial roots, complex numbers and the unit circle, see [Complex numbers, polynomials and roots](../../mathematics/complex-numbers-and-polynomials.md).

## Why ARMA models?

ARMA models describe dynamic dependence in stationary time series.

They allow the current value of a series to depend on:

- its own past values;
- current and past random shocks.

## Autoregressive models

An autoregressive model relates the current value to past values of the same series.

The simplest case is an AR(1):

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

Here:

- `X_t` is the current value;
- `X_{t-1}` is the previous value;
- `phi` measures how strongly the previous value carries forward;
- `epsilon_t` is the new shock at time `t`.

Example:

$$
X_t=0.8X_{t-1}+\varepsilon_t.
$$

If `X_{t-1}=10` and `epsilon_t=1`, then

$$
X_t=0.8(10)+1=9.
$$

### Why AR models have long memory

The AR(1) equation contains only `X_{t-1}`, but `X_{t-1}` itself depends on earlier values and earlier shocks.

Since

$$
X_{t-1}=\phi X_{t-2}+\varepsilon_{t-1},
$$

substitution gives

$$
X_t=\phi^2X_{t-2}+\phi\varepsilon_{t-1}+\varepsilon_t.
$$

Continuing the substitution gives, when the effects decay,

$$
X_t=\varepsilon_t+\phi\varepsilon_{t-1}+\phi^2\varepsilon_{t-2}+\phi^3\varepsilon_{t-3}+\cdots.
$$

So an old shock can keep affecting the process indirectly far into the future.

This is why the AR dependency structure is called global.

If `phi = 0.8`, the effect of a unit shock evolves as

$$
1,\ 0.8,\ 0.8^2,\ 0.8^3,\ldots
$$

or

$$
1,\ 0.8,\ 0.64,\ 0.512,\ldots.
$$

## Moving-average models

A moving-average model relates the current value directly to current and past shocks.

An MA(1) is

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1}.
$$

Today therefore depends on:

- today's shock `epsilon_t`;
- yesterday's shock `epsilon_{t-1}`.

An MA(1) does not include `epsilon_{t-2}` or earlier shocks in the equation for `X_t`.

### How long does a shock survive in an MA(1)?

Suppose a shock `epsilon_t` occurs today.

It affects today's value because

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1}.
$$

One period later,

$$
X_{t+1}=\varepsilon_{t+1}+\theta\varepsilon_t,
$$

so the same shock `epsilon_t` still affects `X_{t+1}` through `theta`.

Two periods later,

$$
X_{t+2}=\varepsilon_{t+2}+\theta\varepsilon_{t+1}.
$$

Now `epsilon_t` is no longer present.

So in an MA(1), one particular shock affects exactly two observations:

```text
shock epsilon_t
→ affects X_t directly
→ affects X_{t+1} through theta
→ has no effect on X_{t+2}, X_{t+3}, ...
```

More generally, in an MA(q), a shock can affect the current observation and the next `q` observations. After that, its effect is exactly zero.

This is why the MA dependency structure is called local.

## AR versus MA

The core distinction is

```text
AR: remembers past values of the series
MA: remembers past shocks
```

AR dependence can stretch arbitrarily far into the past through repeated dependence on previous `X` values.

MA dependence is limited to the specified number of shock lags. A shock in an MA(q) disappears completely after `q` future periods.

## ARMA models

An ARMA model combines both mechanisms.

The general ARMA(p,q) model can be written as

$$
X_t
=\phi_1X_{t-1}+\cdots+\phi_pX_{t-p}
+\varepsilon_t
+\theta_1\varepsilon_{t-1}+\cdots+\theta_q\varepsilon_{t-q}.
$$

The orders mean:

$$
p=\text{number of AR lags},
$$

$$
q=\text{number of MA lags}.
$$

Examples:

- `ARMA(1,0)` is an AR(1);
- `ARMA(0,1)` is an MA(1);
- `ARMA(2,1)` contains two lags of `X` and one lag of the shock.

For example,

$$
X_t=0.7X_{t-1}-0.2X_{t-2}+\varepsilon_t+0.4\varepsilon_{t-1}
$$

is an ARMA(2,1).

## Lag-polynomial notation

Lag-polynomial notation is a compact way of writing ARMA models.

The lag operator is defined by

$$
LX_t=X_{t-1}.
$$

Applying it repeatedly gives

$$
L^2X_t=X_{t-2},
$$

and more generally

$$
L^kX_t=X_{t-k}.
$$

### AR(1)

Start with

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

Move the lagged `X` term to the left:

$$
X_t-\phi X_{t-1}=\varepsilon_t.
$$

Using `X_{t-1}=LX_t`:

$$
X_t-\phi LX_t=\varepsilon_t.
$$

Factor out `X_t`:

$$
(1-\phi L)X_t=\varepsilon_t.
$$

So the AR lag polynomial is

$$
\phi(L)=1-\phi L.
$$

### AR(2)

For

$$
X_t=\phi_1X_{t-1}+\phi_2X_{t-2}+\varepsilon_t,
$$

move the AR terms to the left:

$$
X_t-\phi_1X_{t-1}-\phi_2X_{t-2}=\varepsilon_t.
$$

Then

$$
(1-\phi_1L-\phi_2L^2)X_t=\varepsilon_t.
$$

The general AR polynomial is therefore

$$
\phi(L)=1-\phi_1L-\cdots-\phi_pL^p.
$$

### MA(1)

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
$$

use

$$
\varepsilon_{t-1}=L\varepsilon_t
$$

to get

$$
X_t=(1+\theta L)\varepsilon_t.
$$

So the MA lag polynomial is

$$
\theta(L)=1+\theta L.
$$

More generally,

$$
\theta(L)=1+\theta_1L+\cdots+\theta_qL^q.
$$

### General ARMA notation

The general ARMA(p,q) model can therefore be written as

$$
\boxed{\phi(L)X_t=\theta(L)\varepsilon_t}.
$$

This notation is important because stationarity and invertibility are studied using the roots of these lag polynomials.

### Sign rule for the AR side

Do not memorize an alternating sign pattern.

Instead, always begin with the actual model and move all `X` terms to the left.

For example,

$$
X_t=0.7X_{t-1}-0.2X_{t-2}+\varepsilon_t+0.4\varepsilon_{t-1}
$$

becomes

$$
X_t-0.7X_{t-1}+0.2X_{t-2}
=
\varepsilon_t+0.4\varepsilon_{t-1}.
$$

Hence

$$
(1-0.7L+0.2L^2)X_t
=
(1+0.4L)\varepsilon_t.
$$

The `+0.2L^2` appears because the original AR coefficient was `-0.2`, and moving that term to the left changes its sign.

A useful rule is:

```text
use the actual coefficient first
→ move all AR terms to the left
→ replace X_{t-k} by L^k X_t
→ factor out X_t
```

### Quick examples

If

$$
X_t=0.6X_{t-1}+\varepsilon_t-0.4\varepsilon_{t-1},
$$

then

$$
(1-0.6L)X_t=(1-0.4L)\varepsilon_t.
$$

If

$$
X_t=0.5X_{t-1}-0.3X_{t-2}+\varepsilon_t,
$$

then

$$
(1-0.5L+0.3L^2)X_t=\varepsilon_t.
$$

## What comes next

The next steps are:

1. use characteristic roots to determine stationarity;
2. connect AR roots to causality;
3. derive statistical properties such as the mean and ACF;
4. study invertibility of the MA part.

## What to remember

- AR models use past values of `X`.
- MA models use current and past shocks.
- ARMA models combine both.
- `p` counts AR lags and `q` counts MA lags.
- An AR model can indirectly contain the effects of very old shocks.
- In an MA(1), a shock affects `X_t` and `X_{t+1}`, then disappears completely.
- More generally, a shock in an MA(q) affects the current value and at most the next `q` values.
- `LX_t=X_{t-1}` and `L^kX_t=X_{t-k}`.
- The compact ARMA form is `phi(L)X_t = theta(L)epsilon_t`.
- On the AR side, move all `X` terms to the left before forming the lag polynomial.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, part 2: Autoregressive Moving Average (ARMA) Models.
