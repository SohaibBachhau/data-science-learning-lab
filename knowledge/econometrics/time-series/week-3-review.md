# Week 3 Review: Non-Stationary Time Series Models

Status: `developing`

This page is a complete review of the Week 3 material covered in the videos and lecture.

It is deliberately more detailed than a normal summary. The goal is that this page can be used later as a stand-alone revision chapter before doing exercises.

## Week 3 in one sentence

Week 3 answers the question:

> What do we do when the time series is not stationary in levels?

The answer develops in stages:

```text
detect non-stationarity
-> understand why it is non-stationary
-> difference when appropriate
-> identify unit roots
-> determine order of integration
-> model the stationary transformed series with ARIMA
-> extend to seasonal ARIMA when seasonality matters
-> estimate the unknown parameters with maximum likelihood
```

## 1. Why Week 3 is needed

Week 2 focused on stationary ARMA models.

The problem is that many real economic and financial time series are non-stationary.

Examples can include:

- stock prices;
- GDP levels;
- price indices;
- airline-passenger totals;
- variables with deterministic trends;
- variables with stochastic trends;
- variables with seasonal patterns.

ARMA models should not simply be fitted to a non-stationary level series without first dealing with the source of non-stationarity.

## 2. Weak stationarity recap

A weakly stationary process has a time-invariant mean and an autocovariance function that depends only on the lag.

Informally:

> the basic statistical environment does not change merely because calendar time passes.

A non-stationary process violates at least one of these stability conditions.

## 3. Visual signs of non-stationarity

Two basic diagnostic tools are the time-series plot and the ACF.

### Time-series plot

Warning signs include:

- upward or downward trend;
- repeating seasonal pattern;
- variance increasing with the level;
- long wandering movements in the level.

A logarithmic transformation can help when the size of the fluctuations grows with the level.

### ACF

A stationary series often has an ACF that returns toward zero relatively quickly.

A strongly persistent non-stationary series can have an ACF that decays very slowly.

Seasonality can show up as repeated dependence at seasonal lags.

For monthly data, those seasonal lags are often

$$
12,24,36,\ldots.
$$

## 4. Ordinary differencing

The first difference is

$$
\Delta X_t
=
X_t-X_{t-1}.
$$

Using the lag operator,

$$
\Delta X_t
=
(1-L)X_t.
$$

The level `X_t` tells us where the process is.

The first difference `Delta X_t` tells us how much the process changed.

Differencing can remove some deterministic trends and unit-root stochastic trends.

## 5. Seasonal differencing

For seasonal period `s`,

$$
\Delta_sX_t
=
X_t-X_{t-s}.
$$

Using the lag operator,

$$
\Delta_s
=
1-L^s.
$$

For monthly data with yearly seasonality,

$$
\Delta_{12}X_t
=
X_t-X_{t-12}.
$$

This compares a month to the same month one year earlier.

## 6. Combining ordinary and seasonal differencing

If both ordinary trend non-stationarity and seasonal non-stationarity are present, we can use

$$
\Delta\Delta_sX_t.
$$

For monthly data,

$$
\Delta\Delta_{12}X_t.
$$

Expand:

$$
(1-L)(1-L^{12})X_t
=
(1-L-L^{12}+L^{13})X_t.
$$

Therefore

$$
\boxed{
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13}.
}
$$

The order of ordinary and seasonal differencing does not matter because the lag operators commute.

## 7. Order of integration

The order of integration tells us the minimum number of ordinary differences needed to make the series stationary.

We write

$$
X_t\sim I(d).
$$

### I(0)

The series is already stationary.

### I(1)

One difference is needed:

$$
X_t\sim I(1)
\quad\Rightarrow\quad
\Delta X_t\sim I(0).
$$

### I(2)

Two differences are needed:

$$
X_t\sim I(2)
\quad\Rightarrow\quad
\Delta^2X_t\sim I(0).
$$

The word **minimum** is essential.

## 8. Overdifferencing

Do not difference a stationary series simply to be safe.

Overdifferencing can:

- create unnecessary dependence;
- introduce moving-average structure;
- reduce estimation efficiency.

The target is the smallest differencing order that produces stationarity.

## 9. Unit roots

Consider the AR(1)

$$
X_t
=
\phi X_{t-1}
+
\varepsilon_t.
$$

The AR polynomial is

$$
1-\phi L.
$$

The characteristic equation is

$$
1-\phi z=0,
$$

