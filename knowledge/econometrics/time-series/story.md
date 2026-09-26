# The Story of Time Series Econometrics

Status: `developing`

This page is the low-friction narrative for time series. It grows with the course. The goal is to make it easy to remember what each topic is for before opening the detailed mathematics.

## The story so far

A time series is a sequence of observations recorded through time, such as daily stock prices, monthly unemployment or quarterly GDP growth.

The important difference from ordinary cross-sectional data is that order matters. Today's observation may be related to yesterday's observation, and that relationship can itself contain useful information.

We model the observed sequence as one realization of an underlying stochastic process.

Each `X_t` is a random variable. The number we actually observe at time `t` is written `x_t`.

Once we think of the data as coming from a stochastic process, we want to describe its basic behavior.

The mean tells us the expected level of the process.

The variance tells us how much it fluctuates around that level.

Autocovariance asks whether observations of the same process at different times tend to move together.

The lag `h` simply tells us how far apart the two observations are.

Stationarity then gives us a form of stability. For a weakly stationary process, the mean and variance do not change over time, and the covariance between observations depends only on how far apart they are, not on the specific calendar date.

This matters because we normally observe only one historical path. If the basic statistical relationship changed arbitrarily at every date, old observations would tell us much less about the same underlying process.

Autocorrelation takes the autocovariance and puts it on a standardized scale between -1 and 1:

$$
\rho(h)=\frac{\gamma(h)}{\gamma(0)}.
$$

The important idea is simpler than the formula:

> How strongly are observations `h` periods apart related?

The autocorrelation function, or ACF, collects that relationship across many lags.

A correlogram is simply a plot of the estimated sample autocorrelations across those lags.

## White noise: the benchmark shock process

White noise is the simplest stationary benchmark.

It has zero mean, constant variance and zero autocovariance at every nonzero lag. In other words, past shocks do not have a linear relationship with current shocks.

Its theoretical ACF is therefore 1 at lag 0 and 0 at every nonzero lag.

IID noise is stronger than white noise.

IID means the observations are independent and identically distributed. A useful way to remember it is:

> Every observation is a fresh draw from the same distribution.

White noise only rules out linear dependence through covariance. Independence rules out all dependence.

## Random walk: accumulated shocks

A random walk is built from white-noise shocks:

$$
X_t=X_{t-1}+\varepsilon_t.
$$

So white noise is the sequence of shocks, while the random walk is the accumulated total of those shocks.

A shock today changes the level today and remains embedded in future levels. This creates persistence and a stochastic trend.

The mean of the basic random walk can stay constant, but the variance grows over time:

$$
\operatorname{Var}(X_t)=t\sigma_\varepsilon^2.
$$

Its autocovariance also depends on calendar time:

$$
\operatorname{Cov}(X_t,X_{t-h})
=
(t-h)\sigma_\varepsilon^2.
$$

That violates weak stationarity.

## Components in observed time series

Real time series often contain several visually different components.

A common additive representation is

$$
X_t=T_t+S_t+R_t,
$$

where `T_t` is trend, `S_t` is seasonality and `R_t` is the remainder.

Trend is a long-run increase or decrease.

Seasonality is a repeating pattern with a fixed known period, such as 12 months or 4 quarters.

Cycles are also repeated up-and-down movements, but unlike seasonality they do not have a fixed period. Cyclic behavior can still be compatible with stationarity.

A multiplicative representation,

$$
X_t=T_tS_tR_t,
$$

is useful when fluctuations grow with the level of the series. Taking logs converts this into an additive form.

## Where non-stationarity can come from

Week 1 highlights several common sources of non-stationarity:

- deterministic trend;
- stochastic trend;
- seasonality;
- level-dependent variability.

A deterministic trend changes predictably with time.

A stochastic trend, such as a random walk, is driven by accumulated shocks.

Seasonality makes the expected level depend on where we are in the seasonal cycle.

Level-dependent variability can make the variance change as the series level changes.

These are the kinds of patterns we look for before applying stationary time-series models.

## Lag operator and differencing

The lag operator is compact notation for moving backward in time:

$$
LX_t=X_{t-1}.
$$

More generally,

$$
L^jX_t=X_{t-j}.
$$

The first difference is

$$
\Delta X_t=X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta X_t=(1-L)X_t.
$$

The key conceptual move is that differencing changes the object we model.

Instead of modeling the level `X_t`, we model how much it changed from the previous period.

