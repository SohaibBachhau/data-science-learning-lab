# Time Series Econometrics

This directory contains permanent notes on econometric methods for data observed over time.

## Start here

For a narrative review before the formal mathematics, read [The Story of Time Series Econometrics](story.md).

For definitions you should be able to explain in ordinary words, use the [Time-Series Intuition](intuition/README.md) folder. These pages deliberately use almost no mathematics and focus on what each idea means, why it matters, and how to explain it naturally.

## Current notes

1. [Basic properties of time series](basic-properties.md)
2. [White noise and IID noise](white-noise-and-iid.md)
3. [Random walk](random-walk.md)
4. [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
5. [Lag operator and differencing](lag-operator-and-differencing.md)
6. [Higher-order and seasonal differencing](higher-order-and-seasonal-differencing.md)
7. [Log differences, growth rates and returns](log-differences-growth-and-returns.md)
8. [AR, MA and ARMA models](arma-models.md)
9. [Statistical properties of stationary ARMA models](statistical-properties.md)
10. [Invertibility of MA models](invertibility.md)
11. [Parameter estimation for stationary ARMA models](parameter-estimation.md)
12. [ACF, PACF and lag-order selection](acf-pacf-and-lag-order-selection.md)
13. [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
14. [Unit-root testing: ADF and KPSS](unit-root-testing.md)

## Week 2 map

The stationary-model material follows this chain:

```text
AR / MA / ARMA intuition
-> lag-polynomial notation
-> AR roots
-> stationarity and causality
-> MA(infinity) representation
-> statistical properties
-> mean / conditional mean / ACF / ACVF
-> MA roots
-> invertibility and identification
-> AR(infinity) representation
-> parameter estimation
-> likelihood and log-likelihood
-> ACF / PACF model identification
-> GDP-growth application
```

The main structural distinction is:

```text
AR polynomial -> stationarity and causality
MA polynomial -> invertibility
```

After a model structure has been chosen, its unknown parameters can be estimated from data. Week 2 emphasizes maximum likelihood for general ARMA models. ACF and PACF patterns then provide simple clues for choosing AR and MA lag orders.

## Week 3 map

Week 3 begins where Week 2 stops. ARMA models assume stationarity, so we now need a framework for time series whose level is not stationary.

The material covered so far follows this chain:

```text
non-stationary time series
-> inspect the time-series plot
-> inspect the ACF
-> trend / seasonality / level-dependent variability
-> ordinary differencing
-> seasonal differencing
-> order of integration I(d)
-> avoid overdifferencing
-> AR(1) unit-root case
-> random walk
-> characteristic root z = 1
-> distinguish unit-root from explosive non-stationarity
-> permanent versus decaying shock effects
-> ADF unit-root test
-> phi* = phi - 1
-> H0: phi* = 0
-> ADF deterministic specifications
-> KPSS stationarity test
-> complementary ADF / KPSS logic
-> determine integration order d
-> next: ARIMA
```

The central Week 3 distinctions so far are:

```text
all AR roots |z| > 1 -> stationary
root on unit circle |z| = 1 -> unit-root non-stationary
root inside unit circle |z| < 1 -> explosive non-stationary
```

and

```text
ADF:  H0 = unit root
KPSS: H0 = stationary
```

The course slides use the Dickey-Fuller notation

$$
\phi^*=\phi-1.
$$

For the unit-root case `phi=1`,

$$
\phi^*=0,
$$

so the Dickey-Fuller / ADF null can be written as

$$
H_0:\phi^*=0.
$$

Keep this notation when working through Week 3 problems so the notes match the lecture slides.

## Mathematical foundations

General mathematics is kept in `knowledge/mathematics/` rather than duplicated here.

For Week 2 and Week 3, see [Complex numbers, polynomials and roots](../../mathematics/complex-numbers-and-polynomials.md) for the background needed to work with characteristic roots and the unit circle, and [Geometric series](../../mathematics/geometric-series.md) for the series expansion used when inverting lag polynomials.

## Plain-language intuition

The `intuition/` folder is a second layer of notes for verbal understanding. It currently includes plain-language explanations of:

- stationarity;
- AR, MA and ARMA;
- causality;
- conditional versus unconditional quantities;
- mean reversion;
- autocovariance, autocorrelation and the ACF;
- invertibility;
- maximum likelihood;
- the PACF and lag-order selection;
- non-stationarity and unit roots;
- ADF and KPSS.

Use these pages when you want to answer a conceptual question without immediately reaching for equations. The goal is not just to know the formal rule, but to understand the problem each concept is solving.

## Scope

The time-series branch will develop around:

- stochastic processes and time-series realizations;
- mean, variance, autocovariance and autocorrelation;
- weak stationarity;
- white noise and random walks;
- deterministic and stochastic trends;
- differencing and seasonal differencing;
- log differences, growth rates and returns;
- stationary ARMA models;
- non-stationary models;
- unit roots and integration;
- ADF and KPSS testing;
- ARIMA and seasonal ARIMA models;
- forecasting and impulse responses;
- model selection and diagnostic checking;
- spurious regression and cointegration.

## Learning approach

Use the story page for orientation and recall. Use the intuition folder to practice explaining concepts in ordinary language. Use the permanent concept notes for definitions, derivations, assumptions, notation and exercises. Keep reusable mathematics under `knowledge/mathematics/` and course-specific material under `courses/`.

When learning a new topic, prefer this order:

```text
intuition and story
-> terminology
-> mathematical rule
-> worked example
-> exam-style exercise
-> mixed practice
```

## Status

`developing`
