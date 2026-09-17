# PACF and Lag-Order Selection

## What the PACF is trying to measure

The PACF asks whether an older observation still has a direct relationship with today's observation once the observations in between have already been accounted for.

Suppose today's value is related to the value two periods ago. That relationship may be genuinely direct, or it may simply exist because the value two periods ago affected yesterday, and yesterday affected today.

The ordinary ACF sees both kinds of relationships together.

The PACF tries to remove the indirect path through the intermediate lags and isolate what remains directly at that lag.

## Example with an AR(1)

In an AR(1), today's value depends directly on yesterday's value.

Because yesterday depended on the day before, and that day depended on the one before that, today's value can still be correlated with observations from several periods ago.

That is why the ACF of an AR(1) can continue for many lags.

But once yesterday's value is controlled for, the observation from two periods ago no longer adds a separate direct AR relationship.

That is why the PACF of an AR(1) cuts off after lag 1.

## Why PACF helps identify AR order

If a model has two direct autoregressive lags, then the PACF can remain important through lag 2 and then cut off.

So a simple interpretation is:

> The last clearly important PACF lag gives a clue about how many direct AR lags the model needs.

That is why a PACF that is significant at lags 1 and 2 and then becomes negligible suggests an AR(2).

## Why ACF helps identify MA order

An MA model has finite shock memory.

For an MA(3), a shock can influence the current observation and up to three subsequent observations. Beyond that range, observations no longer share that shock directly.

That is why the theoretical ACF cuts off after lag 3.

So the ACF is especially useful for recognizing MA order.

## The main pattern

A useful memory rule is:

```text
PACF cutoff -> think AR order
ACF cutoff  -> think MA order
```

For a mixed ARMA model, neither function usually gives a clean cutoff. Both tend to tail off gradually or oscillate, so the exact AR and MA orders require more model-selection work.

## What "cut off" means

A cutoff means that after a certain lag the theoretical correlations are zero.

In real sample data, the estimated bars will almost never become perfectly zero because of sampling noise. So in practice, we look for bars that become statistically insignificant rather than literally equal to zero.

## What "decay" means

Decay means the correlations become smaller in magnitude as the lag increases.

A simple example is a sequence like:

```text
0.8, 0.64, 0.51, 0.41, ...
```

The dependence is still present at later lags, but it gradually weakens.

## What "oscillate" means

Oscillation means the correlation can move from positive to negative and back again while its overall magnitude dies out.

So a sequence might look roughly like:

```text
positive -> smaller positive -> negative -> negative -> smaller negative -> positive ...
```

The important idea is that it waves around zero instead of approaching zero smoothly from only one side.

## A good verbal answer for PACF

If someone asks, "What is the PACF?", a good answer is:

> The PACF measures the direct relationship between observations a certain number of periods apart after removing the linear influence of the observations in between.

If someone asks, "Why is PACF useful?", a good answer is:

> It helps identify AR order because an AR model has a finite number of direct autoregressive lags, even though its ordinary autocorrelation can persist much further into the past.