so

$$
z=\frac{1}{\phi}.
$$

If

$$
\phi=1,
$$

then

$$
z=1
$$

and the model becomes

$$
X_t=X_{t-1}+\varepsilon_t.
$$

This is a random walk.

## 10. What "unit root" means

A unit root is a characteristic root on the unit circle:

$$
\boxed{|z|=1.}
$$

In the basic real-valued AR(1) unit-root case:

$$
z=1.
$$

Under the root convention used in this course:

$$
|z|>1
\Rightarrow
\text{stationary},
$$

$$
|z|=1
\Rightarrow
\text{unit-root non-stationary},
$$

$$
|z|<1
\Rightarrow
\text{explosive non-stationary}.
$$

This gives an important warning:

> "No unit root" is not identical to "stationary."

A root can lie inside the unit circle and be explosive.

## 11. Mean reversion versus persistent shocks

For a stationary AR(1) with

$$
|\phi|<1,
$$

a shock propagates through

$$
\phi,
\phi^2,
\phi^3,
\ldots
$$

and eventually dies out.

The process is mean-reverting.

For a random walk with

$$
\phi=1,
$$

the shock remains embedded in the future level.

This is why unit-root processes have persistent shocks and stochastic trends.

## 12. Why differencing removes a random-walk unit root

From

$$
X_t=X_{t-1}+\varepsilon_t,
$$

subtract `X_{t-1}`:

$$
X_t-X_{t-1}
=
\varepsilon_t.
$$

Therefore

$$
\boxed{
\Delta X_t=\varepsilon_t.
}
$$

The non-stationary level becomes stationary white noise.

This is the simplest example of an `I(1)` process.

## 13. Deterministic trend versus stochastic trend

A deterministic trend can be written as

$$
X_t
=
\beta_0+\beta_1t+u_t
$$

with stationary `u_t`.

The trend is predictable from time.

A stochastic trend, such as a random walk, is generated by accumulated random shocks.

Both can look like trending series, but they represent different forms of non-stationarity.

## 14. Trend-stationarity

Suppose

$$
X_t=2+0.5t+u_t
$$

with stationary `u_t`.

Then

$$
E(X_t)=2+0.5t,
$$

so the level is not weakly stationary.

However,

$$
X_t-(2+0.5t)=u_t
$$

is stationary.

Therefore the process is **trend-stationary**.

Trend-stationary does not mean weakly stationary in levels.

## 15. Dickey-Fuller transformation

Start with

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

Subtract `X_{t-1}`:

$$
\Delta X_t
=
(\phi-1)X_{t-1}
+
\varepsilon_t.
$$

The course slides define

$$
\boxed{
\phi^*=\phi-1.
}
$$

So

$$
\boxed{
\Delta X_t
=
\phi^*X_{t-1}
+
\varepsilon_t.
}
$$

Under the unit-root null,

$$
\phi=1,
$$

so

$$
\boxed{
\phi^*=0.
}
$$

This is why the Dickey-Fuller test can be expressed as testing

$$
H_0:\phi^*=0.
$$

## 16. Why special Dickey-Fuller critical values are needed

Under the unit-root null, the usual regression t-statistic does not have the standard t distribution.

Dickey and Fuller therefore derived a special asymptotic distribution.

So a unit-root test is not just an ordinary regression t-test.

## 17. ADF test

The Augmented Dickey-Fuller test uses

$$
\boxed{
H_0:\text{unit root}.
}
$$

A small p-value leads us to reject the unit-root null.

The exact stationary alternative depends on the deterministic specification.

## 18. ADF deterministic specifications

### None

Alternative:

> stationary around zero.

### Constant

Alternative:

> stationary around a non-zero mean.

### Trend

Alternative:

> trend-stationary around a deterministic trend.

So rejecting the unit-root null in an ADF test with trend does not mean the level has a constant mean.

It means the process is consistent with stationarity around a deterministic trend.

## 19. Why ADF is "augmented"

The basic Dickey-Fuller setup is built from an AR(1)-type representation.

The Augmented Dickey-Fuller test allows additional autoregressive lag terms.

This helps account for richer serial dependence in the data.

An ADF specification therefore involves:

```text
deterministic specification
+
autoregressive lag order
```

Software often includes a lag-selection procedure.

## 20. KPSS test

KPSS reverses the null hypothesis:

$$
\boxed{
H_0:\text{stationary}.
}
$$

