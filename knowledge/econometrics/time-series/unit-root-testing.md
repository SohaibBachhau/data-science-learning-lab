# Unit-Root Testing: ADF and KPSS

Status: `developing`

## Central question

How can we statistically test whether a time series has a unit root, and how can ADF and KPSS be used to determine the order of integration?

## Why visual inspection is not enough

A time-series plot and ACF can suggest non-stationarity, but visual inspection is not a formal statistical test.

Week 3 therefore introduces two complementary tests:

- Augmented Dickey-Fuller (ADF);
- Kwiatkowski-Phillips-Schmidt-Shin (KPSS).

Their null hypotheses point in opposite directions.

## ADF and KPSS at a glance

### ADF

The ADF test uses

$$
H_0:\text{the series has a unit root}
$$

against a stationary alternative determined by the chosen deterministic specification.

A small p-value leads us to reject the unit-root null.

### KPSS

The KPSS test uses

$$
H_0:\text{the series is stationary}
$$

with the exact form of stationarity again depending on the deterministic specification.

A small p-value leads us to reject stationarity.

### Memory rule

```text
ADF:  H0 = unit root
KPSS: H0 = stationary
```

Because the nulls are opposite, the tests are complementary.

## Dickey-Fuller starting point

Begin with the AR(1) model

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

A unit root occurs when

$$
\phi=1.
$$

The course rewrites the model in first differences.

Subtract `X_{t-1}` from both sides:

$$
X_t-X_{t-1}
=
\phi X_{t-1}-X_{t-1}+\varepsilon_t.
$$

Therefore

$$
\Delta X_t
=
(\phi-1)X_{t-1}+\varepsilon_t.
$$

The slides define

$$
\boxed{\phi^*=\phi-1.}
$$

So the Dickey-Fuller form is

$$
\boxed{\Delta X_t=\phi^*X_{t-1}+\varepsilon_t.}
$$

Use `phi*` throughout these notes because that is the notation used in the course slides.

## The unit-root null in phi-star notation

Under the unit-root null,

$$
\phi=1.
$$

Then

$$
\phi^*=\phi-1=0.
$$

So testing for a unit root is equivalent to testing

$$
\boxed{H_0:\phi^*=0.}
$$

This is the core mathematical idea behind the Dickey-Fuller test.

## Why ordinary t critical values are not used

Under the unit-root null, the usual normal / t approximation for the estimator does not apply in the standard way.

Dickey and Fuller therefore derived a special limiting distribution for the unit-root test.

This is why software reports Dickey-Fuller / ADF critical values rather than treating the coefficient as an ordinary regression coefficient test.

## From DF to ADF

The basic Dickey-Fuller setup starts from the AR(1) structure.

The Augmented Dickey-Fuller test extends the idea so that the test can include additional autoregressive terms and different deterministic specifications.

For the ADF test, we therefore need to choose:

1. the deterministic specification;
2. the autoregressive lag order used in the test.

Software packages often provide a lag-length selection procedure.

## ADF deterministic specifications

The slides give three possibilities.

### 1. None

The alternative hypothesis is that the series is stationary with zero mean.

Conceptually, the test does not include a deterministic constant or trend.

A simple representation is

$$
\Delta X_t
=
\phi^*X_{t-1}
+\text{ADF lag terms}
+\varepsilon_t.
$$

The alternative allows the process to fluctuate around zero.

### 2. Constant

The alternative hypothesis is that the series is stationary with a non-zero mean.

Conceptually, the test includes a constant:

$$
\Delta X_t
=
\alpha
+\phi^*X_{t-1}
+\text{ADF lag terms}
+\varepsilon_t.
$$

This is appropriate when the stationary alternative is centered around a non-zero long-run level.

### 3. Trend

The alternative hypothesis is that the series is trend-stationary around a deterministic trend.

Conceptually, the test includes a constant and deterministic time trend:

$$
\Delta X_t
=
\alpha
+\beta t
+\phi^*X_{t-1}
+\text{ADF lag terms}
+\varepsilon_t.
$$

