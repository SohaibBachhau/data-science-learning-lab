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

An MA(1) does not directly include `epsilon_{t-2}` or earlier shocks.

That means the direct memory of the shock is limited.

This is why the MA dependency structure is called local.

More generally, an MA(q) contains shocks up to `q` periods back.

## AR versus MA

The core distinction is

```text
AR: remembers past values of the series
MA: remembers past shocks
```

AR dependence can stretch arbitrarily far into the past through repeated dependence on previous `X` values.

MA dependence is directly limited to the specified number of shock lags.

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

## What comes next

The next steps are:

1. write ARMA models using lag-polynomial notation;
2. use characteristic roots to determine stationarity;
3. derive statistical properties such as the mean and ACF;
4. study invertibility of the MA part.

## What to remember

- AR models use past values of `X`.
- MA models use current and past shocks.
- ARMA models combine both.
- `p` counts AR lags and `q` counts MA lags.
- An AR model can indirectly contain the effects of very old shocks.
- An MA(q) has direct shock dependence only up to `q` periods back.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, part 2: Autoregressive Moving Average (ARMA) Models.
