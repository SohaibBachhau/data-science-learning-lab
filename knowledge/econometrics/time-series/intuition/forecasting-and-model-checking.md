# Intuition: Forecasting, Impulse Responses and Model Checking

Status: developing

## Why we forecast

Imagine being asked to predict next month's unemployment rate. You cannot see next month yet, but you know the past. A forecast uses the information currently available to give a sensible answer, not a promise. Under squared-error loss, the best mathematical guess is the average future value implied by what we know now: the conditional expectation.

For a mean-reverting series, the recent observation matters strongly for the near future. Over a long horizon, its influence fades, and forecasts approach the long-run mean. For a random walk, the current level is the best no-drift forecast because shocks permanently accumulate; there is no stable level mean to return to.

## A point forecast is only half the story

Two models may both predict "10 next month." In one model, future outcomes are usually between 9 and 11. In the other, they often range between 3 and 17. Those forecasts do not communicate the same risk. A prediction interval expresses future observation uncertainty. Longer horizons generally leave room for more unknown shocks, which is why intervals often widen.

## A forecast and an impulse response answer different questions

A forecast asks: "Where do we expect to end up?" An impulse response asks: "If one extra surprise happens now, how will it change the future path?" In a stable AR model, the effect trickles away. In a moving-average model, it can disappear abruptly after a specified number of dates. In a random-walk **level**, it remains built into the series.

Think of a shock as dropping a pebble into a pond. Forecasting predicts the water level given what we know; an impulse response traces the extra ripples caused by that pebble, relative to the original water path.

## Why not choose the model that fits yesterday best?

With enough knobs, a model can copy historical quirks that will never recur. That is overfitting. Information criteria reward fit while charging a price for extra parameters. Different criteria charge different prices. But a low criterion value still does not excuse a model whose residuals contain predictable patterns.

Residuals are what the model could not explain. If they still show autocorrelation, the model may have missed time dependence. Ljung–Box tests the absence of residual autocorrelation across a group of lags. Jarque–Bera instead asks whether the residual distribution looks normal. These are distinct questions with distinct null hypotheses.

## How to tell whether the forecasts actually work

Pretend you are standing at a past date, build a model using only information available then, forecast ahead, and compare with what subsequently happened. Repeat with later starting dates. This chronological repetition is time-series cross-validation.

MAE tells you the average absolute miss. RMSE penalizes big misses more heavily. Compare the model to a simple benchmark, not just to another complicated model. The Diebold–Mariano test asks whether the average loss difference between two methods could plausibly be zero.

## Quick recall

- Conditional mean: optimal under squared loss.
- Prediction interval: uncertainty about a future observation.
- Impulse response: incremental effect of one surprise.
- AIC/BIC: fit versus model complexity.
- Ljung–Box: joint residual autocorrelation test.
- Jarque–Bera: normality test.
- Out-of-sample evaluation: the real check against historical overfitting.
- Granger causality is a separate predictive concept, not the same as causal ARMA representation.

For formulas, examples and assumptions, follow the Week 4 and Week 5 links in the [main time-series index](../README.md).
