# Week 1 Exam Consolidation

Status: `reviewed 2026-10-06`

## Purpose

This page is the short exam-oriented checkpoint for Week 1 of Fundamentals of Time Series Econometrics.

The 2026 preparation exam places most weight on open-ended derivation/computation and yes/no questions that require an explanation. The goal here is therefore not just recognition. You should be able to reproduce the logic, show the calculation and explain the conclusion.

## 1. Weak stationarity

A process is weakly stationary when its unconditional first and second moments are stable over time.

The two formal conditions are

$$
E(X_t)=\mu
$$

for every `t`, and

$$
\operatorname{Cov}(X_t,X_{t-h})=\gamma(h),
$$

so the autocovariance depends only on the lag `h`, not on the calendar time `t`.

Because

$$
\gamma(0)=\operatorname{Var}(X_t),
$$

weak stationarity also implies constant variance.

Memory rule:

> same center, same spread, same dependence structure.

### Fast exam check

If one condition fails, stop. The process is non-stationary.

Example:

$$
X_t=5+0.3t+\varepsilon_t
$$

has

$$
E(X_t)=5+0.3t,
$$

which depends on `t`. No further calculation is needed to conclude non-stationarity.

## 2. Autocovariance and the ACF

For a weakly stationary process,

$$
\gamma(h)=\operatorname{Cov}(X_t,X_{t-h})
$$

and

$$
\rho(h)=\frac{\gamma(h)}{\gamma(0)}.
$$

At lag zero,

$$
\gamma(0)=\operatorname{Var}(X_t)
$$

and

$$
\rho(0)=1.
$$

### White-noise expansion method

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
\qquad
\varepsilon_t\sim WN(0,\sigma^2),
$$

we have

$$
\gamma(0)=(1+\theta^2)\sigma^2.
$$

At lag 1,

$$
X_{t-1}=\varepsilon_{t-1}+\theta\varepsilon_{t-2}.
$$

Expand the covariance and keep only pairings with the same white-noise date. The only shared shock is `\varepsilon_{t-1}`, so

$$
\gamma(1)=\theta\sigma^2.
$$

Hence,

$$
\rho(1)=\frac{\theta}{1+\theta^2}.
$$

For `h>1`, there are no shared shocks:

$$
\gamma(h)=\rho(h)=0.
$$

Practical rule:

> write both dates out, expand the covariance, then look for overlapping shocks.

### ACF fingerprints

```text
white noise -> zero theoretical ACF after lag 0
MA(q) -> ACF cuts off after lag q
AR(p) -> ACF usually decays or oscillates
random walk / unit-root behavior -> sample ACF usually stays high and decays slowly
```

For an MA(q), "cuts off after q" means all theoretical autocorrelations after lag `q` are zero. It does not require every lag from 1 through `q` to be nonzero.

## 3. White noise versus random walk

White noise

$$
\varepsilon_t\sim WN(0,\sigma^2)
$$

has zero mean, constant variance and zero autocovariance at nonzero lags. It is weakly stationary.

A random walk

$$
X_t=X_{t-1}+\varepsilon_t
$$

can be written as accumulated shocks:

$$
X_t=\varepsilon_1+\cdots+\varepsilon_t
$$

when starting from zero.

Its mean can still be zero, but

$$
\operatorname{Var}(X_t)=t\sigma^2,
$$

which depends on time.

Also,

$$
\operatorname{Cov}(X_t,X_{t-h})=(t-h)\sigma^2,
$$

which depends on `t` as well as `h`.

Therefore the random walk is non-stationary.

First differencing gives

$$
\Delta X_t=\varepsilon_t,
$$

so the first difference is stationary white noise.

## 4. Lag operator

The basic rule is

$$
LX_t=X_{t-1}.
$$

More generally,

$$
L^kX_t=X_{t-k}.
$$

Examples:

$$
L^2X_t=X_{t-2},
$$

$$
L^4X_{t+3}=X_{t-1},
$$

$$
L^{-1}X_t=X_{t+1}.
$$

## 5. First differencing

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

Since `LX_t=X_{t-1}`,

$$
\Delta X_t=(1-L)X_t.
$$

For a linear deterministic trend,

$$
X_t=\beta_0+\beta_1t+\varepsilon_t,
$$

we obtain