This makes KPSS complementary to ADF.

## 21. KPSS deterministic specifications

The stationarity null can be specified as:

### None

Stationary around zero.

### Constant

Stationary around a non-zero mean.

### Trend

Trend-stationary around a deterministic trend.

The deterministic specification matters because it changes what kind of stationarity is being tested.

## 22. ADF and KPSS together

The easiest memory rule is:

```text
ADF:
H0 = unit root
small p-value -> reject unit root

KPSS:
H0 = stationary
small p-value -> reject stationarity
```

Typical consistent outcomes are:

| ADF | KPSS | Interpretation |
| --- | --- | --- |
| reject unit root | do not reject stationarity | evidence points toward stationarity |
| do not reject unit root | reject stationarity | evidence points toward non-stationarity |

If the two tests do not point cleanly in one direction, investigate the specification and the data more carefully.

## 23. Determining d with ADF

Start with the level `X_t`.

If the ADF test rejects the unit-root null:

$$
X_t\sim I(0).
$$

If not, test

$$
\Delta X_t.
$$

If the unit-root null is rejected there:

$$
X_t\sim I(1).
$$

Continue only if necessary.

Memory rule:

```text
ADF:
difference until you REJECT the unit-root null
```

## 24. Determining d with KPSS

Start with the level.

If KPSS does not reject stationarity:

$$
X_t\sim I(0)
$$

under that specification.

If stationarity is rejected, difference and test again.

Memory rule:

```text
KPSS:
difference until you DO NOT REJECT the stationarity null
```

## 25. NVIDIA empirical example

The Week 3 lecture uses NVIDIA stock prices and returns to connect the testing procedure to real data.

### Stock price

The stock-price series visibly trends.

The lecture therefore includes a trend in the ADF and KPSS specifications.

Reported p-values:

$$
p_{ADF}=1.0
$$

and

$$
p_{KPSS}=0.01.
$$

For ADF:

$$
1.0>0.05
$$

so the unit-root null is not rejected.

For KPSS with trend:

$$
0.01<0.05
$$

so trend-stationarity is rejected.

The lecture therefore treats the NVIDIA stock price as non-stationary with a unit root.

### Returns

For the return series, the lecture uses a constant rather than a trend.

Reported p-values:

$$
p_{ADF}=0.0
$$

and

$$
p_{KPSS}=0.1.
$$

ADF rejects the unit-root null.

KPSS does not reject stationarity at 5%.

So the returns are treated as stationary.

The lecture therefore concludes that the stock-price series is integrated of order one:

$$
\boxed{
X_t\sim I(1).
}
$$

This example also shows why a visible trend alone does not tell us whether the process is deterministically trend-stationary or unit-root non-stationary.

## 26. ARIMA

Once the integration order is known, we can model the stationary transformed series.

The ARIMA model is

$$
\boxed{
\phi(L)\Delta^dX_t
=
\theta(L)\varepsilon_t.
}
$$

This is an

$$
\boxed{
\text{ARIMA}(p,d,q)
}
$$

model.

Interpretation:

```text
p = AR order
d = ordinary differencing order
q = MA order
```

The most important conceptual statement is:

> ARIMA(p,d,q) is an ARMA(p,q) model applied to Delta^d X_t.

## 27. ARIMA examples

### ARIMA(1,1,0)

If

$$
\Delta X_t
=
0.7\Delta X_{t-1}
+
\varepsilon_t,
$$

then

$$
X_t
$$

follows ARIMA(1,1,0).

### ARIMA(0,1,1)

If

$$
\Delta X_t
=
\varepsilon_t
+
0.5\varepsilon_{t-1},
$$

then

$$
X_t
$$

follows ARIMA(0,1,1).

### ARIMA(1,2,1)

If

$$
\Delta^2X_t
=
0.6\Delta^2X_{t-1}
+
\varepsilon_t
+
0.3\varepsilon_{t-1},
$$

then

$$
X_t
$$

follows ARIMA(1,2,1).

## 28. ARIMA statistical properties

Define

$$
Y_t=\Delta^dX_t.
$$

Then `Y_t` is stationary.

So the statistical properties of the stationary ARMA model from Week 2 apply to `Y_t`.

This includes:

- AR stationarity conditions;
- ARMA means;
- ACF and PACF behavior;
- MA invertibility;
- maximum-likelihood estimation.

Do not automatically apply these stationary formulas to the non-stationary level.

