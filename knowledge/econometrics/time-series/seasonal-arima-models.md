# Seasonal ARIMA (SARIMA) Models

Status: `developing`

## Central question

How do we model a non-stationary time series when both ordinary time dependence and seasonal dependence matter?

Ordinary ARIMA captures non-seasonal dynamics such as relationships with the previous month or previous quarter.

Seasonal ARIMA, often written SARIMA, adds a second layer of dynamics at seasonal lags such as:

$$
12,24,36,\ldots
$$

for monthly data with yearly seasonality.

The Week 3 notation is

$$
\boxed{
\text{ARIMA}(p,d,q)\times(P,D,Q)_s
}
$$

where the lowercase orders describe the ordinary part of the model and the uppercase orders describe the seasonal part.

## Why seasonal ARIMA is needed

For periodic data, two different time scales can matter at the same time.

For monthly airline-passenger data, for example:

1. April may depend on March, February, and other nearby months;
2. April may also depend especially strongly on previous Aprils.

So we can have ordinary dependence along

$$
t-1,t-2,t-3,\ldots
$$

and seasonal dependence along

$$
t-12,t-24,t-36,\ldots.
$$

A seasonal ARIMA model combines both.

## The general seasonal ARIMA model

The course writes

$$
\boxed{
\phi(L)\Phi(L^s)
\Delta^d\Delta_s^D X_t
=
\theta(L)\Theta(L^s)\varepsilon_t
}
$$

with seasonal period `s`.

The pieces are:

$$
\phi(L)
$$

for the non-seasonal AR polynomial,

$$
\theta(L)
$$

for the non-seasonal MA polynomial,

$$
\Phi(L^s)
$$

for the seasonal AR polynomial,

and

$$
\Theta(L^s)
$$

for the seasonal MA polynomial.

The differencing operators are

$$
\Delta^d
$$

for ordinary differencing and

$$
\Delta_s^D
$$

for seasonal differencing.

## What the six orders mean

In

$$
\text{ARIMA}(p,d,q)\times(P,D,Q)_s,
$$

the non-seasonal part is:

```text
p = ordinary AR order
d = ordinary differencing order
q = ordinary MA order
```

and the seasonal part is:

```text
P = seasonal AR order
D = seasonal differencing order
Q = seasonal MA order
s = length of the seasonal cycle
```

For yearly seasonality:

- monthly data usually use `s=12`;
- quarterly data usually use `s=4`.

## Reading a SARIMA model

Consider

$$
\boxed{
\text{ARIMA}(1,1,0)\times(1,1,1)_{12}.
}
$$

Read it piece by piece:

```text
p = 1 -> one ordinary AR term
d = 1 -> one ordinary difference
q = 0 -> no ordinary MA term

P = 1 -> one seasonal AR term
D = 1 -> one seasonal difference
Q = 1 -> one seasonal MA term

s = 12 -> yearly seasonality in monthly data
```

The model therefore combines ordinary monthly dependence with yearly seasonal dependence.

## Ordinary differencing and seasonal differencing

The first ordinary difference is

$$
\Delta X_t
=
X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta=1-L.
$$

The seasonal difference is

$$
\Delta_sX_t
=
X_t-X_{t-s},
$$

so

$$
\Delta_s=1-L^s.
$$

For monthly data,

$$
\Delta_{12}X_t
=
X_t-X_{t-12}.
$$

If both

$$
d=1
$$

and

$$
D=1,
$$

then the transformed series is

$$
\Delta\Delta_{12}X_t.
$$

## Expanding the double difference

For monthly data,

$$
\Delta\Delta_{12}X_t
=
(1-L)(1-L^{12})X_t.
$$

Multiply the operators:

$$
(1-L-L^{12}+L^{13})X_t.
$$

Therefore

$$
\boxed{
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13}.
}
$$

The `t-13` term appears because ordinary and seasonal differencing interact:

$$
L\times L^{12}=L^{13}.
$$

This interaction-lag idea also appears when non-seasonal and seasonal AR or MA polynomials are multiplied.

## Non-seasonal AR versus seasonal AR

An ordinary AR(1) polynomial is

$$
\phi(L)=1-\phi_1L.
$$

It links the present to lag 1.

A seasonal AR(1) polynomial for monthly data is

$$
\Phi(L^{12})
=
1-\Phi_1L^{12}.
$$

It links the present to lag 12.

So:

```text
ordinary AR(1) -> t-1
seasonal AR(1) -> t-12
```