For a random walk,

$$
X_t=X_{t-1}+\varepsilon_t,
$$

so

$$
\Delta X_t=\varepsilon_t.
$$

The level is non-stationary, while the first difference is stationary white noise.

Differencing also removes a deterministic linear trend in the sense that

$$
X_t=\beta_0+\beta_1t+\varepsilon_t
$$

becomes

$$
\Delta X_t=\beta_1+\Delta\varepsilon_t.
$$

The growing level is replaced by a constant increment.

## Week 2 begins: modeling stationary dynamics

Once a series is stationary, the next question is not just whether it is stable, but how values depend on the past.

This is where AR, MA and ARMA models enter.

An autoregressive model, or AR model, says that the current value depends on earlier values of the same series.

The simplest example is

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

The previous value carries forward through `phi`, while `epsilon_t` is the new shock arriving today.

Because `X_{t-1}` itself contains older shocks, an AR model can carry the influence of a shock far into the future. The effect may shrink over time, but it does not have to disappear after a fixed number of periods.

A moving-average model, or MA model, works differently. It models the current value directly using current and past shocks.

For example,

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1}.
$$

This MA(1) remembers today's shock and yesterday's shock directly, but no shock further back.

So the easiest distinction to remember is:

> AR remembers past values. MA remembers past shocks.

An ARMA model combines the two ideas. In ARMA(p,q), `p` counts the number of AR lags and `q` counts the number of MA shock lags.

## Lag polynomials, roots and stationarity

Lag-polynomial notation compresses an ARMA equation into

$$
\phi(L)X_t=\theta(L)\varepsilon_t.
$$

The AR polynomial `phi(L)` is the part that determines stationarity.

To test stationarity, replace `L` by a normal variable such as `z`, solve

$$
\phi(z)=0,
$$

and inspect the roots.

The rule is:

> Every AR root must lie outside the unit circle.

For an AR(1), this is equivalent to `|phi|<1`. For higher-order AR models, the individual coefficients themselves can be misleading, so the roots of the whole polynomial are what matter.

Complex roots are handled by measuring their distance from zero using the modulus

$$
|a+bi|=\sqrt{a^2+b^2}.
$$

## Why causality appears

Stationarity is about stable behavior over time. Causality asks a different but related question:

> Can today's value be generated using only shocks that have happened now or in the past?

A causal representation looks like

$$
X_t
=
\psi_0\varepsilon_t
+\psi_1\varepsilon_{t-1}
+\psi_2\varepsilon_{t-2}
+\cdots.
$$

There are no future shocks such as `epsilon_{t+1}`.

To get this representation, we invert the AR lag polynomial. The geometric-series rule makes the simple AR(1) case transparent:

$$
\frac{1}{1-\phi L}
=
1+\phi L+\phi^2L^2+\cdots
$$

when `|phi|<1`.

This turns the AR model into an MA(infinity) representation:

$$
X_t
=
\varepsilon_t
+\phi\varepsilon_{t-1}
+\phi^2\varepsilon_{t-2}
+\cdots.
$$

This reveals the old-shock story directly: an AR process can be viewed as the accumulation of infinitely many past shocks whose influence eventually dies away.

In the framework used in this course, the same AR-root condition that gives stationarity also gives causality. So once all AR roots are outside the unit circle, the process is stationary and causal.

The mathematics behind roots, complex numbers and geometric series is kept in the mathematics branch and linked from the detailed time-series notes.

## Statistical properties: what the stationary model looks like

Once a stationary ARMA model has been specified, we want to know what kind of behavior it implies.

The unconditional mean is the long-run center of the process. The conditional mean is different: it uses the information currently available and tells us the best expected next value.

A process can therefore have a long-run mean of 2 while today's conditional mean is 4.4 because the latest observation was unusually high. These statements are not contradictory. One describes the process overall; the other describes what we expect given the current situation.

This leads naturally to mean reversion. In a stable AR model, deviations from the long-run mean are carried forward only partially, so an unusually high or low observation tends to move back toward the normal level over time unless new shocks keep pushing it away.

The ACF then describes the memory pattern of the process.

For an AR(1), autocorrelation fades gradually. With a positive coefficient it decays smoothly; with a negative coefficient it alternates sign while shrinking.

For higher-order AR models, the ACF can oscillate around zero. Oscillation means that the autocorrelations can move from positive to negative and later back again while their overall magnitude becomes smaller.