$$
\Delta X_t=\beta_1+\varepsilon_t-\varepsilon_{t-1}.
$$

The time trend disappears.

## 6. Second differencing

The second difference is

$$
\Delta^2X_t
=
(1-L)^2X_t
=
X_t-2X_{t-1}+X_{t-2}.
$$

For

$$
X_t=at^2,
$$

the first difference is

$$
\Delta X_t=2at-a
$$

and the second difference is

$$
\Delta^2X_t=2a.
$$

So second differencing removes a quadratic deterministic trend.

## 7. Seasonal differencing

For seasonal period `s`,

$$
\Delta_sX_t
=
X_t-X_{t-s}
=
(1-L^s)X_t.
$$

Typical examples:

```text
monthly annual seasonality -> s = 12
quarterly annual seasonality -> s = 4
```

If

$$
X_t=S_t+\varepsilon_t
$$

with

$$
S_t=S_{t-s},
$$

then

$$
\Delta_sX_t=\varepsilon_t-\varepsilon_{t-s}.
$$

The repeating seasonal component cancels.

### Trend plus seasonality

Use both operators:

$$
\Delta_s\Delta X_t.
$$

The order does not matter:

$$
\Delta_s\Delta=\Delta\Delta_s.
$$

Expanding,

$$
(1-L)(1-L^s)X_t
=
X_t-X_{t-1}-X_{t-s}+X_{t-s-1}.
$$

For quarterly data,

$$
(1-L)(1-L^4)X_t
=
X_t-X_{t-1}-X_{t-4}+X_{t-5}.
$$

## 8. Log differences and growth rates

The exact proportional growth rate is

$$
g_t=\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

The exact percentage growth rate is

$$
100g_t
=
100\frac{X_t-X_{t-1}}{X_{t-1}}.
$$

The log difference is

$$
\Delta\log X_t
=
\log X_t-\log X_{t-1}
=
\log\left(\frac{X_t}{X_{t-1}}\right).
$$

For small growth rates,

$$
\Delta\log X_t\approx g_t.
$$

Hence,

$$
100\Delta\log X_t
\approx
\text{percentage growth rate}.
$$

Example: from 200 to 210, the exact growth rate is 5%, while the log difference is approximately 4.88%.

## Common traps from the 6 October review

1. **Variance squares coefficients.**

   $$
   \operatorname{Var}(aX)=a^2\operatorname{Var}(X).
   $$

   If `a=-0.6`, then `a^2=+0.36`.

2. **Covariance can keep the sign.**

   $$
   \operatorname{Cov}(aX,bY)=ab\operatorname{Cov}(X,Y).
   $$

   A negative MA coefficient can therefore give negative lag-1 autocorrelation.

3. **Do not lose the minus sign when differencing.**

   Write

   $$
   X_t-(\text{entire }X_{t-1}\text{ expression})
   $$

   before simplifying.

4. **A seasonal component is not generally a constant.**

   `S_t=S_{t-s}` means it repeats every `s` periods. Its value can differ across seasons.

5. **Do not confuse white noise with a random walk.**

   White noise has no nonzero-lag autocorrelation. A random walk accumulates shocks and is non-stationary.

6. **Second differencing is not the same as a two-period difference.**

   $$
   \Delta^2X_t=X_t-2X_{t-1}+X_{t-2},
   $$

   while

   $$
   X_t-X_{t-2}
   $$

   is simply a two-period change.

## Retrieval test

You should be able to do these without notes:

1. State weak stationarity in words and formulas.
2. Explain why constant mean alone is not enough.
3. Derive the variance and autocovariance of a random walk.
4. For an MA(1), derive `\gamma(0)`, `\gamma(1)` and `\rho(1)`.
5. Explain why an MA ACF cuts off and an AR ACF decays.
6. Translate between `L^kX_t` and time-index notation.
7. Expand `(1-L)^2X_t`.
8. Expand `(1-L)(1-L^4)X_t`.
9. Explain why first differencing removes a linear trend.
10. Explain why second differencing removes a quadratic trend.
11. Explain why seasonal differencing removes a repeating seasonal component.
12. Compute an exact percentage growth rate and the corresponding log-growth approximation.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 3: Basic Properties of Time Series.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, part 4: Simple Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 exercise book.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, 2026 Prep Exam Solutions Manual.
