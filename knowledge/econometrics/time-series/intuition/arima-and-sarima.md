# ARIMA and Seasonal ARIMA: Intuition

This page is the low-math story for the second half of Week 3.

## Why ARIMA exists

ARMA models are for stationary time series.

But many real series are not stationary in levels.

The ARIMA idea is:

> If differencing makes the series stationary, model the differenced series with ARMA.

So ARIMA is not a completely new family unrelated to ARMA.

It is ARMA plus differencing.

## What ARIMA(p,d,q) means

Read

$$
\text{ARIMA}(p,d,q)
$$

as:

```text
p = how many AR lags are used after differencing
d = how many times the original series is differenced
q = how many MA lags are used after differencing
```

The most important sentence is:

> ARIMA(p,d,q) is an ARMA(p,q) model for the stationary series Delta^d X_t.

## Example

Suppose the level `X_t` is non-stationary but

$$
\Delta X_t
$$

is stationary.

Suppose the stationary change follows an AR(1).

Then the original level follows

$$
\text{ARIMA}(1,1,0).
$$

The AR part belongs to the **change**, not directly to the non-stationary level.

## Why the I matters

The `I` means Integrated.

An `I(1)` process needs one difference.

An `I(2)` process needs two differences.

So `d` in ARIMA is exactly the integration order we learned earlier.

## How p, d and q are chosen

Think in two stages.

First choose `d`.

Use unit-root / stationarity testing and differencing until the series is stationary.

Then choose `p` and `q`.

Look at the ACF and PACF of the **stationary differenced series**.

Do not use the non-stationary level to identify the ARMA part.

## Why seasonal ARIMA exists

Some data have more than one kind of memory.

Monthly data can depend on:

- the previous month;
- the same month last year.

So there are two clocks:

```text
ordinary clock:
1, 2, 3, ...

seasonal clock:
12, 24, 36, ...
```

Seasonal ARIMA models both at the same time.

## Reading SARIMA notation

The course writes

$$
\text{ARIMA}(p,d,q)\times(P,D,Q)_s.
$$

The lowercase part is ordinary.

The uppercase part is seasonal.

For monthly data with yearly seasonality,

$$
s=12.
$$

So a seasonal AR(1) means dependence on 12 months ago, not one month ago.

A seasonal MA(1) means using the shock from 12 months ago.

## Ordinary difference versus seasonal difference

An ordinary difference asks:

> How much did the series change since the previous period?

$$
\Delta X_t
=
X_t-X_{t-1}.
$$

A seasonal difference asks:

> How different is this period from the same season last cycle?

For monthly yearly data:

$$
\Delta_{12}X_t
=
X_t-X_{t-12}.
$$

If both are needed, use both.

## Why lag 13 appears

Suppose monthly data have an ordinary lag 1 and a seasonal lag 12.

When the two model parts are multiplied,

$$
L\times L^{12}=L^{13}.
$$

So lag 13 can appear automatically.

This does not mean we separately chose a 13th-order AR or MA process.

It is an interaction between the ordinary and seasonal parts.

## Seasonal cutoff intuition

The old Week 2 rules still work.

AR:

> ACF decays, PACF cuts off.

MA:

> ACF cuts off, PACF decays.

For seasonal structure, apply those rules at seasonal lags.

For monthly data:

```text
seasonal AR(1):
ACF decays at 12,24,36,...
PACF cuts off at 12

seasonal MA(1):
ACF cuts off at 12
PACF decays at 12,24,36,...
```

## The airline model story

The airline-passenger data have both trend and yearly seasonality.

The famous model is

$$
\text{ARIMA}(0,1,1)\times(0,1,1)_{12}.
$$

In words:

> Difference once normally, difference once seasonally, then model what remains with an ordinary MA(1) and a seasonal MA(1).

That is all the airline model is conceptually.

## What maximum likelihood does

Once the model structure is chosen, the coefficient values are still unknown.

Maximum likelihood asks:

> Which coefficient values make the observed data most plausible under the model?

For the airline model, that means estimating the ordinary MA coefficient, the seasonal MA coefficient, and the innovation variance.

The lecture reports

$$
\hat\theta=-0.4018,
$$

$$
\hat\Theta=-0.5569,
$$

and

$$
\hat\sigma_\varepsilon^2=0.0013.
$$

## Why software uses an algorithm

Maximum likelihood tells us **what** we want to maximize.

It does not usually give a simple formula that can be solved by hand for a realistic SARIMA model.

So software numerically searches over possible parameter values.

The useful distinction is:

```text
maximum likelihood:
the statistical objective

optimizer:
the numerical search procedure
```

## One complete Week 3 story

```text
The level looks non-stationary
-> inspect plot and ACF
-> test with ADF/KPSS
-> decide how much differencing is needed
-> get a stationary transformed series
-> identify ordinary AR/MA structure
-> identify seasonal structure if needed
-> specify ARIMA/SARIMA
-> estimate the coefficients with maximum likelihood
```

## Quick self-check

Can you explain in ordinary words:

1. why ARIMA is really an extension of ARMA?
2. what `d` means?
3. why the ACF/PACF should be inspected after differencing?
4. why monthly data can have both lag 1 and lag 12 dependence?
5. what `P,D,Q` mean?
6. why lag 13 can appear?
7. why seasonal AR and seasonal MA have the same cutoff logic as ordinary AR and MA?
8. what the airline model says?
9. what maximum likelihood does after the model order is chosen?