For quarterly data with `s=4`, seasonal AR(1) would use lag 4 instead.

## Non-seasonal MA versus seasonal MA

An ordinary MA(1) polynomial is

$$
\theta(L)
=
1+\theta_1L.
$$

It contains the previous-period shock

$$
\varepsilon_{t-1}.
$$

A seasonal MA(1) polynomial for monthly data is

$$
\Theta(L^{12})
=
1+\Theta_1L^{12}.
$$

It contains the shock from twelve periods earlier:

$$
\varepsilon_{t-12}.
$$

So:

```text
ordinary MA(1) -> epsilon_(t-1)
seasonal MA(1) -> epsilon_(t-12)
```

## A fully expanded numerical SARIMA example

Consider

$$
\boxed{
\text{ARIMA}(1,1,1)\times(1,1,1)_{12}
}
$$

with

$$
\phi_1=0.4,
\qquad
\Phi_1=0.6,
\qquad
\theta_1=0.3,
\qquad
\Theta_1=0.5.
$$

Define the stationary double-differenced series

$$
Y_t=\Delta\Delta_{12}X_t.
$$

The model is

$$
(1-0.4L)(1-0.6L^{12})Y_t
=
(1+0.3L)(1+0.5L^{12})\varepsilon_t.
$$

### Expand the AR side

Multiply

$$
(1-0.4L)(1-0.6L^{12}).
$$

This gives

$$
1-0.4L-0.6L^{12}+0.24L^{13}.
$$

Therefore the left-hand side is

$$
Y_t
-0.4Y_{t-1}
-0.6Y_{t-12}
+0.24Y_{t-13}.
$$

### Expand the MA side

Multiply

$$
(1+0.3L)(1+0.5L^{12}).
$$

This gives

$$
1+0.3L+0.5L^{12}+0.15L^{13}.
$$

Therefore the right-hand side is

$$
\varepsilon_t
+0.3\varepsilon_{t-1}
+0.5\varepsilon_{t-12}
+0.15\varepsilon_{t-13}.
$$

### Final stationary equation

So

$$
\boxed{
Y_t
-0.4Y_{t-1}
-0.6Y_{t-12}
+0.24Y_{t-13}
=
\varepsilon_t
+0.3\varepsilon_{t-1}
+0.5\varepsilon_{t-12}
+0.15\varepsilon_{t-13}.
}
$$

Equivalently,

$$
\boxed{
Y_t
=
0.4Y_{t-1}
+0.6Y_{t-12}
-0.24Y_{t-13}
+\varepsilon_t
+0.3\varepsilon_{t-1}
+0.5\varepsilon_{t-12}
+0.15\varepsilon_{t-13}.
}
$$

This shows exactly why lag 13 can appear even though the model orders only contain ordinary lag 1 and seasonal lag 12.

The lag-13 term is an interaction:

$$
1+12=13.
$$

## Two clocks intuition

A useful mental model is that SARIMA has two clocks running at the same time.

The ordinary clock is

$$
1,2,3,\ldots
$$

and the seasonal clock is

$$
s,2s,3s,\ldots.
$$

For monthly data:

$$
1,2,3,\ldots
$$

captures nearby-month dependence, while

$$
12,24,36,\ldots
$$

captures yearly seasonal dependence.

When these parts are multiplied, interaction lags such as

$$
13,25,37,\ldots
$$

can appear.

## Seasonal ACF and PACF patterns

The ordinary Week 2 cutoff rules carry over to the seasonal lags.

For monthly data, the seasonal lags are

$$
12,24,36,48,\ldots.
$$

### Seasonal AR(1)

Consider

$$
\text{ARIMA}(0,0,0)\times(1,0,0)_{12}.
$$

The Week 3 slides state:

- the ACF decays at the seasonal lags;
- the PACF has one significant seasonal spike at lag 12.

So conceptually:

```text
ACF:
lag 12  -> large
lag 24  -> smaller
lag 36  -> smaller again
...

PACF:
lag 12 -> significant
lag 24, 36, ... -> no seasonal cutoff spikes
```

This is exactly the ordinary AR rule moved to the seasonal timeline.

### Seasonal MA(1)

Consider

$$
\text{ARIMA}(0,0,0)\times(0,0,1)_{12}.
$$

The Week 3 slides state:

- the ACF has one significant seasonal spike at lag 12 and then cuts off;
- the PACF decays at lags 12, 24, 36, and so on.

Again, this is exactly the ordinary MA rule moved to the seasonal timeline.

## ACF/PACF memory table