## 29. Deterministic trend in ARIMA

An intercept in the stationary model for the differenced series can imply a deterministic trend in the level.

For a stationary ARMA(p,q) process with intercept `alpha`,

$$
\mu
=
\frac{\alpha}
{1-\sum_{i=1}^p\phi_i}.
$$

If

$$
d=1
$$

and

$$
E(\Delta X_t)=\mu,
$$

then the level changes by `mu` on average each period.

That implies a linear trend in the level.

## 30. Selecting p, d and q

The complete logic is:

```text
use ADF/KPSS and differencing -> choose d
use ACF/PACF of Delta^d X_t -> choose p and q
estimate coefficients -> maximum likelihood
```

Do not choose `p` and `q` from the ACF/PACF of the non-stationary level.

Use the stationary transformed series.

## 31. Seasonal ARIMA

Seasonal ARIMA extends ARIMA by adding seasonal dynamics.

The notation is

$$
\boxed{
\text{ARIMA}(p,d,q)\times(P,D,Q)_s.
}
$$

The lowercase orders describe ordinary dynamics.

The uppercase orders describe seasonal dynamics.

The general model is

$$
\boxed{
\phi(L)\Phi(L^s)
\Delta^d\Delta_s^D X_t
=
\theta(L)\Theta(L^s)\varepsilon_t.
}
$$

## 32. Meaning of the seasonal orders

```text
P = seasonal AR order
D = seasonal differencing order
Q = seasonal MA order
s = seasonal period
```

For monthly yearly seasonality,

$$
s=12.
$$

For quarterly yearly seasonality,

$$
s=4.
$$

## 33. Ordinary versus seasonal lags

With monthly data:

```text
ordinary lags:
1, 2, 3, ...

seasonal lags:
12, 24, 36, ...
```

Ordinary AR(1) uses `X_(t-1)`.

Seasonal AR(1) uses `X_(t-12)`.

Ordinary MA(1) uses `epsilon_(t-1)`.

Seasonal MA(1) uses `epsilon_(t-12)`.

## 34. Interaction lags

Because the non-seasonal and seasonal polynomials are multiplied, interaction lags can appear.

For example:

$$
L\times L^{12}
=
L^{13}.
$$

So a model containing ordinary lag 1 and seasonal lag 12 can produce a lag-13 term.

This does not mean the model separately chose a 13th-order component.

It is generated automatically by the multiplicative structure.

## 35. Detailed numerical SARIMA expansion

Consider

$$
\text{ARIMA}(1,1,1)\times(1,1,1)_{12}
$$

with

$$
\phi_1=0.4,
\qquad
\Phi_1=0.6,
\qquad
\theta_1=0.3,
\qquad
\Theta_1=0.5.
$$

Define

$$
Y_t
=
\Delta\Delta_{12}X_t.
$$

The model is

$$
(1-0.4L)(1-0.6L^{12})Y_t
=
(1+0.3L)(1+0.5L^{12})\varepsilon_t.
$$

AR side:

$$
(1-0.4L)(1-0.6L^{12})
=
1-0.4L-0.6L^{12}+0.24L^{13}.
$$

MA side:

$$
(1+0.3L)(1+0.5L^{12})
=
1+0.3L+0.5L^{12}+0.15L^{13}.
$$

Therefore

$$
\boxed{
Y_t
-0.4Y_{t-1}
-0.6Y_{t-12}
+0.24Y_{t-13}
=
\varepsilon_t
+0.3\varepsilon_{t-1}
+0.5\varepsilon_{t-12}
+0.15\varepsilon_{t-13}.
}
$$

## 36. Seasonal ACF/PACF cutoff rules

The Week 2 rules are reused at seasonal lags.

For monthly data:

$$
12,24,36,\ldots
$$

are the seasonal lags.

### Seasonal AR(1)

For

$$
\text{ARIMA}(0,0,0)\times(1,0,0)_{12},
$$

the slides state:

```text
ACF  -> decays at seasonal lags 12,24,36,...
PACF -> one significant seasonal spike at lag 12
```

### Seasonal MA(1)

For

$$
\text{ARIMA}(0,0,0)\times(0,0,1)_{12},
$$

the slides state:

```text
ACF  -> significant spike at lag 12 and then seasonal cutoff
PACF -> decays at seasonal lags 12,24,36,...
```

The memory rule is therefore the same as Week 2:

