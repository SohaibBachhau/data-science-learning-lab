# ACF, PACF and Lag-Order Selection

Status: `developing`

After specifying the general ARMA framework and learning how parameters can be estimated, the next practical question is:

> How many AR lags and MA lags should the model contain?

In ARMA$(p,q)$ terminology, we need to choose $p$ and $q$.

Week 2 introduces the autocorrelation function (ACF) and partial autocorrelation function (PACF) as simple tools for suggesting those lag orders. More formal model-selection methods are treated later in the course.

## ACF recap

The ACF at lag $h$ measures the overall linear relationship between $X_t$ and $X_{t-h}$.

It does not distinguish between a direct relationship and a relationship that operates indirectly through intermediate observations.

For example, $X_t$ and $X_{t-2}$ may be correlated because $X_{t-2}$ directly helps explain $X_t$, or simply because

```text
X_{t-2} -> X_{t-1} -> X_t.
```

The ACF captures the total relationship.

## What the PACF measures

The PACF at lag $h$ measures the direct linear relationship between $X_t$ and $X_{t-h}$ after controlling for the observations at the intermediate lags.

For lag 2, the PACF asks:

> After accounting for $X_{t-1}$, is there still a direct relationship between $X_t$ and $X_{t-2}$?

This is why the PACF is especially useful for recognizing autoregressive order.

## AR(1) intuition

Consider

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

The ACF does not stop at lag 1. In a stationary AR(1),

$$
\rho(h)=\phi^h,
$$

so correlations can remain at lag 2, lag 3, and beyond.

But those later relationships are inherited through the chain of lag-1 dependence. Once $X_{t-1}$ is controlled for, there is no additional direct AR relationship between $X_t$ and $X_{t-2}$.

Therefore, for an AR(1):

- the ACF decays gradually;
- the PACF has a significant lag 1 and then cuts off.

## AR(p) pattern

For an AR$(p)$ process, the PACF cuts off after lag $p$.

The ACF generally decays exponentially or oscillates rather than becoming exactly zero after a fixed lag.

So if the PACF is significant at lags 1 and 2 and then becomes negligible, while the ACF gradually tails off, that suggests an AR(2).

## MA(q) pattern

For an MA$(q)$ process, the ACF cuts off after lag $q$.

This follows from the finite memory of an MA process. Once two observations are separated by more than $q$ periods, they do not share any of the same finite set of shocks, so the theoretical autocorrelation is zero.

The PACF of an MA process generally decays exponentially or oscillates rather than cutting off sharply.

So if the ACF is significant through lag 3 and then cuts off, while the PACF gradually tails off, that suggests an MA(3).

Remember that "cuts off after lag $q$" does not mean every lag from 1 through $q$ must be nonzero. For example, the MA(2)

$$
X_t=\varepsilon_t+0.8\varepsilon_{t-2}
$$

has zero autocorrelation at lag 1, a nonzero autocorrelation at lag 2, and zero autocorrelation after lag 2.

## ARMA(p,q) pattern

For a mixed ARMA$(p,q)$ model, both the ACF and PACF generally decay or oscillate.

There is usually no simple sharp cutoff that directly reveals both $p$ and $q$.

So the Week 2 pattern is:

| Model | ACF | PACF |
| --- | --- | --- |
| AR$(p)$ | decays / oscillates | cuts off after $p$ |
| MA$(q)$ | cuts off after $q$ | decays / oscillates |
| ARMA$(p,q)$ | decays / oscillates | decays / oscillates |

A useful memory rule is:

```text
ACF -> especially useful for MA order q
PACF -> especially useful for AR order p
```

## What "decay" means

Decay means that the correlations become smaller in magnitude as the lag increases.

For a positive AR(1) with $\phi=0.8$, the ACF is

$$
1,\ 0.8,\ 0.64,\ 0.512,\ldots
$$

which gradually approaches zero.

## What "oscillate" means

Oscillation means that the correlations can move above and below zero while their overall magnitude gradually dies out.

For the AR(2)

$$
X_t-X_{t-1}+0.5X_{t-2}=\varepsilon_t,
$$

we obtained approximately

$$
\rho(0)=1,
\quad
\rho(1)=0.667,
\quad
\rho(2)=0.167,
\quad
\rho(3)=-0.167,
\quad
\rho(4)=-0.25,
\quad
\rho(5)=-0.167.
$$

The ACF crosses zero and moves around it rather than declining smoothly from one side. That is what oscillation means in this context.

## GDP-growth example from the lecture

The Week 2 lecture applies the ACF/PACF idea to GDP growth.

The PACF cuts off after the second lag, so the lecture suggests two autoregressive lags. The selected model is therefore

$$
\text{ARMA}(2,0),
$$

which is simply an AR(2).

After choosing the lag order, the parameters are estimated by maximum likelihood.

This gives the practical sequence:

```text
inspect the series
-> inspect ACF and PACF
-> suggest p and q
-> specify ARMA(p,q)
-> estimate parameters
```

## Sample versus theoretical patterns

The cutoff rules are theoretical model patterns. In real samples, estimated autocorrelations do not usually become exactly zero. Sampling noise means small bars can appear even at lags where the theoretical value is zero.

In practice, a correlogram uses significance bands to help judge which sample autocorrelations are meaningfully different from zero.

For Week 2, the main task is to recognize the theoretical patterns and use them as simple model-identification clues.

## Quick examples

### Example 1

PACF: significant lags 1 and 2, then cutoff.

ACF: gradual decay.

Suggested model:

$$
\boxed{AR(2)}.
$$

### Example 2

ACF: significant through lag 3, then cutoff.

PACF: gradual decay.

Suggested model:

$$
\boxed{MA(3)}.
$$

### Example 3

ACF: gradual decay.

PACF: gradual decay.

Suggested model type:

$$
\boxed{ARMA(p,q)}.
$$

The exact $p$ and $q$ are not generally readable from one sharp cutoff in this case, so further model-selection work is needed.

## What to remember

- ACF measures the overall correlation between observations separated by a lag.
- PACF measures the direct relationship after controlling for intermediate lags.
- AR$(p)$: PACF cuts off after $p$, ACF tails off.
- MA$(q)$: ACF cuts off after $q$, PACF tails off.
- ARMA$(p,q)$: both generally tail off.
- ACF is especially useful for suggesting $q$.
- PACF is especially useful for suggesting $p$.
- "Oscillate" means correlations can alternate around zero while gradually dying out.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 lecture: Lag Order Selection and GDP Growth application.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, part 4: Statistical Properties of ARMA Models.
