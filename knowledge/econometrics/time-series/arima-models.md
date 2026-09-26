# ARIMA Models

Status: `developing`

## Central question

How can we model a time series whose level is non-stationary, but whose suitably differenced version is stationary?

Week 2 gave us ARMA models for stationary time series. Week 3 extends that framework by first differencing a non-stationary series until it becomes stationary, and then fitting an ARMA model to the transformed series.

That idea gives the Autoregressive Integrated Moving Average model:

$$
\boxed{\text{ARIMA}(p,d,q)}.
$$

The key interpretation is:

> ARIMA(p,d,q) is an ARMA(p,q) model applied to the d-times differenced series.

## Why ARIMA is needed

ARMA models require stationarity.

Many economic and financial time series are not stationary in levels. They may contain a stochastic trend, so the level wanders over time even though the changes around that level behave in a stable way.

If differencing makes the series stationary, there is no need to abandon the ARMA framework. We simply apply ARMA to the differenced process.

The Week 3 logic is therefore:

```text
non-stationary X_t
-> difference d times
-> stationary Delta^d X_t
-> model Delta^d X_t with ARMA(p,q)
-> ARIMA(p,d,q)
```

## General ARIMA model

The course writes the ARIMA model as

$$
\boxed{
\phi(L)\Delta^d X_t
=
\theta(L)\varepsilon_t
}
$$

where

$$
\phi(L)
=
1-\phi_1L-\cdots-\phi_pL^p
$$

is the autoregressive polynomial, and

$$
\theta(L)
=
1+\theta_1L+\cdots+\theta_qL^q
$$

is the moving-average polynomial.

The innovation process satisfies the usual white-noise assumptions.

Define

$$
Y_t=\Delta^dX_t.
$$

Then the ARIMA equation becomes

$$
\phi(L)Y_t
=
\theta(L)\varepsilon_t.
$$

This is just an ordinary stationary ARMA(p,q) model for `Y_t`.

## What p, d and q mean

In

$$
\text{ARIMA}(p,d,q),
$$

the three orders have different roles.

### p: autoregressive order

`p` is the number of ordinary AR lags in the stationary differenced process.

For example,

$$
p=2
$$

means the stationary process contains terms such as

$$
Y_{t-1}
\quad\text{and}\quad
Y_{t-2}.
$$

### d: order of integration

`d` is the number of ordinary differences needed to make the original series stationary.

Examples:

```text
d = 0 -> X_t is already stationary
d = 1 -> Delta X_t is stationary
d = 2 -> Delta^2 X_t is stationary
```

This is the same integration order introduced earlier in Week 3.

### q: moving-average order

`q` is the number of ordinary lagged shocks used in the stationary differenced process.

For example,

$$
q=1
$$

means the stationary process contains

$$
\varepsilon_{t-1}.
$$

## First example: ARIMA(1,1,0)

Suppose

$$
X_t\sim I(1)
$$

and the first difference follows

$$
\Delta X_t
=
0.7\Delta X_{t-1}
+
\varepsilon_t.
$$

The differenced series has one AR lag and no MA lag.

Therefore

$$
\boxed{
X_t\text{ follows ARIMA}(1,1,0).
}
$$

The important point is that the AR(1) structure is applied to

$$
\Delta X_t,
$$

not directly to the non-stationary level `X_t`.

## Second example: ARIMA(0,1,1)

Suppose

$$
\Delta X_t
=
\varepsilon_t
+
0.5\varepsilon_{t-1}.
$$

Then the first difference is MA(1), so

$$
\boxed{
X_t\text{ follows ARIMA}(0,1,1).
}
$$

Here

```text
p = 0
d = 1
q = 1
```

## Third example: ARIMA(1,2,1)

Suppose

$$
\Delta^2X_t
=
0.6\Delta^2X_{t-1}
+
\varepsilon_t
+
0.3\varepsilon_{t-1}.
$$

The second difference is ARMA(1,1).

Therefore

$$
\boxed{
X_t\text{ follows ARIMA}(1,2,1).
}
$$

This example is useful because it reinforces the interpretation:

> the AR and MA dynamics belong to the stationary transformed series.

## The meaning of "Integrated"

The `I` in ARIMA stands for **Integrated**.

In time-series terminology, an `I(d)` series is one that becomes stationary after `d` ordinary differences.

ARIMA therefore incorporates the integration order directly into the model.