MA models look different. Their ACF has a cutoff. An MA(1) can have autocorrelation at lag 1, but after lag 1 the theoretical ACF is zero. An MA(2) can have autocorrelation up to lag 2, but after lag 2 it is zero.

This difference between gradual AR decay and finite MA cutoff later becomes useful for model identification.

Conditional distributions also let us turn an AR model into probability statements. Once the past is observed, the model gives a conditional center for the next observation, and probabilities should be measured around that conditional center rather than around yesterday's observation alone.

## Invertibility: working backwards from observations to shocks

Causality focused on the AR side and asked whether current values can be built from current and past shocks.

Invertibility shifts attention to the MA side and asks the reverse question:

> Can the hidden shocks be recovered from current and past observed values?

For an MA model, this matters because different parameter values can sometimes generate exactly the same autocorrelation behavior. For an MA(1), for example, a coefficient of 0.5 and a coefficient of 2 produce the same lag-1 autocorrelation.

Without an extra restriction, we would have more than one parameterization describing the same observed dependence structure. That is an identification problem.

The invertibility condition solves it by selecting one standard representation. The mathematical rule mirrors the stationarity test:

> Every MA root must lie outside the unit circle.

For an MA(1), this reduces to `|theta|<1`.

There is a useful symmetry here:

```text
causality: shocks -> observed X values
invertibility: observed X values -> shocks
```

A causal AR process can be rewritten as an MA(infinity) process. An invertible MA process can be rewritten as an AR(infinity) process.

So Week 2 gives us two different kinds of "working backwards" with lag polynomials: invert the AR side to reveal old shocks inside the current value, and invert the MA side to recover shocks from observed values.

## Parameter estimation: the coefficients are not known in real data

Until now, equations have often been written as if values such as `phi=0.8` or `theta=0.5` were already given.

In real applications, we observe the data but do not know those coefficients. We therefore need to estimate them.

The lecture mentions Yule-Walker estimation, least squares for AR models, and maximum likelihood for ARMA models. Maximum likelihood receives most of the attention because it is the general approach.

The maximum-likelihood question is:

> Which parameter values make the data we actually observed most plausible under the model and the assumed error distribution?

Suppose two candidate parameter values imply very different residuals. One produces residuals close to zero; another repeatedly requires much larger errors. If the assumed error distribution is normal and centered at zero, the first set of residuals is more plausible, so that candidate parameter value receives a higher likelihood.

This is why maximum likelihood needs a full distributional assumption. White noise properties alone do not tell us the complete shape of the probability distribution.

Because time-series observations are dependent, we build the likelihood using conditional densities. In words, at every date we ask:

> Given what had already happened, how plausible is the value that happened next?

The likelihood combines those conditional plausibilities across the sample.

Taking the natural logarithm gives the log-likelihood. The log changes products into sums and makes the calculations easier, but it does not change which parameter values maximize the function.

For realistic ARMA models, the maximum is usually found numerically by software. The course does not require manually deriving every general ARMA conditional density.

## PACF: separating direct from indirect lag relationships

The ACF measures the overall relationship between observations separated by a certain number of periods.

The PACF asks a more focused question:

> Is there still a direct relationship between today's value and the value `h` periods ago after the intermediate lags have been controlled for?

This distinction is especially useful for AR models.

In an AR(1), today's value directly depends only on yesterday. Yet today's value can still be correlated with the value two or three periods ago because the dependence travels through yesterday.

The ACF sees those indirect relationships, so it gradually decays.

The PACF removes the effect of the intermediate observations. Once yesterday is controlled for, an AR(1) has no additional direct AR lag. Therefore its PACF cuts off after lag 1.

The general Week 2 pattern is:

```text
AR(p):   ACF decays or oscillates, PACF cuts off after p
MA(q):   ACF cuts off after q, PACF decays or oscillates
ARMA:    both ACF and PACF generally decay or oscillate
```

That gives a useful memory rule:

```text
PACF cutoff -> think AR order p
ACF cutoff  -> think MA order q
```

For a mixed ARMA model, both functions usually tail off, so the exact values of `p` and `q` are not identified by one clean cutoff. More formal model-selection methods come later in the course.

## The GDP-growth example brings Week 2 together

The lecture closes Week 2 by applying the whole workflow to GDP growth.

First, inspect the series.

Then inspect the ACF and PACF.

