# ADF and KPSS: Intuition

This page gives the plain-language story behind the unit-root tests.

## Why do we need a test?

A graph can look like it has a trend.

An ACF can decay slowly.

Those clues are useful, but they are not formal evidence.

ADF and KPSS give us statistical tests for the kind of non-stationarity we care about in Week 3.

## ADF asks: is there a unit root?

The ADF test starts by assuming the difficult case.

Its null hypothesis is:

> The series has a unit root.

So when the ADF p-value is small, we reject that unit-root story.

The exact stationary alternative depends on whether the test uses:

- no deterministic term;
- a constant;
- a deterministic trend.

## KPSS asks the opposite question

KPSS starts from:

> The series is stationary.

So a small KPSS p-value means we reject stationarity.

That is the opposite direction from ADF.

## The easiest memory rule

```text
ADF:
H0 = unit root
small p-value -> reject unit root

KPSS:
H0 = stationary
small p-value -> reject stationarity
```

## Why use both?

Because they begin from opposite assumptions.

If ADF rejects a unit root and KPSS does not reject stationarity, both tests point toward stationarity.

If ADF does not reject a unit root and KPSS rejects stationarity, both point toward non-stationarity.

If the tests do not line up neatly, that is a sign to look more carefully at the specification, lag choice and the data.

## Where phi-star comes from

The course starts from

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

A unit root means

$$
\phi=1.
$$

After rewriting the model in first differences, the slides define

$$
\phi^*=\phi-1.
$$

So the unit-root case becomes

$$
\phi^*=0.
$$

This is why the Dickey-Fuller / ADF test is built around testing whether `phi*` equals zero.

## None, constant and trend

These choices answer:

> What kind of stationary behavior should the alternative or null allow?

### None

The stationary process is centered around zero.

### Constant

The stationary process can be centered around a non-zero level.

### Trend

The process can be stationary around a deterministic time trend.

That last case is called trend-stationary.

## Trend-stationary does not mean flat

A trend-stationary series can keep rising through time.

What matters is that once the predictable deterministic trend is removed, the remaining fluctuations are stationary.

So "stationary around a trend" is not the same as "stationary around a constant."

## Why the ADF is augmented

The basic Dickey-Fuller idea comes from a simple AR(1) setup.

The ADF test allows extra autoregressive terms so that the test can handle richer dynamic dependence.

In practice, software can help select the lag length.

For this course, remember that an ADF specification involves:

1. deterministic terms;
2. autoregressive lag order.

## How integration order is found

Start with the level.

If the level is stationary, it is `I(0)`.

If not, difference once and test again.

If the first difference is stationary, the original series is `I(1)`.

If not, difference again.

The first point at which the transformed series becomes stationary gives the integration order.

### With ADF

```text
difference until you reject the unit-root null
```

### With KPSS

```text
difference until you do not reject the stationarity null
```

## Careful language

With ADF, a large p-value does not prove that a unit root exists.

It means:

> We cannot reject the unit-root null.

With KPSS, a large p-value does not prove stationarity.

It means:

> We do not reject the stationarity null.

## One-sentence explanations

**ADF:** a test whose null hypothesis is that the series has a unit root.

**KPSS:** a test whose null hypothesis is that the series is stationary.

**phi-star:** `phi* = phi - 1`, so the unit-root case `phi = 1` becomes `phi* = 0`.

**Trend specification:** allows a deterministic time trend in the stationary benchmark.

**Integration-order testing:** repeatedly test the level and successive differences until the transformed series is stationary.

## Quick self-check

1. What is the ADF null?
2. What is the KPSS null?
3. What does a small ADF p-value mean?
4. What does a small KPSS p-value mean?
5. Why is `phi*=0` the unit-root null?
6. What changes when you choose none, constant or trend?
7. How would you determine whether a series is `I(1)`?