For example,

$$
X_t\sim I(1)
$$

naturally leads to an ARIMA model with

$$
d=1.
$$

## First and second differencing: the slide intuition

The Week 3 slides give a useful qualitative interpretation:

```text
first differencing  -> allows the level to vary freely
second differencing -> allows the slope to vary freely
```

This should not be read as a new formal definition. It is an intuition for what successive differencing removes from the level representation.

With first differencing, the level itself is not forced to remain around one fixed mean. We model its changes.

With second differencing, even the first difference can move over time, while the change in that first difference is modeled as stationary.

## Statistical properties

After differencing, the process

$$
Y_t=\Delta^dX_t
$$

is stationary.

Therefore the Week 2 ARMA results apply to `Y_t`.

This includes:

- the usual AR stationarity condition;
- the same mean formulas for a stationary ARMA process;
- the same ACF and PACF behavior;
- the same invertibility logic for the MA polynomial;
- the same maximum-likelihood estimation framework.

Do not automatically apply stationary ARMA formulas directly to the non-stationary level `X_t`.

Apply them to

$$
\Delta^dX_t.
$$

## Stationarity condition in ARIMA

The differencing part removes the unit-root non-stationarity.

After the required differencing has been performed, the remaining AR polynomial must satisfy the same stationarity condition as in Week 2:

$$
\boxed{
\text{all roots of }\phi(z)=0\text{ must satisfy }|z|>1.
}
$$

So an ARIMA model separates two issues:

1. unit-root non-stationarity is handled through `d`;
2. the remaining AR dynamics must be stationary.

## Deterministic trends in ARIMA

The basic ARIMA construction naturally allows stochastic trends through integration and differencing.

The Week 3 slides also discuss allowing a deterministic component by including an intercept in the stationary ARMA model for the differenced series.

For a stationary ARMA(p,q) model with intercept `alpha`,

$$
\mu
=
\frac{\alpha}
{1-\sum_{i=1}^p\phi_i}.
$$

If

$$
d=1,
$$

then

$$
Y_t=\Delta X_t.
$$

If the differenced process has constant mean

$$
E(\Delta X_t)=\mu,
$$

then the level changes by `mu` on average each period.

That implies a linear deterministic trend in `X_t` with slope `mu`.

For example, if

$$
E(\Delta X_t)=2,
$$

then the expected level can move like

```text
100, 102, 104, 106, 108, ...
```

so the level has a linear trend with slope 2.

This gives an important connection:

$$
\boxed{
\text{constant mean in }\Delta X_t
\Longrightarrow
\text{linear trend in }X_t
}
$$

for the `d=1` case.

The slides note that in many applications the mean of the differenced process is assumed to be zero unless a deterministic trend is clearly justified.

## Choosing d

The integration order `d` is selected using the unit-root logic developed earlier in Week 3.

### With ADF

Start with the level.

If the unit-root null cannot be rejected, difference the series and test again.

Continue until the unit-root null is rejected.

The number of differences required is `d`.

### With KPSS

Start with the level.

If the stationarity null is rejected, difference the series and test again.

Continue until stationarity is no longer rejected.

Again, the minimum number of differences required is `d`.

The purpose is not to difference as much as possible.

The purpose is to find the **minimum** differencing order required for stationarity.

## Choosing p and q

Once `d` has been selected, define

$$
Y_t=\Delta^dX_t.
$$

Now `Y_t` is stationary, so the Week 2 model-identification rules can be applied.

The basic patterns are:

| Model for the stationary series | ACF | PACF |
| --- | --- | --- |
| AR(p) | decays or oscillates | cuts off after p |
| MA(q) | cuts off after q | decays or oscillates |
| ARMA(p,q) | generally decays | generally decays |

So:

```text
PACF cutoff -> evidence for AR order p
ACF cutoff  -> evidence for MA order q
```

## Which ACF and PACF should be inspected?

This is an important exam point.

If the original series is non-stationary and

$$
d=1,
$$

do **not** select `p` and `q` from the ACF and PACF of the original `X_t`.

Instead inspect the ACF and PACF of

$$
\boxed{\Delta X_t}.
$$

More generally, inspect

$$
\boxed{\Delta^dX_t}.
$$

The ARMA part of the ARIMA model describes the stationary transformed series.

## Complete model-selection example

Suppose:

