# Causality

In this course, causality means that today's value can be explained using information from today and the past, without needing shocks from the future.

That is why the slides also describe it as being future-independent.

The idea is simple: if we are describing how a real time series evolves through time, it should not need tomorrow's random shock in order to generate today's observation.

For a well-behaved stationary AR model, we can rewrite the current value as the result of the current shock plus weighted past shocks. Very old shocks may still matter, but their influence becomes smaller and smaller.

So causality is not mainly about cause-and-effect in the everyday philosophical sense. It is about the direction of time in the model.

A useful way to say it is:

> A causal time-series model builds today's value from present and past shocks, not future ones.

In the Week 2 ARMA framework, the same AR-root condition that gives stationarity also gives causality.

## One-sentence answer

Causality means that today's observation can be generated from current and past information without depending on future shocks.