The PACF cuts off after lag 2, suggesting two autoregressive lags.

So the model is chosen as ARMA(2,0), which is simply an AR(2).

The parameters are then estimated with maximum likelihood.

This gives the practical Week 2 workflow:

```text
understand the series
-> specify stationary dynamics
-> use AR and MA structure
-> check stationarity / causality / invertibility
-> study statistical properties
-> inspect ACF and PACF
-> choose lag orders
-> estimate unknown parameters
```

## Week 3 begins: when the level is not stationary

Week 2 gave us a framework for stationary ARMA dynamics. Week 3 starts by asking what happens when the observed level does not satisfy stationarity.

A non-stationary series may have a changing mean, a changing autocovariance structure, seasonality, or variability that grows with the level.

The first clues come from the time-series plot and the ACF.

A stationary ACF usually falls toward zero relatively quickly. A non-stationary series often has an ACF that decays slowly because distant observations remain strongly related. Seasonality can create repeated ACF spikes at seasonal lags.

If variability increases with the level of the series, a logarithmic transformation can help stabilize the variance.

### Differencing changes levels into changes

The first difference is

$
\Delta X_t=X_t-X_{t-1}.
$

This changes the object we model. Instead of asking about the level, we ask how much the level changed since the previous period.

For a random walk,

$
X_t=X_{t-1}+\varepsilon_t,
$

so

$
\Delta X_t=\varepsilon_t.
$

The non-stationary level becomes stationary white noise after one difference.

Seasonality can be treated with a seasonal difference,

$
\Delta_sX_t=X_t-X_{t-s}.
$

For monthly data, the common yearly seasonal difference is

$
\Delta_{12}X_t=X_t-X_{t-12}.
$

If both ordinary trend and seasonality are present, the two difference operators can be combined.

### Integration order counts how much differencing is needed

The notation `I(d)` records the minimum number of ordinary differences required to obtain a stationary series.

```text
I(0) -> already stationary
I(1) -> first difference is stationary
I(2) -> second difference is stationary
```

The word "minimum" matters. Differencing a series that is already stationary is not harmless. Overdifferencing can introduce unnecessary dependence and moving-average structure into the errors and can make estimation less efficient.

### Unit roots explain why the random walk is non-stationary

Return to the AR(1):

$
X_t=\phi X_{t-1}+\varepsilon_t.
$

When `|phi|<1`, old shocks gradually lose their influence and the process is mean-reverting.

When

$
\phi=1,
$

the model becomes a random walk.

The AR polynomial is

$
1-\phi L.
$

The characteristic equation is

$
1-\phi z=0,
$

so

$
z=\frac{1}{\phi}.
$

For `phi=1`, the root is

$
z=1.
$

That is the basic unit-root case.

The root language gives an important distinction:

```text
|z| > 1 -> stationary
|z| = 1 -> unit-root non-stationary
|z| < 1 -> explosive non-stationary
```

So "does not have a unit root" is not enough to conclude stationarity. A root can lie inside the unit circle and still produce non-stationarity.

### Shock persistence is the main intuition

For a stationary AR(1), a shock is carried forward with powers such as

$
\phi,\phi^2,\phi^3,\ldots
$

and those effects shrink when `|phi|<1`.

For a unit-root process, the shock does not get multiplied by a coefficient smaller than one. It remains embedded in the level.

So the story is:

```text
stationary AR(1) -> shocks decay -> mean reversion
unit-root process -> shocks persist -> stochastic trend
```

### Dickey-Fuller rewrites the unit-root question

Starting from

$
X_t=\phi X_{t-1}+\varepsilon_t,
$

subtract `X_{t-1}`:

$
\Delta X_t
=
(\phi-1)X_{t-1}+\varepsilon_t.
$

The Week 3 slides define

$
\phi^*=\phi-1.
$

So

$
\Delta X_t
=
\phi^*X_{t-1}+\varepsilon_t.
$

A unit root means `phi=1`, therefore

$
\phi^*=0.
$

This turns the unit-root question into the null hypothesis

$
H_0:\phi^*=0.
$

The ordinary t-test distribution is not valid in the usual way under the unit-root null, so Dickey and Fuller derived a special limiting distribution for the test.

### ADF and KPSS start from opposite null hypotheses

The ADF test uses

$
H_0:\text{unit root}.
$

The KPSS test uses

$
H_0:\text{stationarity}.
$

That gives the memory rule:

