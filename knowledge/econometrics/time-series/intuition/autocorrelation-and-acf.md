# Autocovariance, Autocorrelation and the ACF

Autocovariance and autocorrelation both describe how a time series is related to its own past.

Autocovariance asks whether values that are a certain number of periods apart tend to move together. Its size depends on the scale of the series, so it can be harder to interpret directly.

Autocorrelation expresses the same idea on a standardized scale. It tells us how strongly today's value is related to a value one period ago, two periods ago, three periods ago, and so on.

The ACF, or autocorrelation function, simply collects those autocorrelations across many lags.

A useful way to think about it is:

> The ACF is the memory pattern of the time series.

Different models leave different fingerprints in the ACF.

For an AR model, the ACF usually fades gradually or oscillates around zero. The effect of the past can continue for many lags.

For an MA model, the ACF cuts off after a fixed number of lags. An MA(1) can have autocorrelation at lag 1, but after that the theoretical autocorrelation is zero. An MA(2) can have autocorrelation up to lag 2, but after lag 2 it is zero.

An MA(2) does not have to have nonzero autocorrelation at both lag 1 and lag 2. The key statement is only that nothing survives after lag 2.

Oscillation means that the autocorrelations can move from positive to negative and back again while generally becoming smaller in magnitude.

## One-sentence answers

**Autocorrelation:** how strongly a time series is related to its own past at a given lag.

**ACF:** the pattern of autocorrelation across many lags.

**Oscillating ACF:** an ACF that moves above and below zero while its overall size tends to die out.