| Component | ACF | PACF |
| --- | --- | --- |
| ordinary AR(1) | decays across ordinary lags | cuts off at lag 1 |
| ordinary MA(1) | cuts off at lag 1 | decays across ordinary lags |
| seasonal AR(1), s=12 | decays at 12,24,36,... | cuts off at lag 12 |
| seasonal MA(1), s=12 | cuts off at lag 12 | decays at 12,24,36,... |

For higher orders, the same logic generalizes.

For example, sharp PACF spikes at seasonal lags 12 and 24 can indicate

$$
P=2.
$$

## Why full SARIMA ACF/PACF plots can look messy

The clean cutoff rules are easiest to see in pure AR or pure MA examples.

A complete model can contain:

- ordinary AR terms;
- ordinary MA terms;
- seasonal AR terms;
- seasonal MA terms;
- ordinary differencing;
- seasonal differencing.

These pieces interact.

Therefore a full empirical ACF/PACF may not show one perfectly clean textbook pattern.

The cutoff rules are still useful clues, but they should be interpreted as part of the whole model-identification process.

## The airline model

The famous Box-Jenkins airline model used in the Week 3 lecture is

$$
\boxed{
\text{ARIMA}(0,1,1)\times(0,1,1)_{12}.
}
$$

This model has:

```text
p = 0
d = 1
q = 1

P = 0
D = 1
Q = 1

s = 12
```

So after ordinary and seasonal differencing, the model contains:

- one ordinary MA(1) term;
- one seasonal MA(1) term;
- no AR terms.

## Airline model in lag-polynomial form

Because

$$
p=P=0,
$$

we have

$$
\phi(L)=1
$$

and

$$
\Phi(L^{12})=1.
$$

The model therefore reduces to

$$
\boxed{
\Delta\Delta_{12}X_t
=
\theta(L)\Theta(L^{12})\varepsilon_t.
}
$$

With

$$
\theta(L)=1+\theta L
$$

and

$$
\Theta(L^{12})=1+\Theta L^{12},
$$

we get

$$
\Delta\Delta_{12}X_t
=
(1+\theta L)(1+\Theta L^{12})\varepsilon_t.
$$

## Expanding the airline model

The left-hand side is

$$
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13}.
$$

The right-hand side is

$$
(1+\theta L)(1+\Theta L^{12})\varepsilon_t.
$$

Expand:

$$
=
\left(
1+\theta L+\Theta L^{12}+\theta\Theta L^{13}
\right)\varepsilon_t.
$$

So

$$
\boxed{
X_t-X_{t-1}-X_{t-12}+X_{t-13}
=
\varepsilon_t
+\theta\varepsilon_{t-1}
+\Theta\varepsilon_{t-12}
+\theta\Theta\varepsilon_{t-13}.
}
$$

Again, the lag-13 shock comes from the interaction between ordinary lag 1 and seasonal lag 12.

## Why the airline model is MA(1) x seasonal MA(1)

The lecture examines the ACF/PACF of the first and seasonal differenced series,

$$
\Delta\Delta_{12}X_t.
$$

The ACF is significant around lag 1 and lag 12.

This suggests:

$$
q=1
$$

for the ordinary component, and

$$
Q=1
$$

for the seasonal component.

The resulting model is therefore

$$
\boxed{
(0,1,1)\times(0,1,1)_{12}.
}
$$

The lecture describes this as a combination of a non-seasonal MA(1) and a seasonal MA(1) after differencing.

## Maximum-likelihood estimation of the airline model

Once the model order has been chosen, the coefficients are estimated.

The Week 3 lecture reports maximum-likelihood estimates

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

Because the slide convention is

$$
\theta(L)=1+\theta L
$$

and

$$
\Theta(L^{12})=1+\Theta L^{12},
$$

the fitted polynomials become

$$
1-0.4018L
$$

and

$$
1-0.5569L^{12}.
$$

Therefore

$$
\Delta\Delta_{12}X_t
=
(1-0.4018L)(1-0.5569L^{12})\varepsilon_t.
$$

Expand:

$$
(1-0.4018L)(1-0.5569L^{12})
=
1-0.4018L-0.5569L^{12}+0.2238L^{13}.
$$

Hence

$$
\boxed{
\Delta\Delta_{12}X_t
=
\varepsilon_t
-0.4018\varepsilon_{t-1}
-0.5569\varepsilon_{t-12}
+0.2238\varepsilon_{t-13}.
}
$$

## Fitted airline model in the original level

Since