```text
ADF:  small p-value -> reject unit root
KPSS: small p-value -> reject stationarity
```

The tests are complementary because they start from opposite assumptions.

### None, constant and trend change the stationary benchmark

The unit-root tests can include different deterministic components.

For ADF, the stationary alternative can be:

```text
none     -> stationary around zero
constant -> stationary around a non-zero mean
trend    -> stationary around a deterministic trend
```

For KPSS, those same descriptions belong to the null hypothesis.

A trend-stationary process is not weakly stationary in levels. Its mean may move predictably with time, but after the deterministic trend is removed, the remaining process is stationary.

That is different from a stochastic trend such as a random walk, where accumulated shocks move the level.

### Testing the order of integration

To determine `d`, begin with the level and then difference only when necessary.

With ADF:

```text
test X_t
-> if unit root is not rejected, test Delta X_t
-> continue until the unit-root null is rejected
-> number of differences = d
```

With KPSS:

```text
test X_t
-> if stationarity is rejected, test Delta X_t
-> continue until stationarity is not rejected
-> number of differences = d
```

So Week 3 has now connected the visual idea of a wandering series to a formal sequence:

```text
non-stationary level
-> unit root
-> differencing
-> integration order
-> ADF / KPSS testing
-> next: ARIMA
```

## ARIMA: ARMA after differencing

Once the integration order has been determined, ARIMA follows directly from Week 2. If

$
Y_t=\Delta^dX_t
$

is stationary, then model \(Y_t\) with ARMA:

$
\phi(L)Y_t=\theta(L)\varepsilon_t.
$

Substituting back gives

$
\boxed{\phi(L)\Delta^dX_t=\theta(L)\varepsilon_t.}
$

This is ARIMA(p,d,q). The orders mean:

~~~text
p = AR order in the stationary differenced process
d = number of ordinary differences
q = MA order in the stationary differenced process
~~~

The key sentence is:

> ARIMA(p,d,q) is ARMA(p,q) applied to the stationary series Delta^d X_t.

For example,

$
\Delta X_t=0.7\Delta X_{t-1}+\varepsilon_t
$

is ARIMA(1,1,0), while

$
\Delta X_t=\varepsilon_t+0.5\varepsilon_{t-1}
$

is ARIMA(0,1,1).

The integration order d is selected using the Week 3 unit-root and stationarity logic. Once the differenced series is stationary, p and q are selected from the ACF and PACF of that stationary transformed series, not from the original non-stationary level.

An intercept in the stationary differenced model can also imply a deterministic trend in the level. If d=1 and the mean of \(\Delta X_t\) is a non-zero constant, then the level changes by that amount on average each period and therefore has a linear trend.

## Seasonal ARIMA: two clocks at once

Seasonal data can have both ordinary dependence and seasonal dependence. With monthly data, April can depend on March, but it can also depend especially strongly on the previous April.

So two time scales can matter:

~~~text
ordinary lags:
1, 2, 3, ...

seasonal lags:
12, 24, 36, ...
~~~

The course writes the seasonal ARIMA model as

$
\boxed{\text{ARIMA}(p,d,q)\times(P,D,Q)_s}
$

with

$
\boxed{
\phi(L)\Phi(L^s)\Delta^d\Delta_s^D X_t
=
\theta(L)\Theta(L^s)\varepsilon_t.
}
$

The lowercase orders describe ordinary dynamics. The uppercase orders describe seasonal dynamics. The seasonal period s tells us how often the seasonal cycle repeats. For monthly yearly data, \(s=12\); for quarterly yearly data, \(s=4\).

The seasonal difference is

$
\Delta_sX_t=X_t-X_{t-s}.
$

For monthly data,

$
\Delta_{12}X_t=X_t-X_{t-12}.
$

If both one ordinary difference and one seasonal difference are used,

$
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13}.
$

The lag-13 term comes from the interaction

$
L\times L^{12}=L^{13}.
$

The same multiplicative interaction can create lag-13 AR or MA terms when ordinary and seasonal polynomials are multiplied.

An ordinary AR(1) acts at lag 1, while a seasonal AR(1) with monthly data acts at lag 12. An ordinary MA(1) uses the shock at lag 1, while a seasonal MA(1) uses the shock at lag 12.

### Seasonal ACF and PACF rules

The Week 2 cutoff rules still apply, but now at seasonal lags.

For a monthly seasonal AR(1):