Under this alternative, the level of `X_t` need not be weakly stationary.

Instead, deviations from a deterministic trend are stationary.

## Important distinction: trend-stationary is not weakly stationary in levels

Suppose

$$
X_t=2+0.5t+u_t,
$$

where `u_t` is stationary.

Then

$$
E(X_t)=2+0.5t,
$$

so the mean changes over time.

Therefore `X_t` is not weakly stationary in levels.

But

$$
X_t-(2+0.5t)=u_t
$$

is stationary.

That is what **trend-stationary** means.

So when using the trend specification, do not say simply:

> "the alternative says X_t is stationary."

A more accurate statement is:

> "the alternative says X_t is stationary around a deterministic trend."

## What about Delta X_t in a trend-stationary process?

Using

$$
X_t=2+0.5t+u_t,
$$

we get

$$
\Delta X_t
=
[2+0.5t+u_t]
-
[2+0.5(t-1)+u_{t-1}],
$$

so

$$
\Delta X_t
=
0.5+u_t-u_{t-1}.
$$

Equivalently,

$$
\Delta X_t=0.5+\Delta u_t.
$$

This can be stationary even though `X_t` itself is not weakly stationary in levels.

The ADF regression uses `Delta X_t` on the left-hand side as part of the testing construction, but the test is still telling us about the nature of `X_t`.

## ADF p-value interpretation

Suppose the significance level is 5%.

If

$$
p<0.05,
$$

reject

$$
H_0:\phi^*=0.
$$

That means we reject the unit-root null.

The exact stationary conclusion depends on the deterministic specification.

If

$$
p>0.05,
$$

do not reject the unit-root null.

The careful wording is:

> We cannot reject the null hypothesis of a unit root.

Do not automatically say:

> We proved the series has a unit root.

Failing to reject is not the same as proving the null is true.

## ADF alternative should not be memorized as simply "no unit root"

A process can have no root exactly on the unit circle and still be non-stationary because it is explosive.

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

So when discussing the ADF test in this course, state the alternative using the specific stationarity form from the chosen deterministic specification.

## KPSS test

KPSS reverses the testing logic.

The null is stationarity.

This makes it useful as a complement to ADF.

## KPSS deterministic specifications

The slides again give three specifications.

### 1. None

Null hypothesis:

$$
H_0:\text{the series is stationary with zero mean.}
$$

### 2. Constant

Null hypothesis:

$$
H_0:\text{the series is stationary with a non-zero mean.}
$$

### 3. Trend

Null hypothesis:

$$
H_0:\text{the series is trend-stationary around a deterministic trend.}
$$

The deterministic components therefore change the exact stationarity statement being tested.

## KPSS p-value interpretation

At a 5% significance level:

If

$$
p<0.05,
$$

reject the stationarity null.

If

$$
p>0.05,
$$

do not reject the stationarity null.

This is the opposite direction from ADF.

## Reading ADF and KPSS together

A convenient conceptual table is:

| ADF result | KPSS result | Interpretation |
| --- | --- | --- |
| Reject unit root | Do not reject stationarity | Evidence points toward stationarity |
| Do not reject unit root | Reject stationarity | Evidence points toward non-stationarity |
| Same-direction evidence is not obtained | Same-direction evidence is not obtained | Investigate specification, lag choice, sample behavior and the series more carefully |

The course emphasizes that ADF and KPSS are complementary because their null hypotheses are opposite.

## Determining the order of integration with ADF

The order of integration is the minimum number of ordinary differences required to obtain stationarity.

### Step 1: test the level

Run the ADF test on

$$
X_t.
$$

If the unit-root null is rejected, then under the chosen specification the level is stationary and

$$
X_t\sim I(0).
$$

### Step 2: if needed, test the first difference

If the unit-root null cannot be rejected for `X_t`, calculate

$$
\Delta X_t
$$

and run the ADF test again.

If the unit-root null is rejected for `Delta X_t`, then

$$
X_t\sim I(1).
$$

