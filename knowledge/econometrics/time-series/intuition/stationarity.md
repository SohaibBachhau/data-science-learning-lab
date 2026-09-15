# Stationarity

Stationarity means that the basic statistical behavior of a time series is stable over time.

In plain language, the series may move up and down, but it does not completely change its personality as time passes.

If a process is stationary, its typical level stays stable, its amount of variation stays stable, and the relationship between observations depends on how far apart they are rather than on the specific calendar date.

A stationary series does **not** have to be flat. It can fluctuate a lot. It can also be strongly autocorrelated. The key point is that the rules generating those fluctuations stay stable.

A useful way to say it is:

> A stationary time series behaves according to the same statistical rules throughout time.

Why do we care? Because if the process keeps changing its basic behavior, old observations may tell us little about what happens later. Stationarity makes past data much more informative about the same underlying process.

A random walk is a standard example of non-stationarity because shocks accumulate permanently and the uncertainty grows over time.

## One-sentence answer

Stationarity means that a time series can move around, but its underlying statistical behavior remains stable over time.