~~~text
ACF  -> decays at 12, 24, 36, ...
PACF -> one significant seasonal spike at 12
~~~

For a monthly seasonal MA(1):

~~~text
ACF  -> significant seasonal spike at 12, then seasonal cutoff
PACF -> decays at 12, 24, 36, ...
~~~

The clean rules are easiest to see in pure seasonal AR or MA examples. A full mixed SARIMA model can look less tidy because ordinary and seasonal components interact.

## The airline model brings SARIMA together

The Week 3 lecture uses the Box-Jenkins airline model

$
\boxed{\text{ARIMA}(0,1,1)\times(0,1,1)_{12}.}
$

It has one ordinary difference, one seasonal difference, one ordinary MA(1), one seasonal MA(1), and no AR terms.

Therefore

$
\Delta\Delta_{12}X_t
=
(1+\theta L)(1+\Theta L^{12})\varepsilon_t.
$

Expanding gives

$
X_t-X_{t-1}-X_{t-12}+X_{t-13}
=
\varepsilon_t
+\theta\varepsilon_{t-1}
+\Theta\varepsilon_{t-12}
+\theta\Theta\varepsilon_{t-13}.
$

The lecture chooses this structure because the ACF of the ordinary-and-seasonally differenced series has important behavior around lag 1 and lag 12, suggesting ordinary MA(1) and seasonal MA(1) components.

## Maximum likelihood returns in Week 3

After the ARIMA or seasonal ARIMA order has been selected, the unknown coefficients still have to be estimated.

Week 3 uses maximum likelihood, just as Week 2 did for ARMA models. Model-order selection tells us which coefficients exist. Maximum likelihood estimates their numerical values.

For the airline model, the lecture reports

$
\hat\theta=-0.4018,
$

$
\hat\Theta=-0.5569,
$

and

$
\hat\sigma_\varepsilon^2=0.0013.
$

Using the slide sign convention,

$
\theta(L)=1+\theta L
$

and

$
\Theta(L^{12})=1+\Theta L^{12},
$

the fitted model becomes

$
\Delta\Delta_{12}X_t
=
(1-0.4018L)(1-0.5569L^{12})\varepsilon_t.
$

So

$
\Delta\Delta_{12}X_t
=
\varepsilon_t
-0.4018\varepsilon_{t-1}
-0.5569\varepsilon_{t-12}
+0.2238\varepsilon_{t-13}.
$

The lecture specifies maximum likelihood but does not name the numerical optimizer. In practice, software generally searches numerically for parameter values that maximize the log-likelihood.

## The NVIDIA example connects testing to integration

The Week 3 lecture revisits NVIDIA stock prices. The price series has a visible trend, so trend specifications are used in ADF and KPSS.

For the stock-price level, the lecture reports

$
p_{ADF}=1.0
$

and

$
p_{KPSS}=0.01.
$

The unit-root null is not rejected by ADF, while trend-stationarity is rejected by KPSS. The lecture therefore treats the stock-price level as unit-root non-stationary.

For NVIDIA returns, the lecture uses constant specifications and reports

$
p_{ADF}=0.0
$

and

$
p_{KPSS}=0.1.
$

ADF rejects the unit-root null and KPSS does not reject stationarity. The return series is therefore treated as stationary.

The practical conclusion is

$
\boxed{\text{NVIDIA stock price is }I(1).}
$

The level is non-stationary, while its first-difference-type return transformation is stationary.

This example reinforces an important point: a visible trend alone does not tell us whether the process is trend-stationary or unit-root non-stationary. The tests help distinguish the two cases.

## The story in one chain

