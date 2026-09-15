# Time Series Econometrics

This directory contains permanent notes on econometric methods for data observed over time.

## Start here

For a quick narrative review before the formal mathematics, read [The Story of Time Series Econometrics](story.md).

For definitions you should be able to explain in ordinary words, use the [Time-Series Intuition](intuition/README.md) folder. These pages deliberately use almost no mathematics and focus on explaining what each term means and why it matters.

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
- autocovariance, autocorrelation and the ACF.

Use these pages when you want to answer a conceptual question without immediately reaching for equations.

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

Use the story page for orientation and recall. Use the intuition folder to practice explaining concepts in ordinary language. Use the permanent concept notes for definitions, derivations, assumptions and exercises. Keep course-specific material under `courses/`.

## Status

`developing`