```text
PACF cutoff -> AR
ACF cutoff  -> MA
```

but apply it at seasonal lags when identifying seasonal structure.

## 37. Airline model

The famous Box-Jenkins airline model is

$$
\boxed{
\text{ARIMA}(0,1,1)\times(0,1,1)_{12}.
}
$$

It contains:

- one ordinary difference;
- one seasonal difference;
- one ordinary MA(1);
- one seasonal MA(1);
- no AR terms.

The lecture therefore describes it as a non-seasonal MA(1) combined with a seasonal MA(1) after differencing.

## 38. Airline model expansion

Because there are no AR terms,

$$
\phi(L)=1
$$

and

$$
\Phi(L^{12})=1.
$$

Therefore

$$
\Delta\Delta_{12}X_t
=
(1+\theta L)(1+\Theta L^{12})\varepsilon_t.
$$

Expand:

$$
\boxed{
X_t-X_{t-1}-X_{t-12}+X_{t-13}
=
\varepsilon_t
+\theta\varepsilon_{t-1}
+\Theta\varepsilon_{t-12}
+\theta\Theta\varepsilon_{t-13}.
}
$$

## 39. Why the airline model was selected

After the ordinary and seasonal differences are applied, the lecture examines the ACF and PACF.

The ACF is significant around lag 1 and lag 12.

This suggests:

$$
q=1
$$

for the ordinary MA part and

$$
Q=1
$$

for the seasonal MA part.

This gives

$$
(0,1,1)\times(0,1,1)_{12}.
$$

## 40. Parameter estimation

Once the model order has been chosen, estimate the unknown coefficients.

The Week 3 lecture uses maximum likelihood.

For the airline model, the reported estimates are

$$
\boxed{
\hat\theta=-0.4018
}
$$

$$
\boxed{
\hat\Theta=-0.5569
}
$$

and

$$
\boxed{
\hat\sigma_\varepsilon^2=0.0013.
}
$$

With the slide sign convention,

$$
\theta(L)=1+\theta L
$$

and

$$
\Theta(L^{12})=1+\Theta L^{12},
$$

the fitted model is

$$
\Delta\Delta_{12}X_t
=
(1-0.4018L)(1-0.5569L^{12})\varepsilon_t.
$$

Expand:

$$
\boxed{
\Delta\Delta_{12}X_t
=
\varepsilon_t
-0.4018\varepsilon_{t-1}
-0.5569\varepsilon_{t-12}
+0.2238\varepsilon_{t-13}.
}
$$

## 41. Fitted airline model in levels

Since

$$
\Delta\Delta_{12}X_t
=
X_t-X_{t-1}-X_{t-12}+X_{t-13},
$$

the fitted level equation becomes

$$
\boxed{
X_t
=
X_{t-1}
+
X_{t-12}
-
X_{t-13}
+
\varepsilon_t
-
0.4018\varepsilon_{t-1}
-
0.5569\varepsilon_{t-12}
+
0.2238\varepsilon_{t-13}.
}
$$

This equation brings together almost every Week 3 idea:

- ordinary differencing;
- seasonal differencing;
- lag operators;
- ordinary MA structure;
- seasonal MA structure;
- multiplicative interaction;
- estimated parameters.

## 42. Maximum likelihood versus the numerical algorithm

The statistical method is maximum likelihood.

It defines the parameter values we want:

> choose the parameters that make the observed data most likely under the model.

In practical software, a numerical optimization algorithm usually searches for those values.

The lecture itself specifies maximum likelihood but does not name a particular optimizer.

So keep the distinction:

```text
MLE -> statistical estimation principle
numerical optimizer -> computational method used to find the maximum
```

## 43. Complete Week 3 workflow

A useful master workflow is:

```text
1. Plot X_t.
2. Inspect the ACF.
3. Look for trend, seasonality and changing variance.
4. Transform variance if needed, for example with logs.
5. Decide which deterministic specification is plausible.
6. Use ADF and/or KPSS.
7. Determine the minimum ordinary integration order d.
8. Apply seasonal differencing if seasonal non-stationarity is present.
9. Verify the transformed series is stationary.
10. Inspect the ACF/PACF of the stationary transformed series.
11. Choose ordinary p and q.
12. Inspect seasonal lags to choose P and Q.
13. Specify ARIMA or seasonal ARIMA.
14. Estimate unknown coefficients with maximum likelihood.
15. Write out the fitted model and understand where each lag comes from.
16. Later weeks add forecasting, model selection and diagnostic checking.
```

