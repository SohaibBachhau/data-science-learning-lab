# Log Differences, Growth Rates and Returns

Status: `developing`

## Central question

How are ordinary growth rates, log differences and financial returns related?

## Concise answer

The ordinary percentage growth rate compares the change in a variable with its previous level. The log difference,

$$
\Delta\log X_t
=
\log X_t-\log X_{t-1},
$$

is approximately equal to the proportional growth rate when changes are small.

## Absolute change

The ordinary first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

This measures the absolute change in the variable.

It does not adjust for the original level.

## Percentage growth rate

The proportional growth rate is

$$
g_t
=
\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

Multiplying by 100 gives the percentage growth rate:

$$
100g_t
=
100\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

Equivalently,

$$
g_t
=
\frac{X_t}{X_{t-1}}-1.
$$

## Log difference

The log difference is

$$
\Delta\log X_t
=
\log X_t-\log X_{t-1}.
$$

Using the logarithm rule,

$$
\Delta\log X_t
=
\log\left(\frac{X_t}{X_{t-1}}\right).
$$

Since

$$
\frac{X_t}{X_{t-1}}=1+g_t,
$$

we obtain

$$
\Delta\log X_t
=
\log(1+g_t).
$$

For small `g_t`,

$$
\log(1+g_t)\approx g_t.
$$

Therefore,

$$
\Delta\log X_t
\approx
\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

Multiplying by 100 gives the common approximation

$$
100\Delta\log X_t
\approx
\text{percentage growth rate}.
$$

## Example

Suppose

$$
X_{t-1}=100
$$

and

$$
X_t=105.
$$

The exact percentage growth rate is

$$
100\frac{105-100}{100}=5\%.
$$

The log difference is

$$
100[\log(105)-\log(100)]
\approx 4.88\%.
$$

The two are close because the change is relatively small.

## Why the approximation is not exact

The relationship

$$
\Delta\log X_t
\approx
\frac{\Delta X_t}{X_{t-1}}
$$

is an approximation.

It becomes less accurate when the growth rate is large.

## Financial returns

If `P_t` is a price, the log return is

$$
r_t
=
\log P_t-\log P_{t-1}.
$$

This converts a price level into a relative change.

In many financial applications, price levels can be highly persistent while returns behave more like stationary series.

## GDP growth

A common time-series transformation is to express GDP growth approximately as

$$
100\Delta\log(\text{GDP}_t).
$$

This makes the quantity easier to interpret as a percentage growth rate.

## Why logs are useful more broadly

Logs also turn multiplicative relationships into additive ones:

$$
X_t=T_tS_tR_t
$$

becomes

$$
\log X_t
=
\log T_t+\log S_t+\log R_t.
$$

They can also help when the size of fluctuations grows with the level of the series.

## Common mistakes

- `\Delta X_t` is an absolute change, not a percentage growth rate.
- A log difference is not exactly equal to the ordinary growth rate.
- Multiply by 100 only when you want percentage units.
- Log differences require positive values of the original variable.
- A price level and a return are different objects.

## Retrieval questions

1. What is the difference between an absolute change and a growth rate?
2. Write the exact proportional growth rate.
3. Show why `\Delta\log X_t=\log(X_t/X_{t-1})`.
4. Why is `\Delta\log X_t\approx g_t` for small growth rates?
5. When will the approximation be less accurate?
6. What is a log return?
7. Why can log transformations help with multiplicative time-series structure?

## Related notes

- [Lag operator and differencing](lag-operator-and-differencing.md)
- [Higher-order and seasonal differencing](higher-order-and-seasonal-differencing.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
