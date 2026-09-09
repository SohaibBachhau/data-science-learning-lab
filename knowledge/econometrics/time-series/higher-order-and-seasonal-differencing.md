# Higher-Order and Seasonal Differencing

Status: `developing`

## Central question

How do higher-order and seasonal differences extend ordinary first differencing?

## Concise answer

A higher-order difference repeatedly applies the ordinary difference operator. A seasonal difference compares the current observation with the observation from the same position in the previous seasonal cycle.

## Second differences

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

The second difference is the difference of the first differences:

$$
\Delta^2X_t
=
\Delta X_t-\Delta X_{t-1}.
$$

Substituting the first differences gives

$$
\Delta^2X_t
=
(X_t-X_{t-1})-(X_{t-1}-X_{t-2}),
$$

so

$$
\Delta^2X_t
=
X_t-2X_{t-1}+X_{t-2}.
$$

Using the lag operator,

$$
\Delta^2X_t
=
(1-L)^2X_t
=
(1-2L+L^2)X_t.
$$

## Why second differencing can remove a quadratic trend

Suppose

$$
X_t=t^2.
$$

Then the first differences are

$$
3,5,7,9,\ldots
$$

which still trend upward.

The second differences are constant:

$$
2,2,2,\ldots
$$

So a quadratic deterministic trend can be removed by second differencing.

The general idea is that repeated differencing can reduce the order of a polynomial trend.

## Seasonal differencing

For a seasonal period `s`, define

$$
\Delta_sX_t
=
X_t-X_{t-s}.
$$

Using the lag operator,

$$
\Delta_sX_t
=
(1-L^s)X_t.
$$

Examples:

- monthly data often use `s=12`;
- quarterly data often use `s=4`.

Seasonal differencing compares the current observation with the same season in the previous cycle.

## Why seasonal differencing works

If a seasonal component repeats every `s` periods, then subtracting `X_{t-s}` removes that repeating component.

For example, with a pure period-4 seasonal pattern,

$$
10,15,20,25,10,15,20,25,\ldots
$$

we obtain

$$
\Delta_4X_t=0
$$

after the first four observations.

## Combining ordinary and seasonal differences

A series can contain both a non-seasonal trend and seasonality.

Then we can apply both operators:

$$
\Delta_s\Delta X_t.
$$

For monthly data,

$$
\Delta_{12}\Delta X_t
=
(1-L^{12})(1-L)X_t.
$$

Expanding gives

$$
\Delta_{12}\Delta X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13}.
$$

## Why the order does not matter

The ordinary and seasonal difference operators commute:

$$
\Delta_s\Delta
=
\Delta\Delta_s.
$$

Using lag notation,

$$
(1-L^s)(1-L)
=
1-L-L^s+L^{s+1},
$$

while

$$
(1-L)(1-L^s)
=
1-L^s-L+L^{s+1}.
$$

These are the same expression.

Therefore,

$$
\Delta_s\Delta X_t
=
\Delta\Delta_sX_t.
$$

## Common mistakes

- A second difference is not the same as a two-period difference.
- `\Delta^2X_t` means differencing twice.
- Seasonal differencing uses `X_{t-s}`, not `X_{t-1}`.
- The seasonal period must match the repeating pattern.
- More differencing is not automatically better.
- Ordinary and seasonal differencing target different forms of non-stationarity.

## Retrieval questions

1. Derive `\Delta^2X_t=X_t-2X_{t-1}+X_{t-2}`.
2. Why can second differencing remove a quadratic trend?
3. What is `\Delta_sX_t`?
4. What seasonal period would be natural for monthly data? For quarterly data?
5. Expand `\Delta_{12}\Delta X_t`.
6. Show why ordinary and seasonal differencing commute.
7. Why should differencing not be applied automatically?

## Related notes

- [Lag operator and differencing](lag-operator-and-differencing.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [Log differences, growth rates and returns](log-differences-growth-and-returns.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