1. the ADF test cannot reject a unit root for `X_t`;
2. the ADF test rejects a unit root for `Delta X_t`;
3. the PACF of `Delta X_t` cuts off after lag 3;
4. the ACF of `Delta X_t` decays gradually.

Then:

$$
d=1
$$

because one difference was required.

The PACF cutoff suggests

$$
p=3.
$$

The decaying ACF is consistent with an AR structure, so

$$
q=0.
$$

Therefore the candidate model is

$$
\boxed{
\text{ARIMA}(3,1,0).
}
$$

## Another model-selection example

Suppose:

1. `X_t` is `I(1)`;
2. the ACF of `Delta X_t` cuts off after lag 1;
3. the PACF of `Delta X_t` decays.

Then the stationary differenced process looks like MA(1).

Therefore

$$
\boxed{
\text{ARIMA}(0,1,1).
}
$$

## ARIMA workflow

A useful practical sequence is

```text
1. inspect X_t
2. test for unit-root / stationarity
3. determine d
4. compute Delta^d X_t
5. verify that the transformed series is stationary
6. inspect ACF and PACF of Delta^d X_t
7. choose p and q
8. estimate the unknown ARMA coefficients
9. check the fitted model later with diagnostic tools
```

The Week 3 part stops mainly at steps 1 through 8. More formal model selection and diagnostic checking come later in the course.

## Parameter estimation

Once the model order

$$
(p,d,q)
$$

has been selected, the unknown AR and MA coefficients can be estimated.

The Week 3 lecture follows the same logic as Week 2:

> use maximum likelihood to estimate the unknown parameters of the chosen model.

The order selection and parameter estimation are different tasks.

For example, deciding that the model is

$$
\text{ARIMA}(1,1,1)
$$

means the orders `p=1,d=1,q=1` have already been chosen.

Maximum likelihood then estimates numerical values for coefficients such as

$$
\phi_1,
\qquad
\theta_1,
\qquad
\sigma_\varepsilon^2.
$$

### Implementation note

The lecture states that maximum likelihood is used, but does not specify a particular numerical optimizer.

In practical software, the likelihood is usually maximized numerically: the program starts from candidate parameter values, evaluates the log-likelihood, changes the parameters, and iterates until it finds a numerical maximum.

The important course-level distinction is:

```text
maximum likelihood -> defines the objective
optimization algorithm -> numerically searches for the maximizing parameters
```

## Common mistakes

- Applying ARMA directly to a non-stationary level without first dealing with the integration order.
- Thinking `d` is an AR or MA lag order.
- Looking at the ACF/PACF of the non-stationary level to choose `p` and `q`.
- Forgetting that ARMA properties apply to `Delta^d X_t`, not automatically to the original level.
- Assuming more differencing is always safer.
- Confusing a stochastic trend handled by differencing with a deterministic trend.
- Forgetting that a constant mean in `Delta X_t` implies a linear trend in the level when `d=1`.
- Thinking maximum likelihood chooses `p,d,q`. MLE estimates coefficients after the model order has been chosen.

## Retrieval questions

1. Why can ARMA not simply be applied to every time series in levels?
2. Give the general ARIMA(p,d,q) equation.
3. What do `p`, `d`, and `q` represent?
4. Why is ARIMA(p,d,q) best thought of as ARMA(p,q) applied to `Delta^dX_t`?
5. What does the word Integrated mean in ARIMA?
6. Write an example of an ARIMA(1,1,0).
7. Write an example of an ARIMA(0,1,1).
8. If `Delta^2X_t` follows ARMA(1,1), what ARIMA model does `X_t` follow?
9. How is `d` selected?
10. Which series should be used to inspect the ACF and PACF when `d=1`?
11. How do the usual ACF/PACF rules carry over from Week 2?
12. What does an intercept in the stationary differenced process imply for the level when `d=1`?
13. What is the difference between selecting the model order and estimating the coefficients?
14. Why is maximum likelihood generally implemented numerically?

## Related notes

- [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [Unit-root testing: ADF and KPSS](unit-root-testing.md)
- [AR, MA and ARMA models](arma-models.md)
- [ACF, PACF and lag-order selection](acf-pacf-and-lag-order-selection.md)
- [Seasonal ARIMA models](seasonal-arima-models.md)
- [Week 3 review](week-3-review.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 3: Autoregressive Integrated Moving Average (ARIMA) Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 lecture: Non-Stationary Time Series Models.