## 44. High-value distinctions to remember

### Stationary versus unit-root versus explosive

$$
|z|>1
\Rightarrow
\text{stationary}
$$

$$
|z|=1
\Rightarrow
\text{unit-root non-stationary}
$$

$$
|z|<1
\Rightarrow
\text{explosive non-stationary}
$$

### ADF versus KPSS

```text
ADF  -> H0 = unit root
KPSS -> H0 = stationary
```

### Ordinary versus seasonal differencing

```text
Delta X_t     = X_t - X_(t-1)
Delta_s X_t   = X_t - X_(t-s)
```

### ARIMA versus SARIMA

```text
ARIMA(p,d,q)
-> ordinary dynamics

ARIMA(p,d,q) x (P,D,Q)_s
-> ordinary + seasonal dynamics
```

### Model selection versus estimation

```text
choose orders
-> p,d,q,P,D,Q

estimate coefficients
-> phi, theta, Phi, Theta, variance
```

## 45. Common Week 3 mistakes

- Saying a unit root means `|z|<=1`. It means `|z|=1`.
- Saying a process is stationary simply because it has no unit root.
- Confusing a root inside the unit circle with a unit root.
- Forgetting that a random walk is `I(1)`.
- Forgetting that `d` is the minimum number of ordinary differences.
- Overdifferencing an already stationary process.
- Saying ADF has stationarity as the null.
- Saying KPSS has a unit root as the null.
- Saying a large ADF p-value proves a unit root.
- Forgetting the deterministic specification in ADF/KPSS.
- Calling trend-stationary the same as weakly stationary in levels.
- Using `delta` instead of the slide notation `phi*`.
- Forgetting that `phi*=phi-1`.
- Forgetting that the unit-root null is `phi*=0`.
- Choosing ARIMA `p,q` from the ACF/PACF of a non-stationary level.
- Forgetting that SARIMA has separate ordinary and seasonal orders.
- Confusing `P` with `p` or `Q` with `q`.
- Forgetting the seasonal period `s`.
- Forgetting interaction lags such as 13 in monthly multiplicative SARIMA.
- Mixing up ACF and PACF cutoff rules.
- Thinking maximum likelihood chooses the model order.
- Forgetting the slide MA sign convention when plugging in negative parameter estimates.

## 46. Retrieval checklist

Before starting the Week 3 exercises, you should be able to answer these without looking:

1. What makes a process weakly stationary?
2. What visual clues suggest non-stationarity?
3. Why can a random walk be non-stationary even if its expected level is constant?
4. What is a unit root?
5. What is the difference between `|z|>1`, `|z|=1`, and `|z|<1`?
6. Why is "no unit root" not automatically equivalent to stationarity?
7. What does `I(1)` mean?
8. Why is overdifferencing undesirable?
9. What is `phi*` in the Dickey-Fuller transformation?
10. What are the ADF and KPSS null hypotheses?
11. What do none, constant, and trend mean in ADF/KPSS?
12. How do you determine `d` with ADF?
13. How do you determine `d` with KPSS?
14. What does ARIMA(p,d,q) mean?
15. Which series should be used for ACF/PACF identification after differencing?
16. What does each symbol in `ARIMA(p,d,q)x(P,D,Q)_s` mean?
17. Expand `Delta Delta_12 X_t`.
18. Why can lag 13 appear in monthly SARIMA?
19. What are the seasonal AR(1) and seasonal MA(1) ACF/PACF patterns?
20. Write and expand the airline model.
21. What are the fitted airline-model estimates from the lecture?
22. What is the difference between model-order selection and parameter estimation?
23. What does maximum likelihood do?
24. Why is a numerical optimizer typically needed in practice?

## Related notes

- [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [Unit-root testing: ADF and KPSS](unit-root-testing.md)
- [ARIMA models](arima-models.md)
- [Seasonal ARIMA models](seasonal-arima-models.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [ACF, PACF and lag-order selection](acf-pacf-and-lag-order-selection.md)
- [The Story of Time Series Econometrics](story.md)
- [Plain-language intuition](intuition/README.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 1: Non-stationarity, Unit-Roots, and Differencing.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 2: Unit-Root Testing.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 3: Autoregressive Integrated Moving Average (ARIMA) Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 4: Seasonal ARIMA Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 lecture: Non-Stationary Time Series Models.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 exercise book.