$$
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13},
$$

we obtain

$$
X_t-X_{t-1}-X_{t-12}+X_{t-13}
=
\varepsilon_t
-0.4018\varepsilon_{t-1}
-0.5569\varepsilon_{t-12}
+0.2238\varepsilon_{t-13}.
$$

Solving for `X_t`:

$$
\boxed{
X_t
=
X_{t-1}
+
X_{t-12}
-
X_{t-13}
+
\varepsilon_t
-
0.4018\varepsilon_{t-1}
-
0.5569\varepsilon_{t-12}
+
0.2238\varepsilon_{t-13}.
}
$$

This is a useful equation because it shows where every part comes from:

```text
X_(t-1), X_(t-12), X_(t-13)
-> ordinary + seasonal differencing

epsilon_t, epsilon_(t-1), epsilon_(t-12), epsilon_(t-13)
-> ordinary MA + seasonal MA + interaction
```

## Model selection versus parameter estimation

These are separate stages.

### Model selection

Choose

$$
(p,d,q)\times(P,D,Q)_s.
$$

This uses ideas such as:

- visual inspection;
- unit-root and stationarity tests;
- ordinary and seasonal differencing;
- ACF and PACF patterns.

### Parameter estimation

Once the orders are fixed, estimate numerical coefficients such as

$$
\phi_i,
\qquad
\theta_j,
\qquad
\Phi_i,
\qquad
\Theta_j,
\qquad
\sigma_\varepsilon^2.
$$

The Week 3 lecture uses maximum likelihood.

Maximum likelihood does not itself mean that the software chose the model order.

It means that, conditional on the chosen model structure, the unknown coefficients are selected to maximize the likelihood.

## Practical numerical optimization note

The lecture says that the parameters are estimated with maximum likelihood but does not name the numerical optimization algorithm.

In practical statistical software, the log-likelihood for a model such as SARIMA is usually maximized numerically.

Conceptually:

```text
start with candidate parameters
-> evaluate log-likelihood
-> adjust parameters
-> evaluate again
-> continue until a numerical optimum is reached
```

The important distinction is:

```text
maximum likelihood = the statistical objective
optimizer = the numerical method used to find the maximum
```

## Common mistakes

- Treating `P,D,Q` as duplicates of `p,d,q`. They act at seasonal lags.
- Forgetting the seasonal period `s`.
- Using lag 12 just because the data are monthly even when there is no yearly seasonality.
- Forgetting that seasonal AR(1) acts at lag `s`, not lag 1.
- Forgetting that seasonal MA(1) uses `epsilon_(t-s)`.
- Forgetting the interaction lag `1+s` when ordinary and seasonal polynomials are multiplied.
- Looking for seasonal structure only at lag 1.
- Applying the clean ACF/PACF cutoff rules mechanically to a complicated mixed model.
- Forgetting that `d` and `D` solve different kinds of non-stationarity.
- Confusing model-order selection with coefficient estimation.
- Forgetting the sign convention in the slides: `theta(L)=1+theta L`, so a negative estimated `theta` produces a minus sign in the fitted polynomial.

## Retrieval questions

1. What does each symbol in `ARIMA(p,d,q) x (P,D,Q)_s` mean?
2. Why can two different time scales matter in monthly seasonal data?
3. Write the general SARIMA lag-polynomial equation.
4. What is the difference between ordinary and seasonal differencing?
5. Expand `Delta Delta_12 X_t`.
6. Why does a lag-13 term appear?
7. What is the difference between `phi(L)` and `Phi(L^s)`?
8. What is the difference between `theta(L)` and `Theta(L^s)`?
9. What ACF/PACF pattern does a seasonal AR(1) generate at seasonal lags?
10. What ACF/PACF pattern does a seasonal MA(1) generate at seasonal lags?
11. Expand an `ARIMA(1,1,1) x (1,1,1)_12` model with given coefficients.
12. What is the airline model?
13. Why is the airline model described as ordinary MA(1) plus seasonal MA(1) after differencing?
14. What were the fitted airline-model estimates reported in the Week 3 lecture?
15. How do model selection and maximum-likelihood parameter estimation differ?

## Related notes

- [ARIMA models](arima-models.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [Higher-order and seasonal differencing](higher-order-and-seasonal-differencing.md)
- [ACF, PACF and lag-order selection](acf-pacf-and-lag-order-selection.md)
- [Week 3 review](week-3-review.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 4: Seasonal ARIMA Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 lecture: Non-Stationary Time Series Models.
