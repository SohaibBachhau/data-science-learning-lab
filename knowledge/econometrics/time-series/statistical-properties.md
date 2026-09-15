# Statistical Properties of Stationary ARMA Models

Status: `developing`

This note covers the Week 2 statistical-properties block: unconditional and conditional means, mean reversion, variance/autocovariance rules, and ACF behavior for AR and MA models.

## Unconditional mean

For a stationary AR(1) with intercept,

$$
X_t=\alpha+\phi X_{t-1}+\varepsilon_t,
$$

stationarity implies

$$
E(X_t)=E(X_{t-1})=\mu.
$$

Because the innovation has mean zero,

$$
\mu=\alpha+\phi\mu,
$$

so

$$
\boxed{\mu=\frac{\alpha}{1-\phi}}.
$$

For a stationary ARMA(p,q),

$$
\boxed{\mu=\frac{\alpha}{1-\sum_{i=1}^p\phi_i}}.
$$

The MA coefficients do not appear because the shocks have zero mean.

## Conditional versus unconditional mean

The unconditional mean is the long-run center of the process.

The conditional mean is the expected next value given what is already known.

For the AR(1),

$$
E(X_t\mid X_{t-1})=\alpha+\phi X_{t-1}.
$$

Example:

$$
X_t=0.5+0.9X_{t-1}+\varepsilon_t.
$$

Its unconditional mean is

$$
\mu=\frac{0.5}{1-0.9}=5.
$$

If yesterday was `X_{t-1}=8`, then

$$
E(X_t\mid X_{t-1}=8)=0.5+0.9(8)=7.7.
$$

These are not contradictory: 5 is the long-run center, while 7.7 is the best prediction given an unusually high previous observation.

## Conditional variance

For a simple AR(1), once `X_{t-1}` is known, the only remaining uncertainty in `X_t` is the new innovation.

Therefore,

$$
\boxed{\operatorname{Var}(X_t\mid X_{t-1})=\sigma_\varepsilon^2}.
$$

## Mean reversion

Using the stationary mean `mu`, the AR(1) can be rewritten as

$$
X_t-\mu=\phi(X_{t-1}-\mu)+\varepsilon_t.
$$

Ignoring the new shock for a moment, a deviation from the mean is multiplied by `phi` each period.

If `|phi|<1`, deviations shrink over time. This is mean reversion.

For example, with `phi=0.8`, a deviation of 10 would evolve approximately as

$$
10,\ 8,\ 6.4,\ 5.12,\ldots
$$

in the absence of new shocks.

## Variance and covariance rules used repeatedly

Three rules are especially important:

$$
\gamma(0)=\operatorname{Var}(X_t),
$$

$$
\operatorname{Var}(cX)=c^2\operatorname{Var}(X),
$$

and

$$
\operatorname{Var}(X+Y)
=
\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y).
$$

Covariance is linear:

$$
\operatorname{Cov}(aX+bY,Z)
=
a\operatorname{Cov}(X,Z)+b\operatorname{Cov}(Y,Z).
$$

A useful working rule is to expand covariance expressions like brackets, then use the fact that white-noise shocks at different dates are uncorrelated.

## AR(1) autocovariance and ACF

For

$$
X_t=\phi X_{t-1}+\varepsilon_t,
$$

we get

$$
\gamma(1)=\phi\gamma(0).
$$

More generally,

$$
\boxed{\gamma(h)=\phi^h\gamma(0)}
$$

and therefore

$$
\boxed{\rho(h)=\phi^h}.
$$

The stationary variance is

$$
\boxed{\gamma(0)=\frac{\sigma_\varepsilon^2}{1-\phi^2}}.
$$

If `phi>0`, the ACF decays gradually toward zero.

If `phi<0`, the ACF alternates sign while its magnitude shrinks.

## MA(1) autocovariance and ACF

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
$$

we have

$$
\boxed{\gamma(0)=(1+\theta^2)\sigma_\varepsilon^2},
$$

$$
\boxed{\gamma(1)=\theta\sigma_\varepsilon^2},
$$

and

$$
\boxed{\gamma(h)=0\quad\text{for }h>1}.
$$

Hence

$$
\boxed{\rho(1)=\frac{\theta}{1+\theta^2}}
$$

and the ACF is zero after lag 1.

This is the key MA pattern: the ACF cuts off after the MA order.

## MA(2) example

For

$$
X_t=\varepsilon_t+0.8\varepsilon_{t-2},
\qquad \varepsilon_t\sim WN(0,1),
$$

we get

$$
\gamma(0)=1+0.8^2=1.64.
$$

At lag 1, `X_t` and `X_{t-1}` share no common shock, so

$$
\gamma(1)=0.
$$

At lag 2, both contain `epsilon_{t-2}`, so

$$
\gamma(2)=0.8.
$$

Therefore,

$$
\rho(1)=0,
$$

$$
\rho(2)=\frac{0.8}{1.64}\approx0.488,
$$

and all autocorrelations after lag 2 are zero.

A useful practical trick is to write the shock dates appearing in `X_t` and `X_{t-h}` side by side. Only shocks with the same date can survive the covariance calculation.

## AR(2) ACF recursion

For a stationary AR(2),

$$
X_t=\phi_1X_{t-1}+\phi_2X_{t-2}+\varepsilon_t,
$$

the ACF follows the recursion

$$
\boxed{\rho(h)=\phi_1\rho(h-1)+\phi_2\rho(h-2)}.
$$

For

$$
X_t=X_{t-1}-0.5X_{t-2}+\varepsilon_t,
$$

this becomes

$$
\rho(h)=\rho(h-1)-0.5\rho(h-2).
$$

The first autocorrelation is

$$
\rho(1)=\frac{2}{3}.
$$

Then

$$
\rho(2)=\frac16,
$$

$$
\rho(3)=-\frac16,
$$

$$
\rho(4)=-\frac14,
$$

$$
\rho(5)=-\frac16.
$$

This illustrates an oscillating ACF: the autocorrelations can cross zero and move between positive and negative values while their overall magnitude dies out.

## Conditional probability from an AR model

If the past observations are known, the AR equation gives the conditional mean. If a conditional distribution is supplied, this can be used to calculate probabilities for the next observation.

In the Week 2 GDP-growth example,

$$
X_t=0.008+0.92X_{t-1}-0.14X_{t-3}+\varepsilon_t.
$$

With the supplied past values, the conditional mean is approximately

$$
0.0164.
$$

The important interpretation is that probability statements about `X_t` are centered on this conditional mean, not simply on yesterday's observed growth rate.

## ACF patterns to remember

- AR(1): ACF decays geometrically as `phi^h`.
- AR(p): ACF generally decays or oscillates rather than cutting off suddenly.
- MA(q): ACF cuts off after lag `q`.
- An MA(q) does not need every lag from 1 through `q` to have nonzero autocorrelation. It only guarantees zero autocorrelation after `q`.

## What comes next

The next Week 2 topic is invertibility of the MA polynomial.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, Statistical Properties.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 exercise book, exercises on AR(2) autocorrelation, ARMA means, MA(2) ACF and conditional probabilities.