### Step 3: continue only if necessary

If the first difference still appears to contain a unit root, calculate

$$
\Delta^2X_t
$$

and test again.

If the second difference is the first stationary transformation, then

$$
X_t\sim I(2).
$$

So the memory rule is:

```text
ADF:
difference until you REJECT the unit-root null
```

The number of differences required is `d`.

## Determining the order of integration with KPSS

The procedure is analogous, but the stopping rule is reversed.

### Step 1

Run KPSS on

$$
X_t.
$$

If stationarity is not rejected, the series can be treated as `I(0)` under that specification.

### Step 2

If stationarity is rejected, test

$$
\Delta X_t.
$$

If stationarity is now not rejected, then the level is `I(1)`.

### Step 3

Continue differencing only if necessary.

So the memory rule is:

```text
KPSS:
difference until you DO NOT REJECT the stationarity null
```

## A complete integration-order example

Suppose ADF gives:

| Series | ADF p-value |
| --- | ---: |
| `X_t` | 0.42 |
| `Delta X_t` | 0.01 |

At the 5% level:

For the level,

$$
0.42>0.05,
$$

so we do not reject the unit-root null.

For the first difference,

$$
0.01<0.05,
$$

so we reject the unit-root null.

Therefore exactly one difference was required:

$$
\boxed{X_t\sim I(1).}
$$

## Why the deterministic specification matters

The specification changes the stationary benchmark.

For example, a series with a strong deterministic trend may be stationary around that trend but not stationary around a constant.

If we omit the trend from the test, we are asking a different statistical question from the trend specification.

So before interpreting an ADF or KPSS result, always identify whether the test used:

- none;
- constant;
- trend.

## Lag order in the ADF test

The ADF test also requires choosing the order of autoregressive terms to include.

This matters because the series may have more dynamic dependence than the basic AR(1) Dickey-Fuller setup allows.

The Week 3 slides note that software often includes a lag-length selection procedure to choose an appropriate number of autoregressive terms.

At this stage, the main exam-level point is to remember that ADF specification has two parts:

```text
deterministic specification
+
autoregressive lag order
```

## Common mistakes

- Using `delta` for the transformed AR coefficient when the course slides use `phi*`.
- Forgetting that `phi*=phi-1`.
- Forgetting that a unit root corresponds to `phi*=0`.
- Saying ADF has `H0 = stationary`. It does not.
- Saying KPSS has `H0 = unit root`. It does not.
- Treating a large ADF p-value as proof of a unit root.
- Treating "no unit root" as automatically equivalent to stationarity.
- Forgetting that none / constant / trend change the exact stationary hypothesis.
- Calling a trend-stationary level series weakly stationary.
- Ignoring the ADF lag-order choice.
- Differencing more times than necessary when determining `d`.

## Retrieval questions

1. What is the null hypothesis of the ADF test?
2. What is the null hypothesis of the KPSS test?
3. Why are ADF and KPSS called complementary?
4. Starting from `X_t=phi X_{t-1}+epsilon_t`, derive the Dickey-Fuller regression.
5. What is `phi*`?
6. Why does a unit root imply `phi*=0`?
7. Why do we not use an ordinary t-test distribution for the unit-root test?
8. What are the three ADF deterministic specifications?
9. What is the alternative under the ADF constant specification?
10. What is the alternative under the ADF trend specification?
11. Why is trend-stationary not the same as weakly stationary in levels?
12. What are the three KPSS null specifications?
13. How do you interpret a small ADF p-value?
14. How do you interpret a small KPSS p-value?
15. How do you determine `d` using ADF?
16. How do you determine `d` using KPSS?
17. Why must the order of integration use the minimum number of differences?
18. What two choices must be made when specifying an ADF test?

## Related notes

- [Non-stationarity, unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [Lag operator and differencing](lag-operator-and-differencing.md)
- [AR, MA and ARMA models](arma-models.md)
- [The Story of Time Series Econometrics](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3, part 2: Unit-Root Testing.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 3 exercise book.