```text
observations through time
-> stochastic process
-> mean and variance
-> autocovariance
-> weak stationarity
-> autocorrelation / ACF
-> white noise
-> IID as a stronger dependence assumption
-> random walk
-> trend / seasonality / cycles / changing variability
-> sources of non-stationarity
-> lag operator
-> differencing and transformations
-> stationary dynamics
-> AR: past values
-> MA: past shocks
-> ARMA: both mechanisms together
-> lag-polynomial notation
-> AR characteristic roots
-> roots outside unit circle
-> stationarity
-> invert the AR polynomial
-> MA(infinity) representation
-> current and past shocks only
-> causality
-> unconditional versus conditional behavior
-> mean reversion
-> AR ACF decays or oscillates
-> MA ACF cuts off
-> MA characteristic roots
-> invertibility
-> recover shocks from observed values
-> AR(infinity) representation
-> unknown parameters in real data
-> maximum likelihood
-> conditional likelihood
-> log-likelihood
-> ACF and PACF lag-order clues
-> choose p and q
-> estimate the final model
-> non-stationary levels
-> differencing and seasonal differencing
-> integration order I(d)
-> unit-root versus explosive non-stationarity
-> persistent versus decaying shocks
-> Dickey-Fuller transformation
-> phi* = phi - 1
-> ADF: H0 = unit root
-> KPSS: H0 = stationary
-> determine d by repeated testing
-> ARIMA(p,d,q)
-> ARMA on Delta^d X_t
-> choose p and q from the stationary transformed series
-> seasonal ARIMA (p,d,q) x (P,D,Q)_s
-> ordinary and seasonal lags
-> seasonal ACF/PACF cutoff rules
-> multiplicative interaction lags
-> airline model
-> maximum-likelihood parameter estimation
-> NVIDIA unit-root example
-> Week 3 exercises
```

## What comes next

Week 3 theory is now complete in these notes.

The chapter now covers non-stationarity, ordinary and seasonal differencing, order of integration, unit roots, overdifferencing, Dickey-Fuller and ADF logic, KPSS, ARIMA, seasonal ARIMA, seasonal ACF/PACF patterns, the airline model, the NVIDIA example, and maximum-likelihood estimation.

The next step is retrieval and problem solving: work through the Week 3 exercise-book questions, identify which ideas do not yet come out automatically, and then return to the detailed notes for targeted reinforcement.

## What to remember right now

Stationarity does not mean the series is constant.

Stationarity does not mean autocorrelation must be zero.

White noise is stationary and has zero autocorrelation at nonzero lags.

IID is stronger than white noise because independence is stronger than zero covariance.

A random walk accumulates shocks, so shocks have persistent effects on the level.

Trend and seasonality are common sources of non-stationarity.

Seasonality has a fixed known period; cycles do not.

The lag operator moves a variable backward in time.

Differencing changes levels into changes and can remove some forms of non-stationarity.

AR models use past values of the series.

MA models use current and past shocks.

ARMA models combine both mechanisms.

Stationarity and causality are determined by the AR roots in the Week 2 ARMA framework.

All AR roots must lie outside the unit circle.

A causal model can be written using only current and past shocks.

A stationary AR model can be rewritten as an MA(infinity) representation by inverting the AR lag polynomial.

The unconditional mean is the long-run center; the conditional mean uses current information.

Mean reversion means deviations tend to shrink back toward the long-run level in a stable process.

AR ACFs decay or oscillate; MA ACFs cut off after the MA order.

Invertibility is determined by the MA roots, which must also lie outside the unit circle.

Invertibility provides a unique MA representation and lets shocks be recovered from observed values.

Maximum likelihood chooses the parameter values that make the observed data most plausible under the assumed distribution.

Time-series likelihoods are built conditionally on the past because observations are dependent.

PACF isolates direct lag relationships and is especially useful for identifying AR order.

ACF cutoffs suggest MA order; PACF cutoffs suggest AR order.

## When you forget the mathematics

Start with this page. Once the story is back in your head, use the detailed notes:

- [Basic properties of time series](basic-properties.md)
- [White noise and IID noise](white-noise-and-iid.md)
- [Random walk](random-walk.md)
- [Time-series components and sources of non-stationarity](components-and-nonstationarity.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [AR, MA and ARMA models](arma-models.md)
- [Statistical properties of stationary ARMA models](statistical-properties.md)
- [Invertibility of MA models](invertibility.md)
- [Parameter estimation](parameter-estimation.md)
- [ACF, PACF and lag-order selection](acf-pacf-and-lag-order-selection.md)
- [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [Unit-root testing: ADF and KPSS](unit-root-testing.md)
- [ARIMA models](arima-models.md)
- [Seasonal ARIMA models](seasonal-arima-models.md)
- [Week 3 full review](week-3-review.md)
- [Plain-language time-series intuition](intuition/README.md)
- [Complex numbers, polynomials and roots](../../mathematics/complex-numbers-and-polynomials.md)
- [Geometric series](../../mathematics/geometric-series.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1, parts 2-4.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 1 lecture and exercise book.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, parts 1-5.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 pre-lecture / lecture.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 exercise book.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, parts 1-4.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 exercise book.
