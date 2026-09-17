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

## Week 2 map

The stationary-model material now follows this chain:

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

## Mathematical foundations

General mathematics is kept in `knowledge/mathematics/` rather than duplicated here.

For Week 2, see [Complex numbers, polynomials and roots](../../mathematics/complex-numbers-and-polynomials.md) for the background needed to work with characteristic roots and the unit circle, and [Geometric series](../../mathematics/geometric-series.md) for the series expansion used when inverting lag polynomials.

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
- the PACF and lag-order selection.

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
